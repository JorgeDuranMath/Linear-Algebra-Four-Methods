

\# Dataset Documentation



\## 1. Overview



This project uses a subset of 400 brain MRI images to demonstrate four linear algebra methods: Principal Component Analysis (PCA), Singular Value Decomposition (SVD), Eigendecomposition, and Least Squares.



The project focuses on mathematical analysis, numerical verification, and dimensionality reduction. It is not a medical diagnostic system.



\## 2. Dataset Source



The images originate from a Brain Tumor MRI dataset. The Masoud Nickparvar Kaggle collection has been identified as the probable source, but the exact archive version has not yet been independently verified.



Probable dataset page:

https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset



The dataset is not redistributed in this repository. Users should obtain it from its original provider and review the applicable license and terms.



\## 3. Subset Description



The analysis uses 400 images distributed equally across four classes:



\- Glioma: 100

\- Meningioma: 100

\- No Tumor: 100

\- Pituitary: 100



The subset contains 400 observations in total.



\## 4. Image Preprocessing



The project uses the following representation:



1\. Convert each selected image to grayscale.

2\. Resize each image to 128 x 128 pixels.

3\. Represent the image as 16,384 pixel features.

4\. Normalize pixel values to the interval \[0, 1].

5\. Assemble the image matrix X with shape (400, 16384).



The exact image selection, ordering, resizing settings, and reproducibility procedure must be verified against the original preprocessing notebook before a complete reproduction recipe can be published.



\## 5. Generated Files



The project uses the following prepared data files:



\- X\_mri\_400.npy — Image feature matrix.

\- y\_mri\_400.npy — Class labels.

\- filenames\_mri\_400.json — Image filename records.



These data files are not included in the public GitHub repository.



\## 6. Reproducibility Status



The numerical experiments were performed on the prepared 400-image subset. Exact dataset reconstruction instructions remain pending verification of the original archive version and image-selection procedure.



Users should not assume that selecting any 100 images per class will reproduce the reported numerical results.



\## 7. Intended Use



This project is intended for educational, mathematical, and numerical-analysis demonstrations. It does not provide clinical predictions, medical advice, or diagnostic validation.

&#x20; 

