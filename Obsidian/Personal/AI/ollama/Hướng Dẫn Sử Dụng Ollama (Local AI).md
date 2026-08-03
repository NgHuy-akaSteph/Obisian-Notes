Ollama hoạt động chủ yếu qua giao diện dòng lệnh (Terminal/Command Prompt). Dưới đây là luồng làm việc cơ bản từ lúc tải mô hình đến khi tích hợp vào code.

## 1. Quản lý Mô hình (Models)

Giống như Docker Hub, Ollama có một thư viện các mô hình (Ollama Library). Bạn có thể lên trang `ollama.com/library` để tìm tên model.

- **Tải và chạy ngay một model:**
    
    ```
    ollama run qwen2.5:7b
    ```
    
    _Lệnh này sẽ tự động tải model về (nếu chưa có) và mở ngay giao diện chat trên Terminal._
    
- **Chỉ tải model (không chạy ngay):** (Rất hữu ích để tải trước các model nhúng - embedding cho RAG)
    
    ```
    ollama pull nomic-embed-text
    ```
    
- **Xem danh sách các model đang có trên máy:**
    
    ```
    ollama list
    ```
    
- **Xóa một model cho nhẹ ổ cứng:**
    
    ```
    ollama rm qwen2.5:7b
    ```
    

## 2. Tương tác trực tiếp trên Terminal

Khi bạn dùng lệnh `ollama run <tên-model>`, một dấu nhắc `>>>` sẽ hiện ra. Bạn có thể chat trực tiếp với AI tại đây.

- Để gửi tin nhắn: Gõ nội dung và nhấn Enter.
    
- Để dán văn bản dài (multiline): Bọc văn bản trong `"""` (ba dấu nháy kép).
    
- Để thoát khỏi chat: Gõ `/bye` hoặc nhấn `Ctrl + D`.
    

## 3. Gọi qua API (Dành cho code Backend/RAG)

Đây là phần quan trọng nhất cho dự án của bạn. Ngay khi phần mềm Ollama được bật (hoặc chạy lệnh `ollama serve`), nó sẽ mở một máy chủ ngầm tại cổng **`11434`**.

Bạn có thể dùng bất kỳ ngôn ngữ nào để gọi API này. Dưới đây là ví dụ gọi bằng `cURL`:

**Tạo văn bản (Chat/RAG text generation):**

```
curl http://localhost:11434/api/generate -d '{
  "model": "qwen2.5:7b",
  "prompt": "Tóm tắt ngắn gọn: Công nghệ RAG là gì?",
  "stream": false
}'
```

**Tạo Vector (Embedding cho RAG):**

```
curl http://localhost:11434/api/embeddings -d '{
  "model": "nomic-embed-text",
  "prompt": "Văn bản cần chuyển thành vector để lưu vào database"
}'
```

## 4. Tùy chỉnh Model với Modelfile (Nâng cao)

Khi làm OCR/Trích xuất dữ liệu, bạn muốn AI luôn trả lời theo một định dạng nhất định (ví dụ: JSON) và đóng vai chuyên gia. Bạn có thể tạo một file tên là `Modelfile` (không có đuôi file):

```
# Nội dung file Modelfile
FROM qwen2.5:7b

# Thiết lập nhiệt độ (0 = trả lời chính xác, ít sáng tạo; 1 = sáng tạo)
PARAMETER temperature 0

# Cài đặt lời nhắc hệ thống mặc định
SYSTEM """
Bạn là một hệ thống trích xuất dữ liệu OCR. 
Đầu vào của bạn là văn bản thô. 
Nhiệm vụ của bạn là bóc tách Tên và Số điện thoại, trả về định dạng JSON.
"""
```

Sau đó, mở terminal tại thư mục chứa file đó và chạy lệnh build:

```
ollama create my-ocr-model -f ./Modelfile
```

Giờ đây, bạn có một model nội bộ tên là `my-ocr-model` chuyên dùng để bóc tách dữ liệu!