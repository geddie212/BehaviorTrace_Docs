# BehaviorTrace — State Confirmation Study Guide

BehaviorTrace is a platform for running **state confirmation (EMA) studies** using wearable
biosignals collected from **EmotiBit** devices. Participants label their current state via a
Progressive Web App (PWA) while biosignals are recorded and later used for machine learning
model training and prediction.

This README provides a **high-level, four-step pathway** for study administrators to go from
initial setup to training and testing a prediction model.

> ⚠️ **Important**
> - EmotiBit devices must be **fully configured and operational** before beginning.
> - The current version (**v1.0**) supports **EMA / state confirmation labels only**.
> - Model training uses a **window / stride–based strategy** for mixed-frequency biosignals.

---

## Study Workflow Overview

### [Step 1 — Initial Platform Setup](initial_setup.md)
Set up the BehaviorTrace web app, database, and deployment.


---

### [Step 2 — Study Setup (EMA / State Confirmation)](study_setup.md)
Create the study, define EMA state labels, and prepare the participant-facing app.

---

### [Step 3 — Data Upload (EmotiBit SD Cards → SQL)](data_upload.md)
Process and upload all biosignal data to the SQL database.


---

### [Step 4 — Model Training & Prediction](training_and_prediction.md)
Train and test a machine learning model using EMA labels and biosignals.


---

## Repository

https://github.com/geddie212/BehaviorTrace
