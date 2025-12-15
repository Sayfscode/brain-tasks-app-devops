Intro

This project is my first DevOps deployment project.
The aim of this project was to understand how a simple frontend application can be deployed using Docker, AWS, and Kubernetes.

Application Details
	•	Application: Brain Tasks App
	•	Frontend: React
	•	The application runs inside a Docker container
	•	The final application is deployed on AWS EKS (Kubernetes)


Tools and Services Used
	•	GitHub – to store the source code
	•	Docker – to containerize the application
	•	AWS ECR – to store Docker images
	•	AWS EKS – to run the application using Kubernetes
	•	AWS CodeBuild – to build and push Docker images
	•	AWS CloudWatch Logs – to view build and deployment logs


Dockerization
	•	A Dockerfile was created to build the React application
	•	The app is served using Nginx
	•	The Docker image is built locally and also through AWS CodeBuild

AWS ECR (Elastic Container Registry)
	•	An ECR repository was created
	•	Docker images are pushed to ECR
	•	CodeBuild is configured to authenticate and push images automatically

Kubernetes Deployment (EKS)
	•	An EKS cluster was created with worker nodes
	•	Kubernetes manifests were written:
	•	deployment.yaml → Deploys the application pods
	•	service.yaml → Exposes the application using a LoadBalancer
	•	The application is accessible publicly using the LoadBalancer DNS provided by AWS


CI/CD Process 

The CI/CD process followed in this project:
	1.	Code is pushed to GitHub
	2.	AWS CodeBuild pulls the code
	3.	Docker image is built
	4.	Image is pushed to AWS ECR
	5.	Application is deployed to EKS using Kubernetes manifests

Instead of using CodeDeploy (had account issues), deployment is done using a custom script approach, which is allowed as per the project requirements.


CodeBuild:
	•	Pulls code from GitHub
	•	Builds Docker image
	•	Pushes image to ECR
	•	Deploys the application to EKS using kubectl



Monitoring and Logs
	•	AWS CloudWatch Logs is used to view:
	•	CodeBuild build logs
	•	Docker image build and push logs
	•	Application logs can be checked using Kubernetes pod logs



Application Access

The application is deployed on Kubernetes using a Service of type LoadBalancer.

Kubernetes automatically created an AWS Classic Load Balancer for external access.

Application URL:
http://a8ee9728b82484316836e2d1dc5c3d59-1547154432.ap-south-1.elb.amazonaws.com

Kubernetes LoadBalancer ARN:
arn:aws:elasticloadbalancing:ap-south-1:731493185938:loadbalancer/a8ee9728b82484316836e2d1dc5c3d59

