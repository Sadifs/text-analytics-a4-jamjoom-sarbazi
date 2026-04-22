# Work Division — Assignment 4 (NER)

## Team Members

Aziza Jamjoom
Sadaf Sarbazi

---

## Project Overview

We worked collaboratively on all major components of this project, from dataset selection to model evaluation. Early on, we explored multiple dataset options and jointly decided to use the Broad Twitter Corpus because of our shared interest in social media analytics and the unique challenges associated with informal, user-generated text.

---

## Data Exploration & Setup

Both team members participated in exploring the dataset, understanding its structure, and identifying key preprocessing steps such as filtering non-English tweets and removing noise (e.g., emojis). We also reviewed baseline model performance together to better understand the complexity of the task.

---

## Annotation Process

The annotation work was divided evenly between both team members. Each of us manually annotated a subset of tweets using Human Signal, with an overlap portion to measure inter-annotator agreement.

Throughout the annotation process, we worked closely together to refine our annotation guidelines. We regularly discussed edge cases (e.g., distinguishing between ORG vs PROD, handling Twitter handles, and labeling creative works) and updated our guidelines iteratively to ensure consistency and clarity. This collaborative approach contributed to achieving a strong inter-annotator agreement.

---

## Modeling & Evaluation

Both team members contributed to implementing and evaluating the models, including the CRF, Bi-LSTM, and fine-tuned Transformer. We worked together to interpret results, analyze performance metrics, and conduct error analysis.

One challenge we encountered was with the Bi-LSTM model, which collapsed to predicting only non-entity (“O”) labels due to class imbalance and limited training data. We attempted to address this by adjusting model parameters and training configurations; however, these changes negatively impacted the performance and stability of the other models.

Given these trade-offs, we decided to maintain a consistent modeling pipeline and proceed with the original configurations to ensure fair comparison across models.

---

## Collaboration Summary

Overall, this project was highly collaborative. Key decisions — including dataset selection, annotation guidelines, and model evaluation — were made jointly. Tasks such as annotation were divided for efficiency, while discussions and refinements were done together to maintain consistency and quality across all components of the project.

---

