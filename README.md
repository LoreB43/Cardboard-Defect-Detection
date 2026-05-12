<img width="1126" height="1477" alt="light setup" src="https://github.com/user-attachments/assets/7cf8bc7d-b6e1-400c-8017-cc6177cc4d12" />
# Cardboard Defects Detection - Machine Vision System
Implementation of a real-time machine vision pipeline designed to ensure quality control in packaging production lines by detecting geometrical, texture, and structural defects in cardboards.
<img src="https://github.com/user-attachments/assets/65f1b73f-718f-40e6-af6b-13454b3e180a"  width="35%" />
<img src="https://github.com/user-attachments/assets/abe64b98-6831-4174-a0ed-91e23e529577"  width="35%"/>

---
## Problem Objectives
Lo scopo del progetto quello di implementare un machine vision system per individuare difetti su dei cardboard in un contesto packaging ottimizzato allo scopo di funzionare for high-speed conveyor belts (up to 111.75 m/min) with a motion blur threshold below 5px

### Tech Stack
Language: Python  
Libraries: OpenCV, NumPy, Matplotlib  
Hardware Integration: Configured for IDS UI-3060CP-C-HQ industrial cameras. 

## Problem
Complicata disposizione dei delle pieghe e fori dei cardboard posizionati a 90 gradi e leggermete obliqui che complicavano la situazione per evidenziare i dettagli del problema

Multi-Channel Analysis: Leverages RGB channel separation and tangential lighting (Red/White LEDs) to isolate specific features like folds and surface scratches.  
Advanced Feature Extraction: Uses a combination of Canny edge detection, Sobel operators, and Probabilistic Hough Transforms.  
Automated Scoring System: A custom mathematical model to classify defects based on shape similarity (cv.matchShapes), hole counting, and angular deviation of fold lines.  

## Solution
Calibration: Calculated pixel-to-mm scale (0.3730 mm/px) and optimized exposure time (1ms).  
Preprocessing: Perspective correction, vertical alignment, and CLAHE for contrast enhancement.  
Detection Logic:  
Geometrical: Compares test samples against a high-quality reference using hierarchical contour analysis.  
Texture: Isolates damage by subtracting structural masks from Sobel gradient maps.  
Folds & Scratches: Segmented region analysis to detect improper folding or surface irregularities.  
## Problems

## Results
The system demonstrated high robustness across varying lighting conditions, achieving a near-zero false negative rate over a dataset of 108 test images.
<img width="1126" height="1477" alt="light setup" src="https://github.com/user-attachments/assets/ba722fed-e842-4a0a-ac38-aea7a2e8fe3f" />

<img src="https://github.com/user-attachments/assets/dd3e52df-4aa7-4a03-8288-2e5eae0bc28a" width="30%">
<img src="https://github.com/user-attachments/assets/4f1884b0-4cd0-48b5-be7c-a8300793612c" width="30%">

## Future Work

## How to Run

