## Serverless Three Tier Web Application

Sample 3-tier web app for an eCommerce platform
We are leveraging AWS Serverless technologioes to implement our 3-tier application

### Architecture

![Alt text](static-content/Screen%20Shot%202021-12-05%20at%2012.58.20%20AM.png?raw=true "Title")



This project contains source code and supporting files for a serverless application that you can deploy with the SAM CLI. It includes the following files and folders.

```
- static-content - Code for Static Website hosted in S3 and Cloudfront
- application - Code for the App and Data Tier
- events - Invocation events that you can use to invoke the serverless function.
- tests - Unit tests for the application code
- template.yaml - A template that defines the application's AWS resources
```

The application uses several AWS resources, including Lambda functions, API Gateway API and RDS Aurora Serverless MySQL DB. These resources are defined in the `template.yaml` file in this project. You can update the template to add AWS resources through the same deployment process that updates your application code.

#### Deploy Static Contents

Static-Contents : contains all the static components
content-deploy.yaml : Cloudfromation template to Create DNS, Bucket, Certificates and Cloudfront Content Distribution
index.html: Content

`aws s3 cp s3://<s3-key></s3-location> static-content/index.html`

`aws cloudformation deploy --template-file static-content/content-deploy.yaml --stack-name mdemo-app-static --parameter-overrides Key1=Value1 Key2=Value2 --tags Key1=Value1 Key2=Value2`

#### Deploy Dynamic Contents

![Alt text](static-content/Screen%20Shot%202021-12-05%20at%2012.58.37%20AM.png?raw=true "Title")

Web, Application and Data Layer

The Serverless Application Model Command Line Interface (SAM CLI) is an abstraction of CloudFormation that adds functionality for building and testing Serverless applications. It uses Docker to run your functions in an Amazon Linux environment that matches Lambda. It can also emulate your application's build environment and API.

**Create Project**

> `sam init --runtime python3.8 –-name demo-web-app`
    -----------------------
    Generating application:
    -----------------------
    Name: demo-web-app
    Runtime: python3.8
    Architectures: x86_64
    Dependency Manager: pip
    Application Template: hello-world
    Output Directory: .

    Next application steps can be found in the README file at ./demo-web-app/README.md
    

    Commands you can use next
    =========================
    [*] Create pipeline: cd demo-web-app && sam pipeline init --bootstrap
    [*] Test Function in the Cloud: sam sync --stack-name {stack-name} --watch
    



**Note**: Because the project is created with the default AWS sample Hello World application, customers need to edit the app.py and template.yaml files to add content for their use case.


> $ sam build
Building codeuri: /Users/bmat/workdir/demo-web-app/hello_world runtime: python3.8 metadata: {} architecture: x86_64 functions: [‘HelloWorldFunction’] 
…
Build Succeeded
Built Artifact: ./aws-sam/build Built Template: .aws…



**Cloudformation Lint**

> $ cfn-lint template.yaml


Deployment

`$ sam deploy --guided --capabilities CAPABILITY_IAM CAPABILITY_AUTO_EXPAND`

Configuring SAM deploy


	Looking for config file [samconfig.toml] :  Not found

	Setting default arguments for 'sam deploy'
	Stack Name [sam-app]: demo-web-app

    Allow SAM CLI IAM role creation [Y/n]: Y
	Save arguments to samconfig.yaml [Y/n]: Y

	Looking for resources needed for deployment: Not found.
	Creating the required resources...
> 
`$ sam deploy --guided --capabilities CAPABILITY_IAM CAPABILITY_AUTO_EXPAND`

Configuring SAM deploy

	Looking for config file [samconfig.toml] :  Not found

	Setting default arguments for 'sam deploy'
	Stack Name [sam-app]: demo-web-app

    Allow SAM CLI IAM role creation [Y/n]: Y
	Save arguments to samconfig.yaml [Y/n]: Y

	Looking for resources needed for deployment: Not found.
	Creating the required resources...
	Successfully created	Successfully created

