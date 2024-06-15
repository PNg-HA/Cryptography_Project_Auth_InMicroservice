# Xác thực và ủy quyền người dùng trong kiến trúc microservice
Đồ án của NT219 Mật mã Học - Xác thực và ủy quyền người dùng trong kiến trúc microservice thông qua dynamic token (JWT). 
Thành viên nhóm:
- Nguyễn Nhật Quân: phụ trách mảng Dev (code các service).
- Phạm Nguyễn Hải Anh: phụ trách mảng Ops (triển khai docker, triển khai web có tên miền, cân bằng tải với AWS ALB)
Bản báo cáo chi tiết: [Nhom1_21520586-21522497.docx](Nhom1_21520586-21522497.docx)
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

## Triển khai trên AWS
Con load balancer sẽ được gắn tên miền “mmhmicro.online” kèm với certificate đã ký được từ ZeroSSL.
### Mô hình triển khai
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/7c8b251e-7480-4d20-8124-606c7ffc15be)



+ Import chứng chỉ đã được ký cho tên miền “mmhmicro.online” vào AWS Certificate Manage
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/e206835e-7de3-4be4-8101-9c3716e3b980)

+	Tạo hosted zone cho domain trên AWS 53. Khi đó AWS sẽ cung cấp tên của 4 name server. Nhập chúng vào nơi mua domain.
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/cbe53cf2-c3c3-497b-bcc2-f20c4ab006bd)
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/7fe39be3-ab96-4ec5-93e1-bedb818171d2)

+	Tạo Load Balancer và Target group cho server

Load balancer này chứa certificate import từ ACM. Giao thức lắng nghe từ internet là HTTPS, giao thức giao tiếp với server là HTTP
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/ad1b2914-2f5d-49a9-a0fb-ecf3a66b17f0)
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/b73ae974-cff7-4d41-94cc-929d63f66c9e)

+	Tại AWS Route 53, tạo DNS record type A để chuyển từ “mmhmicro.online” sang tên DNS của con load balancer.
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/69a044db-73ba-4e06-bb92-f5fe860c9748)

## Demo
+	Đăng ký tài khoản:
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/23e85153-ec42-4f1c-a89a-89febc281ba8)

+	Đăng nhập, server sẽ trả về 1 opaque token có hiệu lực trong 10p:
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/2365e65a-9fdc-4329-a072-ed6d40ae927c)

+	Sử dụng token vừa cấp để thao tác trên task service (tạo ghi chú):
![image](https://github.com/PNg-HA/NT219_Crypto_Project_AuthForUserInMcrservice/assets/93396414/665bad6c-21cd-44a1-bf18-73bc8e49c6ee)


