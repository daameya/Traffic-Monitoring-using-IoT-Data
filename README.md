# Traffic-Monitoring-using-IoT-Data

[![Python: 3.11](https://img.shields.io/badge/Python-3.9-blue?style=for-the-badge)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

This project enables real-time data collection and analysis from an IoT device installed in a vehicle. The device gathers information such as vehicle status, GPS location, weather conditions, medical data, and camera feeds while the vehicle is en route from Central London to Birmingham. The data is transmitted to a central system for real-time processing, enabling analytics, alerts, and insights.

## System Architecture
![System_architecture.png](images%2FSystem_architecture.png)

## Vehicle Path
Driver travels from Central London to Birmingham
![Vehicle_Path.png](images%2FVehicle_Path.png)

## System Components
- **config.py**: This file contains essential environment variables and credentials:
    - `AWS_ACCESS_KEY`: AWS access key for authentication.
    - `AWS_SECRET_KEY`: AWS secret key for secure access.
- **main.py**: This script simulates a vehicle moving from London to Birmingham, sends `GPS coordinates` to track vehicle movement along the route, fetches and streams real-time `traffic camera` and `weather` data from vehicle, simulates `emergency events` (`accidents`, `medical issues`) and sends alerts and publishes all data to `Kafka` topics for real-time processing.
- **spark-jobs.py**: This python script defines schemas for `vehicle`, `GPS`, `traffic`, `weather`, and `emergency` data, reads real-time data from Kafka topics, writes structured data to `AWS S3` for storage and creates `Spark DataFrames` for further processing and visualization.


## Setting up the System
This Docker Compose file allows you to easily spin up Zookkeeper and Kafka application in Docker containers. 

## Prerequisites
- Python 3.9 or above installed on your machine
- Docker Compose installed on your machine
- Docker installed on your machine

## S3 Bucket Policy
![S3_bucket_policy.png](images%2FS3_bucket_policy.png)

## Installation
1. Clone the repository
```bash
git clone https://github.com/daameya/Traffic-Monitoring-using-IoT-Data.git
cd Traffic-Monitoring-using-IoT-Data
```
2. Run using docker compose
```bash
docker-compose up -d
```
This command will start Zookeeper and Kafka containers in detached mode (`-d` flag). Kafka will be accessible at `localhost:9092`

3. Set up the virtual environment
```bash
python -m venv env
root env/bin/activate
```

4. Install dependencies
```bash
pip install -r requirements.txt
```

5. Generate required data and driver travel from London to Birmingham 
```bash
python jobs/main.py
```

6. Paste the following command in cmd to run jobs/spark-jobs.py from root

```bash
docker exec -it traffic-monitoring-using-iot-data-spark-master-1 spark-submit ^
--master spark://spark-master:7077 ^
--packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.0,org.apache.hadoop:hadoop-aws:3.3.1,com.amazonaws:aws-java-sdk:1.11.469 jobs/spark-jobs.py
```

## License

This project is distributed by daameya under the terms of the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact
### Data Scientist

- [Ameya Damle](https://github.com/daameya)

For queries, reach out at ameyadamleuk@gmail.com or create an issue in this repository.