# Mini Project Viva Prep

## 1) Demo Evaluation (5 Marks)

### A. Execution
What to show:
- Open the notebook and run all cells top-to-bottom.
- Show that the pipeline completes without errors.
- Show generated artifacts:
  - artifacts/pca_reduced_data.csv
  - artifacts/run_metadata.json

What this proves:
- The implementation is executable and reproducible.

### B. Concepts Covered
Linear algebra concepts actually used in this project:
- Matrix representation of dataset
- Standardization as linear transformation
- Covariance structure of transformed data
- Eigenvalues and eigenvectors (through PCA decomposition)
- Orthogonal principal-component basis
- Projection of data onto PCA subspace
- Reduced model construction from principal components

### C. Output of Each Component
- Matrix representation: numeric feature matrix X of shape n x d
- Matrix simplification/reduction: dimensionality drops from d to k (k chosen by variance threshold)
- Basis and orthogonal basis: principal component directions are orthogonal
- Projection-based output: rows projected from X to X_pca_95 (lower-dimensional coordinates)
- Least squares connection: PCA directions come from maximizing variance and are equivalent to spectral decomposition of covariance; reconstruction error minimization aligns with least-squares geometry
- Eigen analysis: explained variance ratio and cumulative variance curve
- Final output: reduced dataset plus model metrics and run metadata

---

## 2) Workflow-Wise Viva Script (Concept -> Purpose -> Outcome)

Use this exact pattern in viva answers.

### Step 1: Data Matrix Formation
Concept:
- Matrix representation of data.

Purpose:
- Convert tabular IMU features into a numerical matrix suitable for linear algebra operations.

Outcome:
- Feature matrix X (numeric columns) and optional target vector y.

### Step 2: Standardization
Concept:
- Linear transformation (centering and scaling per feature).

Purpose:
- Remove unit/scale mismatch so no single feature dominates variance.

Outcome:
- Standardized matrix X_scaled with comparable feature scales.

### Step 3: Covariance + Eigenvalue/Eigenvector Analysis
Concept:
- Covariance matrix spectral decomposition.

Purpose:
- Identify directions of maximum variance and quantify their importance.

Outcome:
- Eigen-directions (principal components), explained variance ratio, and cumulative variance.

### Step 4: Orthogonal Basis Formation
Concept:
- Orthogonal basis from principal components.

Purpose:
- Build independent axes that remove redundancy/correlation among original features.

Outcome:
- Principal-component basis where components are mutually orthogonal.

### Step 5: Projection to Reduced Subspace
Concept:
- Orthogonal projection from high-dimensional space to lower-dimensional subspace.

Purpose:
- Keep most information with fewer dimensions (chosen by threshold, e.g., 95%).

Outcome:
- Reduced matrix X_pca_95 and dataframe pca_df with PCs.

### Step 6: Model Training and Tuning on Reduced Space
Concept:
- Predictive modeling in reduced vector space.

Purpose:
- Test whether reduced coordinates preserve predictive signal.

Outcome:
- Baseline and tuned SVC accuracy; best hyperparameters from grid search.

### Step 7: Evaluation + Reproducibility
Concept:
- Metric comparison and deterministic artifact persistence.

Purpose:
- Show measurable effect of pipeline and make results auditable.

Outcome:
- Evaluation summary + saved reduced data and metadata files.

---

## 3) Rubric-Aligned Direct Answers

### What does your data matrix represent?
- Rows are samples from imu_data.csv.
- Columns are numeric features after cleaning.
- Target column is excluded from PCA projection and added back later for supervised evaluation.

### Why was each mathematical step applied?
- Standardization: make dimensions comparable.
- Covariance/eigen analysis: find dominant variance directions.
- Orthogonal basis and projection: compress while preserving structure.
- Reduced modeling: validate that compressed representation is still useful.

### How did each step improve prediction or reveal patterns?
- PCA reveals variance concentration across fewer components.
- Cumulative variance curve gives explicit k for retention targets.
- Reduced representation removes redundancy and can stabilize generalization.

### How does one step connect to the next?
- Clean matrix -> scaled matrix -> covariance/eigen directions -> orthogonal PCs -> projected reduced matrix -> model training -> metric evaluation -> persisted outputs.

---

## 4) Short Viva Responses (High-Scoring, Crisp)

Q: Which concept is central in your project?
A: PCA via eigenvalue-eigenvector analysis of the standardized feature covariance matrix.

Q: Why PCA here?
A: The IMU feature space has correlated dimensions. PCA gives orthogonal directions and retains most variance in fewer components.

Q: How did you select number of components?
A: Using cumulative explained variance thresholds (90%, 95%, 99%). For the final reduced set, I used the minimum k achieving 95% retention.

Q: What is your projection output?
A: A reduced feature matrix (principal component scores) stored as pca_df and exported to artifacts/pca_reduced_data.csv.

Q: Where is least squares in this story?
A: Geometrically, PCA projection minimizes reconstruction error in a least-squares sense for a fixed number of components.

Q: Final project output?
A: Reduced dataset, model performance summary, and run metadata for reproducibility.

---

## 5) Demo Checklist (Before Presentation)

- Run all notebook cells successfully.
- Keep one screenshot/plot of explained variance and cumulative curve.
- Be ready to state chosen k for 95% variance.
- Be ready to show generated artifacts folder.
- Practice 60-second Concept -> Purpose -> Outcome explanation for each stage.
