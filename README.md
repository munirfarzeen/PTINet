# PTINet: Context-aware Multi-task Learning for Pedestrian Intent and Trajectory Prediction

PTINet is a deep learning framework designed to jointly predict pedestrian trajectories and crossing intentions by leveraging both local and global contextual cues. It is particularly suited for applications in autonomous driving and robotic navigation, where anticipating human movement is crucial for safety and efficiency.

## Overview

PTINet integrates:

- **Past Trajectories**: Historical movement data of pedestrians.
- **Local Contextual Features (LCF)**: Attributes specific to pedestrians, including behavior and surrounding scene characteristics.
- **Global Features (GF)**: Environmental information such as traffic signs, road types, and optical flow from consecutive frames.

By combining these inputs, PTINet jointly predicts:

- **Pedestrian Trajectory**: Future positions over a specified time horizon.
- **Pedestrian Intention**: Likelihood of crossing or not crossing.

This multi-task learning approach enhances the model's ability to understand and predict pedestrian behavior in complex urban environments.

---

## 📦 Installation

### Prerequisites

- **Operating System**: Ubuntu 20.04 or later
- **Python**: 3.8 or higher
- **CUDA**: 11.1 or higher (for GPU support)

### Setup Instructions

```bash
git clone https://github.com/munirfarzeen/PTINet.git
cd PTINet
python3 -m venv ptinet_env
source ptinet_env/bin/activate
pip install -r requirements.txt
```

> ⚠️ Make sure you have PyTorch with CUDA support installed if using a GPU.

To verify CUDA support:

```bash
python -c "import torch; print(torch.cuda.is_available())"
```

---
## 🧹 Optical Flow Calculation & Data Preprocessing
PTINet requires dense optical flow as input to extract motion cues. We use RAFT (Recurrent All-Pairs Field Transforms) for computing dense optical flow, as described in the paper. 

PTINet uses the JAAD and PIE datasets.

### Step 1: Download Datasets

- [JAAD](http://data.nvision2.eecs.yorku.ca/JAAD_dataset/)
- [PIE](https://data.nvision2.eecs.yorku.ca/PIE_dataset/)
- [TITAN](https://usa.honda-ri.com/titan)
  
### Step 2: Download RAFT
```bash
git clone https://github.com/princeton-vl/RAFT.git
cd RAFT
pip install -r requirements.txt
```
Follow the RAFT documentation to obtain optical flow for JAAD and PIE dataset.
### Step 3: Organise Data

```
PTINet/
└── data/
    ├── JAAD/
    │   ├── images/
    │   └── optical_flow/
    ├── PIE/
    │   ├── images/
    │   └── optical_flow/
    └── TITAN/
```

### Step 4: Preprocess

```bash
python preprocess_data.py --dataset jaad
python preprocess_data.py --dataset pie
python preprocess_data.py --dataset titan
```

Processed files will be saved under the `processed/` directory.

---

## 🏋️‍♂️ Training

Train the model with:

```bash
python train.py --dataset jaad --epochs 50 --batch_size 32 --learning_rate 0.001
```

### Arguments

| Argument         | Description                        | Default   |
|------------------|------------------------------------|-----------|
| `--dataset`      | Dataset to use (`jaad`, `pie`, `titan`)     | Required  |
| `--epochs`       | Number of epochs                   | 50        |
| `--batch_size`   | Batch size                         | 32        |
| `--learning_rate`| Learning rate                      | 0.001     |

Checkpoints are saved in the `checkpoints/` folder.

---

## 📊 Evaluation

Evaluate a trained model:

```bash
python evaluate.py --dataset jaad --checkpoint checkpoints/jaad_model.pth
```

### Evaluation Metrics

#### Trajectory Prediction

- **ADE**: Average Displacement Error
- **FDE**: Final Displacement Error

#### Intention Prediction

- **Accuracy**
- **Precision**
- **Recall**
- **F1-score**

Results will be shown in the terminal and optionally saved in:

```
results/
├── jaad_eval_results.txt
```

> Ensure dataset and checkpoint correspond to each other.

---
## 📫 Contact

For questions, please raise an issue or contact the authors through GitHub.

---

## 📖 Citation

If you utilize PTINet in your research or applications, please cite the following publication:

```bibtex
@article{munir2025context,
  title        = {Context-aware multi-task learning for pedestrian intent and trajectory prediction},
  author       = {Munir, Farzeen},
  journal      = {Transportation Research Part C},
  year         = {2025},
  note         = {Article posted: 07 June 2025; Submitted: 09 June 2025},
  volume       = {},
  number       = {},
  pages        = {105203},
  doi          = {},
  publisher    = {Elsevier},
  copyright    = {© 2025 The Authors. Published by Elsevier Ltd. This is an open access article under the CC BY license. (http://creativecommons.org/licenses/by/4.0/)},
  url          = {},
}

```

---

For questions, please raise an issue or contact the authors through GitHub.


