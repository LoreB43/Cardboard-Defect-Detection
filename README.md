# Cardboard Defects Detection - Machine Vision System
Implementation of a real-time machine vision pipeline designed to ensure quality control in packaging production lines by detecting geometrical, texture, and structural defects in cardboards.

---
## Project Objectives   
Implementation of a real-time machine vision pipeline designed to ensure quality control in packaging production lines by detecting geometrical, texture, and structural defects in cardboards.  

## Realization

### 🚀 Key Features
Real-time Performance: Optimized for high-speed conveyor belts (up to 111.75 m/min) with a motion blur threshold below 5px.  
Multi-Channel Analysis: Leverages RGB channel separation and tangential lighting (Red/White LEDs) to isolate specific features like folds and surface scratches.  
Advanced Feature Extraction: Uses a combination of Canny edge detection, Sobel operators, and Probabilistic Hough Transforms.  
Automated Scoring System: A custom mathematical model to classify defects based on shape similarity (cv.matchShapes), hole counting, and angular deviation of fold lines.  

### 🛠 Tech Stack
Language: Python  
Libraries: OpenCV, NumPy, Matplotlib  
Hardware Integration: Configured for IDS UI-3060CP-C-HQ industrial cameras.  

### 📋 Methodology
Calibration: Calculated pixel-to-mm scale (0.3730 mm/px) and optimized exposure time (1ms).  
Preprocessing: Perspective correction, vertical alignment, and CLAHE for contrast enhancement.  
Detection Logic:  
Geometrical: Compares test samples against a high-quality reference using hierarchical contour analysis.  
Texture: Isolates damage by subtracting structural masks from Sobel gradient maps.  
Folds & Scratches: Segmented region analysis to detect improper folding or surface irregularities.  
## Problems

## Solutions

### 📈 Results
The system demonstrated high robustness across varying lighting conditions, achieving a near-zero false negative rate over a dataset of 108 test images.
<img src="https://github.com/user-attachments/assets/dd3e52df-4aa7-4a03-8288-2e5eae0bc28a" width="30%">
<img src="https://github.com/user-attachments/assets/4f1884b0-4cd0-48b5-be7c-a8300793612c" width="30%">

## Future Work

## How to Run

