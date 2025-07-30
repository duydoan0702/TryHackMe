
# TryHackMe

## 🧩 Challenge: Nmap Switches

## 📝 Description
Giống như hầu hết các công cụ kiểm thử thâm nhập, **Nmap** được chạy từ **terminal**. Có các phiên bản dành cho cả Windows và Linux. Trong bài này, chúng tôi giả định bạn đang sử dụng Linux; tuy nhiên, các lệnh switch phải giống hệt nhau. Nmap được cài đặt mặc định trong cả Kali Linux và TryHackMe Attack Box.

Có thể truy cập Nmap bằng cách nhập nmap vào dòng lệnh terminal, theo sau là một số **lệnh switch** (các đối số lệnh cho phép chương trình thực hiện các tác vụ khác nhau) mà chúng tôi sẽ đề cập bên dưới.

Tất cả những gì bạn cần là menu trợ giúp của nmap (truy cập bằng lệnh `nmap -h`) và/hoặc trang hướng dẫn sử dụng nmap (truy cập bằng lệnh `man nmap`). Đối với mỗi câu trả lời, hãy bao gồm tất cả các phần của lệnh switch trừ khi có quy định khác. Bao gồm cả dấu gạch nối (-) ở đầu câu trả lời.

> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
1. Công tắc đầu tiên được liệt kê trong menu trợ giúp cho `Syn Scan` là gì (sẽ nói thêm về điều này sau!)?
2. Bạn sẽ sử dụng công tắc nào để "Scan UDP"?
3. Nếu bạn muốn phát hiện hệ điều hành mà mục tiêu đang chạy, bạn sẽ sử dụng công tắc nào?
4. Nmap cung cấp một công tắc để phát hiện phiên bản của các dịch vụ đang chạy trên mục tiêu. Công tắc này là gì?
5. Đầu ra mặc định do nmap cung cấp thường không cung cấp đủ thông tin cho người kiểm thử thâm nhập. Làm thế nào để tăng độ chi tiết?
6. Mức độ chi tiết một thì tốt, nhưng mức độ chi tiết hai thì tốt hơn! Làm thế nào để thiết lập mức độ chi tiết hai?
**(Lưu ý: nên luôn sử dụng ít nhất tùy chọn này)**
7. Chúng ta nên luôn lưu kết quả quét điều này có nghĩa là chúng ta chỉ cần chạy quét một lần (giảm lưu lượng mạng và do đó giảm khả năng bị phát hiện), đồng thời cung cấp cho chúng ta một tham chiếu để sử dụng khi viết báo cáo cho khách hàng.
Bạn sẽ sử dụng công tắc nào để lưu kết quả nmap ở ba định dạng chính?
8. Bạn sẽ sử dụng công tắc nào để lưu kết quả nmap ở định dạng "normal"?

9. Một định dạng đầu ra rất hữu ích: làm thế nào để lưu kết quả theo định dạng "grepable"?
10. Đôi khi kết quả chúng ta nhận được vẫn chưa đủ. Nếu không quan tâm đến mức độ ồn ào, chúng ta có thể bật chế độ "aggressive". Đây là một công tắc tắt để kích hoạt phát hiện dịch vụ, phát hiện hệ điều hành, theo dõi tuyến đường và quét tập lệnh phổ biến.

Bạn sẽ kích hoạt cài đặt này như thế nào?

11. Nmap cung cấp năm cấp độ mẫu "thời gian". Về cơ bản, chúng được sử dụng để tăng tốc độ quét. Tuy nhiên, hãy cẩn thận: tốc độ cao hơn sẽ gây nhiễu và có thể phát sinh lỗi!

Làm thế nào để thiết lập mẫu thời gian ở cấp độ 5?

12. Làm thế nào để kích hoạt một tập lệnh từ thư viện tập lệnh nmap (sẽ nói thêm về điều này sau!)?

13.   Bạn sẽ kích hoạt tất cả các tập lệnh trong danh mục "lỗ hổng" như thế nào?
    
## 🔧 Công cụ
1. **openvpn**

---


## 🛠️ Cách giải

1. **Syn Scan** Là một loại quét phổ biến của Nmap (gọi là TCP SYN Scan)

```
-sS
```

2. Quét UDP ta sử dụng switch `-sU` , UDP không có handshake như TCP nên kết quả thường chậm hơn và ít chính xác hơn.

3. Để phát hiện hệ điều hành ta dùng switch `-O`

4. Để phát hiện dichj vụ ta dùng `-sV`

5. Để tăng mức độ chi tiết (verbosity) thấy được nhiều thông tin hơn, ta dùng: `-v`

6. Để sử dụng mức độ chi tiết level 2, ta dùng: `-vv`

7. Dùng `-oA <filename>` để xuất kết quả ở 3 định dạng chính.
- Normal (`.nnam`)
- Grepable (`.gmap`)
- XML(`.xml`)

8. Xuất kết quả ở dạng normal, ta dùng: `-oN`

9. Xuất kết quả ở dạng grepable, ta dùng: `-oG`

10. Aggressive mode bật các tính năng như: phát hiện dịch vụ `-sV`, phát hiện hệ điều hành `-O`, truy vết đường đi `--traceroute` , và quét script mặc định `-sC`.

```
-A
```

11. Nmap có 6 cấp độ thời gian từ `T0` đến `T5`. Cấp 5 là nhanh nhất

```
-T5
```

12. Nmap có một thư viện các script sẵn gọi là NSE (Nmap Scripting Engine).
Để chạy một script cụ thể, ta dùng tuỳ chọn --script=<script-name>.

```
--script
```
13.  Mỗi script trong NSE được gắn với một hoặc nhiều category như auth, default, vuln, discovery

```
--script=vuln
```



