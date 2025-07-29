
# TryHackMe

## 🧩 Challenge: Introduction

## 📝 Description
Xin lưu ý: Máy này chỉ dùng cho mục đích quét. Bạn không cần phải đăng nhập hoặc khai thác bất kỳ lỗ hổng bảo mật nào để truy cập.

Nếu bạn đang sử dụng TryHackMe AttackBox, bạn sẽ cần triển khai riêng. Nhấp vào nút Khởi động AttackBox ở góc trên bên phải để khởi chạy máy.

> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Chiến lược giải
- Kết nối với máy ảo
  
## 🔧 Công cụ
1. **openvpn**
Là một phần mềm mã hóa mã nguồn mở để tạo **mạng riêng ảo(VPN)** giữa 2 điểm client <-> server qua giao thức **SSl/TLS** . Nó cho phép :
  - Mã hóa lưu lượng mạng
  - Giả lập kết nối nội bộ từ xa
  - Truy cập các hệ thống nội bộ (như các máy trong Tryhackme/Hackthebox)
---


## 🛠️ Cách giải

1. Bấm vào nút `Start Machine` rồi tải file `.opvn` về và kết nối bằng `openvpn`

```
sudo openvpn duydoan0702.ovpn
```
2.Kiểm tra địa chỉ ip mới

```
curl 10.10.10.10/whoami
```
