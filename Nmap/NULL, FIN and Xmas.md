
# TryHackMe

## 🧩 Challenge: NULL,FIN and Xmas

## 📝 Description
Quét cổng **TCP NULL, FIN và Xmas** ít được sử dụng hơn bất kỳ loại nào khác mà chúng tôi đã đề cập, vì vậy chúng tôi sẽ không đi sâu vào chi tiết ở đây. Cả ba loại đều được liên kết với nhau và được sử dụng chủ yếu vì chúng có xu hướng "`Stealth`" hơn, nói một cách tương đối, so với quét "Stealth" Scan. Bắt đầu với quét NULL:

- Đúng như tên gọi, quét NULL (`-sN`) xảy ra khi yêu cầu TCP được gửi mà không có cờ nào được đặt. Theo RFC, máy chủ đích sẽ phản hồi bằng RST nếu cổng bị đóng.

<img width="1020" height="339" alt="image" src="https://github.com/user-attachments/assets/fbc546f7-f9ec-49e7-8cb7-f84f380e38e3" />

- Quét FIN (`-sF`) hoạt động gần như giống hệt nhau; tuy nhiên, thay vì gửi một gói tin hoàn toàn trống, một yêu cầu sẽ được gửi kèm cờ FIN (thường được dùng để đóng nhẹ nhàng một kết nối đang hoạt động). Một lần nữa, Nmap mong đợi một RST nếu cổng bị đóng.

<img width="1017" height="339" alt="image" src="https://github.com/user-attachments/assets/92af2ef7-4ea3-48ae-a10e-2da35fb9747b" />

- Giống như hai loại quét khác trong lớp này, quét Xmas (`-sX`) gửi một gói tin TCP bị lỗi và mong đợi phản hồi RST cho các cổng đã đóng. Nó được gọi là quét Xmas vì các cờ mà nó đặt (PSH, URG và FIN) khiến nó trông giống như một cây thông Noel nhấp nháy khi được xem như một gói tin bị bắt trong Wireshark.

<img width="1130" height="337" alt="image" src="https://github.com/user-attachments/assets/b3f79f33-51ed-4e14-9dd7-052779d4cfe1" />

Phản hồi dự kiến cho các cổng mở với các lần quét này cũng giống hệt nhau và rất giống với phản hồi của quét UDP. Nếu cổng mở thì sẽ không có phản hồi nào cho gói tin bị lỗi. Thật không may (cũng như với các cổng UDP mở), đây cũng là một hành vi dự kiến nếu cổng được bảo vệ bởi tường lửa, vì vậy các lần quét NULL, FIN và Xmas sẽ chỉ xác định các cổng là đang mở|đã lọc, đã đóng hoặc đã lọc. Nếu một cổng được xác định là đã lọc với một trong những lần quét này thì thường là do mục tiêu đã phản hồi bằng một gói tin ICMP không thể truy cập.

Cũng cần lưu ý rằng mặc dù RFC 793 yêu cầu các máy chủ mạng phản hồi các gói tin bị lỗi bằng gói tin RST TCP cho các cổng đã đóng, và không phản hồi gì cả đối với các cổng đang mở; nhưng điều này không phải lúc nào cũng đúng trong thực tế. Đặc biệt, Microsoft Windows (và rất nhiều thiết bị mạng Cisco) được biết là phản hồi bằng gói tin RST cho bất kỳ gói tin TCP bị lỗi nào -- bất kể cổng đó có thực sự mở hay không. Điều này dẫn đến tất cả các cổng đều hiển thị là đã đóng.

Tuy nhiên, mục tiêu ở đây tất nhiên là tránh tường lửa. Nhiều tường lửa được cấu hình để chặn các gói tin TCP đến các cổng bị chặn có cờ SYN được đặt (do đó chặn các yêu cầu khởi tạo kết nối mới). Bằng cách gửi các yêu cầu không chứa cờ SYN, chúng ta thực sự đã vượt qua được loại tường lửa này. Mặc dù về lý thuyết thì điều này tốt, nhưng hầu hết các giải pháp IDS hiện đại đều am hiểu các kiểu quét này, vì vậy đừng tin rằng chúng hiệu quả 100% khi xử lý các hệ thống hiện đại.


> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
1. Trong ba loại quét được hiển thị, loại nào sử dụng cờ URG?
2. Tại sao quét NULL, FIN và Xmas thường được sử dụng?
3. Hệ điều hành phổ biến nào có thể phản hồi quét NULL, FIN hoặc Xmas bằng RST cho mọi cổng?
---


## 🛠️ Cách giải

1. Trong TCP Xmas scan, 3 cờ URG, PUSH, FIN đều được bật — tạo nên hiệu ứng như "cây thông Noel".

2. NULL, FIN, và Xmas scans được thế kế để tránh **firewall** và **hệ thống IDS**

```
firewall evasion
```

4. Hệ điều hành Windows không tuân theo RFC 793 chuẩn, nên khi gặp các loại scan đặc biệt như NULL/FIN/Xmas, nó luôn trả về RST dù cổng mở hay đóng.

 

