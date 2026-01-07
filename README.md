# The deformed relativistic Hartree–Bogoliubov theory in continuum (DRHBc) and Machine Learning 

A comprehensive machine learning framework that corrects theoretical predictions from nuclear Density Functional Theory (DRHBc model) using physics-informed feature engineering and Δ-learning approaches. This project significantly improves the accuracy of nuclear binding energies, charge radii, and separation energy predictions while maintaining physical consistency.

## Files

### `Scraping Data.ipynb`

- **Purpose:** To programmatically acquire raw nuclear data from an online source and organize it into a structured format for further analysis.
- **Key Methods:**
    - Uses the `requests` library to download a `.txt` file containing nuclear data from a specified URL (`drhbctable.jcnp.org`).
    - Employs `pandas` to read an existing `Data.csv` file (presumably a processed version of the scraped data or a related dataset).
    - Iterates through unique proton numbers (Z) in the dataset to filter and save subsets of data into individual CSV files, creating a separate file for each isotopic chain (fixed Z).
    - Utilizes system commands (`zip`) to compress the generated directory of Z-specific data files into a single `.zip` archive.
- **Main Logic:** This notebook first downloads a comprehensive nuclear data table. It then takes a master `Data.csv` file, likely derived from such a table, and systematically organizes it by splitting the data into separate files based on the proton number (Z), making it easier to analyze specific isotopic chains. Finally, it archives these organized files for convenience.

### `Nuclear Data Analysis.ipynb`

- **Purpose:** To perform extensive exploratory data analysis (EDA) and visualization of nuclear properties derived from the `Data.csv` file. This notebook aims to uncover trends, relationships, and compare theoretical predictions with experimental observations.
- **Key Methods:**
    - Leverages `pandas` for data loading, cleaning (handling missing values, type conversion), and manipulation.
    - Utilizes `matplotlib.pyplot` and `seaborn` for creating a diverse range of static and statistical plots.
    - Generates scatter plots to compare experimental versus calculated values (e.g., binding energies, charge radii), visualize nuclear radii (neutron, proton, matter) against nucleon numbers, and illustrate nucleon deformations and Fermi levels.
    - Creates line plots to show trends of separation energies and Fermi levels as functions of neutron, proton, or mass numbers, and to depict S2n trends across isotopic chains.
    - Employs heatmaps to visualize the distribution of properties like binding energy and matter deformation across the nuclear chart (Z vs. N).
    - Computes and visualizes a correlation matrix of various nuclear parameters to identify strong relationships.
    - Includes a `seaborn.pairplot` for a broad overview of variable distributions and pairwise relationships.
- **Main Logic:** This notebook focuses on interpreting nuclear physics data. It starts by preparing the `Data.csv` for analysis. It then systematically visualizes key nuclear properties—such as binding energies, separation energies, radii, deformations, and Fermi levels—to identify patterns, shell closures, and structural changes. A significant part involves comparing theoretical model predictions (e.g., DRHBc) with available experimental data and exploring the interdependencies between different nuclear characteristics through correlation analysis.

  # Nuclear Data Analysis with Machine Learning Corrections

This project implements a machine learning framework to correct theoretical predictions from nuclear Density Functional Theory (specifically the DRHBc model). Using physics-informed feature engineering and Δ-learning approaches, we significantly improve the accuracy of binding energy and charge radius predictions.

## Project Structure

### `Scraping Data.ipynb`
- **Purpose:** To programmatically acquire raw nuclear data from an online source and organize it into a structured format for further analysis.
- **Key Methods:**
    - Uses the `requests` library to download a `.txt` file containing nuclear data from `drhbctable.jcnp.org`.
    - Employs `pandas` to read and process the `Data.csv` file.
    - Organizes data by proton number (Z) into separate CSV files for individual isotopic chains.
    - Creates compressed archives of organized data files.

### `Nuclear Data Analysis.ipynb` 
- **Purpose:** Comprehensive machine learning pipeline for correcting DRHBc theoretical predictions using physics-informed ML approaches.
- **Key Features:**
    - **Physics-Informed Feature Engineering:** Creates domain-specific features like isospin asymmetry, geometric scaling, shell proximity, and parity effects.
    - **Δ-Learning Framework:** Predicts residuals between theoretical and experimental values rather than absolute quantities.
    - **Dual ML Approaches:** Compares direct ML imputation vs. physics-constrained indirect ML for separation energies.
    - **Advanced Models:** Implements Linear Regression, Ridge, Lasso, Random Forest, XGBoost, and SVR for regression tasks.
    - **Classification:** Binary classification of deformed vs. spherical nuclei using multiple algorithms.
    - **Unsupervised Learning:** PCA, t-SNE, and clustering (K-Means, DBSCAN, Agglomerative, GMM) for pattern discovery.
    - **Comprehensive Validation:** Statistical comparison between ML approaches and experimental data.
    - **Pattern Discovery:** Analysis of Eb-Rch relationships and deformation effects.

### **Key ML Methodologies**

#### 1. **Physics-Constrained Δ-Learning**
- Predicts residual errors: ΔEb = Eb_exp - Eb_cal, ΔRch = Rch_exp - Rch_cal
- Maintains physical relationships while correcting systematic theory errors
- Features include shell proximity, deformation parameters, asymmetry terms

#### 2. **Separation Energy Imputation**
- **Direct ML:** Direct prediction of Sn, S2n, S2p from nuclear features
- **Indirect ML:** Calculation from ML-corrected binding energies using physics formulas
- Comparative analysis validates thermodynamic consistency

#### 3. **Deformation Classification**
- Binary classification: deformed (|β_t| > 0.1) vs. spherical nuclei
- Algorithms: Logistic Regression, k-NN, Random Forest, XGBoost, SVM
- Near-perfect classification accuracy for identifying deformation islands

#### 4. **Pattern Discovery**
- Eb vs. Rch relationship analysis comparing DRHBc theory vs. ML-corrected
- Separate regression analysis for deformed and spherical nuclei
- Preservation of fundamental physics relationships by ML corrections

### **Key Results**

#### Statistical Findings:
- **Indirect ML superior:** 90-96% improvement in MAE over Direct ML for separation energies
- **High reliability:** Indirect ML correct 99.3-99.7% of time in high-uncertainty predictions
- **Physics preservation:** ML maintains Eb-Rch relationships (slope changes < 5%)
- **Full coverage:** All 5437 nuclei processed with improved accuracy

#### Model Performance:
- **Binding Energy:** XGBoost best (R² = 0.9147, MAE = 0.3332 MeV)
- **Charge Radius:** Random Forest best (R² = 0.8132, MAE = 0.0088 fm)
- **Classification:** Random Forest/XGBoost (Accuracy = 1.000, F1 = 1.000)


## Usage

1. **Data Acquisition:** Run `Scraping Data.ipynb` to download and organize nuclear data
2. **ML Analysis:** Run `Nuclear Data Analysis.ipynb` to perform comprehensive ML corrections
3. **Report Generation:** Compile `Report/main.tex` to generate the final report

## Key Innovations

1. **Physics-Informed ML:** Integration of nuclear physics knowledge into ML features
2. **Δ-Learning Paradigm:** Focus on correcting systematic theory errors rather than predicting absolute values
3. **Thermodynamic Consistency:** Enforcement of nuclear additivity constraints via indirect ML approach
4. **Comprehensive Validation:** Statistical comparison between multiple ML methodologies
5. **Pattern Discovery:** Unsupervised learning to identify natural nuclear regimes



## License

This project is for academic and research purposes. Please contact the authors for permissions.
