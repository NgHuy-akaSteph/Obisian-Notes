## 1. Cấp độ Mầm non (Các thao tác sinh tồn cơ bản)
*Dành cho thao tác gõ code, sửa xóa và di chuyển khoảng cách gần.*

| Phím gõ | Chế độ | Chức năng | Nguồn gốc |
| :--- | :---: | :--- | :--- |
| `i` | Normal | Chuyển sang Insert mode (Bắt đầu gõ) | Vim gốc |
| `jk` hoặc `kj` | Insert | Thoát ra Normal mode (Nhanh hơn bấm Esc) | **Custom** |
| `h` `j` `k` `l` | Normal | Di chuyển Trái / Xuống / Lên / Phải | Vim gốc |
| `u` | Normal | Undo (Hoàn tác) | Vim gốc |
| `<C-r>` | Normal | Redo (Làm lại) | Vim gốc |
| `<C-s>` | All | Lưu tất cả file (Save All) | **Custom** |
| `<leader>qq`| Normal | Thoát hẳn IDE (Quit) | **Custom** |

## 2. Cấp độ Cơ bản (Chỉnh sửa & Copy/Paste nhanh)
*Cắt, dán và thao tác với văn bản mà không cần dùng chuột.*

| Phím gõ | Chế độ | Chức năng | Nguồn gốc |
| :--- | :---: | :--- | :--- |
| `yy` | Normal | Copy (Yank) toàn bộ dòng hiện tại | Vim gốc |
| `yw` | Normal | Copy từ vị trí con trỏ đến hết từ | Vim gốc |
| `Y` | Normal | Copy từ vị trí con trỏ đến **cuối dòng** | **Custom** |
| `p` / `P` | Normal | Paste (Dán) đằng sau / đằng trước con trỏ | Vim gốc |
| `p` | Visual | Paste đè lên đoạn text được bôi đen (**Không làm mất clipboard**) | **Custom** |
| `dd` | Normal | Cắt / Xóa toàn bộ dòng hiện tại | Vim gốc |
| `dw` / `cw` | Normal | Xóa từ (c: xóa xong tự động sang Insert mode) | Vim gốc |
| `<leader>d` | Normal | Xóa nhưng **không lưu vào Clipboard** | **Custom** |
| `v` | Normal | Chuyển sang chế độ bôi đen (Visual mode) | Vim gốc |
| `V` | Normal | Bôi đen cả dòng (Visual Line mode) | Vim gốc |

## 3. Cấp độ Trung cấp (Di chuyển tốc độ cao & Quản lý Window)
*Thay vì gõ phím di chuyển nhiều lần, hãy dùng các phím này để nhảy cóc.*

| Phím gõ | Chế độ | Chức năng | Nguồn gốc |
| :--- | :---: | :--- | :--- |
| `H` / `L` | Normal | Nhảy đến **đầu dòng** / **cuối dòng** (Thay cho ^ và $) | **Custom** |
| `w` / `b` | Normal | Nhảy đến từ tiếp theo / lùi lại từ trước đó (Dừng ở dấu câu) | Vim gốc |
| `W` / `B` | Normal | Nhảy theo **chuỗi liền** (Bỏ qua dấu câu, dừng ở khoảng trắng)| Vim gốc |
| `%` | Normal | Nhảy qua lại giữa dấu mở/đóng ngoặc `{ }`, `( )` tương ứng | Vim gốc |
| `<leader>\|` | Normal | Chia màn hình dọc (Split Vertical) | **Custom** |
| `<leader>-` | Normal | Chia màn hình ngang (Split Horizontal) | **Custom** |
| `<leader>wd` | Normal | Hủy chia màn hình (Unsplit) | **Custom** |
| `<C-h> <C-j> <C-k> <C-l>`| Normal| Nhảy con trỏ sang các màn hình Split khác | **Custom** |
| `<S-h>` / `<S-l>`| Normal | Chuyển sang Tab file bên trái / bên phải | **Custom** |
| `<leader>bd` | Normal | Đóng Tab/Buffer hiện tại | **Custom** |

## 4. Cấp độ Nâng cao (Giả lập Telescope - Tìm kiếm mọi thứ)
*Sử dụng phím Leader để mở các popup tìm kiếm mạnh mẽ của IntelliJ.*

| Phím gõ | Chế độ | Chức năng | Tương đương LazyVim |
| :--- | :---: | :--- | :--- |
| `<leader>e` | Normal | Bật/tắt cây thư mục bên trái (Project Explorer)| `<leader>e` (Neo-tree) |
| `<leader><space>` | Normal | Tìm file bất kỳ trong project | `<leader><space>` |
| `<leader>ff` | Normal | Tìm file bất kỳ trong project | `<leader>ff` |
| `<leader>sg` | Normal | Tìm một đoạn text trong toàn project | `<leader>sg` (live_grep) |
| `<leader>sc` | Normal | Tìm Class/Symbol cụ thể | `<leader>ss` (lsp_symbols) |
| `<leader>fb` | Normal | Xem danh sách các file/buffer vừa mở | `<leader>fb` (buffers) |
| `<leader>ur` | Normal | Tắt highlight màu vàng sau khi Search xong | `<leader>ur` |

## 5. Cấp độ "Trùm cuối" (Code Actions, LSP & IntelliJ Tools)
*Thao tác trực tiếp với các tính năng thông minh của Java/Spring Boot qua IdeaVim.*

| Phím gõ | Chế độ | Chức năng | Phân loại |
| :--- | :---: | :--- | :--- |
| `gd` | Normal | Đi tới phần định nghĩa (Go to Declaration) | Vim gốc |
| `gI` | Normal | Đi tới file Implementation của Interface (Cực hữu ích cho Spring Boot) | **Custom** |
| `gr` | Normal | Mở popup xem những nơi nào đang gọi hàm/biến này (Find Usages) | **Custom** |
| `K` | Normal | Mở popup xem tài liệu / Javadoc của hàm/biến | **Custom** |
| `]d` / `[d` | Normal | Nhảy đến lỗi (Error/Warning) tiếp theo / trước đó | **Custom** |
| `]m` / `[m` | Normal | Nhảy xuống Hàm (Method) tiếp theo / ngược lên Hàm trước đó | **Custom** |
| `<leader>cf` | N/V | Format lại code cho chuẩn (Áp dụng cả Normal hoặc bôi đen Visual) | **Custom** |
| `<leader>cr` | Normal | Đổi tên biến/hàm an toàn trên toàn project (Rename) | **Custom** |
| `<leader>ca` | Normal | Mở menu gợi ý sửa lỗi của IntelliJ (Code Actions/Intentions) | **Custom** |
| `<C-\>` | N/I/T | Mở / Đóng nhanh cửa sổ Terminal (Có thể dùng `<leader>t`) | **Custom** |
| `<leader>dr` | Normal | Mở cửa sổ Debug | **Custom** |
| `<leader>rr` | Normal | Mở cửa sổ Run | **Custom** |