
#include "DHT.h"

  

// ==========================================

// ĐỊNH NGHĨA CHÂN & CẤU HÌNH

// ==========================================

const int DHTPIN = 4;      

const int DHTTYPE = DHT11;  

const int IR_PIN = 22;      

const int LED_PIN = 18;    

const int RELAY_PIN = 14;  

const int BUTTON_PIN = 25; // Chân cho nút bấm cơ (Sử dụng INPUT_PULLUP)

  

const float TEMP_THRESHOLD = 29.0;

const bool RELAY_ACTIVE_LOW = false;

  

DHT dht(DHTPIN, DHTTYPE);

  

// ==========================================

// BIẾN TOÀN CỤC CHIA SẺ GIỮA CÁC TASK

// ==========================================

volatile float currentTemp = 0.0;

volatile bool isManualMode = false; // Trạng thái: false = AUTO, true = MANUAL

  

TaskHandle_t TaskDHT_Handle;

TaskHandle_t TaskLogic_Handle;

  

// Khai báo trước hàm để biên dịch không lỗi

void controlFan(bool state);

void TaskReadDHT(void * pvParameters);

void TaskControlLogic(void * pvParameters);

  

void setup() {

  Serial.begin(115200);

  dht.begin();

  pinMode(IR_PIN, INPUT);

  pinMode(LED_PIN, OUTPUT);

  pinMode(RELAY_PIN, OUTPUT);

  pinMode(BUTTON_PIN, INPUT_PULLUP); // Bật điện trở kéo lên bên trong cho nút nhấn

  controlFan(false); // Khởi động mặc định tắt quạt

  Serial.println("==========================================");

  Serial.println("Hệ thống khởi động với FreeRTOS...");

  Serial.println("Chế độ mặc định: AUTO");

  Serial.println("==========================================");

  

  // --- TẠO TASK 1: ĐỌC NHIỆT ĐỘ ---

  xTaskCreatePinnedToCore(

    TaskReadDHT,      

    "Task_DHT11",    

    2048,            

    NULL,            

    1,                

    &TaskDHT_Handle,  

    1                

  );

  

  // --- TẠO TASK 2: XỬ LÝ LOGIC & ĐIỀU KHIỂN ---

  xTaskCreatePinnedToCore(

    TaskControlLogic,

    "Task_Logic",    

    2048,            

    NULL,            

    2,                

    &TaskLogic_Handle,

    1                

  );

}

  

void loop() {

  vTaskDelete(NULL); // Xóa hàm loop để giải phóng tài nguyên cho FreeRTOS

}

  

// ==========================================

// ĐỊNH NGHĨA CÁC TASK

// ==========================================

  

// TASK 1: Chuyên đọc DHT11 (Chạy chậm mỗi 2s)

void TaskReadDHT(void * pvParameters) {

  for(;;) {

    float t = dht.readTemperature();

    if (!isnan(t)) {

      currentTemp = t;

      Serial.printf("[DHT11] Nhiệt độ hiện tại: %.1f *C\n", currentTemp);

    } else {

      Serial.println("[Lỗi] Không đọc được DHT11!");

    }

    vTaskDelay(2000 / portTICK_PERIOD_MS);

  }

}

  

// TASK 2: Chuyên quét Nút, Cảm biến cửa và xử lý logic (Chạy nhanh 50ms)

void TaskControlLogic(void * pvParameters) {

  static int lastDoorState = -1;

  static bool lastFanState = false;

  static int lastButtonState = HIGH; // Mặc định do INPUT_PULLUP là HIGH

  

  for(;;) {

    // --- 1. ĐỌC TRẠNG THÁI CẢM BIẾN & NÚT BẤM ---

    int doorState = digitalRead(IR_PIN);

    int currentButtonState = digitalRead(BUTTON_PIN);

    // In trạng thái cửa nếu có thay đổi

    if (doorState != lastDoorState) {

      if (doorState == HIGH) {

        Serial.println("[IR Sensor] Cửa đang MỞ!");

      } else {

        Serial.println("[IR Sensor] Cửa đã ĐÓNG!");

      }

      lastDoorState = doorState;

    }

  

    // Xử lý sự kiện nhấn nút (Từ HIGH xuống LOW)

    if (lastButtonState == HIGH && currentButtonState == LOW) {

      isManualMode = !isManualMode; // Đảo trạng thái chế độ

      Serial.println("\n------------------------------------------");

      Serial.print(">>> ĐÃ CHUYỂN CHẾ ĐỘ SANG: ");

      Serial.println(isManualMode ? "MANUAL (Ép quạt chạy)" : "AUTO (Theo nhiệt độ)");

      Serial.println("------------------------------------------\n");

    }

    lastButtonState = currentButtonState;

    // --- 2. XỬ LÝ LOGIC ĐIỀU KHIỂN ---

    if (isManualMode) {

      // THƯỜNG TRƯỜNG HỢP A: CHẾ ĐỘ MANUAL (Ưu tiên tuyệt đối)

      digitalWrite(LED_PIN, LOW); // Tắt đèn cảnh báo cửa

      if (lastFanState == false) {

         Serial.println("[Manual] Đang BẬT QUẠT (Bỏ qua cảm biến)");

         lastFanState = true;

      }

      controlFan(true);

    } else {

      // THƯỜNG TRƯỜNG HỢP B: CHẾ ĐỘ AUTO (Kiểm soát bởi cửa và nhiệt độ)

      if (doorState == HIGH) {

        // CỬA MỞ -> Ngắt quạt an toàn

        digitalWrite(LED_PIN, HIGH);

        controlFan(false);

        if (lastFanState == true) {

            Serial.println("[Auto] Tủ mở -> TẮT QUẠT khẩn cấp");

            lastFanState = false;

        }

      }

      else {

        // CỬA ĐÓNG -> Xét theo nhiệt độ

        digitalWrite(LED_PIN, LOW);

        if (currentTemp < TEMP_THRESHOLD) {

          if (lastFanState == true) {

             Serial.println("[Auto] Nhiệt độ ổn định -> TẮT QUẠT");

             lastFanState = false;

          }

          controlFan(false);

        } else {

          if (lastFanState == false) {

             Serial.println("[Auto] Nhiệt độ vượt ngưỡng -> BẬT QUẠT");

             lastFanState = true;

          }

          controlFan(true);  

        }

      }

    }

    // Delay 50ms đóng vai trò chống dội phím (debounce) hoàn hảo cho nút nhấn

    vTaskDelay(50 / portTICK_PERIOD_MS);

  }

}

  

// Hàm điều khiển Relay

void controlFan(bool state) {

  if (state) {

    digitalWrite(RELAY_PIN, RELAY_ACTIVE_LOW ? LOW : HIGH);

  } else {

    digitalWrite(RELAY_PIN, RELAY_ACTIVE_LOW ? HIGH : LOW);

  }

}