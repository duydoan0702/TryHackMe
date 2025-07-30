
# TryHackMe

## 🧩 Challenge: UDP Scans

## 📝 Description
Không giống như TCP, kết nối UDP không có trạng thái. Điều này có nghĩa là, thay vì khởi tạo kết nối bằng một "bắt tay" qua lại, các kết nối UDP dựa vào việc gửi các gói tin đến một cổng đích và về cơ bản hy vọng rằng chúng sẽ đến đích. Điều này khiến UDP trở nên tuyệt vời cho các kết nối dựa trên **tốc độ hơn chất lượng** (ví dụ: chia sẻ video), nhưng việc thiếu xác nhận khiến UDP khó quét hơn đáng kể (và chậm hơn nhiều). Công tắc cho quét UDP của Nmap là (`-sU`).

Khi một gói tin được gửi đến một cổng **UDP đang mở**, sẽ không có phản hồi. Khi điều này xảy ra, Nmap sẽ coi cổng đó là `(open|filtered)`. Nói cách khác, nó nghi ngờ rằng cổng đó đang mở, nhưng có thể nó đã bị tường lửa chặn. Nếu nhận được phản hồi UDP (điều này rất hiếm khi xảy ra), thì cổng đó sẽ được đánh dấu là mở. Thông thường, nếu không có phản hồi, yêu cầu sẽ được gửi lại lần thứ hai để kiểm tra lại. Nếu vẫn không có phản hồi, cổng sẽ được đánh dấu là mở|đã lọc và Nmap sẽ tiếp tục.

Khi một gói tin được gửi đến một cổng **UDP đã đóng**, mục tiêu sẽ phản hồi bằng một gói ICMP (ping) chứa thông báo rằng cổng đó không thể truy cập được. Thông báo này sẽ xác định rõ ràng các cổng đã đóng, sau đó Nmap sẽ đánh dấu các cổng này là đã đóng và tiếp tục.

---

Do khó khăn trong việc xác định xem một cổng UDP có thực sự mở hay không, nên việc quét UDP thường **chậm hơn** đáng kể so với các loại quét TCP khác (mất khoảng **20 phút để quét 1000 cổng đầu tiên**, với kết nối tốt). Vì lý do này, việc chạy quét Nmap với tùy chọn `--top-ports <number>` thường là một phương pháp hay. Ví dụ: quét với nmap `-sU --top-ports 20 <target>`. Lệnh này sẽ quét 20 cổng UDP được sử dụng phổ biến nhất, giúp rút ngắn thời gian quét xuống mức chấp nhận được.

<img width="626" height="474" alt="image" src="https://github.com/user-attachments/assets/c00d45d8-4d2f-43e8-bdab-57e794b98f6e" />


---

Khi quét các cổng UDP, Nmap thường gửi các yêu cầu hoàn toàn trống - chỉ là các gói UDP thô. Tuy nhiên, đối với các cổng thường bị chiếm dụng bởi các dịch vụ quen thuộc, nó sẽ gửi một tải trọng giao thức cụ thể, có nhiều khả năng tạo ra phản hồi từ đó có thể rút ra kết quả chính xác hơn.

> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
1. Nếu cổng UDP không phản hồi khi quét Nmap, cổng đó sẽ được đánh dấu là gì?
2. Khi một cổng UDP bị đóng, theo quy ước, mục tiêu sẽ gửi lại thông báo "port unreachable". Giao thức nào sẽ được sử dụng để thực hiện việc này?

---


## 🛠️ Cách giải

1.

```
open|filtered
```

2.

```
ICMP
```

- UDP là giao thức không kết nối nên khi bạn gửi gói UDP đến một cổng không mở, sẽ không có phản hồi từ chính giao thức UDP.

- Tuy nhiên, để báo lỗi, hệ thống đích sẽ gửi một gói ICMP (Internet Control Message Protocol) loại "Destination Unreachable – Port Unreachable" quay lại.

- Đây là cách mà Nmap UDP scan (-sU) có thể phát hiện cổng UDP nào đóng.
