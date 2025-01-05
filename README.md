# ESP32-CAM Robot Car

## Giới thiệu

Đây là dự án điều khiển xe robot sử dụng ESP32-CAM qua Wi-Fi. Dự án bao gồm hai phần chính:

1.  **Phần lập trình cho ESP32-CAM:**
    *   Thiết lập ESP32-CAM làm một máy chủ web (web server).
    *   Điều khiển động cơ của xe (tiến, lùi, trái, phải, dừng).
    *   Truyền hình ảnh từ camera.
    *   Nhận lệnh điều khiển từ client qua TCP socket.
    *   (Chưa phát triển) Gửi trạng thái của xe (vị trí, hướng, pin, ...) về client.
2.  **Ứng dụng điều khiển (client):**
    *   Kết nối với ESP32-CAM qua TCP socket.
    *   Gửi lệnh điều khiển đến ESP32-CAM.
    *   Hiển thị giao diện người dùng (UI) để điều khiển xe.
    *   (Chưa tích hợp vào app sẽ phát triển sau) Hiển thị hình ảnh từ camera.
    *   (Chưa tích hợp vào app sẽ phát triển sau) Hiển thị trạng thái của xe.

## Yêu cầu

### Phần cứng

*   ESP32-CAM
*   Khung xe robot (bao gồm động cơ, bánh xe, ...)
*   Mạch cầu H (L298N) để điều khiển động cơ
*   Pin và nguồn điện

### Phần mềm

*   **ESP32-CAM:**
    *   Arduino IDE hoặc ESP-IDF
    *   Thư viện `WiFi`, `WiFiClient`, `WebServer`, `esp_camera`
*   **Ứng dụng điều khiển:**
    *   Ngôn ngữ: C++
    *   Thư viện: SDL2, SDL2\_net
    *   (Tùy chọn) Thư viện JSON (ví dụ: nlohmann/json cho C++)

## Cài đặt

### ESP32-CAM

1.  Cài đặt Arduino IDE hoặc ESP-IDF.
2.  Cài đặt board ESP32 trong Arduino IDE (tham khảo hướng dẫn trên trang chủ của Espressif).
3.  Mở mã nguồn ESP32-CAM (file `.ino` hoặc thư mục dự án ESP-IDF).
4.  Sửa đổi thông tin Wi-Fi (SSID và password) trong mã nguồn.
5.  (Tùy chọn) Thay đổi chân điều khiển động cơ, cấu hình camera, ...
6.  Biên dịch và nạp chương trình lên ESP32-CAM.
7.  Mở Serial Monitor để lấy địa chỉ IP của ESP32-CAM.

### Ứng dụng điều khiển

1.  Cài đặt thư viện SDL2 và SDL2\_net (tham khảo hướng dẫn cài đặt trên trang chủ của SDL).
2.  Mở mã nguồn ứng dụng điều khiển bằng trình soạn thảo (ví dụ: VS Code, Code::Blocks).
3.  (Tùy chọn) Sửa đổi địa chỉ IP của ESP32-CAM trong mã nguồn.
4.  Biên dịch mã nguồn (sử dụng `g++` hoặc IDE).
5.  Tạo file CMakeLists.txt đính kèm bên trên.
6.  Gõ "cmake -S . -B .   " trong terminal.
7.  Tiếp theo gõ "make" hoặc "mingw32-make" tùy máy, xong gõ "./main  " để chạy nhé.
8.  Chạy ứng dụng.

## Cách sử dụng

1.  Cấp nguồn cho xe robot.
2.  Chạy ứng dụng điều khiển.
3.  Nhập địa chỉ IP của ESP32-CAM.
4.  Sử dụng các phím mũi tên (hoặc các nút điều khiển trên giao diện) để điều khiển xe.

## Sơ đồ chân kết nối (tham khảo)

| ESP32-CAM | Mạch cầu H | Chức năng    |
| :-------- | :--------- | :----------- |
| GPIO14    | IN1        | Động cơ A - 1 |
| GPIO15    | IN2        | Động cơ A - 2 |
| GPIO16    | IN3        | Động cơ B - 1 |
| GPIO4     | IN4        | Động cơ B - 2 |

**Lưu ý:** Sơ đồ chân kết nối có thể thay đổi tùy theo mạch cầu H và cách bạn đấu dây.

## Các vấn đề đã biết và lưu ý

*   Chưa xử lý triệt để các trường hợp lỗi.
*   Chưa có xác thực và bảo mật kết nối.
*   Giao diện người dùng đơn giản.
*   Hiệu suất truyền hình ảnh có thể bị ảnh hưởng bởi tốc độ mạng.

## Phát triển trong tương lai

*   Thêm xác thực và bảo mật kết nối.
*   Cải thiện giao diện người dùng (hiển thị hình ảnh, bản đồ, ...).
*   Thêm các tính năng nâng cao (điều khiển bằng giọng nói, tự động tránh vật cản, ...).
*   Tối ưu hóa hiệu suất truyền hình ảnh.
*   Xử lý lỗi


**Lưu ý:**

*   Bạn cần thay đổi các thông tin trong file README.md (địa chỉ IP, sơ đồ chân, ...) cho phù hợp với dự án của bạn.
*   Nhớ thay đổi `wifiname` và `12345678` thành SSID và password của mạng Wi-Fi bạn muốn kết nối.
*   Thay `192.168.1.102` bằng IP của ESP32-CAM của bạn.
