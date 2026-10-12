# 🧠 Mental Health Score Predictor

An end-to-end machine learning web app that predicts a student's **mental health score (0–10)** from social media usage and lifestyle habits such as sleep, stress, study time, and physical activity.

🔗 **Live Demo:** [https://mental-health-score-2-wymj.onrender.com](https://mental-health-score-2-wymj.onrender.com)

> ⏳ The app is hosted on Render's free tier, so the first request may take 30–60 seconds while the server wakes up.

---

## 📌 Overview

Social media is part of every student's daily routine. This project explores how habits like screen time, sleep, stress, and physical activity relate to mental well-being, and turns that analysis into a working product:

1. **Data analysis and model training** in a Jupyter Notebook
2. **REST API** built with FastAPI to serve predictions
3. **Interactive frontend** that shows the predicted score on a live gauge
4. **Deployment** on Render

---

## ✨ Features

- Predicts a mental health score from **12 input features**
- Interactive score gauge with a clean, responsive UI
- Input validation with **Pydantic** (invalid values are rejected with clear errors)
- Auto-generated API docs with Swagger UI at `/docs`
- CORS enabled so the frontend can talk to the API
- Complete preprocessing and model saved as a single Scikit-learn `Pipeline`

---

## 🛠️ Tech Stack

| Area | Tools |
|---|---|
| **Language** | Python, JavaScript |
| **Data and ML** | Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, Joblib |
| **Backend** | FastAPI, Pydantic, Uvicorn |
| **Frontend** | HTML5, CSS3 (Grid, Flexbox, animations), JavaScript (Fetch API, async/await, SVG) |
| **Deployment and Tools** | Render, Git, GitHub, VS Code, Jupyter Notebook |

---

## 📊 Dataset

**Student Social Media and Mental Health Impact** dataset with about **5,000 student records**.

| Feature | Type | Description |
|---|---|---|
| `Age` | Number | Age of the student (10–100) |
| `Gender` | Category | Male / Female |
| `Country` | Category | Student's country (grouped into top countries and "Other") |
| `Academic_Level` | Category | High School / Undergraduate / Graduate |
| `Most_Used_Platform` | Category | Instagram, TikTok, WhatsApp, YouTube, etc. |
| `Purpose_Of_Use` | Category | Networking / Education / Entertainment / News |
| `Avg_Daily_Usage_Hours` | Number | Daily social media hours |
| `Daily_Unlocks` | Number | Phone unlocks per day |
| `Study_Hours` | Number | Daily study hours |
| `Physical_Activity_Hours` | Number | Daily physical activity hours |
| `Sleep_Hours_Per_Night` | Number | Average sleep hours |
| `Stress_Level` | Category | Low / Medium / High / Very High |
| **`Mental_Health_Score`** | **Target** | Score the model predicts |

---

## 🤖 Machine Learning Workflow

1. **Data exploration and cleaning** with Pandas, Matplotlib, and Seaborn
2. **Feature engineering and preprocessing** using a Scikit-learn `ColumnTransformer`:
   - Log transformation and scaling for skewed numeric features
   - Standard scaling for other numeric features
   - Ordinal encoding for `Stress_Level` (Low → Very High)
   - One-hot encoding for nominal categorical features
3. **Model comparison:** Linear Regression vs Random Forest
4. **Hyperparameter tuning** with `RandomizedSearchCV` (5-fold cross-validation)
5. **Overfitting analysis** by comparing training and test scores
6. **Model export** with Joblib (`Mental_Health_Model.pkl`)

### Results (test set)

| Model | R² | MAE | RMSE |
|---|---|---|---|
| Linear Regression | 0.740 | 0.536 | 0.676 |
| **Random Forest (default), deployed** | **0.878** | **0.347** | **0.464** |
| Random Forest (tuned) | 0.865 | 0.369 | 0.487 |

The default Random Forest scored highest on the test set and is the model used in the deployed app. The tuned model overfits less (training R² 0.95 vs 0.98), but its test score was slightly lower.

---

## 📁 Project Structure

```
Mental-Health-Score/
├── main.py                       # FastAPI backend (API + model loading)
├── Mental_Health_Model.pkl       # Trained Scikit-learn pipeline
├── ML_Project.ipynb              # Data analysis and model training notebook
├── Student Social Media And Mental Health Impact.csv   # Dataset
├── index.html                    # Frontend page
├── style.css                     # Frontend styling
├── script.js                     # Frontend logic (calls the API)
├── requirements.txt              # Python dependencies
└── README.md
```

---

## 🚀 Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/HarshalKapse21/Mental-Health-Score.git
cd Mental-Health-Score
```

### 2. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 3. Start the API

```bash
python -m uvicorn main:app --port 8000 --reload
```

The API runs at `http://127.0.0.1:8000`. Open `http://127.0.0.1:8000/docs` to test it in Swagger UI.

### 4. Open the frontend

In `script.js`, set the API address to your local server:

```js
const API_BASE = "http://127.0.0.1:8000";
```

Then open `index.html` with VS Code **Live Server** (or any static server).

---

## 🔌 API Reference

### `POST /predict`

**Request body**

```json
{
  "age": 20,
  "gender": "Female",
  "country": "India",
  "academic_level": "Undergraduate",
  "most_used_platform": "Instagram",
  "purpose_of_use": "Entertainment",
  "avg_daily_usage_hours": 5,
  "daily_unlocks": 80,
  "study_hours": 3,
  "physical_activity_hours": 1,
  "sleep_hours_per_night": 6,
  "stress_level": "High"
}
```

**Response**

```json
{
  "predicted_mental_health_score": 6.2
}
```

*(The score above is only an example; actual output depends on the model.)*

---

## ☁️ Deployment (Render)

| Setting | Value |
|---|---|
| **Build Command** | `pip install -r requirements.txt` |
| **Start Command** | `uvicorn main:app --host 0.0.0.0 --port $PORT` |

---

## ⚠️ Disclaimer

This is a **learning project** built on a public dataset. It is **not a medical or diagnostic tool** and should not be used to make decisions about anyone's health. If you or someone you know is struggling, please reach out to a qualified mental health professional.

---

## 🔮 Future Improvements

- Add model explainability (feature importance / SHAP)
- Add charts showing how each input affects the score
- Add unit tests for the API
- Try other models such as Gradient Boosting or XGBoost

---

## 👨‍💻 Author

**Harshal Kapse**

- GitHub: [@HarshalKapse21](https://github.com/HarshalKapse21)

⭐ If you found this project useful, consider giving it a star!
