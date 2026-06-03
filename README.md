# FOUNDATION-MODELS-FOR-RAGA-CLASSIFICATION-
# MERT vs CultureMERT for Carnatic Raga Representation Learning

## Overview

This project compares **MERT** and **CultureMERT**, two self-supervised music representation learning models, on the task of learning meaningful representations for **Carnatic classical music**.

The objective was to investigate whether a culturally adapted model (CultureMERT) provides better embeddings for Indian classical music than a general-purpose music representation model (MERT).

The comparison was performed using the **Saraga Carnatic dataset** through embedding extraction, visualization, nearest-neighbor analysis, and supervised classification experiments.

---

## Objectives

* Study the architecture and representation learning approach of MERT and CultureMERT.
* Generate embeddings from Carnatic music recordings.
* Visualize embedding spaces using UMAP.
* Evaluate representation quality using supervised probes.
* Compare MERT and CultureMERT on Carnatic raga classification.
* Analyze the effect of dataset size and label distribution on evaluation.

---

## Models

### MERT

MERT (Music Understanding Representation Transformer) is a large-scale self-supervised music representation model trained on diverse musical audio data. It learns general-purpose musical representations without requiring manual labels.

### CultureMERT

CultureMERT extends the idea of self-supervised music representation learning by incorporating culturally specific musical knowledge during training. It is designed to better capture characteristics of non-Western musical traditions such as Indian classical music.

---

## Dataset

### Saraga Carnatic

The Saraga dataset is a collection of annotated recordings of Indian classical music.

During exploration, many recordings were found to have missing or unique raga annotations, making supervised evaluation difficult. Therefore, only ragas with at least two recordings were retained.

### Final Evaluation Subset

* **78 recordings**
* **25 ragas**
* Only ragas with at least two recordings were included

Most frequent ragas:

| Raga          | Recordings |
| ------------- | ---------- |
| Tōḍi          | 6          |
| Kamās         | 6          |
| Rāgamālika    | 6          |
| Saurāṣṭram    | 6          |
| Behāg         | 5          |
| Ṣanmukhapriya | 4          |
| Kalyāṇi       | 4          |

---

## Methodology

### 1. Embedding Extraction

For both MERT and CultureMERT:

1. Audio was loaded at 24 kHz.
2. The first 30 seconds of each recording were used.
3. Hidden representations were extracted from the pretrained model.
4. Mean pooling was applied across the temporal dimension.
5. A fixed-length 768-dimensional embedding was obtained.

---

### 2. Embedding Visualization

UMAP was used to project the 768-dimensional embeddings into two dimensions.

This allowed visual inspection of:

* Local neighborhood structure
* Global embedding geometry
* Potential clustering of recordings belonging to the same raga

---

### 3. Neighbor Agreement Analysis

Neighbor agreement measures how frequently the nearest neighbors of a recording belong to the same raga.

A higher value indicates better local grouping of musically similar recordings.

---

### 4. Supervised Evaluation

Several classification models were trained on the extracted embeddings.

#### Logistic Regression

Evaluates linear separability of the embedding space.

#### Random Forest

Captures non-linear relationships in the embeddings.

#### Multi-Layer Perceptron (MLP)

A shallow neural network used as a stronger supervised probe.

#### Support Vector Machine (SVM)

Uses an RBF kernel to evaluate non-linear structure in the representation space.

---

## Results

| Method              | MERT  | CultureMERT |
| ------------------- | ----- | ----------- |
| Neighbor Agreement  | 0.085 | 0.050       |
| Logistic Regression | 0.086 | 0.086       |
| Random Forest       | 0.149 | 0.085       |
| MLP                 | 0.130 | 0.107       |
| SVM                 | 0.077 | 0.103       |

---

## Observations

* Both models generated meaningful music embeddings.
* Logistic Regression produced identical performance for both models.
* MERT achieved higher scores in Neighbor Agreement, Random Forest, and MLP evaluations.
* CultureMERT achieved higher performance in the SVM evaluation.
* No model consistently outperformed the other across all evaluation methods.
* Differences between models were relatively small, indicating that dataset size may be a major limiting factor.

---

## Hyperparameter Study

UMAP hyperparameters were varied to observe how visualization changes with different settings.

Parameters explored:

* Different values of `n_neighbors`
* Different values of `min_dist`

### Findings

* Smaller `n_neighbors` emphasized local structure and small clusters.
* Larger `n_neighbors` preserved more global structure.
* Cluster geometry changed noticeably with hyperparameter choice.
* Overall conclusions regarding model comparison remained unchanged.

---

## What I Observed

The quality and distribution of the dataset had a major impact on the experiments. Initially, many ragas appeared only once, making meaningful evaluation difficult. Restricting the dataset to repeated ragas produced a more reliable benchmark.

The embedding spaces produced by MERT and CultureMERT showed noticeable visual differences when projected using UMAP. However, these visual differences did not always correspond to improved classification performance.

---

## What Surprised Me

I initially expected CultureMERT to consistently outperform MERT because it was specifically designed to capture culturally relevant musical characteristics.

However, the results were mixed. MERT performed better in Neighbor Agreement, Random Forest, and MLP evaluations, while CultureMERT achieved better performance in the SVM evaluation.

This suggests that model performance depends heavily on the evaluation method and available training data. The project highlighted how difficult it is to draw strong conclusions from small, sparsely annotated datasets.

---

## Limitations

The primary limitation of this study is dataset size.

Although Saraga contains many recordings:

* Only a subset had usable raga annotations.
* Several ragas still had very few examples.
* The final evaluation subset contained only 78 recordings across 25 ragas.

Because of this:

* Classification results may have high variance.
* Statistical conclusions are limited.
* Full end-to-end fine-tuning was not performed due to the high risk of overfitting.

Therefore, the findings should be considered exploratory rather than definitive.

---

## Conclusion

This project compared MERT and CultureMERT on Carnatic classical music using the Saraga dataset.

Embeddings were evaluated through:

* UMAP visualization
* Neighbor agreement analysis
* Logistic Regression
* Random Forest
* Multi-Layer Perceptron (MLP)
* Support Vector Machine (SVM)

Both models produced useful musical representations. However, CultureMERT did not demonstrate a clear and consistent advantage over MERT on the selected evaluation subset.

Future work could involve:

* Larger annotated Carnatic datasets
* End-to-end fine-tuning
* More extensive hyperparameter studies
* Evaluation on additional Indian classical music corpora

---


```text
.


---

## References

1. MERT: Music Understanding Representation Learning with Large-Scale Self-Supervised Training
2. CultureMERT: Culture-Aware Music Representation Learning
3. Saraga Dataset
4. MIRDATA Library
