
## DISEASE PREDICTION AND SPECIALIST RECOMMENDATION SYSTEM
> **_Predict the disease, identify the right specialist, and recommend the best doctor from structured healthcare data._**

Disease Prediction and Specialist Recommendation System is a **machine learning-based healthcare decision-support project** that predicts a likely disease from user-entered symptoms, maps that disease to the most relevant medical specialist, and then recommends a top-ranked doctor using structured doctor profile data. The project was built as an end-to-end pipeline so the system does not stop at classification alone, but continues into actionable recommendation.

**Project Timeline:** Developed and completed between **March 28, 2025** and **April 26, 2025** as an academic project for my **Machine Learning course** during my **Master’s program**.

---

## Overview

**Disease Prediction and Specialist Recommendation System** is an integrated machine learning project that combines **symptom-to-disease learning**, **disease-to-specialist mapping**, and **doctor ranking** into one connected workflow. Many disease prediction projects only stop at the classification stage and only return a disease label. This project extends the result into a more practical healthcare support pipeline by also telling the user **which specialist to consult next** and, where matching doctor data is available, **which doctor can be recommended first**.

The system starts by reading symptom-based disease data, converting raw symptom columns into a binary feature matrix, and training multiple machine learning algorithms on the processed dataset. Once a disease is predicted, the project uses a disease-versus-specialist mapping table to identify the correct specialist. Finally, doctor profile data, satisfaction values, ratings, availability, and qualification-based scoring are used to rank doctors and return a top recommendation.

This project is stronger than a standalone classifier because it connects **prediction with recommendation**, making the workflow more meaningful from a user perspective.

---

## Problem Statement

A user may know their symptoms, but not necessarily:

- what disease those symptoms indicate
- which specialist is the right one to consult
- or which doctor should be preferred from the available options

This project addresses that gap by building a complete recommendation flow where:

1. The user enters symptoms
2. The system predicts the most likely disease
3. The disease is mapped to a specialist
4. The system recommends a top-ranked doctor from the doctor dataset

This transforms a pure classification problem into a more practical **healthcare recommendation prototype**.

---

## Project Highlights

- **4920** symptom-disease records used for the main prediction dataset
- **41** diseases in the primary disease dataset
- **131** unique symptoms extracted for training
- Binary encoded feature matrix expanded to **4920 × 132**
- **5** machine learning models trained and evaluated
- **70% / 30%** train-test split used for performance evaluation
- **41** disease-to-specialist mappings built from the mapping dataset
- **16** unique specialist labels in the disease-specialist mapping file
- **19** specialist entries in the specialist reference file
- **563** doctor profile rows in the doctor dataset
- **78** unique doctor names identified
- **23** specialist types present in the doctor dataset
- **107** specialist categories in the specialist count dataset
- **23,908** total available doctor counts summed from the specialist count file
- **100% accuracy** observed for all 5 trained models on the uploaded processed dataset split
- Doctor satisfaction score range: **67% to 100%**
- Average doctor satisfaction score: **97.40%**
- Doctor ratings range: **0 to 832**
- Average ratings value: **197.54**

---

## Key Features

### Disease Prediction
- Accepts user-entered symptoms
- Converts symptoms into binary feature vectors
- Predicts disease using multiple machine learning models
- Uses majority voting for more robust final prediction
- Displays prediction confidence based on model agreement

### Specialist Recommendation
- Maps predicted disease to the relevant medical specialist
- Automatically guides the user on which doctor specialization to consult next
- Example: **Migraine → Neurologist**

### Doctor Recommendation
- Ranks doctors using structured doctor profile data
- Uses satisfaction, ratings, availability, and qualification-based scoring
- Returns the best doctor where specialist overlap exists between the specialist mapping and the doctor dataset

### Multi-Dataset Integration
- Combines multiple healthcare-related files into one end-to-end workflow:
  - symptom-to-disease dataset
  - symptom reference dataset
  - disease-to-specialist mapping dataset
  - specialist directory dataset
  - doctor profile ranking dataset
  - specialist availability dataset

---

## Dataset Overview

The project integrates multiple structured files to create a complete disease prediction and specialist recommendation pipeline.

### 1. `Original_Dataset.csv`
Primary disease prediction dataset.

- **4920 rows**
- **41 diseases**
- Up to **17 symptom columns** per record
- Each disease appears **120 times**
- Perfectly balanced class distribution
- Used as the main training dataset for disease classification

### 2. `Symptom_Weights.csv`
Symptom reference dataset.

- **130 rows**
- Stores symptom-related entries used as reference/support data
- Useful for future symptom weighting and severity-based extensions

### 3. `Doctor_Versus_Disease.csv`
Disease-to-specialist mapping dataset.

- **41 rows**
- **16 unique mapped specialist labels**
- Used to build the disease → specialist lookup dictionary

### 4. `Doctor_Specialist.csv`
Specialist reference dataset.

- **19 specialist entries**
- Used as supplementary specialist reference data

### 5. `PakistanSurgerySpecialist.csv`
Doctor profile dataset.

- **563 total rows**
- **78 unique doctor names**
- **23 specialist types**
- Includes doctor names, specialist type, ratings, qualifications, availability, and satisfaction values

### 6. `pk_medical_specialist_counts.csv`
Specialist availability dataset.

- **107 rows**
- **107 unique specialist categories**
- **23,908** total available doctor counts combined across all listed categories

### 7. `Specialist.xlsx`
Supplementary integrated dataset.

- **4920 rows × 133 columns**
- Useful for extended analysis and merged workflow experimentation

---

## Data Preprocessing

The preprocessing stage converts raw symptom records into a machine-learning-ready format.

### Steps Performed

1. Load the disease dataset into a Pandas DataFrame
2. Fill missing symptom fields with `0`
3. Flatten all symptom columns to identify unique symptoms
4. Extract **131 unique symptoms**
5. Create a binary symptom matrix where:
   - `1` = symptom present
   - `0` = symptom absent
6. Build the encoded disease-symptom dataset of size **4920 × 132**
7. Split the data into **70% training** and **30% testing**

### Why This Matters

The original dataset stores symptoms across separate columns like `Symptom_1`, `Symptom_2`, etc. Machine learning models perform better when each possible symptom becomes its own independent feature column. That is why the project transforms the raw data into a binary encoded feature space.

---

## Machine Learning Models Used

The project trains multiple models and combines their outputs using majority voting.

### 1. Logistic Regression
- Used as a linear classification baseline
- Estimates disease probability from symptom patterns
- Strong baseline for structured tabular data

### 2. Random Forest Classifier
- Ensemble learning algorithm using multiple decision trees
- Improves robustness and reduces overfitting
- Effective for structured symptom combinations

### 3. Support Vector Machine (SVM)
- Finds separating boundaries between disease classes
- Useful when disease classes are separable in feature space

### 4. K-Nearest Neighbors (KNN)
- Predicts disease based on closest similar cases
- Works through similarity between symptom profiles

### 5. Naive Bayes
- Probabilistic classifier based on Bayes' theorem
- Simple, fast, and effective baseline model

---

## Model Performance

The notebook output shows the following accuracies on the processed dataset:

- **Logistic Regression:** `1.0000` (**100.00%**)
- **Random Forest:** `1.0000` (**100.00%**)
- **Support Vector Machine:** `1.0000` (**100.00%**)
- **K-Nearest Neighbors:** `1.0000` (**100.00%**)
- **Naive Bayes:** `1.0000` (**100.00%**)

### Final Prediction Strategy

Instead of relying on a single model, the system uses **majority voting across all 5 models** to generate the final disease result. Prediction confidence is shown as the percentage of models agreeing on a disease label.

### Important Note on Accuracy

These perfect scores are promising for the uploaded dataset, but they should **not** be treated as clinical validation. The dataset is highly structured and balanced, so real-world healthcare deployment would still require external validation, larger datasets, and medical review.

---

## Specialist Recommendation

After disease prediction, the system maps the predicted disease to the correct specialist using `Doctor_Versus_Disease.csv`.

### Mapping Statistics

- **41 diseases** mapped to specialists
- **16 unique specialist labels**
- Example mappings:
  - `Acne → Dermatologist`
  - `Hyperthyroidism → Endocrinologist`
  - `Migraine → Neurologist`
  - `Chronic Cholestasis → Hepatologist`

### Recommendation Logic

A dictionary lookup is used to convert the predicted disease into a specialist recommendation. This creates the second stage of the healthcare support pipeline.

---

## Doctor Ranking and Recommendation

The final stage recommends a doctor based on specialist match and ranking score.

### Doctor Dataset Statistics

From `PakistanSurgerySpecialist.csv`:

- **563** total doctor profile rows
- **78** unique doctor names
- **23** specialist types
- Satisfaction score range: **67% to 100%**
- Average satisfaction score: **97.40%**
- Ratings range: **0 to 832**
- Average ratings value: **197.54**

### Ranking Logic Used

The notebook applies two recommendation styles.

#### Basic Recommendation Score

```text
Recommendation Score = 0.5 × Normalized Ratings + 0.5 × Normalized Satisfaction
````

#### Advanced Recommendation Score

```text
Recommendation Score = 0.3 × Normalized Ratings + 0.3 × Normalized Satisfaction + 0.2 × Normalized Availability + 0.2 × Normalized Qualification Score
```

### Qualification Scoring Includes

The notebook assigns weights to common medical qualification keywords such as:

* `MBBS`
* `FCPS`
* `MD`
* `Diploma`
* `MRCOG`
* `Fellowship`

### Current Specialist Overlap for Doctor Recommendation

Although the disease-specialist mapping covers more specialist types, the current doctor recommendation pipeline has clean direct overlap mainly for these **4 specialist categories**:

* **Cardiologist**
* **Dermatologist**
* **Gastroenterologist**
* **Gynecologist**

That means:

* **Disease prediction and specialist recommendation work across the mapped disease set**
* **Doctor recommendation is strongest for these overlapping specialist categories**
* For some diseases, the system may recommend the correct specialist even when a doctor is not returned from the filtered ranking data

### Top Specialist Availability Examples

From `pk_medical_specialist_counts.csv`:

* **General Physician:** 2491 available doctors
* **Dentist:** 1948 available doctors
* **Psychologist:** 1898 available doctors
* **General Practitioner:** 1843 available doctors
* **Gynecologist:** 1685 available doctors

---

## User Flow and Prediction Pipeline

### High-Level Workflow

1. User enters the number of symptoms
2. User enters symptoms one by one
3. Symptoms are converted into a binary feature vector
4. All 5 trained models predict disease independently
5. Majority voting calculates disease confidence percentages
6. The predicted disease is mapped to a specialist
7. A doctor is selected from the ranked doctor list where matching specialist data is available
8. Final output is displayed with:

   * Predicted Disease
   * Prediction Confidence (%)
   * Recommended Specialist
   * Doctor Name

---

## Tech Stack

* **Language:** Python
* **Environment:** Jupyter Notebook
* **Libraries:**

  * Pandas
  * NumPy
  * Scikit-learn
  * Matplotlib
  * Seaborn
  * OpenPyXL

---

## Repository Structure

```bash
Disease-Prediction-and-Specialist-Recommendation/
│
├── README.md
├── Disease_Prediction_and_Specialist_Recommendation.ipynb
├── data/
│   ├── Original_Dataset.csv
│   ├── Symptom_Weights.csv
│   ├── Doctor_Versus_Disease.csv
│   ├── Doctor_Specialist.csv
│   ├── PakistanSurgerySpecialist.csv
│   ├── pk_medical_specialist_counts.csv
│   └── Specialist.xlsx
│
├── outputs/
│   ├── doctor_ranking_results.csv
│   ├── prediction_results.csv
│   └── plots/
│
└── requirements.txt
```

---

## Setup and Installation

### Prerequisites

* Python **3.9+**
* Jupyter Notebook or JupyterLab
* Required Python libraries installed

### Install Dependencies

```bash
pip install pandas numpy scikit-learn matplotlib seaborn openpyxl jupyter
```

### Project Setup

1. Clone the repository

```bash
git clone <your-repo-url>
cd Disease-Prediction-and-Specialist-Recommendation
```

2. Place all dataset files inside the `data/` folder

3. Open Jupyter Notebook

```bash
jupyter notebook
```

4. Run the notebook cells in sequence

---

## How to Run

1. Open the notebook
2. Load all required datasets
3. Run preprocessing to build the binary symptom matrix
4. Train the machine learning models
5. Execute the final prediction function
6. Enter the number of symptoms
7. Enter symptom names exactly as expected by the symptom list
8. View the output with disease, confidence, specialist, and doctor recommendation

---

## Example Output Format

```text
Predicted Disease | Prediction Confidence (%) | Recommended Specialist | Doctor Name
```

### Example Interpretation

* If most models agree on **Migraine**, the system recommends **Neurologist**
* If that specialist has matching doctor data in the ranking dataset, the system also returns the **top-ranked doctor**

---

## Testing and Evaluation

### What Was Evaluated

* Binary symptom encoding pipeline
* Disease prediction performance across 5 models
* Disease-to-specialist mapping correctness
* Ranked doctor retrieval based on specialist match
* End-to-end pipeline from symptom input to doctor recommendation

### Observed Results

* All **5 models achieved 100.00% accuracy** on the processed dataset split
* The specialist recommendation stage successfully maps diseases to specialists using the lookup dataset
* Doctor recommendation works best for the overlapping specialist categories available in the doctor profile dataset

---

## Limitations

* This is a **decision-support prototype**, not a clinical diagnostic tool
* Perfect accuracy on a structured dataset does not guarantee real-world medical reliability
* Doctor recommendation currently has strongest direct coverage for **4 overlapping specialist categories**
* The system does not currently use:

  * patient history
  * age
  * gender
  * symptom severity
  * symptom duration
  * lab reports
  * real-time hospital availability
* Some specialist labels across files still need better normalization for full-scale deployment

---

## Future Enhancements

Possible improvements for the next version:

* Build a **web application** using Flask, Streamlit, or React with backend API
* Add **symptom severity weighting** and duration-based logic
* Integrate **live hospital and doctor APIs**
* Improve specialist normalization across all datasets
* Expand doctor recommendation coverage beyond the current overlapping categories
* Add **top-N doctor recommendation**
* Include **model explainability**
* Use **cross-validation**, confusion matrix, precision, recall, and F1-score
* Add chatbot or voice-based symptom input
* Introduce emergency triage support and stronger medical disclaimers

---

## Medical Disclaimer

This project is for **academic, educational, and demonstration purposes only**. It is not a substitute for professional medical advice, diagnosis, or treatment. The outputs should be treated as prototype recommendations and not as clinically approved medical decisions.

---

## Contributors

**Machine Learning Project Team**

* Komatlapalli Venkata Naga Sri
* Gadipudi Sandeep
* Monavarthy Rama Sai Surya Teja

---

## Acknowledgements

* Healthcare datasets used for symptom-to-disease prediction and specialist mapping
* Structured doctor profile data used for ranking and recommendation
* Scikit-learn for machine learning model development
* Pandas and NumPy for preprocessing and feature engineering

```


