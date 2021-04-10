# Data Science Thesis 2021

This repository pertains to the **Data Science Thesis**
Author: Adam Horvath-Reparszky
Student-ID: 13326481

Internal Supervisior: Dr. Shaodi You
Email: s.you@uva.nl

Company Supervisor: Hernani Costa
Email: hernani@lalaland.ai

## Thesis Schedule
| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

## File Information
* `run_bg_removal.py` - This is the main python script that performs the **Background Removal** service.
* `MODNet` - This folder contains the class definitions for the algorithm currently employed.

## Pipeline
1. Constantly polls an AWS SQS Queue for new images to be processed.
2. Performs the **Background Removal** service on each image.
3. Updates a DynamoDB table with the background removal result.
4. Stores the background-devoid image in a target AWS IBM S3 bucket.

## Example
<p align="middle">
  <img src="demo2.jpeg" width="256"/>
  <img src="demo1.jpeg" width="256"/>
</p>

## Flags used by `run_bg_removal.py`
* `aws_source_bucket_name` - Name of the AWS IBM S3 bucket containing the images to be processed (Default : *lala-auto-focus*)
* `aws_target_bucket_name` - Name of the AWS IBM S3 bucket that will store the background-devoid images (Default : *background-removal*)
* `aws_dynamodb_table_name` - Name of the AWS DynamoDB table containing the image metadata (Default : *NewImages*)
* `model_path` - Path to MODNet model (Default : *MODNet/model_best.pth*)
* `aws_default_region_name` - Name of AWS Region (Default : *us-east-1*)
* `aws_queue_name` - Name of the AWS SQS Queue to poll (Default : *BackgroundRemovalQueue*)
* `verbose` - Enable / Disable display of logging information (Default action : *store_true*)
* `delete_sqs_message` - Enable / Disable deletion of SQS messages (Default action : *store_true*)
* `break_loop` - Flag to disable the constant polling of the AWS SQS Queue (Default action : *store_true*)

## Command Line
* For testing purposes<br>
`python run_bg_removal.py --break_loop --verbose [--other_flags]`
* Otherwise<br>
`python run_bg_removal.py --delete_sqs_message --verbose [--other_flags]`

## Docker
1. In the **Dockerfile**, replace the placeholders for the environment variables *AWS_ACCESS_KEY_ID*, *AWS_SECRET_ACCESS_KEY*, and *AWS_DEFAULT_REGION* with actual credentials.
2. Build the Docker image using the following command<br>
`docker build -t IMAGE_NAME:VERSION_TAG .`
3. Run the Docker image using the following command<br>
`docker run --gpus all --rm IMAGE_NAME:VERSION_TAG --delete_sqs_message --verbose [--other_flags]`