
# TryHackMe

## 🧩 Challenge: Introduction

## 📝 Description
Khi nói đến hack, kiến thức là sức mạnh. Càng hiểu biết về hệ thống hoặc mạng mục tiêu, bạn càng có nhiều lựa chọn. Điều này khiến việc liệt kê chính xác trước khi thực hiện bất kỳ nỗ lực khai thác nào là bắt buộc.

Giả sử chúng ta được cung cấp một địa chỉ IP (hoặc nhiều địa chỉ IP) để thực hiện kiểm tra bảo mật. Trước khi làm bất cứ điều gì khác, chúng ta cần nắm được "bối cảnh" mà mình đang tấn công. Điều này có nghĩa là chúng ta cần xác định những dịch vụ nào đang chạy trên các mục tiêu. Ví dụ: có thể một trong số chúng đang chạy máy chủ web, và một dịch vụ khác đang hoạt động như Bộ điều khiển miền Active Directory của Windows. Giai đoạn đầu tiên trong việc thiết lập "bản đồ" bối cảnh này là quét cổng. Khi máy tính chạy dịch vụ mạng, nó sẽ mở một cấu trúc mạng gọi là "cổng" để nhận kết nối. Cổng là cần thiết để thực hiện nhiều yêu cầu mạng hoặc cung cấp nhiều dịch vụ. Ví dụ: khi bạn tải nhiều trang web cùng lúc trong trình duyệt web, chương trình phải có cách nào đó để xác định tab nào đang tải trang web nào. Điều này được thực hiện bằng cách thiết lập kết nối đến các máy chủ web từ xa bằng các cổng khác nhau trên máy cục bộ của bạn. Tương tự, nếu bạn muốn một máy chủ có thể chạy nhiều dịch vụ (ví dụ: có thể bạn muốn máy chủ web của mình chạy cả phiên bản HTTP và HTTPS của trang web), thì bạn cần một số cách để chuyển hướng lưu lượng truy cập đến dịch vụ phù hợp. Một lần nữa, cổng chính là giải pháp cho vấn đề này. Kết nối mạng được thực hiện giữa hai cổng - một cổng mở đang lắng nghe trên máy chủ và một cổng được chọn ngẫu nhiên trên máy tính của bạn. Ví dụ: khi bạn kết nối đến một trang web, máy tính của bạn có thể mở cổng 49534 để kết nối với cổng 443 của máy chủ.

<img width="579" height="543" alt="image" src="https://github.com/user-attachments/assets/b3080b89-3a9b-415f-ac4e-21fa33de930e" />


> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Chiến lược giải
- 
  
## 🔧 Công cụ
1. **openvpn**

---


## 🛠️ Cách giải

1. 
