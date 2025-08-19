# SWIFT-Model-of-Eye-Movements

This project implements a simplified version of the SWIFT model (Engbert & Rabe, 2024) to study how people process written language through eye-tracking data.

In reading research, eye-tracking provides crucial information about how readers decide when to move their eyes and where to look next. These decisions depend both on:
Cognitive states of the reader
Text properties such as word frequency, predictability, and sentence structure
Modeling these dynamics statistically is challenging due to the complexity and variability of eye movements.

Goal

The SWIFT model is a dynamic generative model of eye movement control during reading. It simulates how a reader’s gaze shifts across a sentence as they process its content. The model incorporates:

Fixation duration – how long the eye stays on a word
Saccades – eye movements to the next word
Because the full SWIFT model is computationally intensive and has an intractable likelihood, this project uses a simplified SWIFT model with BayesFlow for Bayesian parameter inference.

Project Tasks

Implement the simplified SWIFT model in BayesFlow
Use real eye-tracking data from a controlled reading experiment
Estimate parameters related to gaze control and reading dynamics
Investigate how well the model captures:
Observed fixation durations
Saccade patterns and regressions

Features

* **Automatic data preprocessing**

  * Schema normalization for fixation data
  * Corpus merging for word properties (frequency, predictability, word length)
  * Missing value imputation (fixation durations, regressions, jumps)

* **Flexible inference methods**

  * BayesFlow (v1/v2 APIs)
  * Approximate Bayesian Computation (ABC) fallback

* **Simulation & diagnostics**

  * SWIFT-inspired fixation simulator
  * Posterior distribution plots
  * Posterior predictive checks (PPC)
  * ECDF comparisons between observed and simulated fixations
  * Data quality plots (histograms, scatterplots)

---

## 📂 Repository Structure

```
.
├── sbi_version_5.ipynb   # Main Jupyter notebook
├── sbi_version_5.py      # Colab-exported script
├── README.md             # Project documentation
└── swift_outputs/        # Auto-generated figures and posterior plots
```

---

## 🔧 Data Requirements

Source Data

This project uses eye-tracking data from natural reading experiments, combining multiple sources:

**CopCo – Copenhagen Corpus of Natural Reading (Danish)**

Eye-tracking recordings from natural reading of Danish texts
1,832 sentences (34,897 tokens)
Gaze data from 22 participants
Contains fixation durations, saccades, and gaze behavior in natural text reading
Ideal for reading research and statistical modeling of eye-movement control
🔗 CopCo Corpus (ArXiv Reference)
Size: < 300 MB

**Controlled Reading Experiment Dataset**
Fixation sequences for an individual participant
OSF Dataset – Fixation sequences

**Corpus File (Word Properties)**
Word-level features: length, frequency, predictability
OSF Corpus File

Export
Final dataset saved as: swift_model_enhanced.csv
Ensures compatibility with the BayesFlow SWIFT inference pipeline

Suitability

The final dataset contains:
Observed fixation durations
Saccade behavior (forward jumps, regressions)
Word-level predictors (length, frequency, predictability)
This makes it well-suited for Bayesian parameter inference of the SWIFT model, enabling the estimation of parameters related to gaze control and reading dynamics.


The fixation dataset should be a **CSV file** with (at minimum) the following columns:
swift_model_enhanced.csv

Column Name	                 Description
sentence_id	                 Sentence index (grouping fixations by sentence)
word_index	                  Word position within a sentence
word	                        The actual word/token
fix_dur_ms	                  Fixation duration in milliseconds
forward_jump_size	           Saccade length (distance moved to next fixation, negative = regression)
is_regression               	Binary indicator of regression saccade (1 = regression, 0 = forward)
word_length	                 Number of characters in the word
log10_word_frequency	        Log10 frequency of the word (from corpus or proxy distribution)
predictability	              Predictability (from corpus or logistic proxy of frequency/length/position)
prev_fix_dur_ms	             Previous fixation duration (shifted or imputed if missing)


## ⚡ Quick Start Guide

### Run on Google Colab

1. Open [Google Colab](https://colab.research.google.com)
2. Create a new notebook
3. Upload this repository’s notebook/script

```python
from google.colab import files
uploaded = files.upload()   # upload fixation CSV (swift_model.csv)
```

4. Run all cells

   ```bash
   Runtime > Run all
   ```

5. Results (plots, enhanced CSV, posterior samples) are saved in:

   ```
   /content/swift_outputs/
   ```

---

## 📊 Outputs

* Enhanced fixation dataset (`swift_model_enhanced.csv`)
* Histograms of fixation durations
* Scatterplots (duration vs. word length, frequency, predictability)
* Posterior distributions of 10 SWIFT parameters
* Posterior Predictive Check (PPC) plots
* ECDF plots (observed vs. simulated fixations)

---

## 🔬 SWIFT Model Parameters

The Bayesian inference estimates the following 10 parameters:

1. **base\_logdur** – baseline log fixation duration
2. **beta\_freq** – frequency effect
3. **beta\_wlen** – word length effect
4. **beta\_pred** – predictability effect
5. **extra\_sd** – noise in fixation durations
6. **sac\_base** – baseline saccade size
7. **sac\_wlen** – effect of word length on saccade size
8. **sac\_sd** – noise in saccades
9. **p\_reg** – base regression probability
10. **reg\_scale** – regression probability scaling

---

## 📦 Installation

Dependencies (automatically installed in Colab):

* Python ≥ 3.8
* NumPy, Pandas, Matplotlib
* BayesFlow (`pip install bayesflow`)
* Torch (for BayesFlow v2)

Install manually if running locally:

```bash
pip install -r requirements.txt
```

---

## 📜 Citation

If you use this code in your research, please cite the original **SWIFT model** and **BayesFlow**:

* Engbert, R., Nuthmann, A., Richter, E. M., & Kliegl, R. (2005). *SWIFT: A dynamical model of saccade generation during reading.* Psychological Review, 112(4), 777.
* Radev, S. T., Mertens, U. K., Voss, A., Ardizzone, L., & Köthe, U. (2020). *BayesFlow: Learning complex stochastic models with invertible neural networks.* IEEE Transactions on Neural Networks and Learning Systems.

---

## 📌 License

MIT License – free to use, modify, and distribute.

---

