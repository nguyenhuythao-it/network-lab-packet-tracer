# Lab - Network Address Translation (NAT)
## Mục tiêu
Cấu hình địa chỉ IP cho các interface trên Router PNH, ISP và Google; thiết lập NAT động (Dynamic NAT) và NAT overload (PAT) trên Router PNH; thiết lập NAT tĩnh (Static NAT) trên Router Google để xuất bản dịch vụ ra Internet; kiểm tra kết nối và dịch vụ bằng ping và truy cập port.
## File
- [nat-lab.pkt](nat-lab.pkt)
- [nat-config.txt](nat-config.txt)
## Các bước chính
Router PNH: gán IP cho g0/0 → 172.16.0.1/24, g0/1 → 192.168.0.1/24, g0/2 → 6.6.6.6/24; 
tạo access-list 1 để chọn host nội bộ; 
tạo NAT pool `ip nat pool PNH 6.6.6.6 6.6.6.6 netmask 255.255.255.0`; 
cấu hình `ip nat inside source list 1 pool PNH overload`; 
đánh dấu interface g0/0, g0/1 là inside, g0/2 là outside; 
thiết lập default route `ip route 0.0.0.0 0.0.0.0 6.6.6.1`. 
Router ISP: gán IP cho g0/0 → 6.6.6.1/24, g0/1 → 8.8.8.1/24, g0/2 → 7.7.7.1/24. 
Router Google: gán IP cho g0/0 → 172.16.0.1/24, g0/1 → 8.8.8.8/24; 
thiết lập default route `ip route 0.0.0.0 0.0.0.0 8.8.8.1`; 
cấu hình NAT tĩnh để xuất bản dịch vụ: `ip nat inside source static tcp 172.16.0.10 53 8.8.8.8 53`
(DNS), `ip nat inside source static tcp 172.16.0.20 80 8.8.8.8 80` 
(HTTP), `ip nat inside source static tcp 172.16.0.20 443 8.8.8.8 443` 
(HTTPS), `ip nat inside source static tcp 172.16.0.30 25 8.8.8.8 25` 
(SMTP), `ip nat inside source static tcp 172.16.0.30 110 8.8.8.8 110` 
(POP3); đánh dấu g0/0 là inside, g0/1 là outside.
## Kết quả
Các host nội bộ mạng 192.168.0.x truy cập Internet thông qua NAT overload; 
các dịch vụ nội bộ (DNS, Web, Mail) được NAT tĩnh và xuất bản ra địa chỉ công cộng 8.8.8.8; 
ping và truy cập dịch vụ từ ngoài Internet đến địa chỉ 8.8.8.8 thành công.
