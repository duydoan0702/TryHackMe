
# TryHackMe

## 🧩 Challenge: Practical

## 📝 Description

Hãy vận dụng những kiến thức đã học để quét máy mục tiêu và trả lời các câu hỏi sau!

Địa chỉ IP của máy ảo (VM) bạn đã bật trong Nhiệm vụ 1 là 10.201.119.41

(Lưu ý: Nếu bạn chưa đăng ký, hãy đảm bảo máy này đã khởi động được khoảng mười phút)

> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
1. Địa chỉ IP đích có phản hồi yêu cầu ICMP echo (ping) không (Có/Không)?

2. Thực hiện quét Xmas trên 999 cổng đầu tiên của mục tiêu -- có bao nhiêu cổng được hiển thị là đang mở hoặc được lọc?

3. Có một lý do được đưa ra cho việc này -- đó là gì?

Lưu ý: Câu trả lời sẽ có trong kết quả quét của bạn. Hãy suy nghĩ kỹ về việc nên sử dụng công tắc nào -- và đọc kỹ gợi ý trước khi yêu cầu trợ giúp!

4. Thực hiện quét TCP SYN trên 5000 cổng đầu tiên của mục tiêu -- có bao nhiêu cổng được hiển thị là đang mở?

5. Mở Wireshark (xem hướng dẫn tại Wireshark Room của Cryillic) và thực hiện quét TCP Connect trên cổng 80 của mục tiêu, đồng thời theo dõi kết quả. Đảm bảo bạn hiểu rõ những gì đang diễn ra. Triển khai tập lệnh ftp-anon trên hộp. Nmap có thể đăng nhập thành công vào máy chủ FTP trên cổng 21 không? (Có/Không)

---


## 🛠️ Cách giải

1. Địa chỉ IP không phải hồi yêu cầu ICMP nên ta `-Pn` để bỏ qua lệnh ping



