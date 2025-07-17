Loan Default Predictor

**Author:** Ikachu
**Date:** July 17, 2025

---
### **Project Overview**

This repository contains the complete end-to-end project for building and deploying a machine learning model to predict loan defaults. The goal is to leverage supervised learning on structured financial data to identify high-risk loan applicants, enabling a fintech company to make smarter lending decisions and reduce financial losses.

The project follows a structured development process, culminating in a production-ready REST API that can serve real-time predictions.

---
### **Final Product: A Live API**

The final output of this project is a live API built with **FastAPI**.

* **Endpoint**: `/predict`
* **Method**: `POST`
* **Input**: A JSON object containing a new loan applicant's details.
* **Output**: A JSON response containing the binary prediction (`1` for default, `0` for non-default) and the model's confidence score (probability of default).

This API is designed to be integrated into other business systems, such as a loan application website or an internal underwriting dashboard.

---
### **Project Structure**

The repository is organized into a professional and reproducible structure:

```

fintech\_loan\_predictor/
│
├── data/
│   └── loan\_data.csv         \# The raw dataset used for training.
│
├── notebooks/
│   ├── 01-EDA.ipynb          \# Exploratory Data Analysis.
│   ├── 02-Preprocessing.ipynb \# Data cleaning and preparation.
│   ├── 03-Model-Training.ipynb \# Baseline model training.
│   ├── 04-Advanced-Modeling.ipynb \# Advanced modeling with LightGBM.
│   └── 05-Final-Pipeline.ipynb \# Building the final production pipeline.
│
├── src/
│   └── main.py               \# The source code for the FastAPI application.
│
├── .gitignore                \# Specifies files for Git to ignore.
├── loan\_predictor\_pipeline.joblib \# The final, serialized production model.
├── requirements.txt          \# A list of all Python dependencies.
└── README.md                 \# This project documentation.

````

---
### **How to Run This Project**

1.  **Clone the repository:**
    ```bash
    git clone [Your GitHub Repo URL]
    cd fintech_loan_predictor
    ```

2.  **Set up the environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: .\venv\Scripts\activate
    pip install -r requirements.txt
    ```

3.  **Run the API server:**
    ```bash
    uvicorn src.main:app --reload
    ```

4.  **Access the interactive API documentation** by navigating to `http://127.0.0.1:8000/docs` in your web browser.

---
### **Key Development Stages**

This project was built incrementally, focusing on key stages of the machine learning lifecycle.

* **Stage 1: Foundation & Setup**
    * Established a structured project directory.
    * Set up a Python virtual environment to manage dependencies.
    * Initialized a Git repository for version control.

* **Stage 2: Data Analysis & Discovery (EDA)**
    * Performed a deep dive into the dataset to understand its features, distributions, and potential challenges.
    * Identified a key business problem: a **class imbalance** where defaults (~16%) are the minority class.
    * Discovered strong predictive features like `fico` score and `purpose` of the loan.

* **Stage 3: Preprocessing & Modeling**
    * Converted categorical features into a numerical format using one-hot encoding.
    * Established a robust data splitting strategy (`train_test_split`) with stratification.
    * Trained baseline models (Logistic Regression, Random Forest) to establish performance benchmarks.
    * Implemented a powerful, industry-standard **LightGBM** model.
    * Addressed the class imbalance problem directly by using the `scale_pos_weight` parameter, significantly improving the model's ability to identify true defaults.

* **Stage 4: Productionalization**
    * Encapsulated the entire workflow (preprocessing and modeling) into a single, reusable `scikit-learn` **Pipeline**.
    * Trained the final pipeline on the full dataset and serialized it into a `loan_predictor_pipeline.joblib` file.
    * Built a robust API using **FastAPI** to serve the trained model and used **Pydantic** for data validation.
