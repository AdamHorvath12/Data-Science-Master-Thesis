# Data Science Thesis 2021

This repository pertains to the **Data Science Thesis** of Adam Horvath-Reparszky at University of Amsterdam in 2021.

**Author**: Adam Horvath-Reparszky

* **Student-ID**: 13326481

* **Email**: adam.horvath-reparszky@student.uva.nl

**Internal Supervisior**: Dr. Shaodi You

* **Email**: s.you@uva.nl

**Company Supervisor**: Hernani Costa

* **Email**: hernani@lalaland.ai

## Thesis Schedule
| Week  | Date | Planned Achievement  | Achieved |
| ------------- | ------------- | ------------- | ------------- |
| Week 1 | 29/03 - 04/04 | Examine research papers in the field of garment transferring |  |
| Week 2  | 05/04 - 11/04  | Start to do experiments using the selected papers. Decide which dataset I am going to use |  |
| Week 3 |  12/04 - 18/04 | Finish experiments and start to identify general problems and categorise them. Select the evaluation measures |  |
| Week 4  | 19/04 - 25/04 | Test the evaluation measures. Start writing the Abstartct/Introduction/Related Work part in the Thesis draft |  |
| Week 5 |  26/04 - 02/05 | Writing the Thesis draft (Abstract/Intro/Literature review). Get new ideas how to solve existing problems (artifacts) |  |
| Week 6  |  03/05 - 09/05 | Try out solutions for solving problems. Improve the Thesis draft|  |
| Week 7 | 10/05 - 16/05 | Try out solutions for solving problems. Improve the Thesis Draft |  |
| Week 8  | 17/05 - 23/05 | Writing Methodology + Results |  |
| Week 9 | 24/05 - 30/05 | Writing Methodology + Results|  |
| Week 10  | 31/05 - 06/06 | Evaluation part |  |
| Week 11 | 07/06 - 13/0607/06 - 13/06 | Finalise the Methodology part + Future work|  |
| Week 12  | 14/06 - 20/06 | Final version of Thesis Draft |  |
| Week 13 | 21/06 - 27/06 | Finishing the thesis and prepare for Thesis Defense |  |

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