# Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB
This is an end to end streaming pipeline with  FastAPI, Apache Kafka, Apache Spark, MongoDB document store and visualizing data with Streamlit dashboard all together packaged in a docker enviroment with individual docker containers running. Collections were created in Postman to test the json documents with ports attached to the documents.

# Introduction
A data set gotten from [kaggle] (https://www.kaggle.com/datasets/carrie1/ecommerce-data) was used. The data set in CSV format was first transformed into key/value pairs and then json format because Apache kafka can only read data in json format by encoding the data at the producer level and decoding that data at the consumer level. A python script was used to transform data into json format so that kafka producer can read the data effectively, and data was ingested into the API for testing with postman. All the applications FastApi, Kafka, Spark and MongoDB were hosted as a docker containers. The API takes data and writes it into a Kafka topic where messages are buffered and processed with Spark. A jupyter notebook was created for Spark to listen to Kafka and takes Data out of Kafka, process it and store it into MongoDB. Streamlit was us used to access data from MongoDB and also visualize the data
## GOAL: the main goal is to send messages and test via API which Kafka consumer can read, send to spark output topic subscribed to kafka topic with mongodb showing data as documents and streamlit to visualize each customers_id and invoices (what each customers purchase for a specific time duration). I started with 3 customers details, before loading all the remaining customers using python.

# Api Ingest
Two APIs were created. A root API (hello world) was first created to test if the API actually work with a GET command.
![test-api-1](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/de63dd51-e066-48c3-beae-531b4d8f874d)

# Testing
Postman was used for testing the API. Data was written into postman and request was sent. response 201 gotton means API is working.
![test-api-with-postman-2](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/97bcd7bb-de5a-4f00-be3c-db4fd3809d61)

# Starting up kafka
A docker-compose file for kafka was created and run in the docker network. A topic called "Injestion-Topic" was created to test kafka producer and consumer 
![creating-kafka-topic](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/c2ddc898-e593-40cb-b035-45e52114b383)

### A python script witch also contains the Kafka producer and topics was created to test the kafka connection.
![testing-kafka-producer-on-jupyter-4](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/63046d7b-bbb1-4764-a024-a1d8730955f1)

### kafka consumer consume messages subscribed to that particulat topic on the producer python script.
![testing-kafka-consumer-on-jupyter-5](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/007741ae-2331-4a26-99ef-0e58e36f6694)

### Message created in the postman collection was sent with a POST request to the producer via tha API, and consumer reads the message sent.
![testing-with-postman-3](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/2f2840a8-9c41-4452-87d2-dfd9dd8f0b6e)

## kafka consumer subscribed to the "Injestion-topic" reads the message sent.
### The docker-compose file for kafka was stopped, dockerfile and requirements.txt file was built, docker-compose file was started again with a dockerfile to ingest the API. Kafka producer and consumer was enabled Postman was used to send message to kafka consumer, consumer reads message sent by Postman.
![kafka-receive-message-1](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/a6c11df9-b6f4-4c3d-8124-d4b8c6d22971)

### All docker containers were shut down, Docker-compose file that contains (Kafka and spark) was run, Another topic "SPARK-OUTPUT" topic was created in kafka to read streams of messages produced by kafka. Postman was used to send message to kafka ingestion topic, spark-output topic reads messages consumed by ingestion topic with Spark SQL, and also write messages back to consume thesame messages.
## Jupyter notebook showing kafka and spark configurations and how spark reads message from kafka streams
![spark-1](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/497319f3-9369-4beb-ac3a-0c46005fe695)
![spark-2](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/bf50f333-151f-4a47-9ee7-16cc7ac4c78c)
## Kafka-spark output showing spark-output topic reading messages sent by kafka
![kafka-spark](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/11d18ae8-e0a6-4a1a-92d3-e7f5a9c83819)
![data-streaming from Kafka to spark output topic](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/d5631ea1-1892-4d1b-906b-5c17fb6df3cc)
![spark-3](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/f438800f-4610-433f-938f-0ac5d0c05ce4)
![spark-subscribe-to-ingestion-topic](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/58962c43-5cf7-47ba-b39e-a46b8b390978)

## Docker-compose file containing Kafka and spark was shutdown, and compose file connecting kafka-spark and mongodb was ran, Kafka producers and consumers were enabled again, Postman was used to send message to kafka ingestion topic, spark-output topic reads messages consumed by ingestion topic, and also consumes thesame messages. Mongodb consumes messages sent to kafka-spark 
### jupyter notbook images showing connection between kafka-spark and mongodb
![spark-mongo-jupyter](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/52c68bde-aefb-47cf-9108-1c4dd9fba75f)
![spark-mongo-jupyter-2](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/f34c760f-71e1-45d8-a10b-260d11a6b092)
### Mongodb consumes messages 
![spark-mongodb-doc](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/f723e89e-0af2-43a9-b221-79e835e98441)
![Mongo-1](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/bf011a4a-8c90-44de-8d1a-e4b1627fc9f1)
![mongo-3](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/2f06975e-8629-4af5-bbbf-48e5c7317412)

## Note: kafka can only read messages in JSON format converted to KEY and VALUSE and then ENCODE message sent to the topic and messages ared DECODED at consumer and converted back into JSON format in KEY and VALUE format.
### Some transformation was done to convert the topics into ROWS and COLUMNS as document because MongoDB is a document store Database.
![mongo-3](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/2f06975e-8629-4af5-bbbf-48e5c7317412)
### Transforming data into Rows and Columns
![all-data-2](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/ff5a53fa-be17-4258-83dc-4afa69332c6c)
![all-data-1](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/2e81b3d4-7287-44d1-bd5b-0bed3277234c)
![all-data-last](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/4a5b9662-5079-4f4b-81eb-41740fa72324)
![mongo-2](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/739e773e-a280-4169-85af-879e597c1461)

## API-CLIENT with python scripts was then used to send all the data (OUTPUT.TXT) because we started with only 3 users data for the project
![api-client-data-vsc](https://github.com/liltims77/Building-an-End-to-End-Data-Streaming-Pipeline-with-FastAPI-Apache-Kafka-Apache-Spark-MongoDB/assets/41475769/a5c59b21-b0b3-49f8-9d99-1602921e1c1a)








