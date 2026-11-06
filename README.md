# Applied Linear Algebra for Machine Learning — Four Numerical Methods

**A mathematics-first portfolio project using MRI image matrices to demonstrate PCA, SVD, eigendecomposition, and least squares.**

This project illustrates how linear algebra supports dimensionality reduction, matrix approximation, spectral analysis, and numerical regression. MRI images provide a common numerical dataset across four methods; **this is not a tumor-detection model or a clinical diagnostic tool**.

## Project at a glance

- **Observations:** 400 MRI images, with 100 images from each of four source categories (`glioma`, `meningioma`, `notumor`, `pituitary`). The labels describe dataset organization, not model predictions.
- **Preprocessing:** convert to grayscale, resize to 128 × 128 pixels, normalize intensities to [0, 1], and flatten each image to 16,384 features.
- **Data matrix:** `X` has shape `(400, 16384)`.
- **Methods:** principal component analysis (PCA), singular value decomposition (SVD), eigendecomposition of a Gram matrix, and least-squares fitting.
- **Implementation:** Python notebooks using numerical and scientific-computing tools.

## Methods and results

### 1. Principal component analysis (PCA)

PCA identifies orthogonal directions of variance in the **column-centered** MRI matrix. Its retained-variance thresholds and relative reconstruction errors illustrate the trade-off between fewer components and approximation quality.

| Target explained variance | Components | Relative reconstruction error |
| --- | ---: | ---: |
| 90% | 142 | 0.31607 |
| 95% | 210 | 0.22247 |
| 99% | 323 | 0.09895 |

The first 10 principal components account for approximately **50.53%** of the centered-data variance.

### 2. Singular value decomposition (SVD)

SVD of the **uncentered** MRI matrix supports low-rank reconstruction and compression. Singular-value energy is calculated using squared singular values.

| Target singular-value energy | Singular directions | Relative reconstruction error |
| --- | ---: | ---: |
| 90% | 44 | 0.31504 |
| 95% | 106 | 0.22320 |
| 99% | 257 | 0.09956 |

The complete reduced SVD achieves relative numerical reconstruction error of approximately **1.33 × 10⁻¹⁵**.

**Note:** PCA and this SVD analysis use different matrix centering conventions; their component counts should not be compared as though they measure identical quantities.

### 3. Eigendecomposition

The Gram matrix `G = X @ X.T` has shape `(400, 400)` and is symmetric positive semidefinite. Its eigenvalues correspond to the squared singular values of the same uncentered matrix `X`.

- Largest eigenvalue: approximately **349,460.0203**.
- **5** leading eigenvectors retain approximately **80.3894%** of the spectral energy.
- To retain at least **90%, 95%, and 99%**, the analysis requires **44, 106, and 257** eigenvectors, respectively.
- Numerical reconstruction errors agree with the corresponding theoretical calculations reported in the notebooks.

This section demonstrates the connection between singular values, eigenvalues, spectral energy, and low-rank approximation.

### 4. Least squares

Least squares fits a linear model using leading SVD-derived image features to predict each image's **mean pixel intensity**. The target is a numerical property derived from the images—not a tumor label or patient outcome.

For a model with 20 reduced features and an intercept:

| Metric | Recorded result |
| --- | ---: |
| Design-matrix shape | `(400, 21)` |
| Design-matrix rank | 21 |
| Condition number | 10.1557 |
| RMSE (in-sample) | 0.00165998 |
| MAE (in-sample) | 0.00119254 |
| R² (in-sample) | 0.99948981 |
| Relative normal-equation error | ≈ 9.42 × 10⁻¹⁴ |

**Interpretation:** This is an **in-sample mathematical demonstration** of reduced-feature regression. Because the target is derived from the input images and the reported metrics are not held-out predictions, these numbers should not be presented as evidence of clinical or out-of-sample predictive performance.

## Repository notebooks

Run the notebooks in the order shown, because later notebooks depend on the processed matrix created by the first notebook.

| Order | Notebook | Blocks | Main purpose |
| --- | --- | --- | --- |
| 1 | [`01_Data_Preparation.ipynb`](notebooks/01_Data_Preparation.ipynb) | 01–05 | Select, inspect, preprocess, and save the MRI image matrix |
| 2 | [`02_PCA.ipynb`](notebooks/02_PCA.ipynb) | 06–10 | Centering, explained variance, component selection, and reconstruction |
| 3 | [`03_SVD.ipynb`](notebooks/03_SVD.ipynb) | 11–15 | Singular values, low-rank reconstruction, and energy thresholds |
| 4 | [`04_Eigendecomposition.ipynb`](notebooks/04_Eigendecomposition.ipynb) | 16–20 | Gram matrix, eigenvalues, spectral energy, and reconstruction |
| 5 | [`05_Least_Squares.ipynb`](notebooks/05_Least_Squares.ipynb) | 21–25 | Reduced-feature regression, residuals, conditioning, and feature-count comparisons |



## Running the analysis

The notebooks were developed in **Google Colab** and mount Google Drive. At present, their code references the project directory:

```text
/content/drive/MyDrive/MATHEMATICS_PROJECTS/PROJECT_03_LA_ML_FOUR_METHODS
```

The first notebook also reads the original images from a separate **user-specific Google Drive folder**. To reproduce the workflow elsewhere, obtain the permitted source dataset and update that input path in Notebook 01, along with any project paths, before executing the notebooks in sequence.

Notebook 01 generates:

```text
data/processed/X_mri_400.npy
data/processed/y_mri_400.npy
data/processed/filenames_mri_400.json
```

The dataset selection uses a fixed random seed (`42`) and selects 100 images per category from the available source files. Reproducing the **exact same subset** requires matching the original archive/version and input file set; the source-version audit is not yet closed. The repository's standalone reproducibility has **not yet been independently re-tested**.

## Dataset provenance and licensing — verification pending

Working records identify **Masoud Nickparvar's Brain Tumor MRI dataset on Kaggle** as the probable source and **CC BY 4.0** as the recorded license. However, the **exact original ZIP archive/version and applicable attribution/license terms still require confirmation before public release**. Do not interpret this note as a verified license statement. Source URL, version, and required attribution will be added after verification.

The original medical images, generated processed arrays, and copied datasets should not be publicly redistributed until the source and redistribution permissions are confirmed.

## Limitations

- A balanced sample of 400 images is used to demonstrate methods, not to estimate clinical performance.
- MRI label categories are descriptive metadata; no MRI diagnostic classifier is evaluated here.
- PCA analyzes a centered matrix, whereas the reported SVD/Gram spectral results use uncentered `X`.
- Least-squares results are **in-sample** and target image mean intensity; they are not evidence of tumor classification or generalization.
- Notebook execution currently depends on Google Drive-specific paths and a separately stored input dataset.
- Source-version, licensing, clean-environment reproducibility, and repository-security checks remain open pre-publication tasks.

## Applications of these mathematical techniques

The same methods are useful beyond medical imaging: multivariate exploratory analysis, dimensionality reduction, image and signal compression, numerical conditioning checks, spectral analysis, reduced-rank approximation, and least-squares modeling. This repository documents numerical workflow, mathematical interpretation, and checks designed to make analytical results interpretable and auditable.

## Status

**Portfolio preparation in progress — not yet published.** The notebooks' calculations and saved outputs were previously checked; publication checks for provenance, standalone reproducibility, package requirements, repository structure, and secrets remain pending.

## Author

**Jorge Peña Durán** — Applied Mathematics · Linear Algebra · Numerical Analysis · Machine Learning Model Evaluation

GitHub: [JorgeDuranMath](https://github.com/JorgeDuranMath)
