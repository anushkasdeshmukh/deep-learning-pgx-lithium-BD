**Methodology**
This project employs a hybrid study design that combines retrospective data analysis with prospective cohort recruitment to develop and validate a DL-based PGx model for predicting lithium response in individuals with BD. Our objective is to integrate genomics, epigenomics, transcriptomics, and clinical data to build a predictive model that classifies lithium responders and yields interpretable biological insights.

**1. Study Design Overview**
The study has two phases:
(1) Retrospective phase: model pre-training using existing retrospective datasets, and
(2) Prospective phase: fine-tuning and validation using data from 100 newly recruited BD patients.
A target of 100 participants aligns with recent PGx studies demonstrating feasibility of DL approaches in psychiatric cohorts of 60-100 patients. This sample balances statistical power with pilot-study practicality.
Retrospective data will be drawn from the International Consortium on Lithium Genetics (ConLiGen), which includes ~2,500 genotype-labeled patients, and the Pharmacogenomics of Bipolar Disorder (PGBD) study, which includes 345 patients treated with lithium and detailed clinical metadata. These datasets will be used to pre-train a multilayer neural network using genotype and clinical features.
The prospective phase addresses the limitations of retrospective data (e.g., heterogeneity, missing omics layers) by collecting standardized, high-resolution data, including RNA sequencing, methylation profiling, and clinical phenotyping, from 100 lithium-naïve BD patients. These data will fine-tune and validate the model in a real-world context.

**2. Data Sources and Cohort Recruitment**
Retrospective datasets will be used to extract single-nucleotide polymorphisms (SNPs), clinical features, and, where available, transcriptomic or methylation data. Lithium response will be labeled using the Alda scale, with responders defined as those scoring ≥7.
The prospective cohort will consist of 100 patients diagnosed with bipolar I or II disorder (DSM-5 criteria), initiating or currently receiving lithium monotherapy. Patients must be free of unstable medical conditions or contraindications. Informed consent will be obtained for clinical and molecular data collection. Participants will undergo a baseline visit, biospecimen collection, and follow-up every 6 months for outcome tracking and label refinement.

**3. Multi-Omics and Clinical Data Collection**
Whole-blood RNA-seq will measure gene expression, emphasizing pathways related to mitochondrial function and circadian regulation. Blood samples will be collected at consistent times to minimize variability, and transcript counts will be normalized (e.g., TPM).
Genome-wide DNA methylation will be assessed via the Illumina MethylationEPIC array (850K CpGs). Preprocessing will include background correction, probe filtering, and cell-type adjustment. Prior findings on differentially methylated regions (DMRs) related to lithium response will guide feature selection.
Clinical data will include demographics, diagnostic subtype, illness duration, comorbidities, symptom scales (YMRS, MADRS, CGI-BP), treatment history, thyroid/renal function, and adherence measures (pill counts, serum levels). Longitudinal follow-up will capture mood state, function, and side effects at 6-month intervals. Where feasible, repeat biospecimen collection will support modeling of time-varying biological changes.

**4. Outcome Definition and Label Harmonization**
In the retrospective datasets, outcomes will be labeled using the Alda scale. In the prospective cohort, lithium response will be defined as ≥6 months of therapy with ≥50% symptom reduction and CGI-BP ratings of “much improved” or “very much improved.” Partial responders will be tracked separately. Harmonized labeling will support joint modeling across cohorts.

**5. Data Integration and Feature Selection**
To align modalities across datasets, we will apply batch correction techniques (e.g., ComBat, limma) and normalize transcriptomic or epigenomic data for platform differences. Genotype data will be used to derive polygenic risk scores.
We will use a late-fusion architecture, where each data type (gene expression, methylation, clinical) is first processed independently before integration into the final model. Feature selection will include:
Univariate filtering (e.g., low-variance removal)
Biological prioritization (literature-supported markers)
Embedded methods (LASSO, random forest importance)
Dimensionality reduction (PCA, autoencoders)
The goal is to reduce thousands of raw features to a final model input of 50-100 informative variables.

**6. Model Development and Training**
We will build a multilayer feed-forward neural network (MFNN) optimized for high-dimensional tabular data. Each data modality will feed into dedicated sub-networks, followed by shared dense layers. The architecture will include 2-3 hidden layers with ReLU activations and a sigmoid output for binary classification. Regularization techniques (dropout, L2) and the Adam optimizer will be used during training.
Model development will occur in two stages:
Stage 1: Pre-train on retrospective data to learn broad clinical and genetic patterns.
Stage 2: Fine-tune on prospective multi-omic data.
The prospective set will be split 50/25/25 for training, validation, and testing. We will use 10-fold cross-validation for hyperparameter tuning, apply early stopping to prevent overfitting, and address class imbalance (~30% responders) using class weighting and/or SMOTE.

**7. Model Evaluation and Interpretability**
Performance will be evaluated on the held-out test set using AUROC (primary metric), accuracy, sensitivity, specificity, precision, and F1 score. Calibration plots and 95% confidence intervals (via bootstrapping) will be reported. Model interpretability will be assessed using SHAP (SHapley Additive exPlanations) to identify which features contribute most to predictions, globally and per patient, ensuring alignment with known biology.

**8. Longitudinal Follow-Up and Validation**
Patients will be followed every 6 months for up to 36 months. If a patient’s clinical status changes (e.g., initial response followed by relapse), labels will be updated. These new data will support model retraining, enhancing generalizability. We may also validate the model using external datasets or temporally withheld subsets to simulate real-world deployment.

**9. Ethics and Data Governance (Canadian-Aligned)**
This study will undergo REB approval in compliance with Canadian regulations, including the Tri-Council Policy Statement (TCPS 2). All participants will provide informed consent for genomic and clinical data use. Data will be anonymized, encrypted, and stored securely under PIPEDA guidelines. No individual results will be returned. Equity will be prioritized in recruitment, and fairness will be monitored during model development to mitigate bias across demographic subgroups.


