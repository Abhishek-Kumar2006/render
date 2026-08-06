# 🏏 IPL Win Predictor

A machine learning web app that predicts the **live win probability** of the batting and bowling teams during an IPL (Indian Premier League) cricket match, based on the current match situation — target, score, overs, and wickets.

Built with **scikit-learn** for the model and **Streamlit** for the interactive web interface.

## 🔗 Live Demo

Deploy this repo to a platform like [Render](https://render.com) or [Streamlit Community Cloud](https://streamlit.io/cloud) to get a shareable link.

## 📸 How It Works

1. Select the **batting team** and **bowling team**.
2. Select the **host city**.
3. Enter the **target score**, **current score**, **overs completed**, and **wickets lost**.
4. Click **Predict Probability** to see the live win percentage for each team.

Under the hood, the app derives key features from your inputs:

- **Runs left** = Target − Current score
- **Balls left** = 120 − (Overs × 6)
- **Wickets in hand** = 10 − Wickets lost
- **Current Run Rate (CRR)** = Score / Overs
- **Required Run Rate (RRR)** = (Runs left × 6) / Balls left

These features are fed into a trained classification pipeline that outputs the probability of each team winning.

## 🧠 Model

The model was trained in `IPL Project.ipynb` using historical IPL `matches.csv` and `deliveries.csv` ball-by-ball data:

- **Preprocessing:** `ColumnTransformer` with `OneHotEncoder` on categorical features (`batting_team`, `bowling_team`, `city`)
- **Algorithm:** Logistic Regression (`liblinear` solver), wrapped in an `sklearn.pipeline.Pipeline`
- **Target variable:** Whether the batting team won the match
- The trained pipeline is serialized to `pipe.pkl` and loaded directly by the Streamlit app for inference

> The notebook also experiments with a `RandomForestClassifier`, which achieved higher accuracy on the test set, as an alternative to Logistic Regression.

## 📁 Project Structure

```
render/
├── app.py                # Streamlit web app (loads pipe.pkl and serves predictions)
├── pipe.pkl               # Trained scikit-learn pipeline (preprocessing + model)
├── IPL Project.ipynb      # Notebook: data cleaning, feature engineering, model training
├── requirements.txt       # Python dependencies
└── README.md
```

## 🛠️ Tech Stack

- Python
- pandas, numpy
- scikit-learn
- Streamlit

## 🚀 Getting Started

### Prerequisites

- Python 3.9+

### Installation

```bash
git clone https://github.com/Abhishek-Kumar2006/render.git
cd render
pip install -r requirements.txt
```

### Run Locally

```bash
streamlit run app.py
```

The app will open in your browser, typically at `http://localhost:8501`.

## 🏟️ Supported Teams

Chennai Super Kings, Delhi Capitals, Kings XI Punjab, Kolkata Knight Riders, Mumbai Indians, Rajasthan Royals, Royal Challengers Bangalore, Sunrisers Hyderabad

## 🌆 Supported Host Cities

Includes major Indian venues (Mumbai, Chennai, Bangalore, Delhi, Kolkata, Hyderabad, Jaipur, Chandigarh, Pune, Ahmedabad, and more) as well as international venues (Cape Town, Durban, Johannesburg, Sharjah, Abu Dhabi, and others).

## 📊 Dataset

The model is trained on the classic Kaggle IPL dataset (`matches.csv` and `deliveries.csv`), covering ball-by-ball data across IPL seasons.

## 📄 License

No license specified. Feel free to open an issue or reach out to the repository owner if you'd like to use this project.

## 🙋 Author

**Abhishek-Kumar2006** — [GitHub](https://github.com/Abhishek-Kumar2006)
