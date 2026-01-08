# Hand Gesture Recognition

This Python script utilizes **OpenCV** and **MediaPipe** to detect a human hand, recognize various hand gestures, and display the detected gesture in real-time using a webcam feed.

## ✨ Features

* **Real-time Hand Detection:** Uses MediaPipe to accurately track a single hand's landmarks.
* **Gesture Recognition:** Identifies several common hand gestures.
* **Visual Feedback:** Draws hand landmarks, a bounding box around the hand, and displays the recognized gesture with a transparent background box on the video feed.
* **Webcam Initialization:** Includes robust code for attempting to open the webcam and logging its properties.

## 🚀 Recognized Gestures

The script currently recognizes the following hand gestures:

| Gesture | Description | Finger States (Thumb, Index, Middle, Ring, Pinky) |
| :--- | :--- | :--- |
| **Hi** | Open Hand (Palm facing camera) | `[1, 1, 1, 1, 1]` |
| **Thumbs Up** | Thumb up, hand not tilted down | `[1, 0, 0, 0, 0]` |
| **Thumbs Down** | Thumb up, hand tilted downwards | `[1, 0, 0, 0, 0]` (with tilt check) |
| **Live Long** | Thumb, Index, and Middle fingers up (often associated with Vulcan salute) | `[1, 1, 1, 0, 0]` |
| **Victory** | Index and Middle fingers up (V-sign) | `[0, 1, 1, 0, 0]` |
| **Peace** | Ring and Pinky fingers up | `[0, 0, 0, 1, 1]` |
| **Point Up** | Index finger up | `[0, 1, 0, 0, 0]` |
| **Fist** | All fingers down | `[0, 0, 0, 0, 0]` |



## 🛠️ Prerequisites

You need **Python 3.x** installed on your system.

## 📦 Installation

1.  **Clone the repository (or save the code):**
    ```bash
    # If you save the code in a file named gesture_recognizer.py
    ```

2.  **Install the necessary Python libraries:**
    ```bash
    pip install opencv-python mediapipe pyautogui
    ```
    * `opencv-python`: For video capture and display.
    * `mediapipe`: For hand tracking and landmark detection.
    * `pyautogui`: (Currently imported but unused in the provided code, though often used in related projects for system control).

## 🏃 Usage

1.  Ensure your webcam is connected and working.
2.  Run the script from your terminal:
    ```bash
    python gesture_recognizer.py
    ```
    (Replace `gesture_recognizer.py` with the name you saved the file as).

3.  A window titled **"Hand Gesture Detection"** will open, showing your webcam feed.
4.  Perform the gestures in front of the camera to see the real-time recognition.
5.  Press the **ESC** key to exit the application.

### Important Notes for Windows Users

The script uses `cv2.VideoCapture(0, cv2.CAP_DSHOW)` for Windows compatibility. If you encounter issues on a different OS (like macOS or Linux), you might need to remove the `cv2.CAP_DSHOW` argument or use a different camera index (e.g., `1` or `2`).

## ⚙️ Code Structure

* `mp_hands.Hands(...)`: Initializes the MediaPipe hand detection model.
* `tip_ids`: A list of landmark indices corresponding to the tips of the fingers (`[4, 8, 12, 16, 20]`).
* `get_finger_states(hand_landmarks)`: Determines if each finger is up (`1`) or down (`0`) based on the relative positions of the tip and the base joint.
* `is_thumbs_down(hand_landmarks)`: Calculates the angle of the thumb relative to the wrist to distinguish between **Thumbs Up** and **Thumbs Down** when the thumb is extended.
* `detect_gesture(fingers, hand_landmarks, w, h)`: Contains the logic to map the `finger` states to the specific gesture names.
* **Main Loop:** Continuously captures frames, processes them with MediaPipe, draws the landmarks, detects the gesture, and displays the result.

## 💡 Customization & Extension

* **Add New Gestures:** You can easily extend the `detect_gesture` function by defining new logic based on combinations of the `fingers` list (`[Thumb, Index, Middle, Ring, Pinky]`) or by analyzing specific landmark coordinates/angles.
* **Integrate Actions:** The `pyautogui` library is imported. You can add code inside the main loop to execute system actions (e.g., press a key, scroll, move the mouse) when a specific gesture is detected (e.g., use "Thumbs Up" to press the spacebar).
* **Performance:** Adjust the `min_detection_confidence` (default is 0.7) when initializing `mp_hands.Hands` to tune the balance between detection accuracy and speed.

---

## 📄 License

This project is open-source and available under [Specify your license, e.g., the MIT License].
