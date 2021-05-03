# Internship-Long
https://create-it-myself.com/know-how/construct-nginx-django-posgresql-by-docker-compose/

VPS
VPS (Virtual Private Server) là một loại máy chủ “phát triển web, thiết kế web, webmaster, phát triển game…”; là dạng máy chủ ảo, server ảo được tạo ra bằng phương pháp phân chia một máy chủ vật lý thành nhiều máy chủ khác nhau có tính năng tương tự như máy chủ riêng (dedicated server), chạy dưới dạng chia sẻ tài nguyên từ máy chủ vật lý ban đầu đó.
Mỗi VPS hosting là một hệ thống hoàn toàn riêng biệt, có một phần CPU, dung lượng RAM riêng, dung lượng ổ HDD riêng, địa chỉ IP riêng và hệ điều hành riêng, người dùng có toàn quyền quản lý root và có thể restart lại hệ thống bất cứ lúc nào.

SSH
SSH (Secure Shell) là một giao thức điều khiển từ xa cho phép người dùng kiểm soát và chĩnh sửa server từ xa qua internet. Dịch vụ được tạo ra nhằm thay thế cho trình Telnet (1. trong các máy dựa vào hệ điều hành UNIX và được nối vào mạng Internet, đây là một chương trình cho phép người sử dụng tiến hành thâm nhập vào các máy tính ở xa thông qua các ghép nối TCP/IP.) vốn không có mã hoá và sử dụng kỹ thuật cryptographic (mật mã) để đảm bảo tất cả giao tiếp gửi tới và gửi từ server từ xa diễn ra trong tình trạng mã hoá. Nó cung cấp thuật toán để chứng thực người dùng từ xa, chuyển inout từ client tới host, và replay kết quả trả về tới khách hàng.

APP SERVER
App server là một loại máy chủ được thiết kế để cài đặt, vận hành và host các ứng dụng. Đã có sự phát triển vượt bậc về số lượng ứng dụng được đưa lên Internet. Các ứng dụng đó ngày càng trở nên lớn hơn với nhu cầu bổ sung nhiều chức năng, đồng thời việc chạy và bảo trì chúng cũng trở nên phức tạp hơn. Do đó, thuật ngữ "app server" được đặt ra và đưa vào thế giới Internet.
App server (application server hay máy chủ ứng dụng) là một framework phần mềm hỗn hợp cho phép cả việc tạo các ứng dụng web và môi trường máy chủ để chạy chúng.
App server thường bao gồm nhiều phần tử tính toán khác nhau, chạy các tác vụ cụ thể cần thiết cho hoạt động của đám mây, phần mềm và ứng dụng dựa trên web.
Nằm giữa tầng máy chủ dựa trên web chính và tầng back-end của máy chủ cơ sở dữ liệu (database server), app server về cơ bản là sự kết nối giữa máy chủ cơ sở dữ liệu và người dùng doanh nghiệp hoặc ứng dụng tiêu dùng mà nó hỗ trợ, thông qua việc đưa các giao thức và API (Application Programming Interface) khác nhau vào để sử dụng.

NGINX
Trong kiến trúc “Three tier architecture”. Máy chủ webserver (trong trường hợp của bạn là Nginx) sẽ xử lý nhiều yêu cầu về hình ảnh và tài nguyên tĩnh (images and static resouces). Các yêu cầu cần được tạo tự động sau đó sẽ được chuyển đến máy chủ ứng dụng (trong ví dụ của bạn là Gunicorn). (Ngoài ra phần thứ 3 trong 3 lớp là Cơ sở dữ liệu).
Lịch sử, mỗi tầng này sẽ được lưu trữ trên các máy riêng biệt (và rất có thể sẽ có nhiều máy trong 2 tầng đầu tiên, tức là: 5 máy chủ webserver gửi yêu cầu đến 2 máy chủ ứng dụng (app server) lần lượt truy vấn một cơ sở dữ liệu).
Trong hiện đại, chúng ta hiện có các ứng dụng của tất cả các hình dạng và kích tướng. Không phải mọi project cuối tuần hoặc địa điểm kinh doanh nhỏ đều thực sự cần mã lực của nhiều máy sẽ chạy khá happily trên một single box. Điều này đã tạo ra các mục mới vào các mảng các giải pháp lưu trữ. Một số giải pháp sẽ kết hợp app server với webserver (Apache https + mod_wsgi, Nginx + mod_uwsgi, etc). Và không có gì lạ khi lưu trữ cơ sở dữ liệu trên cùng một máy với một trong những tổ hợp máy web/app server.

Gunicorn
Trong trường hợp Gunicorn, chúng ta đã đưa ra quyết định cụ thể để giữ mọi thứ tách biệt với Nginx trong khi dựa vào hành vi uỷ quyền của Nginx. Cụ thể, nếu chúng ta có thể giả định rằng Gunicorn sẽ không bao giờ đọc các kết nối trực tiếp từ internet, thì chúng ta không lo lắng về các máy Khách chạy chậm. Điều này có nghĩa là mô hình xử lý Gunicorn đơn giản đến mức khó tin.
Sự tách biệt cũng cho phép Gunicorn được viết bằng Python thuần túy, giảm thiểu chi phí phát triển trong khi không ảnh hưởng đáng kể đến hiệu suất. Nó cũng cho phép người dùng khả năng sử dụng các proxy khác (giả sử họ đệm chính xác).
Đối với câu hỏi thứ hai của bạn về những gì thực sự xử lý yêu cầu HTTP, câu trả lời đơn giản là Gunicorn. Câu trả lời đầy đủ là cả Nginx và Gunicorn đều xử lý yêu cầu. Về cơ bản, Nginx sẽ nhận được yêu cầu và nếu đó là một yêu cầu động (thường dựa trên các mẫu URL) thì nó sẽ đưa yêu cầu đó cho Gunicorn, tổ chức này sẽ xử lý và sau đó trả lại phản hồi cho Nginx, sau đó sẽ chuyển phản hồi trở lại ban đầu khách hàng.
Vì vậy, cuối cùng, có. Bạn cần cả Nginx và Gunicorn (hoặc thứ gì đó tương tự) để triển khai Django thích hợp. Nếu bạn đặc biệt muốn tổ chức Django với Nginx, thì tôi sẽ điều tra Gunicorn, mod_uwsgi và có thể CherryPy như những ứng cử viên cho phe Django.


Cài đặt và cấu hình Django vs Postgres, Nginx và Gunicorn
-	Cài đặt: Server (VPS).
-	Cài đặt User Django:
o	Bước 1: Cập nhập gói (đảm bảo các gói được cài đặt trên VPS đều được cập nhập).
	Sudo apt-get update
	Sudo apt-get upgrade
	=> Lệnh đầu là download bất kỳ bản cập nhập nào cho các gói được quản lý thông qua apt-get.
	=> Lệnh thứ 2 là sau khi chạy các lệnh trên, nếu có bản cập nhập để cài đặt, cài đặt các bản cập nhập.
o	Bước 2: Cài đặt và tạo Virtualenv.
	Sudo apt-get install python-virtualenv
	(Tạo virtualenv để cài đặt Django và các gói Python khác bên nó): 
•	Sudo virtualenv /opt/myenv
	=> Một folder mới “myenv” đã được tạo trong folder “/opt”. Đây là nơi virtualenv của ta sẽ sống.
o	Bước 3: Cài đặt Django.
	Source /opt/myenv/bin/activate
	Cài đặt django:
•	Pip install django
o	Bước 4: Cài đặt PostgreSQL.
	(Có thể không cần sử dụng virtualenv cho cài đặt PostgreSQL), để huỷ kích hoạt:
•	Deactivate
	Cài đặt các gói phụ thuộc để PostgreSQL hoạt động với Django:
•	Sudo apt-get install libpq-dev python-dev
	Cài đặt PostgreSQL:
•	Sudo apt-get install postgresql postgresql-contrib
o	Bước 5: Cài đặt NGINX.
	Nginx là một web server cực kỳ nhanh và nhẹ. Sử dụng nó để cung cấp các file tĩnh cho ứng dụng của Django:
•	Sudo apt-get install nginx
o	Bước 6: Cài đặt Gunicorn.
	Gunicorn là một Server HTTP WSGI Python rất mạnh. Vì nó là một gói Python, trước tiên ta cần kích hoạt virtualenv của bạn để cài đặt nó:
•	Source /opt/myenv/bin/activate
•	Cài đặt Gunicorn:
o	Pip install gunicorn
o	Có thể dừng lại ở đây.
o	Bước 7: Cấu hình PostgreSQL.
	Tạo database, tạo user và cấp cho user mà ta đã tạo quyền truy cập vào database mà ta đã tạo:
•	Sudo su – postgres
•	Tạo database:
o	Createdb <name_database>
•	Tạo user database:
o	Createuser -P
o	<Điền username, password>
•	Kích hoạt giao diện PostgreSQL:
o	Psql
•	Cấp cho user mới quyền truy cập vào database mới của bạn:
o	GRANT ALL PRIVILEGES ON DATABASE  <db_name> TO myuser;
o	Bước 8: Tạo project Django.
	Cd /opt/myenv
	Đảm bảo virtualenv đang hoạt động:
•	Source /opt/myenv/bin/activate
	Tạo một dự án Django mới:
•	Django-admin.py startproject <myproject>
	Để Django có thể nói nói chuyện với database của ta, ta cần cài đặt backend cho PostgreSQL:
•	Pip install psycopg2
	Thay đổi thành folder “myproject”:
•	Cd /opt/myenv/myproject/myproject
	Setting file setting.py:
-	    DATABASES = {
-	        'default': {
-	            'ENGINE': 'django.db.backends.postgresql_psycopg2', # Add 'postgresql_psycopg2', 'mysql', 'sqlite3' or 'oracle'.
-	            'NAME': 'mydb',                      # Or path to database file if using sqlite3.
-	            # The following settings are not used with sqlite3:
-	            'USER': 'myuser',
-	            'PASSWORD': 'password',
-	            'HOST': 'localhost',                      # Empty for localhost through domain sockets or           '127.0.0.1' for localhost through TCP.
-	            'PORT': '',                      # Set to empty string for default.
-	        }
-	    }
	Thoát khỏi setting.py. Chuyển đến folder trong folder dự án Django:
•	Cd /opt/myenv/myproject
•	Source /opt/myenv/bin/activate
	Cấu hình ban đầu và các bảng khác vào database:
•	Python manage.py syncdb
•	Bạn sẽ thấy một số kết quả mô tả bảng nào đã được cài đặt, sau đó là dấu nhắc hỏi bạn có muốn tạo một superuser hay không. Điều này là tuỳ chọn và phụ thuộc vào việc bạn sẽ sử dụng hệ thống xác thực của Django hay administrator Django.
o	Bước 9: Cấu hình Gunicorn.
	Đầu tiên, hãy chạy qua Gunicorn với cài đặt mặc định. Đây là lệnh để chỉ chạy Gunicorn mặc định:
•	Gunicorn_django --bind yourdomainorip.com:8001
•	Đảm bảo thay thế “yourdomainorip.com” bằng domain của bạn hoặc IP của VPS nếu bạn muốn.
	Bây giờ hay truy cập trình duyệt web và truy cập yourdomainorip.com:8001 để xem hello Django.
	Tuy nhiên, nếu nhìn kỹ kết quả từ lệnh trên, bạn sẽ thấy chỉ có một nhân viên Gunicorn được khởi động. Điều gì sẽ xảy ra nếu đang chạy một ứng dụng quy mô lớn trên một VPS lớn? Đừng sợ! Tất cả những gì cần làm là sửa đổi lệnh một chút như sau:
•	Gunicorn_django --workers3 --bind yourdomainorip.com:8001
•	Đến đây sẽ thấy rằng 3 công nhân đã được khởi động thay vì chỉ 1 công nhân. Có thể thay đổi số này thành bất kỳ số nào phù hợp với nhu cầu của bạn.
	Vì đã chạy lệnh khởi động Gunicorn dưới dạng root, nên Gunicorn hiện đang chạy dưới dạng root. Nếu không muốn điều đó, thì sao? Ta có thể thay đổi lệnh ở trên một chút để chứa:
Gunicorn_django --worker=3 --user=nobody --bind yourdomainorip.com:8001

	Nếu muốn cài đặt nhiều tuỳ chọn hơn cho Gunicorn, thì cách tốt nhất là cài đặt file cấu hình mà bạn có thể gọi khi chạy Gunicorn. Điều này sẽ dẫn đến một lệnh Gunicorn ngắn hơn và dễ đọc/Cấu hình hơn.
	Có thể đặt file cấu hình cho gunicorn ở bất kỳ đâu. Để đơn giản, ta sẽ đặt nó trong folder virtualenv của ta. Điều hướng đến folder virtualenv:
•	Cd /opt/myenv
•	Bây giờ hãy mở file cấu hình bằng editor:
o	Sudo nano gunicorn_config.py
o	Thêm các nội dụng vào file:
    command = '/opt/myenv/bin/gunicorn'
    pythonpath = '/opt/myenv/myproject'
    bind = '127.0.0.1:8001'
    workers = 3
    user = nobody

•	Lưu và thoát khỏi file. Những gì các tùy chọn này làm là đặt đường dẫn đến file binary gunicorn, thêm folder dự án của bạn vào đường dẫn Python, đặt domain và cổng để ràng buộc Gunicorn, đặt số lượng nhân viên gunicorn và đặt user mà Gunicorn sẽ chạy.
•	Để chạy server, lần này ta cần lệnh dài hơn một chút. Nhập lệnh sau vào dấu nhắc của bạn:
o	/opt/myenv/bin/gunicorn -c /opt/myenv/gunicorn_config.py myproject.wsgi
•	Bạn sẽ nhận thấy rằng trong lệnh trên, ta chuyển cờ “-c”. Điều này cho gunicorn biết rằng ta có một file cấu hình mà ta muốn sử dụng, file này ta chuyển vào chỉ sau cờ “-c”. Cuối cùng, ta chuyển tham chiếu ký hiệu có dấu chấm Python đến file WSGI của ta để Gunicorn biết file WSGI của ta ở đâu.
•	Chạy Gunicorn theo cách này yêu cầu bạn chạy Gunicorn trong phiên màn hình của chính nó (nếu bạn đã quen với việc sử dụng màn hình) hoặc bạn làm nền cho quá trình bằng cách nhấn “ctrl + z” rồi nhập “bg” và “enter” tất cả ngay sau khi chạy lệnh Gunicorn. Điều này sẽ làm nền cho quá trình để nó tiếp tục chạy ngay cả sau khi phiên hiện tại của bạn đã đóng. Điều này cũng đặt ra vấn đề cần phải khởi động hoặc khởi động lại Gunicorn theo cách thủ công nếu VPS của bạn được khởi động lại hoặc nó gặp sự cố vì lý do nào đó. Để giải quyết vấn đề này, hầu hết mọi người sử dụng supervisord để quản lý Gunicorn và khởi động / khởi động lại nó khi cần thiết.
o	Bước 10: Cấu hình NGINX.
Trước khi ta đi quá xa, trước tiên hãy bắt đầu NGINX như sau:
sudo service nginx start
Vì ta chỉ cài đặt NGINX để xử lý các file tĩnh nên trước tiên, ta cần quyết định nơi các file tĩnh của ta sẽ được lưu trữ. Mở file settings.py cho dự án Django của bạn và chỉnh sửa dòng STATIC_ROOT để trông giống như sau:
    STATIC_ROOT = "/opt/myenv/static/"
Con đường này có thể ở bất cứ đâu bạn muốn. Nhưng để làm sạch, tôi thường đặt nó ngay bên ngoài folder dự án Django của tôi, nhưng bên trong folder virtualenv của tôi.
Đến đây bạn đã cài đặt nơi chứa các file tĩnh của bạn , hãy cấu hình NGINX để xử lý các file đó. Mở file cấu hình NGINX mới bằng lệnh sau (bạn có thể thay thế “nano” bằng editor mà bạn chọn):
sudo nano /etc/nginx/sites-available/myproject
Bạn có thể đặt tên file bạn muốn , nhưng tiêu chuẩn thường là đặt tên file có liên quan đến trang web mà bạn đang cấu hình . Bây giờ thêm phần sau vào file :
    server {
        server_name yourdomainorip.com;

        access_log off;

        location /static/ {
            alias /opt/myenv/static/;
        }

        location / {
                proxy_pass http://127.0.0.1:8001;
                proxy_set_header X-Forwarded-Host $server_name;
                proxy_set_header X-Real-IP $remote_addr;
                add_header P3P 'CP="ALL DSP COR PSAa PSDa OUR NOR ONL UNI COM NAV"';
        }
    }
Lưu và thoát khỏi file . Cấu hình trên đã đặt NGINX để phục vụ bất kỳ thứ gì được yêu cầu tại yourdomainorip.com/static/ từ folder tĩnh mà ta đặt cho dự án Django của bạn . Mọi thứ được yêu cầu tại yourdomainorip.com sẽ ủy quyền cho localhost trên cổng 8001, đó là nơi ta đã yêu cầu Gunicorn chạy. Các dòng khác đảm bảo tên server và địa chỉ IP của yêu cầu được chuyển đến Gunicorn. Nếu không có điều này, địa chỉ IP của mọi yêu cầu sẽ trở thành 127.0.0.1 và tên server chỉ là tên server VPS của bạn.
Bây giờ ta cần cài đặt một softlink trong folder / etc / nginx / sites-enable trỏ đến file cấu hình này. Đó là cách NGINX biết trang web này đang hoạt động. Thay đổi folder thành / etc / nginx / sites-enable như thế này:
cd /etc/nginx/sites-enabled
Khi đó, hãy chạy lệnh này:
sudo ln -s ../sites-available/myproject
Điều này sẽ tạo softlink mà ta cần để NGINX biết cách tôn trọng file cấu hình mới cho trang web của ta .
Ngoài ra, hãy xóa khối server nginx mặc định:
`sudo rm default '
Tuy nhiên, ta cần khởi động lại NGINX để nó biết tìm kiếm các thay đổi của ta . Để làm điều này, hãy chạy như sau:
sudo service nginx restart
Và đó là nó! Đến đây bạn đã cài đặt Django và làm việc với PostgreSQL và ứng dụng của bạn có thể truy cập web với NGINX cung cấp nội dung tĩnh và Gunicorn đóng role là server ứng dụng của bạn. Nếu có thắc mắc hay cần tư vấn thêm, hãy để lại trong phần comment .


https://www.mdeditor.tw/pl/pR6U

https://github.com/ntlong1099/Internship-Long/blob/main/68747470733a2f2f692e696d6775722e636f6d2f735a5a674577712e6a7067.jfif
