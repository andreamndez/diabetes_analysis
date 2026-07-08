 # Diabetes Prediction and Clinical Analysis (PIMA Dataset)

This project presents a classification system designed to predict diabetes risk, prioritizing **clinical interpretability** and rigorous data processing. By leveraging machine learning techniques, the raw PIMA dataset is transformed into a predictive model capable of capturing complex metabolic relationships.

## 🖥️ Technologies

* **Language:** Python
* **Data Cleaning:** Pandas, NumPy
* **Pipeline & Modeling:** Scikit-Learn
* **Interpretability:** SHAP
* **Visualization:** Seaborn, Matplotlib

## 🚀 Project Process

1.  **Exploratory Data Analysis (EDA):** Examination of variable distributions and feature relationships.

2.  **Data Cleaning:** Implementation of a segmented imputation strategy for missing values (recorded as 0).

3.  **Modeling:** Implementation of machine learning pipelines, comparing ensemble models (`Random Forest`) and linear models (`Logistic Regression`).

4.  **Interpretability (SHAP):** Application of game theory-based methods to explain individual predictions and feature impact.

## 📊 Methodology & Analysis

### Segmented Median Imputation Strategy

For variables such as `Insulin`, `Glucose`, and `BMI`, missing values are imputed using the **segmented median by diagnosis (Outcome)**. This approach preserves the biological signal of each class, ensuring the model maintains the distinction between diabetic and healthy metabolic profiles.

### Statistical Analysis

A **Correlation Matrix (Heatmap)** is used to identify linear relationships and detect multicollinearity.

![Correlation matrix](images/correlation_matrix.png)

Subsequent **boxplot analysis** confirms clear classification signals and validates the median as the most reliable statistic for handling outliers in this dataset.

![Boxplot analysis](images/boxenplots.png)

### Pipelines Architecture

To ensure reproducibility and prevent **data leakage**, the workflow is structured using `Scikit-Learn Pipelines`:

* **Standardization:** `StandardScaler` is applied to normalize variables, a requirement for accurate Logistic Regression coefficient comparison.

* **Automation:** Imputation and scaling are encapsulated within a unified pipeline to ensure robust model deployment.

## ⚙️ Modeling & Results

### Machine Learning Approaches

* **Random Forest:** Used for its ability to handle nonlinear relationships and its resistance to overfitting. Hyperparameters (`max_depth`, `n_estimators`) are optimized via `GridSearchCV` to balance bias and variance.

* **Logistic Regression (Linear Model):** Implemented to obtain a coefficient-based analysis, allowing for a more direct interpretation of the weight each variable contributes to the log-odds of the diagnosis.

* **Permutation Importance:** Permutation importance is calculated as an agnostic validation method. By shuffling a variable and measuring the actual drop in model performance, it is confirmed that the importance attributed to `Glucose` is a predictive reality rather than a bias.

### Clinical Interpretation (SHAP)

**SHAP** is employed to address the “black box” problem in machine learning, allowing for a precise assignment of contribution values to each variable:

* **Summary Plots:** Confirm that high `Glucose` values consistently drive diabetes predictions.

![SHAP Summary Plot](images/SHAP_findings.png)

* **Dependence Plots:** Reveal metabolic synergy, where the risk associated with `Glucose` is significantly amplified by elevated `BMI` and `Insulin`.

![Dependence Plots](images/dependence_plot_glucose.png)

## 🌟 Clinical Insights

The resulting model functions as a proxy for metabolic homeostasis, identifying the "triad of resistance":

1.  **Glucose:** The primary "state marker," representing the end-product of regulatory failure.

2.  **Insulin:** Acts as a compensatory mechanism; high levels often indicate early-stage metabolic struggle.

3.  **BMI & Skin Thickness:** Serve as "load modifiers," where increased adiposity correlates with peripheral insulin resistance.

The model does not merely predict a binary label; it has learned to identify the stages of metabolic deterioration.

### 1. Glucose as a “State Marker”

Glucose stands out as the dominant predictor because it is the end product of regulatory failure. Clinically, it represents hyperglycemia, the diagnostic hallmark of diabetes. The model correctly identifies this point of no return where homeostasis has been compromised.

### 2 and 3. The Metabolic Triad: Insulin, BMI, and Skin Thickness

The true value of the model lies in its ability to interpret the triad of resistance:

* **Insulin:** Acts as a compensatory mechanism. In the early stages, elevated levels attempt to counteract cellular resistance; the model discerns that this compensation, when extreme, is a risk indicator.

* **BMI (Body Mass Index):** Functions as the “load modifier.” The Dependence Plots confirm that the risk associated with insulin is significantly amplified in patients with a high BMI, reflecting how central obesity increases peripheral insulin resistance.

* **Skin Thickness:** Acts as a proxy for subcutaneous adiposity. By incorporating it, the model achieves greater sensitivity: greater skin thickness translates to a larger fat reserve, which metabolically correlates with a pro-inflammatory state and greater difficulty regulating glucose.

## Conclusion

The depth of this model lies in its ability to go beyond a simple correlation. By detecting complex interactions (such as the synergy between insulin, glucose, and BMI), the model serves as a simplified representation of metabolic homeostasis. The predominance of glucose confirms the model’s clinical validity, while the weight assigned to interactions with BMI, insulin, and skin thickness validates its ability to capture the component of insulin resistance typical of the type 2 diabetes phenotype. While glucose serves as a warning sign, the metabolic triad (insulin, glucose, and BMI) provides the physiological context needed to understand why the patient reached that state.

----------------------------------
*Created by Andrea Mendez* 

