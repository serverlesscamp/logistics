# Attending a camp

Thanks for coming to a Serverless Code Camp. This document gives you a quick intro what you can expect and how to set things up 
on your machine so you can get the most value out of the camp:

## What you can expect

Serverless code camp is a peer-learning event. This means that you will learn cool new stuff -- how to use cloud functions and deploy serverless apps -- with the help of the other participants. The event facilitators will be there to provide some guidance, examples, and help you if you get stuck, but it will mostly be up to you to poke, experiment, try things out and take the learning in the direction that suits you the most. 

We will pair up the participants to work together, based on their interest and level of knowledge. If you've never had any experience with cloud functions, this will give you a nice chance to explore the basics. If you already did a lot of work, then this will give you an excuse to try some more exotic things out, and experiment with topics you don't normally get to do at work.

This means that you can also choose the language and the platform you want to experiment with. For beginners, that need more guidance, we suggest using AWS and JavaScript/Node.js, as that's how you'll be able to get the most help. If you feel you can experiment more, then you can choose any of the other languages AWS and Azure functions support.

Please bring your own computer to the camp, so you can be comfortable coding from the start, and so that you have the code from the exercises on your machine when you leave. This is how you need to set it up:

* [If you plan to use AWS Lambda and API Gateway](#setup-for-aws)
* [If you plan to use Azure Cloud Functions](#setup-for-azure)

## Setup for AWS

* Register for an AWS account upfront if you don't already have one. To use Lambda, you'll need a verified account (typically using phone verification), and the stuff we'll do will fit into the free account allowance, but you will need an individual account. Register at [aws.amazon.com/](https://aws.amazon.com)
* Install [AWS Command line tools](https://aws.amazon.com/cli/)
* Configure AWS Command Line tools to [work with your credentials](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html).
If you do not want to use the access credentials for your main user account, but want to set up a separate user profile for the camp, assign the following roles to the user: [AWSLambdaFullAccess](https://console.aws.amazon.com/iam/home?region=us-east-1#policies/arn:aws:iam::aws:policy/AWSLambdaFullAccess), [IAMFullAccess](https://console.aws.amazon.com/iam/home?region=us-east-1#policies/arn:aws:iam::aws:policy/IAMFullAccess), [AmazonAPIGatewayAdministrator](https://console.aws.amazon.com/iam/home?region=us-east-1#policies/arn:aws:iam::aws:policy/AmazonAPIGatewayAdministrator)
* If you plan to use JavaScript (recommended for beginners), install [Node.js](https://nodejs.org). If you plan to use a different language, set up the SDK for the chosen environment. Here are the links: [Java](http://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-install.html), [.NET](https://aws.amazon.com/documentation/sdk-for-net/), [Ruby](https://aws.amazon.com/documentation/sdk-for-ruby/). You can find links for other environments, and toolkits for IDEs, at [AWS Documentation page](https://aws.amazon.com/documentation/) -- search for SDKs & Toolkits.

### Test your AWS setup

Test that your account has the privileges to create IAM roles, lambda functions and APIs. 

The following commands should all work OK, without throwing errors:

1. Set up a simple IAM role

  ```bash
  aws iam create-role \
  --role-name=hello-world-lambda-executor \
  --assume-role-policy-document '{"Version": "2012-10-17", "Statement": [{"Effect": "Allow","Principal": {"Service": "lambda.amazonaws.com"},"Action": "sts:AssumeRole"}]}' \
  --query Role.Arn --output text
  ```

2. Wait about 10 seconds, then use the result printed by the previous command instead of `<ROLE>` in the command below, to set up a simple Lambda function (get the ZIP file from the [test-lambda](test-lambda) directory and put it in the local directory where this command is executed).

  ```bash
  aws lambda create-function \
  --function-name hello-world-function2 \
  --role <ROLE> \
  --runtime nodejs4.3 \
  --handler main.handler \
  --zip-file fileb://test-lambda.zip 
  ```

3. set up a simple API interface:

  ```bash
  aws apigateway create-rest-api --name test-api
  ```

## Setup for Azure

### Setup an Azure account

* If you have MSDN, you likely already have access to Azure. If not, you'll need an Azure subscription. Register at [azure.microsoft.com](https://azure.microsoft.com), you can also use the free trial for this camp. (Note: the trial registration requires a valid credit card and phone number for the verification)

### Your first function

* You can create your first function directly from the [Azure Functions website](https://functions.azure.com/try). You can find the detailed instruction in the [getting started guide](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function).
* If you want to work with your functions locally and use git for version control you can set it up using the [continuous deployment guide](https://docs.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment).
* You can start learning more about Azure Functions from the [official documentation](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview).

### Test your Azure setup
* You can use the built-in Azure Functions Management interface inside the [Azure Portal](https://portal.azure.com/)

### Using Azure Functions from the command line (Early Beta)
* **Note:** the Azure Functions CLI is using Node.js but currently **only supporting Windows**.
* Currently two CLI exist for Azure Functions:
  * Old: [azurefunctions](https://www.npmjs.com/package/azurefunctions)
    * some features might not work
    * [available options](https://github.com/azure/azure-webjobs-sdk-script/pull/477)
  * New: [azure-functions-cli](https://www.npmjs.com/package/azure-functions-cli)
    * some features might not work
    * not fully documented, usage samples are missing
    * [available options](https://www.npmjs.com/package/azure-functions-cli)

