# 🎫 Support Ticket Classification & Prioritization System

![Python](https://img.shields.io/badge/Python-3.14-blue?style=for-the-badge&logo=python)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?style=for-the-badge&logo=scikit-learn)
![NLTK](https://img.shields.io/badge/NLTK-NLP-green?style=for-the-badge)
![Streamlit](https://img.shields.io/badge/Streamlit-Web%20App-red?style=for-the-badge&logo=streamlit)
![GitHub](https://img.shields.io/badge/GitHub-Public-black?style=for-the-badge&logo=github)

> An ML-powered system that automatically classifies customer support tickets into categories and assigns priority levels, helping support teams respond faster and reduce backlog.

---

## 📌 Table of Contents
- [About the Project](#about-the-project)
- [How It Works](#how-it-works)
- [Key Features](#key-features)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Setup and Installation](#setup-and-installation)
- [How to Run](#how-to-run)
- [Web App Usage](#web-app-usage)
- [How Tickets Are Categorized](#how-tickets-are-categorized)
- [How Priority Is Decided](#how-priority-is-decided)
- [Model Evaluation Results](#model-evaluation-results)
- [Dataset Selection Process](#dataset-selection-process)
- [Future Improvements](#future-improvements)

---

## 🧠 About the Project

Customer support teams receive hundreds or thousands of tickets every day. Manually sorting them into categories and figuring out which ones are urgent wastes valuable time. This project builds a **Machine Learning system** that:

- Reads raw support ticket text
- Automatically classifies tickets into categories
- Assigns a priority level (High / Medium / Low)
- Evaluates model performance using proper ML metrics
- Displays everything in an interactive web app

This mirrors real systems used in SaaS companies, IT helpdesks, and internal support platforms.

---

## ⚙️ How It Works
Raw Ticket Text

│

▼

┌─────────────────────┐

│  Text Cleaning      │  → Lowercase, remove symbols,

│  (preprocessor.py)  │    stopwords, lemmatization

└─────────────────────┘

│

▼

┌─────────────────────┐

│  TF-IDF Feature     │  → Convert ticket text into

│  Extraction         │    numerical vectors

│  (feature_extractor)│

└─────────────────────┘

│

▼

┌─────────────────────┐

│  Train/Test Split   │  → 80% training, 20% testing

└─────────────────────┘

│

▼

┌─────────────────────┐

│  Logistic Regression│  → Trains a classification model

│  Classifier         │    on ticket category labels

│  (classifier.py)    │

└─────────────────────┘

│

▼

┌─────────────────────┐

│  Rule-Based Priority│  → Detects urgency keywords to

│  Detection          │    assign High/Medium/Low

│  (classifier.py)    │

└─────────────────────┘

│

▼

┌─────────────────────┐

│  Model Evaluation   │  → Accuracy, precision, recall,

│  (evaluator.py)     │    F1-score, confusion matrix

└─────────────────────┘

│

▼

┌─────────────────────┐

│  Streamlit Web App  │  → Upload data, train model,

│  (app.py)           │    classify new tickets live

└─────────────────────┘

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 📂 Upload Any Dataset | Accepts any CSV with ticket text and category labels |
| 🧹 Text Cleaning | Removes noise, punctuation, stopwords, lemmatizes words |
| 🔢 TF-IDF Feature Extraction | Converts ticket text into ML-ready numerical vectors |
| 🤖 Category Classification | Logistic Regression model predicts ticket category |
| ⚡ Priority Assignment | Rule-based keyword detection for High/Medium/Low priority |
| 📊 Model Evaluation | Accuracy, precision, recall, F1-score reported |
| 🗺️ Confusion Matrix | Visual breakdown of correct vs incorrect predictions |
| 🌐 Web App | Train and classify tickets directly in the browser |
| 🔍 Confidence Scores | Shows prediction confidence for every category |

---

## 📁 Project Structure
support-ticket-classifier/

│

├── data/                              ← Dataset and saved models

│   ├── all_tickets_processed_improved_v3.csv

│   ├── category_model.pkl             ← Saved trained model

│   ├── category_vectorizer.pkl        ← Saved TF-IDF vectorizer

│   └── confusion_matrix.png           ← Saved evaluation chart

│

├── src/                               ← Core ML modules

│   ├── init.py

│   ├── preprocessor.py                ← Text cleaning and preprocessing

│   ├── feature_extractor.py           ← TF-IDF vectorization, train/test split

│   ├── classifier.py                  ← Category model training, priority rules

│   └── evaluator.py                   ← Model evaluation, confusion matrix

│

├── app.py                             ← Streamlit web application

├── main.py                            ← Terminal-based runner

├── requirements.txt                   ← Python dependencies

├── .gitignore                         ← Files excluded from Git

└── README.md                          ← Project documentation

---

## 🛠️ Tech Stack

| Category | Tools Used |
|---|---|
| Language | Python 3.14 |
| NLP and Text Processing | NLTK (stopwords, lemmatization) |
| ML and Vectorization | Scikit-learn (TfidfVectorizer, LogisticRegression) |
| Model Persistence | Joblib |
| Data Handling | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Web App | Streamlit |
| Version Control | Git and GitHub |

---

## 📦 Setup and Installation

### 1 — Clone the Repository
git clone https://github.com/Deez-puff/support-ticket-classifier.git

cd support-ticket-classifier

### 2 — Install Dependencies
pip install -r requirements.txt

### 3 — Download NLTK Data
python -c "import nltk; nltk.download('stopwords'); nltk.download('wordnet')"

### 4 — Download the Dataset
Download the IT Service Ticket Classification dataset from Kaggle:
👉 https://www.kaggle.com/datasets/adisongoh/it-service-ticket-classification-dataset

Place the CSV file inside the data/ folder.

---

## ▶️ How to Run

### Option 1 — Web App (Recommended)
python -m streamlit run app.py
Opens automatically in your browser at http://localhost:8501

### Option 2 — Terminal
python main.py
Prints training progress, evaluation metrics, classification report, and saves the confusion matrix to data/

---

## 🌐 Web App Usage

### Mode 1 — Train New Model
1. Upload your CSV dataset
2. Select which column contains the ticket text
3. Select which column contains the category label
4. Click Train Model
5. View accuracy, precision, recall, F1-score, and confusion matrix

### Mode 2 — Classify a Ticket
1. Switch to Classify a Ticket mode in the sidebar
2. Type or paste any support ticket text
3. Click Classify Ticket
4. View the predicted category, priority level, and confidence breakdown chart

---

## 📐 How Tickets Are Categorized

The classification pipeline works as follows:

1. Text Cleaning — Raw ticket text is lowercased, stripped of punctuation and numbers, stopwords are removed, and words are lemmatized to their root form
2. TF-IDF Vectorization — Cleaned text is converted into numerical vectors using Term Frequency-Inverse Document Frequency, capturing both single words and two-word phrases
3. Logistic Regression Classification — A multi-class Logistic Regression model is trained on the TF-IDF vectors to predict one of 8 categories: Hardware, HR Support, Access, Miscellaneous, Storage, Purchase, Internal Project, Administrative rights

---

## ⚡ How Priority Is Decided

Since the dataset does not include a priority label, a rule-based keyword detection system was built to simulate real-world urgency triage:

| Priority | Trigger Keywords |
|---|---|
| 🔴 High | urgent, asap, immediately, critical, emergency, down, broken, crash, failure, blocked, outage |
| 🟡 Medium | issue, problem, error, bug, trouble, slow, delay, warning, incorrect |
| 🟢 Low | request, inquiry, question, information, would like, when possible, minor |

---

## 📊 Model Evaluation Results

The model was evaluated on a held-out test set of 9,568 tickets (20% of the dataset):

| Metric | Score |
|---|---|
| Accuracy | 85.43% |
| Precision (weighted) | 85.79% |
| Recall (weighted) | 85.43% |
| F1-Score (weighted) | 85.43% |

### Class-wise Performance

| Category | Precision | Recall | F1-Score | Support |
|---|---|---|---|---|
| Access | 0.91 | 0.88 | 0.89 | 1425 |
| Administrative rights | 0.87 | 0.64 | 0.74 | 352 |
| HR Support | 0.86 | 0.86 | 0.86 | 2183 |
| Hardware | 0.80 | 0.89 | 0.84 | 2724 |
| Internal Project | 0.92 | 0.82 | 0.87 | 424 |
| Miscellaneous | 0.83 | 0.82 | 0.82 | 1412 |
| Purchase | 0.97 | 0.87 | 0.92 | 493 |
| Storage | 0.93 | 0.84 | 0.88 | 555 |

---

## 🔄 Dataset Selection Process

This project initially used the Kaggle Customer Support Ticket Dataset but diagnostic testing revealed that its ticket descriptions were synthetically templated — the text carried almost no relationship to the assigned category labels. The model trained on it performed at roughly random-guess accuracy (around 20% for 5 categories).

After confirming this issue through exploratory analysis, the project switched to the IT Service Ticket Classification Dataset, which contains genuine varied ticket text tied meaningfully to its category labels, resulting in an 85% accurate model.

This demonstrates a key real-world ML skill: diagnosing whether poor model performance stems from a code issue or a data quality issue and making an evidence-based decision to switch datasets.

---

## 🚀 Future Improvements

- [ ] Replace rule-based priority system with a trained ML priority classifier
- [ ] Try Random Forest, XGBoost, or fine-tuned BERT for higher accuracy
- [ ] Add support for multi-label tickets
- [ ] Build an automatic ticket routing system
- [ ] Add a feedback loop where corrected predictions retrain the model
- [ ] Deploy on Streamlit Cloud for public access
- [ ] Add support for non-English tickets

---

## 👨‍💻 Author
Deepak Rajesh

Built as part of **Future Interns ML Task 2 — 2026**

---

## 📄 License

This project is open source and available under the MIT License.
