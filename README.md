# [OmniMamba](https://github.com/Yusaong/OmniMamba)

Official repository for OmniMamba: Wavelet-Enhanced Omni-Perspective State Space Modeling for dental CBCT segmentation.

## Installation 

Requirements: `Ubuntu 20.04`, `CUDA 11.8`

1. Create a virtual environment: `conda create -n omnimamba python=3.10 -y` and `conda activate umamba `
2. Install [Pytorch](https://pytorch.org/get-started/previous-versions/#linux-and-windows-4) 2.0.1: `pip install torch==2.0.1 torchvision==0.15.2 --index-url https://download.pytorch.org/whl/cu118`
3. Install [Mamba](https://github.com/state-spaces/mamba): `pip install causal-conv1d>=1.2.0` and `pip install mamba-ssm --no-cache-dir`
4. Download code: `git clone https://github.com/Yusaong/OmniMamba`
5. `cd OmniMamba/omnimamba` and run `pip install -e .`


sanity test: Enter python command-line interface and run

```bash
import torch
import mamba_ssm
```

![network](https://github.com/Yusaong/OmniMamba/tree/main/assets/network_architecture.png)


## Model Training
OmniMamaba is built on the popular [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) framework. Prepare your dataset following this [guideline](https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/dataset_format.md).

### Preprocessing

```bash
nnUNetv2_plan_and_preprocess -d DATASET_ID --verify_dataset_integrity
```

### Train 3D models

- Train 3D `OmniMamba` model

```bash
nnUNetv2_train DATASET_ID 3d_fullres all -tr nnUNetTrainerOmniMamba
```

## Inference

- Predict testing cases with `OmniMamba` model

```bash
nnUNetv2_predict -i INPUT_FOLDER -o OUTPUT_FOLDER -d DATASET_ID -c CONFIGURATION -f all -tr nnUNetTrainerOmniMamba --disable_tta
```

## Acknowledgements

We thank the authors of [nnU-Net](https://github.com/MIC-DKFZ/nnUNet), [Mamba](https://github.com/state-spaces/mamba) and [UMamba](https://github.com/bowang-lab/U-Mamba) for making their valuable code publicly available.

