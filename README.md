# EEG-based AI-BCI Wheelchair Advancement

This repository accompanies the research study:

> **EEG-based AI-BCI Wheelchair Advancement: Hybrid Deep Learning with Motor Imagery for Brain Computer Interface**

---

## Authors

- Bipul Thapa
- Biplov Paneru
- Bishwash Paneru
- Khem Narayan Poudyal

---

## DOI

https://doi.org/10.48550/arXiv.2509.25667

---

# Citation

If you use this repository, preprocessing pipeline, dataset preparation methodology, or the proposed **TFormerEEG** architecture in your research, please cite:

```bibtex
@article{thapa2025eegbci,
  title={EEG-based AI-BCI Wheelchair Advancement: Hybrid Deep Learning with Motor Imagery for Brain Computer Interface},
  author={Thapa, Bipul and Paneru, Biplov and Paneru, Bishwash and Poudyal, Khem Narayan},
  journal={arXiv preprint arXiv:2509.25667},
  year={2025},
  doi={10.48550/arXiv.2509.25667}
}
```

---

# Project Overview

This project focuses on:

- EEG Motor Imagery signal preprocessing
- Brain-Computer Interface (BCI) research
- Deep learning for EEG classification
- Hybrid Transformer-based EEG architectures
- AI-assisted wheelchair advancement systems

The repository includes:

- EEG preprocessing pipeline
- Feature extraction workflow
- Deep learning model implementations
- Transformer-based EEG architectures
- Performance evaluation notebooks

---

# Dataset Information

This project uses the EEG Motor Imagery dataset from:

> Kaya et al. (2018)  
> *A large electroencephalographic motor imagery dataset for electroencephalographic brain computer interfaces*

DOI:

https://doi.org/10.1038/sdata.2018.211

---

# Dataset Download Instructions

Download the following `.mat` files for **CLASubjectE**:

```text
CLASubjectE1601223StLRHand.mat
CLASubjectE1601193StLRHand.mat
CLASubjectE1512253StLRHand.mat
```

Place the downloaded files in a local directory.

Example:

```text
C:\Users\YourName\Downloads\
```

Update the paths inside the preprocessing script:

```python
mat_file_paths = [
    r"path_to_your_folder/CLASubjectE1601223StLRHand.mat",
    r"path_to_your_folder/CLASubjectE1601193StLRHand.mat",
    r"path_to_your_folder/CLASubjectE1512253StLRHand.mat",
]
```

> **Note:**  
> This implementation currently uses **Subject E**, but can be extended to additional subjects.

---

# EEG Channel Configuration

## Original EEG Channels

```text
Fp1, Fp2, F3, F4, C3, C4, P3, P4, O1, O2,
A1, A2, F7, F8, T3, T4, T5, T6, Fz, Cz, Pz, X5
```

## Removed Channels

The following channels are excluded during preprocessing:

```text
A1
A2
X5
```

## Remaining Channels

A total of **19 EEG channels** are retained for feature extraction and modeling.

---

# Processing Pipeline

## 1. Data Extraction

The function:

```python
process_data(mat_data)
```

performs the following operations:

- Extracts EEG signal data from:

```python
o_data['data']
```

- Extracts marker labels from:

```python
o_data['marker']
```

- Removes unwanted EEG channels
- Retains selected EEG channels for processing

---

## 2. Event Detection

Motor imagery events are detected using marker transitions.

### Event Mapping

| Marker Transition | Class |
|---|---|
| `0 → 1` | Class 1 |
| `0 → 2` | Class 2 |

Each detected event stores:

```python
[class_label, onset_sample]
```

### Returned Variables

| Variable | Description |
|---|---|
| `class_info_array` | Event labels and onset indices |
| `data_key` | Filtered EEG data |
| `marker_data` | EEG marker labels |

---

## 3. Feature Extraction

For each detected event:

- 200 samples before onset are extracted
- 200 samples after onset are extracted

### Window Processing

For every EEG window:

- Signals are flattened into a 1D feature vector
- Corresponding label is appended

### Per Event Output

| Output | Description |
|---|---|
| Row 1 | Before onset window |
| Row 2 | After onset window |

---

# Feature Dimension

Given:

- 200 temporal samples
- 19 EEG channels

The resulting feature dimension becomes:

```text
200 × 19 = 3800 features
+ 1 label column
= 3801 total columns
```

---

# Output Dataset

The preprocessing pipeline:

- Processes all `.mat` files
- Extracts EEG windows
- Generates feature vectors
- Combines all extracted samples
- Saves the final dataset as CSV

## Output File

```text
D:\paper eeg\combined_eeg_features.csv
```

## Final Dataset Shape

```text
(3808, 3801)
```

| Dimension | Description |
|---|---|
| 3808 rows | Extracted EEG windows |
| 3801 columns | 3800 features + 1 label |

---

# Implemented Models

The repository includes implementations of:

- XGBoost
- EEGNet
- Transformer-based EEG models
- TFormerEEG

---

# Best Performance

| Model | Accuracy |
|---|---|
| TFormerEEG | ~93% |

---

# Repository Structure

```text
models/
│
├── motor-imagery-all-models.ipynb
├── motor_Imagery_EEG.ipynb
```

---

# Important Files

## Model Performance Evaluation

```text
models/motor-imagery-all-models.ipynb
```

Contains:

- Model training
- Cross-validation
- Accuracy evaluation
- F1-score analysis
- Performance comparison

---

## EEG Data Loading and Preprocessing

```text
models/motor_Imagery_EEG.ipynb
```

Contains:

- EEG loading pipeline
- Channel filtering
- Event detection
- Feature extraction
- CSV dataset generation

---

# Dependencies

Install required Python libraries:

```bash
pip install numpy pandas scipy matplotlib
```

---

# Summary

This repository provides a complete EEG Motor Imagery processing and deep learning framework for Brain-Computer Interface research.

The pipeline:

- Loads raw EEG `.mat` files
- Filters EEG channels
- Detects motor imagery events
- Extracts temporal EEG windows
- Converts EEG data into machine learning-ready features
- Trains deep learning architectures
- Evaluates Transformer-based EEG classification models

The proposed **TFormerEEG** architecture achieved the best overall performance with approximately **93% accuracy**.
