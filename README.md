# AI-Based EM Image Restoration

This repository preserves the supplied **AI Restoration Studio** project for restoration and super-resolution of grayscale scanning electron microscopy images. The desktop app implements a Restormer restoration stage followed by EDSR 2× super-resolution. The supplied folder also contains training notebooks, evaluation outputs, model checkpoints, documentation, an installer, and paired datasets.

## Project layout

| Path | Contents |
| --- | --- |
| `SRC/Applications/Source Code/` | PyQt6 desktop application and assets |
| `SRC/Applications/ISS/` | Inno Setup installer definition |
| `SRC/Applications/EXE/`, `SRC/Applications/Installer/` | Windows binaries in the Release archive |
| `SRC/Models/Restoration_Models/` | MIRNet-v2, MPRNet, and NAFNet notebooks, results, and checkpoints |
| `SRC/Models/Super_Resolution_Models/` | ESRGAN, RCAN, SRCNN, and SwinIR notebooks, results, and checkpoints |
| [`Dataset/`](Dataset/README.md) | Paired restoration and super-resolution images in Release archives; every original subdirectory has a download guide |
| `Documentation/` | Report, slides, and demonstration video |
| [`Screenshots/`](Screenshots/README.md) | Original empty screenshots directory, retained in the repository tree |

## Large files and dataset

GitHub's per-file Git limit prevents four supplied files from being committed directly. Download [release `v1.0-project-files`](https://github.com/ArviZuko/AI-Based-EM-Image-Restoration/releases/tag/v1.0-project-files):

- `large-project-files.zip` contains the supplied Windows executable and installer plus `NAFNet_weights.pth` and `ESRGAN_weights.pth`.
- `dataset-part-01-of-06.zip` through `dataset-part-06-of-06.zip` contain **all 16,636 files** in the supplied `Dataset/` tree. These are independent ZIP archives, not a multipart ZIP.

Extract every archive into the **repository root**, keeping the paths stored inside each ZIP. The resulting `Dataset/Restoration/` and `Dataset/Super Resolution/` folders preserve the supplied train, validation, and test splits. The dataset is also described in the [source publication on Kaggle](https://www.kaggle.com/datasets/omkadam05/semicon-v2-dual-dataset).

The repository keeps the original folder hierarchy. Each directory whose files are supplied through a Release archive has its own `README.md` listing the exact archive(s) needed for that directory. This includes the [executable](SRC/Applications/EXE/README.md), [installer](SRC/Applications/Installer/README.md), [NAFNet checkpoint](SRC/Models/Restoration_Models/NAFNet/README.md), and [ESRGAN checkpoint](SRC/Models/Super_Resolution_Models/ESRGAN/README.md).

## Run the application

Install Python 3.10–3.12 and dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python "SRC\Applications\Source Code\app.py"
```

**Checkpoint availability:** The supplied folder does not contain the `Restormer_weights.pth` and `EDSR_weights.pth` files required by the desktop application's fixed pipeline. Place compatible checkpoints beside `app.py` or in a `weights` subfolder before running inference. The included checkpoints belong to the seven model experiments listed above; they do not substitute for those two files.

The installer and executable in the Release archive are supplied as received. Their runtime behavior has not been independently verified here.

## Attribution

The dataset is derived from NFFA-Europe SEM imagery. Check the source dataset and model licenses before redistribution or other reuse. No project-level license was supplied.
