
# TryHackMe

## 🧩 Challenge: Searching for Scripts

## 📝 Description
Được rồi, vậy là chúng ta đã biết cách sử dụng các tập lệnh trong Nmap, nhưng vẫn chưa biết cách tìm các tập lệnh này.

Chúng ta có hai lựa chọn cho việc này, ý tưởng nhất là nên sử dụng kết hợp với nhau. Lựa chọn đầu tiên là trang trên trang web Nmap (đã đề cập trong nhiệm vụ trước) chứa danh sách tất cả các tập lệnh chính thức. Lựa chọn thứ hai là bộ nhớ cục bộ trên máy tính tấn công của bạn. Nmap lưu trữ các tập lệnh của mình trên Linux tại `/usr/share/nmap/scripts`. Tất cả các tập lệnh NSE được lưu trữ trong thư mục này theo mặc định đây là nơi Nmap tìm kiếm các tập lệnh khi bạn chỉ định chúng.

Có hai cách để tìm kiếm các tập lệnh đã cài đặt. Một là sử dụng tệp `/usr/share/nmap/scripts/script.db`. Mặc dù có phần mở rộng, nhưng đây thực chất không phải là một cơ sở dữ liệu mà là một tệp văn bản được định dạng chứa tên tệp và danh mục cho từng tập lệnh khả dụng.

<img width="729" height="231" alt="image" src="https://github.com/user-attachments/assets/05357183-5bbe-4a0c-b7fb-04da513d029f" />



Nmap sử dụng tệp này để theo dõi (và sử dụng) các tập lệnh cho công cụ tạo tập lệnh; tuy nhiên, chúng ta cũng có thể grep thông qua tệp này để tìm kiếm các tập lệnh. Ví dụ: `grep "ftp" /usr/share/nmap/scripts/script.db.`

<img width="928" height="179" alt="image" src="https://github.com/user-attachments/assets/1a8a84f8-fd6b-43b5-a875-e6b1f65e99f7" />


Cách thứ hai để tìm kiếm tập lệnh khá đơn giản là sử dụng lệnh ls. Ví dụ, chúng ta có thể nhận được kết quả tương tự như trong ảnh chụp màn hình trước bằng cách sử dụng lệnh `ls -l /usr/share/nmap/scripts/*ftp*`:

<img width="728" height="181" alt="image" src="https://github.com/user-attachments/assets/3106cf9d-6992-4879-8ed5-10b1b8c01e91" />





<img width="766" height="196" alt="image" src="https://github.com/user-attachments/assets/8d59e07e-4fd5-43c7-9d7f-586209fbb315" />


> Link: https://tryhackme.com/room/furthernmap

---

## 🧠 Nhiệm vụ
---


## 🛠️ Cách giải

1. 
