# FedMSIS-BiDir: Federated Self-Training with Temporal Pseudo-Label Refinement for Object Detection

**Shoaib Sajid<sup>1</sup>, Zafar Aziz<sup>2</sup>, Shimaa A. Abdel Hakeem<sup>3</sup>, Hyungwon Kim<sup>4</sup>**

Chungbuk National University, South Korea

<sup>1</sup>shoaib@cbnu.ac.kr &nbsp;|&nbsp; <sup>2</sup>zafar343@cbnu.ac.kr &nbsp;|&nbsp; <sup>3</sup>shimaakotb@cbnu.ac.kr &nbsp;|&nbsp; <sup>4</sup>hwkim@cbnu.ac.kr

**Corresponding authors:** Shimaa A. Abdel Hakeem (shimaakotb@cbnu.ac.kr) and Hyungwon Kim (hwkim@cbnu.ac.kr)

> **Note:** The full code will be released once the associated paper is accepted.

---

## Abstract

Federated learning (FL) enables distributed model training without centralizing raw data, but it often suffers from scarce labeled annotations on client devices. In this work, we address label scarcity in federated object detection by integrating self-training with a novel **bi-directional pseudo-label refinement mechanism** that leverages temporal consistency.

Each client first generates pseudo-labels on its unlabeled video frames using the current global model. Low-confidence detections are then re-evaluated by a tracker that links objects across adjacent frames: if a high-confidence detection of the same class appears at nearly the same location (IoU > 0.9) in a neighboring frame, the low-confidence detection's confidence is boosted and it is added to the training set.

After local training with these refined pseudo-labels, client models are sent to the server. Instead of conventional weighted averaging, we employ a **validation-driven best-model selection** strategy: the server evaluates all received models (and the previous global model) on a held-out validation set and broadcasts the one with the highest mAP to all clients in the next round. This accelerates convergence and propagates the most effective local updates under both homogeneous and heterogeneous data distributions.

---

## Key Contributions

- **Bi-directional pseudo-label refinement:** Low-confidence detections on unlabeled video frames are refined by leveraging temporal consistency from neighboring frames, boosting confidence when a high-confidence detection of the same class is found at a closely matching location (IoU > 0.9).
- **Validation-driven best-model selection:** Instead of standard federated averaging, the server selects and broadcasts the global model with the highest mAP on a held-out validation set, accelerating convergence under both IID and Non-IID data distributions.
- **Semi-supervised federated object detection:** Combines self-training with federated learning to tackle label scarcity across distributed clients without sharing raw data.

---

## Method Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        FedMSIS-BiDir                            │
│                                                                 │
│  ┌──────────┐   pseudo-labels    ┌──────────────────────────┐   │
│  │  Global  │ ─────────────────► │   Client (per round)     │   │
│  │  Model   │                    │                          │   │
│  └──────────┘                    │  1. Generate pseudo-     │   │
│       ▲                          │     labels on unlabeled  │   │
│       │                          │     video frames         │   │
│  best model                      │  2. Bi-dir refinement:   │   │
│  (highest mAP)                   │     boost low-conf       │   │
│       │                          │     detections via       │   │
│  ┌──────────┐   local models     │     temporal neighbors   │   │
│  │  Server  │ ◄───────────────── │  3. Train on refined     │   │
│  │ Selector │                    │     pseudo-labels        │   │
│  └──────────┘                    └──────────────────────────┘   │
│  Evaluates all client models + previous global model on a       │
│  held-out validation set; broadcasts best model next round      │
└─────────────────────────────────────────────────────────────────┘
```

---

## Results

### Cityscapes

| Method | mAP | Δ vs FedSTO |
|---|---|---|
| FedSTO | baseline | — |
| **FedMSIS-BiDir** | baseline + 1.5% | **+1.5%** |

> FedMSIS-BiDir shows even larger gains on challenging classes such as **person** and **bus**.

### BDD100K

| Setting | Method | mAP | Δ vs FedSTO |
|---|---|---|---|
| Non-IID | **FedMSIS-BiDir** | baseline + 0.7% | **+0.7%** |
| IID | **FedMSIS-BiDir** | baseline + 0.3% | **+0.3%** |

### Semi-Supervised Federated Learning with Unlabeled YouTube Videos

| Method | mAP | Δ vs FedSTO |
|---|---|---|
| FedSTO | baseline | — |
| **FedMSIS-BiDir** | baseline + 2.4% | **+2.4%** |

---

## Datasets

- **[Cityscapes](https://www.cityscapes-dataset.com/)** – Urban scene understanding benchmark.
- **[BDD100K](https://bdd-data.berkeley.edu/)** – Large-scale diverse driving video dataset.

---

## Citation

> Citation information will be added once the paper is published.

---

## License

This project is released under the [LICENSE](LICENSE) in this repository.
