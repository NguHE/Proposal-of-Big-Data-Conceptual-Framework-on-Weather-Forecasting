# Proposal-of-Big-Data-Conceptual-Framework-on-Weather-Forecasting
Conceptualize the big data solution for weather forecasting
Big Data Analytics and Technologies course

## Applications of Weather Forecasting 
1. Agriculture
2. Transportation
3. Construction
4. Sport
5. Disaster Management
6. Energy Management
7. Biodiversity Conservation

## Big Data Eco-system Architecture
![image](https://github.com/NguHE/Proposal-of-Big-Data-Conceptual-Framework-on-Weather-Forecasting/assets/125574265/ec8b5309-d1b5-4b18-b56b-fba0898e0218)

## Adoption of Big Data Tools, with sound justification
### 1. Data Sources
- Data source layer is the streaming or generating of data from weather stations, IoT devices such as sensors or input system
- National Climate Centre, Malaysia under MetMalaysia serves as the centre to supply meteorological data captured by weather stations
- Structured data includes temperature, precipitation, solar radiation, visibility, air pressure, wind speed and direction
- Semi-structured data includes satellite imagery to capcture cloud cover
- Unstructured data includes narrative descriptions of textual reports provided by weather observers, textual forecasts and historical climate data 

#### Climate data
- 247 automatic weather stations (AWS) and 183 manual meteorological observation stations as well as 3 global atmospheric watch stations located in Petaling Jaya, Danum Valley, Sabah and Tanah Rata, Pahang in Malaysia
- 3 types of observation reports: hourly report, daily report, monthly report
- Rainfall, temperature, wind speed data, mean sea-level pressure, relative humidity, visibility, solar radiation, evaporation data, upper air data and cloud observations 

#### Radar data
- Data and images for weather radar with a frequency of every 10 minutes
- This covers 9 locations of Meteorological Radar Station throughout the country
- Helps in early warning disaster management

#### Atmospheric science data
- Measurements of air quality and atmospheric composition
- Information on suspended particles, chemical content of rainwater, chemical content of dry deposition, ozone profiles, ultraviolet radiation and more
  
#### Marine data
- Marine parameter data (wind direction, wind speed, weather, wave height, wave period, swell direction, swell period, swell height, and sea surface temperature)
- Summaries of wind roses or wave data 

#### Satellite data
- Data and images for meteorological satellites with a frequency of every 10 minutes
- Obtained from Himawari geostationary satellite provided by Japan

### 2. Ingestion Layer
**Purpose:** Ensures the efficient and reliable collection of real-time and historical weather data, requiring scalable tools to handle the substantial volume of information.
- AWS observing system comprised of sensing instruments, interfaces, processing devices and transmission units
- AWS units with sensing instruments are connected to computer network for collection of data from environment and transmission of data to central processing system
- The processing system is then connected to information system (WIS) and automatic message switching system (AMSS) for further processing process
- This data is then fed into the system, serving as the entry point for the forecasting pipeline
  
![image](https://github.com/NguHE/Proposal-of-Big-Data-Conceptual-Framework-on-Weather-Forecasting/assets/125574265/be9ce7b0-163a-4501-a6f2-010b08480964)

**Apache NiFi** is an open-source data integration platform that offers a visual interface for designing and managing data flows (Hamadou et al., 2020; Alwidian et al., 2020). 
- According to Boyanov (2021), Apache NiFi is efficient in ETL of IoT data which highlights its ability to retrieve meteorological data from IoT devices.
- Thota et al. (2020) supported its ability of low latency and high throughput. With its support for real-time streaming and batch processing, it is well-suited for weather forecasting scenarios with both real-time and historical data.
- It provides end-to-end encryption to secure the transfer of sensitive data (Alwidian et al., 2020).
- Additionally, it offers user-friendly interface and data lineage capabilities. It was applied as ingestion layer for weather forecasting in many studies such as Mangortey et al. (2019) and Thota et al. (2020) for air traffic management, Bottazzi et al. (2021) for Italian meteorological portal, Fote et al. (2020) and Tóth et al. (2022) for agriculture.
- Hamadou et al. (2020) claimed that Apache NiFi is deemed the most suitable option for the ingestion layer. 

The other proposed tool for ingestion layer is **Apache Kafka**. It is a distributed messaging system that organises messages into topics (Tun et al., 2019). Apache Kafka consists of brokers, producers, and consumers (Moharm, 2019; Tun et al., 2019). Producers distribute streaming messages to brokers, which store and publish them. Consumers retrieve these messages for processing. In case one broker fails, Kafka's system is designed to continue working without any interruption because there are other brokers that can take over (Alwidian et al., 2020). 
- This feature with fault-tolerance allows Apache Kafka to deliver reliable messages (Wu et al., 2020; Koutroumanis et al., 2021).
- Kafka's core APIs, such as Kafka Connect, enable easy integration with heterogeneous systems and facilitate the flow of data. Kafka's streaming capabilities, combined with its support for streaming SQL through KSQL, enable real-time processing and querying of data without traditional ETL processes (Kanavos et al., 2021).
- Its scalability, high throughput, fault tolerance, and real-time streaming capabilities make it well-equipped to handle huge data generated by weather stations, satellites, and IoT devices (Jafarpour et al., 2019; Sahal et al., 2020).
- It was applied as ingestion layer for weather forecasting in many studies such as Koutroumanis et al. (2021) while Kanavos et al. (2021) for winter precipitation forecasting, Akanbi (2020) for environmental monitoring, Jamil et al. (2021) for IoT based weather stations, Roukh et al. (2020) for cloud platform for smart farming and Tadrist et al. (2022) for flood forecasting.



| Characteristics        | Apache NiFi                                                    | Apache Kafka                                                  |
|-------------------------|----------------------------------------------------------------|----------------------------------------------------------------|
| Data Ingestion Approach | Pull-based approach                                            | Pull-subscribe model                                          |
| Data Format Support     | Wide range of data: structured, semi-structured, and unstructured | Accepts messages in various formats, often as byte arrays or strings |
| Types of Data           | Batch and Stream                                               | Stream                                                         |
| Type of Loading         | Event and not-event                                            | Event-driven                                                  |
| Ease of Use             | User-friendly interface with a web user interface             | Shell command line                                             |
| Processing Complexity   | Supports complex data routing, transformation, and enrichment | Primarily focuses on message distribution and delivery         |
| Scalability             | Horizontal scalability                                         | Horizontal scalability                                         |
| Fault Tolerance         | Yes                                                            | Yes                                                            |
| Data Security           | Yes                                                            | Requires implementation                                       |
| Fault Tolerance         | Offers data provenance and lineage features for visibility and traceability | Provides fault tolerance and data durability through replication mechanisms |

After comparison, **Apache Nifi** is more suitable for weather forecasting. It stands out with its flexible data flow management as weather data sources are diverse from weather stations, satellites, radars or IoT devices. It also provides data governance features with built-in encryption. Additionally, it supports both batch and stream data for historical data and real-time collection. The use of historical batch data enables the construction of statistical models and enhances the understanding of long-term weather patterns. On the other hand, stream data offers real-time and current information that is valuable for short-term forecasting and continuous monitoring. When these two types of data are merged, meteorologists can enhance the precision and dependability of their weather predictions. This allows them to issue timely warnings, make well-informed decisions and take measures to mitigate potential risks.

### 3. Storage Layer
**Purpose:** Managing and storing vast amounts of wetaher data generated from various sources

**HDFS** is a Java-based file system designed for scalable and reliable data storage (Gaur, 2022). HDFS distributes files across multiple machines which ensure redundancy to protect against data loss in case of failure (Fakherldin et al., 2019). 
- A master/slave architecture is employed, with a single NameNode managing file system operations and multiple DataNodes responsible for data storage on individual compute nodes (Vaishnavi et al., 2020). When data is ingested into HDFS, it is divided into smaller pieces and distributed to different nodes in the cluster for parallel processing.
- Additionally, multiple copies of each data piece are created and distributed to different nodes, including copies on different server racks to enhance data durability.
- More et al. (2020) claimed that HDFS shows benefits in saving effort and resources required for data replication and allows the customer nodes to access data without the burden of storing it locally. This advantage is also supported by Koutroumanis et al. (2021) with data compression techniques, enabling efficient storage of weather data.
- Streaming access to file system data, file permissions, and authentication are among the other features provided by HDFS. However, there are certain scenarios in which HDFS may not perform optimally in the case for low-latency data access, many small files, multiple concurrent writers, or frequent random changes to files (Koutroumanis et al., 2021).
- It was applied as storage layer for weather forecasting in many studies such as Koutroumanis et al. (2021), Gardashova and Jabrayilova (2023), Vaishnavi et al. (2020) while Fakherldin et al. (2019) for National Climatic Data Centre, Pandey and Chauhan (2019) for IoT based smart polyhouse system and Krishnamoorthy and Udhayakumar (2021) for wind energy management.

**Apache Cassandra** is an open-source distributed database management system known for its column-based data model (Jamil et al., 2021). It is widely scalable NoSQL database which offers linear scalability with multiple nodes in a cluster and fault tolerance, allowing for the storage and management of large volumes of structured and unstructured data. 
- It has a query language – Cassandra Query Language (CQL) (Jamil et al., 2021). Its in-memory capabilities and key partitioning methods contribute to efficient data handling. With its distributed architecture and reliable replication mechanisms, Cassandra ensures the durability and availability of data in weather forecasting systems. 
- Additionally, Cassandra supports cloud storage, providing flexibility and scalability as per the system's needs (Kanavos et al., 2021). 
- Cassandra's distributed system architecture ensures that data is distributed among all cluster nodes, with automatic replication for fault tolerance and sharing strategies (Jamil et al., 2021). 
- In the event of node failure, data remains accessible from other nodes in the cluster. Additionally, Cassandra allows for linear scaling by easily adding more nodes to the network to increase overall system capacity. 
- It was applied as storage layer for weather forecasting in many studies such as Jamil et al. (2021) for IoT based weather stations, Roukh et al. (2020) for cloud platform for smart farming, Kanavos et al. (2021) for winter precipitation forecasting, Perçuku et al. (2020) for solar panel system. 



| Characteristic      | HDFS                                                        | Apache Cassandra                                            |
|----------------------|-------------------------------------------------------------|--------------------------------------------------------------|
| Data Model           | N/A (File system)                                           | Column-based                                                 |
| Query Language        | N/A                                                         | CQL                                                          |
| Scalability          | Horizontal scaling                                           | Linear scaling                                               |
| Data Consistency     | Strong consistency within a single file            | Tuneable consistency level  |
| Data Replication     | Fault-tolerant with replication                              | Automatic data replication                                   |
| Latency              | High latency                                                | Low latency                                                  |
| Data Types           | Suited for large files                                       | Suited for structured and unstructured data                    |
| Cloud Readiness      | Yes                                                         | Yes                                                          |
| Integration          | Part of Hadoop ecosystem, integrates well with other Hadoop components such as MapReduce or Apache Spark | Standalone NoSQL database, can integrate with various tools and frameworks such as Apache Spark and Apache Flink |
| Security             | File permission and authentication mechanism               | Authentication, role-based access control, encryption         |
| Data Accessibility   | Batch processing                                            | For both batch and stream processing                           |


After comparison, **Apache Cassandra** is more suitable for weather forecasting with its low latency and supports stream processing. This allows fast process of data to be executed or transmitted in a system. It is highly scalable and can handle massive amounts of data by distributing it across a cluster of nodes. It allows for linear scalability by adding more nodes to the cluster, providing seamless expansion as data volume grows. It is flexible for easy adaptation to changing data requirements and tuneable consistency levels. 

### 4. Processing Layer
**Purpose:** Responsible for computations, transformation tasks on ingested data, including data cleaning, feature engineering, data aggregation, filtering and others to prepare data for analysis and decision making

**Apache Spark** is an open-source, high-speed, distributed computing framework designed to handle large amounts of data (Gaur, 2022). It offers developers efficient execution of streaming, machine learning, and SQL workloads with fast iterative access to datasets (Gaur, 2022). It is much faster than traditional methods like Hadoop because it uses an in-memory processing engine which can recover from node failures without data loss (Moharm, 2019; Tun et al., 2019; Hamadou et al., 2020). 
- Apache Spark utilises Resilient Distributed Datasets (RDD) to process data in memory and handle failures (Tun et al., 2019). When using Spark Streaming, the incoming continuous stream of data is referred to as a Discretized Stream (DStream).
- DStream enables parallel recovery of lost data, improving the efficiency of streaming data analysis. Within a DStream, input data is divided into batches based on time intervals, a process known as windowing.
- It was applied as processing layer for weather forecasting in many studies such as Swe et al. (2019), Fakherldin et al. (2019), Lavanya et al. (2020) and Radhika et al. (2022) while Krishnamoorthy and Udhayakumar (2021) for wind energy management, Kanavos et al. (2021) for winter precipitation forecasting, Erdem et al. (2021) and Vonitsanos et al. (2021) for flight scheduling and Jamil et al. (2021) for IoT based weather stations. 

**Apache Flink** is another open-source data processing framework that supports real-time and batch data processing (Gaur, 2022). It is advanced event-time processing and performs computations at high speeds. 
- It can handle high-velocity data streams, provides fault tolerance and scalability (Gaur, 2022). It has low latency and automatic memory management.
- It supports Table API with interactive mode of Interactive Scala shell. At the topmost layer, Apache Flink provides API's and libraries, including the Dataset API for batch processing and the Datastream API for stream processing.
- It also offers libraries such as Flink ML for machine learning, Gelly for graph processing, and Tables for SQL operations.
- It was applied as processing layer for weather forecasting in several studies such as Akanbi (2020) for environmental monitoring, Lv et al. (2023) for wind speed forecasting, 

| Characteristic      | Apache Spark                                               | Apache Flink                                                  |
|----------------------|------------------------------------------------------------|---------------------------------------------------------------|
| Processing Model     | Hybrid stream and batch                                    | Hybrid stream and batch                                       |
| Interactive mode     | Interactive Spark shell                                    | Interactive Scala shell                                       |
| Scalability          | Horizontal scalability                                      | Horizontal scalability                                        |
| Fault Tolerance      | RDD lineage, data recovery                                  | Checkpoints, automatic recovery                                |
| Performance          | In-memory processing                                        | Low latency, high throughput                                  |
| Memory Management    | Configurable                                                | Automatic                                                     |
| Table Partitioning   | Supported                                                  | Supported                                                     |
| Querying Latency     | Low latency                                                | Low latency                                                   |
| SQL supported        | Spark SQL                                                  | Table API                                                     |
| Ecosystem            | Rich ecosystem with a wide range of libraries              | Growing ecosystem with various integrations                    |
| Community Support    | Large and active community                                   | Growing community                                             |

Both tool support for real-time and batch data processing, making them capable of handling the continuous influx of weather data. They are also scalable, low latency with fault tolerance. After comparison, **Apache Spark** may be preferable with mature ecosystem in weather forecasting, extensive library support, and integration with different data sources. 

### 5. Analytical Layer
**Purpose:** Employes advanced algorithms, machine learning models and statistical techniques to gain valuable insights from the weather data
- The weather forecasts issued by MetMalaysia are generated using the MetMalaysia Weather Research and Forecasting Model (MMD-WRF) analysis model, along with data from the European Centre for Medium-Range Weather Forecasts and the Global Forecast System (Bernama, 2021; Amerudin, 2023).
- Regional models including Regional Spectral Model and the Global Environmental Multiscale are used to make specific predictions based on regions in Malaysia (Amerudin, 2023). The highlight of the regional models that surpass global models is the resolution which allows high accuracy of prediction for areas.
- MetMalaysia also collaborates with the World Meteorological Organization and the United Nations Framework Convention on Climate Change to improve prediction accuracy. Machine learning algorithms such as linear regression, random forest, decision tree, gradient boosting tree, artificial neural networks architectures have been applied to forecast weather by researchers (Hanoon et al., 2021; Ridwan et al., 2021). 


**MLlib** is a component of Apache Spark ecosystem used for machine learning algorithms and tools. It offers a set of core algorithms, including classification, regression, clustering as well as deep learning. 
- MLlib is usually integrates with Apache Spark in the ecosystem. Vonitsanos et al. (2021) applied Apache Spark and MLlib computing systems for developing and implementing prediction models using air flight data. Real-time analytics are provided with robustness and scalability.
- It was also applied as analytical layer with Apache Spark for weather forecasting in the study done by Swe et al. (2019), Xu et al., (2020) for wind speed big data forecasting, Kanavos et al. (2021) for winter precipitation forecasting and Lavanya et al. (2020) for real-time weather analytics.
- However, it requires knowledge of distributed computing concepts and may be more suitable for users with programming experience.

  
**MATLAB** is a proprietary software developed by MathWorks which requires license. It has comprehensive built-in functions and toolboxes for data analysis such as statistical modelling, machine learning, visualisation, and prediction analytics. 
- MATLAB provides a user-friendly interface and is well-suited for prototyping and exploratory analysis. It offers advanced statistical and machine learning capabilities, making it a suitable choice for developing complex forecasting models.
- However, MATLAB offers limited scalability compared to distributed computing frameworks like Apache Spark. It does provide scalability options such as MATLAB distributed computing server, MATLAB production server and parallel computing toolbox.
- It was applied as analytical layer for weather forecasting in the study done by Pandit et al. (2020) for wind energy management, Weng et al. (2021) with neural network and Jeon and Kim (2020) for forecasting the hourly solar irradiance for the following day with deep learning model. 

| Characteristic        | Apache Spark MlLib                                  | MATLAB, Octave                               |
|------------------------|----------------------------------------------------|-----------------------------------------------|
| Programming Language   | Scala, Java, Python, R                              | MATLAB, Octave                               |
| Distributed Processing | Yes                                                | No                                            |
| Streaming Support      | Yes                                                | Yes                                           |
| Scalability            | Good                                               | Limited                                       |
| Algorithm Library      | Rich                                               | Rich                                          |
| Ease of Use            | User-friendly APIs                                 | User-friendly interface                       |
| Visualization Tools     | Integration with other libraries                   | Comprehensive visualization tools             |
| Community Support      | Active and large                                    | Limited, but strong in academia               |

Both tools have their advantages and able to support WRF model. **Apache Spark MLlib** outstands with its distributed computing infrastructure and real-time analytics while MATLAB outstands with its advanced analytical capabilities and user-friendly interface. In this case, Apache Spark MLlib is selected with its in-memory processing engine and distributed computations. It is built on top of the Apache Spark framework which allows for scalable and parallel processing of large datasets and enabling efficient complex forecasting models. MLlib's real-time analytics capabilities, robustness, and scalability make it an ideal choice for the meteorological department's analytical requirements.

### 6. Visualization Layer
**Purpose:** Generate visual representations for interpretation and effective communication of weather information

**Tableau** is known for its intuitive interface and extensive collection of interactive charts and visualisations (Hirve and Pradeep Reddy, 2019). 
- It provides a user-friendly experience with drag-and-drop functionality, making it easy to explore and analyse data (Gaur, 2022). Tableau supports various data sources and integrations, allowing seamless connectivity with different systems.
- It offers advanced customization options for visual design and formatting, and benefits from a large and active community that provides support and resources.
- Tableau seamlessly connects to both local and cloud-based data sources, allowing for direct access or data import for high-performance in-memory processing.
- It helps users make sense of complex data by presenting it in easy-to-understand visuals and interactive web dashboards, turning big data analytics into actionable insights. However, this tool requires license for implementation.
- It was applied as analytical layer for weather forecasting in the study done by Bhargavaram et al. (2022) for rainfall prediction.


**Apache Zeppelin** is an open-source web-based notebooks which create a collaborative environment for data exploration and analysis (Hirve and Pradeep Reddy, 2019). 
- It enables the creation of notebooks that combine code, visualisations, and text, supporting multiple programming languages like Python, R, and Scala. Zeppelin's flexibility allows for customization and extension through plugins and interpreters, making it suitable for advanced analytics and data science tasks.
- It also has a growing community that contributes to its development and support. It was applied in Gallinucci et al. (2019) study as visualisation tool for weather forecasting in precision agriculture.

| Characteristic      | Tableau                                             | Apache Zeppelin                                   |
|----------------------|-----------------------------------------------------|---------------------------------------------------|
| Ease of Use          | User-friendly interface                            | User-friendly interface                           |
| Visualisation        | Wide range of interactive charts and visualisations | Extensive chart options and visualisations        |
| Interactivity        | Interactive dashboards and drill-down capabilities  | Interactive notebooks with data exploration capabilities |
| Collaboration        | Collaboration features for sharing and teamwork    | Collaborative environment for multiple users      |
| Data Sources         | Support for various data sources and integrations  | Support for various data sources and integrations |
| Scalability          | Scalable for handling large                         | Scalable for handling large                        |
| Real-time Updates    | Yes                                                 | Yes                                               |
| Dashboard Creation   | Robust with drag-and-drop interface and layout options | Support interactive dashboards using notebooks and customizable widgets |
| Community and Support | Large user community with extensive resources, forums, and customer support | Growing with online resources and community support |


Both tools support real-time updates and streaming capabilities for visualisations. Tableau is recommended as preferred visualisation tools with its outstanding visualisation capabilities, user-friendly interface and active community supports. While Apache Zeppelin also provides visualization capabilities, it is primarily a notebook-based platform for data science and analytics. It requires some coding knowledge, which may be less suitable for meteorologists and weather forecasters who prefer a more visual and intuitive approach to data visualization.

### 7. Analysis Outcome

![image](https://github.com/NguHE/Proposal-of-Big-Data-Conceptual-Framework-on-Weather-Forecasting/assets/125574265/45048545-aea2-41a4-b0b2-baf230ace4b8)

## Security and Privacy Issues
1. Cyber-attacks
2. Unauthorized access
- **Proposed Solution:** Authentication (Kerberos protocol), access controls, encryption, secure key management, data sharing agreement, auditing mechanism, risk assessments


## Extra Information
### IoT-based system
![image](https://github.com/NguHE/Proposal-of-Big-Data-Conceptual-Framework-on-Weather-Forecasting/assets/125574265/be8f8575-2439-4a15-9303-14250fb6cc89)

### Location of Principal Meteorological Stations in Malaysia
![image](https://github.com/NguHE/Proposal-of-Big-Data-Conceptual-Framework-on-Weather-Forecasting/assets/125574265/488f2e3b-8908-42b5-8d3d-256663b7c1c8)

