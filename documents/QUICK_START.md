# ⚡ Quick Start Guide - AI Assistive System

**Get running in 5 minutes!**

---

## 🚀 Installation (One-Time Setup)

### Step 1: Install Python 3.12
Download from: https://www.python.org/downloads/
- ✅ Check "Add Python to PATH"

### Step 2: Install Software
```powershell
# Open PowerShell in project folder
cd AI-Assistive-System

# Install packages (takes 5-10 min)
pip install -r requirements.txt
```

### Step 3: Find Your Microphone
```powershell
python test_microphone.py
```
**Write down your device number!** (e.g., 12)

---

## ▶️ Running the System

### Start Navigation
```powershell
python navigation_main.py
```

**If microphone doesn't work:**
1. Open `navigation_main.py` in Notepad
2. Find line ~285: `voice_input = VoiceInput(device_index=12)`
3. Change `12` to your device number
4. Save and run again

---

## 🎤 Voice Commands

Speak clearly into your microphone:

| Say This | System Does |
|----------|-------------|
| **"Find the bottle"** | Locates and guides you to bottle |
| **"Where is the chair"** | Recalls where chair was last seen |
| **"What do you see"** | Lists all detected objects |
| **"Stop navigation"** | Exits the system |

### Examples:
- "Find the person"
- "Where is the laptop"
- "Find the door"
- "Where is the cup"

---

## ⌨️ Keyboard Controls

- Press **Q** → Quit the system
- Press **ESC** → Emergency stop

---

## 🎯 Supported Objects

**Common objects the system can detect:**

```
✅ People & Animals: person, dog, cat, bird
✅ Furniture: chair, couch, bed, table, toilet
✅ Electronics: laptop, tv, cell phone, keyboard, mouse
✅ Kitchen: bottle, cup, bowl, fork, knife, spoon, microwave, oven
✅ Personal: backpack, handbag, umbrella, book, clock
✅ Transport: car, bicycle, motorcycle, bus, train
✅ And 50+ more objects...
```

---

## 🖥️ What You'll See

### Display Window Shows:
- 🟢 Green boxes around detected objects
- 📏 Distance in meters (e.g., "1.5m")
- ⬅️ Direction indicators (LEFT/CENTER/RIGHT)
- 📊 FPS counter (should be 10-15 FPS)

### Voice Outputs Example:
```
You: "Find the bottle"
System: "Bottle is on your left, approximately 1.5 meters away"

You: "Where is the chair"
System: "Chair was last seen ahead, 2 meters away"

You: "What do you see"
System: "I see: person, chair, bottle, laptop, and cell phone"
```

---

## ❌ Troubleshooting

### Problem: Camera doesn't start

**Solution:**
```powershell
# Test your camera
python camera_test.py
```
If fails, check:
- Is camera connected?
- Is another app using it? (close Zoom, Skype, etc.)
- Try restarting your computer

---

### Problem: Voice commands not recognized

**Solutions:**
1. **Check microphone permissions:**
   - Windows Settings → Privacy → Microphone → Allow desktop apps

2. **Verify device index:**
   ```powershell
   python test_microphone.py
   ```
   Update the number in `navigation_main.py`

3. **Test voice recognition:**
   ```powershell
   python voice_command_test.py
   ```
   Speak: "Find the bottle"

4. **Improve recognition:**
   - Speak clearly and slowly
   - Reduce background noise
   - Move closer to microphone (1-2 feet)
   - Increase microphone volume in Windows Sound settings

---

### Problem: System is slow (< 10 FPS)

**Solutions:**
1. Close other programs (Chrome, games, etc.)
2. Use smaller camera:
   - Edit `navigation_main.py`
   - Set camera resolution to 640×480

---

### Problem: "pip install" fails

**Solution:**
```powershell
# Install Visual C++ first
# Download: https://aka.ms/vs/17/release/vc_redist.x64.exe
# Run installer, then try again:
pip install -r requirements.txt
```

---

## 🧪 Test Individual Components

Before running full system, test each part:

```powershell
# Test 1: Camera
python camera_test.py
# Should show camera feed. Press 'q' to quit.

# Test 2: Microphone
python test_microphone.py
# Should list all microphones. Note your device number.

# Test 3: Voice recognition
python voice_command_test.py
# Speak "Find the bottle". Should print recognized text.

# Test 4: Object detection
python yolo_test.py
# Should detect objects in camera view.

# Test 5: Distance estimation
python distance_estimator_test.py
# Should show objects with distance labels.
```

If all 5 tests pass → Full system will work! ✅

---

## 📋 Pre-Flight Checklist

Before using the system:

- [ ] Python 3.12 installed
- [ ] All packages installed (`pip install -r requirements.txt`)
- [ ] Camera works (`camera_test.py` passes)
- [ ] Microphone device number found
- [ ] Voice recognition works (`voice_command_test.py` passes)
- [ ] `yolov8n.pt` file exists in project folder
- [ ] Windows microphone permissions enabled

✅ **All checked? You're ready to run!**

```powershell
python navigation_main.py
```

---

## 🆘 Get Help

### Documentation Files:
- 📘 **INSTALLATION_GUIDE.md** - Complete setup (read this if stuck!)
- 📗 **README.md** - Project overview
- 📙 **SPATIAL_MEMORY_DOCUMENTATION.md** - How memory works

### Common Errors:

**Error:** `ModuleNotFoundError: No module named 'cv2'`
```powershell
pip install opencv-python
```

**Error:** `ModuleNotFoundError: No module named 'ultralytics'`
```powershell
pip install ultralytics
```

**Error:** `Cannot open camera`
```powershell
# Try different camera
python diag_camera.py
```

**Error:** `OSError: No Default Input Device Available`
```powershell
# Check microphone connection
python test_microphone.py
```

---

## 💡 Tips for Best Performance

### For Camera:
- Use good lighting (natural light is best)
- Point camera at chest/waist height
- Keep camera lens clean
- Avoid backlighting (don't face windows)

### For Voice Recognition:
- Speak clearly (don't whisper or shout)
- Use exact command phrases
- Wait for response before next command
- Use in quiet environment

### For Distance Accuracy:
- Objects 1-5 meters work best
- Larger objects (chairs, tables) more accurate
- Small objects (cups, phones) less accurate at distance

---

## 🎮 Usage Flow

```
1. Run: python navigation_main.py
         ↓
2. Camera window opens
         ↓
3. System detects objects in view
         ↓
4. Speak voice command: "Find the bottle"
         ↓
5. System responds: "Bottle is on your left, 1.5 meters"
         ↓
6. Turn left and walk toward bottle
         ↓
7. System updates as you move
         ↓
8. Press 'Q' to quit when done
```

---

## 🌟 First Time Usage Tips

1. **Start in a familiar room** with known objects
2. **Test with large objects first** (chair, table, couch)
3. **Practice voice commands** before moving around
4. **Keep hands free** (wear headphones for audio feedback)
5. **Have someone assist** on first few tries
6. **Don't rely solely on the system** - use with traditional aids

---

## ⚠️ Safety Reminders

**DO:**
- ✅ Use in well-lit indoor spaces
- ✅ Have a companion nearby
- ✅ Use with traditional mobility aids
- ✅ Practice in safe environment first

**DON'T:**
- ❌ Use as sole navigation aid
- ❌ Use near stairs or ledges
- ❌ Use in complete darkness
- ❌ Rely on it in unfamiliar environments

---

## 📞 Still Need Help?

1. **Read full guide:** `INSTALLATION_GUIDE.md`
2. **Check GitHub Issues:** [Report problems]
3. **Email:** your.email@example.com

---

## ✅ Success!

If you see this:
```
[INFO] Model loaded successfully
[INFO] Camera initialized
[INFO] Voice input ready on device 12
[INFO] System ready. Press 'q' to quit.
```

**You're all set! Start speaking commands!** 🎉

---

**Quick Reference Card - Keep This Handy!**

| Command | Action |
|---------|--------|
| `python navigation_main.py` | Start system |
| "Find the [object]" | Search for object |
| "Where is [object]" | Recall object location |
| "What do you see" | List detected objects |
| Press Q | Quit |

---

*Last Updated: November 2026*
