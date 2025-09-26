# Heart Disease Risk Prediction App (Streamlit)

An interactive Streamlit application that predicts the risk of heart disease based on user‑provided clinical information. The app loads a pre‑trained K‑Nearest Neighbors (KNN) model along with its scaler and a list of expected feature columns to ensure inputs are correctly aligned before prediction.


## Features
- Simple, web‑based UI built with Streamlit
- Real‑time prediction with a pre‑trained KNN model
- Robust input handling: automatically adds missing one‑hot columns expected by the model
- Clear risk feedback (High vs Low risk)


## Demo Screenshot (optional)
You can run the app locally using the steps below. If you deploy it, consider adding a screenshot or GIF here to show the UI.


## Project Structure
```
D:/ML-part3
├── app.py             # Streamlit app
├── KNN_heart.pkl      # Trained KNN model (pickle)
├── scaler.pkl         # Fitted scaler used during training
├── columns.pkl        # List of expected feature columns (order matters)
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

2) Install dependencies:
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


## Troubleshooting
- FileNotFoundError for model/scaler/columns
  - Ensure `KNN_heart.pkl`, `scaler.pkl`, and `columns.pkl` are in the same directory as `app.py`.

- Version mismatch errors (e.g., from scikit‑learn/joblib)
  - Try aligning package versions to those used during training. Start with the latest scikit‑learn and joblib; if issues persist, downgrade/upgrade carefully.

- Streamlit command not found
  - Ensure your virtual environment is activated and that `streamlit` is installed. On Windows, use PowerShell and activate with `.\.venv\Scripts\Activate`.

- Port already in use
  - Run with a different port: `streamlit run app.py --server.port 8502`.


## Deployment
- Streamlit Community Cloud:
  1. Push this repository to GitHub.
  2. Create a new app on https://streamlit.io/cloud pointing to `app.py`.
  3. In the app’s settings, add Python dependencies (streamlit, pandas, scikit‑learn, joblib) in the package section or via a `requirements.txt` file.

- Other options: Render, Hugging Face Spaces (Streamlit), or any VM where you can run `streamlit run`.


## Example requirements.txt (optional)
If you prefer a pinned dependencies file, create `requirements.txt` with content similar to:
```
streamlit>=1.20
pandas>=1.5
scikit-learn>=1.1
joblib>=1.2
```
Adjust versions to match your environment or training environment if you encounter compatibility issues.


## License
Add your preferred license here (e.g., MIT). If you’re unsure, you can omit this section or keep it as a placeholder.


## Acknowledgments
- Inspired by common open heart disease datasets and educational ML demos.
- Built with Streamlit and scikit‑learn.
