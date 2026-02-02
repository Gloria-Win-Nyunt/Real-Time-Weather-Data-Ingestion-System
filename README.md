# Problem Statement

We are a startup offering smart services to logistics, agriculture, and event management companies

Our clients want real-time weather updates for multiple cities to optimize deliveries, plan outdoor events, and manage crop irrigation systems. 
We must build a real-time weather data ingestion pipeline to fetch weather conditions every 5 minutes from multiple cities globally, process it quickly, and store it for 
* live dashboards
* Alert systems
* Historical analysis

# Key Requirements 

* Real-time or near real time ingestion (every 5 minutes)
* Scalable to thousand of cities
* Highly available and fault_tolerant
* Keep 6 months of historical weather data
* Cost-effective for startup scale (1000+ cities)

# Logical Architecture
source layer -> Ingestion layer -> Processing layer -> Storage layer -> Serving Layer

# Architecture V1
* EventBridge triggers lambda every 5 mins.
* Lambda fetches Weatherstack API for all configured cities.
* Normalize JSON and store two files: Raw and Processed in S3.
* Althena tables automatically sync with S3
* Users query data via Athena or visualize via any visualization tool.

# Architecture V2
* Cron job on ECS Farget (or Airflow DAG) triggers service every 5 mins
* Producer writes weather data as Kafka events or kinesis events
* Kafka Streams or spark structured streams normalize/clean the data in real-time.
* Sink connector dumps it into S3.
* Athena tables automatically sync with S3.
* Users query data via Athena or visualize via any visualization tool.

 # Architecture V3
 * Airflow DAG triggers every 5 minutes
 * Tasks fetch from API, transform, and load into S3
 * Athena tables automatically sync with S3.
 * Users query data via Athena or visualize via any visualization tool.
 * Airflow monitoring retry, and alerting for failures.

# Final Architecture
* EventBridge triggers Lambda every 5 mins
* Lambda fetches Weatherstack API for all configured cities.
* Normalize JSON and store two files: Raw and Processed in S3.
* Athena tables automatically sync with S3.
* Users query data via Athena or visualize via any visualization tool.

# Prerequisties/Tools 
* PyCharm/VS Code
* Git
* UV (Package Manager)
* Docker
* AWS Account (Free Tier)
* AWS CLI


