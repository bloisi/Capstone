# Data Engineering Capstone Project

## Step 1: Scope the Project and Gather Data

### Project Summary

The objective of this project is to give some key information to US National Tourism and Trade Office. For achieve this, it was created an ETL pipeline from three dataset sources: I94 immigration, US demographics and Airport codes.So, we could give some key indicators like most movimented airports or average of tourists that arrives in specific state. 

#### Scope 

Three datasets has chosen for the project:

i94 Immigration Data : this dataset is from the US National Tourism and Trade Office. This data source is used to load fact table;

U.S. City Demographic Data: This dataset contains information about the demographics of all US cities and census-designated places with a population greater or equal to 65,000.This data comes from the US Census Bureau's 2015 American Community Survey;

Airport Codes: The airport codes may refer to either IATA airport code, a three-letter code which is used in passenger reservation, ticketing and baggage-handling systems, or the ICAO airport code which is a four letter code used by ATC systems and for airports that do not have an IATA airport code.

The project implements a data lake using the datasets above loading data in a Redshift database hosted in AWS (Amazon Web Services). Through Pyspark the data has been extracted from immigration data and analysed before loading into the Redshift database. The conceptual data model was based in star schema defining a factless table and three dimension tables. Information like total or visitors, tourism by nationality, ports of entry and number of flights by airport executing queries on the tables. The workspace is the environment, including Pandas, Pyspark and Ipython-sql libraries. Python and SQL are the main languages used on this project. Using Pandas it was possible to see the details in Immigration dataset that was in sas format originally. Getting the meaning and understanding the Immigration data, it was possible to implement the star schema model. Through Pyspark the Immigration dataset was converted to parquet files and uploaded to S3 bucket (AWS service) together with other datasets in csv format. Using Exercise 2: Creating Redshift Cluster using the AWS python SDK the Redshift cluster is launched. So executing ETL code the Redshift stage tables are created and data loaded from dataset files. 

Once, the tables of star schema is loaded, some queries could be executed crossing data between fact and dimension tables. With simple query join using fact and dimension tables you could get total of tourists that arrived in airport or most visited states. An OLAP tool can be used to extract and aggregate infromation.

## Step 2: Explore and Assess the Data

<pre class="wp-block-preformatted">
cicid	i94yr	i94mon	i94cit	i94res	i94port	arrdate	i94mode	i94addr	depdate	...	entdepu	matflag	biryear	dtaddto	gender	insnum	airline	admnum	fltno	visatype
0	6.0	2016.0	4.0	692.0	692.0	XXX	20573.0	NaN	NaN	NaN	...	U	NaN	1979.0	10282016	NaN	NaN	NaN	1.897628e+09	NaN	B2
1	7.0	2016.0	4.0	254.0	276.0	ATL	20551.0	1.0	AL	NaN	...	Y	NaN	1991.0	D/S	M	NaN	NaN	3.736796e+09	00296	F1
2	15.0	2016.0	4.0	101.0	101.0	WAS	20545.0	1.0	MI	20691.0	...	NaN	M	1961.0	09302016	M	NaN	OS	6.666432e+08	93	B2
3	16.0	2016.0	4.0	101.0	101.0	NYC	20545.0	1.0	MA	20567.0	...	NaN	M	1988.0	09302016	NaN	NaN	AA	9.246846e+10	00199	B2
4	17.0	2016.0	4.0	101.0	101.0	NYC	20545.0	1.0	MA	20567.0	...	NaN	M	2012.0	09302016	NaN	NaN	AA	9.246846e+10	00199	B2
</pre>

## Step 3: Define the Data Model
  <img src="capstone.jpg" width="850" title="hover text">

## Step 4: Run ETL to Model the Data

First step is create a S3 bucket and launch a Redshift cluster. The parquet and csv files are uploaded to S3 bucket. The stage tables are created and using COPY command, the data are loaded in Redshift. The last step is load data from stage tables to star schema tables.

## Step 5: Complete Project Write Up

The data was increased by 100x: The partition could be required under files generated from SAS original files or convert cvs files in parquet partition files. The partition could be 83% faster than no partition files. It must analyze some column like date or state to partition data in parquet files. The load routine must consider the column partition to get the partition advantage. The partition creates a folder structure according to partition column values. So, load routine to copy files must create the right structure to load in Redshift database. 
 
The data populates a dashboard that must be updated on a daily basis by 7am every day: Using airflow DAGs and setting default arguments you can schedule to run every day at 7am. The specific arguments execution_date and next_execution_date must be defined to DAGs start at 7am. It is important ETL pipeline starts on time otherwise it will not provide updated information to users. The cost of hiring airflow service in AWS starts at $0.49 (50 DAGs). The Airflow Workflow Jobs can be executed on Amazon EKS or Amazon ECS because they make it easier to manage and autoscale Airflow clusters. You can optimize it for cost using EC2 Spot Instances.

The database needed to be accessed by 100+ people: 
