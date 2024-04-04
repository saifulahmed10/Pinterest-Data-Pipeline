# Pinterest-Data-Pipeline
![CloudPinterestPipeline](https://github.com/saifulahmed10/Pinterest-Data-Pipeline/assets/149619315/ba7117f4-2da5-4205-ad55-d902074f3839)

## Project Overview

This pipeline extracts, transforms, and loads data from an API using batch processing and stream processing with the following Apache services:
- Apache Spark
- Apache Kafka
- Apache Airflow
- Apache Kinesis

These services are used in conjunction with AWS, which includes an EC2 instance as an Apache client machine.

## Table of Contents

- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Amazon Managed Streaming for Apache Kafka (MSK)](#amazon-managed-streaming-for-apache-kafka-msk)
- [Connecting MSK Cluster to S3 Bucket and Creating a Custom Plugin](#connecting-msk-cluster-to-s3-bucket-and-creating-a-custom-plugin)
- [Mounting S3 Bucket to Databricks](#mounting-s3-bucket-to-databricks)
- [Data Transformation and Data Analysis](#data-transformation-and-data-analysis)
- [SQL Queries](#sql-queries)
- [Airflow DAG Configuration](#airflow-dag-configuration)
- [Manual Setup for Kinesis Data Streams and API Integration](#manual-setup-for-kinesis-data-streams-and-api-integration)
- [Processing Streaming Data in Databricks](#processing-streaming-data-in-databricks)

## Technologies Used

- Apache Kafka
- Apache Spark
- Apache Airflow
- Apache Kinesis
- Databricks
- SQL
- Python
- AWS

## Prerequisites

- Set up environment on AWS and GitHub
- Create a .pem file extension to save the key-pair file locally for connecting to the EC2 instance
- Connect to EC2 instance using an SSH Client
- Install Java on Amazon CLI
- Make note of ARN, Bootstrap server string, and Zookeeper string

## Amazon Managed Streaming for Apache Kafka (MSK)

To set up an MSK cluster:
1. Create a `client.properties` file with the appropriate credentials inside the `Kafka_folder/bin` directory.
2. Create topics using the Apache create topics command:
   - `<your_UserId>.pin` for Pinterest posts data
   - `<your_UserId>.geo` for post geolocation data
   - `<your_UserId>.user` for post user data

## Connecting MSK Cluster to an S3 Bucket and Creating a Custom Plugin

- Set up an S3 bucket
- Download the confluent.io package onto the EC2 client machine
- Configure the API endpoint URL format
- Run necessary commands to start the Kafka REST proxy
- Test the API using a Python script

## Mounting S3 Bucket to Databricks

1. Import required libraries
2. Define the path to the Delta table
3. Read the Delta table to a Spark DataFrame
4. Get AWS access key and secret key
5. Mount the specified S3 bucket
6. Disable format checks during Delta table reading
7. Read data from the mounted S3 bucket

## Data Transformation and Data Analysis

Perform data analysis to extract insights from user, geo, and pin data

## SQL Queries

Include SQL queries for data analysis

## Airflow DAG Configuration

Configure Airflow DAG '1279c94681db_dag' for task scheduling and management

## Manual Setup for Kinesis Data Streams and API Integration

### Creating Kinesis Data Streams

1. Create Kinesis Data Streams
2. Set up the number of shards for each stream
3. Create data streams for Pinterest tables

### Configuring API for Kinesis Integration

1. Configure API for Kinesis Integration
2. Use the provided access role ARN for API methods integration
3. Grant necessary permissions for API-Kinesis interaction

### Developing `user_posting_emulation_streaming.py` Script

1. Create a new script based on `user_posting_emulation.py`
2. Modify the script to send requests to the API for Kinesis stream data ingestion

## Processing Streaming Data in Databricks

### Step 1: Reading Credentials and Setting Up

1. Create a new Notebook in Databricks
2. Read credentials from the Delta table
3. Retrieve Access Key and Secret Access Key

### Step 2: Ingesting Data into Kinesis Data Streams

1. Run data ingestion method into Kinesis Data Streams
2. Check Kinesis console for data reception

### Step 3: Processing and Saving Data

1. Read and clean streaming data
2. Save cleaned data into Delta Tables
