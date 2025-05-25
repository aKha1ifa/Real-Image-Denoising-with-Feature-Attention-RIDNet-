# MiniRIDNet: Lightweight Denoising Network with Attention (Inspired by RIDNet)

A PyTorch-based reimplementation of key ideas from the ICCV 2019 paper:  
**"Real Image Denoising with Feature Attention"** by Saeed Anwar and Nick Barnes.

This project demonstrates a simplified version of RIDNet using:
- Dilated convolutions
- Residual learning
- Channel attention

Trained and tested on:
- **MNIST** (grayscale)
- **CIFAR-10** (color)
- A manually tested **real-world noisy photo**

---

## 📌 Key Design Choices

| Component         | Choice / Value                              |
|------------------|----------------------------------------------|
| Architecture     | 1 input conv → 4 EAM blocks → 1 output conv   |
| EAM Details      | Dilated 3×3 convs (d=2,3), residual block, SE attention |
| Channel Attention| SE-style (avg pool → 1×1 convs → sigmoid)     |
| Residual Learning| Global residual (input + output)              |
| Input Resolution | 28×28 (MNIST), 32×32 (CIFAR-10)               |
| Noise Type       | Gaussian (σ=0.5 for MNIST, σ=0.1 for CIFAR-10)|
| Loss Function    | L1 loss                                       |
| Optimizer        | Adam (lr = 1e-3)                              |
| Batch Size       | 64                                            |
| Epochs           | 5                                             |
| Evaluation       | PSNR, SSIM                                    |

---

## 📈 Results

### MNIST (Grayscale)
| Metric | Value     |
|--------|-----------|
| PSNR   | 31.42 dB  |
| SSIM   | 0.9723    |

### CIFAR-10 (Color)
| Metric | Value     |
|--------|-----------|
| PSNR   | 33.01 dB  |
| SSIM   | 0.9676    |

### Real Noisy Photo
- Qualitatively reduced noise
- Preserved texture edges
- Did not fully clean complex artifacts (e.g. blur or color shifts)

> ⚠️ Note: Trained only on synthetic noise — not expected to match real dataset benchmarks.

---

## 🖼️ Sample Outputs

![image](https://github.com/user-attachments/assets/e7896c69-2c2d-48a5-ba8b-9908a4fc79f0)


---

## 🔬 Comparison with RIDNet Paper

| Aspect                 | Original RIDNet Paper                        | This Implementation               |
|------------------------|-----------------------------------------------|-----------------------------------|
| Model Depth            | Deep residual-on-residual with EAMs          | 4 EAM blocks only                 |
| Attention              | Feature attention (complex gating)           | SE-style channel attention        |
| Skip Connections       | Local + short + long skips                   | Local + global skip only          |
| Training Data          | Real + synthetic datasets (e.g., SIDD, DND)  | Only synthetic (MNIST, CIFAR-10)  |
| Resolution             | High-res natural photos                      | 28×28 (MNIST), 32×32 (CIFAR-10)   |
| Best PSNR (paper)      | ~39.2 dB on DND real-noise                   | 33.01 dB (CIFAR-10)               |

---
