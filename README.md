**Automated Infrastructure & Container Deployment with Terraform and GitHub Actions**

This project demonstrates a complete end-to-end DevOps workflow that provisions AWS infrastructure using Terraform and deploys a containerized web application through GitHub Actions.

The system automates infrastructure creation, container build & distribution, and application deployment on AWS EC2.

**
Architecture Overview
**

The project consists of:

1. A containerized frontend (HTML/CSS)

2. Dockerized application image

3. Terraform-managed AWS infrastructure

4. GitHub Actions CI/CD pipeline

5. Remote Terraform state stored in S3


**Deployment Flow**

Developer → Git Push → GitHub Actions → Terraform → AWS
                                            ↓
                                      EC2 + Security Group
                                            ↓
                                      Docker Pull & Run



**Tech Stack
**
1. HTML / CSS

2. Docker

3. Terraform

4. AWS (EC2, Security Group, S3 Backend)

5. GitHub Actions

6. Self-hosted runner (initial testing phase)


**CI/CD Pipeline**

The GitHub Actions workflow automates:

**Trigger**

Push to main

Manual trigger (workflow_dispatch) for infrastructure destruction

**Workflow Steps**

1. Checkout repository

2. Configure AWS credentials (via GitHub Secrets)

3. Run terraform init

4. Run terraform plan

5. Run terraform apply

6. Provision AWS infrastructure

7. EC2 pulls Docker image from registry

8. Application container runs on EC2

Initially, a self-hosted runner was configured and used to validate the pipeline. The workflow was later migrated to GitHub-hosted runners for improved maintainability and simplicity.

**Infrastructure Provisioned**

Terraform provisions:

1. A Security Group with appropriate inbound rules

2. An EC2 instance

3. Remote backend configuration using S3 for state management

The EC2 instance is explicitly associated with the created Security Group to control network access.


**Containerization Strategy**

The application lifecycle follows the standard container workflow:

**Build**

A Dockerfile defines the environment and application configuration.
Running docker build produces a Docker image.

**Ship**

The image is pushed to a container registry (e.g., Docker Hub / ECR), making it accessible from any deployment target.

**Run**

On the EC2 instance:

1. docker pull retrieves the image

2. docker run starts the containerized application

This ensures portability, consistency, and reproducibility across environments.


Terraform Remote Backend

Terraform state is stored remotely in an S3 bucket to:

1. Enable state consistency

2. Prevent local state drift

3. Support collaborative workflows

4. Improve infrastructure reliability


**Infrastructure Lifecycle Management**

A workflow_dispatch event was added to allow manual execution of:


terraform destroy


This enables controlled teardown of infrastructure resources directly from GitHub Actions.


**Local Development**

To build and run locally:

docker build -t app .
docker run -p 80:80 app


**Key Learnings**

1. Implementing Infrastructure as Code using Terraform

2. Configuring remote state with S3 backend

3. Managing AWS credentials securely with GitHub Secrets

4. Automating provisioning through CI/CD pipelines

5. Working with self-hosted vs GitHub-hosted runners

6. Understanding container lifecycle: Build → Ship → Run

7. Managing infrastructure lifecycle with automated destroy workflows


**Project Outcome**

This project demonstrates a production-style DevOps workflow where infrastructure provisioning and application deployment are fully automated, version-controlled, and reproducible.


<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-04-45" src="https://github.com/user-attachments/assets/35af98fe-dff3-47d1-8151-24952b49ae45" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-05-32" src="https://github.com/user-attachments/assets/00245bf5-f1be-423f-b8a1-3fe1083d6a57" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-07-56" src="https://github.com/user-attachments/assets/6366067d-08e2-41c9-a7de-b3a78e2bfe25" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-06-04" src="https://github.com/user-attachments/assets/ab5b2de7-a01e-42d0-8802-d6b6b5be5dd7" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-06-58" src="https://github.com/user-attachments/assets/125d4ac1-8fc0-4518-8398-6fbf046899dc" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-06-51" src="https://github.com/user-attachments/assets/4a6a9f8e-26a1-46b2-ab9c-29ffd5d2b60c" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-06-37" src="https://github.com/user-attachments/assets/27cb6780-1a4a-43d1-8f60-8e225a5ef2e2" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-06-29" src="https://github.com/user-attachments/assets/c716a502-86cd-4006-a834-1a06bdc9f5e3" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-09-28" src="https://github.com/user-attachments/assets/1e77d27c-db98-448f-a376-44c8c9545d23" />
<img width="1366" height="768" alt="Screenshot from 2026-02-11 11-08-09" src="https://github.com/user-attachments/assets/8b023478-2bca-42c8-8dc1-3810e289dde2" />

