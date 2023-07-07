# YouTube Data Analysis Project

This project involves processing and analyzing YouTube data using data engineering techniques. It includes two scripts, `lambda_function.py` and `spark.py`, each serving a specific purpose in the data pipeline. The `lambda_function.py` script handles data ingestion and transformation, while the `spark.py` script performs data processing and writes the results to an output location.

## Lambda Function (lambda_function.py)

The `lambda_function.py` script is designed to be run as an AWS Lambda function. It utilizes the following dependencies:

- `awswrangler`: A Python library for interacting with AWS services, including S3 and Glue.
- `pandas`: A powerful data manipulation library in Python.
- `urllib`: A module for URL encoding and decoding.

### Functionality

1. Reads data from an S3 bucket triggered by an event.
2. Extracts the required columns from the JSON data.
3. Writes the transformed data to an S3 location in Parquet format.
4. Optionally, writes the data to an AWS Glue Catalog table for cataloging and querying purposes.

## Spark Job (spark.py)

The `spark.py` script is designed to be executed as an AWS Glue ETL(Extract Transform Load) job. It uses the AWS Glue API and Spark capabilities for data processing.

### Dependencies

The script relies on the following libraries:

- `awsglue`: The AWS Glue library for Python.
- `pyspark`: The Python library for Apache Spark.

### Functionality

1. Creates a SparkContext, GlueContext, and SparkSession for running the job.
2. Reads data from an AWS Glue Catalog table named "raw_statistics" in the "db_youtube_raw" database.
3. Applies column mappings and transformations to the data.
4. Resolves choice types and drops null fields from the transformed data.
5. Writes the processed data to an S3 location in Parquet format, partitioned by the "region" column.

## Configuration

Both scripts rely on specific environment variables to be set in the execution environment:

- `s3_cleansed_layer`: The S3 path where the transformed data will be stored.
- `glue_catalog_db_name`: The name of the AWS Glue Catalog database.
- `glue_catalog_table_name`: The name of the AWS Glue Catalog table.
- `write_data_operation`: The write operation to perform (e.g., "overwrite", "append", etc.).

Ensure that these variables are set correctly in the execution environment for the scripts to function properly.

## Execution

To execute the scripts, follow these steps:

1. Set up the AWS Lambda function and provide the necessary environment variables.
2. Configure an AWS Glue ETL job and specify the required resources.
3. Run the AWS Glue job with the `spark.py` script as the ETL script.

Make sure that the necessary permissions and access to AWS services are granted to the Lambda function and AWS Glue job for successful execution.

Please note that these scripts serve as a basic implementation for YouTube data analysis and can be further extended or modified based on specific requirements and use cases.
