# Project Title
### Data Engineering Capstone Project
## Step 1: Scope the Project and Gather Data
#### Scope 
The main goal of this project is to demonstrate all abilities achieved in Udacity data engineering course. Three datasets has chosen for the project.

i94 Immigration Data : this dataset is from the US National Tourism and Trade Office. This data source is used to load fact table;

U.S. City Demographic Data: This dataset contains information about the demographics of all US cities and census-designated places with a population greater or equal to 65,000.This data comes from the US Census Bureau's 2015 American Community Survey;

Airport Codes: The airport codes may refer to either IATA airport code, a three-letter code which is used in passenger reservation, ticketing and baggage-handling systems, or the ICAO airport code which is a four letter code used by ATC systems and for airports that do not have an IATA airport code.

The project implements a data lake using the datasets above loading data in a Redshift database hosted in AWS (Amazon Web Services). Through Pyspark the data has been extracted from immigration data and analysed before loading into the Redshift database. The conceptual data model was based in star schema defining a factless table and three dimension tables. Information like total or visitors, tourism by nationality, ports of entry and number of flights by airport executing queries on the tables. The workspace is the environment, including Pandas, Pyspark and Ipython-sql libraries. Python and SQL are the main languages used on this project. Using Pandas it was possible to see the details in Immigration dataset that was in sas format originally. Getting the meaning and understanding the Immigration data, it was possible to implement the star schema model. Through Pyspark the Immigration dataset was converted to parquet files and uploaded to S3 bucket (AWS service) together with other datasets in csv format. Using Exercise 2: Creating Redshift Cluster using the AWS python SDK the Redshift cluster is launched. So executing ETL code the Redshift stage tables are created and data loaded from dataset files.  

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

## Step 5: Complete Project Write Up

The data was increased by 100x: Amazon Redshift allows Petabyte-scale data warehousing. The database Redshift is very scalable, easy to increase nodes, including automatic changes.
(https://aws.amazon.com/redshift/features/)

The data populates a dashboard that must be updated on a daily basis by 7am every day: Through Airflow, ETL tasks can be implemented in DAGs and scheduled to run once per day (07:00 am)

The database needed to be accessed by 100+ people: Using S3, Redshift and AWS EMR (Elastic Mapreduce) combined, the solution can process data at any scale with great performance. (https://adataanalyst.com/wp-content/uploads/2020/07/emr?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc)
