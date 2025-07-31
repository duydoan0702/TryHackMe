
# TryHackMe

## 🧩 Challenge: Overview

## 📝 Description
Công cụ lập trình Nmap (NSE) là một bổ sung cực kỳ mạnh mẽ cho Nmap, mở rộng đáng kể chức năng của nó. Các tập lệnh NSE được viết bằng ngôn ngữ lập trình Lua và có thể được sử dụng để thực hiện nhiều mục đích: từ quét lỗ hổng bảo mật đến tự động khai thác chúng. NSE đặc biệt hữu ích cho việc trinh sát, tuy nhiên, cần lưu ý đến độ phong phú của thư viện tập lệnh.

Có nhiều danh mục. Một số danh mục hữu ích bao gồm:

- `safe` : Không ảnh hưởng đến mục tiêu
- `intrusive` : Không an toàn: có khả năng ảnh hưởng đến mục tiêu
- `vuln` : Quét lỗ hổng
- `exploit` : Cố gắng khai thác lỗ hổng
- `auth` : Cố gắng bỏ qua xác thực cho các dịch vụ đang chạy (ví dụ: Đăng nhập vào máy chủ FTP ẩn danh)
- `brute` : Cố gắng tấn công bằng cách phá khóa thông tin đăng nhập cho các dịch vụ đang chạy
- `discovery` : Cố gắng truy vấn các dịch vụ đang chạy để biết thêm thông tin về mạng (ví dụ: truy vấn máy chủ SNMP).

Trong nhiệm vụ tiếp theo, chúng ta sẽ xem xét cách tương tác với NSE và sử dụng các tập lệnh trong các danh mục này.

> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
1. Các tập lệnh NSE được viết bằng ngôn ngữ nào?
2. Loại tập lệnh nào sẽ là ý tưởng rất tệ để chạy trong môi trường sản xuất?

  
---


## 🛠️ Cách giải

1. tệp lệnh NSE được viết bằng ngôn ngữ `lua`

2. 
```
intrusive
```

