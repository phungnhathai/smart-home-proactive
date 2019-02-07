## Smart Home with a proactive approach based on Machine Learning
  Những giải pháp Smart Home hiện nay cho phép chúng ta điều khiển, quản lý thông qua sự tương tác của chủ nhà như điều khiển bằng giọng nói hay qua các thiết bị di dộng. Với mô hình Smart Home như trên thì chủ nhà phải thiết lập các quy tắc từ đơn gian đến phức tạp để ngôi nhà hoạt động tốt theo ý của mình, như vậy sẽ gây khó khăn, mất thời gian, bất tiện cho chủ nhà. Smart Home chỉ dừng lại ở khái niệm nhà tự động. Với sự phát triển mạnh mẽ của công nghệ, khái niệm nhà thông minh đã dần thay đổi. Những ngôi nhà sẽ thật sự thông minh nếu có khả năng học hỏi, phản ứng một cách chủ động theo những thói quen, hành vi của chủ nhà. Việc ứng dụng Machine Learning vào Smart Home sẽ giúp ngôi nhà có thể trở nên thông minh hơn.
  
  Ví dụ về việc điều khiển máy lạnh trong ngôi nhà: 
  ```Khi đi làm về nhà, chủ nhà muốn điều chỉnh nhiệt độ 25°C, đến lúc đi ngủ lại muốn 26°C, đến khi thức dậy lại muốn nhiệt độ 28°C. Với thói quen như vậy, ngôi nhà có thể học hỏi và từ đó có những điều chỉnh phù hợp trong tương lai.```
  
 ## Thiết kế hệ thống
 
 ### Các tầng trong hệ thống
 Giải pháp nhà thông minh với khả năng học tập và phản ứng theo thói quen của
người dùng được thiết kế chia thành 4 tầng.
 <p align="center">
  <img width="400" src="https://github.com/phungnhathai/smart-home-proactive/blob/master/image/layer.png">
</p>

 
 #### 1. Tầng vật lý
 <p align="center">
 <img width="400" align="center" src="https://github.com/phungnhathai/smart-home-proactive/blob/master/image/physical-layer.png">
  </p>
  <p align="center">Các thiết bị vật lý trong mô hình</p>
 
| Device       | Số lượng       | Chú thích  |
| ------------- |:-------------:|:-----:|
| ESP8266     | 3 | Mạch nhúng Arduino |
| Servo  | 1 |  Hoạt động xoay để đóng mở cửa |
| RFID| 1 | Checkin & Checkout |
| Sensor HC-SR04 | 1 | Phát hiện người để mở cửa tự động |
| Màn hình oled I2C | 1 | Hiển thị nhiệt độ |
| Đèn led | 6 (1 led RGB) | Hệ thống đèn trong nhà |

 Các thiết bị vật lý trong mô hình

#### 2. Tầng giao tiếp
<p align="center">
<img src="https://github.com/phungnhathai/smart-home-proactive/blob/master/image/mqtt.png">
</p>

Tầng giao tiếp có nhiệm vụ tạo kết nối giữa các thiết bị ở tầng vật lý và server
cloud ở tầng xử lý. Giao thức MQTT được sử dụng để gửi và nhận dữ liệu giữa mạch 
nhúng Arduino như là Subcriber và Broker HiveMQ. Để đảm tính bảo mật, chúng tôi
triển khai giao thức bảo mật TLS ở tầng tranport của giao thức MQTT. Giao thức này
cung cấp sự mã hóa dữ liệu, nhằm đảm bảo dữ liệu bí mật và toàn vẹn trong quá trình
truyền nhận. Ngoài ra, hệ thống còn có cơ chế xác thực trong giao thức MQTT, nghĩa
là khi một Client muốn subcribe hoặc publish đến Broker thì phải được xác thực bằng
username và password.

#### 3. Tầng xử lý
Tầng xử lý là một server ảo hóa được triển khai trên nền tảng điện toán đám
mây **OpenStack**. Server này sẽ các chạy dịch vụ:
* **Web server:** được xây dựng trên framework Django, cùng với Django
Channels hỗ trợ websocket và Eclipse Paho giúp giao tiếp với giữa ứng dụng
web với dịch vụ MQTT.
* **Thuật toán Random Forest:** thực hiện quá trình huấn luyện từ tập dataset
truyền vào, quá trình dự đoán đưa ra lệnh điều khiển các thiết bị ở tầng vật lý
* **Dịch vụ MQTT Broker – HiveMQ:** có nhiệm vụ truyền nhận các lệnh điều
khiển và thu thập trạng thái của thiết bị vật lý.
* **Cơ sở dữ liệu SQLite:** cơ sở dữ liệu lưu trữ các lệnh điều khiển, trạng thái
của các thiết bị vật lý từ thao tác của người dùng ở ứng dụng web theo thời
gian. Dữ liệu này sẽ được xử lý để tạo thành tập dataset phục vụ cho quá trình
huấn luyện. 

#### 4. Tầng ứng dụng
Tầng ứng dụng cung cấp do người dùng một giao diện website để điều khiển
các thiết bị trong nhà từ xa, theo dõi quá trình thu thập dữ liệu và huấn luyện. 
* Giao diện Dashboard cho phép theo dõi trạng thái và điều khiển các thiết bị trong mô hình

<p align="center">
<img src="https://github.com/phungnhathai/smart-home-proactive/blob/master/image/dashboard.png">
</p>
<p align="center">Giao diện Dashboard</p>

* Giao diện Training cho phép quản lý, theo dõi quá trình huấn luyện
<p align="center">
<img src="https://github.com/phungnhathai/smart-home-proactive/blob/master/image/Training.png">
</p>
<p align="center">Giao diện Training</p>
