---
title: "{{title}}"
date:
  "{ date }":
tags:
  - tech-note
  - draft
status: In Progress
topic:
---

# {{title}}

> [!info]- 1. Bối cảnh & Hiện trạng (The Context)
> - **Mục tiêu lúc đó là gì?** (Ví dụ: Chuyển đổi kiến trúc, thiết kế tính năng mới...)
> - **Hệ thống/Công cụ đang sử dụng?** (Ngôn ngữ, framework, database, hardware...)
> - **Điều kiện kích hoạt?** (Lỗi/tính năng xảy ra khi nào?)

(Viết bối cảnh của bạn ở đây...)

---

> [!bug]- 2. "Điểm nổ" & Nỗi đau (The Problem)
> - **Triệu chứng bề mặt:** Chuyện gì đã xảy ra? (Log lỗi, màn hình crash, thông số bất thường...)
> - **Mô tả kỹ thuật:** Vấn đề logic nằm ở đâu? 
> - **Hậu quả:** Tác động đến user hoặc hệ thống như thế nào?

(Mô tả vấn đề của bạn ở đây...)

---

> [!search]- 3. Hành trình điều tra (The Investigation)
> - **Manh mối đầu tiên:** Đã check log ở đâu, dùng tool gì để soi?
> - **Giả thuyết sai lầm:** (Tùy chọn) Những hướng đi ban đầu tưởng đúng nhưng lại sai.
> - **Nguyên nhân gốc rễ (Root Cause):** Lời giải thích kỹ thuật cho việc tại sao lỗi lại xảy ra.

(Ghi lại quá trình debug và nguyên nhân gốc rễ...)

---

> [!danger]- 4. Bàn cân Giải pháp (The Trade-offs)
> - **Giải pháp 1:** Ưu điểm / Nhược điểm.
> - **Giải pháp 2:** Ưu điểm / Nhược điểm.
> - **Quyết định:** Đặt lên bàn cân về độ phức tạp, performance, chi phí bảo trì và chốt phương án.

(Phân tích các hướng giải quyết...)

---

> [!check]- 5. Triển khai & Kết quả (The Execution)
> - **Code/Config cốt lõi:** (Chỉ dán những đoạn code quan trọng nhất, logic chính)
> - **Kết quả đo lường:** So sánh Before - After (Latency, tính chính xác, memory...).

(Chèn code snippet và kết quả vào đây...)
```java
// Ví dụ chèn code