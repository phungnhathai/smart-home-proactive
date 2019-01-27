# Smart Home with a proactive approach based on Machine Learning
  Những giải pháp Smart Home hiện nay cho phép chúng ta điều khiển, quản lý thông qua sự tương tác của chủ nhà như điều khiển bằng giọng nói hay qua các thiết bị di dộng. Với mô hình Smart Home như trên thì chủ nhà phải thiết lập các quy tắc từ đơn gian đến phức tạp để ngôi nhà hoạt động tốt theo ý của mình, như vậy sẽ gây khó khăn, mất thời gian, bất tiện cho chủ nhà. Smart Home chỉ dừng lại ở khái niệm nhà tự động. Với sự phát triển mạnh mẽ của công nghệ, khái niệm nhà thông minh đã dần thay đổi. Những ngôi nhà sẽ thật sự thông minh nếu có khả năng học hỏi, phản ứng một cách chủ động theo những thói quen, hành vi của chủ nhà. Việc ứng dụng Machine Learning vào Smart Home sẽ giúp ngôi nhà có thể trở nên thông minh hơn.
  
  Ví dụ về việc điều khiển máy lạnh trong ngôi nhà: 
  Khi đi làm về nhà, chủ nhà muốn điều chỉnh nhiệt độ 25°C, đến lúc đi ngủ lại muốn 26°C, đến khi thức dậy lại muốn nhiệt độ     28°C. Với thói quen như vậy, ngôi nhà có thể học hỏi và từ đó có những điều chỉnh phù hợp trong tương lai.
  
 # Thiết kế hệ thống
 
 ## Các tầng trong hệ thống
 <img src="https://imgur.com/Yw80t7b">
 **Tầng vật lý**
 <img src="https://imgur.com/a/0RUkS2v">
| Device | Số lượng | Nhiệm vụ |
|--------------|-------|------|-------
| ESP8266 | 3 | Nhận lệnh điều khiển từ tầng xử lý cũng như thu thập trạng thái của các thiết bị |
| Servor 9G SG90 | 1  | Hoạt động xoay để đóng mở cửa |
| RFID | 1 | Checkin & Checkout |
| HC-SR04 | 1 | Phát hiện người để mở cửa tự động |
| Màn hình oled I2C | 1 | Hiển thị nhiệt độ |
| Đèn led | 6 (1 led RGB) | Hệ thống đèn trong nhà |
