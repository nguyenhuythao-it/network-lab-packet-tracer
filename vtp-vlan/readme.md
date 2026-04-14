# Lab - Định tuyến tĩnh, VLAN và VTP

## Mục tiêu
- Cấu hình router ISP với nhiều interface (g0/0, g0/1, g0/2).
- Thiết lập định tuyến tĩnh giữa ISP và PNH.
- Cấu hình Core Switch với VTP domain, VLAN, trunk.
- Cấu hình Access Switch (Access1, Access2) ở chế độ client, gán port vào VLAN.
- Cấu hình Router PNH với sub-interface, NAT, DHCP helper.

## File
- [lab-routing-vlan.pkt](lab-routing-vlan.pkt)
- [lab-routing-vlan.txt](lab-routing-vlan.txt)

## Các bước chính
### Router ISP
- Gán IP cho các interface g0/0, g0/1, g0/2.
- Thiết lập static route: `ip route 69.0.0.0 255.255.255.0 7.7.7.1`.

### Core Switch
- Đặt hostname, domain VTP, password.
- Tạo VLAN 2 (system), VLAN 3 (app), VLAN 4 (dmz), VLAN 5 (user).
- Cấu hình trunk trên các cổng g1/0/1-3.

### Access Switches
- Đặt hostname Access1, Access2.
- Tham gia VTP domain `pnh.vn`, password `123`, mode client.
- Gán port access vào VLAN tương ứng (f0/4 → VLAN 2, f0/6 → VLAN 3, f0/8 → VLAN 4, …).

### Router PNH
- Đặt hostname.
- Tạo sub-interface g0/0.1 → VLAN 1, g0/0.2 → VLAN 2, g0/0.3 → VLAN 3, g0/0.4 → VLAN 4, g0/0.5 → VLAN 5.
- Gán IP cho từng sub-interface, bật NAT inside.
- Cấu hình DHCP helper: `ip helper-address 10.2.2.10`.

## Kết quả
- VLAN được tạo và phân phối qua VTP.
- Các port access đã gán đúng VLAN.
- Router PNH định tuyến và NAT thành công.
- Ping thông giữa các mạng.
