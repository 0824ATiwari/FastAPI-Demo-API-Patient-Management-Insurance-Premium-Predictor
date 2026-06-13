FastAPI Demo API — Patient Management & Insurance Premium Predictor
A two-part FastAPI learning project covering CRUD API design, Pydantic v2 validation, and ML model serving.
What's Inside

main.py — CRUD REST API for patient records stored in a JSON file. BMI and weight verdict auto-computed via Pydantic computed_field
app.py — Wraps a pre-trained sklearn model to predict insurance premium category (Low / Medium / High)
frontend.py — Streamlit UI that calls the prediction API. Replace the hardcoded AWS IP before pushing
model.pkl — Pre-trained classification model
patients.json — Flat-file patient database
insurance.csv — Training dataset
fastapi_ml_model.ipynb — Model training notebook

Patient Management Endpoints

GET / — Health check
GET /view — List all patients
GET /patient/{patient_id} — Get one patient
GET /sort?sort_by=bmi&order=asc — Sort by height, weight, or bmi
POST /create — Add patient
PUT /edit/{patient_id} — Update patient
DELETE /delete/{patient_id} — Remove patient

Full interactive docs at http://localhost:8000/docs
Insurance Predictor Endpoint

POST /predict — Accepts age, weight, height, income_lpa, smoker, city, occupation
Returns { "predicted_category": "Low" / "Medium" / "High" }

Dataset Columns

age — User age
weight — kg
height — meters
income_lpa — Annual income in Lakhs Per Annum
smoker — Boolean
city — Indian city
occupation — retired / freelancer / student / government_job / business_owner / unemployed / private_job
insurance_premium_category — Target label: Low / Medium / High

Features

Pydantic v2 validation with Field constraints
Auto-computed: BMI, weight verdict, age group, lifestyle risk, city tier
City tier classification for Tier 1, 2, 3 Indian cities
Sorted queries via query parameters
Swagger UI auto-generated

Tech Stack

FastAPI
Pydantic v2
scikit-learn
pandas
Streamlit
Uvicorn
