# demoproject
🔹 **Nguyễn Quang Tú - K24DTCN241** – Trưởng nhóm & lập trình chính main.cpp
Viết hàm main(), menu chính, menu người dùng, menu admin.
Gọi và điều phối các chức năng từ user.h và wallet.h.
Xử lý luồng hoạt động của hệ thống: đăng nhập, đăng ký, đăng xuất, phân quyền.
Kiểm tra sự tồn tại tài khoản admin, tạo mặc định nếu chưa có.
🔹 **Lò Văn Tín - K24DTCN238** – Xử lý người dùng user.h & user.cpp
Thiết kế và triển khai class User, bao gồm:
Các thuộc tính: username, password (SHA-256 hash), fullName, email, phone, role, walletID, oathSecretKey.
Triển khai các chức năng: registerUser(), login(), changePassword(), updateProfile(), viewUsers(), adminEditUser().
Sinh mã OTP (giả lập).
Đọc/ghi tệp data/users.txt theo định dạng CSV, tạo file .bak.
🔹 **Hồ Xuân Thái - K24DTCN229** – Quản lý ví điểm thưởng wallet.h & wallet.cpp
Thiết kế và triển khai class Wallet, bao gồm:
Các thuộc tính: walletID, balance, transactionLog.
Triển khai các chức năng: depositPoints(), transferPoints(), viewWallet(), saveWallet(), loadWallet().
Xử lý thao tác ghi/đọc tệp data/wallets.txt, quản lý nhật ký giao dịch.
🔹 **Vũ Đình Thề - K24DTCN235** – Thiết lập, bảo mật, cấu hình hệ thống & tài liệu
Tạo và duy trì: Makefile, hướng dẫn biên dịch và chạy.
Cấu hình thư viện OpenSSL, OATH Toolkit.
Viết và cập nhật:README.md (giới thiệu, cách dùng, bảo mật, hướng dẫn OTP).
Cấu trúc thư mục, hướng dẫn setup (trên Linux, macOS, WSL).
Kiểm tra bảo mật: sinh mật khẩu ngẫu nhiên, băm SHA-256, lưu OATH key, OTP đầu vào/giả lập.
Kết quả bàn giao:
Makefile, README.md, cấu hình .gitignore
Hướng dẫn cài đặt chi tiết (Linux, macOS, Windows WSL)
Đảm bảo hệ thống hoạt động xuyên nền tảng
# TÍNH NĂNG CHÍNH
** Xác thực và bảo mật
Đăng ký, đăng nhập tài khoản với mã OTP (sử dụng OATH Toolkit)
Băm mật khẩu bằng SHA-256 (OpenSSL)
OTP được yêu cầu trong các hành động nhạy cảm: đổi mật khẩu, cập nhật thông tin, chuyển điểm
** Quản lý người dùng
Xem và cập nhật thông tin cá nhân
Đổi mật khẩu (yêu cầu OTP)
Đăng ký và đăng nhập tài khoản mới
Quản trị viên có thể chỉnh sửa tài khoản người dùng
**Quản lý ví điểm thưởng**
Tự động tạo ví liên kết khi đăng ký
Xem số dư và lịch sử giao dịch
Chuyển điểm giữa các ví (OTP xác nhận)
**Quyền admin**
Xem toàn bộ danh sách người dùng
Tạo tài khoản mới với mật khẩu sinh tự động
Chỉnh sửa thông tin người dùng và phân quyền
## CẤU TRÚC DỰ ÁN
hethongquanly/
├── include/
│   ├── user.h          # Khai báo lớp User
│   └── wallet.h        # Khai báo lớp Wallet
│
├── src/
│   ├── main.cpp        # Hàm chính và menu
│   ├── user.cpp        # Triển khai hàm User
│   └── wallet.cpp      # Triển khai hàm Wallet
│
├── data/               # Chứa dữ liệu .txt và file backup
│   ├── users.txt
│   └── wallets.txt
│
├── Makefile            # Biên dịch chương trình
├── .gitignore          # Danh sách file không theo dõi bởi Git
└── README.md           # Hướng dẫn và mô tả dự án
### YÊU CẦU HỆ THỐNG
Trình biên dịch C++ hỗ trợ C++11 trở lên (g++, clang++)
OpenSSL để băm SHA-256
OATH Toolkit để sinh và xác thực OTP
#### HƯỚNG DẪN CÀI ĐẶT VÀ CHẠY
**1. Clone repository**
```shell
git clone https://github.com/mokaa1102/hethongquanly.git
cd hethongquanly
```
**2. Cài đặt thư viện phụ thuộc**
- Trên Ubuntu/Debian:
```shell
sudo apt update
sudo apt install build-essential libssl-dev oathtool
```
- Trên macOS (sử dụng Homebrew):
```shell
brew update
brew install openssl oathtool pkg-config
```
- Trên Windows:
Sử dụng Windows Subsystem for Linux (WSL) và làm theo hướng dẫn cho Ubuntu/Debian.

3. Biên dịch chương trình
Sử dụng "Makefile" được cung cấp để biên dịch:
```shell
make
```
Câu lệnh này sẽ tạo ra một file thực thi có tên "hethongquanly" trong thư mục gốc của chương trình.
```shell
g++ src/main.cpp -o hethongquanly -std=c++11 -lssl -lcrypto
```
4. Chạy chương trình
```shell
./hethongquanly
```
- Lần chạy đầu tiên: Chương trình sẽ kiểm tra và nếu không có tài khoản "admin", nó sẽ tự động tạo một tài khoản "admin" với mật khẩu mặc định (admin123) và hiển thị OATH Secret Key.
  Ghi lại OATH Secret Key này và thêm vào ứng dụng xác thực của bạn (One Time Password, Google Authenticator, Microsoft Authenticator,...). Bạn sẽ cần mã OTP từ ứng dụng này để đăng nhập.
- Đăng nhập lần đầu: Đăng nhập với "admin" và mật khẩu "admin123". Nhập mã OTP từ ứng dụng xác thực. Hệ thống sẽ yêu cầu bạn đổi mật khẩu ngay lập tức.
- Lưu trữ dữ liệu: Các file "users.txt" và "wallets.txt" (cùng các file ".bak") sẽ được tạo/cập nhật trong cùng thư mục bạn chạy file "hethongquanly".

# HƯỚNG DẪN SỬ DỤNG
** Menu chính
[1] Đăng nhập – nhập tên đăng nhập, mật khẩu và mã OTP
[2] Đăng ký – nhập thông tin tài khoản, tạo ví liên kết
[0] Thoát – kết thúc chương trình
**Sau khi đăng nhập**
Người dùng:
Xem/Cập nhật thông tin cá nhân
Đổi mật khẩu
Quản lý ví (xem số dư, lịch sử, chuyển điểm)
Đăng xuất
Admin:
Tạo tài khoản cho người dùng khác
Xem và chỉnh sửa thông tin người dùng
Phân quyền người dùng (user/admin)
Đăng xuất
#### LƯU Ý BẢO MẬT
Mật khẩu được băm bằng SHA-256, không lưu dưới dạng văn bản gốc
OTP khi đăng nhập được xác thực bằng OATH Toolkit và ứng dụng OTP
Trong các hành động như đổi mật khẩu hay chuyển điểm, chương trình dùng generateSimulatedOTP() để mô phỏng OTP (in ra màn hình thay vì gửi email/SMS)
Khóa OTP được lưu trực tiếp trong file users.txt, nên cần bảo mật tệp này
##### LƯU TRỮ DỮ LIỆU
Tệp tin	Mô tả	Định dạng
users.txt	Thông tin người dùng	CSV
wallets.txt	Dữ liệu ví và giao dịch	CSV
.bak	Các bản sao lưu	Tự động tạo
