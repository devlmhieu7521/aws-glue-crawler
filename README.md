# aws-glue-crawler
Using AWS Glue Crawler to scan data in S3 Bucket to infer informations and schema of data. After that Using AWS Athena to query data

## Architecture

The architecture of the project to understand about AWS Glue,S3 ,AWS Athena

![Architecture](./images/Architecture.png)



## Glue Crawler

First, I will create database in AWS Glue Data Catalog which is a central metadata repository where the schema information and other metadata for your data assets are stored. This metadata includes information about databases, tables, and columns.

![Create Database](./images/create_database_in_data_catalog.png)

**Create Glue Crawler**:

**Step 1**: Set up the name of the Crawler

![Create Crawler S1](./images/create_glue_crawler_step1.png)

**Step 2**: Choose data source from which Glue Crawler can scan data and infer the schema.

![Create Crawler S2](./images/create_glue_crawler_step2.png)

**Step 3**: Configure security settings. I create IAM role to have permissions to access the target source.

![Create Crawler S3](./images/create_glue_crawler_step3.png)

**Step 4**: Set up Output and Schedule.

In this step, I set up the target source (Glue Data Catalog) when Glue Crawler finish to have the information of the data source.

About Scheduling, I just chose '''On demand'''. It can be set based on cron expression to run it on specific time.

![Create Crawler S4](./images/create_glue_crawler_step4.png)

Done set up Glue Crawler will be liked that:

![Done Crawler](./images/done_create_glue_crawler.png)

Then, I run this Crawler:

![Run Crawler](./images/run_glue_crawler.png)

After, Glue Crawler finish, the schema will be recorded in Glue Data Catalog. It is a table named 'reviews' in database which I set up first.

The schema of the data source:

![Schema](./images/schema.png)

## AWS Athena

After, AWS Glue Crawler scans the data source and stores the information and metadata in AWS Glue Data Catalog, AWS Athena automatically connects to help you query the data using SQL.

**NOTE**: Before you can run the query you want, you need to set up the place to save the query run, I means set up S3 Bucket to save the query.

![NOTE](./images/note_athena.png)

Finally, Here is the result after I use:

- S3 for saving raw data.
- AWS Glue Crawler to scan the data to get the information and metadata.
- Then, AWS Athena to retrieve the data source.



