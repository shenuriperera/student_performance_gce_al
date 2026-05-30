# G.C.E. A/L Exam 2020 Student Performance Simulator & Analytics

![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)
![Data-Science](https://img.shields.io/badge/Data--Science-Analytics-green.svg)
![Machine-Learning](https://img.shields.io/badge/Machine--Learning-Predictive-orange.svg)

## 📝 Project Overview
This repository contains a comprehensive data science and predictive analytics workflow evaluating national performance metrics from the **2020 G.C.E. Advanced Level (A/L) Examination in Sri Lanka**. Utilizing anonymized student records, this project uncovers the structural, pedagogical, and demographic factors impacting academic success (Z-scores) and university admission eligibility. 

Additionally, the repository builds and compares state-of-the-art machine learning models to accurately predict individual Z-scores based on background features and discrete subject grades.

---

## 🎯 Core Research Objectives
1. **Academic Stream Evaluation:** Analyze the statistical distribution of final Z-scores across different fields of study (Arts, Commerce, Physical Sciences, Biological Sciences, Biosystems, and Engineering Technology)[cite: 1, 2].
2. **Demographic Disparity Assessment:** Isolate the impact of gender and age on final scores.
3. **Curriculum and Aptitude Insight:** Investigate performance differences between the New vs. Old syllabus structures and measure the correlation between the Common General Test (CGT) and Z-scores[cite: 1, 2].
4. **University Eligibility Modeling:** Identify the key parameters influencing a student's likelihood of qualifying for state university entrance[cite: 2].

---

## 📂 Repository Structure
```text
├── data/
│   ├── original.csv                        # Raw, uncleaned initial student performance dataset
│   ├── cleaned_data.csv                    # Dataset after logical imputation and cleaning routines
│   └── final_stratified_sample.csv         # Calculated and extracted representative stratified sample
├── notebooks_and_scripts/
│   └── al_student_performance_analysis.ipynb # Complete Python workflow (Preprocessing, EDA, Stats, and ML modeling)

---

## 🛠️ Data Preprocessing & Sampling Methodology
To combat systemic issues within the raw national dataset, a stringent pipeline was executed:
* **Feature Engineering & Deletion:** High-null fields like `island_rank` and `district_rank` were eliminated. Age metrics were generated dynamically using student birth parameters.
* **Logical Imputation:** Missing fields in the `stream` column were reconstructed by grouping records according to the unique combinations of the three distinct core subject selections.
* **Stratified Sampling:** To manage computational execution while preserving system representation, Cochran’s formula was applied to fetch a representative sample size ($n=383$) stratified across `stream` and `syllabus` partitions.

---

## 📊 Key Findings from Exploratory Data Analysis (EDA)

* **Skews in Performance:** Final Z-score distribution across the nation behaves with a noticeable positive skew, signaling tight bottlenecks to achieve exceptional top-tier marks.
* **Performance by Stream:** The **Physical Science** stream displayed the highest median Z-score performance, whereas the Arts and Biological Sciences fields contained the most significant variability in results.
* **Gender Demographics:** Females dominate the sampled space at **64.2%** of enrollment and maintain higher overall median Z-scores compared to their male peers.
* **University Eligibility:** A striking **81.7%** of students within the sample qualified for university entry (earning $\ge 3$ 'S' passes). The **Physical Science** stream achieved a **100% eligibility rate** within our sample.

---

## 🧠 Statistical & Advanced Analytics

### 1. Parametric Evaluation of Stream Performance (ANOVA & Tukey's HSD)
A One-Way ANOVA confirmed that average Z-scores vary significantly among disciplines ($F = 4.486, p = 0.0006$). A Post-Hoc Tukey HSD test isolated the performance gap specifically between **Physical Science & Commerce**, as well as **Engineering Technology & Physical Science** ($p < 0.05$).

### 2. University Eligibility Dynamics (Logistic Regression)
A compiled Logit model isolated the log-odds of a student achieving baseline criteria for state campus allocation. 
$$\ln\left(\frac{p}{1-p}\right) = 2.235 - 0.605(\text{Male}) - 1.292(\text{Biosystems}) - 1.050(\text{Commerce}) - 1.140(\text{Eng. Tech}) - 0.065(\text{Science})$$
* Male candidates feature a **45% lower chance** of securing university eligibility compared to female counterparts across identical settings.
* Students tracking the Commerce, Biosystems, and Engineering Technology pipelines exhibited significantly lower odds of eligibility compared to the baseline Arts stream.

---

## 🚀 Machine Learning Predictive System (Z-Score Prediction)

Five standalone machine learning pipelines were trained on categorical data, metadata, and final subject performance tiers to forecast continuous absolute Z-scores. 

| Model | $R^2$ Score | Mean Absolute Error (MAE) | Hit Rate ($\pm 0.2$ Margin) |
| :--- | :---: | :---: | :---: |
| **Ridge Regression** | **92.19%** | **0.1644** | **71.43%** |
| Decision Tree | 82.46% | 0.2534 | 46.75% |
| Random Forest | 91.13% | 0.1833 | 59.74% |
| Gradient Boosting | 92.96% | 0.1638 | 64.94% |
| K-Nearest Neighbors (KNN) | 84.10% | 0.2521 | 44.16% |

### 🏆 Model Winner: Ridge Regression
While Gradient Boosting provided marginally cleaner raw accuracy readings ($92.96\%$), **Ridge Regression** proved to be the most robust architecture for true generalization. It achieved a superior **71.43% Hit Rate** in keeping margin error bound tighter than $\pm 0.2$ units on raw unseen testing distributions.

---

## 💻 Technical Setup & Installation

### Prerequisites
Ensure you have Python 3.8 or higher installed on your environment.

### Installation
1. Clone the repository to your local directory:
   ```bash
   git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
   cd your-repo-name
2. Install all required dependencies:
   ```bash
   pip install -r requirements.txt
├── reports/
│   └── student_performance_report.pdf      # Detailed final written project analysis and findings
└── README.md                               # Project documentation (this file)
3. Run the notebook file:
jupyter notebook notebooks_and_scripts/codes_forAnalysis.ipynb
👥 Authors & Project Team
Shenuri Perera - s16661
Oshini Jayathunga - s16807
Sandani Gunasekara - s16903
Amashi Fernando - s16979
Department of Statistics, University of Colombo
