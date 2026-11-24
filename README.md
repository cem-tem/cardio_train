# Cardiovascular Disease Classification and Anomaly Detection

How accurately can a classifier identify records labeled with cardiovascular disease, and which measurements deserve a second look? We explored both questions using **70,000 records** in Azure Machine Learning and BigML. The Azure decision forest identified **73.2% of disease-positive records** in its test set. A separate BigML anomaly analysis flagged records with unusually large blood pressure entries, including a diastolic value of **1,100**.

[Read the project report and view the evaluation charts](ML%20course%20term%20paper%20final%203%282%29.pdf)

## Dataset

The [semicolon-delimited CSV](cardio_train.csv) contains an identifier, 11 demographic, measurement and lifestyle fields, and the binary target `cardio`. Age is recorded in days. The fields include height, weight, systolic and diastolic blood pressure, cholesterol, glucose, smoking, alcohol use and physical activity.

| Recorded label | Records |
| --- | ---: |
| Disease present (`cardio = 1`) | 34,979 |
| Disease absent (`cardio = 0`) | 35,021 |

## Classification results

We marked categorical variables, selected `cardio` as the target, and used a 70% training and 30% testing split. In Azure ML Studio, we trained a decision forest with default settings. The report also documents a BigML classifier and its predictions for three additional example records.

| Platform | Test accuracy | Positive class used for precision and recall | Precision | Recall |
| --- | ---: | --- | ---: | ---: |
| Azure ML | 69.4% | Disease present (1) | 67.6% | 73.2% |
| BigML | 73.55% | Disease absent (0) | 71.35% | 77.85% |

Azure reported a ROC AUC of **0.751**. Its confusion matrix shows **2,785 disease-positive records classified as negative** at the 0.5 decision threshold. BigML’s higher reported accuracy comes from its own evaluation split. The report does not establish that both platforms tested on identical rows, and their recall figures refer to different classes.

## What the anomaly detector found

We reviewed the ten highest-scoring records in BigML. The top-ranked record had a diastolic blood pressure entry of 1,100, and the next had an entry of 1,000. These are candidates for source-data verification. An anomaly score measures how unusual a record is within the dataset and does not establish whether its disease label is correct.

## Explore the project

- **Pages 3–4** of the report describe the fields, preprocessing and Azure pipeline.
- **Pages 5–6** show the example predictions, confusion matrices and evaluation metrics.
- **Pages 7–8** show the BigML anomaly ranking and discuss the flagged measurements.

The repository includes the data and the report with screenshots of the cloud workflows. The saved cloud models and exact train/test row assignments are unavailable, so a new run may produce different scores.

**Authors:** Eldar Guliyev and Cem Temel  
**Course:** 4IZ575 Artificial Intelligence in Cloud for Non-Programmers
