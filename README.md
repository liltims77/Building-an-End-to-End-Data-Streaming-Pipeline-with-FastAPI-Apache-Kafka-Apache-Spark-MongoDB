# Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB
This is an end to end streaming pipeline with  FastAPI, Apache Kafka, Apache Spark, MongoDB document store and visualizing data with Streamlit dashboard all together packaged in a docker enviroment with individual docker containers running. Collections were created in Postman to test the json documents with ports attached to the documents.

# Introduction
A data set gotten from [kaggle] (https://www.kaggle.com/datasets/carrie1/ecommerce-data) was used. The data set in CSV format was first transformed into key/value pairs and then json format because Apache kafka can only read data in json format by encoding the data at the producer level and decoding that data at the consumer level. A python script was used to transform data into json format so that kafka producer can read the data effectively, and data was ingested into the API for testing with postman. All the applications FastApi, Kafka, Spark and MongoDB were hosted as a docker containers. The API takes data and writes it into a Kafka topic where messages are buffered and processed with Spark. A jupyter notebook was created for Spark to listen to Kafka and takes Data out of Kafka, process it and store it into MongoDB. Streamlit was us used to access data from MongoDB and also visualize the data.

# Api Ingest
Two APIs were created. A root API (hello world) was first created to test if the API actually work with a GET command.
![test-api-1](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/de63dd51-e066-48c3-beae-531b4d8f874d)

# Testing
Postman was used for testing the API. Data was written into postman and request was sent. response 201 gotton means API is working.
![test-api-with-postman-2](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/97bcd7bb-de5a-4f00-be3c-db4fd3809d61)

# Starting up kafka
A docker-compose file for kafka was created and run in the docker network. A topic called "Injestion-Topic" was created to test kafka producer and consumer 
![creating-kafka-topic](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/c2ddc898-e593-40cb-b035-45e52114b383)


A python script witch also contains the Kafka producer was created to test the kafka connection.
![testing-kafka-producer-on-jupyter-4](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/63046d7b-bbb1-4764-a024-a1d8730955f1)

kafka consumer consume messages on the producer python script.
![testing-kafka-consumer-on-jupyter-5](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/007741ae-2331-4a26-99ef-0e58e36f6694)

Message created in the postman collection was sent with a POST request to the producer via tha API, and consumer reads the message sent.
![testing-with-postman-3](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/2f2840a8-9c41-4452-87d2-dfd9dd8f0b6e)

kafka consumer reads the message sent.
![kafka-receive-message-1](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/6a5c3810-ad75-4ce0-9adf-fd8e43425b2f)
