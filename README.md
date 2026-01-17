# Rural Safe Parking Detection – Stage 1

## Project Overview
This project explores computer vision techniques to support the identification
of safe parking spots in unstructured rural environments using dashcam video data.

Stage 1 focuses on dataset creation, privacy-preserving preprocessing, annotation,
and instance segmentation model training.

---

## Stage 1 Scope
- Dashcam video frame extraction
- Automatic number plate blurring for privacy
- Dataset annotation using Roboflow
- Instance segmentation with YOLOv8
- Iterative model improvement and tuning

---

## Dataset
Source: Custom dashcam recordings from multiple rural locations.

Classes:
- Vehicle
- Obstacle
- Drivable_area

Annotations were created and refined using Roboflow.

---

## Pipeline (Stage 1)
1. Extract frames from dashcam videos
2. Blur detected number plates
3. Upload frames to Roboflow
4. Annotate dataset (3 classes)
5. Train YOLOv8 segmentation models
6. Evaluate and visualize predictions

---

## Notebooks
- `01_dataset_preparation.ipynb`  
  Frame extraction and privacy-preserving preprocessing.

- `02_yolov8_segmentation_training.ipynb`  
  Final YOLOv8 segmentation training configuration (YOLOv8m-seg).

---

## Results
Example segmentation outputs are available in:
assets/examples/

---

## Model Improvement Summary

Through dataset refinement and model tuning, segmentation performance improved
substantially, particularly for the Obstacle class.

- **Average Mask mAP50:** 0.603 → **0.793** (+31.5%)
- **Obstacle Mask mAP50:** 0.213 → **0.722**
- **Average Recall:** 0.591 → **0.710**

---

### Performance Comparison (Mask mAP50)

| Class           | Initial Model | Final Model |
|-----------------|---------------|-------------|
| Drivable_area   | 0.922         | **0.987**   |
| Obstacle        | 0.213         | **0.722**   |
| Vehicle         | 0.674         | 0.670       |
| **Average**     | **0.603**     | **0.793**   |


Improvements were achieved by refining obstacle annotations, increasing input resolution, and carefully tuning model hyperparameters, including batch size, learning rate, and patience, while transitioning from YOLOv8s-seg to YOLOv8m-seg and maintaining consistent data augmentation.

Obstacle segmentation improved by more that 3x, representing the largest gain across all classes.

A minor decrease in Vehicle mAP was observed, likely due to higher image resolution and inconsistent annotations, which will be addressed in future work. 

---

### Key Factors Behind Improvement

- Re-annotation of the Obstacle class to remove ambiguity with unannotated regions
- Increased image resolution (640 → 1024)
- Migration from YOLOv8s-seg to YOLOv8m-seg
- Careful tuning of batch size, learning rate, and early stopping

---

## Future Work (Stage 2)
- Improve Vehicle annotations
- Evaluate semantic segmentation for Obstacles
- Combine instance and semantic segmentation models
- Apply logic-based rules for parking suitability

---

## Tools & Technologies
- Python
- Google Colab
- Roboflow
- YOLOv8 (Ultralytics)
- YOLOv11 (number plate detection)
- OpenCV
- NumPy
- Matplotlib
- Git/GitHub