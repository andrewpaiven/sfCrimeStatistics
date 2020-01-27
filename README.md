# Udacity Data Streaming Nanodegree

## Project 2 - SF Crime Statistics

### Requirements

- Spark 2.4.3
- Scala 2.11.x
- Java 1.8.x
- Kafka build with Scala 2.11.x
- Python 3.6.x or 3.7
- Docker and docker-compose

### How to run this project

#### Starting Kafka
1. Open a terminal and run on this folder: ```docker-compose up``` to start Kafka and Zookeeper. Wait a bit until kafka and zookeeper start

#### Producing messages into kafka
1. Open a new terminal and run: ```python kafka_server.py```

#### Peeking into Kafka data

In order to see data flowing through kafka, you can connect to the kafka docker container and use the kafka-console-consumer to peek into the data

1. Open a new terminal and type ```docker container ls```

2. Check the id of the kafka docker container and connect to its terminal with the following command: ```docker exec -it %id_here% /bin/bash```

3. Peek into the data arriving to kafka with the command: ```kafka-console-consumer --bootstrap-server localhost:9092 --topic com.sfcrime.v1.calls```

#### Starting the spark job

Run the following command:
```spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.4.4 --master local[*] data_stream.py```

### Step 3 questions:

1. How did changing values on the SparkSession property parameters affect the throughput and latency of the data?

The spark property parameters may affect the number of processed rows per second, available on the field processedRowsPerSecond of the progress reports.

2. What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?

One of the hints we can get on whether our configuration is optimal is by the monitoring of processedRowsPerSecond. 

spark.default.parallelism - The default number of partitions in RDDs returned by transformations
spark.streaming.kafka.maxRatePerPartition - Maximum rate at which data will be read from each kafka partition
