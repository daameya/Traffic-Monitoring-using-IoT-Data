# Traffic-Monitoring-using-IoT-Data

Paste the following command in cmd to run jobs/spark-jobs.py from root

docker exec -it traffic-monitoring-using-iot-data-spark-master-1 spark-submit ^
--master spark://spark-master:7077 ^
--packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.0,org.apache.hadoop:hadoop-aws:3.3.1,com.amazonaws:aws-java-sdk:1.11.469 jobs/spark-jobs.py
