
# TryHackMe

## 🧩 Challenge: TCP Connect Scans

## 📝 Description
Để hiểu về quét TCP Connect (-sT), điều quan trọng là bạn phải quen thuộc với bắt tay ba bước TCP. Nếu thuật ngữ này còn mới với bạn, bạn nên hoàn thành bài học Mạng cơ bản trước khi tiếp tục.

Tóm tắt lại, bắt tay ba bước bao gồm ba giai đoạn. Đầu tiên, thiết bị đầu cuối kết nối (trong trường hợp này là máy tấn công của chúng ta) gửi một yêu cầu TCP đến máy chủ mục tiêu với cờ SYN được đặt. Sau đó, máy chủ xác nhận gói tin này bằng một phản hồi TCP chứa cờ SYN, cũng như cờ ACK. Cuối cùng, thiết bị đầu cuối của chúng ta hoàn tất quá trình bắt tay bằng cách gửi một yêu cầu TCP với cờ ACK được đặt.

<img width="272" height="234" alt="image" src="https://github.com/user-attachments/assets/d4f755e0-7a7c-496c-8fcf-59a901662828" />

<img width="1138" height="69" alt="image" src="https://github.com/user-attachments/assets/14671a2e-7289-46b7-95f0-0657896e0cea" />


Đây là một trong những nguyên tắc cơ bản của mạng TCP/IP, nhưng nó liên quan như thế nào đến Nmap?

Đúng như tên gọi, quét TCP Connect hoạt động bằng cách thực hiện bắt tay ba chiều với từng cổng đích. Nói cách khác, Nmap cố gắng kết nối với từng cổng TCP được chỉ định và xác định xem dịch vụ có mở hay không bằng phản hồi mà nó nhận được.

Ví dụ: nếu một cổng bị đóng, RFC 9293 quy định rằng:

"... Nếu kết nối không tồn tại (ĐÃ ĐÓNG), thì một lệnh đặt lại sẽ được gửi để phản hồi bất kỳ phân đoạn nào đến ngoại trừ một lệnh đặt lại khác. Một phân đoạn SYN không khớp với kết nối hiện có sẽ bị từ chối theo cách này."

Nói cách khác, nếu Nmap gửi một yêu cầu TCP với cờ SYN được đặt thành một cổng đã đóng, máy chủ đích sẽ phản hồi bằng một gói tin TCP với cờ RST (Đặt lại) được đặt. Bằng phản hồi này, Nmap có thể xác định rằng cổng đã đóng.

<img width="262" height="229" alt="image" src="https://github.com/user-attachments/assets/ef9c830c-5d19-4d83-9875-b458bea89d7b" />

Tuy nhiên, nếu yêu cầu được gửi đến một cổng mở, mục tiêu sẽ phản hồi bằng một gói tin TCP với cờ SYN/ACK được đặt. Sau đó, Nmap đánh dấu cổng này là đang mở (và hoàn tất quá trình bắt tay bằng cách gửi lại một gói tin TCP với cờ ACK được đặt).

Điều này hoàn toàn ổn, tuy nhiên, vẫn còn một khả năng thứ ba.

Điều gì sẽ xảy ra nếu cổng đang mở nhưng bị ẩn sau tường lửa?

Nhiều tường lửa được cấu hình để loại bỏ các gói tin đến. Nmap gửi một yêu cầu TCP SYN và không nhận được phản hồi nào. Điều này cho thấy cổng đang được tường lửa bảo vệ và do đó cổng được coi là đã bị lọc.

Tuy nhiên, việc cấu hình tường lửa để phản hồi bằng một gói tin TCP RST rất dễ dàng. Ví dụ: trong IPtables cho Linux, một phiên bản đơn giản của lệnh sẽ như sau:

```
iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset
```

Điều này có thể khiến việc đọc chính xác mục tiêu trở nên cực kỳ khó khăn (nếu không muốn nói là không thể).


> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
1. RFC nào định nghĩa hành vi thích hợp cho giao thức TCP?
2. Nếu một cổng bị đóng, máy chủ sẽ gửi cờ nào để chỉ ra điều này?

---


## 🛠️ Cách giải

1. RFC 9293 là tài liệu gốc định nghĩa giao thức TCP ( Tranmission Control Protocol )

```
RFC 9293
```

2. Nếu một gói `TCP SYN` gửi đến một cổng đóng, máy chủ sẽ phản hồi bằng một gói có cờ `RST` để từ chối.
