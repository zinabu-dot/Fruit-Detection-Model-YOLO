# Fruit Detection with YOLOv11

Real-time fruit detection system using YOLOv11 for identifying and counting fruits in images, videos, and live camera feeds.

## Overview

This project uses a trained YOLOv11s model to detect fruits in real-time. The model was trained for 60 epochs with a batch size of 16 at 640x640 resolution.

## Requirements

```bash
pip install ultralytics opencv-python numpy
```

## Quick Start

### 1. Detect on Image

```bash
python yolo_detect.py --model my_model/my_model.pt --source path/to/image.jpg
```

### 2. Detect on Video

```bash
python yolo_detect.py --model my_model/my_model.pt --source path/to/video.mp4
```

### 3. Detect with Webcam (Real-time)

```bash
python yolo_detect.py --model my_model/my_model.pt --source usb0
```

For second camera, use `usb1`, etc.

### 4. Detect on Folder of Images

```bash
python yolo_detect.py --model my_model/my_model.pt --source path/to/folder
```

## Advanced Options

### Set Confidence Threshold

```bash
python yolo_detect.py --model my_model/my_model.pt --source usb0 --thresh 0.6
```

Default threshold is 0.5 (50% confidence).

### Set Display Resolution

```bash
python yolo_detect.py --model my_model/my_model.pt --source usb0 --resolution 1280x720
```

### Record Video Output

```bash
python yolo_detect.py --model my_model/my_model.pt --source usb0 --resolution 640x480 --record
```

Output saved as `demo1.avi`. Resolution must be specified when recording.

## Keyboard Controls

- **Q**: Quit the program
- **S**: Pause inference (press any key to resume)
- **P**: Save current frame as `capture.png`

## Model Information

- **Architecture**: YOLOv11s
- **Training Epochs**: 60
- **Image Size**: 640x640
- **Batch Size**: 16
- **IoU Threshold**: 0.7
- **Model Location**: `my_model/my_model.pt`

## Training Results

Training metrics and visualizations are available in `my_model/train/`:
- `results.png` - Training/validation metrics over time
- `confusion_matrix.png` - Model confusion matrix
- `BoxPR_curve.png` - Precision-Recall curve
- `results.csv` - Detailed metrics per epoch

## Python API Usage

```python
from ultralytics import YOLO
import cv2

# Load model
model = YOLO('my_model/my_model.pt')

# Run inference
results = model('image.jpg')

# Process results
for result in results:
    boxes = result.boxes
    for box in boxes:
        x1, y1, x2, y2 = box.xyxy[0].cpu().numpy()
        conf = box.conf[0].item()
        cls = int(box.cls[0].item())
        print(f"Class: {cls}, Confidence: {conf:.2f}")
```

## Supported Formats

**Images**: `.jpg`, `.jpeg`, `.png`, `.bmp`  
**Videos**: `.avi`, `.mov`, `.mp4`, `.mkv`, `.wmv`

## Troubleshooting

**Camera not working**: Try different USB indices (`usb0`, `usb1`, `usb2`)  
**Low FPS**: Reduce resolution with `--resolution 640x480`  
**No detections**: Lower threshold with `--thresh 0.3`

## Project Structure

```
Fruit Detection/
├── my_model/
│   ├── my_model.pt              # Trained model weights
│   └── train/                   # Training results & metrics
├── yolo_detect.py               # Main detection script
├── 01_training_YOLOv11_Models.ipynb  # Training notebook
└── README.md
```

## License

This project uses Ultralytics YOLOv11 under AGPL-3.0 license.
