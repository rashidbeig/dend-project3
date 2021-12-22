# Project 3 DEND Cloud Datawarehouse

## Description

Sparkify is a music streaming startup with a growing user base and song database.

Their user activity and songs metadata data resides in json files in S3. The goal of the current project is to build an ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights in what songs their users are listening to. 

## How to run

1. To run this project you will need to fill the following information, and save it as *dwh.cfg* in the project root folder.

```
[AWS]
KEY= MYKEY
SECRET= MYSERCRET

[IAM_ROLE]
ARN= MYARN

[CLUSTER]
HOST=MYHOST
DB_NAME=DBNAME
DB_USER=DBUSER
DB_PASSWORD=DBPASSWORD
DB_PORT=5439

[DWH] 
DWH_CLUSTER_TYPE=multi-node
DWH_NUM_NODES=4
DWH_NODE_TYPE=dc2.large

DWH_IAM_ROLE_NAME=dwhRole
DWH_CLUSTER_IDENTIFIER=dwhCluster
DWH_DB=DBNAME
DWH_DB_USER=USER
DWH_DB_PASSWORD=PASSWORD
DWH_PORT=5439
DWH_ENDPOINT = ENDPOINT


[S3]
LOG_DATA='s3://udacity-dend/log_data'
LOG_JSONPATH='s3://udacity-dend/log_json_path.json'
SONG_DATA='s3://udacity-dend/song_data'
```


2. Follow the steps and code in aws_cluster_create.ipynb to create Redshift Cluster
 

3. Complete sql_queries.py to create tables.
Ensure the dwh.cfg details are correct as per create_tables.py

4. Log into Redshift to query data from console to check that tables are created.

5. Run etl.py to copy data into staging tables and insert data into final tables.

6. Create file analysis.py to run the analysis queries.

7. Delete the Redshift cluster

## Structure

This project includes five script files:

- analysis.py runs a few queries on the created star schema to validate that the project has been completed successfully.
- aws_cluster_create_ipynb is a jupyter notebook Redshift cluster is created.
- create_table.py creates fact and dimension tables for the star schema in Redshift.
- etl.py is loads data from S3 into staging tables on Redshift and inserts into analytics tables on Redshift.
- sql_queries.py has SQL statements are defined, which are then used by etl.py, create_table.py and analytics.py.
- dwh.cfg has configuraiton data required to create the Redshift Cluster and then connect to it.
- README.md is current file.

## Database schema design
State and justify your database schema design and ETL pipeline.

#### Staging Tables
- staging_events
- staging_songs

####  Fact Table
- songplays - records in event data associated with song plays i.e. records with page NextSong - 
*songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

#### Dimension Tables
- users - users in the app - 
*user_id, first_name, last_name, gender, level*
- songs - songs in music database - 
*song_id, title, artist_id, year, duration*
- artists - artists in music database - 
*artist_id, name, location, lattitude, longitude*
- time - timestamps of records in songplays broken down into specific units - 
*start_time, hour, day, week, month, year, weekday*


## Queries and Results

Number of rows in each table:

| Table            | rows  |
|---               | --:   |
| staging_events   | 8056  |
| staging_songs    | 14896 |
| artists          | 10025 |
| songplays        | 333   |
| songs            | 14896 |
| time             |  8023 |
| users            |  105  |

# dend-project3
