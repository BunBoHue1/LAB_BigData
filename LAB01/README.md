# Big Data Lab 01: Introduction to Big Data Processing

This laboratory exercise introduces the fundamental concepts of Big Data processing using Apache Spark and Apache Kafka. It covers environment setup, data ingestion from Kaggle, streaming data into Kafka, and performing basic data analysis with PySpark.

## 1. Project Overview

In this lab, we:
- Set up a virtual environment on Ubuntu (WSL).
- Configure a local Kafka cluster using Docker Compose.
- Download the MovieLens dataset automatically using `kagglehub`.
- Push the datasets (`movies`, `ratings`, `tags`) into Kafka topics.
- Consume the data from Kafka using PySpark Structured Streaming.
- Perform analytical queries:
  - Finding the top 5 movies by average rating (with more than 30 reviews).
  - Identifying the 5 "worst" tags based on average movie ratings.
  - Analyzing movies associated with the worst tags.

---

## 2. Environment Setup

### 2.1. Ubuntu (WSL) Configuration
It is recommended to run this lab on **Ubuntu via WSL** (Windows Subsystem for Linux) or a native Linux environment.

1. Open your Ubuntu terminal.
2. Ensure you have Python 3.12+ installed.

### 2.2. Setting Up the Virtual Environment
Create and activate a Python virtual environment to isolate the project dependencies:

```bash
# Create a virtual environment named 'venv'
python -m venv venv

# Activate the virtual environment
source venv/bin/activate
```

### 2.3. Installing Dependencies
Install the required Python packages for PySpark, Kafka, Kaggle integration, and JupyterLab:

```bash
pip install pyspark==4.0.1 kagglehub confluent-kafka jupyterlab
```

---

## 3. Kafka Cluster Setup

We use Docker to quickly spin up a Kafka cluster. The cluster uses the configuration defined in the root directory.

1. Ensure Docker Desktop (or Docker Engine) is installed and running on your system.
2. Navigate to the main repository directory (`LAB_BigData`) where the `docker-compose.yml` file is located.
3. Start the Kafka cluster in detached mode:

```bash
docker compose up -d
```

4. Verify that the containers are running successfully:

```bash
docker ps
```
*Note: The Kafka brokers will be accessible at `localhost:9092`, `localhost:9192`, and `localhost:9292`.*

---

## 4. Running the Data Analysis

Once the environment is prepared and the Kafka cluster is running, you can execute the analysis using the provided Jupyter Notebook.

### 4.1. Start Jupyter Lab

Ensure your virtual environment is activated, then start Jupyter:

```bash
jupyter lab
```

### 4.2. Execute `run.ipynb`
Open the `run.ipynb` file inside the `LAB01` folder and run the cells sequentially to execute the pipeline:

1. **Spark Initialization**: The notebook establishes a Spark session configured to communicate with Kafka.
2. **Data Download**: It automatically downloads the MovieLens dataset from Kaggle via `kagglehub`.
3. **Kafka Topic Creation**: The notebook creates three topics (`ratings`, `movies`, `tags`) with a replication factor of 3.
4. **Data Ingestion**: Pushes the structured data into the respective Kafka topics.
5. **Data Processing & Analysis**:
   - **Problem 1**: Consume the data stream from Kafka topics.
   - **Problem 2**: Filter and aggregate to find the top 5 movies by average rating.
   - **Problem 3**: Join dataframes to find the 5 lowest-rated tags.
   - **Problem 4**: Analyze the specific movies associated with those worst tags.

---

## 5. Troubleshooting

- **Spark Version Issues**: Ensure you are using exactly `pyspark==4.0.1` as newer or older versions might have compatibility issues with the Spark-Kafka packages.
- **Kafka Connection Refused**: Make sure your Docker containers are running (`docker ps`). Check if ports `9092, 9192, 9292` are available and not blocked by a firewall.
- **Missing Dataset**: Ensure you have a stable internet connection for `kagglehub` to properly download the MovieLens dataset.
