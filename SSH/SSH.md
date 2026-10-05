### I. SSH Tunneling (_SSH Port Forwarding_)
kỹ thuật định tuyến lưu lượng mạng qua một kết nối SSH đã được mã hóa. Nói một cách dễ hiểu, nó tạo ra một **"đường hầm" an toàn** kết nối máy tính của bạn với máy chủ từ xa (remote server), giúp dữ liệu truyền qua không bị chặn hoặc nghe lén.
#### 1. Local Port Forwarding ( -L )
- **Nguyên lí:** Chuyển tiếp cổng từ **máy cá nhân (Local)** đến **máy chủ từ xa (Remote)** thông qua máy chủ SSH trung gian
- **Mục đích:**  Truy cập dịch vụ nội bộ (database, web admin...) trên server mà không cần mở cổng public ra Internet.
- **Cú pháp :** `ssh -L [local_port]:[destination_host]:[destination_port] user@ssh_server`
- **Ví dụ** : `ssh -L 3307:localhost:3306 user@my-vps.com` : bạn kết nối vào `localhost:3307` trên máy cá nhân sẽ tương đương với kết nối trực tiếp vào MySQL `3306` trên VPS.

#### 2. Remote Port Forwarding ( -R )
- **Cách hoạt động:** Mở một cổng trên **máy chủ từ xa (Remote)** và chuyển tiếp lưu lượng ngược về một cổng trên **máy cá nhân (Local)**.
- **Mục đích:** Chia sẻ một ứng dụng đang chạy ở localhost cho người bên ngoài truy cập (tương tự cơ chế của Ngrok, Cloudflare Tunnel).
- **Cú pháp :** `ssh -R [remote_port]:[local_host]:[local_port] user@ssh_server `
- **Ví dụ**  :  `ssh -R 8080:localhost:3000 user@my-vps.com` : Bất kỳ ai truy cập `my-vps.com:8080` sẽ được dẫn về web đang chạy trên máy local của bạn

##### 3.Dynamic Port Forwarding ( -D )
- **Mục đích :** Biến SSH client thành một máy chủ **SOCKS Proxy**. Lưu lượng duyệt web hoặc app được cấu hình qua proxy này sẽ đi qua "hầm" SSH đến remote server rồi mới ra Internet.
- **Mục đích:** Dùng như một VPN thu nhỏ để vượt tường lửa, ẩn IP cá nhân hoặc bảo mật đường truyền khi dùng Wi-Fi công cộng.
- **Cú pháp:** `ssh -D [local_port] -N -C user@ssh_server`
- **Ví dụ :** Chạy `ssh -D 1080 -N user@my-vps.com`, sau đó chỉnh cấu hình proxy trên trình duyệt (Firefox/Chrome) là `SOCKS5: localhost:1080`. Toàn bộ lưu lượng web sẽ mang địa chỉ IP của VPS.
#### 4. Khi nào nên dùng SSH Tunnel?
- **Bảo mật kết nối:** Thay vì mở cổng database (PostgreSQL 5432, MySQL 3306, Redis 6379) ra ngoài Internet rất nguy hiểm, bạn chỉ cần mở cổng `22` (SSH) và dùng tunnel để kết nối an toàn.
- **Vượt tường lửa (Bypass Firewall):** Vượt qua các rào cản mạng nội bộ công ty/trường học để truy cập dịch vụ bị chặn.
- **Debug từ xa:** Test webhook (Stripe, GitHub, ZaloPay...) gửi về máy local khi lập trình mà không cần deploy lên server thật.
### II. Cách sử dụng Beszel
### 1. truy cập vào dashboard : ( đã cấu hình SSH Port Forwarding) : 
### 2. Trình giám sát mạng (network/uptime monitors) :
Tính năng theo dõi trạng thái "sống / chết", tốc độ phản hồi và hạn chứng chỉ SSL của website/API
**Nguyên lí :** Cứ định kỳ (ví dụ mỗi 30 giây hoặc 1 phút một lần), Beszel sẽ tự động gửi một tín hiệu (HTTP request / Ping) tới địa chỉ website hoặc API
- **Website có đang sống không** :
	- Trả về `200 OK` : hoạt động bình thường
	- Trả về 500 : bị sập , lỗi 500 , time out , mất mạng
- **Thời gian phản hồi (Response Time / Độ trễ)**:
	- Đo xem API phản hồi nhanh hay chậm (ví dụ: trung bình `45ms`, lúc cao điểm `200ms`).
- **Tỷ lệ mất gói tin (Packet Loss)** : Kiểm tra đường truyền mạng có ổn định không hay chập chờn.
- **Hạn chứng chỉ SSL (HTTPS)** : Theo dõi chứng chỉ SSL còn hạn bao nhiêu ngày để bạn không bao giờ bị tình trạng "trình duyệt báo trang web không an toàn do quên gia hạn SSL".

Các tham số cho 1 biến : 
- **Mục tiêu (URL)**:  `https://api.tnanhdev.id.vn/health`
- **Giao thức**: HTTP / HTTPS
- **Khoảng thời gian**: 60s


### 3. Kết nối với telegram
- Truy cập BOTFATHER để lấy token 
- Truy cập USERINFOBOT để lấy ID
- Ghép thành chuỗi `telegram://<TOKEN>@telegram?chats=<CHAT_ID>`
- telegram://8695699047:AAE5cDIyxA-asVeSJ9x0psIjyJ0GIMGvypw@telegram?chats=7787212995

### 4. Cấu hình uron báo cáo
- Truy cập vào vps bằng ssh : `ssh -i "C:\Users\Admin\.gemini\antigravity-ide\brain\d59b89d0-59bd-4c31-9c3c-7f127ad1560f\scratch\vps_key.pem" userpixel@13.251.205.76`
- Tạo thư mục` mkdir -p /opt/pixelmart/scripts` : -p (--parents) 
- chmod 600 .telegram_alert.env : khóa bảo mật file 
- chmod +x daily_health_report.sh : cấp quyền thực thi
- crontab -e : mở trình quản lí cron