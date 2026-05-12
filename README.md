# Cardboard Defect Detection | Machine Vision System

Real-time computer vision pipeline for industrial quality control, designed to detect geometrical, texture, and structural defects in cardboard blanks on high-speed production lines.

[**📄 Read the Full Technical Report**](https://github.com/LoreB43/Cardboard-Defect-Detection/blob/main/AMSfCA_Report.pdf)

---

## Project Overview
The system provides automated, first-level screening for cardboards on a conveyor belt. It distinguishes between acceptable items and those with missing die-cuts, improper folds, surface damage, or dimensional inaccuracies.

### Key Technical Specs:
*   **Throughput:** Optimized for speeds up to **111.75 m/min**.
*   **Precision:** Motion blur kept below **5px** via calibrated 1ms exposure.

---

## Problems
Detecting defects on cardboard is more complex than it appears due to several "hidden" variables:

1.  **Geometric Ambiguity:** The analyzed cardboard features a high number of folds and die-cuts with **non-perpendicular angles**. Distinguishing between a intentional fold and a structural deformity requires high-precision orientation correction.
2.  **Real-Time Constraints:** At 1.86 m/s, the window for image acquisition and processing is minimal. Any lag in the pipeline results in motion blur that makes texture analysis (scratches) impossible.
3.  **Lighting Sensitivity:** Folds are only visible through shadows created by tangential light. However, too much light causes overexposure on the cardboard surface, while too little makes it impossible to distinguish the cardboard from the conveyor background.
4.  **Signal vs. Noise:** Scratches and creases (defects) often have the same "visual signature" as intentional fold lines. The system must intelligently **subtract known structural features** to isolate actual damage.

<img src="https://github.com/user-attachments/assets/abe64b98-6831-4174-a0ed-91e23e529577" width="30%" alt="Defect detection process" />

---

## Solution

### Calibration & Preprocessing
Camera calibration and image preprocessing are important to achieve the best results in image analysis
*   **Spatial Calibration:** Established a **0.3730 mm/px** scale using checkerboard patterns.
*   **Perspective & Alignment:** Automated vertical alignment using Hough Lines on external contours to ensure consistent comparison across samples.
*   **Multi-Channel Separation:** Leveraged Red and Green channels separately to maximize contrast of specific fold orientations.

<img src="https://github.com/user-attachments/assets/108b69ce-7c9f-4297-afb6-c9289a4708b8" width=50% />


The structure and texture are then identified, and a metric is used to assess the damage to the cardboard

### 1. Texture & Structural Analysis
*   **Texture Isolation:** Used **Sobel operators** and subtracted a "Main Feature Mask" to remove folds and edges, leaving only surface anomalies (scratches).
*   **Fold Validation:** Probabilistic Hough Transform to verify the presence, length, and angle of every required fold.

<img src="https://github.com/user-attachments/assets/0378eb07-9d75-4b14-8a84-bd9cdfb9674f" width=30% />



### 2. Geometrical Defect Detection
A custom mathematical model calculates a **Composite Defect Score**:
$$Score = w_g \cdot d_g + w_m \cdot M + w_e \cdot E + w_h \cdot \sum \text{max}(0, d_h^{(i)} - \theta_h)$$
*   Compares the test sample to a high-quality reference using `cv.matchShapes`.
*   Penalizes missing/extra holes ($M/E$) and shape deviations ($d_h$).

<img src="https://github.com/user-attachments/assets/7794b7cf-7143-43ea-80ed-1db0d41f971a" width=53% />

<img src="https://github.com/user-attachments/assets/41c45a6e-b794-4f11-a2ac-66e5fc268f67" width=43% />

---

## 📈 Results & Performance

The system was stress-tested under four different lighting configurations and varying defect types.

| Metric | Result |
| :--- | :--- |
| **Dataset Size** | 108 Images |
| **False Negatives (Missed Defects)** | **0%** (Critical for Industrial Safety) |
| **False Positives (False Alarms)** | ~5.5% (6/108 images) |
| **Detection Robustness** | High, even with non-perpendicular folds |
| **Max Conveyor Speed** | 111.75 m/min |

> **Note:** The near-zero false negative rate ensures that no defective cardboard reaches the packaging stage, fulfilling the primary industrial requirement.

---

## How to Run
1.  **Clone the repo:** `git clone https://github.com/LoreB43/Cardboard-Defect-Detection.git`
2.  **Install dependencies:** `pip install opencv-python numpy matplotlib`
3.  **Run the analysis:** Open `Cardboard_pipeline.ipynb` in Jupyter Notebook.

## Authors
*   **Lorenzo Berti**
*   **Saad Nabil**
*   *Academic Year 2024-2025 | Politecnico di Milano*
