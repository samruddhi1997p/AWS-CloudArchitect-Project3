# Cloud Security - Secure the Recipe Vault Web Application
 
In this project:
 
* Deploy and assess a simple web application environment’s security posture
* Test the security of the environment by simulating attack scenarios and exploiting cloud configuration vulnerabilities
* Implement monitoring to identify insecure configurations and malicious activity 
* Apply methods learned in the course to harden and secure the environment
* Design a DevSecOps pipeline
 
## Dependencies and Prerequisites

### Access to AWS account  
Students will need to use their personal AWS accounts.  Udacity will provide a $100 credit for any usage costs. If project instructions are followed we do not anticipate usage costs to exceed this amount.
 
### Installation of the AWS CLI and Local Setup of AWS API keys
Instructions and examples in this project will make use of the AWS CLI in order to automate and reduce time and complexity.

## Exercise 1 - Deploy Project Environment
 
**_Deliverables for Exercise 1:_**
* **E1T4.txt** - Text file identifying 2 poor security practices with justification. 
 
### Task 1:  Review Architecture Diagram
In this task, the objective is to familiarize yourself with the starting architecture diagram. An architecture diagram has been provided which reflects the resources that will be deployed in your AWS account.
 
The diagram file, title `AWS-WebServiceDiagram-v1-insecure.png`, can be found in the _starter_ directory in this repo.
 
![base environment](AWS-WebServiceDiagram-v1-insecure.png)
 
#### Expected user flow:
- Clients will invoke a public-facing web service to pull free recipes.  
- The web service is hosted by an HTTP load balancer listening on port 80.
- The web service is forwarding requests to the web application instance which listens on port 5000.
- The web application instance will, in turn, use the public-facing AWS API to pull recipe files from the S3 bucket hosting free recipes. An IAM role and policy will provide the web app instance permissions required to access objects in the S3 bucket.
- Another S3 bucket is used as a vault to store secret recipes; there are privileged users who would need access to this bucket. The web application server does not need access to this bucket.
 
#### Attack flow:
- Scripts simulating an attack will be run from a separate instance which is in an un-trusted subnet.
- The scripts will attempt to break into the web application instance using the public IP and attempt to access data in the secret recipe S3 bucket.
 
### Task 2: Review CloudFormation Template
In this task, the objective is to familiarize yourself with the starter code and to get you up and running quickly. Spend a few minutes going through the .yml files in the _starter_ folder to get a feel for how parts of the code will map to the components in the architecture diagram. 
 
Additionally, we have provided a CloudFormation template which will deploy the following resources in AWS:
 
#### VPC Stack for the underlying network:
* A VPC with 2 public subnets, one private subnet, and internet gateways etc for internet access.
 
#### S3 bucket stack:
* 2 S3 buckets that will contain data objects for the application.
 
#### Application stack:
* An EC2 instance that will act as an external attacker from which we will test the ability of our environment to handle threats
* An EC2 instance that will be running a simple web service.
* Application LoadBalancer
* Security groups
* IAM role
 
### Task 3: Deployment of Initial Infrastructure
In this task, the objective is to deploy the CloudFormation stacks that will create the below environment.
We will utilize the AWS CLI in this guide, however you are welcome to use the AWS console to deploy the CloudFormation templates.
 
 
#### 1. From the root directory of the repository - execute the below command to deploy the templates.
 
##### Deploy the S3 buckets

##### Deploy the VPC and Subnets
 
##### Deploy the Application Stack 

#### 2. Once you see Status is CREATE_COMPLETE for all 3 stacks, obtain the required parameters needed for the project.
 
#### 3.  Upload data to S3 buckets

#### 4. Test the application
 
### Task 4:  Identify Bad Practices
  
## Exercise 2: Enable Security Monitoring
 
### Task 1: Enable Security Monitoring using AWS Native Tools

#### 1. Enable AWS Config (skip this step if you already have it enabled)    

#### 2. Enable AWS Security Hub
  
#### 3. Enable AWS Inspector scan

#### 4. Enable AWS Guard Duty
 
### Task 2: Identify and Triage Vulnerabilities
 
## Exercise 3 - Attack Simulation
  
### Task 1: Brute force attack to exploit SSH ports facing the internet and an insecure configuration on the server
 
#### 1. Log in to the attack simulation server using your SSH key pair.
#### 2. Run the below commands to start a brute force attack against the application server.  You will need the application server hostname for this. 
#### 3. Answer the following questions:
 
### Task 2: Accessing Secret Recipe Data File from S3
  
#### 1. Run the following API calls to view and download files from the secret recipes S3 bucket.  You will need the name of the S3 bucket for this.

## Exercise 4 - Implement Security Hardening

### Task 1 - Remediation plan

### Task 2 - Hardening

#### Remove SSH Vulnerability on the Application Instance

#### Apply Network Controls to Restrict Application Server Traffic

#### Least Privilege Access to S3  

#### Apply Default Server-side Encryption to the S3 Bucket

### Task 3: Check Monitoring Tools to see if the Changes that were made have Reduced the Number of Findings

### Task 4: Questions and Analysis

###  _Optional Standout Suggestion_ Task 5 - Additional Hardening

## Exercise 5 - Designing a DevSecOps Pipeline

### Task 1:  Design a DevSecOps pipeline

### Task 2 - Tools and Documentation

### _Optional Standout Suggestion_ Task 3 - Scanning Infrastructure Code

## Exercise 6 - Clean up 

