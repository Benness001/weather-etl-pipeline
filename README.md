# 🌤️Lagos Weather ETL Pipeline

An automated data engineering pipeline that extracts real-time weather data 
for Lagos, Nigeria, transforms it into a structured format, and loads it into 
Snowflake — orchestrated hourly with Apache Airflow.

---

##  Architecture
OpenWeatherMap API → Python ETL → Apache Airflow → Snowflake

---

## 🛠️ Tech Stack

| Layer          | Tool                    |
|----------------|-------------------------|
| Data Source    | OpenWeatherMap API      |
| Language       | Python 3.12             |
| Orchestration  | Apache Airflow 2.9.1    |
| Data Warehouse | Snowflake               |
| Environment    | Ubuntu/WSL              |

---

## 📁 Project Structure

weather_pipeline/
│
├── airflow/
│   └── dags/
│     └── weather_dag.py        # Airflow DAG — orchestrates ETL hourly
│
├── notebooks/                   # Your Databricks notebooks
│   └── weather_etl.py
│
├── scripts/                     # Reusable Python functions
│   ├── extract.py               # Pulls data from OpenWeatherMap API
│   ├── transform.py             # Cleans and structures raw data
│   └── load.py
│
├── config/
│   └── config.py                # API keys, credentials (never push to GitHub!)
│
├── .env                         # Environment variables
├── .gitignore                   # Ignore .env and sensitive files
├── requirements.txt             # Python dependencies
├── test_pipeline.py             # Manual end-to-end test script
└── README.md

---

## ⚙️ Setup Instructions

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/weather-pipeline.git
cd weather-pipeline
```

### 2. Create and activate virtual environment
```bash
python3 -m venv weather_venv
source weather_venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Create your `.env` file
```bash
cp .env.example .env
# Fill in your API keys and Snowflake credentials
```

### 5. Set up Snowflake table
Run the SQL in `snowflake/weather_table.sql` in your Snowflake worksheet.

### 6. Initialize and start Airflow
```bash
export AIRFLOW_HOME=~/weather_pipeline/airflow
airflow db migrate
airflow webserver --port 8080   # Terminal 1
airflow scheduler               # Terminal 2
```

### 7. Trigger the DAG
Visit `http://localhost:8080` and trigger `lagos_weather_etl_pipeline`

---

## 📊 Data Captured Per Run

| Field                | Description                        |
|----------------------|------------------------------------|
| city                 | City name                          |
| country              | Country code                       |
| latitude/longitude   | Geographic coordinates             |
| temperature_c        | Current temperature in Celsius     |
| feels_like_c         | Feels like temperature             |
| humidity_pct         | Humidity percentage                |
| pressure_hpa         | Atmospheric pressure               |
| weather_description  | Weather condition description      |
| wind_speed_mps       | Wind speed in metres per second    |
| cloudiness_pct       | Cloud coverage percentage          |
| sunrise/sunset_utc   | Sunrise and sunset times           |
| recorded_at          | Timestamp of data capture          |

---

## 🔐 Security

- All credentials stored in `.env` file
- `.env` excluded from version control via `.gitignore`
- Never hardcoded API keys or passwords

---

## 👤 Author

Your Name — [LinkedIn](https://linkedin.com/in/yourprofile) | 
[GitHub](https://github.com/yourusername)

