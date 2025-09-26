# Heart Disease Risk Prediction App (Streamlit)

An interactive Streamlit application that predicts the risk of heart disease based on user‑provided clinical information. The app loads a pre‑trained K‑Nearest Neighbors (KNN) model along with its scaler and a list of expected feature columns to ensure inputs are correctly aligned before prediction.

Note: In the app's UI, the title appears as "Heart Stroke prediction." This refers to the same heart disease risk predictor described here.


## Features
- Simple, web‑based UI built with Streamlit
- Real‑time prediction with a pre‑trained KNN model
- Robust input handling: automatically adds missing one‑hot columns expected by the model
- Clear risk feedback (High vs Low risk)


## Project Structure
```
heart risk prediction
├── app.py             # Streamlit app
├── KNN_heart.pkl      # Trained KNN model (pickle)
├── scaler.pkl         # Fitted scaler used during training
├── columns.pkl        # List of expected feature columns (order matters)
├── requirements.txt   # Python dependencies for the app
└── README.md          # This file
```


## Requirements
- Python 3.8–3.12 (tested commonly with 3.9/3.10)
- pip (Python package manager)

Python packages used by the app:
- streamlit
- pandas
- scikit-learn (for the scaler’s transform API)
- joblib (to load model artifacts)

You can install them directly with pip as shown below.


## Installation
It’s recommended (but not required) to use a virtual environment.

1) Create and activate a virtual environment (optional):
- Windows (PowerShell):
  ```powershell
  python -m venv .venv
  .\.venv\Scripts\Activate
  ```
- macOS/Linux (bash):
  ```bash
  python -m venv .venv
  source .venv/bin/activate
  ```

2) Install dependencies (recommended):
```bash
pip install -r requirements.txt
```
Or install packages individually:
```bash
pip install streamlit pandas scikit-learn joblib
```


## Running the App
From the project root (where app.py is located), run:
```bash
streamlit run app.py
```
This will start a local server and open the app in your default browser (typically at http://localhost:8501). If the browser does not open automatically, copy the printed URL into your browser.


## How It Works
1. The app collects the following inputs via the UI:
   - Age (18–100)
   - Sex (M/F)
   - Chest Pain Type (ATA, NAP, TA, ASY)
   - Resting Blood Pressure (mm Hg)
   - Cholesterol (mg/dL)
   - Fasting Blood Sugar > 120 mg/dL (0 or 1)
   - Resting ECG (Normal, ST, LVH)
   - Max Heart Rate (60–220)
   - Exercise‑Induced Angina (Y/N)
   - Oldpeak (ST Depression)
   - ST Slope (Up, Flat, Down)

2. A dictionary is built with numerical fields and one‑hot encoded categorical fields (e.g., `Sex_M`, `ChestPainType_ATA`, etc.).

3. The app loads `columns.pkl` to get the exact list and order of feature columns the model expects. Any missing columns are added and set to 0 so the input aligns perfectly with the model’s training schema.

4. The input is scaled with `scaler.pkl` and fed to the KNN model from `KNN_heart.pkl` to obtain the prediction.

5. The result is displayed as either:
   - High Risk of Heart Disease (⚠️)
   - Low Risk of Heart Disease (✅)


## Files Explained
- `app.py`: Main Streamlit application.
- `KNN_heart.pkl`: Serialized KNN model trained on the heart dataset.
- `scaler.pkl`: Serialized scaler (e.g., StandardScaler) fitted on the training data and used for inference.
- `columns.pkl`: Serialized Python list (or similar) containing the exact feature names (including one‑hot encoded column names) and their order.

Note on security: pickle/joblib files are executable code. Only open artifacts you trust.


