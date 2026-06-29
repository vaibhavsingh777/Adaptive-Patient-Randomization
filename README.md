# Adaptive Patient Randomization via Graph-Coloring Heuristics

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Dependencies](https://img.shields.io/badge/Dependencies-NumPy%20%7C%20Pandas%20%7C%20Scikit--Learn-lightgrey)
![Domain](https://img.shields.io/badge/Domain-Healthcare%20Informatics%20%7C%20Clinical%20Trials-success)

## 📌 Overview
This repository contains a robust, explainable algorithmic framework for **Covariate-Adaptive Randomization (CAR)** in clinical trials. 

While deep learning approaches (like GNNs) excel at pattern recognition, they introduce "black box" mechanics that are incompatible with the strict mathematical transparency required by regulatory bodies (e.g., the FDA). Instead, this project models patient assignment as a **stochastic graph-coloring problem**, utilizing deterministic constraint-based heuristics to minimize terminal cohort imbalance across 10+ clinical covariates.

This approach successfully bridges historical biostatistics (Pocock-Simon Minimization) with modern computational optimization, effectively balancing highly variable cohorts while maintaining the strict randomization unpredictability required to prevent selection bias.

## 🚀 The 7-Day Implementation Roadmap

This project was architected and executed over a focused 7-day sprint:

### **Phase 1: Biostatistical Foundations (Days 1–2)**
* **Literature Review:** Studied foundational literature, specifically *Pocock & Simon (1975)* on sequential treatment assignment and minimization techniques.
* **Algorithmic Translation:** Mapped classical tabular "marginal imbalance scores" into a continuous graph format, defining patients as nodes and clinical similarity as weighted edges.

### **Phase 2: The Heuristic Engine (Days 3–4)**
* **Distance Metrics:** Implemented an RBF (Gaussian) Kernel distance function to calculate precise multidimensional similarity between incoming patients and previously assigned cohorts.
* **Graph-Coloring Cost Function:** Engineered a dynamic cost-minimization algorithm that penalizes the grouping of highly similar patients into the same trial arm.

### **Phase 3: Dropout-Aware Constraints (Days 5–6)**
* **Attrition Modeling:** Integrated a probability matrix for patient dropout based on severe disease progression and non-compliance markers.
* **Weight Discounting:** Modified the core heuristic to dynamically discount the influence of high-attrition-risk patients by 50%, preventing the algorithm from over-balancing against "ghost" data points.

### **Phase 4: Simulation & Benchmarking (Day 7)**
* **Monte Carlo Execution:** Ran extensive simulations on synthetic UGDP (University Group Diabetes Program) data arrays.
* **Validation:** Extracted terminal Euclidean distance metrics between the mean feature vectors of the Treatment and Control groups, proving a >30% reduction in cohort imbalance compared to simple randomization.

## ⚙️ Core Methodology

### 1. The Cost Function (Explainable AI)
Instead of backpropagation, the algorithm uses an explicit cost function. If a new patient is highly similar to patients already assigned to Group A, the "cost" of assigning them to Group A increases proportionally to their RBF Kernel similarity.

### 2. Stochastic Compliance (`p_optimal`)
Purely deterministic algorithms are rejected in clinical trials because investigators could guess the next assignment, introducing selection bias. This algorithm features a `p_optimal` parameter (set to 0.85). The engine calculates the mathematically optimal group, but only assigns the patient to that group 85% of the time. The remaining 15% is a random assignment, satisfying regulatory demands for unpredictability.

## 💻 Installation & Usage

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/yourusername/adaptive-patient-randomization.git](https://github.com/yourusername/adaptive-patient-randomization.git)
   cd adaptive-patient-randomization
