# 🌦️ Weather ETL Pipeline with Apache Airflow

This project implements a complete ETL (Extract, Transform, Load) data pipeline using Apache Airflow to fetch, process, and store real-time weather data from the [Open-Meteo API](https://open-meteo.com/). The data is stored in a PostgreSQL database and the entire stack runs in Docker using Docker Compose.

---

## 🧩 Features

- 🌐 Extracts current weather data for London (can be configured for other locations)
- 🔄 Transforms data to extract key weather metrics
- 🗄️ Loads the data into a PostgreSQL database
- 🛠️ Orchestrated using Apache Airflow with CeleryExecutor
- 🐳 Containerized using Docker and Docker Compose

---

## 🏗️ Project Structure

```
.
├── Dockerfile              # Custom Airflow image with required dependencies
├── docker-compose.yml      # Multi-service setup including Airflow, PostgreSQL, Redis
├── etlweather.py           # Airflow DAG that defines the ETL pipeline
└── README.md               # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:

- Docker
- Docker Compose

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/weather-etl-airflow.git
cd weather-etl-airflow
```

### 2. Initialize Airflow

```bash
mkdir -p ./dags ./logs ./plugins
echo -e "AIRFLOW_UID=$(id -u)" > .env
docker-compose up airflow-init
```

### 3. Start the Services

```bash
docker-compose up
```

Airflow Web UI: [http://localhost:8080](http://localhost:8080)  
Default login: `airflow / airflow`

---

## ⚙️ Airflow DAG

The DAG is defined in `etlweather.py` and includes the following tasks:

- `extract_weather_data`: Calls Open-Meteo API using Airflow's `HttpHook`.
- `transform_weather_data`: Parses and structures the weather data.
- `load_weather_data`: Saves the data into a PostgreSQL table (`weather_data`).

---

## 📊 Sample Data Output

| latitude | longitude | temperature | windspeed | winddirection | weathercode | timestamp           |
|----------|-----------|-------------|-----------|---------------|-------------|---------------------|
| 51.5074  | -0.1278   | 17.5        | 15.2      | 230           | 3           | 2025-06-04 12:34:56 |

---

## 🔒 Environment Configuration

- Airflow connections are managed via the UI:
  - `open_meteo_api`: HTTP connection to `https://api.open-meteo.com`
  - `postgres_default`: PostgreSQL connection used for data loading

---

## 🧹 TODOs / Enhancements

- [ ] Parameterize coordinates using Airflow Variables
- [ ] Add data validation and quality checks
- [ ] Configure alerts or retries for failed tasks
- [ ] Extend to multiple cities or forecast data

---

## 📄 License

This project is licensed under the MIT License.
