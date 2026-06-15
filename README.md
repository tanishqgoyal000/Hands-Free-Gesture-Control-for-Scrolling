👁️ GazeScroll — Hands-Free Gesture Control for Scrolling

A computer vision project that lets you scroll through content (e.g., Instagram Reels, any feed) without touching your device — using simple, intentional eye gestures detected via your webcam.

Built as an exploration of gesture-based hands-free interaction for short-form video consumption, inspired by accessibility eye-tracking features (like iOS's eye-tracking accessibility mode and Samsung's earlier eye-scroll experiments).


✨ Features


🎥 Real-time face & eye tracking using MediaPipe FaceLandmarker
👀 Double blink → scroll up
😳 Eye widen (both eyes) → scroll down
🎯 Per-user calibration — adapts to your natural eye openness baseline
⚡ Lightweight, runs entirely on-device via webcam (no cloud, no data leaves your machine)



🧠 How It Works


Face landmark detection — MediaPipe's FaceLandmarker model extracts 478 facial landmarks per frame from the webcam feed
Eye Aspect Ratio (EAR) — computed per eye as the ratio of vertical eye-opening to horizontal eye-width; a standard metric for eye-closure detection
Calibration — captures a few seconds of your relaxed, eyes-open EAR as a personal baseline
Gesture state machine:

If EAR drops below a threshold and recovers twice within a short time window → double blink detected
If EAR rises and stays above a threshold for a few frames → eye widen detected



Action trigger — maps detected gestures to scroll actions via pyautogui



🛠️ Tech Stack


Python 3.10+
MediaPipe (FaceLandmarker, Tasks API)
OpenCV (webcam capture & visualization)
PyAutoGUI (simulated scroll/keypress actions)
NumPy



🚀 Setup & Usage

bash# Install dependencies
pip install mediapipe opencv-python pyautogui numpy --break-system-packages

# Download the face landmarker model (one-time, ~5MB)
curl -L -o face_landmarker.task \
  "https://storage.googleapis.com/mediapipe-models/face_landmarker/face_landmarker/float16/1/face_landmarker.task"

# Run
python3 blink_widen_scroll.py

Controls:


Press c to calibrate — sit normally with both eyes open for ~2 seconds
Double blink → scroll up
Widen both eyes → scroll down
Press q to quit


macOS users: grant Camera and Accessibility permissions to your terminal/IDE under System Settings → Privacy & Security.


📌 Limitations & Future Work


Sensitive to lighting conditions and camera quality
Requires per-session calibration (baseline EAR varies by person, lighting, and camera angle)
Currently controls the active window via simulated keypresses/scroll — a browser extension version (via WebSocket bridge or MediaPipe's JS/WASM build) would allow more precise, page-level scroll control
Could be extended with additional gestures (e.g., head tilt, nod) for more app controls



💡 Motivation

This started as a simple question: what if you could scroll through Reels while eating, without touching your phone? It turned into a hands-on exploration of real-time computer vision, facial landmark detection, signal thresholding, and gesture-based UX — and a genuinely useful accessibility-adjacent tool.
