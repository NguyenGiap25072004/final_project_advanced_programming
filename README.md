# ESP32-CAM Robot Car

## Giới thiệu

Đây là dự án điều khiển xe robot sử dụng ESP32-CAM qua Wi-Fi. Dự án bao gồm hai phần chính:

1.  **Phần sụn (firmware) cho ESP32-CAM:**
    *   Thiết lập ESP32-CAM làm một máy chủ web (web server).
    *   Điều khiển động cơ của xe (tiến, lùi, trái, phải, dừng).
    *   Truyền hình ảnh từ camera.
    *   Nhận lệnh điều khiển từ client qua TCP socket.
    *   (Tùy chọn) Gửi trạng thái của xe (vị trí, hướng, pin, ...) về client.
2.  **Ứng dụng điều khiển (client):**
    *   Kết nối với ESP32-CAM qua TCP socket.
    *   Gửi lệnh điều khiển đến ESP32-CAM.
    *   Hiển thị giao diện người dùng (UI) để điều khiển xe.
    *   (Tùy chọn) Hiển thị hình ảnh từ camera.
    *   (Tùy chọn) Hiển thị trạng thái của xe.

## Yêu cầu

### Phần cứng

*   ESP32-CAM
*   Khung xe robot (bao gồm động cơ, bánh xe, ...)
*   Mạch cầu H (L298N, L293D, ...) để điều khiển động cơ
*   Pin và nguồn điện
*   (Tùy chọn) Cảm biến (siêu âm, hồng ngoại, ...)
*   (Tùy chọn) LED, còi, ...

### Phần mềm

*   **ESP32-CAM:**
    *   Arduino IDE hoặc ESP-IDF
    *   Thư viện `WiFi`, `WiFiClient`, `WebServer`, `esp_camera`
*   **Ứng dụng điều khiển:**
    *   Ngôn ngữ: C++
    *   Thư viện: SDL2, SDL2\_net
    *   (Tùy chọn) Thư viện JSON (ví dụ: nlohmann/json cho C++)
    *   (Tùy chọn) Thư viện để decode JPEG (nếu cần hiển thị hình ảnh)

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
5.  Chạy ứng dụng.

## Cách sử dụng

1.  Cấp nguồn cho xe robot.
2.  Chạy ứng dụng điều khiển.
3.  Nhập địa chỉ IP của ESP32-CAM (nếu cần).
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

## Đóng góp

Mọi đóng góp đều được hoan nghênh! Vui lòng tạo Pull Request nếu bạn muốn đóng góp cho dự án.

## Giấy phép

Dự án này được phát hành theo giấy phép MIT.

---

**Lưu ý:**

*   Bạn cần thay đổi các thông tin trong file README.md (địa chỉ IP, sơ đồ chân, ...) cho phù hợp với dự án của bạn.
*   Đây chỉ là một ví dụ cơ bản, bạn có thể thêm nhiều thông tin hơn (ví dụ: hình ảnh, video, hướng dẫn chi tiết, ...) để file README.md trở nên đầy đủ và hấp dẫn hơn.
*   Format code trong file README.md này có thể hiển thị không hoàn toàn đúng, bạn có thể điều chỉnh lại nếu cần thiết.
*   Nhớ thay đổi `Giaphoai123` và `12345678` thành SSID và password của mạng Wi-Fi bạn muốn kết nối.
*   Thay `192.168.1.102` bằng IP của ESP32-CAM của bạn.
*   Format lại code của cả hai chương trình (ESP32 và Application) cho dễ nhìn hơn.
*   Xử lý các lỗi đã nêu ở trên.
