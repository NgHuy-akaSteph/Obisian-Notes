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

### 1.3 Chuẩn hóa NF
#### a) Chuẩn hóa 1NF

#### b) Chuẩn hóa 2NF

#### c) Chuẩn hóa 3NF
- Một lược đồ quan hệ R đạt dạng chuẩn 3 nếu mọi phụ thuộc hàm 
  X -> A $\in$ F+ (F là tập phụ thuộc hàm không hiển nhiên định nghĩa trên R, A là thuộc tính đơn, X là tập thuộc tính con của tập F+)
- - X là một siêu khóa của R
- - A là một thuộc tính khóa
- -> R đạt chuẩn 3 thì R đạt chuẩn 2
#### d) Các bước chuẩn hóa
- Đưa về chuẩn 1:
	- Nhóm các thuộc tính đơn còn lại tạo thành 1 quan hệ. Chọn khóa cho nó.
	- Nhóm các thuộc tính lặp tách ra cùng với khóa của quan hệ trên tạo thành 1 quan hệ ( hay một số quan hệ theo chủ đề)
- Đưa về dạng chuẩn 2:
	- Tách các nhóm thuộc tính phụ thuộc hàm vào một bộ phận của khóa (xét các quan hệ có khóa kép).
	- Nhóm còn lại tạo thành 1 quan hệ với khóa cũ.
	- Mỗi nhóm tách ra, gồm các thuộc tính cùng phụ thuộc và một hay một số thuộc tính nào đó của khóa, cộng thêm các thuộc tính mà chúng phụ thuộc tạo thành 1 quan hệ, với các khóa là các thuộc tính cộng thêm này.
- Đưa về dạng chuẩn 3: 
	- Tách các thuộc tính phụ thuộc hàm vào một hay một số bộ phận của khóa.
	- Nhóm còn lại tạo thành 1 quan hệ với khóa cũ
	- Mỗi nhóm tách ra gồm thuộc tính cùng phụ thuộc hàm vào một hay một số thuộc tính không phải là khóa, cộng thêm các thuộc tính mà chúng phụ thuộc tạo thành một quan hệ, với khóa là các thuộc tính cộng thêm này.
- Ví dụ: 
## 2. Bài tập 

B1: Chuẩn hóa 1NF đến 3NF
B2: Vẽ ERD (biểu diễn các bảng và quan hệ)
B3: Viết chương trình




