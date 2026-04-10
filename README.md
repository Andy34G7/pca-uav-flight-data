# PCA UAV Flight Data: Variance Inference with PCA

This project uses Principal Component Analysis (PCA) on `imu_data.csv` to answer:

How much variance can be retained after dimensionality reduction, and how many principal components are needed to reach target thresholds such as 90%, 95%, and 99%?

The main notebook is `dimensionality-reduction-using-pca.ipynb`.

## Project Goal

The workflow is designed to:

1. Load and validate IMU data.
2. Clean and standardize numeric features.
3. Fit PCA and compute explained/cumulative variance.
4. Infer the minimum number of components for selected variance targets.
5. Build a reduced PCA feature set.
6. Train and tune a classifier on the reduced space.
7. Persist outputs and run metadata for reproducibility.

## Repository Structure

- `dimensionality-reduction-using-pca.ipynb`: End-to-end PCA variance inference workflow.
- `imu_data.csv`: Input dataset.
- `README.md`: Project documentation.
- `LICENSE`: License file.

## Environment and Dependencies

Required Python packages:

- `numpy`
- `pandas`
- `matplotlib`
- `scikit-learn`

Install example:

```bash
pip install numpy pandas matplotlib scikit-learn
```

## Notebook Workflow

The notebook is organized into seven sections.

### 1. Set Up Environment and Dependencies

- Imports libraries.
- Sets random seed.
- Defines paths for input data and artifact output.

### 2. Load Configuration and Input Data

- Defines runtime configuration (target candidates, variance thresholds, split ratio).
- Loads `imu_data.csv`.
- Prints shape and columns for quick schema inspection.

### 3. Validate and Clean Data

- Summarizes null counts and duplicate rows.
- Infers target column from common names (`class`, `label`, `target`, `y`, `activity`) with fallback to last column.
- Coerces non-target columns to numeric when possible.
- Removes duplicates.

### 4. Implement Modern Processing Pipeline

- Builds a numeric feature matrix.
- Applies median imputation and standard scaling.
- Fits full PCA.
- Computes individual explained variance and cumulative explained variance.
- Plots variance curves and prints component counts for 90%, 95%, and 99% thresholds.
- Constructs `pca_df` using the 95% retained-variance component count.

### 5. Train and Tune Model

- Splits PCA-reduced data into train/test sets.
- Trains a baseline SVC model.
- Runs `GridSearchCV` for parameter tuning.
- Reports baseline and tuned accuracy with best parameters.

### 6. Evaluate with Automated Metrics

- Builds an evaluation summary.
- Applies lightweight assertions to verify basic expected conditions.

### 7. Persist Artifacts and Reproducible Outputs

- Saves reduced data to `artifacts/pca_reduced_data.csv`.
- Saves run metadata to `artifacts/run_metadata.json`.

## Interpreting Variance Results

If $k$ is the smallest number of components such that cumulative explained variance satisfies

$$
\sum_{i=1}^{k} \text{EVR}_i \geq 0.95
$$

then $k$ is the dimensionality recommended under a 95% variance-retention rule.

## How to Run

1. Open `dimensionality-reduction-using-pca.ipynb`.
2. Select a Python kernel.
3. Run all cells from top to bottom.
4. Review the variance plot, component counts, model metrics, and generated artifacts.

