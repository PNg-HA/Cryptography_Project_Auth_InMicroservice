# Xác thực và ủy quyền người dùng trong kiến trúc microservice
Đồ án của NT219 Mật mã Học - Xác thực và ủy quyền người dùng trong kiến trúc microservice. 
Thành viên nhóm:
- Nguyễn Nhật Quân: phụ trách mảng Dev (code các service).
- Phạm Nguyễn Hải Anh: phụ trách mảng Ops (triển khai docker, triển khai web có tên miền, cân bằng tải với AWS ALB)

## Kiến trúc
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/2f98b8e6-dd5f-4ae8-9a1b-da2a8e5a387e)

Mô hình gồm:
  - Gateway
  - Auth
  - Task

Các service được chạy từ các file server.py

## Thực hiện
Xem [guide.txt](guide.txt) để thực hiện trên mạng bridge của Docker tại localhost:
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/6dd4125c-5ae6-4fc2-b1cb-3ed253e3a188)

Nếu muốn đổi ip cho các container, xem lại các server.py trong repo và đổi lại các ip của các service cho phù hợp 

