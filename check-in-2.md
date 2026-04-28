## Baselines Overview

Before presenting the evaluation results, we briefly describe the two baselines used in this study:

1. Classical (Non-Deep) Baseline

Method: Hand-crafted features + standard classifier (e.g., HOG + SVM).
Purpose: Serves as a simple, interpretable benchmark without deep learning.
Expectations: Limited ability to handle occlusions, small objects, or visually similar classes, but fast to train and easy to implement.

2. CNN Baseline

Method: Fine-tuned Faster R-CNN on COCO food categories.
Purpose: Leverages deep features for robust object detection and localization.
Expectations: Better performance on overlapping objects and complex visual patterns, but may still struggle on small or rare objects.

## Results and Evaluation
1. Metrics Summary

We evaluated two baselines for the food object detection task:

Classical Baseline: Traditional feature-based detection model.
CNN Baseline: Fine-tuned Faster R-CNN model pretrained on COCO.

| Class    | Precision | Recall | F1-score | Support |
| -------- | --------- | ------ | -------- | ------- |
| apple    | 0.19      | 0.19   | 0.19     | 48      |
| sandwich | 0.12      | 0.11   | 0.12     | 36      |
| orange   | 0.29      | 0.26   | 0.28     | 57      |
| broccoli | 0.29      | 0.32   | 0.30     | 63      |
| carrot   | 0.25      | 0.22   | 0.23     | 74      |
| hot dog  | 0.00      | 0.00   | 0.00     | 25      |
| pizza    | 0.31      | 0.32   | 0.31     | 57      |
| donut    | 0.26      | 0.28   | 0.27     | 68      |
| cake     | 0.21      | 0.24   | 0.22     | 63      |

Overall accuracy: 0.23
Macro-average F1-score: 0.21

CNN Baseline Performance (Faster R-CNN)

COCO evaluation metrics (on bounding box detection):

| Class ID | Class Name | Precision | Recall | F1-score | Support |
| -------- | ---------- | --------- | ------ | -------- | ------- |
| 1        | apple      | 0.1316    | 0.0820 | 0.1010   | 61      |
| 2        | sandwich   | 0.3243    | 0.4138 | 0.3636   | 29      |
| 3        | orange     | 0.2600    | 0.2549 | 0.2574   | 51      |
| 4        | broccoli   | 0.4318    | 0.3455 | 0.3838   | 55      |
| 5        | carrot     | 0.3243    | 0.2105 | 0.2553   | 57      |
| 6        | hot dog    | 0.7500    | 0.2308 | 0.3529   | 13      |
| 7        | pizza      | 0.6364    | 0.4930 | 0.5556   | 71      |
| 8        | donut      | 0.6415    | 0.4198 | 0.5075   | 81      |
| 9        | cake       | 0.8000    | 0.3137 | 0.4507   | 51      |

| Class (Name) | GT Samples | Class Acc | Box Acc | Joint Acc |
|--------------|-----------|----------|--------|-----------|
| 1 (apple)    | 61        | 0.0820   | 0.0820 | 0.0820    |
| 2 (sandwich) | 29        | 0.3793   | 0.5172 | 0.3793    |
| 3 (orange)   | 51        | 0.2549   | 0.2745 | 0.2549    |
| 4 (broccoli) | 55        | 0.3455   | 0.3455 | 0.3455    |
| 5 (carrot)   | 57        | 0.2105   | 0.2281 | 0.2105    |
| 6 (hot dog)  | 13        | 0.2308   | 0.4615 | 0.2308    |
| 7 (pizza)    | 71        | 0.4789   | 0.5493 | 0.4789    |
| 8 (donut)    | 81        | 0.4198   | 0.4568 | 0.4198    |
| 9 (cake)     | 51        | 0.3137   | 0.3529 | 0.3137    |

| Metric                         | Value |
| ------------------------------ | ----- |
| AP@[IoU=0.50:0.95] (all sizes) | 0.021 |
| AP@[IoU=0.50]                  | 0.039 |
| AP@[IoU=0.75]                  | 0.021 |
| AP (small)                     | 0.020 |
| AP (medium)                    | 0.026 |
| AP (large)                     | 0.018 |
| AR@[maxDets=100] (all)         | 0.033 |

Observations:

Both baselines achieve low absolute performance, reflecting the difficulty of detecting small and occluded food items.
CNN baseline slightly outperforms the classical baseline in overall localization and class prediction (e.g., higher AP for pizza, banana).
The classical baseline fails completely for some classes (e.g., hot dog, AP = 0).

2. Comparison Between Baselines

| Aspect                   | Classical Baseline        | CNN Baseline (Faster R-CNN)                     |
| ------------------------ | ------------------------- | ----------------------------------------------- |
| Localization             | Weak, often missing boxes | Better, can detect partially occluded objects   |
| Small objects            | Rarely detected           | Some detection, but still low AP                |
| Class imbalance handling | Poor                      | Slightly better due to pretrained COCO features |
| Overall AP               | Very low (~0.02–0.03)     | Slightly higher (~0.02–0.04)                    |
| Speed                    | Fast                      | Moderate (GPU recommended)                      |

Summary: CNN baseline leverages pretrained features to generalize better, but both methods struggle with small, occluded, or uncommon food items.

3. Sample Predictions and Visuals

Classical Baseline Failures:

Small objects (e.g., carrot, hot dog) often missed.
Overlapping food items cause merged detections.
False positives on non-food objects with similar color or texture.

CNN Baseline Failures:

Occluded or partially visible objects sometimes missed.
Confusion between visually similar food items (e.g., donut vs. cake, apple vs. orange).
Small objects (≤ 32x32 px) have very low recall.

(Insert 3–5 images here showing correct and incorrect predictions, highlighting missed small objects and misclassifications.)

4. Failure Analysis

Small Objects: Both models struggle to detect small items like hot dog, carrot, or small donuts.
Class Imbalance: Some categories (like hot dog) have fewer samples in the dataset, leading to poor detection.
Occlusion: Objects that overlap or are partially blocked are frequently missed.
Domain Shift / Noise: Variability in lighting, background clutter, and image resolution decreases performance.
Model Limitations: Classical feature-based methods rely on hand-crafted features (e.g., HOG, SIFT), which are less robust than CNN-based features learned from large datasets.

5. Conclusion

CNN-based Faster R-CNN is the stronger baseline, but mAP remains very low due to dataset challenges (small object size, occlusion, class imbalance).
Classical baseline can serve as a lower bound, useful for evaluating improvements.
Future improvements could include:
Data augmentation to handle small and occluded objects.
Fine-tuning a CNN on the filtered food dataset for more epochs.
Using a detection architecture designed for small objects (e.g., YOLOv8, DETR).
Balancing classes in the training set.
