# Big Data Lab 03: Graph Analytics with GraphX / GraphFrames

This laboratory exercise introduces graph-parallel computing using **Apache Spark GraphFrames** — a DataFrame-based graph processing library built on top of Spark. It covers building property graphs from real-world data, applying graph algorithms (PageRank, Motif Finding), and analyzing the MovieLens dataset through a graph lens.

## 1. Project Overview

In this lab, we:
- Set up a virtual environment on Ubuntu (WSL) with GraphFrames support.
- Reuse the MovieLens Kafka pipeline from Lab 01 & Lab 02 (via a standalone setup notebook).
- Construct a bipartite **User → Movie** graph using GraphFrames.
- Solve 4 exercises using graph operations:
  - **Exercise 0**: Read and prepare data from Kafka (movies, ratings, tags).
  - **Exercise 1**: Detect popularity bias via in-degree and weighted in-degree analysis.
  - **Exercise 2**: Rank the 20 most relevant movies using global PageRank.
  - **Exercise 3 (Bonus)**: Identify the 10 most polarizing movies using Motif Finding.

---

## 2. Learning Objectives

- Understand the **property graph model**: vertices and edges with typed attributes.
- Build **bipartite GraphFrames** from Spark DataFrames.
- Apply graph algorithms:
  - **In-Degree / Weighted In-Degree** → popularity metrics
  - **PageRank** → relevance ranking via link authority
  - **Motif Finding** → pattern-based subgraph queries
- Distinguish between DataFrame-based solutions and graph-based solutions for the same problem.

---

## 3. System Architecture

The pipeline consists of two stages:

### Stage 1: Data Setup (`lab03_data_setup.ipynb`)
- Downloads the MovieLens dataset via `kagglehub`.
- Creates Kafka topics: `Lab1_movies`, `Lab1_ratings`, `Lab1_tags`.
- Pushes all data into Kafka in JSON format (one-time setup).
- Verifies data integrity by reading back from Kafka.

### Stage 2: Graph Analysis (`lab3_solution.ipynb`)
- Reads data from Kafka topics (batch mode).
- Constructs a GraphFrame with `9,742` movie vertices and `610` user vertices.
- Exercises:
  - **Exercise 0**: Schema definition + Kafka batch read
  - **Exercise 1**: `inDegrees` + `edges.groupBy().agg()` → Popularity Bias
  - **Exercise 2**: `g.pageRank(resetProbability=0.15, maxIter=5)` → Top-20 relevant movies
  - **Exercise 3**: `g.find("(u1)-[e1]->(m); (u2)-[e2]->(m)")` → Polarization analysis

---

## 4. Environment Setup

### 4.1. Ubuntu (WSL) Configuration

It is recommended to run this lab on **Ubuntu via WSL** (Windows Subsystem for Linux) or a native Linux environment.

1. Open your Ubuntu terminal.
2. Ensure you have Python 3.12+ installed.

> **Important**: Do **not** use the existing `venv/` folder — it is a Windows virtual environment and will not work on WSL/Ubuntu.

### 4.2. Setting Up the Virtual Environment

Create a dedicated Linux virtual environment named `venv_wsl`:

```bash
# Navigate to the root lab directory
cd '/mnt/e/HK 252/Big Data/Lab 1 2 3 4/LAB_BigData'

# Create a new Linux-compatible virtual environment
python3 -m venv venv_wsl

# Activate it
source venv_wsl/bin/activate
```

### 4.3. Installing Dependencies

Install all required packages, including GraphFrames Python client and NumPy:

```bash
pip install pyspark==4.0.1 kagglehub confluent-kafka numpy graphframes-py==0.11.0 jupyterlab ipykernel
```

*Note: `graphframes-py==0.11.0` is the official Python client for GraphFrames 0.11.0. The matching JVM JAR (`io.graphframes:graphframes-spark4_2.13:0.11.0`) is downloaded automatically by Spark on first run.*

---

## 5. Kafka Cluster Setup

We reuse the same Docker-based Kafka cluster defined in the root directory.

1. Ensure Docker Desktop (or Docker Engine) is installed and running.
2. Navigate to the root repository directory (`LAB_BigData`):

```bash
cd '/mnt/e/HK 252/Big Data/Lab 1 2 3 4/LAB_BigData'
```

3. If any previous containers are conflicting, remove them first:

```bash
docker rm -f broker-1 broker-2 broker-3 zookeeper
```

4. Start the Kafka cluster in detached mode:

```bash
docker compose up -d
```

5. Verify containers are running:

```bash
docker ps
```

*Note: Kafka brokers are accessible at `localhost:9092`, `localhost:9192`, and `localhost:9292`.*

---

## 6. Running the Lab

Once the environment is prepared and the Kafka cluster is running, execute the notebooks in order.

### 6.1. Start Jupyter Lab

Ensure `venv_wsl` is activated, then start Jupyter:

```bash
source venv_wsl/bin/activate
jupyter lab
```

### 6.2. Step 1 — Run `lab03_data_setup.ipynb` (One-time Setup)

Open `LAB03/lab03_data_setup.ipynb` and run all cells sequentially:

1. **Spark Initialization**: Creates a SparkSession with Kafka support (`local[*]` mode).
2. **Data Download**: Downloads the MovieLens dataset from Kaggle via `kagglehub`.
3. **Topic Management**: Deletes old topics (if any) and recreates `Lab1_movies`, `Lab1_ratings`, `Lab1_tags`.
4. **Data Push**: Pushes all CSV data into Kafka in JSON format (100,836 ratings, 9,742 movies, 3,683 tags).
5. **Verification**: Reads back from Kafka and prints record counts to confirm success.

> This notebook only needs to be run **once**. Skip it on subsequent runs if Kafka already has the data.

### 6.3. Step 2 — Run `lab3_solution.ipynb`

Open `LAB03/lab3_solution.ipynb` and run all cells sequentially:

1. **Spark + GraphFrames Initialization**: Creates a SparkSession with both Kafka and GraphFrames JARs. Sets a local checkpoint directory (required for `connectedComponents`).
2. **Exercise 0 — Data Preparation**: Reads `Lab1_movies`, `Lab1_ratings`, `Lab1_tags` from Kafka using defined schemas. DataFrames are cached to avoid repeated Kafka reads.
3. **Graph Construction**: Builds a bipartite GraphFrame:
   - Vertices: Movies (type=`movie`) + Users (type=`user`)
   - Edges: Ratings (User → Movie) with `weight = rating`
4. **Exercise 1 — Popularity Bias**:
   - Computes `inDegrees` (num_raters) and weighted in-degree (total_rating_score) per movie.
   - Outputs Top-20 movies with both metrics.
5. **Exercise 2 — PageRank**:
   - Runs `g.pageRank(resetProbability=0.15, maxIter=5)` on the full graph.
   - Outputs Top-20 movies by PageRank score with genres.
6. **Exercise 3 (Bonus) — Polarization via Motifs**:
   - Uses `g.find("(u1)-[e1]->(m); (u2)-[e2]->(m)")` to find user pairs rating the same movie.
   - Filters pairs where `|rating1 - rating2| >= 3.0`.
   - Outputs Top-10 most polarizing movies with `movieId`, `title`, and `polarized_pairs` count.

---

## 7. Troubleshooting

- **`No module named 'numpy'`**: Run `pip install numpy` in the activated `venv_wsl` environment. `graphframes-py` depends on it transitively through `pyspark.ml`.
- **`ModuleNotFoundError: No module named 'graphframes'`**: Ensure you ran `pip install graphframes-py==0.11.0` and are using the `venv_wsl` kernel in Jupyter (not the Windows `venv`).
- **Kafka `AnalysisException` / empty DataFrames**: The data topics do not exist or are empty. Re-run `lab03_data_setup.ipynb` to repopulate them.
- **Docker container name conflict**: Run `docker rm -f broker-1 broker-2 broker-3 zookeeper` before `docker compose up -d`.
- **Spark JARs download fails (Ivy error)**: Ensure you have a stable internet connection on first run. The JARs are cached in `~/.ivy2.5.2/` for subsequent runs.
- **PageRank / ConnectedComponents hangs**: Verify that the checkpoint directory was set (`spark.sparkContext.setCheckpointDir(...)`). Without it, GraphFrames iterative algorithms will fail.
