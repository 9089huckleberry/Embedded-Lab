# Arduino MPU6050 + Processing 3D Cone Visualization

This project uses an **Arduino Uno** and an **MPU6050 (gyroscope + accelerometer)** to control a 3D rotating cone in **Processing**. The gyroscope data is smoothed to avoid jittery movement.

---

## 🔌 Hardware Required

- Arduino Uno
- MPU6050 module
- Jumper wires
- USB cable

### 📦 Wiring (Arduino <-> MPU6050)

| MPU6050 Pin | Arduino Uno Pin |
|-------------|------------------|
| VCC         | 5V               |
| GND         | GND              |
| SDA         | A4               |
| SCL         | A5               |

---

## 📥 Arduino Code

Upload the following code to your Arduino:

```cpp
#include <Wire.h>
#include <MPU6050.h>

MPU6050 mpu;

void setup() {
  Serial.begin(9600);
  Wire.begin();
  mpu.initialize();

  if (!mpu.testConnection()) {
    Serial.println("MPU6050 connection failed!");
    while (1);
  }
}

void loop() {
  int16_t ax, ay, az;
  int16_t gx, gy, gz;

  mpu.getMotion6(&ax, &ay, &az, &gx, &gy, &gz);
  Serial.print(ax); Serial.print(",");
  Serial.print(ay); Serial.print(",");
  Serial.print(az); Serial.print(",");
  Serial.print(gx); Serial.print(",");
  Serial.print(gy); Serial.print(",");
  Serial.println(gz);
  delay(20);
}
