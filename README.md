"# node-http-serverless-soon" 

# A. Introduction

There are many different Serverless Framework available that we can use to implement a Serverless Application (https://geekflare.com/serverless-apps-frameworks/).

Basically these frameworks provide the step-by-step instructions to guide us through the procedure to follow that build the serverless application.

In this repository, we will use the Serverless Framework available at https://www.serverless.com/framework to build our serverless application.

Serverless Framework is a vendor-agnostic framework which supports serveless application development and deployment in a lot of cloud providers such as AWS, Microsoft Azure, Google Cloud, Apache OpenWhisk and Oracle Cloud.

We will provide the details for doing the same using AWS Serverless Application Model (https://aws.amazon.com/serverless/sam/) in another repository.

For a detailed comparison of the Serverless Framework versus the AWS Serverless Application Model, please refer to the link at https://www.serverless.direct/post/serverless-framework-vs-aws-sam-a-detailed-comparison

# B. Pre-requisites for this tutorial

In order to complete the tutorial, please ensure you have met the following pre-requisites:
- You have an AWS account.
- You have setup the AWS CLI tool and can access/provision the AWS services/resources via the Windows Command Prompt.
- You have the required permissions to access/provision AWS services/resources such as S3, Lambda, API Gateway and CloudFormation.

I am using Windows 10 Home Edition for the illustration but the instructions should be quite similar for other operating systems such as Linux or MacOS.

# C. Step-By-Step Instructions

## Step 1: Install npm and node

Since we are going to deploy a Node.js application, we need to install the Node Package Manager (npm) and node package itself as the first step.

To install the node package, please download the Windows installer at https://nodejs.org/en/download/

![alt text](images/module_3.6_install_node_and_npm.png)

And then follow the instructions of the Installer to complete the installation process.

Note that installing node using the Installer also installs npm.

![alt text](images/module_3.6_node_and_npm_version.png)

## Step 2: Create an empty application folder

Create an application folder in your local machine/laptop with the name:
__github-3.6-soon-node-http-serverless__.

![alt text](images/module_3.6_change_to_project_folder.png)

## Step 3: Install the serverless package globally

![alt text](images/module_3.6_install_serverless_framework.png)

## Step 4: Start the serverless setup process

Use the __serverless__ command to setup your serverless application. You will be prompted with a number of questions to configure your serverless environment:

![alt text](images/module_3.6_run_serverless_1_of_8.png)

### Step 4.1: Select AWS - Node.js - HTTP API

Use up and down arrow keys to navigate the options above. In this case, we are going to select __AWS - Node.js - HTTP API__. Press the __Enter__ key to confirm the selection.

![alt text](images/module_3.6_run_serverless_2_of_8.png)

### Step 4.2: Type node-http-serverless-soon as the project name.

![alt text](images/module_3.6_run_serverless_3_of_8.png)

Upon completion of the download, the Serverless Framework will create some template files to a new project folder __node-http-serverless-soon__ in the current folder.

![alt text](images/module_3.6_run_serverless_4_of_8.png)

The details of the files in the
__C:\Users\bunny\github-3.6-soon-node-http-serverless\node-http-serverless-soon__ folder are shown below:

__.gitignore__
```
# package directories
node_modules
jspm_packages

# Serverless directories
.serverless
```

__index.js__
``` Node.js
module.exports.handler = async (event) => {
  return {
    statusCode: 200,
    body: JSON.stringify(
      {
        message: "Go Serverless v3.0! Your function executed successfully!",
        input: event,
      },
      null,
      2
    ),
  };
};
```

__serverless.yml__
``` yaml
service: node-http-serverless-soon
frameworkVersion: '3'

provider:
  name: aws
  runtime: nodejs18.x

functions:
  api:
    handler: index.handler
    events:
      - httpApi:
          path: /
          method: get
```

The contents of README.md is too long and left out for brevity.

### Step 4.3: Press n and then Enter for Register or Login to Serverless Framework.

![alt text](images/module_3.6_run_serverless_5_of_8.png)

### Step 4.4: Press n and then Enter for Do you want to deploy now?

![alt text](images/module_3.6_run_serverless_6_of_8.png)

Beware that when you type __n__ and then __Enter__ for the first time, the cursor will go to the second line as shown above. Please type __n__ again and you will see the same prompt appearing again:

![alt text](images/module_3.6_run_serverless_7_of_8.png)

Now, just press the __Enter__ key to confirm the selection.

Here is the screensshot of the complete setup process.

![alt text](images/module_3.6_run_serverless_8_of_8.png)

## Step 5: Deploy the serverless application

Before you deploy your application, please ensure that you are in the project folder that you just created.

![alt text](images/module_3.6_change_to_project_folder_before_deploy.png)

If you deploy the application in the wrong folder, you will get an error:

Error:
```
This command can only be run in a Serverless service directory. Make sure to reference a valid config file in the current working directory if you're using a custom config file
```

To deploy the application, use the __serverless deploy__ command:

![alt text](images/module_3.6_serverless_deploy_1_of_6.png)

The next few screenshots showed what happened during the application deployment process.

![alt text](images/module_3.6_serverless_deploy_2_of_6.png)

The configuration details in the __serverless.yml__ file are used to create the CloudFormation stack files to be uploaded to the provider AWS.

These stack files are generated in a folder __.serverless__ within the project folder.

![alt text](images/module_3.6_serverless_deploy_3_of_6.png)

![alt text](images/module_3.6_serverless_deploy_4_of_6.png)

The deployment details within these stack files are uploaded to AWS to create the necessary resources needed to run the application.

![alt text](images/module_3.6_serverless_deploy_5_of_6.png)

Once all the resources are created in AWS, the details of the endpoints and so on are retrieved for display to the user.

![alt text](images/module_3.6_serverless_deploy_6_of_6.png)

The preceding screenshot shows that the endpoint for the GET API is accessible at __https://3pz6pcd4hj.execute-api.us-east-1.amazonaws.com/__

We can use the __curl__ command to test the endpoint as shown in the next screenshot.

![alt text](images/module_3.6_serverless_test_curl.png)

``` yaml
{
  "message": "Go Serverless v3.0! Your function executed successfully!",
  "input": {
    "version": "2.0",
    "routeKey": "GET /",
    "rawPath": "/",
    "rawQueryString": "",
    "headers": {
      "accept": "*/*",
      "content-length": "0",
      "host": "3pz6pcd4hj.execute-api.us-east-1.amazonaws.com",
      "user-agent": "curl/8.4.0",
      "x-amzn-trace-id": "Root=1-662a58ec-63b554190cf68e3e61ad20eb",
      "x-forwarded-for": "182.55.97.21",
      "x-forwarded-port": "443",
      "x-forwarded-proto": "https"
    },
    "requestContext": {
      "accountId": "266109346134",
      "apiId": "3pz6pcd4hj",
      "domainName": "3pz6pcd4hj.execute-api.us-east-1.amazonaws.com",
      "domainPrefix": "3pz6pcd4hj",
      "http": {
        "method": "GET",
        "path": "/",
        "protocol": "HTTP/1.1",
        "sourceIp": "182.55.97.21",
        "userAgent": "curl/8.4.0"
      },
      "requestId": "WyLU8hzqIAMEPpA=",
      "routeKey": "GET /",
      "stage": "$default",
      "time": "25/Apr/2024:13:21:48 +0000",
      "timeEpoch": 1714051308176
    },
    "isBase64Encoded": false
  }
}
```

Alternatively, we can test the endpoint using the browser:

![alt text](images/module_3.6_serverless_test_browser.png)

# D. Verifications of resources created in AWS

The next few screenshots showed the resources created in AWS:
- CloudFormation stack
- S3 bucket
- Lambda function
- API Gateway
- CloudWatch logs

![alt text](images/module_3.6_aws_created_resources_cloudformation.png)

![alt text](images/module_3.6_aws_created_resources_s3_bucket.png)

![alt text](images/module_3.6_aws_created_resources_lambda.png)

![alt text](images/module_3.6_aws_created_resources_api_gateway.png)

![alt text](images/module_3.6_aws_created_resources_cloudwatch.png)

# E. Destroy the resources created in AWS

Once we have verified our application is working as expected, we should delete all the resources that are deployed to AWS using the __serverless remove__ command.

![alt text](images/module_3.6_serverless_remove_1_of_3.png)

![alt text](images/module_3.6_serverless_remove_2_of_3.png)

![alt text](images/module_3.6_serverless_remove_3_of_3.png)

# Suggestion for future works

So far we have seen how the serverless application is implemented with only a GET REST API endpoint.

We will look at how the application features can be enhanced to make the endpoint respond to:
- Other REST API actions such as POST, PUT, etc.
- Events that are triggerd by other AWS services such as S3 bucket when data is loaded into it, etc.
