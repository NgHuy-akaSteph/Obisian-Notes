1. DHT11
```
#include "DHT.h"

  

// Định nghĩa chân tín hiệu D4 (GPIO 4) trên ESP32

#define DHTPIN 4    

  

// Chọn loại cảm biến là DHT11

#define DHTTYPE DHT11  

  

// Khởi tạo đối tượng dht

DHT dht(DHTPIN, DHTTYPE);

  

void setup() {

  // Khởi tạo giao tiếp Serial ở tốc độ 115200 baud (thường dùng cho ESP32)

  Serial.begin(115200);

  Serial.println(F("Đang khởi động bài test DHT11!"));

  

  // Bắt đầu đọc cảm biến

  dht.begin();

}

  

void loop() {

  // Đợi ít nhất 2 giây giữa các lần đọc (Cảm biến DHT11 đọc khá chậm)

  delay(2000);

  

  // Đọc độ ẩm (%)

  float h = dht.readHumidity();

  // Đọc nhiệt độ theo độ C (Celsius)

  float t = dht.readTemperature();
  

  // Kiểm tra xem có lỗi trong quá trình đọc không (NaN = Not a Number)

  if (isnan(h) || isnan(t) || isnan(f)) {

    Serial.println(F("Lỗi: Không thể đọc dữ liệu từ cảm biến DHT!"));

    return;

  }

  

  // Tính toán chỉ số cảm nhận nhiệt (Heat Index)

  float hif = dht.computeHeatIndex(f, h);

  float hic = dht.computeHeatIndex(t, h, false);

  

  // In kết quả ra Serial Monitor

  Serial.print(F("Độ ẩm: "));

  Serial.print(h);

  Serial.print(F("%  |  Nhiệt độ: "));

  Serial.print(t);

  Serial.print(F("°C "));
}
```
2. IR obstance sensor
```

```