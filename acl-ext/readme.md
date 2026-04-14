# Lab - Access Control List (ACL)

## Mục tiêu
- Cấu hình địa chỉ IP cho các interface trên Router PNH và Router ISP.
- Tạo ACL để kiểm soát truy cập giữa các mạng.
- Áp dụng ACL vào interface để lọc lưu lượng.
- Kiểm tra kết quả bằng ping và truy cập dịch vụ.

## File
- [acl-lab.pkt](acl-lab.pkt)
- [acl-config.txt](acl-config.txt)

## Các bước chính
### Router PNH
- Gán IP cho các interface:  
  - g0/0 → 172.16.0.1/24  
  - g0/1 → 192.168.0.1/24  
  - g0/2 → 7.7.7.1/30  
- Tạo ACL số 100:  
  - Cho phép host 192.168.0.150 truy cập mạng 172.16.0.0/24.  
  - Chặn host 192.168.0.150 truy cập web (TCP port 80, 443).  
  - Cho phép host 192.168.0.200 truy cập web server 172.16.0.10 (port 80, 443).  
  - Chặn host 192.168.0.200 truy cập toàn bộ mạng 172.16.0.0/24.  
  - Cho phép tất cả lưu lượng khác.  
- Áp dụng ACL 100 vào interface g0/1 (hướng inbound).  

- Tạo ACL số 101:  
  - Chặn ICMP type 8 (echo request).  
  - Cho phép ICMP khác.  
- Áp dụng ACL 101 vào interface g0/2 (hướng inbound).  

### Router ISP
- Gán IP cho các interface:  
  - g0/0 → 8.8.8.1/24  
  - g0/1 → 9.9.9.1/30  
  - g0/2 → 7.7.7.2/30  

## Kết quả
- Host 192.168.0.150 không thể truy cập web nhưng vẫn ping được mạng 172.16.0.0/24.  
- Host 192.168.0.200 chỉ được phép truy cập web server 172.16.0.10, bị chặn với các IP khác trong mạng 172.16.0.0/24.  
- ICMP echo request bị chặn trên interface g0/2, nhưng các loại ICMP khác vẫn được phép.  
- ACL hoạt động đúng theo yêu cầu.
