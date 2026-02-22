# Dự án: Thiết kế & Triển khai Hạ tầng Mạng Doanh nghiệp
## 1. Tổng quan dự án
Dự án tập trung vào việc thiết kế một hạ tầng mạng quy mô doanh nghiệp nhỏ/vừa, đảm bảo tính bảo mật và tối ưu hóa tài nguyên địa chỉ IP. Hệ thống phân chia thành các VLAN riêng biệt cho từng phòng ban, tích hợp mạng không dây và các dịch vụ mạng cơ bản.

### Các công nghệ trọng tâm:
Subnetting (VLSM): Tối ưu hóa dải IP 192.168.49.0/24.<br>
VLAN & Trunking: Phân tách luồng dữ liệu giữa các phân khu.<br>
Static Routing: Thiết lập kết nối liên mạng giữa các Router Cisco.<br>
Network Services: Cấu hình Wireless, Telnet, DNS và Email Server.<br>

### 2. Kế hoạch địa chỉ IP (IP Addressing Plan)<br>
Sử dụng kỹ thuật VLSM để chia nhỏ mạng chính thành các Subnet phù hợp với nhu cầu thực tế của từng bộ phận.<br>
Phân khu (Subnet)	Địa chỉ IP	Subnet Mask	Gateway	Mục đích<br>
VLAN 1	192.168.49.0/26	255.255.255.192	192.168.49.1	<br>
49 Users <br>
VLAN 2	192.168.49.64/27	255.255.255.224	192.168.49.65	<br>
29 Users <br>
VLAN 3	192.168.49.96/27	255.255.255.224	192.168.49.100	<br>
19 Users <br>
VLAN 4	192.168.49.128/27	255.255.255.224	192.168.49.129	<br>
Server  <br>

Link A (R1-R2)	192.168.49.160/30	255.255.255.252	-	<br>
Kết nối Router <br>
Link B (R2-R3)	192.168.49.164/30	255.255.255.252	-	<br>
Kết nối Router <br>

### 3. Mô phỏng hệ thống (Cisco Simulation)<br>
Hệ thống được thiết lập và kiểm thử trên môi trường mô phỏng Cisco (Packet Tracer/GNS3) với cấu hình chi tiết cho từng lớp thiết bị.<br>
Cấu hình thiết bị chính:<br>
Router (R1, R2, R3):<br>
Cấu hình Sub-interface trên cổng Giga 0/0 để hỗ trợ định tuyến liên VLAN (Inter-VLAN Routing).<br>
Thiết lập Static Route dựa trên bảng định tuyến để đảm bảo mọi Laptop đều có thể ping thấy Server (192.168.49.130).<br>
Bảo mật truy cập CLI bằng mật khẩu Telnet.<br>

Switch (SW1, SW2):<br>
Cấu hình VLAN Access cho các cổng kết nối người dùng (VLAN 1, 2, 3).<br>
Cấu hình cổng Trunk (Giga0/1) để truyền tải nhiều VLAN lên Router.<br>

Wireless:<br>
Thiết lập 2 Access Point (WR1, WR2) cấp phát IP cho các Laptop không dây trong dải 192.168.0.x.<br>
Kiểm thử & Kết quả (Verification):<br>
Định tuyến: Kiểm tra bảng định tuyến trên R2 thấy đầy đủ các lớp mạng đích thông qua Next Hop tương ứng.<br>
Dịch vụ: Laptop từ các VLAN khác nhau truy cập thành công dịch vụ Email (user1@gmail.com) và phân giải tên miền qua DNS.<br>
Quản trị: Truy cập từ xa vào Router thông qua Telnet thành công từ bất kỳ thiết bị nào trong mạng.<br>
