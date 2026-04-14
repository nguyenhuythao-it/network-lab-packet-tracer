# Lab - Định tuyến động với RIP v2

## Mục tiêu
- Cấu hình địa chỉ IP cho các interface trên Router0, Router1, Router2.
- Kích hoạt giao thức định tuyến động RIP version 2.
- Quảng bá các mạng nội bộ qua RIP để các router học được route lẫn nhau.
- Kiểm tra kết nối giữa các mạng bằng lệnh `ping`.

## File
- [rip-lab.pkt](rip-lab.pkt)
- [rip-config.txt](rip-config.txt)

## Kết quả
- Các router học được route của nhau qua RIP.  
- Lệnh `show ip route` hiển thị đầy đủ các mạng.  
- Ping từ PC tới các mạng khác thành công.
