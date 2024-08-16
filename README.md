# Project Overview

## Objective
We aim to deploy a microservices-based application, specifically the Socks Shop, using a modern approach that emphasizes automation and efficiency. The goal is to use **Infrastructure as Code (IaaC)** for rapid and reliable deployment on Kubernetes.

## Setup Details Explained

### What You'll Do
Your main task is to set up the Socks Shop application, a demonstration of a microservices architecture, available on GitHub. You'll be using tools and technologies that automate the setup process, ensuring that the application can be deployed quickly and consistently.

### Resources
- **Socks Shop Microservices Demo**: [GitHub Repository](https://github.com/microservices-demo/microservices-demo)
- **Detailed Implementation Guide**: [GitHub Repository](https://github.com/microservices-demo/microservices-demo/blob/master/DEPLOY.md)

## Task Instructions

### Use Infrastructure as Code
Automate the deployment process. This means all the steps to get the application running on Kubernetes should be scripted and easily executable.

### Focus on Clarity and Maintenance
Your deployment scripts and configurations should be easy to understand and maintain. Think of someone else (or yourself in the future) needing to update or replicate your setup.

## Key Evaluation Criteria

1. **Deployment Pipeline**: How the application moves from code to a running environment.
2. **Monitoring and Alerts**: Implement Prometheus for monitoring and set up Alertmanager for alerts.
3. **Logging**: Ensure the application's operations can be tracked and analyzed through logs.
4. **Tools for Setup**: Use either Ansible or Terraform for managing configurations. Choose an Infrastructure as a Service (IaaS) provider where your Kubernetes cluster will live.
5. **Security and HTTPS**: Make sure the application is accessible over HTTPS by using Let’s Encrypt for certificates. Consider implementing network security measures and use Ansible Vault for handling sensitive information securely.

## Extra Project Requirements for Bonus Points

1. **HTTPS Requirement**: The application must be securely accessible over HTTPS.
2. **Infrastructure Security**: Enhance security by setting up network perimeter security rules.
3. **Sensitive Information**: Use Ansible Vault to encrypt sensitive data, adding an extra layer of security.

## Project Goals Summarized
This project is about deploying a microservices-based application using automated tools to ensure quick, reliable, and secure deployment on Kubernetes. By focusing on **Infrastructure as Code**, you'll create a reproducible and maintainable deployment process that leverages modern DevOps practices and tools.
