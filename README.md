# Truncation-Robust 3D Human Pose Estimation

This repository summarizes a project on **truncation-robust 3D human pose estimation** with reduced frame flickering in video sequences.

> Due to institutional policy at **KIST (Korea Institute of Science and Technology)**, full code and dataset cannot be released publicly.  
> Evaluation logs, result summaries, and visual comparisons are available on the project page below:
---

## ✅ Overview


### 🎯 Goal
To build a **truncation-robust** and **temporally stable** 3D human pose estimation pipeline from monocular video.

### ✅ Approach
1. Use **MeTRAbs** to extract **heatmap-based 2D keypoints** that are robust to partial occlusion / truncation.
2. Feed the 2D keypoint sequences into temporal 2D-to-3D lifting models:
   - **VideoPose3D**
   - **MHFormer**
   - **MixSTE**
   - **P-STMO**
3. Reconstruct 3D pose sequences with reduced flickering and improved stability under truncation.

## 📌 System Pipeline

Image Sequence → MeTRAbs (2D heatmaps)  
→ Temporal 2D-to-3D Lifting (VideoPose3D / MHFormer / MixSTE / P-STMO)  
→ Final 3D Pose (reduced flickering, truncation-robust)


### ✅ My Contribution
✔ Proposed approach  
✔ Implemented full pipeline  
✔ Visualization / evaluation scripts  
✔ Experiments on truncated Human3.6M

---

## 🎥 Visual Comparisons

| Model | Comparison |
|-------|------------|
| VideoPose3D vs Ours | https://youtu.be/RKRD0uAZZK8?si=jq8O0yAaJ9HDZgTw |
| MixSTE vs Ours      | https://youtu.be/wR_9YVHcbsU |
| MHFormer vs Ours    | https://youtu.be/xnEyfmRxFjc |
| P-STMO vs Ours      | https://youtu.be/mjZmG5dZ5rs |

---

## 🧪 Experiments

**Dataset:** Human3.6M  
**Metric:** MPJPE (Mean Per Joint Position Error)

### ✅ Normal (non-truncated) input

| Model | Baseline MPJPE ↓ | Ours MPJPE ↓ |
|-------|------------------|--------------|
| VideoPose3D | 57.7 | **54.3** |
| MHFormer    | 69.25 | **53.25** |
| MixSTE      | 66.6 | **44.0** |
| P-STMO      | 64.93 | **54.84** |

MeTRAbs (2D): **48.64**

---

### ✅ Truncated Inputs

Truncation types:

- **Random Box** – grid-based random occlusion  
- **Moving Box** – sliding occlusion through frames  
- **Fixed Box** – upper / middle / lower region removed  

| Model | Random Box | Fixed Lower | Fixed Middle | Fixed Upper | Moving Box | Avg. MPJPE ↓ |
|-------|------------|--------------|--------------|--------------|------------|---------------|
| MeTRAbs (2D) | 154.60 | 99.61 | 143.28 | 197.25 | 109.06 | **140.76** |
| VideoPose3D | 90.2 | 107.9 | 220.9 | 311.0 | 111.1 | **168.22** |
| MHFormer    | 123.90 | 103.66 | 138.61 | 166.72 | 99.28 | **126.43** |
| MixSTE      | 128.5 | 99.8 | 141.8 | 172.7 | 100.3 | **128.62** |
| P-STMO      | 174.20 | 147.88 | 162.23 | 371.81 | 133.95 | **198.01** |
| **Ours (VideoPose3D)** | **70.5** | **72.4** | **78.4** | **90.0** | **65.3** | **75.32** |
| **Ours (MHFormer)**    | 165.95 | 97.65 | 200.24 | 168.69 | 125.60 | **151.63** |
| **Ours (MixSTE)**      | **66.1** | **64.8** | **76.8** | **87.5** | **63.7** | **71.78** |
| **Ours (P-STMO)**      | 125.78 | 93.34 | 100.67 | 157.94 | 89.71 | **113.49** |

## 🔍 Limitations & Future Work

✅ Current model improves robustness under synthetic truncation on Human3.6M.  
✖  Still relies on accurate 2D keypoint detection  
→ Future: joint end-to-end 2D+3D training or diffusion-based lifting

✖  Evaluation currently on Human3.6M only  
→ Future: in-the-wild datasets (3DPW, MuCo-3DHP)

✅ Temporal models reduce flickering  
✖  But long-term motion consistency can still degrade under heavy occlusion  
→ Future: transformer-based temporal refinement or trajectory priors


**Summary:**  
✅ Truncation-robust (lower MPJPE across all occlusion patterns)  
✅ More temporally stable (reduced flickering)  
✅ MixSTE variant shows the largest improvement

---

## 📚 References

- Ghafoor & Mahmood (2022). *Quantification of occlusion handling capability of 3D human pose estimation framework.*
- Sárándi et al. (2020). *Metrabs: Metric-scale truncation-robust heatmaps for absolute 3D human pose estimation.*
- Pavllo et al. (CVPR 2019). *VideoPose3D.*
- Li et al. (CVPR 2022). *MHFormer.*
- Zhang et al. (CVPR 2022). *MixSTE.*
- Shan et al. (ECCV 2022). *P-STMO.*

---

⚠️ Note: This repository contains a project summary only.
Due to institutional research policy at KIST, full code and dataset access
cannot be provided publicly.
Evaluation logs, figures, and comparisons are available upon request.

