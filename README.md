# Deploying Socks Shop: A Microservices-Based Application on Kubernetes Using Infrastructure as Code (IaC)

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


## Infrastructure Provisioning

Using Terraform, we will provision the necessary infrastructure resources on AWS, including VPCs, subnets, security groups, and an EKS cluster. This approach ensures a clear and reproducible infrastructure setup.

## Prerequisites

You need to have a cloud infrastructure for this project I used Aws

* [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
* [Terraform Download]()


### Getting Started

1. Cretae a project folder and Initialize your git Repository
Proceed to create sub-folders for your terraform and other configurations
```bash
   mkdir socks-app
   mkdir terraform kubernetes monitoring
   cd socks-app
   git init
   ```
2. provision your infrastructure
Initialize the your terraform files, using this command which will download the necessary providers and set up the backend:

   ```bash
   terraform init
   ```
3. **Initialize the Terraform Project**
   Run the following command to initialize the Terraform project, which will download the necessary providers and set up the backend:

   ```bash
   terraform init
   ```
4. **Create an Execution Plan**
   Generate an execution plan to review the actions Terraform will take to provision your infrastructure:

   ```bash
   terraform plan
   ```
5. **Apply the Terraform Configuration**
   Apply the changes to provision the infrastructure. The `--auto-approve` flag can be added to avoid the prompt for confirmation:

   ```bash

   terraform apply --auto-approve
   ```

  The EKS cluster creation process may take several minutes to complete. Once the cluster is created, you will see the following output:
  ![cluster-up](img/cluster-create.png)
  ![cluster-up](img/cluster-up.png)
  
  you can check the cluster on your aws console
  ![cluster-created](img/aws-3.png)



6. Configure your Kubernetes to connect to your Cluster
    Install and update kubectl to connect to your EKS cluster. You can use the following command to install kubectl:

    aws eks update-kubeconfig --name socksShop-eks-lgXOS --region us-east-1
  Once you run this command a new kubeconfig file will be created in your .kube folder.

  run the following command the command 
  ```
   kubectl apply -f deployment.yaml
  ```
  ![deployment](img/kubectl.png)
  
  You can use the kubeconfig file to access the Kubernetes cluster and deploy the Socks Shop application.
  check the status of your pods using the command
  ```
  kubectl get pods -n sock-shop 
  ```
  ![pod status](img/connectedcluster.png)
  
 After the pods are running, you can access the Socks Shop application through portforwarding running the following command:
 ```
  kubectl port-forward service/front-end -n sock-shop 8980:80
  ```
  ![port-forward](img/06-port-frw.png)

  you can also check it on your browser
  ![portforwarding browser](img/07-port-frw.png)

  seeing the front end of the application means the application is running successfully
  now you can wrap it to your domain name using ngix ingress controller
  ```
  helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
  helm repo update
  ```
  after updating your helm repo, you can install the ingress controller using the following command
  ```
  helm install ingress-nginx ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace
  ```
  ![ingress-controller](img/07-helm.png)
  
  you can check the domain dns or Elb ip of your ingress controller using the following command
  ```
  kubectl get services -o wide -n ingress-nginx
  ```
  ![ingress-controller](img/ingress-service.png)
 
  once you have your load balancer ip you can access your app using the ip address
  ![elb ip](img/9-not-secure.png)

  you can see from the image above that the application is not secure, to make it secure you can use cert-manager to generate a certificate for your domain name
  
  you can proceed to encrypt your domain name using cert-manager
  