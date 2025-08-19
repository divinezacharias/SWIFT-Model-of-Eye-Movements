# SWIFT-Model-of-Eye-Movements

This repository provides a Python script to perform Bayesian parameter inference for the SWIFT eye-tracking model using fixation data.
It leverages BayesFlow (v1/v2) and Approximate Bayesian Computation (ABC) for inference and includes **diagnostic visualizations and posterior predictive checks.

---

## 🚀 Features

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

The fixation dataset should be a **CSV file** with (at minimum) the following columns:
swift_model_enhanced.csv

* `sentence_id` 
* `word_index` 
* `fix_dur_ms` 
* `word_length`
* `log10_word_frequency`
* `predictability`
* `forward_jump_size`
* `is_regression`
* `prev_fix_dur_ms`


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

