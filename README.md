# SenseCap
IMU-Sensor Alignment and Activity-Based Highlight Detection in MTB videos

# 🚴 IMU-Based Movement Classification

This project focuses on recognizing and classifying movement patterns (e.g. jumping, turning) using data from multiple IMU sensors (Head, Wrist, Seat).

---

## 🔧 Project Structure

All data is stored in **Google Drive**, organized by session:

Google Drive/

└── ML-MTB-Modell/

├── Session_01/

│ ├── Head_123.csv

│ ├── Wrist_123.csv

│ ├── Seat_123.csv

│ ├── hot.json # Fine-grained labels (Action, Pedaling, etc.)

│ └── sequences.json # Coarse sequence labels (Jumping, Turning, etc.)

├── Session_02/

│ └── ...
└── ...







Each session contains:
- **3 CSV files** with sensor data (one per sensor)
- **1 HOT label file** (`hot.json`) with frame-wise action labels
- **1 Sequence label file** (`sequences.json`) with action points (e.g. Jumping, Left, Right)

---

## 📒 Notebooks

### 1. `SenseCap_v4_2_globalModel_balancedData.ipynb`
Trains a global model on all available sessions except for a selected test session.
- Windowing (e.g. `window_size = 60` frames)
- Sensor fusion into 27-feature windows
- Classification using an LSTM 

### 2. `test-one-session_Notebook.ipynb`
Evaluates the trained model on one **unseen session**:
- Visualizes `true vs predicted labels`
- Calculates metrics like accuracy, confusion matrix, etc.

---

## 🧪 Labels

### Frame-level HOT labels
Fine-grained annotations for every frame:
- `"Action"`, `"Pushing"`, `"Pedaling"`, `"Resting"`

### Sequence-level labels
Coarse labels based on key button presses or video annotation:
- `"Jumping"`, `"Left"`, `"Right"`, `"Back Wheel block"`, `"Other"`

Sequence labels are mapped to the corresponding frame ranges.

---

## 🗃️ Data Processing Overview

- **Sampling rate**: ~60 Hz → `window_size = 60` frames ≈ 1 second
- **Sensor fusion**: combines Head, Wrist, and Seat data into one feature vector (27 values per frame window)
- **Window labeling**: uses majority label (mode) per window from HOT labels, optionally combined with sequence labels

---

## 📈 Project Goals

- Recognize and classify physical activities based on IMU data
- Test generalization to unseen sessions (cross-session validation)
- Visualize prediction results for validation and debugging

---

#Contact
Project Team: Marlene Brandster & Ruven Overberg
further information/questions: ruven.overberg@gmx.de  bm6109@mci4me.at

