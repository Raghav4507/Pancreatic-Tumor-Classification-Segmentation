# Pancreatic Cancer Detection Using EfficientNet and U-Net  


This project focuses on automating pancreatic cancer detection from CT scan images using deep learning. The pipeline integrates **binary classification** using EfficientNet and **weakly supervised tumor segmentation** using U-Net trained on Grad-CAM–based pseudo labels.

---

## 🔍 Project Objective
Pancreatic cancer is difficult to detect early due to low-contrast tumor regions and the absence of pixel-level annotations.  
This project aims to:

1. **Classify CT images** as *Normal* or *Tumor* using EfficientNetB0.  
2. **Segment tumor regions** using U-Net trained on pseudo masks generated from Grad-CAM heatmaps.  
3. Provide interpretable visual outputs that highlight regions of interest for medical relevance.

---

## 📁 Dataset
- Source: Kaggle – *Pancreatic CT Images*  
- Two classes:  
  - `normal`  
  - `pancreatic_tumor`
- Train set: 421 normal, 578 tumor  
- Test set: 225 normal, 187 tumor  
- Images resized to **128×128**  
- No segmentation masks provided → pseudo masks generated automatically

---

## 🧠 Models Used

### **1. EfficientNetB0 (Classification)**
- Pretrained on ImageNet  
- Fine-tuned on CT dataset  
- Output:  
  - **0 = Normal**  
  - **1 = Tumor**  
- Achieved classification accuracy: **~97%**

### **2. U-Net (Segmentation)**
- Encoder–decoder architecture for pixel-level prediction  
- Trained using generated pseudo masks  
- Loss function: **Binary Cross Entropy + Dice Loss**  
- Achieved segmentation accuracy: **~93%**

---

## 🖼 Key Techniques

### **ROI Extraction with Laplacian**
- Laplacian edge detection used to highlight tumor boundaries  
- ROI cropped and resized to improve focus and model performance

### **Grad-CAM Heatmaps**
- Highlight the regions used by EfficientNet during prediction  
- Heatmaps thresholded to generate pseudo masks  
- Masks refined using morphological operations

### **CRF Post-Processing**
- Conditional Random Field used to clean U-Net outputs  
- Produces sharper and more consistent tumor boundaries

---

## 📊 Results Summary
- **Classification Accuracy:** ~97%  
- **Segmentation Accuracy:** ~93%  
- Visual overlays demonstrate clear detection of tumor areas  
- Effective weakly supervised approach despite lack of ground-truth labels

---

## 🚀 Pipeline Overview
1. Load and preprocess CT images  
2. Apply ROI extraction using Laplacian  
3. Train EfficientNet for classification  
4. Generate Grad-CAM heatmaps → pseudo masks  
5. Train U-Net using pseudo masks  
6. Apply CRF refinement  
7. Visualize and evaluate segmentation boundaries

---

## 🛠 Tools & Technologies
- Python
- TensorFlow / Keras
- EfficientNetB0
- U-Net
- OpenCV
- NumPy, Matplotlib
- CRF (pydensecrf)

---

## 📌 Conclusion
This project demonstrates a complete end-to-end system for pancreatic cancer detection and localization using deep learning. By combining classification, Grad-CAM visualization, pseudo-mask generation, and segmentation, the model provides an interpretable and effective diagnostic aid — even in the absence of manual segmentation labels.

