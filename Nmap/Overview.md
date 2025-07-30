
# TryHackMe

## 🧩 Challenge: Overview

## 📝 Description
Khi quét cổng bằng Nmap, có ba kiểu quét cơ bản. Đó là:

- Quét Kết nối TCP (-sT)
- Quét "Nửa mở" SYN (-sS)
- Quét UDP (-sU)

Ngoài ra còn có một số kiểu quét cổng ít phổ biến hơn, một số trong đó chúng tôi cũng sẽ đề cập (mặc dù ít chi tiết hơn). Đó là:

- Quét TCP Null (-sN)
- Quét TCP FIN (-sF)
- Quét TCP Xmas (-sX)

Hầu hết các kiểu quét này (ngoại trừ quét UDP) được sử dụng cho các mục đích rất giống nhau, tuy nhiên, cách thức hoạt động của chúng khác nhau giữa các lần quét. Điều này có nghĩa là, mặc dù một trong ba kiểu quét đầu tiên có thể là lựa chọn hàng đầu của bạn trong hầu hết các trường hợp, nhưng cần lưu ý rằng vẫn còn các kiểu quét khác.

Về quét mạng, chúng ta cũng sẽ xem xét sơ qua về quét ICMP (hay "ping").



> Link: https://tryhackme.com/room/furthernmap


---


## 🛠️ Cách giải

1. Quét kết nối TCP
   
