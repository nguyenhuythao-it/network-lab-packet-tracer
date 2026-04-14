# Lab - Network Address Translation (NAT)
## Mục tiêu
Cấu hình địa chỉ IP cho các interface trên Router PNH, ISP và Google; thiết lập NAT động (Dynamic NAT) và NAT overload (PAT) trên Router PNH; thiết lập NAT tĩnh (Static NAT) trên Router Google để xuất bản dịch vụ ra Internet; kiểm tra kết nối và dịch vụ bằng ping và truy cập port.
## File
- [nat-lab.pkt](nat-lab.pkt)
- [nat-config.txt](nat-config.txt)
## Các bước chính
- Router PNH: gán IP cho g0/0 → 172.16.0.1/24, g0/1 → 192.168.0.1/24, g0/2 → 6.6.6.6/24; tạo access-list 1 để chọn host nội bộ; tạo NAT pool; đánh dấu interface g0/0, g0/1 là inside, g0/2 là outside; thiết lập default route 
- Router ISP: gán IP cho g0/0 → 6.6.6.1/24, g0/1 → 8.8.8.1/24, g0/2 → 7.7.7.1/24.
- Router Google: gán IP cho g0/0 → 172.16.0.1/24, g0/1 → 8.8.8.8/24; thiết lập default route ; cấu hình NAT tĩnh để xuất bản dịch vụ: (DNS),(HTTP), (HTTPS), (SMTP), (POP3)
## Kết quả
Các host nội bộ mạng 192.168.0.x truy cập Internet thông qua NAT overload; các dịch vụ nội bộ (DNS, Web, Mail) được NAT tĩnh và xuất bản ra địa chỉ công cộng 8.8.8.8; ping và truy cập dịch vụ từ ngoài Internet đến địa chỉ 8.8.8.8 thành công.
