# esp32-lora-controller
A DIY Long-Range Drone Remote Controller based on ESP32, LoRa Ra-02 (SX1278) and ST7735 Display. Features telemetry, custom PCB design, and low latency configuration
**Sơ đồ nối dây tay điều khiển
**
KHỐI TRUNG TÂM: CÁC DÂY DÙNG CHUNG (SPI BUS)
Tên Chân (SPI)	Chân ESP32	Nối vào Màn Hình	 Nối vào LoRa Ra-02
SCK (CLK)	       GPIO 18	  Chân SCK/SCL       	Chân SCK
MISO	           GPIO 19  (Không cần nối)	      Chân MISO
MOSI	           GPIO 23	  Chân SDA/MOSI      	Chân MOSI

Chân  Màn Hình 	Chân ESP32	      Ghi chú
LED (BL)	     3.3V	Đèn nền        (Có thể nối qua điện trở 100Ω nếu quá sáng)
SCK	           GPIO 18	           Dùng chung (như bảng trên)
SDA (MOSI)	   GPIO 23	           Dùng chung (như bảng trên)
A0 (DC)	       GPIO 2	             Chân lệnh/dữ liệu (Hoặc GPIO 4 tùy cấu hình)
RESET	         GPIO 4            	Chân Reset màn hình
CS	           GPIO 15	          Chọn chip màn hình
GND	           GND	
VCC	          3.3V

KHỐI LORA (Ra-02 SX1278)
Chân LoRa	  Chân ESP32	  Ghi chú
NSS (CS)	  GPIO 5	      Chọn chip LoRa
DIO0	      GPIO 26	      Chân ngắt (Quan trọng để nhận gói tin)
RST	        GPIO 14	      Chân Reset LoRa
SCK	        GPIO 18	      Dùng chung
MISO	      GPIO 19	      Dùng chung
MOSI	      GPIO 23	      Dùng chung
3.3V	      3.3V	        Hàn thêm tụ 100µF vào đây
GND       	GND

KHỐI JOYSTICK
Chức năng	        Joystick	          Chân ESP32	    Ghi chú
GA (Throttle)	    Trái - Dọc (VRy)	  GPIO 32	
XOAY (Yaw)	      Trái - Ngang (VRx)	GPIO 33	
TIẾN/LÙI (Pitch)	Phải - Dọc (VRy)	  GPIO 34	        Input Only (Chuẩn)
NGHIÊNG (Roll)	  Phải - Ngang (VRx)	GPIO 35	        Input Only (Chuẩn)
Nút bấm (SW)	    SW (Trái/Phải)	   (Tùy chọn)	      Có thể nối vào GPIO 0 hoặc 13
Nguồn	            VCC	               3.3V	
Mass	            GND	               GND
