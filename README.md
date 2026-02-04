# Multimodal Object Detection with Visible & Infrared Fusion

This repository implements **multimodal object detection** by combining **visible (RGB)** 
and **infrared (IR)** images using **early fusion, mid fusion, and late fusion** strategies.  
The project evaluates how different fusion stages affect detection performance under 
challenging conditions such as **low-light and night scenes**.

This work is based on my bachelor research project and experimental evaluation using 
**YOLOv5** and the **M3FD dataset**.

---

## 📌 Project Overview

Traditional object detection models perform well in good lighting conditions but struggle 
at night or in low visibility. Infrared images are robust in low-light conditions but lack 
rich visual details for classification.

**Goal:**  
To determine **which fusion strategy (early, mid, or late fusion)** is most effective for 
multimodal object detection.

---

## 📂 Dataset

The dataset used in this project is **M3FD (Multimodal Multi-spectral Firearm Dataset)**, 
which contains paired **visible (RGB)** and **infrared (IR)** images captured under 
daytime and nighttime conditions.

- Total images: 8,400 (visible + infrared)
- Classes: Person, Car, Bus, Motorcycle, Lamp, Truck
- Image resolution: 1024 × 768

🔗 **Download link (GitHub):**  [https://github.com/JinyuanLiu-CV/TarDAL]

> ⚠️ The dataset is **not included** in this repository due to its large size.  
> Please download it manually and place it in the appropriate data directory.

---

## 📁 Repository Structure
```text

Multi-modal_Object_Detection/
├── early_fusion/
├── mid_fusion/
├── late_fusion/
└── README.md
```
---

## 🔍 Fusion Strategies Implemented

### 1️⃣ Early Fusion (Input-Level)
Visible and infrared images are combined **before** being fed into the model.

Implemented methods:
- 4-channel fusion (RGB + IR)
- Pixel-wise average
- Pixel-wise addition
- Pixel-wise multiplication
- Wavelet transform fusion

📁 Folder: `early_fusion/`

---

### 2️⃣ Mid Fusion (Feature-Level)
Visible and infrared images are processed by **separate backbones**, then fused at the 
**feature map stage** inside YOLOv5.

Implemented methods:
- Average feature maps
- Channel Switching & Spatial Attention (CSSA)
- Iterative Cross-Attention (ICA)

📁 Folder: `mid_fusion/`

---

### 3️⃣ Late Fusion (Decision-Level)
Visible and infrared models are trained **independently**, and their predictions are 
combined at inference time.

Implemented methods:
- Non-Maximum Suppression (NMS)
- Average prediction fusion
- **Probabilistic Ensembling (ProEn)**

📁 Folder: `late_fusion/`

---

## 🧠 Model & Evaluation

- **Model:** YOLOv5s (PyTorch)
- **Dataset:** M3FD (Visible + Infrared)
- **Evaluation Metric:** mAP@0.5 (mAP50)
- **Classes:** Person, Car

---

## 📊 Key Results

| Method | mAP50 |
|------|------|
| Visible only | 0.8637 |
| Infrared only | 0.9309 |
| Best Early Fusion (Wavelet) | 0.9284 |
| Best Mid Fusion (ICA) | 0.9121 |
| **Late Fusion (Probabilistic Ensembling)** | **0.9333** ✅ |

🔑 **Conclusion:**  
Late fusion with **Probabilistic Ensembling** achieved the **best overall performance**, 
outperforming both single-modality and other fusion strategies.



## ⚙️ Environment

- Python 3.x  
- PyTorch  
- YOLOv5  
- OpenCV  
- NumPy  

Hardware used:
- NVIDIA RTX 2080 (8GB)
- Intel i5-10400F
- 64GB RAM

---

## 🚀 Future Work

- Extend experiments to larger datasets (FLIR, KAIST)
- Explore learned fusion strategies
- Reduce false positives in late fusion
- Improve computational efficiency of mid fusion

---

## 👤 Author

**Tri Luan Le**  
Master Project – Multimodal Object Detection  
The University of Adelaide

---
