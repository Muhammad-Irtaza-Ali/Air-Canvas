# Air Canvas with OCR

This project implements an **Air Canvas** using **OpenCV** and **Mediapipe**, allowing users to draw in the air using hand gestures. Additionally, it integrates **OCR (Optical Character Recognition)** using **Tesseract** to recognize handwritten text from the canvas.

## Features

- **Hand Tracking**: Uses **Mediapipe Hands** to detect and track finger movements.
- **Air Drawing**: Allows users to draw using different colors (Blue, Green, Red, Yellow) by selecting them through on-screen buttons.
- **Undo Functionality**: Users can undo their last drawn action.
- **Clear Canvas**: A button to clear the entire drawing area.
- **OCR Text Recognition**: Converts handwritten content into digital text using **Tesseract OCR**.
- **Keyboard Shortcuts**:
  - Press `q` to exit the program.
  - Press `d` to toggle OCR detection.
  - Press `z` to undo the last action.

## Technologies Used

- **Python**
- **OpenCV** (Computer Vision Library)
- **Mediapipe** (Hand Tracking)
- **Numpy** (For array operations)
- **Deque** (For efficient point storage)
- **Tesseract OCR** (Text Recognition)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/AirCanvas-OCR.git
   cd AirCanvas-OCR
   ```

2. Install dependencies:
   ```bash
   pip install opencv-python numpy mediapipe pytesseract
   ```

3. Ensure Tesseract OCR is installed:
   - Download and install from: [Tesseract OCR](https://github.com/tesseract-ocr/tesseract)
   - Set the path in the script:
     ```python
     pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
     ```

## Usage

1. Run the program:
   ```bash
   python air_canvas.py
   ```

2. Use hand gestures to draw:
   - Move your **index finger** to draw.
   - Move your **thumb and index finger together** to change color.
   - Hover over the top buttons to change colors or clear the canvas.
   
3. Enable OCR detection:
   - Press `d` to toggle OCR and extract text from the drawing area.
   
## Code Overview

### 1. **Hand Tracking & Drawing**
- **Mediapipe Hands** detects hand landmarks.
- Tracks the index finger to draw based on its movement.
- Allows users to change colors by selecting buttons on the screen.

### 2. **OCR Processing**
- Captures the **Region of Interest (ROI)** where the drawing happens.
- Applies **grayscale conversion, thresholding, dilation, and erosion** for better OCR recognition.
- Uses **Tesseract OCR** to extract and display handwritten text.

## Example Output

After drawing, enabling OCR will recognize and print the detected text:
```
Detected Text: Hello World
```

## Future Enhancements
- Implementing **word smoothing techniques** for better recognition.
- Adding **gesture-based eraser** for smoother experience.
- Supporting **multilingual OCR** for broader usability.

## Author
This project was developed by **Muhammad Irtaza Ali** to explore real-time hand tracking, computer vision, and OCR applications.

