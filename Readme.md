# 🚀 DCGAN Face Generation

This project implements **Generative Adversarial Networks (GANs)** to generate human face images.  
It includes both a **Simple GAN** and a **Deep Convolutional GAN (DCGAN)** built from scratch using PyTorch.

The goal of this project was to **deeply understand GANs**, their training dynamics, and how architectural choices affect output quality.

---

# 📌 Project Overview

Generative Adversarial Networks consist of two models:

- **Generator (G)** → Generates fake images from random noise  
- **Discriminator (D)** → Distinguishes between real and fake images  

They are trained together in a **minimax game**:
- Generator tries to **fool the Discriminator**
- Discriminator tries to **correctly classify real vs fake**

---

# 🧠 Architectures Implemented

## 🔹 1. Simple GAN

A fully connected GAN to understand the basics.

### Generator
- Input: 100-dimensional noise vector
- Fully connected layers → image

### Discriminator
- Fully connected layers → binary output (real/fake)

📌 Purpose:
> To build intuition before moving to convolution-based GANs

---

## 🔹 2. DCGAN (Deep Convolutional GAN)

A convolution-based GAN for generating higher quality images.

---

## 🎨 Generator Architecture

- Input: Noise vector (100)
- Dense layer → reshape → (128, 8, 8)
- ConvTranspose layers:
  - 8×8×128 → 16×16×128
  - 16×16×128 → 32×32×128
  - 32×32×128 → 64×64×64
- Final Conv layer → 64×64×3
- Activation: `Tanh`

---

## 🧠 Discriminator Architecture

- Input: 64×64×3 image
- Conv layers:
  - 64×64×3 → 32×32×64
  - 32×32×64 → 16×16×128
  - 16×16×128 → 8×8×256
- Flatten → Dense → 1
- Activation: `Sigmoid`

---

# 🖼️ Architecture Diagram

<!-- ADD YOUR DCGAN DIAGRAM HERE -->

---

# 📊 Dataset

- Dataset: Custom face dataset
- Total images: **~1200**
- Preprocessing:
  - Resized to **64×64**
  - Normalized to **[-1, 1]**
  - Random horizontal flipping (augmentation)

---

## 🖼️ Sample Dataset Images

<!-- ADD SAMPLE DATASET IMAGES HERE -->

---

# ⚙️ Training Details

- Framework: **PyTorch**
- Optimizer: `Adam`
  - Learning rate: `0.0002`
  - Betas: `(0.5, 0.999)`
- Loss: `Binary Cross Entropy (BCELoss)`
- Batch size: `32`
- Noise dimension: `100`

---

## ⏱️ Training

- Total epochs trained: **50 epochs**
- Device: GPU (Kaggle)

---

# 📈 Results

After training for 50 epochs:

- Model successfully learns:
  - Facial structure
  - Skin tones
  - Basic features (eyes, nose, etc.)

- Limitations:
  - Blurry outputs
  - Some distortions
  - Limited diversity (due to dataset size)

---

## 🖼️ Generated Outputs

<!-- ADD GENERATED OUTPUT IMAGES HERE -->

---

# 🧠 Observations

- GAN training is **unstable and sensitive**
- Generator improves gradually:
  - Early → noise
  - Mid → blurry faces
  - Later → structured faces
- Dataset size significantly impacts quality
- Architectural improvements (BatchNorm, deeper layers) improve results

---

# 🚀 How to Run

```bash
# Clone repo
git clone <your-repo-link>

# Install dependencies
pip install torch torchvision matplotlib tqdm