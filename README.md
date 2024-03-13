# Pinterest-Data-Pipeline

This pipeline will extract, transform and load data from an API using batch processing and stream processing, using the following Apache services:
- Apache Spark
- Apache Kafka
- Apache Airflow
- Apache Kinesis

These services will be used in conjunction with AWS, which will contain an EC2 instance as an Apache client machine.

# Technologies Used

- ***`Apache Kafka`*** 
- ***`Apache Spark`***    
- ***`Apache Airflow`***   
- ***`Apache Kinesis`***
- ***`Databricks`***
- ***`SQL`***
- ***`Python`***
- ***`AWS`***

# Prerequisites

- Set up environment on AWS and GitHub
- .pem file extension was created to save the key-pair file locally. Which would allow me to connect to my EC2 instance
- Connect EC2 instance in the terminal using ***`SSH Client`***.
- Install ***`Java`*** on Amazon CLI
- Make note of ARN, Bootstrap server string and Zookeeper string

# Amazon Managed Streaming for Apache Kafka (MSK)

To set up an MSK cluster, a ***`client.properties`*** file will need to be made with the appropriate credentials inside your ***`Kafka_folder/bin`*** directory
Then create topics using the Apache create topics command.

Three topics made:
<your_UserId>.pin for the Pinterest posts data
<your_UserId>.geo for the post geolocation data
<your_UserId>.user for the post user data

