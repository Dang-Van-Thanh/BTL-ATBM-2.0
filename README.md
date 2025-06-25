# Sơ đồ thư mục dự án
```
📁 BTL-ATBM/
│
├── app.py                   # Điểm khởi động Flask app
├── .env                     # Biến môi trường (DB, SECRET_KEY, ...)
├── requirements.txt         # Các thư viện cần cài
│
├── models.py                # Định nghĩa bảng User & LoginLog
├── utils.py                 # Xử lý SHA, salt, Triple DES
├── auth.py                  # Xử lý logic: đăng ký, đăng nhập, đổi mật khẩu
│
├── templates/               # Giao diện HTML
│   ├── layout.html
│   ├── index.html
│   ├── register.html
│   ├── login.html
│   ├── change_password.html
│   └── admin.html
│
└── static/                  # CSS, JS, ảnh (nếu có)
```
# SQL-database
```
-- Tạo CSDL
CREATE DATABASE FlaskAuth;
GO
USE FlaskAuth;

-- Bảng người dùng
CREATE TABLE NguoiDung (
    id INT IDENTITY(1,1) PRIMARY KEY,
    username_hash VARCHAR(64) NOT NULL UNIQUE,
    password_encrypted VARCHAR(256) NOT NULL,
    salt VARCHAR(32) NOT NULL,
    fail_count INT DEFAULT 0,
    is_locked BIT DEFAULT 0,
    is_admin BIT DEFAULT 0
);

-- Bảng lịch sử đăng nhập
CREATE TABLE LichSuDangNhap (
    id INT IDENTITY(1,1) PRIMARY KEY,
    username_hash VARCHAR(64),
    ip_address VARCHAR(45),
    success BIT,
    timestamp DATETIME DEFAULT GETDATE()
);
```
# Nội dung file .env
```
DB_SERVER=localhost
DB_NAME=FlaskAuth
DB_DRIVER=ODBC Driver 17 for SQL Server
USE_WINDOWS_AUTH=True
SECRET_KEY=your_secret_key_here
```
# Cách chạy
## Lệnh cấp phép tạm thời
```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```
## Tạo/Kích hoạt môi trường ảo
```
python -m venv venv
.\venv\Scripts\activate
```
## Tải thư viện
```
pip install -r requirements.txt
```
## Chạy dự án
```
python app.py
```
# Hình ảnh minh hoạ
## Trang chủ
![image](https://github.com/user-attachments/assets/d62a033b-8aec-4ad0-a362-ac5857bc482d)
## Đăng ký
![image](https://github.com/user-attachments/assets/5cbb674c-36fd-4bf5-9d6c-f9542e9da543)
### Đăng ký thành công
![image](https://github.com/user-attachments/assets/1d3e10fa-1583-41c5-84a9-2a52374ab313)
### Đăng ký thất bại
![image](https://github.com/user-attachments/assets/6b676324-3c1e-4176-b602-9b53c95b10bb)
## Đăng nhập
![image](https://github.com/user-attachments/assets/4fe73bde-761f-48d3-b279-527f7b8f001c)
### Đăng nhập thành công
![image](https://github.com/user-attachments/assets/330cb9c9-fe53-42ae-a5a8-2acc6c85e308)
### Đăng nhập thất bại
![image](https://github.com/user-attachments/assets/a80f73cd-57d7-4ffb-aa49-41a41d6b7ca6)
### Đăng nhập bị khoá tài khoản
![image](https://github.com/user-attachments/assets/06366201-b77b-4c6a-b68d-1aaa4ed18f37)
## Đổi mật khẩu
![image](https://github.com/user-attachments/assets/505af81a-2843-402a-b750-6830778e7429)
### Đổi mật khẩu thành công
![image](https://github.com/user-attachments/assets/17017230-5cc0-41d6-b2de-cb4959b45bae)
### Đổi mật khẩu thất bại
![image](https://github.com/user-attachments/assets/fbb43d8a-016b-4cae-8e09-bcf16abe25f2)
## Quản trị
### Bình thường
![image](https://github.com/user-attachments/assets/e8cefedd-a85f-4cba-b0b6-1e43c059d656)
### Có tài khoản bị khoá
![image](https://github.com/user-attachments/assets/7330a0df-9342-421a-aa55-a6b8445ff655)











