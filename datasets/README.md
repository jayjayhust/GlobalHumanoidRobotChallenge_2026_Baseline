# Challenge 2026 Dataset

This dataset provides training/evaluation data for the 2026 Global Humanoid Robot Challenge Simulation Competition.

**Data Format**: LeRobot v2.1

## Directory Structure

```
Packing_box/box_closing_001/         - Carton Packing (Dual-arm Coordination)
```

## Dataset Overview

- **Carton Packing (Dual-arm Coordination)**
  - `box_closing_001`: 50 episodes

## Data Format

Each dataset contains multiple episodes stored in Parquet format:

```
{dataset_name}/data/chunk-000/episode_XXXXXX.parquet
```

- Dataset ID format: `{action}_{number}` (e.g., `box_closing_001`)
- Episode filename: `episode_{6-digit number}.parquet` (zero-padded)

Field definitions can be found in the main project at `lerobot/common/policies/utils.py` under observation/action definitions.

## Hugging Face Upload/Download

### Method 1: Hugging Face CLI

```bash
# Install HF CLI
powershell -ExecutionPolicy ByPass -c "irm https://hf.co/cli/install.ps1 | iex"

# Login
hf auth login

# Upload
hf upload UBTECH-Robotics/challenge2026_dataset .

# Download
hf download UBTECH-Robotics/challenge2026_dataset
```

### Method 2: Python

```python
from huggingface_hub import login, upload_folder, snapshot_download

# Login
login()

# Upload
upload_folder(
    folder_path=".",
    repo_id="UBTECH-Robotics/challenge2026_dataset",
    repo_type="dataset"
)

# Download
snapshot_download(
    repo_id="UBTECH-Robotics/challenge2026_dataset",
    repo_type="dataset"
)
```

### Method 3: Git + Git-XET

```bash
# Install git-xet
git xet install

# Clone (HTTPS)
git clone https://huggingface.co/UBTECH-Robotics/challenge2026_dataset
cd challenge2026_dataset

# Push
git push

# Or use SSH
git clone git@hf.co:UBTECH-Robotics/challenge2026_dataset
```

## Dataset Naming Convention

| Level | Format | Example |
|-------|--------|---------|
| Task | / | `Packing_box` |
| Dataset Directory | `{action}_{number}` | `box_closing_001/`, `box_closing_002/` |
| Episode File | `episode_{6-digit number}.parquet` | `episode_000000.parquet` |

When adding new datasets, increment the number sequentially (e.g., `_001`, `_002`, `_003`).
