This repository is associated with the following research study:

EEG-based AI-BCI Wheelchair Advancement: Hybrid Deep Learning with Motor Imagery for Brain Computer Interface

Authors:

Bipul Thapa
Biplov Paneru
Bishwash Paneru
Khem Narayan Poudyal

📌 DOI: https://doi.org/10.48550/arXiv.2509.25667


If you use this code, dataset processing pipeline, or the proposed CTHM (Convolutional Transformer Hybrid Model) in your research, please cite the paper as follows:

BibTeX
@article{thapa2025eegbci,
  title={EEG-based AI-BCI Wheelchair Advancement: Hybrid Deep Learning with Motor Imagery for Brain Computer Interface},
  author={Thapa, Bipul and Paneru, Biplov and Paneru, Bishwash and Poudyal, Khem Narayan},
  journal={arXiv preprint arXiv:2509.25667},
  year={2025},
  doi={10.48550/arXiv.2509.25667}
}
Project details:


EEG Motor Imagery Dataset Processing

This project processes the EEG Motor Imagery Dataset from:

Kaya et al. (2018)
“A large electroencephalographic motor imagery dataset for electroencephalographic brain computer interfaces”
DOI: https://doi.org/10.1038/sdata.2018.211

📥 Dataset Download Instructions
Visit the dataset repository associated with the paper.
Download the .mat files for CLASubjectE:
CLASubjectE1601223StLRHand.mat
CLASubjectE1601193StLRHand.mat
CLASubjectE1512253StLRHand.mat

⚠️ Note: This implementation uses Subject E. It can be extended to other subjects as needed.

Place the downloaded files in a local directory
Example:

C:\Users\YourName\Downloads\

Update the file paths in the script:

mat_file_paths = [
    r"path_to_your_folder/CLASubjectE1601223StLRHand.mat",
    r"path_to_your_folder/CLASubjectE1601193StLRHand.mat",
    r"path_to_your_folder/CLASubjectE1512253StLRHand.mat",
]
Run the script.
🧠 EEG Channel Configuration

We define 22 EEG channel names:

Fp1, Fp2, F3, F4, C3, C4, P3, P4, O1, O2,
A1, A2, F7, F8, T3, T4, T5, T6, Fz, Cz, Pz, X5
Removed Channels:
A1
A2
X5

These channels are excluded from feature extraction.

Remaining Channels Used:

19 EEG channels are retained for processing.

⚙️ Processing Pipeline
1️⃣ Data Extraction

The function process_data(mat_data):

Extracts:
EEG signal data → o_data['data']
Marker labels → o_data['marker']
Filters:
Keeps only selected EEG channels
Removes unwanted channels
2️⃣ Event Detection

The script detects motor imagery events based on marker transitions:

0 → 1 → Class 1
0 → 2 → Class 2

Each detected event stores:

[class_label, onset_sample]

Returned values:

class_info_array → Event label and onset index
data_key → Filtered EEG data
marker_data → Label data
3️⃣ Feature Extraction

For each detected event:

Extract 200 samples before onset
Extract 200 samples after onset

For each window:

EEG signals are flattened into a 1D feature vector
Corresponding marker label is appended at the end
Per Event Output:
1 row → Before onset
1 row → After onset
📊 Feature Dimension

If:

200 samples
19 channels

Then:

200 × 19 = 3800 features
+ 1 label column
= 3801 columns total
📁 Output

The script:

Processes all three .mat files
Extracts features
Combines all extracted rows
Saves a single CSV file:
D:\paper eeg\combined_eeg_features.csv
Final Dataset Shape:
(3808, 3801)
3808 rows → All extracted windows
3801 columns → 3800 features + 1 label
📦 Dependencies

Install required libraries:

pip install numpy pandas scipy
▶️ How to Run
python your_script_name.py
🔬 Summary

This pipeline:

Loads raw EEG .mat files
Filters selected EEG channels
Detects motor imagery events
Extracts time-windowed features
Converts EEG signals into flattened ML-ready feature vectors
Saves a combined CSV dataset for machine learning




🔬 Ablation Study — CTHM (Convolutional Transformer Hybrid Model)

To evaluate the contribution of each architectural component, we performed an ablation study on the proposed CTHM (Convolutional Transformer Hybrid Model).

We compared:

Hybrid_Full (CTHM) → CNN + Transformer
CNN_Only → Convolutional backbone only
Transformer_Only → Transformer encoder only
for ablation study

Baseline models: 
