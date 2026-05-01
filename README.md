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

## Datasets

- **[Cityscapes](https://www.cityscapes-dataset.com/)** – Urban scene understanding benchmark.
- **[BDD100K](https://bdd-data.berkeley.edu/)** – Large-scale diverse driving video dataset.

---

## Code

> Working code will be added once the paper is accepted.

---

## License

This project is released under the [LICENSE](LICENSE) in this repository.
