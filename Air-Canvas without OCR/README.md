# Air Canvas

## Introduction
This project is an **Air Canvas**, which allows users to draw in the air using hand gestures captured by a webcam. It utilizes **OpenCV, MediaPipe, and NumPy** to track hand movements and translate them into digital drawings on a virtual canvas.

## Objective
By running this project, users will:

1. Use a webcam to track hand gestures in real-time.
2. Draw in different colors using simple finger movements.
3. Switch between colors and clear the canvas using predefined gesture-based controls.

## Features
- **Hand Tracking:** Detects hand landmarks and movements using **MediaPipe Hands**.
- **Gesture-Based Drawing:** Draw by moving the index finger in the air.
- **Color Selection:** Choose between **Blue, Green, Red, and Yellow**.
- **Clear Canvas:** A designated button to clear the drawing.
- **Real-Time Processing:** Uses OpenCV to process frames efficiently.

## Dependencies
Ensure you have the following libraries installed before running the project:

```bash
pip install opencv-python mediapipe numpy
```

## How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/Air-Canvas.git
   ```
2. Navigate to the project directory:
   ```bash
   cd Air-Canvas
   ```
3. Run the Python script:
   ```bash
   python air_canvas.py
   ```
4. The webcam will activate, and you can start drawing in the air using hand gestures.

## Usage Instructions
1. **Start Drawing:** Move your index finger while keeping other fingers closed.
2. **Switch Colors:**
   - Blue: Move hand over the **blue box** at the top.
   - Green: Move hand over the **green box** at the top.
   - Red: Move hand over the **red box** at the top.
   - Yellow: Move hand over the **yellow box** at the top.
3. **Clear the Canvas:** Move your hand over the "CLEAR" box.
4. **Exit:** Press `q` to close the application.

## File Structure
- **air_canvas.py**: Main script to run the Air Canvas application.
- **README.md**: Instructions to set up and run the project.

## Future Enhancements
- **Integrate OCR** to recognize and convert handwritten text.
- **Add more gestures** to enhance functionality.
- **Support saving drawings** as images.

## Author
This project was developed by **Muhammad Irtaza Ali** as part of an exploration into OpenCV and hand-tracking technologies.

