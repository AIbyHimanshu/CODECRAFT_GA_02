# CODECRAFT_GA_02 — Image Generation with Pre-trained Models (Model Comparison)

This repository contains my solution for **Task 02: Image Generation with Pre-trained Models**, where I generate images from text prompts using two different **pre-trained Stable Diffusion pipelines**, and compare them using:

- **Qualitative results** (side-by-side image outputs)
- **Quantitative metric**: **CLIP prompt–image similarity**
- **Efficiency metric**: **Runtime per prompt**
- A summary **comparison chart**

---

## Models Used

### **Model A — Stable Diffusion v1.5 (Diffusers / PyTorch)**
- Checkpoint: `runwayml/stable-diffusion-v1-5`
- Resolution used: **512px**
- Generated **2 images per prompt**

### **Model B — Stable Diffusion v2.1 (Diffusers / PyTorch)**
- Checkpoint: `stabilityai/stable-diffusion-2-1` (or equivalent SD v2.1 pipeline used in the notebook)
- Resolution used: **768px**
- Generated **2 images per prompt**

> Both models were run on **Google Colab (Tesla T4 GPU)**.

---

## Prompts Used

1. `a futuristic cyberpunk street at night, neon lights, rain, ultra-detailed, cinematic`
2. `a robot barista serving coffee in a cozy cafe, warm lighting, cinematic`
3. `a floating castle above the clouds, sunrise, epic fantasy art, highly detailed`

Total images generated: **3 prompts × 2 images × 2 models = 12 images**

---

## Results Summary (CLIP + Runtime)

| Prompt | SD v1.5 Avg CLIP | SD v1.5 Time | SD v2.1 Avg CLIP | SD v2.1 Time | Winner (CLIP) |
|------|-------------------:|------------:|------------------:|------------:|:-------------|
| P1 (Cyberpunk street) | 0.3382 | 9.5s | 0.3301 | 7.9s | SD v1.5 |
| P2 (Robot barista) | 0.3622 | 7.8s | 0.3685 | 7.8s | SD v2.1 |
| P3 (Floating castle) | 0.3500 | 7.9s | 0.3486 | 7.9s | SD v1.5 |

**Observations**
- SD v1.5 slightly wins on **P1 and P3** in prompt alignment (CLIP).
- SD v2.1 wins on **P2**, suggesting better alignment for “robot-in-cafe” composition.
- Runtime is similar overall; first run usually takes longer due to model caching.

---

## Outputs

### Generated Images
The generated outputs are stored in the output folders created by the notebook.

Example outputs included:
- `prompt1_1.png`, `prompt1_2.png`
- `prompt2_1.png`, `prompt2_2.png`
- `prompt3_1.png`, `prompt3_2.png`

### Comparison Chart
A combined chart was generated and saved as:

- `task02_comparison_chart.png`

This chart includes:
- **Prompt-image alignment (Avg CLIP score)**
- **Runtime per prompt**

---

## Project Structure

```bash
.
├── GA_02.ipynb
├── task02_comparison_chart.png
├── outputs
└── README.md
