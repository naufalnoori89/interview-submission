# Interview Solution By Naufal Mohamed Noori

(Date: 28 December 2025)

### Problem Statement
To design and develop a data warehouse using industrial-standard framework from 3 possible datalake inputs for latter consumption by data analyst, machine learning, analystic, and technology in usable formats dictated (AWS, GCP, Azure, Snowflake, local dbt, etc.) .

Inputs:
1. CRM System - contact information, demographic information, email communications, call recordings, form submissions.
2. Events System - registrations and attendance at student events
3. Application System - applications, education history and qualifications, statuses, certifications. 

###  Proposed Architecture
I will be using medallion architecture approach to produce the final datatype consumable by various parties stated above. The proposed pipeline:

Data Source --> Data Ingestion (Landing) --> Broze Layer (Raw Data) --> Silver Later (Cleaned Data) --> Gold Layer (Transformed Data) --> Consumption (Data Ready For Users)

1. Data Source
- CRM (contacts, emails, calls, forms)
- Events (registrations, attendance)
- Applications (education history, status changes)

2. Data Ingestion
- This part is quite tricky as no 'clear' input stated from the interview documents. Hence I will make assumption that the data will come from a database and will be fetch in batch. 'Dummy' data will be created from all 3 possible sources to showcase the migration between each layer in the pipeline. As known there are bunch of sandbox opensource data related to the CRM etc out there but fro simplicity I am going to create the dummy data from scratch.

3. Bronze Layer (Raw data)
- Just an exact copy of the data pulled out from ingestion. Usually data organization are done here from unstructured and structred data. However, as simplication made in this demo we only need to deal with structure data from a simple 'demo' database

4. Silver Layer (Cleaned)
At this stage, I will perform various standard data cleanup as follows:
    - Standardized IDs
    - Clean timestamps
    - Remove duplicates
    - Handling null values (Depends if we determine null is not ok for certain column)

5. Gold Layer (Transformed)
The last stage is to create a final analytic transformed data ready for end user consumption. For this demo, I will focus on 3 outputs which are:
    - Student Dimension
        - This table will emphasizes on the student details, the origin of the students, and the program the applied for
    - Student Engagement
        - This tabe will emphasize on student interaction with QS application via emails or web appplication or any other mean of engagements (Physical signup etc). 
    - Aggregated Engagement Scores
        - This will contains some score of engagement which gauges value the students' level of connection/interest to QS

### Consumption
The final data are ready to be used by:
- BI Dashboards
- Data Science Models
- AI (If we are to handle and train ML model etc in our ETL pipeline - but in our simple case it is not - this will be the answer for the enhancement question)

