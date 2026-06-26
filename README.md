# intravenous-therapy
# 🩺 Vision-Based AI System for Intravenous Therapy Monitoring and Complication Detection

## 📖 Overview

Intravenous (IV) therapy is one of the most frequently performed medical procedures in hospitals worldwide. Despite its widespread use, IV therapy is associated with serious complications that can threaten patient safety if not detected promptly. Existing IV monitoring systems primarily focus on fluid level, drip rate, or pressure monitoring and are unable to identify internal air bubbles or external IV insertion-site abnormalities.

This project presents a **Vision-Based Artificial Intelligence System** that employs **Computer Vision** and **Deep Learning** to continuously monitor IV therapy in real time. The proposed system automatically detects:

* 💨 **Air bubbles** inside IV tubing
* 🔴 **Redness**
* 🤕 **Swelling**
* 🩹 **Bruising** around the IV insertion site

Using **ResNet152V2 transfer learning**, the system provides automated, non-invasive monitoring capable of detecting both **internal** and **external** IV-related complications before they become clinically significant. By enabling early intervention, the proposed solution aims to improve patient safety, reduce nursing workload, and support smarter healthcare systems.

---

# 🚨 Problem Statement

Although IV therapy is considered a routine medical procedure, it presents two major clinical risks.

### 1. Air Embolism

Even a small air bubble entering the bloodstream may lead to **air embolism**, obstructing blood flow to vital organs such as the heart, lungs, or brain. This can result in:

* Respiratory distress
* Stroke-like symptoms
* Cardiac arrest
* Organ failure
* Death

Current IV monitoring devices are generally incapable of detecting small or transient air bubbles before they reach the patient.

---

### 2. Local IV Site Complications

Studies indicate that **30–56% of patients** receiving IV therapy develop local complications including:

* Phlebitis
* Infiltration
* Extravasation
* Hematoma
* Infection
* Thrombophlebitis

These conditions initially appear as visible symptoms such as redness, swelling, bruising, and skin discoloration. Routine manual inspections may delay detection, increasing the likelihood of severe complications.

---

# 💡 Proposed Solution

The proposed AI-powered vision system continuously captures images of:

* IV tubing
* IV insertion site

The captured images are processed using **deep convolutional neural networks** to detect abnormalities automatically.

Unlike existing solutions, this system simultaneously monitors:

* Internal IV tube abnormalities (air bubbles)
* External skin-level complications (redness, swelling, bruising)

This integrated monitoring framework improves patient safety through continuous, real-time surveillance.

---

# ✨ Novelty

The proposed system introduces several unique contributions:

* Simultaneous monitoring of **air bubbles** and **local IV site complications**
* Vision-based, non-contact monitoring
* Robust performance across:

  * Clear IV fluids
  * Pale yellow fluids
  * Deep yellow fluids
  * Blood (red fluids)
* Works under varying:

  * Lighting conditions
  * Backgrounds
  * Camera angles
* Detects different bubble sizes
* Supports diverse skin tones
* Utilizes Transfer Learning for improved medical image classification

To the best of our knowledge, no existing IV monitoring system integrates **real-time computer vision-based detection of both internal and external IV-related abnormalities within a single framework**.

---

# 🎯 Objectives

* Detect air bubbles before they pose a risk of air embolism.
* Identify redness, swelling, and bruising at the IV insertion site.
* Enable continuous, automated monitoring of IV therapy.
* Reduce dependency on periodic manual inspections.
* Improve patient safety through early AI-assisted clinical alerts.

---

# 🏗️ System Workflow

```text
Camera
   │
   ▼
Image Acquisition
   │
   ▼
Image Preprocessing
   │
   ▼
Data Augmentation
   │
   ▼
ResNet152V2 Feature Extraction
   │
   ▼
Global Average Pooling (2048 Features)
   │
   ▼
Fully Connected Neural Network
(Dense → BatchNorm → Dropout → Dense → Softmax)
   │
   ▼
Prediction
   │
   ▼
Clinical Alert Generation
```

---

# 🧠 Software Architecture

## 1. Image Acquisition

A camera continuously captures images of:

* IV tubing
* IV insertion site

---

## 2. Image Preprocessing

Each image undergoes:

* Image resizing
* Pixel normalization

### Data Augmentation

* Rotation
* Horizontal Flip
* Zoom
* Brightness Adjustment
* Width Shift
* Height Shift

This increases dataset diversity, reduces overfitting, and improves robustness under varying hospital conditions.

---

## 3. Feature Extraction

### Backbone Network

**ResNet152V2**

The pretrained ImageNet model is used as a feature extractor.

Key characteristics:

* ImageNet pretrained weights
* Frozen convolutional layers
* Deep residual learning
* Excellent feature representation

The convolutional feature maps are converted into a compact **2048-dimensional feature vector** using **Global Average Pooling (GAP)**.

---

## 4. Classification Network

```text
Input (2048 Features)
        │
Dense (256) + ReLU
        │
Batch Normalization
        │
Dropout (0.5)
        │
Dense (64) + ReLU
        │
Batch Normalization
        │
Dropout (0.4)
        │
Dense (2)
        │
Softmax
```

Each classifier performs binary classification for:

* Air Bubble Detection
* Redness Detection
* Swelling Detection
* Bruising Detection

---

# ⚙️ Training Configuration

| Parameter               | Value                           |
| ----------------------- | ------------------------------- |
| Backbone                | ResNet152V2                     |
| Transfer Learning       | Yes                             |
| ImageNet Weights        | Frozen                          |
| Optimizer               | Adam                            |
| Learning Rate           | 0.0001                          |
| Batch Size              | 32                              |
| Epochs                  | 30                              |
| Loss Function           | Sparse Categorical Crossentropy |
| Hidden Activation       | ReLU                            |
| Output Activation       | Softmax                         |
| Regularization          | L2                              |
| Dropout                 | 0.5, 0.4                        |
| Learning Rate Scheduler | ReduceLROnPlateau               |
| Early Stopping          | Enabled                         |

---

# 📊 Performance

## Air Bubble Detection

**Validation Accuracy:** **98.29%**

---

## Local Site Complication Detection

| Complication | Validation Accuracy |
| ------------ | ------------------- |
| Bruising     | **95.95%**          |
| Redness      | **94.15%**          |
| Swelling     | **93.65%**          |

---

# 📈 Model Comparison

Three transfer learning architectures were evaluated:

* ResNet152V2
* EfficientNetV2M
* NASNetMobile

Among these, **ResNet152V2** consistently achieved the highest validation accuracy due to:

* Deep residual learning
* Superior feature extraction capability
* Better generalization on medical images
* Improved classification performance

---

# 🚀 Key Features

* Real-time IV monitoring
* AI-powered computer vision
* Non-contact monitoring
* Automated clinical alerts
* Air bubble detection
* Redness detection
* Swelling detection
* Bruising detection
* Transfer Learning
* Multi-fluid compatibility
* Diverse skin tone support
* Cost-effective deployment

---

# 🛠️ Technologies Used

## Programming

* Python

## Deep Learning

* TensorFlow
* Keras

## Computer Vision

* OpenCV

## Transfer Learning Models

* ResNet152V2
* EfficientNetV2M
* NASNetMobile

## Libraries

* NumPy
* Pandas
* Matplotlib
* Scikit-learn

---

# 📂 Project Structure

```text
Vision-Based-IV-Monitoring/
│
├── Bubble_Dataset/
│   ├── Bubble/
│   └── WithoutBubble/
│
├── Redness_Dataset/
│
├── Swelling_Dataset/
│
├── Bruising_Dataset/
│
├── Models/
│   ├── ResNet152V2
│   ├── EfficientNetV2M
│   └── NASNetMobile
│
├── notebooks/
│
├── results/
│
├── README.md
│
└── requirements.txt
```

---

# 💻 Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/vision-based-iv-monitoring.git
```

Navigate to the project directory:

```bash
cd vision-based-iv-monitoring
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

---

# ▶️ Running the Project

Train the model:

```bash
python train.py
```

Run inference:

```bash
python predict.py
```

---

# 🏥 Applications

* Hospitals
* Intensive Care Units (ICUs)
* Emergency Departments
* Oncology Wards
* Pediatric Care
* Home Healthcare
* Smart Hospitals
* Remote Patient Monitoring Systems

---

# 🔮 Future Enhancements

* Multi-patient monitoring
* Edge AI deployment (Jetson Nano, Raspberry Pi)
* Mobile application integration
* Explainable AI using Grad-CAM
* Severity grading of IV complications
* IoT-enabled smart IV stand
* Hospital dashboard integration
* Electronic Health Record (EHR) integration

---

# 📜 Patent Status

**Patent Filed**

**Title:** *Vision-Based AI for IV Therapy Monitoring and Complication Detection with ResNet-Based Neuro-Symbolic System*

---



# 📄 License

This project is intended for **academic research, educational purposes, and healthcare innovation**. For commercial use or redistribution, please contact the project authors.
