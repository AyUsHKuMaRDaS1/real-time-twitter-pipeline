# Real-Time Twitter Data Pipeline

## 📊 Overview
This project builds a real-time data pipeline to stream tweets from Twitter, push them to Kafka, process them using PySpark, and load them into BigQuery for SQL-based analytics.

## 🧰 Architecture
```
Twitter API --> Kafka (Docker) --> PySpark (Structured Streaming) --> BigQuery (GCP)
```

## 📄 Folder Structure
```
real-time-twitter-pipeline/
├── docker/                # Kafka + Zookeeper setup
├── ingestion/             # Twitter to Kafka producer
├── processing/            # PySpark to BigQuery consumer
├── config.json            # Configs for Spark & BigQuery
├── requirements.txt       # Python dependencies
├── .env.example           # Template for secrets
├── .gitignore             # Ignore sensitive/local files
└── README.md              # Project guide
```

## 📖 How to Run

### 1. Start Kafka
```bash
cd docker
docker-compose up
```

### 2. Start Tweet Ingestion
Edit `twitter_producer.py` and paste your Twitter Bearer Token:
```python
BEARER_TOKEN = "your_actual_token"
```
Then run:
```bash
python ingestion/twitter_producer.py
```

### 3. Start Spark Stream
Edit `config.json` and update:
- `gcp_project`
- `bigquery_dataset`
- `bigquery_table`
- `gcs_temp_bucket`

Then run:
```bash
spark-submit processing/spark_stream.py
```

## 🎯 Output
Tweets with `id` and `text` fields will be stored in your BigQuery table in real time.
