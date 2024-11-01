## Lambda in a VPC

### Cloud Quest Security: Lambda Security

#### Services used:

- **AWS Lambda:** Serverless compute
- **Amazon RDS:** Managed Relational Database Service.
- **AWS Secrets Manager:** A service to store encrypted strings (such as passwords) and access them securely.
- **Amazon VPC:** A virtual network
- **VPC Endpoints:** To give access
- **S3 Bucket:** Storage service

This repository contains the CloudFormation template (deployment.yaml) for a secure AWS Lambda function implementation, inspired by the Cloud Quest Security challenges.

#### Key Security Features:

- **VPC Endpoints:** The Lambda function operates within a VPC, accessing S3 and Secrets Manager through secure private endpoints, minimizing public internet exposure.
- **IAM Roles:** The function assumes a dedicated IAM role with least privilege access, allowing only necessary actions on specific resources.
- **Secrets Manager:** Sensitive information like database credentials are stored securely in Secrets Manager and accessed using IAM permissions.
- **Strong Encryptions:** The S3 bucket enforces server-side encryption with AES256 for data at rest.
- **Security Groups:** Security groups restrict inbound and outbound traffic, limiting communication to authorized sources.
- **Best Practices:** The template adheres to AWS security best practices for secure resource deployment.

#### Template Breakdown:

The CloudFormation template defines the following resources:

- **S3 Bucket:** Encrypted bucket for storing query results.
- **S3 Bucket Policy:** Allows access to the bucket only by the specific Lambda function.
- **S3 Gateway Endpoint:** VPC endpoint for private access to S3.
- **Database (RDS):** MySQL database instance within the private subnet of a VPC.
- **Database Security Group:** Controls inbound and outbound traffic for the database.
- **RDS Connection Parameters Secret:** Securely stores database connection details in Secrets Manager.
- **Secrets Manager Endpoint:** VPC endpoint for private access to Secrets Manager.
- **Secrets Manager Endpoint Security Group:** Allows inbound request from LambdaSecurityGroup only.
- **Function Execution Role:** IAM role for the Lambda function with specific permissions.
- **Lambda Security Group:** Controls inbound and outbound traffic for the Lambda function.
- **DatabaseFunction:** The Lambda function itself, configured to run in the VPC and connect to the database securely.

#### Deployment:

1. Replace the placeholder values for DBUsername and DBPassword with your desired credentials in the deployment.yaml file.
2. Ensure you have a pre-existing shared VPC with appropriate imports for shared-vpc-VpcId, shared-vpc-VPCPrivateSubnet2RouteTable, and shared-vpc-PrivateSubnet2.
3. Deploy the CloudFormation template using the AWS CLI or CloudFormation console.

### Disclaimer:

- This template is for educational purposes only and may require modifications for production environments. Always review security best practices before deploying in a production environment.

![diagram-v1](https://github.com/user-attachments/assets/ebcb380b-a5c8-4453-b47d-aef53e8b3369)
