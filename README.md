
# Insider Threat Detection using Spatio-Temporal Two-Step Hybrid Model (GNN + LSTM)

## 📌 Project Overview

This project presents a **supervised spatio-temporal insider threat detection system** that combines **Graph Neural Networks (GNN)** and **Long Short-Term Memory (LSTM)** with a **two-step hierarchical classification framework** to detect malicious insider activities such as **data exfiltration** and **sabotage**.

The system models both:

* **Spatial behavior relationships** (user–activity interactions)
* **Temporal evolution of user behavior**

It is designed to address **extreme class imbalance** present in insider threat datasets such as CERT r4.2.

---

## 🎯 Objectives

* Detect insider threats from enterprise activity logs
* Classify threats into:

  * **0 → Normal**
  * **1 → Data Exfiltration**
  * **2 → Sabotage**
* Improve detection of rare sabotage events using hybrid loss and hierarchical modeling
* Capture behavioral evolution using temporal sequences

---

## 📂 Dataset

Dataset used: **CERT Insider Threat Dataset r4.2**

Source:
https://www.sei.cmu.edu/library/insider-threat-test-dataset/

Dataset Characteristics:

* ~1000 users
* Multi-source logs:

  * Logon
  * File
  * Email
  * HTTP
  * Device (USB)
* 70 malicious insider scenarios

  * 60 Exfiltration
  * 10 Sabotage
* Highly imbalanced distribution

---

## ⚙️ System Architecture

Pipeline:

```
Raw Logs
   ↓
Data Cleaning & Preprocessing
   ↓
Window Generation (Temporal Aggregation)
   ↓
Feature Engineering
   ↓
Graph Construction (Per Window)
   ↓
GNN Spatial Embedding
   ↓
Sequence Creation (L = 14)
   ↓
LSTM Temporal Modeling
   ↓
Step-1: Threat Detection (Binary)
   ↓
Step-2: Threat Type Classification
   ↓
Final Prediction
```

---

## 🧠 Model Design

### Step-1: Threat Detection

Binary classifier:

```
Normal vs Threat
```

Loss:

* Focal Loss + Binary Cross Entropy
* Handles imbalance between normal and threat samples

---

### Step-2: Threat Type Classification

Multi-class classifier:

```
Exfiltration vs Sabotage
```

Loss:

* Class-weighted Cross Entropy
* Helps learn rare sabotage patterns

---

## 📊 Sequence Creation

Temporal sequence length:

```
L = 14 windows
```

Number of sequences:

```
N_seq = N − L + 1
```

Where:

* N = number of windows for a user

Priority labeling rule:

```
If sabotage exists → label = 2
Else if exfil exists → label = 1
Else → label = 0
```

---

## ⚖️ Class Imbalance Handling

Techniques used:

1. **Weighted Random Sampling**
2. **Hybrid Loss (Focal + BCE)**
3. **Class-Weighted Cross Entropy**
4. **Sabotage Oversampling**
5. **Threshold Tuning**

---

## 🔧 Threshold Tuning

Step-1 probability threshold is optimized using validation data.

Selection criteria:

* Primary: Sabotage Recall
* Secondary: Exfiltration Recall
* Final: Validation Loss / Macro-F1

---

## 📈 Evaluation Metrics

* Accuracy
* Precision
* Recall
* Macro-F1 Score
* Weighted-F1
* Confusion Matrix
* Per-class Recall
* Sabotage Recall (Primary Research Metric)

---

## 🚀 Key Features

✅ Two-step hierarchical detection
✅ Spatio-temporal modeling (GNN + LSTM)
✅ Handles extreme imbalance
✅ Rare event sensitivity (sabotage detection)
✅ Threshold optimization
✅ Sequence-based behavioral learning

---

## 🖥️ Technologies Used

* Python
* PyTorch
* PyTorch Geometric
* Scikit-learn
* Pandas / NumPy
* Matplotlib / Seaborn

---

## 📁 Project Structure (Example)

```
project/
│── data/
│── preprocessing/
│── models/
│── training/
│── evaluation/
│── notebooks/
│── README.md
```

---

## ▶️ How to Run

1. Install dependencies:

```
pip install torch torchvision torchaudio
pip install torch-geometric
pip install pandas numpy scikit-learn matplotlib seaborn
```

2. Prepare dataset path

3. Run preprocessing and training notebooks/scripts

4. Tune threshold using validation set

5. Evaluate on test data

---

## 📌 Research Contributions

* Hybrid GNN-LSTM insider threat detection architecture
* Two-step classification for imbalance mitigation
* Priority-based sequence labeling
* Threshold optimization for rare class detection
* Improved sabotage detection sensitivity

---

## 👤 Author

**Saran Vignesh P R**

---

## 📜 License

This project is intended for academic and research purposes.

---

## ⭐ Acknowledgement

CERT Insider Threat Dataset provided by:

Carnegie Mellon University (CMU) & ExactData LLC

---
