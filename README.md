# btvn3_web
Bài tập 3   : môn Phát triển ứng dụng trên nền web
Giảng viên  : Đỗ Duy Cốp
Lớp học phần: 58KTPM
Ngày giao   : 2025-10-24 13:50
Hạn nộp     : 2025-11-05 00:00
--------------------------------------------------
Yêu cầu     : LẬP TRÌNH ỨNG DỤNG WEB trên nền linux
1. Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
   <img width="893" height="410" alt="image" src="https://github.com/user-attachments/assets/905cf1cf-3bdc-471d-a82e-649220b7e18c" />

2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)
<img width="1893" height="975" alt="Screenshot 2025-11-06 181638" src="https://github.com/user-attachments/assets/44ec983d-0449-42dc-b443-1fc28b17d760" />

3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/e52fdd2d-fe96-4148-9510-e67aa8ea2b15" />
4. Lập trình web frontend+backend:
 4.2 Web IOT: Giám sát dữ liệu IOT.
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - hiển thị giá trị mới nhất của các thông số đang giám sát, khi click vào thì hiển thị đồ thị lịch sử quá trình thay đổi (gọi grafana iframe để hiển thị)
 - backend: Sử dụng nodered để đọc dữ liệu từ các cảm biến (có thể dùng api online để lấy dữ liệu theo giời gian thực), 
   nodered sẽ lưu dữ liệu mới nhất (dạng update) vào cơ sở dữ liệu mariadb (sử dụng phpmyadmin để tạp table và quản trị lần đầu)
   nodered sẽ lưu dữ liệu (insert) vào influxdb để lưu giá trị lịch sử, để cho grafana dùng để hiển thị biểu đồ.
   <img width="1914" height="1013" alt="image" src="https://github.com/user-attachments/assets/eba385aa-3aa1-4a2b-8806-c3c2566b06f6" />
1: Chuẩn bị cơ sở dữ liệu MariaDB (cho login và dữ liệu cảm biến)
   <img width="1915" height="861" alt="image" src="https://github.com/user-attachments/assets/b9d4d217-573c-41e4-bffe-6aa1f6100279" />
2: Xây dựng backend trên Node-RED
   <img width="1183" height="550" alt="image" src="https://github.com/user-attachments/assets/20d165ee-04da-48dc-b430-1bb348417a9b" />
   API LẤY DỮ LIỆU MỚI NHẤT
   <img width="1022" height="149" alt="image" src="https://github.com/user-attachments/assets/de7dad60-d9ef-497f-bc6c-f670616936a5" />
3: Setup InfluxDB + Grafana
<img width="1739" height="807" alt="image" src="https://github.com/user-attachments/assets/47e2435b-8c21-4f5f-8167-c6a993b5db7e" />

5. Nginx làm web-server
 - Cấu hình nginx để chạy được website qua url http://nguyetlinh.com  (thay fullname bằng chuỗi ko dấu viết liền tên của bạn)
 - Cấu hình nginx để http://nguyetlinh.com/nodered truy cập vào nodered qua cổng 80, (dù nodered đang chạy ở port 1880)
 - Cấu hình nginx để http://nguyetlinh.com/grafana truy cập vào grafana qua cổng 80, (dù grafana đang chạy ở port 3000)
<img width="1879" height="901" alt="image" src="https://github.com/user-attachments/assets/0aa8642e-9682-4f79-b016-d88fee5b18b8" />

Yêu cầu sinh viên lưu code trên github
có file readme.md có hình ảnh + text: ghi lại nhật ký quá trình làm bài.

 Trang web chính       [http://nguyetlinh.com](192.168.1.6 nguyetlinh.com)                 
 phpMyAdmin            [http://localhost:8080](http://localhost:8080)                 
 Node-RED (qua nginx)  [http://nguyetlinh.com/nodered](http://nguyetlinh.com/nodered) 
 Grafana (qua nginx)   [http://nguyetlinh.com/grafana](http://nguyetlinh.com/grafana) 
 InfluxDB setup        [http://localhost:8086](http://localhost:8086)                 

CÁCH ĐÁNH GIÁ:
1. Cài đặt được môi trường: 1đ
2. Cài đặt được các docker container với cấu hình phù hợp: 1đ
3. Web chạy được, giao diện phù hợp, chạy trên web sever nginx: 2đ
4. nodered api trả về json, test được: 2đ
5. front-end có js gọi được api nodered, nhận về json, hiển thị được kết quả từ json này. 2đ
6. Bài làm có dấu ấn, giải thích rõ ràng, hiểu vấn đề: 2đ
