# Enhanced Brain Tumor Segmentation (Modified Half ResNet-50)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Colab](https://img.shields.io/badge/Google%20Colab-ready-orange)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)

**Repository:** `BrainTumorSegmentation`  
**Author:** Satnam Singh Ramavath  
**Contact:** satnamsinghramavath9320@gmail.com  
**GitHub:** https://github.com/satnamsinghr

---

## Project summary (one-liner)
A compact, efficient segmentation pipeline using a **Modified Half ResNet-50 encoder** + U-Net-style decoder to segment and classify brain tumors on MRI scans — optimized for Colab GPU runs and reproducible experiments.

---

## Motivation
Medical image segmentation is crucial for assisting radiologists and improving diagnosis/therapy planning. This project implements a lighter-weight ResNet-based encoder (reduced parameters / “half” design) combined with a decoder inspired by U-Net, focused on delivering accurate masks with reduced training time and lower memory footprint — practical for researchers and students using Colab or limited hardware.

---

## What’s in this repo
- `notebooks/BrainTumorSegmentation.ipynb` — main Colab notebook: data prep, augmentation, model, training, evaluation, visualization.  
- `papers/brain_tumor_paper.pdf` — the project report.  
- `requirements.txt` — packages and versions to reproduce experiments.  
- `screenshots/` — (add) sample masks, training curves, confusion matrix.  
- `README.md` — this document.

---

## High-level pipeline
1. **Data ingestion** — read MRI scans, labels (masks / class labels).  
2. **Preprocessing** — resize, normalize, augmentation (flip, rotate, brightness, elastic).  
3. **Model** — Modified Half ResNet-50 as encoder (lighter ResNet variant) + decoder inspired by U-Net for pixelwise segmentation.  
4. **Loss** — combination (e.g., Dice loss + categorical cross-entropy) to balance region overlap and class accuracy.  
5. **Training** — Adam optimizer, learning-rate schedule, early stopping, checkpointing.  
6. **Evaluation** — Dice coefficient, IoU, precision, recall, and visual inspection of predicted masks.

> **Note:** Exact hyperparameters, layer details and training settings are documented inside the notebook. Open the notebook to see the precise configs used.

---

## Dataset
This work uses a public Brain MRI tumor dataset (commonly available via Kaggle / academic sources).  
**Important:** Do **not** upload raw/full datasets or large model weights to GitHub. The notebook includes Kaggle / Drive download snippets so you can pull the dataset at runtime.

**Quick dataset download options (used in notebook):**
```python
# Option A: Kaggle (recommended)
!pip install -q kaggle
# Upload kaggle.json to Colab, then:
!kaggle datasets download -d <dataset-id> -p /content/data --unzip

# Option B: Google Drive (if you shared data to your Drive)
from google.colab import drive
drive.mount('/content/drive')
# copy or unzip files from Drive to /content/data

## How to run (recommended: Google Colab)

Click the Open in Colab badge (or open notebooks/BrainTumorSegmentation.ipynb in Colab).

Runtime → Change runtime type → GPU.

Run cells in order; first cells install dependencies and download dataset (Kaggle/Drive).

Train or run inference cells; results (predicted masks and metrics) are saved to the Colab session or Drive.

Local run (optional)

Clone the repo:

git clone https://github.com/satnamsinghr/BrainTumorSegmentation.git
cd BrainTumorSegmentation


Create virtual env and install:

python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows
pip install -r requirements.txt


## Launch the notebook locally:

jupyter notebook notebooks/BrainTumorSegmentation.ipynb

Evaluation & expected outputs

Metrics: Dice coefficient (per class), IoU, Precision, Recall, overall accuracy.

Visual outputs: predicted segmentation masks overlayed on MRIs, sample failure cases, loss/accuracy curves.

Save your best model weights and example outputs to Google Drive for sharing.

Recommended experiments / ablation ideas

Compare full ResNet-50 vs Modified Half ResNet-50 performance / speed.

Try different loss mixes: Dice-only vs Dice + CE.

Test additional augmentations (elastic, grid distortion).

Quantize / prune model for edge deployment.

 

## File / folder structure (recommended)
BrainTumorSegmentation/
├── notebooks/
│   └── BrainTumorSegmentation.ipynb
├── papers/
│   └── brain_tumor_paper.pdf
├── screenshots/
│   ├── training_curve.png
│   └── predicted_mask_01.png
├── requirements.txt
└── README.md

## Reproducibility checklist

 Set Colab runtime to GPU.

 Provide kaggle.json in Colab when using Kaggle API (do not push kaggle.json to repo).

 Set random seeds (already in notebook) for reproducible training.

 Save best model checkpoints to Drive.

## Future work

Add a minimal Flask/FastAPI wrapper for inference and demo (small web app).

Containerize (Dockerfile) for reproducible environment.

Create a small test suite / evaluation script.

## Acknowledgements & references

Project report attached in papers/brain_tumor_paper.pdf.

Datasets and code patterns inspired by public MRI tumor segmentation works and U-Net / ResNet literature.

## Author & contact

Satnam Singh Ramavath

Email: satnamsinghramavath9320@gmail.com

GitHub: https://github.com/satnamsinghr
