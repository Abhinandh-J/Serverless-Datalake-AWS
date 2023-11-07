# Serverless-Datalake-AWS
A small datalake project that showcases a couple of prominently used AWS services working together to automate an ETL task.

Workflow Diagram:
![Serverless Datalake](https://github.com/Abhinandh-J/Serverless-Datalake-AWS/assets/72979737/a42b9d6f-fe9b-43c2-9065-03a294e00646)

Process:
When raw CSV data gets uploaded to the specified input s3 bucket, a lambda function is triggered. This function will start a glue crawler that catalogs the uploaded CSV data.
Once the Glue Crawler has finished cataloging and shows status as "succeeded" (on CloudWatch), a 2nd lambda function gets triggered.
This lambda function will start a Glue PySpark job that can perform ETL tasks and finally write the result as a parquet file in our target s3 bucket. 
For simplicity, the code provided doesn't contain any transformations but it can easily be added in the same script. 
We will use CloudWatch again to monitor the job and once the status shows as "succeeded", AWS SNS will send out an email informing us about the process completion.

NOTE: I realize that there are a lot of tweaks and improvements that can be made to this and a lot of edge cases to be satisfied. This is version 0 and explains the basics of an automated datalake and ETL run.
I would appreciate and love to hear any suggestions or new ideas related to this!
