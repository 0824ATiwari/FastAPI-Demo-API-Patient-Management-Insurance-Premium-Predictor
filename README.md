FastAPI Demo API — Patient Management & Insurance Premium Predictor

A two-part FastAPI project demonstrating REST API design with Pydantic validation and ML model serving. Built as a learning project covering CRUD operations, data modeling, and deploying a trained machine learning model behind an API endpoint.


What's Inside

1. Patient Management API (main.py)

A full CRUD REST API for managing patient health records stored in a JSON file. Supports creating, reading, updating, and deleting patients. BMI and weight verdict (Underweight / Normal / Obese) are computed automatically using Pydantic computed_field.

2. Insurance Premium Predictor API (app.py)

A FastAPI service that wraps a pre-trained scikit-learn classification model (model.pkl) to predict an insurance premium category (Low / Medium / High) based on user inputs. Features like BMI, lifestyle risk, age group, and city tier are derived automatically from raw inputs before inference.

3. Streamlit Frontend (frontend.py)

A simple web UI built with Streamlit that collects user inputs and calls the Insurance Predictor API to display the predicted premium category.


Project Structure

fastapi-demo-api-main/
├── main.py              # Patient Management CRUD API
├── app.py               # Insurance Premium Prediction API (ML model serving)
├── frontend.py          # Streamlit frontend for the prediction API
├── model.pkl            # Pre-trained classification model
├── patients.json        # JSON flat-file database for patient records
├── insurance.csv        # Training dataset (age, weight, BMI, occupation, etc.)
└── fastapi_ml_model.ipynb  # Notebook: model training and exploration


API Endpoints

Patient Management (main.py)

MethodEndpointDescriptionGET/Health checkGET/aboutAPI descriptionGET/viewList all patientsGET/patient/{patient_id}Get patient by IDGET/sort?sort_by=bmi&order=ascSort patients by height, weight, or BMIPOST/createAdd a new patientPUT/edit/{patient_id}Update patient fieldsDELETE/delete/{patient_id}Remove a patient

Insurance Predictor (app.py)

MethodEndpointDescriptionPOST/predictPredict insurance premium category

Sample request body for /predict:

json{
  "age": 32,
  "weight": 75.0,
  "height": 1.72,
  "income_lpa": 12.5,
  "smoker": false,
  "city": "Chandigarh",
  "occupation": "private_job"
}

Response:

json{
  "predicted_category": "Low"
}


Features


Pydantic v2 validation with Field constraints and computed_field for derived attributes
Auto-computed fields: BMI, weight verdict, age group, lifestyle risk, city tier
Input validation: age range, height/weight bounds, gender and occupation literals
Sorted queries with field and order selection via query parameters
Flat-file persistence using patients.json for the CRUD API
ML model serving with a pre-trained pickle model and pandas DataFrame inference
City tier classification across Tier 1, Tier 2, and Tier 3 Indian cities




Dataset

insurance.csv contains synthetic records with the following columns:

ColumnDescriptionageUser ageweightWeight in kgheightHeight in metersincome_lpaAnnual income in LPA (Lakhs Per Annum)smokerBoolean smoking statuscityIndian city nameoccupationOne of: retired, freelancer, student, government_job, business_owner, unemployed, private_jobinsurance_premium_categoryTarget label: Low / Medium / High


Tech Stack


FastAPI — API framework
Pydantic v2 — Data validation and schema modeling
scikit-learn — ML model (pre-trained, loaded via pickle)
pandas — DataFrame construction for model inference
Streamlit — Frontend UI
Uvicorn — ASGI server



Notes


The patient database (patients.json) is a flat file — not suitable for concurrent writes in production.
The hardcoded IP in frontend.py (http://34.226.152.222:8000/predict) should be updated to your deployment URL or localhost for local development.
The verdict field in the Patient model classifies BMI 25–30 as "Normal" rather than "Overweight" — this appears to be an intentional simplification.
