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
**-Đặt password cho 1 user: **

`$passwd <tên user>`

---
**-Xóa 1 user:**

`$userdel <tên user>`

*Sử dụng tham số -r nếu muốn xóa cả thư mục home của user đó*

---

**-Thay đổi thông tin user: **

`$usermod <user name>`

---

**-Đổi mật khẩu cho user: **

`$passwd <user name>`

---

**-Đổi user : **

`	$su <user name>`

**-Xem thông tin user: **

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

###**/etc/shadow **

Chứa chuỗi password đã mã hóa bằng hàm băm và thông tin về khác như Password Age của User.