# DSAN-6500-Final_Project
# Food Object Detection using COCO Subset

## 1. Problem Framing and Scope

This project focuses on **food object detection in images** using a subset of the COCO dataset.

The goal is to detect food-related objects and localize them with **bounding boxes**. This is a **computer vision object detection task**, where the model must identify both the **category** and the **location** of objects in an image.

### Task Definition

Given an input image, the model should:

- Detect food-related objects
- Predict bounding boxes
- Assign a class label to each detected object

### Success Criteria

Performance will be evaluated using standard object detection metrics such as:

- mAP (mean Average Precision)
- Detection precision
- Detection recall
- Qualitative inspection of predicted bounding boxes

### Scope

To keep the project feasible within the semester timeline, we focus on a **subset of food-related categories** rather than the full dataset.

The project will include:

- Dataset exploration and auditing
- Baseline object detection using a pretrained model
- Potential fine-tuning of a detector on the filtered dataset

### Modality

Vision (image-based object detection)

---

# 2. Dataset Access and Documentation

## Dataset

We use the **COCO 2017 dataset**.

Source: https://cocodataset.org/

Annotation type:

- Bounding boxes
- Object category labels

The full COCO dataset contains **80 object categories**, including several food-related classes.

## Selected Food Categories

This project focuses on the following food classes:

| Category | COCO ID |
|--------|--------|
| banana | 47 |
| apple | 48 |
| sandwich | 49 |
| orange | 50 |
| broccoli | 51 |
| carrot | 52 |
| hot dog | 53 |
| pizza | 54 |
| donut | 55 |
| cake | 56 |

## Dataset Size

After filtering the dataset to only include images containing these food categories:

- Images: ~708
- Classes: 10
- Multiple bounding boxes per image

## Dataset License

COCO is released under **Creative Commons Attribution 4.0 (CC BY 4.0)**.

## Dataset Access Instructions

Download the dataset from:

https://cocodataset.org/#download

---

# 3. Data Audit / Exploratory Data Analysis (EDA)

## Representative Samples

Example images with **ground-truth bounding boxes** were visualized to verify that annotations and category filtering are correct.

The notebook includes visualizations showing:

- Bounding boxes for food categories
- Multiple example images from the dataset

## Dataset Characteristics

Key characteristics of the filtered dataset:

- ~708 images
- 10 food-related categories
- Images vary in resolution
- Some images contain multiple objects

## Summary Statistics

The following statistics were analyzed:

- Image size distribution
- Number of objects per image
- Class distribution

Visualizations include:

- Scatter plot of image width vs height
- Histogram of objects per image
- Bar chart showing class frequency

## Observed Artifacts or Biases

Several dataset characteristics were observed:

- Class imbalance across food categories
- Multiple food items in the same image
- Small or partially occluded objects

These factors may affect model performance.

---

# 4. Evaluation Plan

The model will be evaluated using standard **object detection metrics**.

## Metrics

Primary metrics:

- mAP (mean Average Precision)
- Precision
- Recall

These metrics evaluate both:

- classification accuracy
- bounding box localization

## Data Split

The dataset will be split into:

Train: 70%
Validation: 15%
Test: 15%


This allows proper model evaluation and hyperparameter tuning.

---

# 5. Initial Baseline / Representation

As an initial baseline, we use a **pretrained Faster R-CNN model** from PyTorch.

The model was pretrained on the COCO dataset and can detect many object categories including several food classes.

## Baseline Procedure

1. Load a pretrained Faster R-CNN model
2. Run inference on images from the filtered dataset
3. Visualize predicted bounding boxes and class labels

Example output includes:

- predicted bounding boxes
- predicted class labels
- confidence scores

These predictions are visualized and compared with ground-truth annotations.

## Early Observations

Initial results show that the pretrained detector can identify several food categories such as:

- pizza
- banana
- apple

However, performance varies depending on:

- object size
- occlusion
- category frequency

## Next Steps

Future work will include:

- Fine-tuning the model on the filtered food dataset
- Improving detection performance on underrepresented classes
- Quantitative evaluation using mAP

---

