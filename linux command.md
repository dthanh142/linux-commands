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

---


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

---

#3. Lệnh update, upgrade và dist-upgrade

#####**-apt-get update**: 
Được dùng để đồng bộ lại file index của các gói phần mềm. Những file index này được tìm thấy ở những địa chỉ được định nghĩa trong file /etc/apt/sources.list hoặc /etc/apt/sources.list.d. Hệ thống sẽ kiểm tra những file index này để xác định gói phần mềm nào có phiên bản cập nhật. Cần tiến hành update trước khi upgrade hoặc dist-upgrade

**-apt-get upgrade**:

 Tiến hành cập nhật phiên bản mới cho những gói đã cài đặt trong hệ thống nếu tìm thấy những thông tin cập nhật trong file **/etc/apt/sources.list**. Điều này yêu cầu cần chạy lệnh update trước.
Tuy nhiên, việc upgrade sẽ không gỡ bỏ hoặc cài đặt mới những gói phụ thuộc. Ví dụ, khi tiến hành cập nhật 1 gói ứng dụng, những thư viện không còn giá trị sử dụng sẽ không bị gỡ bỏ, hoặc những thư viện mới sẽ không được cài đặt bổ sung.

**-apt-get dist-upgrade**:

 Tương tự như upgrade, nhưng cung cấp cơ chế quản lí những gói phụ thuộc. Khi tiến hành `apt-get dist-upgrade`, ngoài việc cập nhật phiên bản, thì những gói phụ thuộc cũng sẽ được cài đặt thêm hoặc gỡ bỏ tùy thuộc vào độ quan trọng của gói đó.
 
 ---
 
#4.Lệnh wget

GNU wget là 1 ứng dụng miễn phí cung cấp khả năng tải dữ liệu trong môi trường dòng lệnh của linux, nó hỗ trợ các giao thức phổ biến như HTTP, HTTPS và FTP cũng như thông qua các HTTP proxy. Wget là 1 chương trình tải dữ liệu không tương tác nghĩa là có thể chạy nền trong khi user ko đăng nhập vào hệ thống. Điều này khác biệt hoàn toàn so với việc sử dụng các chương trình tải dữ liệu phổ biến khác yêu cầu user phải liên tục hiện hữu trong phiên tải dữ liệu. Wget tuy khá phức tạp cho người mới sử dụng nhưng nó lại hết sức mạnh mẽ và hiệu quả. Nó có thể lần theo từng link HTML, XHTML và CSS và chuyển đổi các link đó lưu chúng lại dưới một phiên bản offline trên máy. Wget xử lý rất tốt những trường hợp do lỗi về mạng, chậm không ổn định...nó sẽ tự động tải file bị lỗi cho đến khi tất cả dữ liệu yêu cầu được tải về. 

 Một số tùy chọn trong wget: 

    -O {tên mới}: lưu file mới tải về dưới 1 tên khác
    -b 	: tải file trong chế độ nền, ví dụ là tải file trong khi tắt máy
    --spider: tải kiểm tra tình trạng link tồn tại hay ko
    -i tải nhiều link 1 lúc
    -P $folder_name : chỉ định lưu tại $folder-name.
    -c: resume download
    -r: download cả thư mục con

Ví dụ:
`$ wget -c -r --no-parent --reject index.html http://localhost:8000/folder1/`

    -c : là có thể resume down được file/directory (nếu server support việc này)
    -r : recursive tức là down được file/directory trong diretory (đệ qui) 
    --no-parent : chỉ down từ folder1/ trở đi, chứ k down ngược http://localhost:8000/
    --reject index.html : không down các file index.html
Mặc định thì wget sẽ thử tới 20 lần retry nếu việc tải dữ liệu không thành công. Nếu bạn muốn thay đổi số lần retry thành 50 lần thì câu lệnh sẽ như sau:

    wget --tries=50 http://wordpress.org/latest.tar.gz

Chúng ta có thể buộc wget chỉ tải về những file có định dạng là ảnh (jpg, gif...) hay pdf... bằng cấu trúc:

    $ wget -r -A $extension $URL
Ví dụ sau sẽ tải về tòan bộ các ảnh có định dạng jpg hoặc gif từ URL:  [http://www.linuxjournal.com/content/downloading-entire-web-site-wget](http://www.linuxjournal.com/content/downloading-entire-web-site-wget)

    $ wget -r -A jpg,gif http://www.linuxjournal.com/content/downloading-entire-web-site-wget

---

#**5.Lệnh CURL:**

Là 1 công cụ đùng để chuyển dữ liệu lên server hoặc từ server về, sử dụng hỗ trợ giao thức HTTP, HTTPSs, LDAP, POP3... Các lệnh được thiết kế để làm việc mà ko cần giao diện người dùng. curl hỗ trợ nhiều tính năng bao gồm POST, GET, chứng thực, tải các tập tin được chia nhỏ, giới hạn tốc độ tập tính, kích thước tập tin...

	- curl [URL]: thì thông tin đc tải về sẽ đc in toàn bộ ra màn hình, và toàn bộ thông tin tải về sẽ được hiển thị lên trong quá trình cài đặt (lưu ý cần lưu vào file nội dung cụ thể nếu ko sẽ bị mất)
	- curl -- slient [URL]: thông tin vẫn tải ra màn hình nhưng ko hiển thị trong quá trình cài đặt
	- curl URL --silent -O {tên file}: Lưu thông tin tải về vào 1 file
	- curl [URL] -- progress: hiển thị quá trình tải ra (theo %)
curl sử dụng lấy thông tin về với điều kiện đi kèm như cookies (tên, pass) hay header (-H "tên header")

---

Tham khảo:

[http://nanchor.blogspot.com/2012/07/co-ban-ve-wget.html](http://nanchor.blogspot.com/2012/07/co-ban-ve-wget.html)

[http://www.justpassion.net/programming/bash-shell/lenh-curl-trong-linux-2.html](http://www.justpassion.net/programming/bash-shell/lenh-curl-trong-linux-2.html)

[http://linux.die.net/man/8/apt-get](http://linux.die.net/man/8/apt-get)
