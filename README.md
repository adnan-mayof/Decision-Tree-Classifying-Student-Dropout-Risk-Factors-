# Decision Tree Classifying Student Dropout Risk Factors

## Introduction

This project focuses on building a Decision Tree classification model to classify factors or indicators that can identify undergraduate student dropout risk. By analyzing a dataset containing student demographics, academic performance, and socio-economic information, the model categorizes which variables are most critical in determining a student's likelihood of leaving their studies. The goal is to provide an interpretable framework that assists educational institutions in allocating resources efficiently and providing proactive support to at-risk students through early interventions.  

**Note**: You can find the RMarkdown file containing codes and results, as well as the Excel file used in this study, in this repository.


 
## Problem Statement

Student dropout is a significant concern for educational institutions, as it not only affects the individual student's academic progress but also influences resource allocation and institutional planning. Identifying factors contributing to student dropout and building an accurate predictive model can enable timely interventions and support systems, ultimately reducing dropout rates. This project addresses the need for an effective Decision Tree model to classify student dropout risk factors or indicators.

## Dataset Description
The analysis uses a dataset containing **4,424 student records** and **35 numeric variables**, including demographic, academic, financial, and macroeconomic indicators. The dependent variable is **Dropout**, where:

- `1` indicates a student who dropped out
- `0` indicates a student who did not drop out

The main objective of the model is to determine which variables are most influential in predicting dropout and to help educational institutions allocate support resources more effectively.

The dataset includes:

- **1 target variable**
  - `Dropout`

- **34 predictor variables**, including:
  - Demographic factors
  - Academic performance indicators
  - Financial status
  - Enrollment behavior
  - Broader economic indicators

Some of the key predictors include:

- `Curricular_Units_2nd_Sem_Approved`
- `Curricular_Units_1st_Sem_Approved`
- `Curricular_Units_2nd_Sem_Grade`
- `Curricular_Units_1st_Sem_Grade`
- `Tuition_fees_up_to_date`
- `Age_At_Enrollment`
- `Application_Mode`
- `Course`



### Key Question

- What factors or indicators contribute significantly to student dropout, and how can they be classified to identify undergraduate students at risk?


## Method

### Data Collection

The dataset used in this analysis was collected from Kaggle, providing a diverse set of student information. This dataset includes variables such as demographics, academic performance, and socio-economic factors.

1. **Data Source:**  [Kaggle dataset](https://www.kaggle.com/datasets/thedevastator/higher-education-predictors-of-student-retention).
2. **Dataset Description:** This dataset, collected by experts from the [VALORIZA Research Center and Polytechnic Institute of Portalegre](https://zenodo.org/records/5777340#.Y7FJotJBwUE), compiles information on students in diverse undergraduate degrees. It includes details from enrollment, such as academic path and socio-economic factors, as well as academic performance at the first and second semesters. The dataset is designed for building classification models to predict students' dropout and success at the end of the course duration.
3. **Code Description Integration:** Integrating Dataset Column Descriptions and Categories from Damiieibikun's GitHub repository appendix, found [here](https://github.com/Damiieibikun/Student-s-Dropout-Prediction-using-Supervised-Machine-Learning-Classifiers). This repository provides the missing information regarding the categorical labels used in the dataset.



### Data Analysis

The project was implemented in **R** using the following process:

1. Clean the environment and load required libraries
2. Import the dataset
3. Inspect the data structure and variables
4. Split the dataset into:
   - **80% training data**
   - **20% testing data**
5. Build a **Decision Tree classifier** using the `rpart` package
6. Evaluate model performance using training and testing accuracy
7. Extract variable importance and interpret the tree structure

The decision tree uses **Gini impurity** to determine the best splits.

## Model Performance

The model performed well on both training and testing data:

- **Training Accuracy:** 86.63%
- **Testing Accuracy:** 86.21%
- **Difference:** 0.0042

This very small difference suggests that the model has a **good fit** and generalizes well to unseen data, with no strong evidence of overfitting or underfitting.

## Variable Importance

The most important predictors identified by the model were:

1. `Curricular_Units_2nd_Sem_Approved`
2. `Curricular_Units_1st_Sem_Approved`
3. `Curricular_Units_2nd_Sem_Grade`
4. `Curricular_Units_1st_Sem_Grade`
5. `Curricular_Units_2nd_Sem_Evaluations`
6. `Curricular_Units_1st_Sem_Evaluations`
7. `Tuition_fees_up_to_date`

These results show that **academic performance** and **financial stability** are the strongest signals associated with dropout risk.

## Figure 1. Decision Tree for Student Dropout Risk Classification

<img width="700" height="432" alt="000010" src="https://github.com/user-attachments/assets/0cada049-7633-4eac-8519-3ee0c2b7f77c" />


*Figure 1 shows the sequence of decision rules used by the classification model to identify students who are at risk of dropping out and may require intervention.*

## Interpretation of the Decision Tree

The decision tree in Figure 1 shows the logic used by the model to classify students according to dropout risk. The model follows an **if-else structure**, where each split is based on a condition that separates students into lower-risk and higher-risk groups.

The most important factor in the model is **Curricular Units Approved in the 2nd Semester**. This is the root of the tree and the first condition on which all subsequent decisions are based. This indicates that second-semester academic performance is the strongest predictor of student dropout.

The tree first checks whether a student has approved **4 or more second-semester units**.

- **If the condition is met**, the student falls into a relatively low-risk group.
- **If the condition is not met**, the student moves into a higher-risk group, and the model continues splitting based on additional conditions.

For students who passed **4 or more second-semester units**, the next important condition is whether **tuition fees are up to date**.

- If tuition fees are up to date, the student remains in a very low-risk group.
- If tuition fees are not up to date, the risk of dropout increases, even when academic performance is comparatively stronger.

For students who passed **fewer than 4 second-semester units**, the model identifies them as a high-risk group and applies additional decision rules.

The next major condition is again **tuition fee status**:

- If tuition fees are **not up to date**, the student falls into the **highest-risk group** in the tree.
- If tuition fees **are up to date**, the model continues splitting based on further academic and demographic conditions.

Among these students, the tree considers whether the student passed at least **2 second-semester units**. If not, the model then considers **Age at Enrollment** to refine the risk classification. This suggests that age plays a secondary role in distinguishing risk among students already showing weak academic progress.

If the student passed at least **2 second-semester units**, the model next checks **1st Semester Enrollment**. This indicates that earlier academic engagement also contributes to the risk profile. Students with very low first-semester enrollment remain highly vulnerable, even when they meet some of the later academic thresholds.

Overall, the tree demonstrates that the model prioritizes decisions in the following order:

1. **Second-semester academic performance**
2. **Tuition payment status**
3. **Age at enrollment**
4. **First-semester enrollment behavior**

This structure shows that dropout risk is driven primarily by a combination of **academic underperformance** and **financial instability**.

## Key Findings

The project reveals several important findings:

- **Second-semester academic success** is the strongest predictor of whether a student will remain enrolled or drop out.
- Students with **fewer approved second-semester units** are much more likely to be at risk.
- **Tuition fees not being up to date** significantly increases dropout risk.
- Even among students with similar academic profiles, financial status can sharply distinguish lower-risk students from higher-risk students.
- Additional variables such as **age at enrollment** and **first-semester enrollment levels** help refine the model, but they are less influential than academic progress and financial status.

## Stakeholder Recommendations

Based on the results of the decision tree, the following recommendations can be made for university management, academic leaders, student support units, and policy stakeholders.

### 1. Prioritize academic monitoring in the second semester

Since `Curricular_Units_2nd_Sem_Approved` is the most important predictor in the model, institutions should closely monitor student academic performance during the second semester.

**Recommendation:**
- Flag students with low numbers of approved second-semester units for immediate review
- Use second-semester progression as an early warning signal

### 2. Link academic risk monitoring with financial support systems

The tree shows that **tuition fee status** is one of the most important secondary conditions affecting dropout risk.

**Recommendation:**
- Integrate financial alerts with academic intervention systems
- Identify students who are both academically underperforming and behind on tuition payments
- Provide targeted fee support, flexible payment options, or financial counseling

### 3. Target the highest-risk group for urgent intervention

Students with **poor second-semester performance and unpaid tuition fees** represent the most critical group in the model.

**Recommendation:**
- Treat this group as a top priority for institutional intervention
- Provide coordinated academic, financial, and advising support

### 4. Develop an early warning system

The decision tree offers clear and interpretable rules that can be used operationally.

**Recommendation:**
- Convert the model rules into a student risk dashboard
- Track students using factors such as approved units, tuition status, age, and enrollment activity
- Trigger alerts for advisors and student support teams

### 5. Strengthen first-year and early-stage engagement

The presence of first-semester enrollment as a later split suggests that early academic engagement still matters.

**Recommendation:**
- Monitor enrollment intensity and engagement from the first semester
- Support students who show signs of weak participation early in their academic journey

## Conclusion

This project demonstrates that a Decision Tree model can provide a clear and interpretable framework for understanding student dropout risk. The findings show that dropout is most strongly associated with **academic performance in the second semester**, followed by **tuition fee status** and other secondary factors such as age and early enrollment behavior.

Because the model is both accurate and easy to interpret, it can serve as a valuable decision-support tool for educational institutions seeking to identify at-risk students and apply timely interventions to improve retention outcomes.
