# YOLOv5 CAPTCHA Object Detection

A computer vision project developed for the **Artificial Intelligence Applications in Cybersecurity** course.

This project explores how deep learning-based object detection can be applied to **CAPTCHA and reCAPTCHA-related images**. A pretrained **YOLOv5** object detection model is used to analyze images from a Google reCAPTCHA dataset and identify objects that belong to the classes supported by the pretrained model.

The project also demonstrates **real-time object detection using a webcam**, providing a practical example of how computer vision models can be used for automated visual analysis.

---

## Overview

CAPTCHAs and reCAPTCHAs are widely used as a security mechanism to distinguish between human users and automated systems.

Many modern CAPTCHA challenges require users to identify specific objects or visual patterns, such as:

* Cars
* Bicycles
* Traffic lights
* Motorcycles
* Buses
* Crosswalks
* Other common objects

This project investigates the use of **AI-based object detection** as a computer vision approach for analyzing CAPTCHA-style images.

---

## Dataset

The project uses the **Google reCAPTCHA dataset** available through Kaggle:

**Dataset:** `sanjeetsinghnaik/google-recaptcha`

The dataset is downloaded programmatically using `kagglehub`.

The downloaded images are then searched recursively and a number of sample images are selected for object detection.

> **Important:** The current implementation does not fine-tune YOLOv5 on this dataset. It uses the pretrained YOLOv5 model directly. Therefore, the project demonstrates the application of an existing object detection model to CAPTCHA-related images rather than training a CAPTCHA-specific detection model.

---

## YOLOv5 Model

The project uses the pretrained:

**YOLOv5s**

YOLO (You Only Look Once) is a family of real-time object detection models capable of detecting multiple objects in an image and predicting:

* Object class
* Bounding box
* Confidence score

The `yolov5s` model provides a lightweight architecture suitable for fast inference and real-time applications.

---

## CAPTCHA Object Detection

For each selected image, the system performs object detection using YOLOv5.

The detection pipeline:

```text
reCAPTCHA Image
       │
       ▼
   OpenCV
       │
       ▼
   YOLOv5
       │
       ▼
Object Detection
       │
       ├── Object Class
       ├── Bounding Box
       └── Confidence Score
       │
       ▼
Visualization + Results
```

The detection function processes an image and returns the detected object labels.

This allows the project to inspect which recognizable objects appear in the CAPTCHA-related images.

---

## Detection Results

YOLOv5 provides detailed detection information for each recognized object.

For every detection, information such as the following can be obtained:

| Information  | Description                       |
| ------------ | --------------------------------- |
| `xmin`       | Left coordinate of bounding box   |
| `ymin`       | Top coordinate of bounding box    |
| `xmax`       | Right coordinate of bounding box  |
| `ymax`       | Bottom coordinate of bounding box |
| `confidence` | Model confidence                  |
| `class`      | Numerical object class            |
| `name`       | Detected object name              |

For example, the model may identify objects such as:

```text
car
truck
bus
traffic light
person
bicycle
motorcycle
```

depending on the contents of the input image and the classes supported by the pretrained YOLOv5 model.

The detected objects are also visualized directly on the input images using bounding boxes.

---

## Real-Time Object Detection

In addition to static images, the project implements real-time object detection using a webcam.

The webcam captures frames continuously:

```text
Webcam
   │
   ▼
Video Frame
   │
   ▼
YOLOv5
   │
   ▼
Object Detection
   │
   ▼
Bounding Boxes
   │
   ▼
Live Display
```

This demonstrates that the same object detection pipeline can be extended from individual CAPTCHA images to live visual streams.

---

## Technologies

| Technology   | Purpose                               |
| ------------ | ------------------------------------- |
| Python       | Main programming language             |
| PyTorch      | Deep learning framework               |
| YOLOv5       | Object detection                      |
| OpenCV       | Image and video processing            |
| KaggleHub    | Dataset download                      |
| Pandas       | Detection result analysis             |
| Google Colab | Development and execution environment |

---

## Running the Project

### 1. Download the Dataset

Run the dataset acquisition section:

```python
import kagglehub

path = kagglehub.dataset_download(
    "sanjeetsinghnaik/google-recaptcha"
)
```

### 2. Load YOLOv5

```python
import torch

model = torch.hub.load(
    "ultralytics/yolov5",
    "yolov5s"
)
```

### 3. Detect Objects in Images

Select sample images from the dataset and run the detection function.

The notebook displays:

* Original image
* Detected objects
* Bounding boxes
* Confidence scores
* Detection table

### 4. Run Real-Time Detection

Run the webcam detection section and press:

```text
Q
```

to stop the webcam detection loop.

---

## Workflow

The complete project workflow can be summarized as:

```text
Google reCAPTCHA Dataset
          │
          ▼
    Image Collection
          │
          ▼
   Sample Image Selection
          │
          ▼
   Pretrained YOLOv5
          │
          ▼
   Object Detection
          │
          ├───────────────┐
          ▼               ▼
Bounding Boxes      Detection Labels
          │               │
          └───────┬───────┘
                  ▼
          CAPTCHA Analysis
                  │
                  ▼
        Cybersecurity Context
```
