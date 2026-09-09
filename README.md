# Google Developer Org | Brain MRI Classification Workshop

### Technical leadership and hands-on computer vision education

[![Leadership](https://img.shields.io/badge/Role-Technical%20Lead-4285F4?logo=google&logoColor=white)](#leadership-and-impact)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-FF6F00?logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)
[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Format](https://img.shields.io/badge/Format-Hands--on%20Workshop-0F9D58)](#workshop-workflow)

> **Leadership highlight:** Sanskriti Aripineni served as **Technical Lead for the Google Developer Student Club**, leading a practical workshop that guided participants through an end-to-end computer-vision workflow—from acquiring and preparing an image dataset to training, evaluating, and interpreting a convolutional neural network.

This educational project demonstrates supervised binary classification of brain MRI images labeled **tumor** or **no tumor**. It was designed to make the machine-learning lifecycle approachable while introducing the technical and ethical limitations of applying AI to medical imagery.

[Open the workshop notebook](notebooks/brain-mri-classification-workshop.ipynb) · [Run in Google Colab](https://colab.research.google.com/github/SanskritiAripineni/Anomaly-Detection-on-MRI-Brain-Scans/blob/main/notebooks/brain-mri-classification-workshop.ipynb) · [View the dataset](https://www.kaggle.com/datasets/navoneel/brain-mri-images-for-brain-tumor-detection)

## At a glance

| Area | Implementation |
| --- | --- |
| Leadership | Technical Lead, Google Developer Student Club |
| Format | Instructor-led, hands-on machine-learning workshop |
| Real-world problem | Introducing scalable image-analysis techniques for complex medical imagery |
| ML task | Supervised binary image classification |
| Classes | Tumor and no tumor |
| Framework | TensorFlow and Keras |
| Model | Custom convolutional neural network |
| Environment | Google Colab |

## The problem

Medical imaging produces large volumes of visually complex data that require specialized expertise to interpret. Variations in scan quality, acquisition settings, anatomy, and pathology make automated analysis challenging, while manual review is time-intensive and difficult to scale.

This workshop translates that broader challenge into an accessible learning exercise. Participants work with a small, labeled brain MRI dataset and build a CNN that learns visual differences between two classes. The goal is not to create a diagnostic system; it is to teach how raw image data moves through a responsible machine-learning workflow and where a classroom model falls short of clinical validation.

## Leadership and impact

As Technical Lead, Sanskriti:

- Structured the workshop as a complete journey from dataset acquisition to model interpretation.
- Led the technical walkthrough of image loading, augmentation, CNN design, training, and evaluation.
- Translated core deep-learning concepts into an implementation suitable for learners.
- Incorporated responsible-AI context so performance metrics were not presented as clinical evidence.
- Delivered a reusable Colab notebook that participants could run without a specialized local environment.

## Workshop workflow

```text
Kaggle MRI dataset
        |
Load and resize to 224 x 224
        |
Training-time image augmentation
        |
Three convolution + max-pooling blocks
        |
Dense layer + dropout
        |
Tumor / no-tumor probability
        |
Learning curves and prediction review
```

Participants learn to:

- Download and authenticate to a Kaggle dataset from Google Colab.
- Build training and holdout datasets from class-labeled image folders.
- Apply random flips, rotations, and zoom to improve input diversity.
- Construct and train a CNN with TensorFlow/Keras.
- Interpret accuracy and loss curves instead of relying on one headline number.
- Compare predicted and actual labels in a visual error-analysis grid.

## Model architecture

| Stage | Configuration |
| --- | --- |
| Input | 224 x 224 RGB images, batch size 32 |
| Preprocessing | Pixel rescaling by `1/255` |
| Augmentation | Horizontal flip, rotation, and zoom |
| Feature extraction | Three convolution blocks with 16, 32, and 64 filters |
| Downsampling | Max pooling after each convolution block |
| Classification head | Flatten -> Dense(128, ReLU) -> Dropout(0.5) |
| Output | Dense(1, sigmoid) |
| Optimization | Adam with binary cross-entropy |

## Run the workshop

The easiest option is to select **Run in Google Colab** above and execute the cells in order.

1. Create or sign in to a Kaggle account.
2. Generate a `kaggle.json` API credential and upload it only when the notebook prompts you.
3. Keep that credential out of Git, screenshots, and shared notebook outputs.
4. Run the dataset, model, training, evaluation, and visualization cells sequentially.

The notebook downloads images into `brain_tumor_dataset/`. A complete run produces a model summary, training logs, accuracy/loss curves, test-batch evaluation, and a prediction grid. No trained checkpoint is committed.

For local exploration:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

The Kaggle upload cell uses Colab-specific utilities and must be adapted for a local Jupyter environment.

## Evaluation boundaries

This repository preserves a teaching implementation, so its metrics should be interpreted accordingly:

- The data loader reserves 20% of images and uses one batch from that pool as the test set.
- A stronger study would create fixed, disjoint train, validation, and test manifests before batching.
- The notebook does not establish patient-level separation or external clinical validation.
- Accuracy alone cannot reveal false-negative risk or class-specific behavior.
- A follow-up should add precision, recall, F1, a confusion matrix, and systematic error analysis.

> **Responsible-use notice:** This is an educational image-classification project—not an anomaly detector, medical device, or clinically validated diagnostic tool.

## Repository structure

```text
.
├── notebooks/
│   └── brain-mri-classification-workshop.ipynb
├── .gitignore
├── requirements.txt
└── README.md
```

## Dataset credit

The workshop uses [Brain MRI Images for Brain Tumor Detection](https://www.kaggle.com/datasets/navoneel/brain-mri-images-for-brain-tumor-detection), published on Kaggle by Navoneel Chakrabarty. Consult the dataset page for its source information and usage terms.
