
# TryHackMe

## 🧩 Challenge: Firewall Evasion

## 📝 Description
Chúng ta đã thấy một số kỹ thuật để vượt tường lửa (ví dụ như quét ẩn, cùng với quét **NULL, FIN và Xmas**); tuy nhiên, có một cấu hình tường lửa rất phổ biến khác mà chúng ta bắt buộc phải biết cách vượt tường lửa.

Máy chủ Windows thông thường của bạn, với tường lửa mặc định, sẽ chặn tất cả các gói tin `ICMP`. Điều này gây ra một vấn đề: chúng ta không chỉ thường sử dụng lệnh ping để thiết lập thủ công hoạt động của mục tiêu, mà Nmap cũng làm điều tương tự theo mặc định. Điều này có nghĩa là Nmap sẽ ghi nhận một máy chủ có cấu hình tường lửa này là đã chết và không cần quét nó nữa.

Vì vậy, chúng ta cần một cách để vượt qua cấu hình này. May mắn thay, Nmap cung cấp một tùy chọn cho việc này: `-Pn`, tùy chọn này yêu cầu Nmap không cần ping máy chủ trước khi quét. Điều này có nghĩa là Nmap sẽ luôn coi máy chủ mục tiêu là còn sống, do đó **bỏ qua lệnh chặn ICMP**; tuy nhiên, cái giá phải trả là quá trình quét có thể **mất rất nhiều thời gian** (nếu máy chủ thực sự đã chết thì Nmap vẫn sẽ kiểm tra và kiểm tra lại mọi cổng được chỉ định).

Điều đáng chú ý là nếu bạn đã trực tiếp ở trên mạng cục bộ, Nmap cũng có thể sử dụng yêu cầu ARP để xác định hoạt động của máy chủ.

---

Có nhiều loại switch khác mà Nmap cho là hữu ích để tránh tường lửa. Chúng tôi sẽ không đi sâu vào chi tiết, tuy nhiên, bạn có thể tìm thấy chúng tại đây.

Các switch sau đây đặc biệt đáng chú ý:

`-f` : Được sử dụng để phân mảnh các gói tin (tức là chia chúng thành các phần nhỏ hơn) giúp giảm khả năng các gói tin bị tường lửa hoặc IDS phát hiện.

Một lựa chọn thay thế cho `-f`, nhưng cung cấp khả năng kiểm soát kích thước của các gói tin tốt hơn: `--mtu <number>`, chấp nhận kích thước đơn vị truyền tối đa để sử dụng cho các gói tin được gửi. Kích thước này phải là bội số của 8.
`--scan-delay <time>ms` : được sử dụng để thêm độ trễ giữa các gói tin được gửi. Điều này rất hữu ích nếu mạng không ổn định, nhưng cũng để tránh bất kỳ kích hoạt tường lửa/IDS dựa trên thời gian nào có thể xảy ra.
`--badsum` : được sử dụng để tạo tổng kiểm tra không hợp lệ cho các gói tin. Bất kỳ ngăn xếp TCP/IP thực tế nào cũng sẽ loại bỏ gói tin này, tuy nhiên, tường lửa có khả năng tự động phản hồi mà không cần kiểm tra tổng kiểm tra của gói tin. Do đó, công tắc này có thể được sử dụng để xác định sự hiện diện của tường lửa/IDS.

> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
1. Giao thức đơn giản nào (và thường được tin cậy) thường bị chặn, yêu cầu sử dụng công tắc `-Pn` ?
2. [Nghiên cứu] Công tắc Nmap nào cho phép bạn thêm một lượng dữ liệu ngẫu nhiên tùy ý vào cuối các gói tin?  

---


## 🛠️ Cách giải
1.
```
ICMP
```
- ICMP (Internet Control Message Protocol) là giao thức được sử dụng trong lệnh ping để kiểm tra xem host có đang hoạt động hay không.

- Tuy nhiên, nhiều tường lửa hoặc thiết bị bảo mật chặn ICMP để ngăn quét mạng.

- Khi ICMP bị chặn, Nmap sẽ cho rằng host “không hoạt động”, mặc dù nó vẫn đang hoạt động. Do đó, bạn cần dùng tuỳ chọn `-Pn`

2.
```
--data-length
```

- Tham số `--data-length <number>` cho phép bạn thêm một lượng dữ liệu ngẫu nhiên vào cuối gói tin, giúp:

    - Tránh phát hiện bởi IDS/IPS.

    - Gây khó khăn cho các hệ thống phát hiện chữ ký tấn công.
