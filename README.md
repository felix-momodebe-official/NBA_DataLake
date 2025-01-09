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
![image](https://github.com/user-attachments/assets/a6cbf382-2163-4a26-b726-508b026ad601)



# Step 5: Manually Check For The Resources
1. In the Search Bar, type S3 and click blue hyper link name

-You should see 2 General purpose bucket named "Sports-analytics-data-lake-container"
![image](https://github.com/user-attachments/assets/15736787-9c45-4a6d-9ea1-ab59ce058e69)



-When you click the bucket name you will see 3 objects are in the bucket
![image](https://github.com/user-attachments/assets/d1ec5127-bc1a-4667-adcd-5a12125278e2)


2. Click on raw-data and you will see it contains "nba_player_data.json"
![image](https://github.com/user-attachments/assets/6b63736b-dc37-4321-9f39-9b482f754fb5)


4. Click the file name and at the top you will see the option to Open the file

-You'll see a long string of various NBA data
![image](https://github.com/user-attachments/assets/bc729bf0-48b7-4255-8cee-99f1ef24a6cb)


4. Head over to Amazon Athena and you could paste the following sample query:
```bash
SELECT FirstName, LastName, Position, Team
FROM nba_players
WHERE Position = 'PG';
```

-Click Run
-You should see an output if you scroll down under "Query Results"

- Athena Query Output:

![image](https://github.com/user-attachments/assets/2d2428a3-6903-4890-bc2d-00619fa4aa74)



### **What We Learned**
1. Securing AWS services with least privilege IAM policies.
2. Automating the creation of services with a script.
3. Integrating external APIs into cloud-based workflows.


### **Future Enhancements**
1. Automate data ingestion with AWS Lambda
2. Implement a data transformation layer with AWS Glue ETL
3. Add advanced analytics and visualizations (AWS QuickSight)

### License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

### Contact

For any questions or inquiries, please reach out to us at: [SuccPinn Cloud & DevOps + AI](https://www.youtube.com/@SuccPinnCloudDevOps)

Happy coding!

