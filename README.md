# AWS CloudFormation Cognito Identity Pool
> An [AWS Lambda-backed Custom Resource](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-custom-resources-lambda.html) for CRUD operations on Cognito Identity Pools

### Background
Cognito Identity Pools are not currently supported within CloudFormation templates. However, CloudFormation provides extensibility via Custom Resources, which enable Create/Update/Delete operations. This is meant to replace having to manually create Cognito Identity Pools manually via the CLI or web console.

### Quick Start

1. Ensure you have node.js >= 4 installed (preferrably via nvm)
1. Install gulp globally
1. Clone this repository
1. Run `npm install`
1. Create an S3 bucket to hold your Lambda Function (skip this if you already have one)
1. Create `config.json` (see below)
1. Run `gulp` this will:
  1. Build the Lambda function and place it in dist.zip
  1. Upload the function to S3
  1. Create the CloudFormation Stack
1. Create your IAM Role Policy(ies). Examples are provided in [cloudformation-role-policies-example.json](cloudformation-role-policies-example.json), which provides managed policies that are attached to the IAM roles. This is necessary for your users to be able to use their credentials to do anything.

### Example `config.json`
Create a `config.json` file. See [The AWS-SDK for JavaScript docs on CognitoIdentity](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/CognitoIdentity.html#createIdentityPool-property) for options, or run `aws cloudformation get-template-summary --template-body file:///path/to/cloudformation.json`

```JSON
{
	"IdentityPoolName": "IdentityPoolName",
	"AllowUnauthenticatedIdentities": false,
	"LambdaS3Bucket": "bucket-name",
	"LambdaS3Key": "CloudFormation-CustomResource-CognitoIdentityPool.zip"
	
}
```

All non-string values will be stringified for the CloudFormation template. If you're going to use the template directly (instead of using gulp), keep this in mind.