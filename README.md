# Machine Learning Assignment

Task 1 contains the training and evaluation code. Tasks 2 and 3 currently contain planning notes.

## Run on Windows 11

Clone the repository in PowerShell:

```powershell
git clone https://github.com/killsumber/assignment_SV.git
cd assignment_SV
```

Use the Python environment where your GPU training already works. Check CUDA before running experiments:

```powershell
python -c "import torch, torchvision; print(torch.__version__); print('CUDA:', torch.cuda.is_available()); print(torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'CPU')"
```

Install missing notebook dependencies in that same environment:

```powershell
python -m pip install -r requirements.txt
```

PyTorch and torchvision are managed separately to preserve the existing CUDA installation. If the check fails, select a compatible installation at https://pytorch.org/get-started/locally/.

Open `notebooks/01_pet_classification.ipynb` in VS Code, select that Python environment as the notebook kernel, and run cells in order. The first cell should print `Device: cuda`. The dataset downloads automatically. Paths are relative to the notebook working directory. Keep the same working directory for subsequent runs.

The ablation cell trains five models for 15 epochs each. Multi-task and transfer learning run in later cells. If GPU memory runs out, reduce `batch_size` in `make_loaders` and in the test DataLoader. Restart the interrupted experiment after changing its batch size and record the change when comparing models.

## Updates and results

Before pulling, save any local notebook changes you want to keep. Review `git status` and commit those changes before updating:

```powershell
git pull --ff-only
```

Run updated cells in a fresh kernel to avoid using old function definitions. Avoid changing code or pulling updates while training is running.

Training writes checkpoints, TensorBoard logs and ablation histories into `task1_results` under the working directory. These files and downloaded data are excluded from Git. Preserve them locally for evaluation and submission. Share relevant CSV metrics or notebook error outputs for review. Include TensorBoard files in the final submission archive as required by the assignment.

To view TensorBoard when the working directory is `notebooks`:

```powershell
python -m tensorboard.main --logdir task1_results/runs
```

The repository copy of each notebook initially has outputs cleared. Training results have not been validated on the Windows PC yet.
