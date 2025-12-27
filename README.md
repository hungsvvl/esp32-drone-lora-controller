# esp32-lora-controller
A DIY Long-Range Drone Remote Controller based on ESP32, LoRa Ra-02 (SX1278) and ST7735 Display. Features telemetry, custom PCB design, and low latency configuration.

## Sơ đồ nối dây tay điều khiển

### 1) Khối trung tâm: SPI Bus (dùng chung)
> ESP32 chia sẻ SPI cho cả màn hình ST7735 và LoRa Ra-02 (SX1278)

| Tín hiệu SPI | ESP32 GPIO | ST7735 Display | LoRa Ra-02 (SX1278) |
|---|---:|---|---|
| SCK (CLK) | GPIO 18 | SCK / SCL | SCK |
| MISO | GPIO 19 | *(không cần nối)* | MISO |
| MOSI | GPIO 23 | SDA / MOSI | MOSI |

---

### 2) Khối màn hình ST7735
| Chân màn hình | ESP32 GPIO | Ghi chú |
|---|---:|---|
| LED (BL) | 3.3V | Đèn nền (có thể nối qua điện trở 100Ω nếu quá sáng) |
| SCK | GPIO 18 | Dùng chung SPI |
| SDA (MOSI) | GPIO 23 | Dùng chung SPI |
| A0 (DC) | GPIO 2 | Chân lệnh/dữ liệu *(có thể dùng GPIO 4 tuỳ cấu hình)* |
| RESET | GPIO 4 | Reset màn hình |
| CS | GPIO 15 | Chọn chip màn hình |
| GND | GND | Mass |
| VCC | 3.3V | Nguồn |

---

### 3) Khối LoRa Ra-02 (SX1278)
| Chân LoRa | ESP32 GPIO | Ghi chú |
|---|---:|---|
| NSS (CS) | GPIO 5 | Chọn chip LoRa |
| DIO0 | GPIO 26 | Chân ngắt (quan trọng để nhận gói tin) |
| RST | GPIO 14 | Reset LoRa |
| SCK | GPIO 18 | Dùng chung SPI |
| MISO | GPIO 19 | Dùng chung SPI |
| MOSI | GPIO 23 | Dùng chung SPI |
| 3.3V | 3.3V | **Khuyến nghị:** hàn thêm tụ 100µF gần module |
| GND | GND | Mass |

---

### 4) Khối Joystick (2 joystick)
| Chức năng | Joystick | ESP32 GPIO | Ghi chú |
|---|---|---:|---|
| GA (Throttle) | Trái – Dọc (VRy) | GPIO 32 | Analog |
| XOAY (Yaw) | Trái – Ngang (VRx) | GPIO 33 | Analog |
| TIẾN/LÙI (Pitch) | Phải – Dọc (VRy) | GPIO 34 | **Input only** (chuẩn) |
| NGHIÊNG (Roll) | Phải – Ngang (VRx) | GPIO 35 | **Input only** (chuẩn) |
| Nút bấm (SW) | SW (Trái/Phải) | *(tuỳ chọn)* | Có thể nối GPIO 0 hoặc GPIO 13 |
| Nguồn | VCC | 3.3V | Nguồn joystick |
| Mass | GND | GND | Mass |
