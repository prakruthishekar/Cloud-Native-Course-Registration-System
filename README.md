# Spring Boot Web Application


## Description

This Spring Boot web application provides functionality for managing assignments. It allows authenticated users to perform operations such as creating, retrieving, updating, and deleting assignments. Additionally, it offers a public health check API endpoint.

## Table of Contents

- [Spring Boot Web Application](#spring-boot-web-application)
  - [Description](#description)
  - [Table of Contents](#table-of-contents)
  - [Features](#features)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)

## Features

**Authenticated Operations:**

- `GET /v1/assignments`: Get a list of all assignments.
- `POST /v1/assignments`: Create a new assignment.
- `GET /v1/assignments/{id}`: Get details of a specific assignment by its ID.
- `DELETE /v1/assignments/{id}`: Delete a specific assignment by its ID.
- `PUT /v1/assignments/{id}`: Update a specific assignment by its ID.

**Public Operation:**

- `GET /healthz`: Health Check API (Available to all users without authentication).

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Java Development Kit (JDK) 8 or higher
- Maven build tool
- MySQL or PostgreSQL database (for storing assignments)
- IDE (Eclipse, IntelliJ IDEA, or your preferred choice)
- Git (for cloning the repository)

## Installation

To set up the Spring Boot web application, follow these steps:

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/your-spring-boot-app.git

1. Navigate to the project directory:

    ```bash
   cd your-spring-boot-app

3. Configure your database connection in application.properties or application.yml.
    ```bash
   export MYSQL_USERNAME=your_username
   export MYSQL_PASSWORD=your_password


4. Build the application:
    ```bash
    mvn clean install
   
5. Run the application:
    ```bash
   mvn spring-boot:run


# Usage

To use this web application, follow these steps:

1. Access the web application by visiting [http://localhost:8080](http://localhost:8080) in your web browser or your preferred API client (e.g., Postman).

2. Authenticate using your credentials to access authenticated endpoints.

3. Use the provided API endpoints to manage assignments and check the health of the application.

## Authentication

To access authenticated endpoints, you must authenticate with valid credentials. This typically involves sending an Authorization header with an authentication token or username/password combination.

## API Endpoints

### Authenticated Endpoints

#### GET /v1/assignments

- **Description**: Get a list of all assignments.
- **Authentication**: Required.
- **Parameters**: None.
- **Response**: JSON array of assignment objects.

#### POST /v1/assignments

- **Description**: Create a new assignment.
- **Authentication**: Required.
- **Parameters**: Assignment data in the request body.
- **Response**: JSON object representing the created assignment.

#### GET /v1/assignments/{id}

- **Description**: Get details of a specific assignment by its ID.
- **Authentication**: Required.
- **Parameters**: id (assignment ID) in the URL path.
- **Response**: JSON object representing the assignment details.

#### DELETE /v1/assignments/{id}

- **Description**: Delete a specific assignment by its ID.
- **Authentication**: Required.
- **Parameters**: id (assignment ID) in the URL path.
- **Response**: Status code indicating success or failure.

#### PUT /v1/assignments/{id}

- **Description**: Update a specific assignment by its ID.
- **Authentication**: Required.
- **Parameters**: id (assignment ID) in the URL path and assignment data in the request body.
- **Response**: JSON object representing the updated assignment.

### Public Endpoint

#### GET /healthz

- **Description**: Health Check API.
- **Authentication**: Not required.
- **Parameters**: None.
- **Response**: Status message indicating the health of the application.



# Build custom machines images that can be to create virtual machines in cloud using Pulumi for Infrastructure as Code.

Install packer in terminal using the below command.
brew tap hashicorp/tap
brew install hashicorp/tap/packer

Create a package and add .hcl file, configure the AMI requirements in the file and execute the below commands
 
Set AWS profile befire running packer
export AWS_PROFILE=dev

check profile
aws configure list

Initialize packer
packer init .

Aligh the format of the packer file
packer fmt cloud.pkr.hcl

Validate packer
packer validate cloud.pkr.hcl

Build packer
packer build cloud.pkr.hcl

When you run Packer with this configuration file, the following steps will occur:

- Packer will start the build process and launch a new temporary EC2 instance in your AWS account using the specified source AMI (var.source_ami) as the base image.

- Packer will connect to the EC2 instance using SSH (Secure Shell).

- The shell provisioner will execute a series of commands on the EC2 instance. In this case, it will:

- Update the package list on the instance with sudo apt-get update.
Install MySQL Server on the instance with sudo apt-get install -y mysql-server.
Set the MySQL root user's password using sudo mysql -e "..."
Install OpenJDK 11 with sudo apt-get install -y openjdk-11-jdk.
Install Maven with sudo apt-get install -y maven.
Once all the provisioner commands have been executed successfully, Packer will stop the EC2 instance.

- Packer will create a new Amazon Machine Image (AMI) based on the state of the EC2 instance. This new AMI will include all the changes and software installations made during the provisioning process.

- The AMI will be registered in your AWS account with the specified name, description, and in the specified region.

- Packer will clean up by terminating the temporary EC2 instance.

- After running this Packer configuration, you will have a custom AMI that includes MySQL, Java (OpenJDK 11), and Maven installed, as well as any other software and configurations you specified. This AMI can be used to launch EC2 instances with these software packages pre-installed.



Set your sql password in command line

export DB_HOST=localhost:3306
export DB_NAME=csye6225 
export DB_USERNAME=root
export DB_PASSWORD=12345678
export SNS_ARN=arn:aws:sns:us-east-1:226534876078:mySNSTopic-6c2cec1
export AWS_REGION=us-east-1
packer validate cloud.pkr.hcl



# Steps to install MySQL in Debian

Create a Swap File: If you haven't already, create a swap file. This will act as "virtual" memory, and while it's slower than actual RAM, it can prevent the OOM killer from terminating processes.

Here's how you can create a 2GB swap file:
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab


# Import SSL/Tls certificate:

The AWS CLI command you provided is used to import an SSL/TLS certificate into AWS Certificate Manager (ACM). ACM is a service provided by AWS for managing SSL/TLS certificates that are used to secure web applications and services.

```
aws acm import-certificate --certificate fileb://Certificate.pem \
      --certificate-chain fileb://CertificateChain.pem \
      --private-key fileb://PrivateKey.pem




# Pulumi AWS Infrastructure Deployment

This repository provides a Pulumi project for deploying infrastructure on AWS across different environments (`dev` and `demo`).

## Prerequisites
- Ensure that the [AWS CLI](https://aws.amazon.com/cli/) is installed and configured with both `dev` and `demo` profiles.
- Install the [Pulumi CLI](https://www.pulumi.com/docs/get-started/aws/install-pulumi/).

## Initialization

For first-time setup:

### Set AWS profile
```bash
aws configure --profile demo
aws configure --profile dev
export AWS_PROFILE=demo
export AWS_PROFILE=dev
aws configure list


```

### Initialize the Pulumi project

```bash
pulumi new aws-python
```

### Create environments for dev and demo
```bash
pulumi stack init dev
pulumi stack init demo
```

### Configure the dev environment
```bash
pulumi stack select dev
pulumi config set aws:profile dev
```

### Configure the demo environment
```bash
pulumi stack select demo
pulumi config set aws:profile demo
```

### Define the CIDR block
```bash
pulumi config set cidrBlock "10.0.0.0/16"
pulumi config set customAmiId "ami-020b251b4f78f405a"
```

### Deploy to the dev environment

```bash
pulumi stack select dev
AWS_PROFILE=dev pulumi up
```

### Deploy to the demo environment
```bash
pulumi stack select demo
AWS_PROFILE=demo pulumi up
```

### Check and Set the AWS region configured
```bash
pulumi config get aws:region
pulumi config set aws:region us-west-1
```

### Destroy resources in the dev environment
```bash
pulumi stack select dev
pulumi destroy
```

### Destroy resources in the demo environment
```bash
pulumi stack select demo
pulumi destroy
```

pulumi stack -> will give the stack selected


If you change the region destroy the stack using the below command
```bash
pulumi stack rm --force demo  
```

This will delete or create the resource which had problem in getting created or deleting the resource

```bash
pulumi refresh 
```

pulumi up

pulumi down

Set the Secret in Pulumi Configuration: You can use the Pulumi CLI to set the secret:

```bash
pulumi config set db_name "csye6225"
pulumi config set username "csye6225"
pulumi config set --secret dbPassword YOUR_PASSWORD_HERE
pulumi config set hosted-zone-id "***23D9PQ1YW****"
pulumi config set domain-name "dev.prakruthi.me"
pulumi config set --secret mail_gun_api_key "******d9594211a436f3-3******"
pulumi config set mail_gun_domain prakruthi.me


```
# Copy the installed packages from the virtual environment to the package directory
cp -r venv/lib/python3.11/site-packages/* .  # replace python3.x with your Python version


# Serverless Lambda Function for Assignment Submission Notification

This repository contains a serverless AWS Lambda function written in Python. The function gets triggered by an AWS SNS topic and sends out an email notification regarding the submission of assignments received from an API.

## Functionality

The Lambda function is designed to perform the following tasks:
- Listen to an AWS SNS topic for incoming messages related to assignment submissions.
- Receive data about the submission from an API trigger through SNS.
- Compose an email notification summarizing the assignment submission details.
- Send the email notification to designated recipients.

## Setup

### Requirements
- AWS account with necessary permissions to create Lambda functions, SNS topics, and IAM roles.
- Python 3.x installed locally.
- AWS CLI configured with appropriate credentials.

### Deployment Steps
1. Clone this repository to your local machine.

2. Navigate to the project directory:
    ```
    cd lambda-assignment-notification
    ```

3. Set up a virtual environment (optional but recommended):
    ```
    python3 -m venv venv
    source venv/bin/activate
    ```

4. Install required dependencies:
    ```
    pip install boto3  # AWS SDK for Python
    # Other necessary packages
    ```

5. Modify the `lambda_function.py` file to suit your specific requirements. Update the email content, recipients, and any other necessary configurations.

6. Deploy the Lambda function to AWS:
    ```
    aws lambda create-function --function-name AssignmentNotification --runtime python3.8 --role <YOUR-ROLE-ARN> --handler lambda_function.lambda_handler --zip-file fileb://lambda_function.zip
    ```
    Replace `<YOUR-ROLE-ARN>` with the ARN of the IAM role associated with your Lambda function.

7. Create an SNS topic in your AWS account and subscribe the Lambda function to this topic.

8. Trigger the Lambda function by publishing a message to the SNS topic with assignment submission details from your API.

## Usage

To trigger the Lambda function and send an assignment submission notification:
1. Make a POST request to your API endpoint responsible for handling assignment submissions.

2. Once the submission is received by the API, publish a message to the configured SNS topic with the relevant details about the assignment submission.

3. The Lambda function will be triggered by the SNS topic and will send out an email notification based on the provided details.

## Configuration

### Environment Variables
- Modify environment variables within the Lambda function configuration if required, for example:
    - `EMAIL_SENDER`: Email address of the sender.
    - `EMAIL_SUBJECT`: Subject line for the assignment submission notification.
    - `RECIPIENTS`: Email addresses of recipients who should receive the notification.

### IAM Permissions
Ensure the IAM role attached to the Lambda function has appropriate permissions to:
- Publish and receive messages from the configured SNS topic.
- Send emails using AWS SES (Simple Email Service) or other email sending services configured.

## Notes
- Update the IAM role permissions and AWS configurations based on your specific setup and security requirements.
- Monitor AWS costs associated with using Lambda, SNS, and other related services.

