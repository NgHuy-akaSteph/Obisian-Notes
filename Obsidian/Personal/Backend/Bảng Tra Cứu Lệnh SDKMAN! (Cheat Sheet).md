**SDKMAN!** (Software Development Kit Manager) là công cụ quản lý nhiều phiên bản SDK (như Java, Maven, Gradle, Groovy, Spring Boot, v.v.) trên hệ điều hành Unix/Linux/macOS và WSL (Windows).

---

## 1. Tra cứu & Hiển thị Trạng thái

| Nhóm chức năng | Lệnh | Mô tả chi tiết | Ví dụ minh họa |
| :--- | :--- | :--- | :--- |
| **Trợ giúp** | `sdk help` | Hiển thị bảng hướng dẫn và danh sách lệnh cơ bản. | `sdk help` |
| **Danh sách SDK** | `sdk list` | Liệt kê tất cả các công cụ/ngôn ngữ được SDKMAN hỗ trợ. | `sdk list` |
| **Danh sách phiên bản** | `sdk list <candidate>` | Liệt kê toàn bộ phiên bản khả dụng và đã cài của một SDK. | `sdk list java`<br>`sdk list maven` |
| **Phiên bản hiện tại** | `sdk current` | Hiển thị tất cả SDK và phiên bản đang kích hoạt trong hệ thống. | `sdk current` |
| **Phiên bản cụ thể** | `sdk current <candidate>` | Kiểm tra phiên bản đang dùng của một SDK cụ thể. | `sdk current java` |
| **Phiên bản SDKMAN** | `sdk version` | Hiển thị phiên bản của chính công cụ SDKMAN. | `sdk version` |

---

## 2. Cài đặt & Gỡ bỏ SDK

| Thao tác | Lệnh | Mô tả chi tiết | Ví dụ minh họa |
| :--- | :--- | :--- | :--- |
| **Cài bản mới nhất** | `sdk install <candidate>` | Cài đặt phiên bản ổn định (stable) mới nhất. | `sdk install gradle` |
| **Cài bản cụ thể** | `sdk install <candidate> <version>` | Cài đặt chính xác một phiên bản chỉ định. | `sdk install java 17.0.8-tem`<br>`sdk install maven 3.9.4` |
| **Cài bản Local** | `sdk install <candidate> <version> <path>` | Liên kết một bản SDK đã có sẵn trên máy vào SDKMAN. | `sdk install java custom-17 /path/to/jdk` |
| **Gỡ cài đặt** | `sdk uninstall <candidate> <version>` | Xóa một phiên bản SDK cụ thể khỏi hệ thống. | `sdk uninstall java 11.0.20-tem` |

---

## 3. Chuyển đổi Phiên bản & Quản lý Dự án

| Mục đích | Lệnh | Phạm vi tác dụng | Ví dụ minh họa |
| :--- | :--- | :--- | :--- |
| **Chuyển tạm thời** | `sdk use <candidate> <version>` | Chỉ áp dụng cho **Terminal Session hiện tại** (đóng đi mở lại sẽ mất). | `sdk use java 11.0.20-tem` |
| **Đặt mặc định** | `sdk default <candidate> <version>` | Áp dụng cho **Toàn hệ thống** (Global) mỗi khi mở terminal mới. | `sdk default java 17.0.8-tem` |
| **Tạo cấu hình dự án** | `sdk env init` | Tạo file `.sdkmanrc` tại thư mục hiện tại để lưu cấu hình SDK. | `sdk env init` |
| **Tải cấu hình dự án** | `sdk env` | Tự động chuyển SDK sang đúng phiên bản ghi trong `.sdkmanrc`. | `sdk env` |
| **Tự chuyển môi trường** | `sdk env install` | Cài đặt các SDK còn thiếu được khai báo trong `.sdkmanrc`. | `sdk env install` |

---

## 4. Nâng cấp & Bảo trì Hệ thống

| Lệnh | Mục đích | Chi tiết |
| :--- | :--- | :--- |
| `sdk update` | Cập nhật danh sách SDK | Đồng bộ danh sách các phiên bản SDK mới nhất từ máy chủ SDKMAN. |
| `sdk upgrade` | Kiểm tra bản cập nhật | Liệt kê các SDK trên máy bạn đã có phiên bản mới hơn. |
| `sdk upgrade <candidate>` | Nâng cấp SDK cụ thể | Cập nhật SDK chỉ định lên phiên bản mới nhất. |
| `sdk selfupdate` | Cập nhật SDKMAN | Cập nhật chính công cụ SDKMAN lên bản mới nhất. |
| `sdk selfupdate force` | Ép buộc cập nhật | Cài lại/cập nhật đè SDKMAN khi gặp lỗi. |
| `sdk offline [enable\|disable]` | Chế độ Ngoại tuyến | Tắt/Bật kết nối mạng cho SDKMAN (dùng khi không có internet). |

---

## 5. Dọn dẹp Dung lượng (Cleanup Commands)

| Lệnh | Công dụng |
| :--- | :--- |
| `sdk flush archives` | Xóa các file `.zip` / `.tar.gz` đã tải về trong quá trình cài đặt. |
| `sdk flush temp` | Dọn dẹp các thư mục tạm thời tạo ra bởi SDKMAN. |
| `sdk flush broadcast` | Xóa bộ nhớ đệm tin nhắn/thông báo từ hệ thống SDKMAN. |

---

## 💡 Quy trình làm việc thực tế dành cho Lập trình viên

```bash
# 1. Tìm bản Java Temurin mong muốn
sdk list java

# 2. Cài đặt Java 17 Temurin
sdk install java 17.0.8-tem

# 3. Đặt làm mặc định cho máy
sdk default java 17.0.8-tem

# 4. Khi vào dự án cũ cần Java 11
cd /path/to/legacy-project
sdk use java 11.0.20-tem

# 5. Lưu lại cấu hình cho dự án cũ
sdk env init
# (Mỗi lần quay lại dự án chỉ cần gõ: sdk env)
```