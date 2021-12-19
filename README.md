# Data Engineering Capstone Project

#### Project Summary
The purpose of the data engineering capstone project is to demonstrate what I've've learned throughout the data engineering nanodegree program. 


The project follows the follow steps:
* Step 1: Scope the Project and Gather Data
* Step 2: Explore and Assess the Data
* Step 3: Define the Data Model
* Step 4: Run ETL to Model the Data
* Step 5: Complete Project Write Up


**Scope**

There will be 1 fact table with 5 dimension tables processed from the datasets below. This data model will be used for a further data analysis using SQL in order to see the relationship between the people immigrating to the US, the demmographics of the state / city they immigrated to and the average country average temprature.
The main dataset is data on immigration to the United States, and supplementary datasets used are U.S. city demographics, and temperature data.

Once the data is processed queries such as: 
- Average household size of the city the immigrant arrived to, by birthyear(age) of the immigrant.
- Median age of immigrants, average temprature by country of residence where average.
- Visa Type by Female and Male Population, state.



**Data Used:**

- I94 Immigration Data
- Temperature Data
- Demographics Data


**Tools Used:**

- AWS
    - Redshift
- Python
    - PySpark
- SQL



**I94 Immigration Data**

This data comes from National Travel and Trourism Office(NTTO). The subject of the data is the immigrants going to the U.S. and the information is gives are where they come from, birth year, gender, visa type, etc.

**Temperature Data**

This data comes from Kaggle, and it shows the temperature in different cities around the world. It's recorded monthly, and the values are the average temperature of that month.

**US Cities Demographics Data**

This data comes from OpenSoft, and it shows the demographics of the cities in the U.S. including the population, median age, the state the city belongs to, etc.


### The Data Model

<img src="../capstone image.PNG" />

- The immigration fact table is the heart of the data model. This table's data comes from the immigration data sets and contains keys that links to the dimension tables. The data dictionary of the immigration dataset contains detailed information on the data that makes up the fact table.
- The visa table holds dimension data related to the immigration
- The person table holds dimension data related to the person
- The travel table holds dimension data related to the travel
- The demo table holds demographic information about the state which the person is residing in
    - This links to the immigration data by state code
- The temp table holds average temprature for each country  
    - This links to the immigration data by country code
    
    
### The pipeline steps are as follows:

- Load the immigration dataset.
- Load the demographic dataset.
- Load the temprature dataset.
- Clean the immigration dataset (drop duplicates / missing data).
- Clean the demographic dataset (drop duplicates / missing data).
- Clean the temprature dataset (drop duplicates / missing data).
- Transform into fact and dimension tables.
- Convert dates and rename columns.
- Aggregate temprature data.
- Merge on country code to temprature data to be able to join.
- Parquet datasets into S3 bucket.


## Data Dictionary

<img src="../capstone image dd.PNG" />


**Rationale for the choice of tools and technologies for the project**

- Apache spark was used because of:
    - it's ability to handle multiple file formats 
    - it's ability to handle large amounts of data.
    - Apache Spark offers a analytics engine for big data.
    - Spark APIs for operating on large datasets.
- Propose how often the data should be updated and why.
    - The current I94 immigration data is updated monthly, and hence the data will be updated monthly.
    
    
**How I would approach the problem differently under the following scenarios:**
- The data was increased by 100x.
    - Spark can handle the increase but we would consider increasing the number of nodes in our cluster.
- The data populates a dashboard that must be updated on a daily basis by 7am every day.
    - In this scenario, Apache Airflow will be used to schedule and run data pipelines.
- The database needed to be accessed by 100+ people.
    - In this scenario, we would move our analytics database into Amazon Redshift.