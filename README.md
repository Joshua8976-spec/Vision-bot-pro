# 🤖 Vision Bot Pro

**An AI-powered autonomous robot built from scratch at home.**

Object detection · Face tracking · Obstacle avoidance · Robotic arm · Wi-Fi control

---

## 📸 Demo

> *Build in progress — demo GIF and photos coming soon!*

---

## 🧠 Overview

Vision Bot Pro is a fully autonomous AI-powered robot built from scratch using a **Raspberry Pi 5 4GB** as the central processing unit and an **Arduino UNO R3** for real-time motor control.

The robot combines computer vision, machine learning, and embedded systems to perform:
- Real-time **object detection and following** using OpenCV
- **Face tracking** using MediaPipe
- **Obstacle avoidance** using an HC-SR04 ultrasonic sensor
- **Object retrieval** using a 3-axis SG90 servo arm
- **Remote monitoring** via a Flask Wi-Fi dashboard

All AI inference runs **completely on-device** — no cloud, no internet required.

---

## ⚙️ Hardware

| Component | Purpose |
|---|---|
| Raspberry Pi 5 4GB | Main brain — Python + AI inference |
| Arduino UNO R3 | Real-time motor + servo control |
| Pi Camera Module V2 | Vision input |
| L298N Motor Driver | DC wheel motor control |
| DC Gear Motors x2 | Wheel movement |
| HC-SR04 Ultrasonic Sensor | Obstacle detection |
| SG90 Servo Motors x3 | Robotic arm (base, joint, gripper) |
| PCA9685 Servo Driver | I2C servo control from Pi |
| 840-point Breadboard | Prototyping |
| 9V Battery Pack | Powers motors via L298N |
| Official 27W USB-C PSU | Powers Raspberry Pi 5 |

---

## 🛠️ Software Stack

| Tool | Purpose |
|---|---|
| Python 3 | Main programming language on Pi |
| OpenCV (cv2) | Object detection and color tracking |
| MediaPipe | Face detection and tracking |
| TensorFlow Lite | On-device AI object identification |
| COCO model | Pre-trained 80-class object detection |
| picamera2 | Pi Camera control |
| Flask | Wi-Fi web dashboard |
| MJPEG stream | Live video over Wi-Fi |
| Arduino IDE | Motor control firmware |
| pyserial | Pi to Arduino serial communication |
| RPi.GPIO | Raspberry Pi GPIO control |

---

## 🗺️ Build Phases

### ✅ Phase 1 — Wheeled Base
> Get the robot moving and avoiding walls

- Wire DC motors to Arduino via L298N motor driver
- Code forward, backward, left, right movement
- Add HC-SR04 ultrasonic sensor for obstacle detection and auto-stop

**Goal:** Robot drives autonomously, stops before obstacles, controllable over USB serial

---

### 🔄 Phase 2 — Computer Vision
> See and follow objects and faces in real time

- Connect Pi Camera Module, test with picamera2
- Use OpenCV color masking to detect and follow a colored object
- Add MediaPipe face detection and tracking

**Goal:** Robot locks onto a face or colored object and steers to keep it centered in frame

---

### ⏳ Phase 3 — AI + Robotic Arm
> Identify objects by name and pick them up

- Build 3-DOF servo arm using SG90 motors + PCA9685 driver
- Run TensorFlow Lite COCO model for real-time object identification
- Set up Flask web server for live Wi-Fi video and remote control

**Goal:** Robot identifies objects by name, navigates toward them, and picks them up with the servo arm

---

## 📁 Repository Structure

```
VisionBotPro/
├── README.md
├── phase1_movement/
│   ├── arduino/
│   │   └── motor_control.ino
│   └── python/
│       └── serial_control.py
├── phase2_vision/
│   ├── opencv/
│   │   └── color_tracking.py
│   └── mediapipe/
│       └── face_tracking.py
├── phase3_ai_arm/
│   ├── tflite/
│   │   └── object_detection.py
│   ├── servo/
│   │   └── arm_control.py
│   └── flask/
│       └── dashboard.py
├── docs/
│   ├── VisionBotPro_Blueprint.pdf
│   ├── VisionBotPro_CircuitDiagram.pdf
│   └── VisionBotPro_CircuitDiagram_Corrected.pdf
└── assets/
    └── images/
```

---

## 🔌 Circuit Connections

Full wiring reference is available in [`docs/VisionBotPro_CircuitDiagram.pdf`](docs/VisionBotPro_CircuitDiagram.pdf)

**Quick reference:**

| From | To | Connection |
|---|---|---|
| Pi Camera V2 | Raspberry Pi 5 | CSI ribbon cable |
| Raspberry Pi 5 | Arduino UNO | USB-A to USB-B |
| Raspberry Pi 5 | PCA9685 | I2C: GPIO 2 (SDA) + GPIO 3 (SCL) |
| PCA9685 | SG90 Servos x3 | Ch 0 base / Ch 1 arm / Ch 2 gripper |
| Arduino UNO | L298N | IN1-4: pins 2-5 / ENA-ENB: pins 6-7 |
| L298N | DC Motors x2 | OUT1/2 left / OUT3/4 right |
| Arduino UNO | HC-SR04 | TRIG: D9 / ECHO: D10 / VCC: 5V |
| 9V Battery | L298N | + to 12V / - to GND |

---

## 🚀 Getting Started

### Prerequisites
```bash
# On Raspberry Pi 5
sudo apt update && sudo apt upgrade -y
pip install opencv-python mediapipe tflite-runtime picamera2 flask pyserial
```

### Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/VisionBotPro.git
cd VisionBotPro
```

### Phase 1 — Run motor control
```bash
# Upload motor_control.ino to Arduino first via Arduino IDE
python phase1_movement/python/serial_control.py
```

### Phase 2 — Run color tracking
```bash
python phase2_vision/opencv/color_tracking.py
```

### Phase 3 — Run full AI robot
```bash
python phase3_ai_arm/tflite/object_detection.py
```

---

## 📖 Documentation

| Document | Description |
|---|---|
| [Blueprint PDF](docs/VisionBotPro_Blueprint.pdf) | Full project plan, hardware, software, goals |
| [Circuit Diagram PDF](docs/VisionBotPro_CircuitDiagram.pdf) | Complete wiring reference |
| [Correction Notes PDF](docs/VisionBotPro_CircuitDiagram_Corrected.pdf) | Circuit diagram annotations |

---

## 💡 Why I Built This

I turned down a ₹40,000 10-day robotics camp and decided to build my own lab at home instead. Every component bought separately, every line of code written myself, every bug debugged from scratch.

This project is part of my personal AI and robotics journey as I head into 11th grade with AI as my major — and aim for bigger goals beyond that.

---

## 📊 Progress

- [ ] Phase 1 — Wheeled base + obstacle avoidance
- [ ] Phase 2 — Camera + OpenCV object and face tracking
- [ ] Phase 3 — TFLite AI detection + servo arm + Wi-Fi dashboard

---

## 🔗 Resources

- [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/)
- [OpenCV Python Tutorials](https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html)
- [MediaPipe Solutions](https://developers.google.com/mediapipe)
- [TensorFlow Lite Guide](https://www.tensorflow.org/lite/guide)
- [Paul McWhorter Pi Tutorials](https://www.youtube.com/@paulmcwhorter)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

*Built with curiosity, determination, and a lot of debugging* 🔧
