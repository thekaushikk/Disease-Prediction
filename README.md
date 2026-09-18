Disease Prediction Using Unsupervised Clustering (K-Means)
Overview

This project explores whether patients can be meaningfully grouped by symptom similarity using unsupervised K-Means clustering, without relying on their known disease labels during training. The goal is to simulate how clustering could help identify patient groups with shared symptom profiles — useful for early risk detection, preventive care triage, or spotting hidden patterns in health data.

Dataset
Size: 2,000 patient records
Features (10 binary symptoms): fever, headache, nausea, vomiting, fatigue, joint pain, skin rash, cough, weight loss, yellow eyes
Target (not used for training): disease label (categorical, encoded for analysis only)
Tech Stack
Python
Pandas, NumPy
scikit-learn (KMeans, StandardScaler, LabelEncoder, silhouette_score)
Matplotlib, Seaborn
Methodology
Preprocessing
Removed non-predictive identifiers.
Label-encoded categorical columns.
Standardized all features using StandardScaler so no single symptom dominates distance calculations.
Choosing k
Used the Elbow Method (SSE vs. number of clusters) to select an appropriate number of clusters.
Selected k = 3 based on the elbow curve.
Clustering
Applied KMeans(n_clusters=3, random_state=42) to the scaled feature set.
Assigned each patient to one of three clusters.
Evaluation
Computed the Silhouette Score to assess cluster separation.
Built a correlation heatmap to examine relationships between symptoms, disease labels, and cluster assignments.
Key Findings
Fatigue showed the strongest correlation with disease outcome (~0.86), followed by weight loss (~0.64) and fever/nausea (~0.70 between each other).
Headache, skin rash, and cough showed weak correlations with disease outcome, suggesting they're less reliable standalone predictors in this dataset.
Disease labels correlated only mildly with cluster assignment (~0.22), indicating clusters captured some real structure, but not a strong one-to-one mapping to actual diagnoses.
Limitations (Important)

This project is exploratory, and its limitations were deliberately analyzed rather than glossed over:

Silhouette Score was low (~0.09), indicating weak cluster separation — clusters overlapped more than a strong clustering result would show.
K-Means assumes continuous, roughly spherical clusters, which is a mismatch for mostly binary/categorical symptom data. Distance-based methods like K-Means often underperform on this data type compared to alternatives such as K-Modes or hierarchical clustering with Jaccard distance.
The disease label was label-encoded and included in correlation analysis; since label encoding assigns arbitrary integer codes to categories, correlations involving the disease column should be interpreted cautiously rather than as strict linear relationships.
What This Project Demonstrates
End-to-end unsupervised ML workflow: data preprocessing → scaling → cluster selection → model fitting → evaluation → interpretation.
Practical use of the Elbow Method and Silhouette Score for validating clustering choices.
Critical evaluation of model results, including recognizing when a method (K-Means) may not be the best fit for the data type (binary symptoms), and what alternatives would be worth trying next.
Possible Extensions
Try K-Modes or K-Prototypes for better handling of categorical/binary features.
Use hierarchical clustering with a Jaccard or Hamming distance metric.
Apply dimensionality reduction (PCA, UMAP) before clustering to improve separation.
Compare unsupervised clustering results against a supervised classifier (e.g., Random Forest) trained on the same features, to benchmark performance.
Disclaimer

This project is for educational and exploratory purposes only. It is not a diagnostic tool and should not be used for real medical decision-making.
