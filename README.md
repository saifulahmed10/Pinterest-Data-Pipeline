# Pinterest-Data-Pipeline

# Project Overview

This pipeline will extract, transform and load data from an API using batch processing and stream processing, using the following Apache services:
- Apache Spark
- Apache Kafka
- Apache Airflow
- Apache Kinesis

These services will be used in conjunction with AWS, which will contain an EC2 instance as an Apache client machine.

# Table of Contents
- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Amazon Managed Streaming for Apache Kafka (MSK)](#amazon-managed-streaming-for-apache-kafka-(MSK))

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

To set up an MSK cluster, a ***`client.properties`*** file will need to be made with the appropriate credentials inside your ***`Kafka_folder/bin`*** directory.
Then create topics using the Apache create topics command.

Three topics made:
- <your_UserId>.pin for the Pinterest posts data
- <your_UserId>.geo for the post geolocation data
- <your_UserId>.user for the post user data

# Connecting MSK cluster to an S3 bucket and creating a custom plugin

Once the S3 bucket is made, the confluent.io package is downloaded onto the EC2 client machine.
When creating the API make sure to add {proxy+} resource and clicking ANY. The endpoint URL should have the following format: http://KafkaClientEC2InstancePublicDNS:8082/{proxy}.

Run the following commands: sudo wget https://packages.confluent.io/archive/7.2/confluent-7.2.0.tar.gz
tar -xvzf confluent-7.2.0.tar.gz and there should be a ***`confluent-7.2.0`*** directory on the EC2 instance.

In the confluent-7.2.0/etc/kafka-rest directory, run nano kafka-rest.properties and add the following credentials.

# Sets up TLS for encryption and SASL for authN.
client.security.protocol = SASL_SSL

# Identifies the SASL mechanism to use.
client.sasl.mechanism = AWS_MSK_IAM

# Binds SASL client implementation.
client.sasl.jaas.config = software.amazon.msk.auth.iam.IAMLoginModule required awsRoleArn="Your Access Role";

# Encapsulates constructing a SigV4 signature based on extracted credentials.
# The SASL client bound by "sasl.jaas.config" invokes this class.
client.sasl.client.callback.handler.class = software.amazon.msk.auth.iam.IAMClientCallbackHandler

To allow communication between the REST proxy and the cluster brokers, all configurations should be prefixed with client.

The invoke URL should be in this format: https://YourAPIInvokeURL/test/topics/<AllYourTopics>. Make a note of this as it will be used later on.

Run the following command in the confluent-7.2.0/bin folder: ./kafka-rest-start /home/ec2-user/confluent-7.2.0/etc/kafka-rest/kafka-rest.properties. If it works you will see INFO Server started, listening for requests... in your EC2 console.

Run python script that allows Python requests library to test the API and obtain a response. To make sure you can send messages to an AWS API gateway API using the invoke URL. 

This data will be getting stored in the S3 bucket if the data is sent to the cluster correctly.
