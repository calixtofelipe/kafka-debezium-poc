# KAFKA DEBEZIUM POC

## Architecture
mysql > debezium connector > kafka confluent > s3 sink connector > s3 (minion)

## Step by Step
- You have to install docker and docker-compose.  
- Download debezium mysql connector and load into *connectors* folder.
[MySql Connector](https://www.confluent.io/hub/debezium/debezium-connector-mysql?_ga=2.238002560.1202799299.1653306682-590055066.1635872888&_gac=1.219439979.1653341333.CjwKCAjw4ayUBhA4EiwATWyBrmJTAxn_cgLABL6y8adcv2I-4tYLvISQjYzLrumTgK-u4J1njiOLyxoCErIQAvD_BwE)  

- Check if you have sufficient memory/cpu in your computer to run all containers. At least, 10 GB memory and 6 cores will be sufficient.

- Start docker compose
```
docker-compose up -d
```


## Commands to check bin log
SHOW VARIABLES LIKE 'log_bin';
SHOW BINARY LOGS;

mysqlbinlog --read-from-remote-server --host=localhost --verbose mysql-bin.000003 -pdebezium --result-file=/tmp/mysql-bin.000003  


## Commands to test minio connection
aws s3 ls --recursive --summarize --endpoint-url=http://localhost:9000  
