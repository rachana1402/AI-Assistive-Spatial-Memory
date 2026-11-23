# AI Assistive System for Visually Impaired Navigation
## Complete Installation and Usage Guide

---

## 📋 Table of Contents

1. [System Requirements](#system-requirements)
2. [Prerequisites Installation](#prerequisites-installation)
3. [Software Installation](#software-installation)
4. [Hardware Setup](#hardware-setup)
5. [Running the System](#running-the-system)
6. [Usage Instructions](#usage-instructions)
7. [Troubleshooting](#troubleshooting)
8. [System Architecture](#system-architecture)

---

## 💻 System Requirements

### Minimum Hardware Requirements
- **Processor:** Intel Core i3 or AMD Ryzen 3 (or better)
- **RAM:** 8 GB (16 GB recommended)
- **Storage:** 5 GB free space
- **Camera:** USB webcam or laptop built-in camera (640×480 minimum)
- **Microphone:** Any USB or built-in microphone
- **Speakers/Headphones:** For voice feedback

### Recommended Hardware (Used in Development)
- **Processor:** AMD Ryzen 5 5625U (6 cores, 2.3 GHz)
- **RAM:** 16 GB
- **Camera:** 720p or higher
- **OS:** Windows 10/11 (64-bit)

### Operating System Support
- ✅ **Windows 10/11** (Primary - Fully Tested)
- ⚠️ **Linux** (Requires modification of audio libraries)
- ⚠️ **macOS** (Requires modification of audio libraries)

---

## 🔧 Prerequisites Installation

### Step 1: Install Python 3.12

1. Download Python 3.12.0 or later from: https://www.python.org/downloads/
2. During installation:
   - ✅ **Check "Add Python to PATH"**
   - ✅ Select "Install for all users"
   - ✅ Click "Install Now"

3. Verify installation:
```powershell
python --version
```
Expected output: `Python 3.12.0` (or higher)

### Step 2: Install Git (Optional - for cloning repository)

1. Download Git from: https://git-scm.com/downloads
2. Install with default settings
3. Verify:
```powershell
git --version
```

### Step 3: Install Visual C++ Redistributable (Required for PyAudio)

1. Download from: https://aka.ms/vs/17/release/vc_redist.x64.exe
2. Run installer
3. Restart if prompted

---

## 📦 Software Installation

### Method 1: Clone from GitHub (Recommended)

1. **Open PowerShell or Command Prompt**

2. **Navigate to your desired installation directory:**
```powershell
cd C:\Users\YourUsername\Desktop
```

3. **Clone the repository:**
```powershell
git clone https://github.com/YourUsername/AI-Assistive-System.git
cd AI-Assistive-System
```

### Method 2: Download ZIP

1. Download the ZIP file from GitHub
2. Extract to your desired location
3. Open PowerShell in that folder

---

### Install Python Dependencies

1. **Navigate to project directory:**
```powershell
cd C:\Users\YourUsername\Desktop\AI-Assistive-System
```

2. **Create virtual environment (recommended):**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

If you get an execution policy error, run:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

3. **Install required packages:**
```powershell
pip install --upgrade pip
pip install -r requirements.txt
```

**Installation time:** 5-10 minutes depending on internet speed

4. **Verify installation:**
```powershell
python -c "import cv2, torch, ultralytics; print('All packages installed successfully!')"
```

---

### Download YOLO Model Weights

The required model files should already be in the project:
- ✅ `yolov8n.pt` - Main detection model
- ✅ `yolov10n.pt` - Alternative model (optional)
- ✅ `yolov8n.onnx` - ONNX format (optional)

If missing, download from:
```powershell
# YOLOv8n (3.2 MB)
Invoke-WebRequest -Uri "https://github.com/ultralytics/assets/releases/download/v0.0.0/yolov8n.pt" -OutFile "yolov8n.pt"
```

---

## 🎤 Hardware Setup

### Camera Setup

1. **Connect your webcam** (or ensure built-in camera is enabled)

2. **Test camera:**
```powershell
python camera_test.py
```

**Expected:** A window should open showing your camera feed. Press 'q' to quit.

3. **If camera doesn't work:**
   - Check Device Manager → Cameras
   - Try different USB ports
   - Update camera drivers

### Microphone Setup

1. **Configure Windows microphone:**
   - Settings → System → Sound → Input
   - Select your microphone
   - Test microphone and adjust volume

2. **Find microphone device index:**
```powershell
python test_microphone.py
```

**Output example:**
```
Available audio input devices:
  [0] Microsoft Sound Mapper - Input
  [1] Microphone (Realtek High Definition Audio)
  [12] Microphone Array (USB Audio Device)
```

3. **Note your microphone device index** (you'll need this later)

4. **Test voice recognition:**
```powershell
python voice_command_test.py
```

Speak clearly: "Find the bottle" or "Where is the chair"

---

## 🚀 Running the System

### Quick Start (Default Settings)

```powershell
python navigation_main.py
```

### With Custom Microphone

If your microphone isn't device index 12, edit `navigation_main.py`:

**Line 285 (approximately):**
```python
voice_input = VoiceInput(device_index=12)  # Change 12 to your device index
```

Or use the alternative main file:
```powershell
python yolo_voice_manager.py
```

### Expected Startup Output

```
[INFO] Initializing YOLOv8 model...
[INFO] Model loaded successfully
[INFO] Starting camera...
[INFO] Camera initialized
[INFO] Starting voice recognition...
[INFO] Voice input ready on device 12
[INFO] System ready. Press 'q' to quit.
```

---

## 🎮 Usage Instructions

### System Modes

The system operates in real-time continuous detection mode with voice command support.

### Display Window

A window will show:
- **Green boxes:** Detected objects with labels
- **Distance labels:** Estimated distance in meters
- **Direction indicators:** Left/Center/Right zones
- **FPS counter:** Processing speed

### Voice Commands

Speak clearly into your microphone:

| Command | Action | Example Output |
|---------|--------|----------------|
| **"Find [object]"** | Search for specific object | "Bottle is on your left, 1.5 meters away" |
| **"Where is [object]"** | Locate object in memory | "Chair was last seen ahead, 2 meters away" |
| **"What do you see"** | List all detected objects | "I see: person, chair, bottle, laptop" |
| **"Stop navigation"** | Exit the system | System shuts down |

### Supported Objects (80 COCO Classes)

```
person, bicycle, car, motorcycle, airplane, bus, train, truck, boat,
traffic light, fire hydrant, stop sign, parking meter, bench, bird,
cat, dog, horse, sheep, cow, elephant, bear, zebra, giraffe, backpack,
umbrella, handbag, tie, suitcase, frisbee, skis, snowboard, sports ball,
kite, baseball bat, baseball glove, skateboard, surfboard, tennis racket,
bottle, wine glass, cup, fork, knife, spoon, bowl, banana, apple,
sandwich, orange, broccoli, carrot, hot dog, pizza, donut, cake, chair,
couch, potted plant, bed, dining table, toilet, tv, laptop, mouse,
remote, keyboard, cell phone, microwave, oven, toaster, sink,
refrigerator, book, clock, vase, scissors, teddy bear, hair drier,
toothbrush
```

### Keyboard Controls

| Key | Action |
|-----|--------|
| **Q** | Quit the system |
| **ESC** | Emergency stop |

### Distance Zones

- **Close:** < 1.0 meter (red zone - immediate obstacle)
- **Medium:** 1.0 - 2.5 meters (yellow zone - approaching)
- **Far:** > 2.5 meters (green zone - safe distance)

---

## 🛠️ Troubleshooting

### Camera Issues

**Problem:** `Error: Cannot open camera`

**Solutions:**
1. Check if another application is using the camera
2. Try different camera index:
   ```python
   camera = cv2.VideoCapture(1)  # Try 0, 1, 2, etc.
   ```
3. Run camera diagnostic:
   ```powershell
   python diag_camera.py
   ```

### Microphone Issues

**Problem:** Voice commands not recognized

**Solutions:**
1. Verify microphone device index:
   ```powershell
   python test_microphone.py
   ```
2. Check Windows microphone permissions:
   - Settings → Privacy → Microphone → Allow desktop apps
3. Increase microphone volume in Windows Sound settings
4. Speak clearly, 1-2 feet from microphone
5. Reduce background noise

**Problem:** `OSError: [Errno -9997] Invalid sample rate`

**Solution:** Update `voice_input.py` sample rate:
```python
SAMPLE_RATE = 16000  # Try 44100 or 48000 if 16000 fails
```

### Performance Issues

**Problem:** Low FPS (< 10 FPS)

**Solutions:**
1. Close other running applications
2. Use smaller camera resolution:
   ```python
   cap.set(cv2.CAP_PROP_FRAME_WIDTH, 640)
   cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 480)
   ```
3. Disable visualization (edit navigation_main.py):
   ```python
   # Comment out cv2.imshow() line
   ```

**Problem:** High CPU usage

**Solutions:**
1. Use YOLOv8n (smaller model) instead of YOLOv10n
2. Reduce detection confidence threshold
3. Enable GPU acceleration (if NVIDIA GPU available):
   ```python
   model = YOLO("yolov8n.pt", device="cuda")
   ```

### Installation Issues

**Problem:** `pip install` fails for PyAudio

**Solutions:**
1. Install Visual C++ Redistributable (see Prerequisites)
2. Try pre-built wheel:
   ```powershell
   pip install pipwin
   pipwin install pyaudio
   ```

**Problem:** PyTorch installation takes too long

**Solution:** Use CPU-only version:
```powershell
pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu
```

### Voice Recognition Issues

**Problem:** "Partial match" or failed recognition

**Solutions:**
1. Speak commands exactly as listed (avoid variations)
2. Enunciate clearly, avoid slurring words
3. Adjust ambient noise adjustment:
   ```python
   recognizer.adjust_for_ambient_noise(source, duration=2)
   ```
4. Use push-to-talk mode instead of continuous listening

---

## 🏗️ System Architecture

### Core Components

```
┌─────────────────────────────────────────────────┐
│              AI Assistive System                │
├─────────────────────────────────────────────────┤
│                                                 │
│  ┌──────────────┐    ┌──────────────┐          │
│  │   Camera     │───▶│  YOLOv8n     │          │
│  │   Input      │    │  Detection   │          │
│  └──────────────┘    └──────────────┘          │
│                            │                    │
│                            ▼                    │
│                  ┌──────────────────┐           │
│                  │ Distance         │           │
│                  │ Estimation       │           │
│                  └──────────────────┘           │
│                            │                    │
│                            ▼                    │
│                  ┌──────────────────┐           │
│                  │ Spatial Memory   │◀────────┐ │
│                  │ (Object Storage) │         │ │
│                  └──────────────────┘         │ │
│                            │                  │ │
│                            ▼                  │ │
│  ┌──────────────┐    ┌──────────────┐        │ │
│  │  Microphone  │───▶│ Voice        │────────┘ │
│  │  Input       │    │ Recognition  │          │
│  └──────────────┘    └──────────────┘          │
│                            │                    │
│                            ▼                    │
│                  ┌──────────────────┐           │
│                  │ Navigation       │           │
│                  │ Guidance         │           │
│                  └──────────────────┘           │
│                            │                    │
│                            ▼                    │
│                  ┌──────────────────┐           │
│                  │ Text-to-Speech   │           │
│                  │ Output           │           │
│                  └──────────────────┘           │
│                                                 │
└─────────────────────────────────────────────────┘
```

### File Structure

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
│   ├── target_guidance.py         # Direction guidance
│   ├── obstacle_guidance.py       # Obstacle avoidance
│   ├── distance_estimator.py      # Distance calculation
│   └── ...
│
├── voice/                          # Voice interaction
│   ├── voice_input.py             # Microphone input
│   ├── voice_manager.py           # TTS output
│   └── ...
│
├── known_faces/                    # Face recognition data (optional)
│   ├── person1/
│   ├── person2/
│   └── ...
│
├── yolov8n.pt                      # YOLO model weights
├── yolov10n.pt                     # Alternative model
│
└── [test files]                    # Diagnostic scripts
```

### Processing Pipeline

```
1. Frame Capture (2-3ms)
         ↓
2. Pre-processing (1-2ms)
         ↓
3. YOLO Detection (71.96ms)
         ↓
4. Post-processing/NMS (2-3ms)
         ↓
5. Distance Estimation (1-2ms)
         ↓
6. Spatial Memory Update (0.5ms)
         ↓
7. Voice Command Processing (async)
         ↓
8. Navigation Guidance (async)
         ↓
9. Display Output (1-2ms)

Total: ~80ms per frame = 12.40 FPS
```

---

## 📊 Performance Metrics

### System Performance (AMD Ryzen 5 5625U)

| Metric | Value |
|--------|-------|
| Inference Latency | 71.96 ms |
| System FPS | 12.40 FPS |
| RAM Usage | 374.79 MB |
| CPU Usage | 429% (multi-core) |
| Detection Classes | 80 (COCO) |
| Spatial Memory Accuracy | 100% |
| Voice Recognition Rate | 90.48% |

---

## 📱 Testing Components Individually

### Test Camera Only
```powershell
python camera_test.py
```

### Test YOLO Detection Only
```powershell
python yolo_test.py
```

### Test Distance Estimation
```powershell
python distance_estimator_test.py
```

### Test Voice Recognition Only
```powershell
python voice_command_test.py
```

### Test Text-to-Speech Only
```powershell
python pyttsx3_test.py
```

### Test Spatial Memory
```powershell
python navigation/object_memory.py
```

---

## 🔄 Updating the System

### Update Python Packages
```powershell
pip install --upgrade -r requirements.txt
```

### Update YOLO Model
```powershell
# Download latest YOLOv8n
Invoke-WebRequest -Uri "https://github.com/ultralytics/assets/releases/download/v0.0.0/yolov8n.pt" -OutFile "yolov8n.pt"
```

### Update from Git Repository
```powershell
git pull origin main
pip install -r requirements.txt
```

---

## 🆘 Support and Documentation

### Additional Documentation
- `SPATIAL_MEMORY_DOCUMENTATION.md` - Spatial memory system details
- `FPS_METRICS_FORMULAS.md` - Performance calculation formulas
- `ACTUAL_METRICS_EVALUATED.md` - Evaluation results
- `OBJECT_STORAGE_EXPLAINED.md` - Object storage architecture

### Common Questions

**Q: Can I use a different YOLO model?**
A: Yes, modify the model path in navigation_main.py:
```python
model = YOLO("yolov8s.pt")  # or yolov8m.pt, yolov8l.pt
```

**Q: How do I add new voice commands?**
A: Edit `voice/voice_manager.py` and add command patterns to the recognition logic.

**Q: Can I use multiple cameras?**
A: Yes, modify the camera index in navigation_main.py:
```python
camera = cv2.VideoCapture(1)  # Use camera 1 instead of 0
```

**Q: Does this work with DroidCam (phone as webcam)?**
A: Yes! Use `camera_droidcam_test.py` to test connectivity first.

---

## 🎓 For Research and Development

### Citing This Work
If you use this system in your research, please cite:
```
AI Assistive System for Visually Impaired Navigation
Using YOLOv8 Object Detection and Spatial Memory
[Your Institution, Year]
```

### Contributing
Contributions are welcome! Please follow these guidelines:
1. Fork the repository
2. Create a feature branch
3. Test thoroughly
4. Submit a pull request

---

## ⚖️ License and Disclaimer

**Educational Use:** This system is designed for research and educational purposes.

**Safety Warning:** This system is a prototype and should NOT be used as the sole navigation aid. Always use with:
- A human guide or companion
- Traditional assistive tools (cane, guide dog)
- Proper training and familiarization

**Limitations:**
- Detection accuracy depends on lighting conditions
- Voice recognition may fail in noisy environments
- Distance estimation has ~10-20% margin of error
- System cannot detect all hazards (steps, low obstacles, etc.)

---

## 📧 Contact

For issues, questions, or suggestions:
- GitHub Issues: [Your Repository URL]
- Email: [Your Email]

---

## ✅ Installation Checklist

Print this checklist and mark off each step:

- [ ] Python 3.12 installed and in PATH
- [ ] Visual C++ Redistributable installed
- [ ] Repository cloned or downloaded
- [ ] Virtual environment created
- [ ] Requirements.txt packages installed
- [ ] YOLO model weights present (yolov8n.pt)
- [ ] Camera tested (camera_test.py works)
- [ ] Microphone device index identified
- [ ] Voice recognition tested (voice_command_test.py works)
- [ ] Main system runs (navigation_main.py starts successfully)
- [ ] Voice commands recognized and responded to
- [ ] All test scripts pass

**If all items are checked, your system is ready to use! 🎉**

---

**Last Updated:** November 2026  
**Version:** 1.0  
**System:** AI Assistive Navigation System for Visually Impaired Users
