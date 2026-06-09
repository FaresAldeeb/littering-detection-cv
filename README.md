# Littering Detection from Fixed-Camera Video

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Computer Vision](https://img.shields.io/badge/Computer%20Vision-YOLO-green)
![Deep Learning](https://img.shields.io/badge/Deep%20Learning-PyTorch-orange)
![Status](https://img.shields.io/badge/Status-Prototype-yellow)

A Computer Vision project that detects possible littering behavior in fixed-camera videos using **YOLO11m**, **ByteTrack**, and video-based event logic.

The system detects **people** and **trash objects**, then analyzes their relationship over time to decide whether a possible littering event happened.

---

## Demo

Add a screenshot or short demo video here after running the notebook.

Example:

```md
![Demo Result](assets/demo_screenshot.png)
```

---

## Project Overview

This project was developed as a Computer Vision final project.

The goal is to build an AI prototype that can help detect possible littering behavior in public areas, such as streets, parks, campuses, and smart city environments.

The project is not only about detecting objects. It also tries to understand the event across video frames.

The system checks if:

- A person appears in the scene
- A trash object appears near the person
- The trash is not just being carried in the person’s hand
- The trash remains in the scene
- The event is confirmed across multiple frames

If these conditions are satisfied, the system shows a possible littering warning and saves evidence.

---

## Key Features

- Detects people and trash objects
- Uses **YOLO11m** for object detection
- Uses **ByteTrack** for object tracking
- Processes fixed-camera videos
- Applies silent calibration to learn pre-existing trash
- Uses carry-check logic to reduce false warnings while trash is still in the hand
- Uses proximity and temporal confirmation before firing an alert
- Saves annotated output videos
- Saves evidence screenshots for detected events
- Generates training and evaluation graphs

---

## Technologies Used

- Python
- OpenCV
- Ultralytics YOLO
- YOLO11m
- ByteTrack
- PyTorch
- NumPy
- Pandas
- Matplotlib
- Pillow
- FiftyOne
- Jupyter Notebook

---

## Dataset

The project uses a combination of local annotated data and optional external data.

| Source | Purpose |
|---|---|
| Local Roboflow export | Domain-specific person and trash annotations |
| Open Images V7 | Extra images for Person, Bottle, Tin can, Plastic bag, and Waste container |
| YOLO11m COCO weights | Pretrained backbone for fine-tuning |

The main classes are:

```text
0 - person
1 - trash
```

The notebook also includes logic for converting polygon annotations into YOLO bounding-box format.

---

## Project Pipeline

```text
Video / Images
      ↓
Frame Extraction
      ↓
Annotation Preparation
      ↓
YOLO Dataset Formatting
      ↓
YOLO11m Training
      ↓
Video Detection + ByteTrack
      ↓
Event Logic
      ↓
Annotated Video + Evidence Screenshots
```

---

## Event Detection Logic

The system uses several rules to make the alert more reliable:

| Logic Component | Purpose |
|---|---|
| Silent calibration | Learns trash that already exists in the scene before detection starts |
| Proximity check | Checks if trash appears near a person |
| Carry-check | Avoids firing when trash is still being held |
| Temporal confirmation | Confirms the event over multiple frames |
| Per-track suppression | Prevents the same trash track from triggering repeated alerts |
| Recent-event suppression | Reduces duplicate warnings from ID switches |

---

## Folder Structure

```text
littering-detection-cv/
│
├── littering_detection.ipynb
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
│
├── assets/
│   └── .gitkeep
│
├── input/
│   └── README.md
│
├── outputs/
│   └── README.md
│
├── evidence/
│   └── README.md
│
├── graphs/
│   └── README.md
│
├── models/
│   └── README.md
│
└── docs/
    └── .gitkeep
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/FaresAldeeb/littering-detection-cv.git
cd littering-detection-cv
```

Install the required packages:

```bash
pip install -r requirements.txt
```

---

## How to Run

1. Open the notebook:

```text
littering_detection.ipynb
```

2. Put your test videos inside:

```text
input/
```

3. Run the notebook cells step by step.

4. The results will be saved in:

```text
outputs/
evidence/
graphs/
```

---

## Important Configuration

At the beginning of the notebook, you can control the stages using these flags:

```python
SKIP_INSTALL  = True
SKIP_DOWNLOAD = True
SKIP_MERGE    = True
SKIP_TRAIN    = True
SKIP_EVAL     = True
```

Set a flag to `False` when you want to run that stage.

For example, to train again:

```python
SKIP_TRAIN = False
```

---

## Results

The system generates:

- Annotated videos with bounding boxes
- Possible littering warnings
- Evidence screenshots
- Graphs and visualizations
- Final event summary

---

## Challenges

Some challenges faced during this project:

- Small trash objects are difficult to detect
- Lighting changes can affect detection
- Similar objects can cause false positives
- Occlusion can hide trash or people
- Person-trash attribution is difficult when multiple people are close together
- Limited custom dataset size affects model generalization

---

## Limitations

This project is an initial prototype.

Littering detection is harder than simple object detection because it requires understanding object relationships and behavior over time.

The system may still produce false positives or miss some events in difficult scenes.

---

## Future Improvements

Possible improvements:

- Use a larger custom dataset
- Improve trash annotation quality
- Add stronger multi-object tracking
- Add action recognition
- Improve person-trash attribution
- Add real-time camera support
- Build a dashboard for smart city monitoring
- Deploy the model on an edge device

---

## Author

**Fares Haitham Aldeeb**  
Bachelor of Artificial Intelligence Student  
University of Prince Mugrin

---

## Project Type

Computer Vision Final Project  
AI / Deep Learning / Object Detection / Smart City
