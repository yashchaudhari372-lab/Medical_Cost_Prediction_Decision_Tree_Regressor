<div align="center">

# 🏥 Medical Cost Prediction using Decision Tree Regressor

### AI Medical Cost Analytics Dashboard | Machine Learning • Regression • Flask

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python) ![Scikit--learn](https://img.shields.io/badge/Scikit--learn-Decision%20Tree-orange?logo=scikitlearn) ![Flask](https://img.shields.io/badge/Flask-Web%20App-black?logo=flask) ![NumPy](https://img.shields.io/badge/NumPy-Data%20Processing-blue?logo=numpy) ![Vercel](https://img.shields.io/badge/Vercel-Live%20Demo-black?logo=vercel)

**An interactive machine learning web application that estimates medical insurance charges using demographic and lifestyle information.**

[🚀 Live Demo](https://medical-cost-prediction-decision-tr.vercel.app/) · [💻 Source Code](https://github.com/yashchaudhari372-lab/Medical_Cost_Prediction_Decision_Tree_Regressor)

</div>

---

## 📌 Project Overview

Medical insurance costs can vary with factors such as age, body mass index (BMI), smoking status, family size, and region. This project provides a web interface for estimating insurance charges using a **Decision Tree Regressor** saved as a serialized machine learning model.

Users enter six details, submit the form, and receive a predicted cost in an interactive analytics dashboard. The application is built with **Flask** and includes a responsive glassmorphism interface, dark/light theme toggle, and a Chart.js comparison chart.

> **Disclaimer:** Predictions are estimates for educational and demonstration purposes, not medical advice, guaranteed insurance quotes, or individualized financial recommendations.

## ✨ Key Features

- **Machine learning prediction:** Loads the saved `mcp_model.pkl` model and generates a numerical insurance-cost estimate.
- **Six input parameters:** Age, sex, BMI, number of children, smoking status, and region.
- **Interactive dashboard:** Displays predicted cost and a bar-chart comparison.
- **Modern UI:** Responsive glassmorphism design, animated gradients, and dark/light modes.
- **Asynchronous form submission:** Fetches predictions from the Flask `/predict` endpoint without refreshing the page.
- **Cloud deployment:** Public demonstration hosted on Vercel.
- **Explicit error handling:** Returns an error if the model cannot load or prediction fails.

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| Programming | Python |
| Machine learning | Decision Tree Regressor, Scikit-learn |
| Numerical processing | NumPy |
| Backend | Flask |
| Frontend | HTML, CSS, JavaScript |
| Visualization | Chart.js |
| UI assets | Font Awesome, Google Fonts |
| Model persistence | Python Pickle (`.pkl`) |
| Deployment | Vercel |

## 📊 Input Features

The deployed form accepts the following six model inputs in this exact order:

| Feature | Description | Input |
|---|---|---|
| `age` | Person's age | 18–100 in the form |
| `sex` | Encoded sex | Female = 0, Male = 1 |
| `bmi` | Body mass index | Numeric value |
| `children` | Number of children | Integer 0–10 in the form |
| `smoker` | Smoking status | No = 0, Yes = 1 |
| `region` | Encoded geographic region | Northeast = 0, Northwest = 1, Southeast = 2, Southwest = 3 |

**Target:** Estimated medical insurance charges, displayed in USD in the application.

**Important:** These encodings describe the deployed form and prediction code. The training data and training notebook are not included in this repository, so training-time preprocessing and encoding consistency have not been independently verified.

## 🧠 How It Works

```text
User enters six input values
              ↓
Flask receives POST /predict
              ↓
Values converted to a NumPy array
              ↓
Saved Decision Tree Regressor (mcp_model.pkl)
              ↓
Predicted insurance cost
              ↓
JSON response to the browser
              ↓
Cost display + interactive Chart.js bar chart
```

A **Decision Tree Regressor** predicts continuous numerical values by partitioning feature space through a series of decision rules. In this project, the model outputs a predicted medical insurance cost rather than a classification label.

## 📁 Repository Structure

```text
Medical_Cost_Prediction_Decision_Tree_Regressor/
├── app.py             # Flask app, inline dashboard UI, and prediction API
├── mcp_model.pkl      # Serialized trained regression model
├── requirements.txt   # Python dependencies
└── README.md          # Project documentation
```

The HTML, CSS, and JavaScript dashboard are embedded in `app.py` using Flask's `render_template_string` rather than separate template files.

## ⚙️ Installation and Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/yashchaudhari372-lab/Medical_Cost_Prediction_Decision_Tree_Regressor.git
cd Medical_Cost_Prediction_Decision_Tree_Regressor
```

### 2. Create and activate a virtual environment

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS/Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Start the Flask application

```bash
python app.py
```

### 5. Open in your browser

```text
http://127.0.0.1:5000/
```

> The repository's `app.py` starts Flask with `debug=True` for local development. Disable debug mode in production. The serialized model must be compatible with your installed Scikit-learn version.

## 🔌 API Documentation

### `GET /`

Renders the medical cost analytics dashboard.

### `POST /predict`

Accepts form-encoded fields (`multipart/form-data` or `application/x-www-form-urlencoded`):

```text
age=35
sex=1
bmi=28.5
children=1
smoker=0
region=0
```

Example cURL request:

```bash
curl -X POST http://127.0.0.1:5000/predict \
  -d "age=35" \
  -d "sex=1" \
  -d "bmi=28.5" \
  -d "children=1" \
  -d "smoker=0" \
  -d "region=0"
```

**Successful response format** (illustrative, not a verified model output):

```json
{
  "status": "success",
  "prediction": 12345.67
}
```

**Error response format:**

```json
{
  "status": "error",
  "message": "Model pickle file (mcp_model.pkl) was not loaded properly."
}
```

## 📈 Model Evaluation

This is a **regression** problem. Relevant metrics include:

| Metric | What it measures | Verified result |
|---|---|---|
| R² Score | Proportion of target variance explained by the model | 69.75% |
| MAE | Mean absolute prediction error | 3,019.71 |
| MSE | Mean squared prediction error | 42,441,621.95 |
| RMSE | Root mean squared prediction error | 6,514.72 |

The repository contains the saved model and inference app, but no verified evaluation report or held-out test dataset. **Do not interpret the dashboard's displayed baseline values as model performance metrics.** Add scores only after evaluating the trained model against a proper held-out test set.

## 🖥️ Dashboard Preview

The web interface provides:

1. A form for entering age, sex, BMI, children, smoking status, and region.
2. A prediction result panel showing the estimated cost in USD.
3. A Chart.js bar chart comparing the estimate with fixed display baselines.
4. A responsive dark/light theme toggle.

**Suggested screenshots:** Add actual dashboard screenshots to a `screenshots/` folder, then embed them here:

```markdown
![Medical Cost Prediction Dashboard](screenshots/dashboard.png)
![Prediction Result](screenshots/prediction-result.png)
```

*The comparison chart's baseline minimum and maximum are hard-coded display values, not a statistical confidence interval or validated training-data bounds.*

## 🌍 Live Demo

**Try the application:** https://medical-cost-prediction-decision-tr.vercel.app/

## 🎯 Potential Applications

- Demonstrating end-to-end machine learning model deployment.
- Exploring relationships between demographic/lifestyle inputs and modeled insurance costs.
- Teaching regression, Flask APIs, and interactive data visualization.
- Prototyping insurance cost estimation interfaces.

## 🔮 Future Improvements

- Publish the training notebook, data source, and reproducible preprocessing pipeline.
- Evaluate the model using a held-out test set and report R², MAE, and RMSE.
- Compare Decision Tree performance with Random Forest, Gradient Boosting, and linear regression.
- Add input validation and stronger server-side error handling.
- Add model explainability and clearly labeled uncertainty estimates.
- Replace static chart baselines with documented, data-derived reference statistics.
- Pin dependency versions and add automated tests.

## 👨‍💻 Author

**Yash Chaudhari**  
Aspiring Data Scientist & Data Analyst

- **GitHub:** https://github.com/yashchaudhari372-lab
- **LinkedIn:** https://www.linkedin.com/in/yashchaudhari08/

---

<div align="center">

**⭐ If you found this project useful, consider starring the repository!**

*Built with Python, Scikit-learn, Flask, and Chart.js.*

</div>
