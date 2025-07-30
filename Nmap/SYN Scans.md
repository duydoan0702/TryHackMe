
# TryHackMe

## 🧩 Challenge: SYN Scans

## 📝 Description
Tương tự như quét TCP, quét SYN (-sS) được sử dụng để quét phạm vi cổng TCP của một hoặc nhiều mục tiêu; tuy nhiên, hai loại quét này hoạt động hơi khác nhau. Quét SYN đôi khi được gọi là quét "Half-open (Nửa mở)" hoặc quét "Stealth (Tàng hình)".

Trong khi quét TCP thực hiện bắt tay ba chiều đầy đủ với mục tiêu, quét SYN gửi lại một gói tin **RST TCP** sau khi nhận được SYN/ACK từ máy chủ (điều này ngăn máy chủ lặp lại yêu cầu). Nói cách khác, trình tự quét một cổng mở trông như sau:

<img width="272" height="234" alt="image" src="https://github.com/user-attachments/assets/9301b296-1a46-4d0f-9bec-2fe9d74536e7" />

<img width="1138" height="69" alt="image" src="https://github.com/user-attachments/assets/89e42a7e-2976-4019-b801-5bbdc2f0d108" />

**Điều này mang lại nhiều lợi ích cho chúng ta với tư cách là hacker:**

- Nó có thể được sử dụng để vượt qua các hệ thống Phát hiện Xâm nhập cũ hơn khi chúng tìm kiếm một giao thức bắt tay ba chiều đầy đủ. Điều này thường không còn đúng với các giải pháp IDS hiện đại; chính vì lý do này mà quét SYN vẫn thường được gọi là quét "ẩn".
- Quét SYN thường không được ghi lại bởi các ứng dụng đang lắng nghe trên các cổng mở, vì thông lệ thông thường là ghi lại kết nối sau khi nó đã được thiết lập đầy đủ. Một lần nữa, điều này phù hợp với ý tưởng quét SYN là ẩn.
- Không cần phải bận tâm đến việc hoàn tất (và ngắt kết nối) một giao thức bắt tay ba chiều cho mỗi cổng, quét SYN nhanh hơn đáng kể so với quét TCP Connect tiêu chuẩn.

**Tuy nhiên, quét SYN có một vài nhược điểm, cụ thể là:**

- Chúng yêu **cầu quyền sudo** để hoạt động chính xác trong Linux. Điều này là do quét SYN yêu cầu khả năng tạo các gói tin thô (trái ngược với giao thức bắt tay TCP đầy đủ), đây là đặc quyền mặc định chỉ dành cho người dùng root.
- Các dịch vụ không ổn định đôi khi bị hạ cấp bởi quét SYN, điều này có thể gây ra vấn đề nếu máy khách đã cung cấp môi trường sản xuất cho thử nghiệm.

Nhìn chung, ưu điểm vượt trội hơn nhược điểm.

Vì lý do này, quét SYN là quét mặc định được Nmap sử dụng nếu chạy với quyền sudo. Nếu chạy mà không có quyền sudo, Nmap sẽ mặc định sử dụng quét TCP Connect mà chúng ta đã thấy trong tác vụ trước.

Khi sử dụng quét SYN để xác định các cổng đã đóng và đã lọc, các quy tắc giống hệt như quét TCP Connect được áp dụng.

Nếu một cổng đã đóng, máy chủ sẽ phản hồi bằng gói tin RST TCP. Nếu cổng bị tường lửa lọc, gói tin TCP SYN sẽ bị loại bỏ hoặc bị giả mạo bằng cách đặt lại TCP.

Về mặt này, hai lần quét là giống hệt nhau: sự khác biệt lớn nằm ở cách chúng xử lý các cổng mở.

Quét SYN cũng có thể hoạt động bằng cách cung cấp cho Nmap các khả năng CAP_NET_RAW, CAP_NET_ADMIN và CAP_NET_BIND_SERVICE; tuy nhiên, điều này có thể không cho phép nhiều tập lệnh NSE chạy đúng cách.




> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ

1. Có hai tên gọi khác của quét SYN, đó là gì?
2. Nmap có thể sử dụng quét SYN mà không cần quyền Sudo (Y/N)?
---


## 🛠️ Cách giải

1.
```
Half-open, Stealth
```

2. Nmap yêu cầu quyền `sudo` để chạy được.
