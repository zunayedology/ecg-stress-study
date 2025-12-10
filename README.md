# ECG and Nonlinear HRV Analysis: Assessing Stress Recovery Before and After Academic Exams

**Authors:** Md Zunayedul Islam (NBP9YT), Yernur Polatbek (BIE00Y), Biswarup Mukherjee (DLPGC5)

**Program:** Erasmus Mundus Joint Master in Artificial Intelligence for Image Processing and Computer Vision (IPCV)  

**Course:** Biomedical Signal Processing (P-ITJEL-0024)

**Institution:** Pázmány Péter Catholic University (PPKE), Hungary  

---

## 📌 Project Overview
This project investigates the physiological impact of academic stress on the Autonomic Nervous System (ANS). Using a custom-built Python pipeline, we analyzed **Electrocardiogram (ECG)** signals from 12 postgraduate students recorded under two experimental conditions: **Before Exam** (Anticipatory Stress) and **After Exam** (Recovery/Rumination).

The goal was to move beyond standard Heart Rate (HR) analysis and verify if advanced **non-linear complexity metrics** (Fractal Dimension, Entropy) offer superior sensitivity in detecting cognitive load and stress recovery states.

## 🧪 The Dataset
* **Subjects:** 12 Postgraduate Students (Age: 22-26).
* **Demographics:** Diverse international cohort (Europe, South Asia, Middle East, South America).
* **Protocol:**
    * **Baseline:** 30-second single-lead ECG recorded immediately before a major exam.
    * **Stress/Recovery:** 30-second ECG recorded immediately after finishing the exam.
* **Data Format:** Raw binary (`.dat`) files with `int16` digitization ($f_s = 250$ Hz).

## ⚙️ Methodology & Pipeline

### 1. Data Extraction & Pre-processing
* **Loader:** Custom binary parser to handle raw `.dat` files and strip headers.
* **Filtering:**
    * **Bandpass:** Butterworth (5–30 Hz) to isolate QRS energy.
    * **Notch:** IIR Notch filter (50 Hz) to remove powerline interference.
* **Validation:** Signal quality checks and sampling rate correction ($f_s$ verified at 250 Hz).

### 2. R-Peak Detection
* **Algorithm:** Modified **Pan-Tompkins** implementation.
    * Differentiation $\rightarrow$ Squaring $\rightarrow$ Moving Window Integration.
    * Adaptive thresholding for peak detection.
* **Refinement:** Search-back mechanism to align detected peaks with the true signal maximum.

### 3. Feature Engineering (30+ Metrics)
We extracted features across three physiological domains:
* **Time-Domain:** Mean HR, SDNN, RMSSD (Vagal Tone), pNN50.
* **Frequency-Domain:** LF Power, HF Power, LF/HF Ratio (Sympathovagal Balance).
* **Non-Linear / Complexity (Advanced):**
    * **Sample Entropy (SampEn):** Measures signal unpredictability.
    * **Higuchi Fractal Dimension (HFD):** Measures signal roughness/complexity.
    * **Symbolic Dynamics Entropy:** Quantifies acceleration/deceleration patterns.
    * **R-Peak Amplitude Variability (RAV):** Surrogate for respiratory depth.

## 📊 Key Findings

### 1. The "Heart Rate Paradox"
Post-exam recovery was not universal. The population split into two phenotypes:
* **The Recoverers:** Heart Rate dropped ($>10$ BPM) and Vagal Tone increased (Healthy recovery).
* **The Ruminators:** Heart Rate *increased* and Vagal Tone collapsed (Sustained anxiety/arousal).

### 2. Complexity > Heart Rate
While Heart Rate changes were inconsistent ($p=0.10$), **Fractal Dimension (HFD)** proved to be a universal marker ($p=0.06$).
* **Result:** Almost all subjects showed a **loss of physiological complexity** post-exam, regardless of their heart rate.
* **Implication:** Stress makes the heart rhythm "mechanically rigid" and less adaptable.

### 3. Demographic Trends
* **Females:** Exhibited higher sensitivity (greater HR increase) than males.
* **Age Resilience:** Strong positive correlation ($r=0.54$) between **Age** and **Vagal Tone retention**, suggesting older students coped better with the stressor.
* **Regional:** "Europe" cluster showed the highest stress response, while "Middle East" was the most resilient.

## 📈 Visualizations
The project includes publication-quality visualizations generated via `matplotlib` and `seaborn`:
* **Paired Spaghetti Plots:** To visualize individual trajectories (Before vs. After).
* **Radar Charts:** For multivariate stress profiling of specific case studies.
* **Violin Plots:** To display population distribution shifts.
* **Poincaré & DFA Plots:** For non-linear dynamics analysis.

## 🚀 How to Run
1.  Clone the repository.
2.  Install dependencies: `pip install numpy pandas scipy matplotlib seaborn`
3.  Mount your dataset path (or use sample data).
4.  Run the notebook `BSP_BYZNESS.ipynb`.

## 📚 References
* Pan, J., & Tompkins, W. J. (1985). A real-time QRS detection algorithm. *IEEE Trans. Biomed. Eng*.
* Shaffer, F., & Ginsberg, J. P. (2017). An overview of heart rate variability metrics and norms. *Frontiers in Public Health*.
* Goldberger, A. L., et al. (2002). Fractal dynamics in physiology: alterations with disease and aging. *PNAS*.

---
*Project completed as part of the Biomedical Signal Processing course at PPKE, Fall 2025.*
