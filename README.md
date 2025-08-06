# Denoising CSI in 5G RAN Using Generative Adversarial Networks (GANs)

## Overview

This project enhances **Channel State Information (CSI)** in 5G Radio Access Networks (RAN) using a **Denoising Generative Adversarial Network (DGAN)** trained on filtered data from the **RadioML 2018.01 dataset**.

### Why CSI Denoising?

CSI is essential for **beamforming, link adaptation, and resource allocation** in 5G networks. However, **environmental noise, interference, and multipath fading** corrupt CSI measurements, leading to degraded network performance. Our GAN-based solution effectively **removes noise and reconstructs clean CSI**, ensuring **better reliability and communication quality**.

---

## Features

* CSI denoising using **GANs**
* 5G-specific modulation filtering from RadioML dataset
* Balanced dataset: **250k samples** from BPSK, QPSK, QAM16, QAM64, 8PSK
* Evaluation Metrics: **MSE, PSNR, SSIM**
* Visualization of **Noisy vs. Denoised CSI**
* **PyTorch** implementation

---

## Methodology

### 1. Data Preparation

#### CSI Dataset Generation:

* Loaded modulation data from **RadioML 2018.01**
* Selected **5G-relevant modulations**: `BPSK`, `QPSK`, `QAM16`, `QAM64`, `8PSK`
* Created a **balanced dataset** with 250,000 samples (50k per class)
* Added **Gaussian noise** to emulate real-world interference
* Saved in `.h5` format with keys: `X` (IQ samples), `Y` (labels), `Z` (SNR)

### 2. Model Architecture

* **Generator (G):** Learns to produce clean CSI from noisy input
* **Discriminator (D):** Distinguishes real vs. denoised CSI

#### Loss Function:

* **Binary Cross-Entropy (BCE) Loss** for adversarial learning
* **Mean Squared Error (MSE)** for accurate reconstruction

### 3. Training Process

* Trained using **adversarial learning** with PyTorch
* Alternating training of G and D
* Used **Adam optimizer** and monitored loss convergence

### 4. Evaluation & Results

* Quantitative metrics: **MSE**, **PSNR**, **SSIM**
* Visual comparison between **Noisy, Clean, and Denoised CSI**

---

## Results & Visualization

### Evaluation Metrics

| Metric | Value    |
| ------ | -------- |
| MSE    | 0.0084   |
| PSNR   | 20.75 dB |
| SSIM   | 0.85     |

### Sample Visualization

Noisy CSI vs. Denoised CSI (Using GANs):

![DGAN Denoising on CSI Data](Screenshot%202025-03-24%20231736.png)

---

## Conclusion

The proposed **DGAN architecture** has shown strong performance in denoising CSI data tailored for 5G applications. With a **low MSE (0.0084)** and a **high SSIM (0.85)**, the model successfully reconstructs high-quality CSI signals from noisy inputs. The **PSNR value of 20.75 dB** further confirms that the generated CSI signals closely resemble the clean ground truth.

These results demonstrate that adversarial training effectively preserves both signal structure and quality, making the approach suitable for real-time RAN applications where accurate CSI is critical. The success of this method on filtered RadioML data opens avenues for:

* Generalization to real-world CSI datasets (e.g., captured using USRPs),
* Extension to multi-antenna (MIMO) settings,
* Integration with link adaptation and scheduling algorithms in 5G networks.

