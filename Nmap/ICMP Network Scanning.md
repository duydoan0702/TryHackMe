
# TryHackMe

## 🧩 Challenge: ICMP Network Scanning

## 📝 Description
Khi kết nối lần đầu đến mạng đích trong bài toán hộp đen, mục tiêu đầu tiên của chúng ta là có được một "**map**" cấu trúc mạng hay nói cách khác, chúng ta muốn xem địa chỉ IP nào chứa các máy chủ đang hoạt động và địa chỉ nào không.

Một cách để thực hiện việc này là sử dụng Nmap để thực hiện cái gọi là "**ping sweep**". Đúng như tên gọi, Nmap gửi một gói tin ICMP đến từng địa chỉ IP khả dụng cho mạng được chỉ định. Khi nhận được phản hồi, nó sẽ đánh dấu địa chỉ IP đã phản hồi là còn hoạt động. Vì những lý do chúng ta sẽ thấy trong bài viết sau, điều này không phải lúc nào cũng chính xác; tuy nhiên, nó có thể cung cấp một số thông tin cơ sở và do đó đáng để tìm hiểu.

Để thực hiện ping sweep, chúng ta sử dụng khóa chuyển đổi `-sn` kết hợp với các dải IP có thể được chỉ định bằng ký hiệu gạch nối (`-`) hoặc CIDR. Ví dụ, chúng ta có thể quét mạng 192.168.0.x bằng cách sử dụng:
- `nmap -sn 192.168.0.1-254`
or
- `nmap -sn 192.168.0.0/24`

Lệnh chuyển đổi `-sn` yêu cầu Nmap không quét bất kỳ cổng nào buộc nó phải dựa chủ yếu vào các gói tin ICMP echo (hoặc yêu cầu ARP trên mạng cục bộ, nếu chạy bằng sudo hoặc trực tiếp với quyền root) để xác định mục tiêu. Ngoài các yêu cầu ICMP echo, lệnh chuyển đổi -sn cũng sẽ khiến nmap gửi một gói tin TCP SYN đến cổng 443 của mục tiêu, cũng như một gói tin TCP ACK (hoặc TCP SYN nếu không chạy với quyền root) đến cổng 80 của mục tiêu.

> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
1. Bạn sẽ thực hiện quét ping trên mạng 172.16.x.x (Netmask: 255.255.0.0) bằng Nmap như thế nào? (Ký hiệu CIDR)

---


## 🛠️ Cách giải

1. Dùng `-sn` để kiểm tra các host còn hoạt động không
```
nmap -sn 172.16.0.0/16
```
- Ứng dụng của `-sn`:
  - Kiểm tra máy nào đang bật trong mạng LAN.

  - Dò thiết bị lạ trong mạng (ví dụ: ai đang xài chùa Wi-Fi).

  - Là bước khởi đầu trong quá trình quét mạng nội bộ.
 
  <img width="576" height="377" alt="image" src="https://github.com/user-attachments/assets/c0c8366e-cda4-406f-b6d4-c1146b3ecbf5" />



