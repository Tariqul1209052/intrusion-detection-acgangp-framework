# Autoencoder--ACGAN-GP Framework for Intrusion Detection

This repository contains Jupyter notebooks for evaluating machine-learning
classifiers on the NSL-KDD and UNSW-NB15 intrusion-detection datasets,
including experiments with autoencoder-based latent representations and
AC-GAN with gradient penalty (ACGAN-GP) for class-conditioned
synthetic-data generation.

> **Reproducibility note:** Run the notebooks using the dataset versions
> and experimental settings. Reported results should be regenerated from the code before being quoted or
> compared.

## Repository contents

  --------------------------------------------------------------------------------------
  File                                               Description
  -------------------------------------------------- -----------------------------------
  `NSL_KDD_Imbalanced_Classification.ipynb`          Baseline classification workflow on
                                                     the original, imbalanced NSL-KDD
                                                     data, including preprocessing,
                                                     autoencoder representation
                                                     learning, classifier evaluation,
                                                     and figures.

  `NSL_KDD_ACGAN_GP_Balanced_Classification.ipynb`   NSL-KDD workflow incorporating
                                                     autoencoder representations and
                                                     ACGAN-GP-based synthetic-data
                                                     generation for selected minority
                                                     classes, followed by classifier
                                                     evaluation.

  `UNSW_NB15_ACGAN_GP_Classification.ipynb`          UNSW-NB15 preprocessing,
                                                     autoencoder representation
                                                     learning, ACGAN-GP synthetic-data
                                                     generation, and classification
                                                     evaluation.
  --------------------------------------------------------------------------------------

## Datasets

The dataset files are obtained from
their official or authorized sources and follow any applicable dataset
terms.

### NSL-KDD

The NSL-KDD notebooks accept training and testing files named either:

-   `KDDTrain.txt` and `KDDTest.txt`, or
-   `KDDTrain+.txt` and `KDDTest+.txt`.

The notebook upload cells prompt for the files and check for the
supported filenames. Ensure that the selected files are from the same
intended NSL-KDD release and match the manuscript's experimental
description.

### UNSW-NB15

The UNSW-NB15 notebook expects:

-   `UNSW_NB15_training-set.csv`
-   `UNSW_NB15_testing-set.csv`

Upload both files when prompted. The notebook uses the dataset's
attack-category and label columns during preprocessing and evaluation.

## Environment and dependencies

The notebooks are designed for a Python/Jupyter environment and include
Google Colab upload functionality. A GPU can accelerate PyTorch model
training, but availability depends on the runtime.

The notebooks use the following main packages:

-   Python
-   NumPy and pandas
-   PyTorch
-   scikit-learn
-   Matplotlib and Seaborn
-   XGBoost and LightGBM
-   SciPy (for statistical procedures where used)

Some notebooks install or update XGBoost and LightGBM within the
notebook. For reproducible work, record the Python and package versions
used for the final experiments rather than relying on automatically
updated package versions.

## How to run

1.  Download or clone this repository and open the relevant `.ipynb`
    notebook in Google Colab or Jupyter.
2.  Obtain the appropriate dataset files and upload them when prompted.
3.  Run the notebook cells, from top to bottom.
4.  Check the preprocessing output, class distributions, and
    train/validation/test separation before training.
5.  Allow the autoencoder and, where applicable, ACGAN-GP training to
    complete.
6.  Run the classifier evaluation cells to generate performance metrics
    and figures.
7.  Save the resulting tables and figures, and verify that they match
    the final manuscript before submission or publication.

Run the baseline NSL-KDD notebook separately from the ACGAN-GP-balanced
NSL-KDD notebook when comparing the original imbalanced setting with the
augmentation setting. Run the UNSW-NB15 notebook separately for its
dataset-specific evaluation.

## Method overview

The notebooks implement the following general workflow, with
dataset-specific preprocessing:

1.  **Load and preprocess data:** Read the training and testing files,
    prepare input features and labels, and transform features for model
    input.
2.  **Learn latent representations:** Train an autoencoder to encode the
    input features into a lower-dimensional latent representation and
    reconstruct the input.
3.  **Generate synthetic representations (ACGAN-GP experiments):** Train
    a class-conditioned generator and discriminator with a
    gradient-penalty term, then generate synthetic latent
    representations for selected classes.
4.  **Augment training data:** Combine the generated representations
    with the applicable training representations according to the
    notebook's class-balancing procedure.
5.  **Train and evaluate classifiers:** Evaluate the implemented
    classifiers and calculate metrics and plots, as specified in each
    notebook.

The exact class mapping, preprocessing operations, model parameters,
augmentation targets, and evaluation procedure should be taken from the
corresponding notebook and the final manuscript. Do not assume that the
two datasets use identical class definitions or preprocessing.

## Outputs

Depending on the notebook and the cells executed, outputs may include:

-   Class-distribution summaries before and after augmentation
-   Autoencoder training and reconstruction diagnostics
-   ACGAN-GP training logs and synthetic-sample summaries
-   Classification reports and performance metrics
-   Confusion matrices and ROC/AUC visualizations
-   Saved publication-oriented figures

Output directory names and files are defined in the individual
notebooks. Check each notebook for the exact save location.

## Reproducibility and interpretation

-   Use the same dataset versions, data splits, random seeds, model
    settings, and package versions as the final manuscript when
    reproducing the reported experiments.
-   Keep the test set separate from model fitting, preprocessing
    decisions, and synthetic-data generation. Any scaling or
    transformation parameters should be fitted on training data only and
    then applied to validation/test data as appropriate.
-   Fit the generator using training data only. Do not use test-set
    observations to generate synthetic training samples.
-   Report repeated-run statistical tests only when they have actually
    been executed on an appropriate set of paired results. A single
    score per classifier is not sufficient for a paired Wilcoxon
    signed-rank comparison.
-   Treat results from NSL-KDD and UNSW-NB15 as dataset-specific
    evaluations unless a formal cross-dataset transfer experiment has
    been conducted.
-   Regenerate figures and numerical results from the notebooks before
    using them in the manuscript.