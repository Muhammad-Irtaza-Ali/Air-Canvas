# **Understanding OpenCV & Mediapipe for Air Canvas**  

## **1. OpenCV Basics**
**OpenCV (Open Source Computer Vision Library)** is an open-source computer vision and image processing library. It provides functionalities for real-time image/video processing.

### **Key Functions Used**
- `cv2.VideoCapture(0)`: Captures video from the default camera (webcam).  
- `cv2.flip(frame, 1)`: Flips the video frame horizontally (mirror effect).  
- `cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)`: Converts BGR image to RGB, required for **Mediapipe**.  
- `cv2.rectangle()`: Draws a rectangle on an image. Used to create the color palette.  
- `cv2.putText()`: Adds text to an image. Used for labeling buttons like "CLEAR", "BLUE", etc.  
- `cv2.line()`: Draws a line on an image. Used to track the drawing movements.  
- `cv2.imshow()`: Displays the processed video feed.  

---

## **2. Mediapipe Hand Tracking**
**Mediapipe** is a framework by Google that provides real-time hand tracking using deep learning models.

### **Key Steps in Hand Tracking**
1. **Initialize Mediapipe Hands**  
   ```python
   mpHands = mp.solutions.hands
   hands = mpHands.Hands(max_num_hands=1, min_detection_confidence=0.7)
   mpDraw = mp.solutions.drawing_utils
   ```
   - `max_num_hands=1`: Detects only one hand.  
   - `min_detection_confidence=0.7`: Minimum confidence level for hand detection.  

2. **Processing Each Frame for Hand Detection**  
   ```python
   result = hands.process(framergb)
   ```
   - Converts the frame to **RGB** before passing it to Mediapipe.  
   - `result.multi_hand_landmarks` stores detected hand landmarks.

3. **Extracting Finger Position**
   ```python
   for handslms in result.multi_hand_landmarks:
       for lm in handslms.landmark:
           lmx = int(lm.x * 640)
           lmy = int(lm.y * 480)
   ```
   - Hand landmarks return **normalized coordinates (0 to 1)**, which are converted into pixel coordinates.

---

## **3. Gesture-Based Drawing**
Your code uses the **index finger and thumb** to detect gestures for drawing.  

### **Finger Detection**
- **Forefinger (Index Finger)** → Used for drawing.  
- **Thumb** → Used to detect clicking (lifted or not).  

```python
fore_finger = (landmarks[8][0], landmarks[8][1])  # Index Finger
thumb = (landmarks[4][0], landmarks[4][1])        # Thumb

if (thumb[1] - fore_finger[1] < 30):
    # Detected a click
```
- When the **thumb is close to the index finger**, the code starts a new stroke.  
- Otherwise, the **index finger tracks drawing movements**.

---

## **4. Color Selection & Clear Button**
- **Touching the button at the top selects a color or clears the board**.  
- The **coordinates of the finger** determine the selected action:
  ```python
  elif center[1] <= 65:
      if 40 <= center[0] <= 140:  # Clear
          bpoints = [deque(maxlen=512)]
          gpoints = [deque(maxlen=512)]
          rpoints = [deque(maxlen=512)]
          ypoints = [deque(maxlen=512)]
  ```
  - The **Clear button** erases all drawings by resetting all deque structures.
  - The **Color buttons** set `colorIndex` to match the selected color.

---

## **5. Drawing Using Deques**
- A **deque (double-ended queue)** is used to store points for each color separately.
- When the **index finger moves**, the new point is stored in the deque:
  ```python
  if colorIndex == 0:
      bpoints[blue_index].appendleft(center)
  elif colorIndex == 1:
      gpoints[green_index].appendleft(center)
  elif colorIndex == 2:
      rpoints[red_index].appendleft(center)
  elif colorIndex == 3:
      ypoints[yellow_index].appendleft(center)
  ```
- This allows **continuous drawing** without breaking strokes.

---

## **6. Displaying Final Output**
- The **frame with hand tracking** is displayed using:
  ```python
  cv2.imshow("Output", frame)
  ```
- The **drawing canvas is displayed separately**:
  ```python
  cv2.imshow("Paint", paintWindow)
  ```

---

# **Conclusion**
**Air Canvas** works by:
1. Capturing **webcam input** using OpenCV.  
2. Using **Mediapipe Hand Tracking** to detect index finger position.  
3. Storing drawing points in **deques** to maintain strokes.  
4. Detecting **gestures for color selection and clearing the board**.  
5. Drawing on a **canvas** using OpenCV functions like `cv2.line()`.  
