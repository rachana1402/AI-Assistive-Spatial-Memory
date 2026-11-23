# 🦯 AI Assistive System for Visually Impaired Navigation

Real-time object detection and voice-guided navigation system for visually impaired users using YOLOv8 and spatial memory.

[![Python 3.12](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![YOLOv8](https://img.shields.io/badge/YOLO-v8-green.svg)](https://github.com/ultralytics/ultralytics)
[![OpenCV](https://img.shields.io/badge/OpenCV-5.0-red.svg)](https://opencv.org/)

---

## 🎯 Features

- ✅ **Real-time Object Detection** - YOLOv8n detecting 80 COCO object classes at 12.40 FPS
- ✅ **Distance Estimation** - Monocular distance calculation with accuracy within 0.2m
- ✅ **Spatial Memory System** - Remembers object locations (100% accuracy)
- ✅ **Voice Commands** - Natural language queries ("Find the bottle", "Where is the chair")
- ✅ **Audio Feedback** - Text-to-speech navigation guidance
- ✅ **Lightweight** - Runs on consumer hardware (AMD Ryzen 5, 374MB RAM)

---

## 🚀 Quick Start

### Installation

```powershell
# 1. Clone repository
git clone https://github.com/YourUsername/AI-Assistive-System.git
cd AI-Assistive-System

# 2. Create virtual environment
python -m venv venv
.\venv\Scripts\Activate.ps1

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the system
python navigation_main.py
```

### First Run

1. Camera window opens showing detected objects
2. Speak voice commands into your microphone:
   - **"Find the bottle"** → System locates and guides you to bottle
   - **"Where is the chair"** → System recalls last seen position
   - **"What do you see"** → System lists all detected objects
3. Press **'Q'** to quit

📖 **Full documentation:** See [`INSTALLATION_GUIDE.md`](INSTALLATION_GUIDE.md)

---

## 📊 Performance Metrics

| Metric | Value | Hardware |
|--------|-------|----------|
| **Inference Time** | 71.96 ms | AMD Ryzen 5 5625U |
| **System FPS** | 12.40 FPS | 16GB RAM |
| **RAM Usage** | 374.79 MB | Windows 11 |
| **Detection Accuracy** | 37.3 mAP@0.5:0.95 | COCO val2017 |
| **Spatial Memory** | 100% accuracy | 316 operations |
| **Voice Recognition** | 90.48% success | 21 test cases |

---

## 🛠️ System Requirements

### Minimum
- **CPU:** Intel Core i3 / AMD Ryzen 3
- **RAM:** 8 GB
- **Camera:** Any USB webcam (640×480)
- **Microphone:** Built-in or USB
- **OS:** Windows 10/11 (64-bit)

### Recommended
- **CPU:** AMD Ryzen 5 / Intel Core i5 (6+ cores)
- **RAM:** 16 GB
- **Camera:** 720p or higher
- **GPU:** Optional (NVIDIA for GPU acceleration)

---

## 📁 Project Structure

```
AI-Assistive-System/
│
├── navigation_main.py              # Main entry point
├── yolo_voice_manager.py           # Alternative main (with face recognition)
├── requirements.txt                # Python dependencies
│
├── navigation/                     # Navigation modules
│   ├── object_memory.py           # Spatial memory system
│   ├── target_search.py           # Object search logic
│   ├── distance_estimator.py      # Distance calculation
│   └── ...
│
├── voice/                          # Voice interaction
│   ├── voice_input.py             # Microphone input
│   └── voice_manager.py           # TTS output
│
├── yolov8n.pt                      # YOLOv8n model weights (3.2 MB)
│
└── docs/                           # Documentation
    ├── INSTALLATION_GUIDE.md      # Complete setup guide
    ├── SPATIAL_MEMORY_DOCUMENTATION.md
    └── FPS_METRICS_FORMULAS.md
```

---

## 🎤 Voice Commands

| Command | Description | Example Output |
|---------|-------------|----------------|
| `Find [object]` | Search for and navigate to object | *"Bottle is on your left, 1.5 meters away"* |
| `Where is [object]` | Recall object from spatial memory | *"Chair was last seen ahead, 2 meters away"* |
| `What do you see` | List all currently detected objects | *"I see: person, chair, bottle, laptop"* |
| `Stop navigation` | Exit the system | *System shuts down* |

### Supported Objects (80 Classes)
person, chair, bottle, cup, laptop, cell phone, book, clock, backpack, handbag, 
keyboard, mouse, tv, couch, dining table, bed, toilet, door, and 62 more...

[Full COCO class list](https://github.com/ultralytics/ultralytics/blob/main/ultralytics/cfg/datasets/coco.yaml)

---

## 🧪 Testing Components

Test individual components before running the full system:

```powershell
# Test camera
python camera_test.py

# Test object detection
python yolo_test.py

# Test distance estimation
python distance_estimator_test.py

# Test voice recognition
python voice_command_test.py

# Test microphone setup
python test_microphone.py
```

---

## 🏗️ System Architecture

```
Camera Input → YOLOv8 Detection → Distance Estimation
                                          ↓
Voice Input ← Spatial Memory ← Object Localization
     ↓
Voice Recognition → Navigation Guidance → TTS Output
```

### Processing Pipeline

1. **Frame Capture** (2-3ms) - Grab frame from camera
2. **Pre-processing** (1-2ms) - Resize, normalize
3. **YOLO Detection** (71.96ms) - Object detection inference
4. **Post-processing** (2-3ms) - Non-Maximum Suppression
5. **Distance Estimation** (1-2ms) - Calculate object distances
6. **Spatial Memory** (0.5ms) - Store object locations
7. **Voice Processing** (async) - Handle voice commands
8. **Navigation Guidance** (async) - Generate directions

**Total:** ~80ms per frame = **12.40 FPS**

---

## 📖 Documentation

- 📘 [`INSTALLATION_GUIDE.md`](INSTALLATION_GUIDE.md) - Complete setup instructions
- 📗 [`SPATIAL_MEMORY_DOCUMENTATION.md`](SPATIAL_MEMORY_DOCUMENTATION.md) - Memory system details
- 📙 [`FPS_METRICS_FORMULAS.md`](FPS_METRICS_FORMULAS.md) - Performance calculations
- 📕 [`OBJECT_STORAGE_EXPLAINED.md`](OBJECT_STORAGE_EXPLAINED.md) - Data structures
- 📔 [`ACTUAL_METRICS_EVALUATED.md`](ACTUAL_METRICS_EVALUATED.md) - Evaluation results

---

## 🔧 Troubleshooting

### Camera Not Working
```powershell
# Test camera connection
python camera_test.py

# Try different camera index (0, 1, 2...)
python diag_camera.py
```

### Microphone Not Recognized
```powershell
# List all audio devices
python test_microphone.py

# Update device index in navigation_main.py (line ~285)
voice_input = VoiceInput(device_index=YOUR_INDEX)
```

### Low FPS Performance
- Close other applications
- Use smaller camera resolution (640×480)
- Reduce detection confidence threshold
- Try YOLOv8n instead of larger models

For more troubleshooting: See [INSTALLATION_GUIDE.md](INSTALLATION_GUIDE.md#troubleshooting)

---

## 🎓 Research Paper

This system was developed as part of research on assistive navigation for visually impaired users.

**Key Contributions:**
1. Real-time object detection optimized for embedded systems
2. Spatial memory system with 100% accuracy
3. Natural voice command interface (90.48% recognition rate)
4. Comprehensive performance evaluation on consumer hardware

**Citation:**
```bibtex
@misc{ai-assistive-system-2026,
  title={AI Assistive System for Visually Impaired Navigation},
  author={[Your Name]},
  year={2026},
  publisher={GitHub},
  url={https://github.com/YourUsername/AI-Assistive-System}
}
```

---

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## ⚠️ Safety Disclaimer

**This is a research prototype and should NOT be used as the sole navigation aid.**

Always use with:
- ✅ A human guide or companion
- ✅ Traditional assistive tools (cane, guide dog)
- ✅ Proper training and familiarization
- ✅ Safe, controlled environments

**Limitations:**
- Detection accuracy depends on lighting and occlusion
- Cannot detect all hazards (stairs, low obstacles, wet floors)
- Voice recognition may fail in noisy environments
- Distance estimation has ~10-20% margin of error

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**Dependencies:**
- YOLOv8: AGPL-3.0 License
- OpenCV: Apache 2.0 License
- PyTorch: BSD License

---

## 🌟 Acknowledgments

- **Ultralytics YOLOv8** - Object detection framework
- **OpenCV** - Computer vision library
- **SpeechRecognition** - Voice command processing
- **pyttsx3** - Text-to-speech engine

---

## 📧 Contact

- **GitHub Issues:** [Report bugs or request features](https://github.com/YourUsername/AI-Assistive-System/issues)
- **Email:** your.email@example.com
- **Research Paper:** [Link to paper when published]

---

## 🗺️ Roadmap

### Current Version (v1.0)
- ✅ YOLOv8 object detection
- ✅ Spatial memory system
- ✅ Voice command interface
- ✅ Distance estimation

### Planned Features (v2.0)
- 🔄 GPU acceleration support
- 🔄 Multi-camera support
- 🔄 Obstacle avoidance pathfinding
- 🔄 Indoor mapping and localization
- 🔄 Multi-language voice support
- 🔄 Mobile app (Android/iOS)
- 🔄 Cloud-based enhancement

---

## 📊 Statistics

![GitHub stars](https://img.shields.io/github/stars/YourUsername/AI-Assistive-System?style=social)
![GitHub forks](https://img.shields.io/github/forks/YourUsername/AI-Assistive-System?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/YourUsername/AI-Assistive-System?style=social)

---

**Made with ❤️ for accessibility and inclusion**

*Last Updated: November 2026*

# AI-Based Assistive Spatial Memory and Guidance System for Visually Impaired Users

## Overview

The AI-Based Assistive Spatial Memory and Guidance System is designed to improve independent mobility and environmental awareness for visually impaired individuals.

The system uses computer vision, artificial intelligence, and voice interaction to identify objects, detect obstacles, recognize familiar people, and provide audio-based guidance.

Unlike conventional object detection systems that only identify objects in the current camera frame, this project introduces **Spatial Memory and Contextual Recall**, which enables the system to remember previously detected objects and provide their last known location and contextual information when requested by the user.

## Key Features

- **Real-Time Object Detection:** Identifies objects in the user's surroundings using YOLO.
- **Voice-Assisted Navigation:** Provides audio guidance through voice interaction.
- **Obstacle Detection:** Identifies nearby obstacles and communicates their direction, such as left, right, or front.
- **Face Recognition:** Recognizes familiar individuals.
- **Add Person:** Allows users to register and store information about familiar people.
- **Spatial Memory:** Stores information about previously detected objects.
- **Contextual Recall:** Retrieves the last known location, detection time, and description of an object when it is not visible in the current frame.
- **Voice-Based Interaction:** Enables users to interact with the system through spoken commands.

## Technology Stack

- **Programming Language:** Python
- **Computer Vision:** OpenCV
- **Object Detection:** YOLO
- **Face Recognition:** Face Recognition / Computer Vision
- **Speech Interaction:** Speech Recognition and Text-to-Speech
- **AI & Machine Learning:** Object Detection and Image Processing

## How It Works

1. The camera captures the user's surroundings.
2. The YOLO model detects objects in real time.
3. The system identifies obstacles and provides directional voice guidance.
4. Detected objects are stored in spatial memory along with their contextual information.
5. When the user asks for an object, the system first checks the current camera frame.
6. If the object is not currently visible, the system retrieves its previously stored information, including its last known position and detection time.
7. The system communicates the information through voice output.

## Project Innovation

The major contribution of this project is the integration of **Spatial Memory and Contextual Recall** into an AI-based assistive navigation system.

For example, if a user asks, "Where is my laptop?" and the laptop is not visible in the current camera frame, the system can retrieve its previously recorded location and the time it was last detected.

This provides additional environmental context beyond conventional real-time object detection.

## Project Objective

To develop an intelligent, voice-assisted system that enhances environmental awareness and supports greater independence for visually impaired individuals through real-time object detection, navigation assistance, and contextual memory.

## Future Enhancements

- Integration with a mobile application.
- Improved object-location tracking.
- More accurate spatial mapping and indoor navigation.
- Integration with wearable assistive devices.
- Enhanced contextual understanding using AI models.

## Project Type

Final Year Engineering Project – Information Science and Engineering.
