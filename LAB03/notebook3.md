{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "2a2fd814",
   "metadata": {},
   "source": [
    "# GraphX\n",
    "Prerequisites:\n",
    "- io.graphframes:graphframes-spark4_2.13:0.9.3 in your SparkSession spark.jars.packages config\n",
    "- pip install graphframes-py"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "91c67710",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "WARNING: Using incubator modules: jdk.incubator.vector\n",
      ":: loading settings :: url = jar:file:/home/hpcc/spark/jars/ivy-2.5.3.jar!/org/apache/ivy/core/settings/ivysettings.xml\n",
      "Ivy Default Cache set to: /home/hpcc/.ivy2.5.2/cache\n",
      "The jars for the packages stored in: /home/hpcc/.ivy2.5.2/jars\n",
      "io.graphframes#graphframes-spark4_2.13 added as a dependency\n",
      "org.apache.spark#spark-sql-kafka-0-10_2.13 added as a dependency\n",
      "org.apache.kafka#kafka-clients added as a dependency\n",
      "org.apache.spark#spark-streaming-kafka-0-10_2.13 added as a dependency\n",
      "org.apache.hadoop#hadoop-aws added as a dependency\n",
      ":: resolving dependencies :: org.apache.spark#spark-submit-parent-2b7910b9-a1f5-42e8-92bf-be90697665da;1.0\n",
      "\tconfs: [default]\n",
      "\tfound io.graphframes#graphframes-spark4_2.13;0.9.3 in central\n",
      "\tfound org.apache.spark#spark-sql-kafka-0-10_2.13;4.0.1 in central\n",
      "\tfound org.apache.spark#spark-token-provider-kafka-0-10_2.13;4.0.1 in central\n",
      "\tfound org.apache.kafka#kafka-clients;3.9.1 in central\n",
      "\tfound com.github.luben#zstd-jni;1.5.6-9 in central\n",
      "\tfound org.lz4#lz4-java;1.8.0 in central\n",
      "\tfound org.xerial.snappy#snappy-java;1.1.10.7 in central\n",
      "\tfound org.slf4j#slf4j-api;2.0.16 in central\n",
      "\tfound org.apache.hadoop#hadoop-client-runtime;3.4.1 in central\n",
      "\tfound org.apache.hadoop#hadoop-client-api;3.4.1 in central\n",
      "\tfound com.google.code.findbugs#jsr305;3.0.0 in central\n",
      "\tfound org.scala-lang.modules#scala-parallel-collections_2.13;1.2.0 in central\n",
      "\tfound org.apache.commons#commons-pool2;2.12.0 in central\n",
      "\tfound org.apache.spark#spark-streaming-kafka-0-10_2.13;4.0.1 in central\n",
      "\tfound org.apache.hadoop#hadoop-aws;3.4.1 in central\n",
      "\tfound software.amazon.awssdk#bundle;2.24.6 in central\n",
      "\tfound org.wildfly.openssl#wildfly-openssl;1.1.3.Final in central\n",
      ":: resolution report :: resolve 895ms :: artifacts dl 26ms\n",
      "\t:: modules in use:\n",
      "\tcom.github.luben#zstd-jni;1.5.6-9 from central in [default]\n",
      "\tcom.google.code.findbugs#jsr305;3.0.0 from central in [default]\n",
      "\tio.graphframes#graphframes-spark4_2.13;0.9.3 from central in [default]\n",
      "\torg.apache.commons#commons-pool2;2.12.0 from central in [default]\n",
      "\torg.apache.hadoop#hadoop-aws;3.4.1 from central in [default]\n",
      "\torg.apache.hadoop#hadoop-client-api;3.4.1 from central in [default]\n",
      "\torg.apache.hadoop#hadoop-client-runtime;3.4.1 from central in [default]\n",
      "\torg.apache.kafka#kafka-clients;3.9.1 from central in [default]\n",
      "\torg.apache.spark#spark-sql-kafka-0-10_2.13;4.0.1 from central in [default]\n",
      "\torg.apache.spark#spark-streaming-kafka-0-10_2.13;4.0.1 from central in [default]\n",
      "\torg.apache.spark#spark-token-provider-kafka-0-10_2.13;4.0.1 from central in [default]\n",
      "\torg.lz4#lz4-java;1.8.0 from central in [default]\n",
      "\torg.scala-lang.modules#scala-parallel-collections_2.13;1.2.0 from central in [default]\n",
      "\torg.slf4j#slf4j-api;2.0.16 from central in [default]\n",
      "\torg.wildfly.openssl#wildfly-openssl;1.1.3.Final from central in [default]\n",
      "\torg.xerial.snappy#snappy-java;1.1.10.7 from central in [default]\n",
      "\tsoftware.amazon.awssdk#bundle;2.24.6 from central in [default]\n",
      "\t---------------------------------------------------------------------\n",
      "\t|                  |            modules            ||   artifacts   |\n",
      "\t|       conf       | number| search|dwnlded|evicted|| number|dwnlded|\n",
      "\t---------------------------------------------------------------------\n",
      "\t|      default     |   17  |   0   |   0   |   0   ||   17  |   0   |\n",
      "\t---------------------------------------------------------------------\n",
      ":: retrieving :: org.apache.spark#spark-submit-parent-2b7910b9-a1f5-42e8-92bf-be90697665da\n",
      "\tconfs: [default]\n",
      "\t0 artifacts copied, 17 already retrieved (0kB/19ms)\n",
      "25/09/16 09:17:04 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable\n",
      "Setting default log level to \"WARN\".\n",
      "To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).\n",
      "25/09/16 09:17:12 WARN MetricsConfig: Cannot locate configuration: tried hadoop-metrics2-s3a-file-system.properties,hadoop-metrics2.properties\n",
      "SLF4J: Failed to load class \"org.slf4j.impl.StaticLoggerBinder\".\n",
      "SLF4J: Defaulting to no-operation (NOP) logger implementation\n",
      "SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.\n"
     ]
    }
   ],
   "source": [
    "from pyspark.sql import SparkSession\n",
    "from pyspark.sql.functions import * \n",
    "spark = (SparkSession.builder.master(\"spark://bd-1:7077\")\\\n",
    ".config(\"spark.jars.packages\", \"io.graphframes:graphframes-spark4_2.13:0.9.3,org.apache.spark:spark-sql-kafka-0-10_2.13:4.0.1,org.apache.kafka:kafka-clients:3.9.1,org.apache.spark:spark-streaming-kafka-0-10_2.13:4.0.1,org.apache.hadoop:hadoop-aws:3.4.1\")\\\n",
    ".config(\"spark.hadoop.fs.s3a.endpoint\", \"http://10.1.11.5:9000\")\n",
    ".config(\"spark.hadoop.fs.s3a.access.key\", \"test\")\n",
    ".config(\"spark.hadoop.fs.s3a.secret.key\", \"hcmuthpcc\")\n",
    ".config(\"spark.hadoop.fs.s3a.path.style.access\", \"true\")\n",
    ".config(\"spark.hadoop.fs.s3a.aws.credentials.provider\", \"org.apache.hadoop.fs.s3a.SimpleAWSCredentialsProvider\")\n",
    ".config(\"spark.hadoop.fs.s3a.impl\", \"org.apache.hadoop.fs.s3a.S3AFileSystem\")\n",
    ".config(\"spark.hadoop.fs.s3a.committer.name\", \"magic\")\n",
    ".config(\"spark.hadoop.fs.s3a.committer.magic.partitioned.enabled\", \"true\")\n",
    ".config(\"spark.hadoop.fs.s3a.fast.upload\", \"true\")\n",
    ".config(\"spark.hadoop.fs.s3a.fast.upload.buffer\", \"disk\")\n",
    ".config(\"spark.hadoop.fs.s3a.committer.staging.conflict-mode\", \"replace\")\n",
    ".config(\"spark.hadoop.fs.s3a.committer.staging.abort.pending.uploads\", \"true\")\n",
    ".appName(\"Lab3\").getOrCreate())\n",
    "\n",
    "spark.sparkContext.setCheckpointDir(\"s3a://big-data/test/checkpoint/\") # Set checkpoint directory"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "1c02e4a0",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "\"Introduction to GraphX\\nGraphX is a distributed graph processing framework built on top of Apache Spark. It allows users to create, manipulate, and analyze large-scale graphs in a parallel and fault-tolerant manner. GraphX provides a unified API for both graph and data-parallel computations, making it easier to work with graph data alongside traditional tabular data.\\nConcepts:\\n1. Graph Representation: GraphX represents graphs using two main components: vertices (nodes) and edges (connections between nodes). Each vertex and edge can have associated properties, allowing for rich data representation.\\n2. RDDs: GraphX leverages Spark's Resilient Distributed Datasets (RDDs) to store and process graph data. Vertices and edges are stored as RDDs, enabling distributed computation across a cluster.\\n3. Pregel API: GraphX provides a Pregel-like API for iterative graph processing. This API allows users to define vertex-centric computations, where each vertex can send and receive messages to and from its neighbors in the graph.\\n4. Graph Operators: GraphX includes a variety of built-in graph operators for common graph algorithms, such as PageRank, Connected Components, and Triangle Counting. These operators can be easily applied to graphs to perform complex analyses.\\n5. Integration with Spark SQL: GraphX can be seamlessly integrated with Spark SQL, allowing users to perform SQL queries on graph data and combine graph processing with traditional data processing tasks.\\nUse Cases:\\n1. Social Network Analysis: GraphX can be used to analyze social networks, identify influential users, and detect communities within the network.\\n2. Recommendation Systems: GraphX can help build recommendation systems by analyzing user-item interactions and finding similar users or items.\\n3. Fraud Detection: GraphX can be used to detect fraudulent activities by analyzing transaction networks and identifying suspicious patterns.\\n4. Knowledge Graphs: GraphX can be used to build and analyze knowledge graphs, which represent relationships between entities in a domain.\\nOverall, GraphX is a powerful tool for working with graph data in a distributed computing environment, enabling users to perform complex graph analyses at scale.\\n\""
      ]
     },
     "execution_count": 1,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "\"\"\"Introduction to GraphX\n",
    "GraphX is a distributed graph processing framework built on top of Apache Spark. It allows users to create, manipulate, and analyze large-scale graphs in a parallel and fault-tolerant manner. GraphX provides a unified API for both graph and data-parallel computations, making it easier to work with graph data alongside traditional tabular data.\n",
    "Concepts:\n",
    "1. Graph Representation: GraphX represents graphs using two main components: vertices (nodes) and edges (connections between nodes). Each vertex and edge can have associated properties, allowing for rich data representation.\n",
    "2. RDDs: GraphX leverages Spark's Resilient Distributed Datasets (RDDs) to store and process graph data. Vertices and edges are stored as RDDs, enabling distributed computation across a cluster.\n",
    "3. Pregel API: GraphX provides a Pregel-like API for iterative graph processing. This API allows users to define vertex-centric computations, where each vertex can send and receive messages to and from its neighbors in the graph.\n",
    "4. Graph Operators: GraphX includes a variety of built-in graph operators for common graph algorithms, such as PageRank, Connected Components, and Triangle Counting. These operators can be easily applied to graphs to perform complex analyses.\n",
    "5. Integration with Spark SQL: GraphX can be seamlessly integrated with Spark SQL, allowing users to perform SQL queries on graph data and combine graph processing with traditional data processing tasks.\n",
    "Use Cases:\n",
    "1. Social Network Analysis: GraphX can be used to analyze social networks, identify influential users, and detect communities within the network.\n",
    "2. Recommendation Systems: GraphX can help build recommendation systems by analyzing user-item interactions and finding similar users or items.\n",
    "3. Fraud Detection: GraphX can be used to detect fraudulent activities by analyzing transaction networks and identifying suspicious patterns.\n",
    "4. Knowledge Graphs: GraphX can be used to build and analyze knowledge graphs, which represent relationships between entities in a domain.\n",
    "Overall, GraphX is a powerful tool for working with graph data in a distributed computing environment, enabling users to perform complex graph analyses at scale.\n",
    "\"\"\""
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "6ad7734a",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "                                                                                \r"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "+----------------+-------+------+--------+----------+\n",
      "|       timestamp|user_id|  item|quantity|session_id|\n",
      "+----------------+-------+------+--------+----------+\n",
      "|2024-01-01 10:00|  alice| apple|       2|    sess_1|\n",
      "|2024-01-01 10:05|  alice|banana|       1|    sess_1|\n",
      "|2024-01-01 11:00|    bob|orange|       3|    sess_2|\n",
      "|2024-01-01 14:00|charlie| apple|       1|    sess_3|\n",
      "|2024-01-01 14:10|charlie|banana|       2|    sess_3|\n",
      "|2024-01-02 09:00|  diana|banana|       1|    sess_4|\n",
      "|2024-01-02 15:00|    bob| apple|       1|    sess_5|\n",
      "|2024-01-02 16:00|    eve|orange|       2|    sess_6|\n",
      "|2024-01-02 16:30|  alice|orange|       1|    sess_7|\n",
      "|2024-01-03 12:00|  diana| apple|       1|    sess_8|\n",
      "+----------------+-------+------+--------+----------+\n",
      "\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "                                                                                \r"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "+-------+---------+--------+\n",
      "|user_id|age_group|location|\n",
      "+-------+---------+--------+\n",
      "|  alice|    young|     NYC|\n",
      "|    bob|   middle|     NYC|\n",
      "|charlie|    young|      LA|\n",
      "|  diana|   middle|      LA|\n",
      "|    eve|   senior|     NYC|\n",
      "+-------+---------+--------+\n",
      "\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "                                                                                \r"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "+------+-----+--------+\n",
      "|  item|price|category|\n",
      "+------+-----+--------+\n",
      "| apple|  1.2|   fruit|\n",
      "|banana|  0.8|   fruit|\n",
      "|orange|  1.5|   fruit|\n",
      "+------+-----+--------+\n",
      "\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "                                                                                \r"
     ]
    }
   ],
   "source": [
    "from pyspark.sql.types import *\n",
    "from pyspark.sql.functions import *\n",
    "# Transaction Data - 10 carefully crafted rows\n",
    "transaction_data = [\n",
    "    (\"2024-01-01 10:00\", \"alice\", \"apple\", 2, \"sess_1\"),\n",
    "    (\"2024-01-01 10:05\", \"alice\", \"banana\", 1, \"sess_1\"),  # Same session co-purchase\n",
    "    (\"2024-01-01 11:00\", \"bob\", \"orange\", 3, \"sess_2\"),\n",
    "    (\"2024-01-01 14:00\", \"charlie\", \"apple\", 1, \"sess_3\"),\n",
    "    (\"2024-01-01 14:10\", \"charlie\", \"banana\", 2, \"sess_3\"), # Same session co-purchase\n",
    "    (\"2024-01-02 09:00\", \"diana\", \"banana\", 1, \"sess_4\"),   # Different day\n",
    "    (\"2024-01-02 15:00\", \"bob\", \"apple\", 1, \"sess_5\"),     # Bob buys apple later (influence?)\n",
    "    (\"2024-01-02 16:00\", \"eve\", \"orange\", 2, \"sess_6\"),\n",
    "    (\"2024-01-02 16:30\", \"alice\", \"orange\", 1, \"sess_7\"),  # Alice tries new item\n",
    "    (\"2024-01-03 12:00\", \"diana\", \"apple\", 1, \"sess_8\")    # Diana influenced by others?\n",
    "]\n",
    "\n",
    "user_data = [\n",
    "    (\"alice\", \"young\", \"NYC\"),\n",
    "    (\"bob\", \"middle\", \"NYC\"), \n",
    "    (\"charlie\", \"young\", \"LA\"),\n",
    "    (\"diana\", \"middle\", \"LA\"),\n",
    "    (\"eve\", \"senior\", \"NYC\")\n",
    "]\n",
    "\n",
    "item_data = [\n",
    "    (\"apple\", 1.20, \"fruit\"),\n",
    "    (\"banana\", 0.80, \"fruit\"), \n",
    "    (\"orange\", 1.50, \"fruit\")\n",
    "]\n",
    "\n",
    "# Create DataFrames\n",
    "transaction_schema = StructType([\n",
    "    StructField(\"timestamp\", StringType(), True),\n",
    "    StructField(\"user_id\", StringType(), True),\n",
    "    StructField(\"item\", StringType(), True),\n",
    "    StructField(\"quantity\", IntegerType(), True),\n",
    "    StructField(\"session_id\", StringType(), True)\n",
    "])\n",
    "\n",
    "transactions_df = spark.createDataFrame(transaction_data, transaction_schema)\n",
    "users_df = spark.createDataFrame(user_data, [\"user_id\", \"age_group\", \"location\"])\n",
    "items_df = spark.createDataFrame(item_data, [\"item\", \"price\", \"category\"])\n",
    "\n",
    "transactions_df.show()\n",
    "users_df.show()\n",
    "items_df.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b874f141",
   "metadata": {},
   "source": [
    "## Problem: User-Item Purchase Network Analysis\n",
    "Find users who bought items that are 'unique' to their location - items that no other user in the same city purchased."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "ab72d4d0",
   "metadata": {},
   "source": [
    "### DataFrame"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "e19af738",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "DataFrame approach result:\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "                                                                                \r"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "+-------+------+--------+\n",
      "|user_id|  item|location|\n",
      "+-------+------+--------+\n",
      "|  alice|banana|     NYC|\n",
      "+-------+------+--------+\n",
      "\n"
     ]
    }
   ],
   "source": [
    "# Step 1: Get all user-item-location combinations\n",
    "user_items = transactions_df.join(users_df, \"user_id\") \\\n",
    "    .select(\"user_id\", \"item\", \"location\").distinct()\n",
    "\n",
    "# Step 2: Count users per item per location\n",
    "item_location_counts = user_items.groupBy(\"item\", \"location\") \\\n",
    "    .agg({\"user_id\": \"count\"}) \\\n",
    "    .withColumnRenamed(\"count(user_id)\", \"user_count\")\n",
    "\n",
    "# Step 3: Find items with only 1 user per location\n",
    "unique_items = item_location_counts.filter(\"user_count = 1\") \\\n",
    "    .select(\"item\", \"location\")\n",
    "\n",
    "# Step 4: Join back to find which users bought these unique items\n",
    "result_df = user_items.join(unique_items, [\"item\", \"location\"]) \\\n",
    "    .select(\"user_id\", \"item\", \"location\")\n",
    "\n",
    "print(\"DataFrame approach result:\")\n",
    "result_df.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "1a3a971a",
   "metadata": {},
   "source": [
    "### GraphX"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "1dabaa49",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Graph created:\n",
      "Vertices: 8\n",
      "Edges: 10\n",
      "GraphX approach result:\n",
      "+------+--------+----------+\n",
      "|   dst|property|user_count|\n",
      "+------+--------+----------+\n",
      "|banana|     NYC|         1|\n",
      "+------+--------+----------+\n",
      "\n"
     ]
    }
   ],
   "source": [
    "from pyspark.sql.functions import *\n",
    "from graphframes import *\n",
    "\n",
    "# Which to be used as id/type/property? Rule of thumb\n",
    "# - id: Unique identifier for vertices (e.g., user_id, item_id)\n",
    "# - type: Type of the vertex (e.g., user, item)\n",
    "# - property: Additional attributes or features of the vertex (e.g., location, category)\n",
    "\n",
    "# Create User-Item bipartite graph\n",
    "# Vertices: users + items with their properties\n",
    "user_vertices = users_df.select(\n",
    "    col(\"user_id\").alias(\"id\"),             \n",
    "    lit(\"user\").alias(\"type\"),\n",
    "    col(\"location\").alias(\"property\")\n",
    ")\n",
    "\n",
    "item_vertices = items_df.select(\n",
    "    col(\"item\").alias(\"id\"),\n",
    "    lit(\"item\").alias(\"type\"),\n",
    "    col(\"category\").alias(\"property\")\n",
    ")\n",
    "\n",
    "vertices = user_vertices.union(item_vertices)\n",
    "\n",
    "# Which to be used as src/dst/relationship? Rule of thumb\n",
    "# - src: Source vertex id (e.g., user_id)\n",
    "# - dst: Destination vertex id (e.g., item_id)\n",
    "# - relationship: Type of relationship (e.g., \"purchased\", \"viewed\")\n",
    "# In this case, we want to create edges based on user-item purchases\n",
    "# -> \"purchased\"\n",
    "\n",
    "# Edges: user -> item purchases\n",
    "edges = transactions_df.select(\n",
    "    col(\"user_id\").alias(\"src\"),\n",
    "    col(\"item\").alias(\"dst\"),\n",
    "    lit(\"purchased\").alias(\"relationship\")\n",
    ").distinct()\n",
    "\n",
    "# Create GraphFrame\n",
    "# In this graphframe, vertices represent users and items, while edges represent user-item interactions (purchases).\n",
    "graph = GraphFrame(vertices, edges)\n",
    "\n",
    "print(\"Graph created:\")\n",
    "print(f\"Vertices: {graph.vertices.count()}\")\n",
    "print(f\"Edges: {graph.edges.count()}\")\n",
    "\n",
    "# Find items unique to each location using graph operations\n",
    "# In a graph mindset, we're trying to find items (dst) that are connected to users (src) from only one location (property).\n",
    "user_item_edges = graph.edges.join(\n",
    "    graph.vertices.filter(\"type = 'user'\").select(\"id\", \"property\"),\n",
    "    graph.edges.src == col(\"id\")\n",
    ").select(\"dst\", \"property\")\n",
    "\n",
    "\n",
    "# Count users per item per location using graph structure\n",
    "item_location_counts = user_item_edges.groupBy(\"dst\", \"property\") \\\n",
    "    .count().withColumnRenamed(\"count\", \"user_count\")\n",
    "\n",
    "unique_items_graph = item_location_counts.filter(\"user_count = 1\")\n",
    "\n",
    "print(\"GraphX approach result:\")\n",
    "unique_items_graph.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3bb5834b",
   "metadata": {},
   "source": [
    "## Problem: Purchase Influence Network\n",
    "Build a user similarity network and find communities of users with similar purchasing behaviors"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a3f2454e",
   "metadata": {},
   "source": [
    "### DataFrame"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "0d38792c",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "DataFrame approach: Too complex for practical demonstration!\n",
      "Would require nested loops, multiple joins, and manual graph traversal\n"
     ]
    }
   ],
   "source": [
    "# This would require multiple complex self-joins and window functions\n",
    "# to compare each user's purchase set with every other user's purchase set\n",
    "# Then apply some similarity threshold and find connected components manually\n",
    "# (Code would be 20+ lines of complex SQL logic)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "fa6aa692",
   "metadata": {},
   "source": [
    "### GraphX"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "7fa8e1cb",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "25/09/16 09:19:31 WARN ConnectedComponents$: The DataFrame returned by ConnectedComponents is persisted and loaded.\n",
      "/home/hpcc/.local/lib/python3.10/site-packages/pyspark/sql/classic/dataframe.py:128: UserWarning: DataFrame constructor is internal. Do not directly use it.\n",
      "  warnings.warn(\"DataFrame constructor is internal. Do not directly use it.\")\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "User communities based on purchase similarity:\n",
      "+-------+--------+---------+------------+\n",
      "|     id|location|age_group|   component|\n",
      "+-------+--------+---------+------------+\n",
      "|  alice|     NYC|    young|420906795008|\n",
      "|    bob|     NYC|   middle|420906795008|\n",
      "|charlie|      LA|    young|420906795008|\n",
      "|  diana|      LA|   middle|420906795008|\n",
      "|    eve|     NYC|   senior|936302870529|\n",
      "+-------+--------+---------+------------+\n",
      "\n"
     ]
    }
   ],
   "source": [
    "# Step 1: Create user-user similarity edges based on shared purchases\n",
    "user_purchases = transactions_df.groupBy(\"user_id\") \\\n",
    "    .agg(collect_set(\"item\").alias(\"items\"))\n",
    "\n",
    "# Create user similarity edges (users who share 2+ items)\n",
    "user_similarities = (user_purchases.alias(\"u1\")     # You need alias to self-join\n",
    "    .crossJoin(user_purchases.alias(\"u2\"))          # Cartesian product - every row from u1 paired with every row from u2\n",
    "    .filter(col(\"u1.user_id\") != col(\"u2.user_id\")) # Removes self-comparisons (alice compared to alice)\n",
    "    .withColumn(\"shared_items\", size(array_intersect(\"u1.items\", \"u2.items\"))) # array_intersect(\"u1.items\", \"u2.items\"): Finds common items between two users and counts them\n",
    "    .filter(\"shared_items >= 2\")                    # keeps only user pairs who share at least 2 items, won't be connected in the graph otherwise \n",
    "    .select(\n",
    "        col(\"u1.user_id\").alias(\"src\"),\n",
    "        col(\"u2.user_id\").alias(\"dst\"),\n",
    "        lit(\"similar\").alias(\"relationship\")        # \"Draw an edge between user1 and user2, named 'similar'\"\n",
    "    ))\n",
    "\n",
    "# Create user-only graph for community detection\n",
    "user_graph_vertices = users_df.select(\n",
    "    col(\"user_id\").alias(\"id\"),\n",
    "    col(\"location\"),\n",
    "    col(\"age_group\")\n",
    ")\n",
    "\n",
    "user_similarity_graph = GraphFrame(user_graph_vertices, user_similarities)\n",
    "\n",
    "# Find connected components (communities)\n",
    "communities = user_similarity_graph.connectedComponents()\n",
    "\n",
    "print(\"User communities based on purchase similarity:\")\n",
    "communities.select(\"id\", \"location\", \"age_group\", \"component\").show()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "ff920f4d",
   "metadata": {},
   "source": [
    "## Problem 3: Item Co-Purchase Network & Importance Ranking\n",
    "\n",
    "Which items are most 'central' to the purchasing ecosystem? Find items that influence other item purchases."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f9eb26ab",
   "metadata": {},
   "source": [
    "### GraphX"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "b43dfd85",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Item co-purchase network:\n",
      "+------+------+------------+\n",
      "|   src|   dst|relationship|\n",
      "+------+------+------------+\n",
      "| apple|banana|co_purchased|\n",
      "|banana| apple|co_purchased|\n",
      "+------+------+------------+\n",
      "\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "                                                                                \r"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Item importance ranking (PageRank):\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "                                                                                \r"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "+------+-----+-------------------+\n",
      "|    id|price|           pagerank|\n",
      "+------+-----+-------------------+\n",
      "| apple|  1.2| 1.3953488372093024|\n",
      "|banana|  0.8| 1.3953488372093024|\n",
      "|orange|  1.5|0.20930232558139536|\n",
      "+------+-----+-------------------+\n",
      "\n",
      "Item network statistics:\n",
      "Items (vertices): 3\n",
      "Co-purchase relationships (edges): 2\n",
      "Items ranked by co-purchase frequency:\n",
      "+------+--------+\n",
      "|    id|inDegree|\n",
      "+------+--------+\n",
      "| apple|       1|\n",
      "|banana|       1|\n",
      "+------+--------+\n",
      "\n"
     ]
    }
   ],
   "source": [
    "# Step 1: Create item co-purchase network\n",
    "# Items bought in same session are connected\n",
    "\n",
    "co_purchases = (transactions_df.alias(\"t1\") # Use alias to self-join later    \n",
    "    .join(transactions_df.alias(\"t2\"), \"session_id\") # self-join in session_id, pairs up all transactions that happened in the same shopping session -> finds co-purchased items\n",
    "    .filter(col(\"t1.item\") != col(\"t2.item\")) # Remove self-pairs (apple paired with apple,...)\n",
    "    .select(                                    # Transform into edge format for GraphX\n",
    "        col(\"t1.item\").alias(\"src\"),            # First item in the pair\n",
    "        col(\"t2.item\").alias(\"dst\"),            # Second item in the pair\n",
    "        lit(\"co_purchased\").alias(\"relationship\") # Edge labeled \"co_purchased\"\n",
    "    ).distinct())                   # Remove duplicate edges (apple->banana and banana->apple are the same in undirected graph)\n",
    "\n",
    "# Create item graph\n",
    "item_graph_vertices = items_df.select(\n",
    "    col(\"item\").alias(\"id\"),\n",
    "    col(\"price\"),\n",
    "    col(\"category\")\n",
    ")\n",
    "\n",
    "item_graph = GraphFrame(item_graph_vertices, co_purchases)\n",
    "\n",
    "print(\"Item co-purchase network:\")\n",
    "item_graph.edges.show()\n",
    "\n",
    "# Apply PageRank to find most influential items\n",
    "pagerank_results = item_graph.pageRank(resetProbability=0.15, maxIter=5)\n",
    "\n",
    "print(\"Item importance ranking (PageRank):\")\n",
    "pagerank_results.vertices \\\n",
    "    .select(\"id\", \"price\", \"pagerank\") \\\n",
    "    .orderBy(desc(\"pagerank\")) \\\n",
    "    .show()\n",
    "\n",
    "# Additional graph metrics\n",
    "print(\"Item network statistics:\")\n",
    "print(f\"Items (vertices): {item_graph.vertices.count()}\")\n",
    "print(f\"Co-purchase relationships (edges): {item_graph.edges.count()}\")\n",
    "\n",
    "# In-degree (how often item is co-purchased with others)\n",
    "indegrees = item_graph.inDegrees\n",
    "print(\"Items ranked by co-purchase frequency:\")\n",
    "indegrees.orderBy(desc(\"inDegree\")).show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "a8af2f5d",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "                                                                                \r"
     ]
    }
   ],
   "source": [
    "# Graph persistence: made of vertices and edges, store them and you store the graph\n",
    "# In a production scenario, you might store these in a graph database or as Parquet files\n",
    "item_graph.vertices.write.mode(\"overwrite\").parquet(\"s3a://big-data/test/graphs/item_graph/vertices\")\n",
    "item_graph.edges.write.mode(\"overwrite\").parquet(\"s3a://big-data/test/graphs/item_graph/edges\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "9f42629b",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "+------+-----+--------+\n",
      "|    id|price|category|\n",
      "+------+-----+--------+\n",
      "|banana|  0.8|   fruit|\n",
      "|orange|  1.5|   fruit|\n",
      "| apple|  1.2|   fruit|\n",
      "+------+-----+--------+\n",
      "\n",
      "+------+------+------------+\n",
      "|   src|   dst|relationship|\n",
      "+------+------+------------+\n",
      "| apple|banana|co_purchased|\n",
      "|banana| apple|co_purchased|\n",
      "+------+------+------------+\n",
      "\n",
      "root\n",
      " |-- id: string (nullable = true)\n",
      " |-- price: double (nullable = true)\n",
      " |-- category: string (nullable = true)\n",
      "\n",
      "root\n",
      " |-- src: string (nullable = true)\n",
      " |-- dst: string (nullable = true)\n",
      " |-- relationship: string (nullable = true)\n",
      "\n"
     ]
    }
   ],
   "source": [
    "# Re-read and verify what I said above!\n",
    "v_df = spark.read.parquet(\"s3a://big-data/test/graphs/item_graph/vertices\")\n",
    "e_df = spark.read.parquet(\"s3a://big-data/test/graphs/item_graph/edges\")\n",
    "v_df.show()\n",
    "e_df.show()\n",
    "v_df.printSchema()\n",
    "e_df.printSchema()\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.10.12"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}