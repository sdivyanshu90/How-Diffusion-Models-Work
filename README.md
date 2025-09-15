# How Diffusion Models Work

> A learning companion for the course **"How Diffusion Models Work"** by [DeepLearning.AI](https://www.deeplearning.ai/) and instructor **Sharon Zhou**.
>
> This README is a structured walkthrough of the main concepts covered in the course, designed for students and learners who want to dive deep into diffusion models and their underlying mechanics.

---

## 🧠 Introduction

Diffusion models are a family of generative models that have rapidly advanced the field of AI-generated media, powering tools like **Stable Diffusion, DALL·E 2, and Imagen**.

At their core, diffusion models learn to **reverse a gradual noising process**:

1. Take real data (e.g., an image).
2. Add noise step by step until it becomes pure noise.
3. Train a neural network to learn the *reverse process*—removing noise step by step until you reconstruct the original distribution.

One of the most well-known implementations is **DDPM (Denoising Diffusion Probabilistic Models)**, which this course explores.

---

## 1. ✨ Intuition

The intuition behind diffusion models comes from **forward and reverse diffusion processes**:

* **Forward Process (Adding Noise)**

  * Start with an image.
  * Add a small amount of Gaussian noise repeatedly over many steps.
  * Eventually, the image turns into pure white noise.
  * This process is fixed, not learned.

* **Reverse Process (Removing Noise)**

  * Train a neural network to predict the noise that was added at each step.
  * By subtracting the predicted noise, you get a cleaner image at each stage.
  * Repeated many times, noise turns back into a meaningful image.

🔑 **Key Idea**: If a model can **denoise** well, it can **generate new data** from noise by reversing the process.

---

## 2. 🎲 Sampling

Sampling in diffusion models refers to the **reverse generation process**: turning noise into data.

* **DDPM Sampling Steps**:

  1. Start with random Gaussian noise.
  2. At each step, use the trained neural network to predict the noise component.
  3. Subtract the noise → get a slightly cleaner image.
  4. Repeat until a final realistic image emerges.

* **Challenge**:

  * Typically requires **hundreds or thousands of steps** for high-quality results.
  * Slow, but yields very sharp and realistic samples.

📌 Example: Generating a face image → begin with static noise → gradually refine → end up with a clear human face.

---

## 3. 🕸️ Neural Network

The **neural network architecture** is the engine of diffusion models:

* Usually a **U-Net** (encoder–decoder with skip connections).
* Input: a noisy image + timestep information.
* Output: predicted noise at that timestep.

### Why U-Net?

* Encoder compresses the image → captures global context.
* Decoder reconstructs details → captures local textures.
* Skip connections preserve spatial details lost in compression.

### Conditioning (Optional but Powerful)

* Text, class labels, or other modalities can be added.
* Example: Text-to-image generation uses embeddings from models like CLIP or transformers.

---

## 4. 🏋️ Training

Training a diffusion model means teaching it to **predict the noise added at each step**.

1. Take an image from the dataset.
2. Pick a random timestep `t`.
3. Add Gaussian noise to the image according to the forward diffusion schedule.
4. Feed the noisy image + timestep into the neural network.
5. Train the network to output the exact noise that was added.

🔑 **Loss Function**:
Usually a simple **Mean Squared Error (MSE)** between the predicted noise and the true noise.

### Why This Works

If the model can predict noise accurately at any step, it can reverse the process for sampling.

---

## 5. ⚡ Controlling & Speeding Up

Diffusion models are powerful but **computationally expensive**. Researchers have developed methods to make them faster and more controllable:

### 🔹 Speeding Up Sampling

* **Fewer Steps**: Use techniques like DDIM (Denoising Diffusion Implicit Models) to cut down steps while maintaining quality.
* **Noise Schedules**: Modify how noise is added/removed for more efficient denoising.

### 🔹 Controlling the Generation

* **Classifier Guidance**: Steer generation towards a target class by using gradients from a classifier.
* **Classifier-Free Guidance**: Train the model to condition and uncondition on prompts; combine them at inference for stronger control.
* **Prompt Engineering**: In text-to-image systems, the quality of the description directly influences the final output.

---

## 6. 📌 Key Takeaways

* Diffusion models work by learning to **denoise data step by step**.
* **DDPM** provides the foundation: forward noise process + reverse learned denoising.
* **Sampling** is slow but high-quality, with improvements like DDIM speeding it up.
* **U-Net architectures** power most diffusion models, often conditioned on text or labels.
* **Control techniques** (guidance, schedules) give flexibility and efficiency.

---

## 🙏 Acknowledgments

This README is inspired by the course **[How Diffusion Models Work](https://www.deeplearning.ai/short-courses/how-diffusion-models-work/)** by **DeepLearning.AI** and instructor **Sharon Zhou**.

All credit for the original course content goes to them. This document is a **learner’s structured summary** for study and review purposes.
