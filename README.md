# Detecting and Identifying Defects in PCBs Using YOLOv5

## Introduction
Printed Circuit Boards (PCBs) are vital components in modern electronics. Ensuring their quality is critical as defects can lead to device failures, costly repairs, and damage to brand reputation. This guide walks through the process of automating PCB defect detection using YOLOv5, a state-of-the-art object detection model. The project is implemented in Python and Jupyter Notebook, covering data collection, annotation, model training, and evaluation.

## Project Structure
```bash 
PCB_Defect_Detection/
│
├── dataset/
│   ├── images/
│   │   ├── train/
│   │   └── val/
│   └── labels/
│       ├── train/
│       └── val/
│
├── notebooks/
│   ├── data_preparation.ipynb
│   └── model_training.ipynb
│
├── dataset.yaml
├── README.md
├── environment.yaml
└── requirements.txt
```

## Installation
Clone the repository:

```bash
git clone https://github.com/Gayathri-Selvaganapathi/PCB_defect_detection_yolo.git
cd PCB_defect_detection_yolo
```

## Install dependencies:

```bash
pip install -r requirements.txt
```

## Download the dataset from Kaggle:

https://www.kaggle.com/datasets/akhatova/pcb-defects

## Extract the dataset and organize it according to the required structure:

```bash
pcb_defects/
├── images/
├── annotations/
```

## Convert XML annotations to YOLOv5 format:

Copy all the folders in the Annotation folder to the xml folder in XmlToTxt repo,then run the below comments.

```bash
# Install the necessary dependencies from the requirements file
!pip install -r xml_to_txt/requirements.txt
# Import the conversion module and run the conversion process
import os
os.chdir("XmlToTxt")
!python xmltotxt.py -c classes.txt -xml xml -out out
```

## Data Preparation
Split the data into training and validation sets:

```bash
to_v5_directories("data/images/train", "data/images/val", "data/labels/train", "data/labels/val", "pcb_defects/{class_name}")
```

## Model Training
Setting up YOLOv5

```bash

git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip install -r requirements.txt
```

## Configure the dataset:

Update the dataset.yaml file to point to the training and validation datasets.

## Train the model:

```bash

python train.py --img 640 --batch 16 --epochs 300 --data dataset.yaml --weights yolov5s.pt --project pcb_defects_run1
```

## Evaluation
Evaluate the trained model:

```bash

python val.py --weights runs/train/pcb_defects/weights/best.pt --data dataset.yaml
```

## License
This project is licensed under the MIT License - see the LICENSE file for details.

