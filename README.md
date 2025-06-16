# Fully Automated CI/CD Pipeline for a Web Application

## Project Overview

This project demonstrates a complete, automated CI/CD (Continuous Integration/Continuous Deployment) pipeline built using Jenkins, Docker, and AWS. The pipeline automatically builds, tests (in a real scenario), and deploys a simple Python Flask web application whenever changes are pushed to the main branch of this GitHub repository.

The goal of this project was to gain hands-on experience with core DevOps tools and practices, creating a robust automation workflow from source code to a live production environment.

---

## Architecture Diagram
![ChatGPT Image Jun 16, 2025, 11_46_30 PM](https://github.com/user-attachments/assets/444101de-5e8f-4e15-9b6f-f978b7ae152d)


**Example of how to reference the image:**
`![CI/CD Architecture Diagram](architecture_diagram.png)`

---

## Technologies Used

* **Cloud Provider:** AWS (Amazon Web Services)
    * **EC2:** Hosted the Jenkins server and the final deployed application.
    * **Security Groups:** Acted as a virtual firewall to control port access.
* **CI/CD Server:** Jenkins
* **Containerization:** Docker
* **Version Control:** Git & GitHub
* **Application:** Python (Flask Framework)
* **Operating System:** Ubuntu Server 22.04 LTS

---

## CI/CD Pipeline Breakdown

The pipeline is defined in the `Jenkinsfile` and consists of the following stages:

1.  **Checkout:** Jenkins pulls the latest code from the `main` branch of this GitHub repository.
2.  **Build:** Jenkins uses the `Dockerfile` in the repository to build a new Docker image of the Flask application. The image is tagged with the unique Jenkins build number for versioning.
3.  **Deploy:**
    * The pipeline first stops and removes any old version of the application container running on the server.
    * It then starts a new container from the newly built Docker image.
    * The application is exposed on port `8081` of the EC2 instance.
4.  **Cleanup:** After the pipeline finishes, old, unused Docker images are pruned to save disk space on the server.

---

## How to Run This Project

To replicate this project, you would need:

1.  An AWS account.
2.  An EC2 instance (t2.medium recommended) running Ubuntu.
3.  Jenkins and Docker installed on the instance.
4.  A GitHub Personal Access Token for authentication.
5.  The `Jenkinsfile` configured in a Jenkins pipeline job pointed at this repository.
