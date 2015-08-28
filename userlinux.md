#1.Các lệnh với user trong linux
**-Tạo 1 user mới:**

`$useradd [option] <tên user>`

Các tùy chọn:

    -u UID
    -G GID : Danh sách các Secondary group có thể cách nhau bằng dấu phẩy ","
    -c ghi chú
    -d directory
    -m Nếu như thư mục của -d chưa có, thì tự động tạo mới.
    -s shell : mặc nhiên sẽ dùng bash shell
---
**-Đặt password cho 1 user:**

`$passwd <tên user>`

---
**-Xóa 1 user:**

`$userdel <tên user>`

*Sử dụng tham số -r nếu muốn xóa cả thư mục home của user đó*

---

**-Thay đổi thông tin user:**

`$usermod <user name>`

---

**-Đổi mật khẩu cho user:**

`$passwd <user name>`

---

**-Đổi user :**

`	$su <user name>`

**-Xem thông tin user:**

`$id`

---

#2. Quản lý các user
Thông tin về các user được lưu trữ trong các files: /etc/passwd và /etc/shadow.

###**/etc/passwd**: 
File này chứa thông tin về user, điều khiển việc login của các user.
File này được lưu dưới dạng ASCII, mỗi dòng lưu thông tin của một user, và mỗi dòng lại phân thành các trường bằng dấu hai chấm. Như vậy thông tin đã được lưu dưới dạng một "bảng". Cấu trúc của nó như sau:
UserName : Password : UserID : PrincipleGroup : Comments : HomeDirectory : Shell

Ý nghĩa của cụ thể của các trường:

**-usename**: tên đăng nhập, phân biệt Hoa/thường, nên dùng chữ thường.

**-password**: lưu chuỗi passwd đã hash, nếu có sử dụng /etc/shadow thì ở đây sẽ là chữ x

**-user ID**: hệ thống dùng user ID để phân biệt người này với người khác.

**-group ID**: Đây là Primary Group của user này.

**-comment**: mô tả cho user.

**-Home Directory**: Thư mục home của từng user, thường sẽ nằm trong /home/tenuser

**-Shell**: Tên chương trình sẽ thực thi ngay sau khi user login vào. Nếu không có shell user sẽ không thể login. Mặc nhiên trên Linux sẽ dùng bash shell.

---

###**/etc/shadow**

Chứa chuỗi password đã mã hóa bằng hàm băm và thông tin về khác như Password Age của User.

#3. Lệnh update, upgrade và dist-upgrade

-apt-get update: Khi 1 gói đã cài đặt trong hệ thống có phiên bản mới, nó sẽ được định nghĩa trong file /etc/apt/sources.list và /etc/apt/sources.list.d
Lệnh apt-get update sẽ cập nhật lại 2 file đó và kiểm tra thông tin về những gói cần cập nhật

-apt-get upgrade: Tiến hành cập nhật phiên bản mới cho những gói đã cài đặt trong hệ thống nếu tìm thấy những thông tin cập nhật trong file /etc/apt/sources.list. Điều này yêu cầu cần chạy lệnh update trước.
Tuy nhiên, việc upgrade sẽ không gỡ bỏ hoặc cài đặt mới những gói phụ thuộc. Ví dụ, khi tiến hành cập nhật 1 gói ứng dụng, những thư viện không còn giá trị sử dụng sẽ không bị gỡ bỏ, hoặc những thư viện mới sẽ không được cài đặt bổ sung.

-apt-get dist-upgrade: Tương tự như upgrade, nhưng cung cấp cơ chế quản lí những gói phụ thuộc. Khi tiến hành dist-upgrade, ngoài việc cập nhật phiên bản, thì những gói phụ thuộc cũng sẽ được cài đặt thêm hoặc gỡ bỏ tùy thuộc vào độ quan trọng của gói đó.