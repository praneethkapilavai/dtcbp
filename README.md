# 💡 AI Classroom Engagement Monitor & Driver Drowsiness Detector

This repository contains two distinct AI computer vision scripts that run natively on OpenCV and dlib to monitor human engagement, drowsiness, and facial focus in real-time. 

## 1. Classroom Engagement Monitor (`classroom_engagement.py`)
This script acts as a real-time analytics engine to monitor the attention levels of multiple students/people in a room. 

**Key Features:**
* **Multi-Person Tracking:** Uses Centroid Tracking to lock onto multiple faces simultaneously, assigning dedicated IDs to each person (e.g., Seat 0, Seat 1).
* **Sleepiness Check (EAR):** Tracks the Euclidean distances of eyes. If a person falls asleep, a loud continuous background PC speaker alarm triggers instantly.
* **Dynamic Lip-Sync Detection:** Intelligently tracks inner-lip variance and overall mouth openness over a sliding frame-window. It can successfully distinguish between someone resting with their mouth open vs. someone actively whispering or talking.
* **Head Pose Estimation (Attention Focus):** Uses OpenCV's `solvePnP` to project a 3D geometric model onto 2D facial landmarks, determining exact 3D spatial orientation (Yaw, Pitch, Roll). It registers if someone looks left, right, down, or straight ahead with a 30-degree leeway.
* **CSV Auto-Reporting:** Generating a complete end-of-session analytical report (`classroom_report.csv`). It contains statistical percentage-based engagement scores, sleeping times, and talking metrics for every tracked seat ID.

## 2. Driver Drowsiness Detector (`face_eye_detection_for_drowsiness.py`)
A safety AI system that triggers an alert when a driver is feeling drowsy and saves visual proof.

**Key Features:**
* Evaluates real-time Eye Aspect Ratio (EAR) against a static geometric threshold.
* Triggers a visual Drowsiness Alert Overlay on the camera feed.
* Captures and saves raw camera screenshots directly to the `dataset` folder as timestamped evidence of falling asleep.

---

## ⚡️ How to Install and Run

1. Clone this repository to preserve the directory structure:<br>
   `git clone https://github.com/praneethkapilavai/dtcbp.git`
2. Open your Command Prompt/Terminal and navigate into the cloned directory.
3. Install all required mathematical and camera dependencies:<br>
   `pip install -r requirements.txt`
4. Run your chosen program:<br>
   - Run **`python classroom_engagement.py`** to track multiple people and generate engagement logs.<br>
   - Run **`python face_eye_detection_for_drowsiness.py`** for basic driver safety.<br>

*(Important: Press the **Esc** key while your camera window is selected to safely exit the loops and save your CSV data!)*

**Note**: If you want to simply visualize the generic 68-point structure on a human face without algorithms, run `face_landmark.py`! 😎

## 💡 Engine Mechanics

The entire logic flow natively relies on the **dlib 68-point facial landmark predictor**.
* **EAR Calculation:** Derived from the Euclidean distances across coordinate mappings `36` through `47`.
* **LAR Calculation:** Derived from the inner mouth heights vs overall horizontal mouth width over coordinate mappings `48` through `67`.
* **Dependencies Used:** Python 3, `opencv-python`, `dlib`, `scipy`, `pandas`, `winsound`

## 🙋‍♂️ Helpdesk
If you face any issues (like the video freezing or scripts failing to run locally), feel free to reach out via GitHub Issues or contact me directly! 

## ℹ References
The ideas presented in this repo were significantly inspired by:
* [dlib C++ library](https://github.com/davisking/dlib) by Davis King
* [Facial mapping landmarks](https://towardsdatascience.com/facial-mapping-landmarks-with-dlib-python-160abcf7d672) by Italo José
* The official [Dlib Website](http://dlib.net/) for the 68-point predictor dat model.
