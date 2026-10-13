# AI Restoration Studio

**AI-Powered Image Denoising and Super-Resolution Platform**

AI Restoration Studio is a standalone deep-learning system for restoring degraded grayscale microscopy and semiconductor images. It combines Restormer for same-resolution denoising and restoration with EDSR for 2x super-resolution in a reproducible desktop and command-line workflow.

```text
Input image
    -> Restormer denoising/restoration
    -> EDSR 2x super-resolution
    -> enhanced output
```

## Key capabilities

- Fixed, reproducible Restormer-to-EDSR inference pipeline.
- Native Windows desktop application and installer definition.
- Standalone command-line inference and reference-based evaluation.
- Reproducible training notebooks and trained checkpoints.
- Benchmark histories, metrics, plots, and representative test outputs.
- Dataset documentation, integrity audit, and technical project report.

## Dataset

The experiments use a dual restoration dataset derived from 4,158 NFFA-Europe MEMS SEM source images. The published archive identifiers are retained for reproducibility:

- `SEMICON_SR_2X_v2`: 512x384 LR to 1024x768 HR, with bicubic 2x downsampling.
- `SEMICON_Noise_v2`: 1024x768 degraded input to 1024x768 clean target, covering 11 documented degradation families.
- Shared source-level split: 2,910 training, 831 validation, and 417 test images.

Download the published dataset from [Kaggle](https://www.kaggle.com/datasets/omkadam05/semicon-v2-dual-dataset). The multi-gigabyte archives are intentionally excluded from GitHub. See [`Dataset/README.md`](Dataset/README.md) and [`Dataset/Dataset_Audit_Report.pdf`](Dataset/Dataset_Audit_Report.pdf).

## Repository structure

```text
AI-Restoration-Studio/
├── README.md
├── requirements.txt
├── App/
│   ├── app.py
│   ├── AI_Restoration_Studio.exe
│   ├── AI_Restoration_Studio.iss
│   └── assets/
├── Dataset/
│   ├── README.md
│   └── Dataset_Audit_Report.pdf
├── Documentation/
│   ├── Final_Project_Report.pdf
│   └── AI_Restoration_Studio_Project_Presentation.pptx
├── Evaluation/
│   └── inference.py
├── Models/
│   ├── README.md
│   ├── Restoration_Models/
│   ├── Super_Resolution_Models/
│   └── Final_Selected_Models/
└── Outputs/
    ├── README.md
    ├── Benchmark_Results/
    └── Test_Outputs/
```

## Installation

Python 3.10-3.12 is recommended.

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

GPU acceleration is used automatically when a compatible PyTorch CUDA installation is available. The included requirements do not force a specific CUDA build.

## Evaluation and inference

Run the deployed Restormer-to-EDSR pipeline:

```powershell
python Evaluation\inference.py --input sample.png --mode full
```

Run an individual stage:

```powershell
python Evaluation\inference.py --input noisy_images --mode denoise
python Evaluation\inference.py --input lr_images --mode sr
```

Evaluate against an explicitly supplied ground-truth directory:

```powershell
python Evaluation\inference.py --input test_inputs --ground-truth test_gt --mode denoise
```

Output are written as PNG images together with `per_image_metrics.csv` and `summary.json`. PSNR, SSIM, MAE, MSE, and RMSE are calculated only when matching ground truth is supplied.

## Desktop application

Run from source with `python "App\Source Code\app.py"`. No verified standalone executable was available in the cleaned project, so `App/EXE/` is intentionally empty. The application implements the fixed `Restormer -> EDSR x2` workflow.

## Models

Eight core experiments are retained for reproducibility and comparison: SRCNN, EDSR, RCAN, ESRGAN, MIRNet-v2, MPRNet, NAFNet, and Restormer. A SwinIR benchmark is also retained because its verified notebook, checkpoint, and outputs are available.

The deployed models are Restormer for same-resolution restoration and EDSR for 2x super-resolution. See [`Models/README.md`](Models/README.md) for task assignments and selection rationale.

## Documentation

- [`Documentation/Comprehensive_Document/Final_Project_Report.pdf`](Documentation/Comprehensive_Document/Final_Project_Report.pdf)
- [`Documentation/PPT/AI_Restoration_Studio_Project_Presentation.pptx`](Documentation/PPT/AI_Restoration_Studio_Project_Presentation.pptx)
- [`BRANDING_AUDIT.md`](BRANDING_AUDIT.md)

## Large files and release readiness

Checkpoint files and the Windows executable are assigned to Git LFS. Before public release, confirm Git LFS quota and all applicable dataset, architecture, and checkpoint licensing terms. Rebuild the executable and installer after changing application assets so compiled resources match the source tree.

## Attribution and licensing

The source imagery originates from NFFA-Europe. Users must follow the authoritative source-data and published-dataset terms. Model architectures and checkpoints may also be governed by their originating project licenses. No verified project-level license was available in the supplied artifacts.
