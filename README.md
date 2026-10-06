# KAN vs MLP for Tabular Data: Pruning and Interpretability

This repository contains experiments comparing **KAN- and MLP-based architectures for tabular data**, with a focus on:

* pruning under a **matched parameter budget**;
* predictive performance;
* model interpretability.

The work is based on the TabKANet architecture proposed in:

> https://www.sciencedirect.com/science/article/pii/S0950705125017368

and the original implementation:

https://github.com/AI-thpremed/TabKANet

---

## 1. Pruning experiment

The pruning experiment uses a modified version of **TabKANet**.

The main modification is the ability to choose the type of Transformer block:

```text
TabKANet
   │
   ├── KAN Transformer
   │
   └── MLP Transformer
```

The KAN and MLP variants are compared using the **same number of trainable parameters**, allowing the comparison to focus on the architecture rather than model size.

Four pruning strategies are evaluated:

| Pruning              |
| -------------------- |
| KAN basis pruning    |
| KAN neuron pruning   |
| Structured pruning   |
| Unstructured pruning |

After pruning, models are fine-tuned and evaluated using 5-fold cross-validation.

The main pruning ratio used in the experiments is **20%**.

### Results

Across the evaluated binary classification, multiclass classification and regression datasets, moderate pruning generally preserves a large fraction of the original performance.

The effect of pruning is dataset-dependent: no single pruning strategy consistently dominates across all tasks. In several cases, fine-tuning after pruning recovers the original performance or even produces a small improvement.

---

## 2. Quality and interpretability

A separate set of experiments studies models designed specifically for **feature-level interpretation**.

These models are architecturally different from the original TabKANet used in the pruning experiment.

Four variants are considered:

```text
KAN additive
MLP additive

KAN Transformer
MLP Transformer
```

In addition, a separate **V2 architecture** is evaluated:

```text
Interpretable V2
```
---

## 3. Interpretability

The interpretability experiments use several complementary approaches:

### KAN functions

For KAN-based models, the learned univariate functions can be extracted directly from the KAN layers.

### Main effects

Feature-level effects are computed for both continuous and categorical features.

### SHAP

SHAP values are used to obtain global feature importance and feature–prediction relationships.

---

## 4. Datasets

Experiments are performed on seven tabular datasets:

* Bank Marketing
* Online Shoppers
* Multi-Segmentation
* Forest Cover Type
* California Housing
* CPU Small
* SARCOS

Both classification and regression tasks are included.

---

## 5. Repository contents

`pruning_experiment.ipynb` contains the matched-parameter KAN/MLP pruning experiments.

`qi_experiment.ipynb` contains the quality and interpretability experiments.

---

## 6. Reference

This project builds on **TabKANet**:

> Weihao Gao, Zheng Gong, Zhuo Deng, Lan Ma 
> *Revisiting the numerical feature embeddings structure in neural network-based tabular modelling*
> arXiv:2409.08806, 2024.

Paper: https://www.sciencedirect.com/science/article/pii/S0950705125017368

Original implementation: https://github.com/AI-thpremed/TabKANet
