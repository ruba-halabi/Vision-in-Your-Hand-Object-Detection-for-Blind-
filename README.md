# Vision-in-Your-Hand-Object-Detection-for-Blind-
Graduation Project: An AI-powered assistive system for the blind using YOLO
# 👁️ Smart HandGuide for the Visually Impaired

**Smart HandGuide** is an IoT and AI-powered assistive wearable device designed to enhance mobility, independence, and safety for visually impaired individuals. Built on the **Raspberry Pi 4**, it combines real-time computer vision object recognition with ultrasonic distance monitoring to deliver multi-modal sensory feedback (audio name alerts and distance-based buzzer beeps).

---

## 📸 Key Features

- **Real-Time Object Detection:** Utilizes **YOLOv8** to identify objects in front of the user via a USB webcam.
- **Audio Announcements (Text-to-Speech):** Converts detected object labels into natural spoken audio via pre-recorded alerts or `pyttsx3` TTS engine.
- **Obstacle Distance Warning:** Uses an **HC-SR04 Ultrasonic Sensor** to measure distance to nearby obstacles.
- **Adaptive Beep Alerts:** Adjusts buzzer frequency depending on proximity:
  - **$\le$ 50 cm:** Rapid alarm beeps
  - **50 cm - 100 cm:** Medium-speed beeps
  - **100 cm - 150 cm:** Slow warning beeps
- **Interactive Control Button:** Dedicated Push Button to toggle ultrasonic sensor alerts on and off instantly.

---

## 🛠️ Hardware & Components

| Component | Quantity | Description / Pin Connection |
| :--- | :---: | :--- |
| **Raspberry Pi 4 Model B** | 1 | Main processing unit |
| **USB Camera** | 1 | Captures real-time environment frames |
| **HC-SR04 Ultrasonic Sensor** | 1 | **TRIG:** GPIO 23, **ECHO:** GPIO 24 |
| **Piezo Buzzer** | 1 | Connected to **GPIO 17** |
| **Push Button** | 1 | Connected to **GPIO 16** (Internal Pull-Up enabled) |
| **Audio Output Device** | 1 | Speaker / Headphones for TTS feedback |

---

## 💻 Tech Stack & Dependencies

- **Programming Language:** Python 3
- **Computer Vision:** OpenCV (`cv2`), Ultralytics `YOLOv8`
- **Hardware Control:** `RPi.GPIO`
- **Audio Engine:** `pyttsx3`, `mpg321` (Command-line audio player)
- **Data & Numeric Processing:** `NumPy`

---

## ⚙️ System Workflow

1. **System Boot:** Waiting 15 seconds upon booting Raspberry Pi to ensure full initialization.
2. **Vision Loop:** 
   - Captures frame from USB Webcam $\rightarrow$ Saves image.
   - Feeds image into **YOLOv8** model $\rightarrow$ Detects class objects.
   - Plays corresponding sound file from `/home/pi/ttsmaker_com/` or falls back to system TTS engine.
3. **Distance Monitoring Loop:**
   - Checks Push Button state to toggle sensor active mode.
   - Measures distance in centimeters using HC-SR04 pulse duration.
   - Triggers buzzer frequency based on distance ranges.

---

## 🚀 Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/YOUR_USERNAME/Smart-HandGuide.git](https://github.com/YOUR_USERNAME/Smart-HandGuide.git)
   cd Smart-HandGuide
Install required dependencies:
pip3 install ultralytics opencv-python pyttsx3 numpy RPi.GPIO
sudo apt-get install mpg321

Download YOLOv8 Weights:
Place your pre-trained model file (yolov8m.pt) in the project root or /home/pi/ directory.

Run the application:
python3 main.py
