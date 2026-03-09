Rural Safe Parking Detection – Stage 1
Project Overview

This project explores computer vision techniques to support the identification of safe parking spots in unstructured rural environments using monocular dashcam video and YOLOv8 segmentation.

Stage 1 focuses on dataset creation, privacy-preserving preprocessing, annotation, instance segmentation model training, and model optimization.

Stage 1 Scope

Dashcam video collection and frame extraction

Automatic license plate blurring for privacy

Establishing annotation rules

Dataset annotation using Roboflow

Dataset augmentation design and application

Instance segmentation with YOLOv8

Iterative model improvement and tuning

Dataset

Source: Custom dashcam recordings collected from multiple rural locations.

Classes

Vehicle

Non_drivable (earlier named Obstacle)

Drivable_area

Class Naming Note

During the course of the project, the class originally labeled Obstacle was renamed to Non_drivable following refinement of annotation guidelines.

Some earlier experiments and figures therefore reference Obstacle, while later results use Non_drivable. The two terms refer to the same semantic category, with improved boundary definition and labeling consistency introduced in the later phase.

Annotations were created and refined using Roboflow.

Pipeline (Stage 1)

Collect dashcam videos

Extract frames from videos

Apply automatic license plate blurring

Upload frames to Roboflow

Annotate dataset (3 classes)

Train YOLOv8 segmentation models

Evaluate model performance

Visualize predictions

Notebooks
01_dataset_preparation.ipynb

Frame extraction and privacy-preserving preprocessing.

02_yolov8_segmentation_training.ipynb

Final YOLOv8 segmentation training configuration (YOLOv8s-seg).

Results

Example segmentation outputs are available in:

assets/examples/

Training curves and evaluation plots are available in:

assets/plots/
Final Model Performance

The final model achieved strong segmentation performance across all classes.

Class		Test mAP50
Drivable_area	0.979
Non_drivable	0.995
Vehicle		0.701
Average		0.892

Drivable_area and Non_drivable achieve near-perfect segmentation, while Vehicle remains the most challenging class due to occlusions, scale variation, and limited test instances.

Key Factors Behind Improvement

Performance improvements were achieved primarily through dataset refinement and annotation consistency, including:

Full-object annotation for the Non_drivable class

Removal of small distant vehicles that were not visible at training resolution

Enforcing a one-mask-per-object annotation policy

Increasing training image resolution (640 → 1024)

These changes significantly improved segmentation stability and mask precision, demonstrating that dataset quality had a larger impact than hyperparameter tuning for this project.

Future Work (Stage 2)

Planned next steps include:

Training with higher image resolution if more GPU resources become available

Reintroducing small distant vehicles once higher resolution training is feasible

Improving vehicle detection across scales

Combining segmentation results with logic-based parking suitability rules

The goal of Stage 2 is to move from scene segmentation to automated safe parking spot identification.

Tools & Technologies

Python

Google Colab

Roboflow

YOLOv8 (Ultralytics)

YOLOv11 (license plate detection for privacy blurring)

OpenCV

NumPy

Matplotlib

Git / GitHub