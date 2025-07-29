
# TryHackMe

## 🧩 Challenge: Introduction

## 📝 Description
Khi nói đến hack, kiến thức là sức mạnh. Càng hiểu biết về hệ thống hoặc mạng mục tiêu, bạn càng có nhiều lựa chọn. Điều này khiến việc liệt kê chính xác trước khi thực hiện bất kỳ nỗ lực khai thác nào là bắt buộc.

Giả sử chúng ta được cung cấp một địa chỉ IP (hoặc nhiều địa chỉ IP) để thực hiện kiểm tra bảo mật. Trước khi làm bất cứ điều gì khác, chúng ta cần nắm được "bối cảnh" mà mình đang tấn công. Điều này có nghĩa là chúng ta cần xác định những dịch vụ nào đang chạy trên các mục tiêu. Ví dụ: có thể một trong số chúng đang chạy máy chủ web, và một dịch vụ khác đang hoạt động như Bộ điều khiển miền Active Directory của Windows. Giai đoạn đầu tiên trong việc thiết lập "bản đồ" bối cảnh này là quét cổng. Khi máy tính chạy dịch vụ mạng, nó sẽ mở một cấu trúc mạng gọi là "cổng" để nhận kết nối. Cổng là cần thiết để thực hiện nhiều yêu cầu mạng hoặc cung cấp nhiều dịch vụ. Ví dụ: khi bạn tải nhiều trang web cùng lúc trong trình duyệt web, chương trình phải có cách nào đó để xác định tab nào đang tải trang web nào. Điều này được thực hiện bằng cách thiết lập kết nối đến các máy chủ web từ xa bằng các cổng khác nhau trên máy cục bộ của bạn. Tương tự, nếu bạn muốn một máy chủ có thể chạy nhiều dịch vụ (ví dụ: có thể bạn muốn máy chủ web của mình chạy cả phiên bản HTTP và HTTPS của trang web), thì bạn cần một số cách để chuyển hướng lưu lượng truy cập đến dịch vụ phù hợp. Một lần nữa, cổng chính là giải pháp cho vấn đề này. Kết nối mạng được thực hiện giữa hai cổng - một cổng mở đang lắng nghe trên máy chủ và một cổng được chọn ngẫu nhiên trên máy tính của bạn. Ví dụ: khi bạn kết nối đến một trang web, máy tính của bạn có thể mở cổng 49534 để kết nối với cổng 443 của máy chủ.


<img width="579" height="543" alt="image" src="https://github.com/user-attachments/assets/b3080b89-3a9b-415f-ac4e-21fa33de930e" />

Như trong ví dụ trước, sơ đồ cho thấy điều gì xảy ra khi bạn kết nối với nhiều trang web cùng lúc. Máy tính của bạn sẽ mở một cổng khác, được đánh số cao (ngẫu nhiên), cổng này được sử dụng cho tất cả các giao tiếp với máy chủ từ xa.

Mỗi máy tính có tổng cộng 65535 cổng khả dụng; tuy nhiên, nhiều cổng trong số này được đăng ký là cổng tiêu chuẩn. Ví dụ: Dịch vụ web HTTP gần như luôn có thể được tìm thấy trên cổng 80 của máy chủ. Dịch vụ web HTTPS có thể được tìm thấy trên cổng 443. Windows NETBIOS có thể được tìm thấy trên cổng 139 và SMB có thể được tìm thấy trên cổng 445. Tuy nhiên, điều quan trọng cần lưu ý là, đặc biệt là trong cài đặt CTF, việc thay đổi ngay cả những cổng tiêu chuẩn này không phải là chưa từng xảy ra, khiến việc chúng ta thực hiện liệt kê phù hợp trên mục tiêu càng trở nên cấp thiết hơn.

Nếu chúng ta không biết máy chủ đang mở cổng nào trong số này, thì chúng ta sẽ không có hy vọng tấn công thành công vào mục tiêu; do đó, điều quan trọng là phải bắt đầu bất kỳ cuộc tấn công nào bằng cách quét cổng. Điều này có thể được thực hiện theo nhiều cách khác nhau – thường là sử dụng một công cụ gọi là nmap, đây là trọng tâm của phòng này. Nmap có thể được sử dụng để thực hiện nhiều loại quét cổng khác nhau – phổ biến nhất trong số này sẽ được giới thiệu trong các nhiệm vụ sắp tới; tuy nhiên, lý thuyết cơ bản là như sau: nmap sẽ lần lượt kết nối với từng cổng của mục tiêu. Tùy thuộc vào cách cổng phản hồi, nó có thể được xác định là đang mở, đóng hoặc bị lọc (thường bằng tường lửa). Khi đã biết cổng nào đang mở, chúng ta có thể xem xét việc liệt kê những dịch vụ nào đang chạy trên mỗi cổng – theo cách thủ công hoặc phổ biến hơn là sử dụng nmap.

Vậy, tại sao lại là nmap? Câu trả lời ngắn gọn là vì hiện tại nó là tiêu chuẩn công nghiệp vì một lý do: không có công cụ quét cổng nào khác có chức năng tương đương (mặc dù một số công cụ mới hiện đang sánh ngang về tốc độ). Đây là một công cụ cực kỳ mạnh mẽ – thậm chí còn mạnh mẽ hơn nhờ công cụ viết kịch bản có thể được sử dụng để quét lỗ hổng bảo mật, và trong một số trường hợp, thậm chí còn thực hiện khai thác trực tiếp! Một lần nữa, điều này sẽ được đề cập chi tiết hơn trong các bài viết sắp tới.

Trước mắt, điều quan trọng là bạn phải hiểu: quét cổng là gì; tại sao cần thiết; và nmap là công cụ được lựa chọn cho bất kỳ loại liệt kê ban đầu nào.


> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
- 1.Cấu trúc mạng nào được sử dụng để chuyển hướng lưu lượng đến đúng ứng dụng trên máy chủ?
- 2. Có bao nhiêu trong số những tính năng này có sẵn trên bất kỳ máy tính nào có kết nối mạng?
- 3. Có bao nhiêu trong số này được coi là "well-Known"? (Đây là những con số "chuẩn" được đề cập trong nhiệm vụ)
  
---


## 🛠️ Cách giải

1. Trong cấu trúc mạng người ta dùng `port` để định tuyến lưu lượng đến ứng dụng trên máy chủ

```
ports
```

2. Có `65535` port khả dụng trên mỗi máy tính có kết nối mạng.

3. **Well-knowns ports** là các cổng có số từ 0 đến 1023.
- Các port phổ biến :

| Port | Service |
|------|---------|
| 21   | FTP     |
| 22   | SSH     |
| 25   | SMTP    |
| 53   | DNS     |
| 80   | HTTP    |
| 443  | HTTPS   |





