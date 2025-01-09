# NBA Data Lake - AWS Analytics Infrastructure
## Introduction:
This project automates the deployment of a scalable NBA analytics data lake leveraging AWS infrastructure. 
The core script (`setup_nba_data_lake.py`) orchestrates the integration between Amazon S3 for storage, AWS Glue for data cataloging, and Amazon Athena for SQL querying capabilities.

# Overview
The setup script (`setup_nba_data_lake.py`) executes a series of automated operations:

Provisions a dedicated Amazon S3 bucket that serves as the primary storage layer for both raw and transformed NBA data
Ingests sample NBA datasets in JSON format into the designated S3 bucket
Establishes an AWS Glue database and generates an external table schema, enabling structured data queries
Implements Amazon Athena configurations to facilitate SQL-based analysis of the NBA data residing in the S3 bucket

# Architecture
```
S3 Bucket (Data Storage)
    ├── Raw Data (JSON)
    └── Processed Data
          └── NBA Statistics
              
AWS Glue (Data Catalog)
    ├── Database
    └── External Table Schema

Amazon Athena
    └── SQL Query Interface
```

# Prerequisites
Before running the script, ensure you have the following:

API Access

- Create a free account at Sportsdata.io
- Navigate to "Developers" → "API Resources" → "Introduction & Testing"
- Register for "SportsDataIO API Free Trial" (select NBA)
- Access the Developer Portal via email confirmation link
- Select NBA from the left navigation panel
- Locate "Standings" section
- Find your API key under "Query String Parameters"
- Save this API key for script configuration

AWS Permissions
Your IAM user/role must have these permissions:

Amazon S3
- `s3:CreateBucket`
- `s3:PutObject`
- `s3:DeleteBucket`
- `s3:ListBucket`

AWS Glue

- `glue:CreateDatabase`
- `glue:CreateTable`
- `glue:DeleteDatabase`
- `glue:DeleteTable`

Amazon Athena
- `athena:StartQueryExecution`
- `athena:GetQueryResults`

# START HERE 
# Step 1: Access your AWS Account

1. Sign into your aws console and launch the aws Cloudshell (No additional authentication required)
OR
2. Authenticate into your AWS account form any terminal with AWS CLI installed (Athentication required: Credentials, Role, etc)

# Step 2: Create the setup_nba_data_lake.py file
1. In the CLI (Command Line Interface), type
```bash
nano setup_nba_data_lake.py
```
   OR
```bash
vi setup_nba_data_lake.py
```



2. In another window, go to [GitHub](https://github.com/alahl1/NBADataLake)

-Copy the contents inside the setup_nba_data_lake.py file

-Go back to the Cloudshell window and paste the contents inside the file.

3. Find the line of code under #Sportsdata.io configurations that says "api_key" 
paste your api key inside the quotations

4. Press ^X to exit, press Y to save the file, press enter to confirm the file name 


# Step 3: Create .env file
1. In the CLI (Command Line Interface), type
```bash
nano .env
```
2. paste the following line of code into your file, ensure you swap out with your API key
```bash
SPORTS_DATA_API_KEY=your_sportsdata_api_key
NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players
```

3. Press ^X to exit, press Y to save the file, press enter to confirm the file name 


# Step 4: Run the script
1. In the CLI type
```bash
python3 setup_nba_data_lake.py
```
-You should see the resources were successfully created, the sample data was uploaded successfully and the Data Lake Setup Completed

# Step 5: Manually Check For The Resources
1. In the Search Bar, type S3 and click blue hyper link name

-You should see 2 General purpose bucket named "Sports-analytics-data-lake"

-When you click the bucket name you will see 3 objects are in the bucket

2. Click on raw-data and you will see it contains "nba_player_data.json"

3. Click the file name and at the top you will see the option to Open the file

-You'll see a long string of various NBA data

4. Head over to Amazon Athena and you could paste the following sample query:
```bash
SELECT FirstName, LastName, Position, Team
FROM nba_players
WHERE Position = 'PG';
```

-Click Run
-You should see an output if you scroll down under "Query Results"

### **What We Learned**
1. Securing AWS services with least privilege IAM policies.
2. Automating the creation of services with a script.
3. Integrating external APIs into cloud-based workflows.


### **Future Enhancements**
1. Automate data ingestion with AWS Lambda
2. Implement a data transformation layer with AWS Glue ETL
3. Add advanced analytics and visualizations (AWS QuickSight)

