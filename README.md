# Brain MRI Classification Workshop

**A hands-on Google Developer Student Club workshop project that introduces image classification with a convolutional neural network (CNN).**

The notebook walks through downloading a labeled brain MRI dataset, preparing images, building a CNN with TensorFlow/Keras, training the model, and visualizing predictions. It is designed as an educational walkthrough of an end-to-end computer vision workflow.

**Task:** supervised binary classification of images labeled `yes` (tumor) or `no` (no tumor). Despite the repository's original name, the implementation is a classifier trained on labeled examples, rather than an unsupervised anomaly detector.

[Open the workshop notebook](Google_Workshop_Anomaly_Detection_on_MRI_Brain_Scans.ipynb) · [Run in Google Colab](https://colab.research.google.com/github/SanskritiAripineni/Anomaly-Detection-on-MRI-Brain-Scans/blob/main/Google_Workshop_Anomaly_Detection_on_MRI_Brain_Scans.ipynb) · [Dataset on Kaggle](https://www.kaggle.com/datasets/navoneel/brain-mri-images-for-brain-tumor-detection)

## What the workshop covers

- Downloading a dataset using the Kaggle CLI in Google Colab.
- Loading image folders and resizing inputs to **224 × 224** pixels.
- Applying image augmentation with random flips, rotations, and zoom.
- Building and training a small CNN for binary classification.
- Plotting training and validation accuracy and loss.
- Comparing predicted labels with dataset labels in an image grid.

## Model and tools

| Component | Implementation |
| --- | --- |
| Environment | Google Colab / Jupyter notebook |
| Framework | TensorFlow and Keras |
| Data access | Kaggle CLI |
| Visualization | Matplotlib |
| Input | 224 × 224 RGB images; batches of 32 |
| Preprocessing | Pixel rescaling by 1/255 |
| Feature extraction | Three convolution blocks with 16, 32, and 64 filters, each followed by max pooling |
| Classification head | Flatten → Dense(128, ReLU) → Dropout(0.5) → Dense(1, sigmoid) |
| Training objective | Binary cross-entropy with Adam |
| Reported metric in notebook | Accuracy |

## Run the notebook

1. Open the **Run in Google Colab** link above. A GPU runtime is optional.
2. Have a Kaggle account and a `kaggle.json` API credentials file available for the notebook's authentication flow. Keep this file out of the repository and any shared notebook outputs.
3. Run the first cell and upload `kaggle.json` when prompted. The cell downloads and extracts the dataset.
4. Run the remaining cells in order to prepare images, build the model, train, and inspect predictions.

If the runtime does not provide the Kaggle CLI, install it in a new cell with `%pip install kaggle` before running the download cell.

The notebook expects the extracted images under `brain_tumor_dataset/`, with class subfolders. It uses Colab-specific upload utilities, so a local Jupyter run requires adapting the credential and dataset setup.

### Expected outputs

A complete run produces a model summary, epoch-by-epoch training logs, accuracy/loss curves, evaluation output, and a grid of images with predicted and actual labels. No pretrained checkpoint is provided; running the notebook trains a model.

The current walkthrough trains for **15 epochs**, evaluates and plots that stage, then continues training the same model for **10 additional epochs** before the final prediction visualization. The first curves therefore describe the initial training stage, not all 25 epochs.

## Evaluation and limitations

This repository preserves an educational workshop implementation. Its printed accuracy should be interpreted in the context of that implementation:

- The loader initially reserves 20% of the images as a holdout pool. The notebook then uses one batch from that pool for testing and the remaining batches for validation.
- The validation/test construction uses `take(1)` and `skip(1)` on a shuffled dataset. A stronger evaluation should use explicit, fixed, disjoint image splits before batching.
- The notebook does not establish patient-level separation or evaluate on an independent external dataset.
- Accuracy alone does not describe performance for each class. Precision, recall, a confusion matrix, and error analysis would be useful extensions.
- Package versions are not pinned, and the loader seed does not make the entire training process deterministic.

**This is an educational image-classification project, not a clinically validated diagnostic tool.** No clinical performance claims are made.

## Repository contents

```text
.
├── README.md
└── Google_Workshop_Anomaly_Detection_on_MRI_Brain_Scans.ipynb
```

## Workshop context and dataset credit

Created for a **Google Developer Student Club workshop**. The notebook focuses on making the basic computer vision workflow accessible through a guided coding exercise.

Dataset: [Brain MRI Images for Brain Tumor Detection](https://www.kaggle.com/datasets/navoneel/brain-mri-images-for-brain-tumor-detection), published on Kaggle by Navoneel Chakrabarty. Consult the dataset page for its usage terms and source information.
