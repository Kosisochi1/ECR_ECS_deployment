# Go CI/CD Pipeline to AWS ECS

## Description
This repository contains a robust GitHub Actions workflow designed to automate the security scanning, building, and deployment of a Go application to Amazon ECS.


### 🚀 Workflow Overview
The pipeline is divided into three primary stages to ensure code quality and secure delivery:
- Pre-build (Manual/Security):  * Secrets detection, static analysis (SonarQube), vulnerability scanning (Trivy & Govulncheck), and testing.
- Build:  Dockerizes the Go application and pushes the image to Amazon ECR.
- Deploy:  Updates the ECS Task Definition and deploys the new image to an ECS Cluster.
### 🛠 Features

#### 🛡 Security & Quality

-  Gitleaks :  Scans the repository for hardcoded secrets.
- SonarQube :  Performs deep code quality and security analysis.
- Trivy :  Scans the filesystem for vulnerabilities.
- Govulncheck :  Analyzes the Go code for known vulnerabilities in dependencies.
- SARIF Upload :  Integration with the GitHub Security tab for vulnerability tracking.
  
### 🧪 Testing 
- Runs standard Go Unit Tests.
- Runs Integration Tests using the --tags=integration flag.
  
### 🏗 DevOps & Deployment
- Docker:  Builds and tags images.
- AWS ECR:  Securely stores container images.
- AWS ECS:  Managed container orchestration for deployment.
- Slack Notifications:  Real-time updates on the status of every job.
  
### ⚙️ Configuration 
Required GitHub Secrets
To run this workflow successfully, you must configure the following secrets in your GitHub repository (Settings > Secrets and variables > Actions):


```
Secret Name              Description

SONAR_TOKEN             Authentication token for SonarQube.

AWS_ACCESS_KEY_ID       AWS IAM user access key.

AWS_SECRET_ACCESS_KEY   AWS IAM user secret key.

ECR_REPO                The full URI of your Amazon ECR repository.

SLACK_WEBHOOK_URL       The incoming webhook URL for your Slack channel.

```

### Environment Specifics
- AWS Region:  eu-west-1
- Go Version:  1.22
- ECS Cluster:  much_todo_demo-cluster
- ECS Service:  much_todo_demo-service
- Task Definition Source:  S3 bucket task-definition-store-bucket

  
### 🚦 How to Trigger
The workflow triggers automatically on:

- Every push to the main branch.
- Every pull request targeting the main branch.
  
### 📁 Directory Structure

- application-code/:  Contains the Go source code, go.mod, and go.sum.
- trivy.yaml:  Configuration file for the Trivy scanner.
- Dockerfile:  Used during the Build stage to package the application.


### 👥 Author

Emmanuel Kosi


### 🛠 Troubleshooting

- ECR Push Failed? Check if the AWS_ACCESS_KEY_ID has AmazonEC2ContainerRegistryPowerUser permissions.

- Deployment Timeout? Check the ECS service events in the AWS Console.
