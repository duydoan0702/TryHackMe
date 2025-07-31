
# TryHackMe

## 🧩 Challenge: Working with the NSE

## 📝 Description
Trong Bài tập 3, chúng ta đã xem xét sơ qua lệnh `--script` để kích hoạt các tập lệnh NSE từ danh mục `vuln` bằng cách sử dụng `--script=vuln`. Không có gì ngạc nhiên khi các danh mục khác hoạt động theo cùng một cách. Nếu lệnh `--script=safe` được chạy, thì bất kỳ tập lệnh an toàn nào phù hợp sẽ được chạy trên mục tiêu (Lưu ý: chỉ các tập lệnh nhắm mục tiêu đến một dịch vụ đang hoạt động mới được kích hoạt).

---

Để chạy một tập lệnh cụ thể, chúng ta sẽ sử dụng `--script=<script-name>`, ví dụ: `--script=http-fileupload-exploiter`.

Có thể chạy đồng thời nhiều tập lệnh theo cách này bằng cách phân tách chúng bằng dấu phẩy. Ví dụ: `--script=smb-enum-users,smb-enum-shares`.

Một số tập lệnh yêu cầu các đối số (ví dụ: thông tin đăng nhập, nếu chúng đang khai thác lỗ hổng đã được xác thực). Những thông số này có thể được cung cấp bằng lệnh `--script-args` của Nmap. Một ví dụ về điều này là tập lệnh `http-put` (được sử dụng để tải tệp lên bằng phương thức PUT). Lệnh này cần hai đối số: URL để tải tệp lên và vị trí của tệp trên ổ đĩa. Ví dụ:

`nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'`

Lưu ý rằng các đối số được phân tách bằng dấu phẩy và được kết nối với tập lệnh tương ứng bằng dấu chấm (ví dụ: `<script-name>.<argument>`).

---

Các tập lệnh Nmap được tích hợp sẵn menu trợ giúp, có thể truy cập bằng lệnh `nmap --script-help <script-name>`. Mặc dù không đầy đủ như liên kết ở trên, nhưng nó vẫn hữu ích khi làm việc cục bộ.







> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ

1. Tập lệnh `ftp-anon.nse` có thể sử dụng đối số tùy chọn nào?
---


## 🛠️ Cách giải

1. `ftp-anon.nse` là một script của Nmap dùng để kiểm tra đăng nhập ẩn danh (anonymous login) trên máy chủ FTP.

```
maxlist
```

<img width="776" height="203" alt="image" src="https://github.com/user-attachments/assets/a76af22f-1745-49c4-b065-e705b46e1fd4" />

| Thông tin                              | Chi tiết                                                                 |
|----------------------------------------|-------------------------------------------------------------------------|
| `21/tcp open ftp`                      | Cổng 21 đang mở và đang chạy dịch vụ FTP                               |
| `Anonymous FTP login allowed (FTP code 230)` | Cho phép đăng nhập anonymous (với mã thành công 230)                     |
| `Can't get directory listing: TIMEOUT` | Đăng nhập được, nhưng không thể liệt kê thư mục do **timeout** (hết thời gian chờ) |



