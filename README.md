# Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB
This is an end to end streaming pipeline with  FastAPI, Apache Kafka, Apache Spark, MongoDB document store and visualizing data with Streamlit dashboard all together packaged in a docker enviroment with individual docker containers running. Collections were created in Postman to test the json documents with ports attached to the documents.

# Introduction
A data set gotten from [kaggle] (https://www.kaggle.com/datasets/carrie1/ecommerce-data) was used. The data set in CSV format was first transformed into key/value pairs and then json format because Apache kafka can only read data in json format by encoding the data at the producer level and decoding that data at the consumer level. A python script was used to transform data into json format so that kafka producer can read the data effectively, and data was ingested into the API for testing with postman. All the applications FastApi, Kafka, Spark and MongoDB were hosted as a docker containers. The API takes data and writes it into a Kafka topic where messages are buffered and processed with Spark. A jupyter notebook was created for Spark to listen to Kafka and takes Data out of Kafka, process it and store it into MongoDB. Streamlit was us used to access data from MongoDB and also visualize the data.

# Api Ingest
Two APIs were created. A root API (hello world) was first created to test if the API actually work with a GET command.


