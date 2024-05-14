# E-Commerce Analytics With Apache Flink
This repository hosts an Apache Flink application tailored for real-time data analysis in an e-commerce environment. Docker Compose is employed to orchestrate the necessary infrastructure components, which include Apache Flink, Elasticsearch, and Postgres. The application ingests financial transaction data from Kafka, performs aggregations, and persists the results in both Postgres and Elasticsearch for further analysis.

## Architecture
![System Architecture](https://github.com/FA3001/Streaming_with_Apache_Flink/raw/main/Visualizaton/System%20Architecture.png)

## Technologies:
- ### Apache Kafka:
  is a distributed streaming platform that allows for the publishing and subscribing of records in real-time. It's designed to handle data streams from multiple sources and deliver them to multiple consumers.
  Kafka's distributed architecture ensures high throughput and fault-tolerance, making it ideal for handling big data problems.
- ### Apache Flink:
  is a stream processing framework that provides powerful capabilities for timely computations over data streams. It's designed to run stateful computations over bounded and unbounded data streams.
  Flink's ability to process event time data and its support for exactly-once semantics makes it a robust solution for real-time data analysis.
  - Sets up the Flink execution environment.
  - Connects to Kafka as a source for financial transaction data.
  - Processes, transforms, and performs aggregations on transaction data streams.
- ### Elasticsearch:
  is a search and analytics engine that allows for the storage, search, and analysis of big volumes of data quickly and in near real-time.
  Its distributed nature allows it to scale horizontally and handle large amounts of data efficiently.
  - Stores transaction data for further analysis.
- ### Kibana:
  is a data visualization tool that provides a window into the Elasticsearch engine.
  It allows users to visualize their data in various formats, making it easier to understand complex data sets.
  - Used For creating Dashboard.
- ### Postgres:
  - Stores transaction data and aggregated results in tables ```bash (transactions, sales_per_category, sales_per_day, sales_per_month)```.
- ### Maven:
  is a build automation tool primarily used for Java projects. It helps manage project dependencies, build processes, and project documentation.
  Maven uses a project object model (POM) file to describe the project's structure, dependencies, and build configurations.

## Code Structure
  ```bash DataStreamJob.java```: Contains the Flink application logic, including Kafka source setup, stream processing, transformations, and sinks for Postgres and Elasticsearch.
  ```bash Deserializer, Dto, and utils ``` packages: Include necessary classes and utilities for deserialization, data transfer objects, and JSON conversion.
## Configuration
  Kafka settings (bootstrap servers, topic, group ID) are configured within the Kafka source setup.
  Postgres connection details (URL, username, password) are defined in the jdbcUrl, username, and password variables.
## Sink Operations
  The application includes sink operations for Postgres using JDBC to create tables ```bash(transactions, sales_per_category, sales_per_day, sales_per_month)``` and perform insert/update operations.
  Additionally, it includes an Elasticsearch sink to index transaction data for further analysis.
## Installation and Setup
1. Clone this repository.
2. Run docker-compose up to start the required services (Apache Flink, Elasticsearch, Postgres).
3. The Sales Transaction Generator main.py helps to generate the sales transactions into Kafka.
4. Download Flink 1.18.0 [Flink 1.18.0](https://archive.apache.org/dist/flink/flink-1.18.0/flink-1.18.0-bin-scala_2.12.tgz) unzip and get flink-1.18.0 directory.
5. Run ```bash start-cluster.sh``` to start it will be on port 8081.
6. Download Maven and run ```bash mvn clean, mvn compile, mvn package``` to generate the JARFILE.
7. Run ```bash flink 1.18.0/bin/flink run -c FlinkEcommerce.DataStreamJob <JARFILE_path>```.
8. Open Flink from http://127.0.0.1:8081/ to see the runing job.

 ![flink](https://github.com/FA3001/Streaming_with_Apache_Flink/blob/main/Visualizaton/Flink.PNG)

9. Open Elasticsearch from http://127.0.0.1:5601/ and from the left menu choose dev.
10. Run ```bash GET transaction ``` this will print the data in json format like

![data](https://github.com/FA3001/Streaming_with_Apache_Flink/blob/main/Visualizaton/ssss.PNG)

11. To create the dashboard choose from left menu ```bash Dashboard``` and choose the data then create the visualizations.

## Dasboard:
![](https://github.com/FA3001/Streaming_with_Apache_Flink/blob/main/Visualizaton/Dashboard.PNG)

