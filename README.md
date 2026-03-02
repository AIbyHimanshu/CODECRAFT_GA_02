# CODECRAFT_GA_02 — Image Generation with Pre-trained Models (Model Comparison)

> Generate images from **text prompts** using **pretrained Stable Diffusion pipelines**, then compare the models using **CLIP prompt–image similarity** and **runtime**, implemented in **Google Colab (T4 GPU)**.

---

## Overview

This project demonstrates **text-to-image generation** using two different **pretrained diffusion models** (no training required).  
Given a text prompt, each model iteratively denoises a latent representation to synthesize a final image.

In addition to generating images, the notebook performs a **model comparison** using:

- **Qualitative analysis**: side-by-side image outputs
- **Quantitative analysis**: **CLIP** prompt–image alignment score
- **Efficiency analysis**: runtime per prompt
- A final summary chart for results

---

## Models Used

### **Model A — Stable Diffusion v1.5**
- Library: **Diffusers / PyTorch**
- Checkpoint: `runwayml/stable-diffusion-v1-5`
- Resolution: **512×512**

### **Model B — Stable Diffusion v2.1**
- Library: **Diffusers / PyTorch**
- Checkpoint: `stabilityai/stable-diffusion-2-1`
- Resolution: **768×768**

> Both models were run on **Google Colab (Tesla T4 GPU)**.

---

## How It Works

```

Text Prompt
│
├──► Model A (SD v1.5) ──► Generated Images (2 per prompt)
│
├──► Model B (SD v2.1) ──► Generated Images (2 per prompt)
│
└──► CLIP Scoring + Runtime Logging ──► Comparison Chart + Summary

```

| Component | Role |
|----------|------|
| **Text prompt** | Describes the desired scene/style |
| **Stable Diffusion** | Generates images via iterative denoising |
| **CLIP (ViT-B/32)** | Measures prompt–image alignment (higher = better match) |
| **Runtime logging** | Tracks efficiency per prompt |

---

## Prompts Used

1. `a futuristic cyberpunk street at night, neon lights, rain, ultra-detailed, cinematic`
2. `a robot barista serving coffee in a cozy cafe, warm lighting, cinematic`
3. `a floating castle above the clouds, sunrise, epic fantasy art, highly detailed`

Total outputs: **3 prompts × 2 images × 2 models = 12 images**

---

## Results Summary (CLIP + Runtime)

| Prompt | SD v1.5 Avg CLIP | SD v1.5 Time | SD v2.1 Avg CLIP | SD v2.1 Time | Winner |
|------|-------------------:|------------:|------------------:|------------:|:------|
| P1 (Cyberpunk street) | 0.3382 | 9.5s | 0.3301 | 7.9s | SD v1.5 |
| P2 (Robot barista) | 0.3622 | 7.8s | 0.3685 | 7.8s | SD v2.1 |
| P3 (Floating castle) | 0.3500 | 7.9s | 0.3486 | 7.9s | SD v1.5 |

### Observations
- **SD v1.5** performed slightly better on **P1 and P3** (higher CLIP alignment).
- **SD v2.1** performed best on **P2**, suggesting better alignment for indoor/character scenes.
- Runtime was very similar after caching; **first prompt is usually slower** due to model downloads.

---

## Project Structure

```

CODECRAFT_GA_02/
│
├── GA_02.ipynb               # Main Colab notebook
├── comparison_chart.png      # Final CLIP + runtime comparison chart
└── README.md                 # This file

```

---

## Getting Started

### Run in Google Colab

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

1. Open `GA_02.ipynb` in Google Colab  
2. Enable GPU: `Runtime → Change runtime type → T4 GPU`
3. Run all cells (`Runtime → Run all`)
4. Outputs are automatically saved as PNG images + `comparison_chart.png`

---

## Notebook Cells

| Cell | Description |
|------|------------|
| **Cell 1** | Install dependencies |
| **Cell 2** | Imports + GPU check + helper functions |
| **Cell 3** | Define prompts and output structure |
| **Cell 4** | Load **Model A (SD v1.5)** and generate images |
| **Cell 5** | Load **Model B (SD v2.1)** and generate images |
| **Cell 6** | Side-by-side visualization of generated outputs |
| **Cell 7** | Load **CLIP ViT-B/32** and compute prompt–image similarity |
| **Cell 8** | Print detailed + summary comparison tables |
| **Cell 9** | Generate + save chart (`comparison_chart.png`) |

---

## Customization

### Change number of images per prompt
Increase/decrease `num_images_per_prompt` in the generation cells.

### Speed vs quality
Adjust inference steps:

- Lower (e.g., `20`) → faster, less detail
- Higher (e.g., `35`) → sharper, slower

---

## Notes

- You may see pip dependency warnings in Colab due to preinstalled packages.  
  The notebook still runs correctly and produces outputs.
- If GitHub shows **“Invalid Notebook”**, remove widget metadata and re-upload (Colab: *Edit → Clear outputs* then download/upload again).

---

## References

- [TensorFlow tutorial (Stable Diffusion overview)](https://www.tensorflow.org/tutorials/generative/generate_images_with_stable_diffusion)
- [DALL-E Mini Image Generator: Create Digital Art with from Text Prompts](https://colab.research.google.com/github/robgon-art/e-dall-e/blob/main/DALL_E_Mini_Image_Generator.ipynb)

---
