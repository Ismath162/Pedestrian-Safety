# 🚦 Pedestrian Safety System using Arduino

A simple **pedestrian safety prototype** built using **Arduino UNO**, **Ultrasonic Sensor (HC-SR04)**, and a **Servo Motor**.  
The system detects nearby objects and activates a safety response automatically.

---

## 🔍 Overview
- Measures distance using an ultrasonic sensor  
- Detects objects within **20 cm**  
- Rotates servo motor to indicate safety action  
- Displays distance in Serial Monitor  

---

## 🧰 Components
- Arduino UNO  
- HC-SR04 Ultrasonic Sensor  
- Servo Motor  
- Jumper Wires  

---

## 🔌 Connections
**Ultrasonic Sensor**
- VCC → 5V  
- GND → GND  
- TRIG → D9  
- ECHO → D10  

**Servo Motor**
- Red → 5V  
- Brown/GND → GND  
- Yellow/Orange → D6  

---

## 💻 Code
```cpp
#include <Servo.h>

#define TRIG_PIN 9
#define ECHO_PIN 10
#define SERVO_PIN 6

Servo myServo;

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  myServo.attach(SERVO_PIN);
  Serial.begin(9600);
}

void loop() {
  long duration;
  int distance;

  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  duration = pulseIn(ECHO_PIN, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.println(distance);

  if (distance < 20)
    myServo.write(90);
  else
    myServo.write(0);

  delay(100);
}
