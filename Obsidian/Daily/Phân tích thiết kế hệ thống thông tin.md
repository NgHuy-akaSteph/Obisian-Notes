## 1.Xây dựng thực thể liên kết

### 1.1 Các bước thực hiện
- B1: Xác định danh sách các loại thực thể cùng danh sách thuộc tính.
- B2: Xác định các mỗi liên kết giữa các loại thực thể
*VD: 
- Mỗi sinh viên cần quản lý các thông tin như: Họ và tên (HotenSV), ngày sinh (NgaySinh), giới tính (GT), nơi sinh (NoiSinh), hộ khẩu thường trú (Tinh). Mỗi sinh viên được cấp một mã sinh viên duy nhất (MaSV) để phân biệt với mọi sinh viên khác.
- Mỗi lớp có MaLop duy nhất và cso tên lớp, thuộc về 1 khoa.
- Mỗi khoa có 1 tên và 1 mã số duy nhất MaKhoa.
- Mỗi giảng viên cx có thông tin: tên, học vị,...

### 1.2 Xây dựng RD

#### a) Thuộc tính: 
- đặc điểm của đối tượng có tên gọi và thuộc về 1 kiểu duy nhất.
 
#### b) Lược đồ quan hệ: 
- tập các thuộc tính cần quản lý và các mối liên hệ giữa chúng
- VD: SinhVien (MaSV, HotenSV, GT, NgaySinh, NoiSinh, Tinh, MaLop)
#### c) Quan hệ
- Sử dụng ký hiệu in hoa để chỉ các lược đồ quan hệ. Các quan hệ dùng chữ cái in thường.
- Về trực quan thì quan hệ (hay bảng quan hệ) như là một bảng 2 chiều gồm các cột và dòng.
- Mỗi quan hệ có n thuộc tính thì được gọi là quan hệ n ngôi
- Để chỉ quan hệ r xác định trên lược đồ quan hệ R ta có thể viết r(R).
#### d) Bộ (Tuple)
- Mỗi bộ là những thông tin về đối tượng thuộc một quan hệ, bộ cx còn được gọi là mẫu tin.
- Thường ta dùng chữ cái thường (như t, s,...) để biểu diễ bộ trong quan hệ, chẳng hạn dể nói t là một bộ quan hệ r thì ta viết t $\in$ r
#### e) Siêu khóa
- S là siêu khóa của R nếu với r là quan hệ trên R, t1, t2 là hai bộ bất kì thuộc r thì t1.S != t2.S
- Một lược đồ quan hệ có thể có một hoặc nhiều siêu khóa






