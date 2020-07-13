---
title: Configure Boto3 in AWS
description: In this step you learn how to configure Boto3 in AWS to programmatically perform all the tasks to upload call recordings to an Amazon S3 bucket
---

## Configure Boto3 in AWS

Boto3 is a package from AWS that allows you to perform most, if not all of the available tasks programmatically. 

> Note: To use Boto3, you will need to first have an AWS account and be able to generate an access key and secret. 

1. Navigate to your AWS instance and go to [IAM](https://console.aws.amazon.com/iam/home).

    ![](/images/use_cases/call-recording-to-s3/iam_add_user.png)

2. Under **Access Type**, select **Programmatic access**.

    ![](/images/use_cases/call-recording-to-s3/iam_create_user.png)

3. Write down (in a secure location) the newly created access key and secret.

4. Create an S3 bucket to which call recording files will be uploaded. Navigate to [AWS S3](https://s3.console.aws.amazon.com/) and click **Create Bucket**.

    ![](/images/use_cases/call-recording-to-s3/s3_create_bucket.png)

5. In the **Bucket Name** field, enter a unique name for the bucket. 

6. At the bottom of the page, clear the selection in the **Block all public access** checkbox. Since you are using the Boto3 client, you need to have the correct permissions on uploading objects to your bucket. Do not do this for production. Instead, create a new IAM role and add the permissions appropriately.

    ![](/images/use_cases/call-recording-to-s3/s3_config.png)

7. Install the Boto3 library using `pip`. In your Linux terminal Type:

    ```bash
    pip install boto3
    ```

8. Create an S3 client in Boto3 and provide the newly created keys:

    ```python
    import boto3
    client = boto3.client(
        's3',
        aws_access_key_id=AWS_ACCESS_KEY_ID,
        aws_secret_access_key=AWS_ACCESS_KEY_SECRET
    )
    ```

9. Next, loop through all the recordings from the `get_company_call_recordings` function you created earlier. For each recording, use the `download_recording` function to get the raw data of the recording. You could have saved the recording to a file, but since you are uploading to an S3 bucket, there's no need to save it locally, then upload it to S3.

    ```python
    for recording in recordings["_embedded"]["recordings"]:
      downloaded_recording = download_recording(token,recording["download_url"])
      client.put_object(Bucket="{MY_BUCKET}",
                           Key=recording["file_name"],
                           Body=downloaded_recording)
    ```

    [client.put_object](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/s3.html#S3.Client.put_object) is a boto3 function that uploads the raw data to the S3 bucket. This function accepts the following parameters:

    | Key | Description |
    | --- | ----------- |
    | `Bucket`      | The name of your newly created Amazon S3 bucket.
    | `Key`      | The name of the file. For this example, we will use the `file_name`, which is returned to us from the `company_call_recordings` API.
    | `Body`      | The raw binary data of the file.


After a few moments, depending on number and size, your files will be uploaded to your Amazon S3 bucket:

    ![](/images/use_cases/call-recording-to-s3/s3_uploaded_files.png)
