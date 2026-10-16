# YOLOv8 Vehicle Counting 🚗💨

> **Đồ án Sinh viên Khoa Công nghệ Thông tin**  
> **Hệ thống đếm phương tiện giao thông trong video**

This project uses YOLOv8 to detect vehicles in video and count them automatically. It can be used as a learning project for computer vision, object detection, and traffic monitoring applications.

## Overview

The system detects vehicles from video frames using YOLOv8, then applies counting logic to track the number of vehicles passing a defined line or area. The project is designed to be easy to understand, configure, and extend for academic and research purposes.

## Features

- Vehicle detection using YOLOv8
- Real-time or offline video processing
- Counting vehicles crossing a detection line
- Easy-to-adjust configuration for different scenes
- Output video with annotated detections
- Suitable for student projects and experimentation

## Tech Stack

- Python
- YOLOv8 (Ultralytics)
- OpenCV
- NumPy
- Optional: tracking and data export libraries

## Repository Structure

```text
.
├── README.md
├── requirements.txt
├── data/
│   ├── videos/
│   └── labels/
├── src/
│   ├── detect.py
│   ├── count.py
│   ├── config.py
│   └── utils.py
├── weights/
│   └── best.pt
├── runs/
│   └── detect/
└── output/
    └── result.mp4
```

## Requirements

- Python 3.8+
- pip
- A GPU is optional but recommended for faster inference

Install dependencies:

```bash
pip install -r requirements.txt
```

If needed, install YOLOv8 manually:

```bash
pip install ultralytics opencv-python numpy
```

## Installation

1. Clone the project:

```bash
git clone https://github.com/pvb-05/yolov8-vehicle-counting.git
cd yolov8-vehicle-counting
```

2. Create a virtual environment (optional but recommended):

```bash
python -m venv venv
source venv/bin/activate   # Linux/macOS
# or
venv\Scripts\activate      # Windows
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

## Usage

Run the detection and counting pipeline on a video file:

```bash
python src/count.py --source data/videos/input.mp4 --weights weights/best.pt --conf 0.25
```

Example arguments:

- `--source`: path to input video
- `--weights`: YOLOv8 model weights
- `--conf`: confidence threshold
- `--output`: output directory or output video path

The script will:

- load the YOLOv8 model
- detect vehicles in each frame
- count vehicles crossing the designated line
- save the result video and metrics

## Dataset

Prepare a dataset with labeled vehicle images or videos. The labels should match the classes you want the model to detect, such as:

- car
- truck
- bus
- motorcycle
- bicycle

If you are using training data, organize it in YOLO format and provide a dataset configuration file.

## Training

Train a YOLOv8 model on your custom dataset:

```bash
yolo task=detect mode=train model=yolov8n.pt data=data/custom_data.yaml epochs=50 imgsz=640
```

You can customize:

- number of epochs
- image size
- batch size
- classes used for detection

## Evaluation

After training, evaluate the model quality:

```bash
yolo task=detect mode=val model=weights/best.pt data=data/custom_data.yaml
```

This helps measure detection accuracy and determine whether the model is suitable for counting tasks.

## Output

The system can generate:

- annotated output video
- vehicle count totals
- logs or statistics for each processed video

## Project Goals

This repository can serve as:

- a student final-year project
- a computer vision demo
- a starting point for intelligent traffic monitoring systems
- a foundation for expanding to multi-camera counting or traffic analytics

## Contributing

Contributions are welcome. If you want to improve the project:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Open a pull request

## License

This project is licensed under the MIT License unless otherwise stated.

## Contact

For questions or collaboration, please contact the project author or open an issue in the GitHub repository.

---

This README is a general template for the project. If you want, I can further refine it into a more professional Vietnamese version or make it match the exact structure of your actual repo files.
