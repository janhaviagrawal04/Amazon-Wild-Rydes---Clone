# Ride-Sharing App - AWS Wild Rydes Clone 🦄

## Project Overview

This project is a serverless ride-sharing application inspired by the AWS Wild Rydes sample project. It is built using a combination of AWS services including CodeCommit, Amplify, Cognito, Lambda, IAM, API Gateway, and DynamoDB. The goal of the project is to demonstrate how these services can be integrated to create a fully-functioning web application that can be deployed and managed entirely in the cloud.

**Note:** The code for this project is based on the AWS Wild Rydes lab, which can be found here: [AWS Wild Rydes Lab]([https://aws.amazon.com/getting-started/hands-on/build-modern-web-app-fargate-lambda-dynamodb-python/](https://aws.amazon.com/getting-started/hands-on/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/module-3/ 
).

## Table of Contents

- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Setup Instructions](#setup-instructions)
  - [1. Creating a CodeCommit Repository](#1-creating-a-codecommit-repository)
  - [2. Configuring IAM and Git Credentials](#2-configuring-iam-and-git-credentials)
  - [3. Cloning the Repository and Copying Code from S3](#3-cloning-the-repository-and-copying-code-from-s3)
  - [4. Hosting the Web App with AWS Amplify](#4-hosting-the-web-app-with-aws-amplify)
  - [5. Implementing User Authentication with Amazon Cognito](#5-implementing-user-authentication-with-amazon-cognito)
  - [6. Creating the Ride-Sharing Backend with Lambda and DynamoDB](#6-creating-the-ride-sharing-backend-with-lambda-and-dynamodb)
  - [7. Connecting the Frontend to the Backend using API Gateway](#7-connecting-the-frontend-to-the-backend-using-api-gateway)
- [Testing and Continuous Deployment](#testing-and-continuous-deployment)
- [License](#license)

## Technologies Used

- **AWS CodeCommit**: For version control and storing the application's HTML, CSS, and JS files.
- **AWS S3**: To store and manage static assets before moving them to CodeCommit.
- **AWS Amplify**: To build and host the web application, enabling continuous deployment.
- **Amazon Cognito**: For user authentication and management.
- **AWS Lambda**: To handle the backend logic of the ride-sharing functionality.
- **Amazon DynamoDB**: To store ride details and other dynamic data.
- **AWS IAM**: For managing access and permissions across AWS services.
- **API Gateway**: To create RESTful APIs that connect the frontend with the backend.

## Setup Instructions

### 1. Creating a CodeCommit Repository

1. **Create an empty repository** in AWS CodeCommit to store your application’s code.

2. **Add IAM policy for CodeCommit access**:
   - Log in with your IAM user (not the Root User).
   - Go to **IAM -> Users -> YourUser -> Add Permissions**.
   - Attach the `AWSCodeCommitPowerUser` policy.
   - This grants your IAM user the necessary permissions to access CodeCommit.

3. **Create Git credentials** for your IAM user:
   - Go to **IAM -> Users -> YourUser -> Security Credentials**.
   - Under **HTTPS Git credentials for AWS CodeCommit**, generate credentials.
   - Download the username and password for future use.

### 2. Configuring IAM and Git Credentials

1. **Clone the repository**:
   - Open AWS CloudShell and clone your CodeCommit repository using the command:
     ```bash
     git clone <Repository_URL>
     ```
   - Enter the Git credentials (username and password) when prompted.

### 3. Cloning the Repository and Copying Code from S3

1. **Copy project code from S3 to CloudShell**:
   - Use the following command to copy the code from the S3 bucket to your cloned repository:
     ```bash
     aws s3 cp s3://your-bucket-name/your-bucket-path ./ --recursive
     ```
   - This command downloads all files from the specified S3 bucket into the current directory.

2. **Commit and push the code to CodeCommit**:
   - Navigate to the repository folder and add the files to the commit:
     ```bash
     git add .
     git commit -m "Initial Commit"
     git push
     ```

### 4. Hosting the Web App with AWS Amplify

1. **Create and configure an Amplify app**:
   - In the AWS Console, go to **AWS Amplify**.
   - Create a new app, select **Host Web App** and choose your CodeCommit repository.
   - Enable continuous deployment to automatically deploy changes pushed to CodeCommit.
   - Deploy the app.

### 5. Implementing User Authentication with Amazon Cognito

1. **Create a Cognito User Pool**:
   - In the AWS Console, go to **Amazon Cognito**.
   - Create a new user pool, configure sign-in options, and enable self-registration.
   - After the pool is created, copy the **User Pool ID** and **App Client ID**.

2. **Update the app configuration**:
   - In your repository, navigate to the **js** folder.
   - Create or edit the `config.js` file to include the User Pool ID, Client ID, and region.
   - Commit the changes, triggering an automatic deployment in Amplify.

### 6. Creating the Ride-Sharing Backend with Lambda and DynamoDB

1. **Set up DynamoDB**:
   - Create a new DynamoDB table with `RideID` as the partition key.
   - Copy the table’s ARN for later use.

2. **Create an IAM role for Lambda**:
   - Create a role with the **AWSLambdaBasicExecutionRole** policy.
   - Add a custom policy that allows `PutItem` actions on your DynamoDB table.

3. **Create a Lambda function**:
   - Write and deploy the Lambda function to handle ride requests.
   - Test the function using a sample event in the AWS Console.

### 7. Connecting the Frontend to the Backend using API Gateway

1. **Create an API in API Gateway**:
   - Build a REST API and create a new resource and method (POST).
   - Link the method to your Lambda function using the Lambda proxy integration.

2. **Set up Cognito authorization**:
   - Add an authorizer in API Gateway using your Cognito User Pool.
   - Test the integration and deploy the API.

3. **Update the app configuration**:
   - Update the `config.js` file with the new API Invoke URL and commit the changes.

## Testing and Continuous Deployment

- Any changes made to the project code in CodeCommit will automatically trigger a new deployment in AWS Amplify.
- You can make updates to the app, test them in your environment, and see the changes reflected on the live website.


**Code Source:** The code for this project is based on the AWS Wild Rydes lab. You can find more details here: [AWS Wild Rydes Lab](https://aws.amazon.com/getting-started/hands-on/build-modern-web-app-fargate-lambda-dynamodb-python/).
