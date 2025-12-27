# esp32-lora-controller
A DIY Long-Range Drone Remote Controller based on ESP32, LoRa Ra-02 (SX1278) and ST7735 Display. Features telemetry, custom PCB design, and low latency configuration.

## Sơ đồ nối dây tay điều khiển

## Wiring Diagram (ASCII mini)

                ┌───────────────────────────────┐
                │            ESP32              │
                │                               │
                │  SPI BUS (shared)             │
                │   GPIO18 = SCK  ──────────────┼───────────┐
                │   GPIO23 = MOSI ──────────────┼───────────┼───────────┐
                │   GPIO19 = MISO ──────────────┼───────────┘           │
                │                               │                       │
                │  ST7735 control               │  LoRa control         │
                │   GPIO15 = TFT_CS  ───────────┼──► ST7735 CS          │
                │   GPIO2  = TFT_DC  ───────────┼──► ST7735 A0/DC       │
                │   GPIO4  = TFT_RST ───────────┼──► ST7735 RESET       │
                │                               │                       │
                │   GPIO5  = LORA_NSS ──────────┼──────────────────────► LoRa NSS/CS
                │   GPIO14 = LORA_RST ──────────┼──────────────────────► LoRa RST
                │   GPIO26 = LORA_DIO0 ─────────┼──────────────────────► LoRa DIO0 (IRQ)
                │                               │
                │  Joysticks (analog)           │
                │   GPIO32 = Throttle (L_VRy)   │
                │   GPIO33 = Yaw      (L_VRx)   │
                │   GPIO34 = Pitch    (R_VRy)   │  (input-only)
                │   GPIO35 = Roll     (R_VRx)   │  (input-only)
                │   GPIO0/13 = SW (optional)    │
                │                               │
                │  Power                         │
                │   3.3V ───────────────┬───────┼───────┬──────────────┐
                │   GND  ───────────────┴───────┼───────┴──────────────┘
                └───────────────────────────────┘

           ┌───────────────────┐                         ┌────────────────────┐
           │   ST7735 Display   │                         │   LoRa Ra-02 (SX1278)│
           │                   │                         │                    │
           │  VCC  ◄───────────┘ (3.3V)                  │  3.3V ◄────────────┘ (3.3V)
           │  GND  ◄────────────  (GND)                  │  GND  ◄─────────────  (GND)
           │  SCK  ◄────────────  GPIO18                 │  SCK  ◄─────────────  GPIO18
           │  SDA  ◄────────────  GPIO23                 │  MOSI ◄─────────────  GPIO23
           │  CS   ◄────────────  GPIO15                 │  MISO ◄─────────────  GPIO19
           │  DC   ◄────────────  GPIO2                  │  NSS  ◄─────────────  GPIO5
           │  RST  ◄────────────  GPIO4                  │  RST  ◄─────────────  GPIO14
           │  BL   ◄────────────  3.3V                   │  DIO0 ◄─────────────  GPIO26
           └───────────────────┘                         │  (add 100µF cap near VCC) │
                                                         └────────────────────┘

           ┌──────────────────────┐
           │     2x Joystick      │
           │                      │
           │  VCC  ◄── 3.3V       │
           │  GND  ◄── GND        │
           │  L_VRy (Throttle) ──► GPIO32 │
           │  L_VRx (Yaw)      ──► GPIO33 │
           │  R_VRy (Pitch)    ──► GPIO34 │
           │  R_VRx (Roll)     ──► GPIO35 │
           │  SW (optional)    ──► GPIO0 or GPIO13 │
           └──────────────────────┘
