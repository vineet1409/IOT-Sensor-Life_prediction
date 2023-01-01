# Smart Building Automation (Sensor-fault-Detection)
As part of the smart building automation, Zigbee-based end-devices such as THL (temperature, humidity, and light) sensors are used to automatically adjust room temperature or light based on their readings. These sensors were, however, subjected to battery drain, and hence their lifecycle was compromised. 

The task was to create an end-to-end ML pipeline with cloud deployment to predict the sensor’s lifecycle (whether endangered or working normally), thereby reducing the cost of frequent setup and installation in buildings


## Architecture
![Architecture](/Images/Architecture.jpg)



## ML Pipeline High Level Overview

![ML_Training_Pipeline](/Images/ML_Training_Pipeline.png)

### Data Ingestion
![data_ingestion](/Images/data_ingestion.png)

### Data Validation
![data_validation](/Images/data_validation.png)

### Data Tranformation
![data_transformation](/Images/data_transformation.png)

### Model Trainer
![model_trainer](/Images/model_trainer.png)

### Model Evaluation
![model_evaluation](/Images/model_evaluation.png)

### Model Prediction
![model_prediction](/Images/model_prediction.png)

### Model Pusher
![model_pusher](/Images/model_pusher.png)


## CI/CD Pipeline using GitHub Action for deployment on AWS EC2
1. Login to AWS console.

2. Create IAM user for deployment

	with specific access
	1. EC2 access : It is virtual machine

	2. S3 bucket: To store artifact and model in s3 bucket

	3. ECR: Elastic Container registry
	To save your docker image in aws

	Description: About the deployment

	1. Build docker image of the source code
	2. Push your docker image to ECR
	3. Launch Your EC2 
	4. Pull Your image from ECR in EC2
	5. Lauch your docker image in EC2



	Policy:
	1. AmazonEC2ContainerRegistryFullAccess
	2. AmazonEC2FullAccess
	3. AmazonS3FullAccess

3.Create a s3 bukcet in ap-south-1
	bucket name: scania-sensor-pipeline
	
4. ECR repo to store/save docker image
	566373416292.dkr.ecr.ap-south-1.amazonaws.com/sensor-fault
	
5. EC2 machine  Ubuntu  Created

6. Open EC2 and Install docker in EC2 Machine 
	
	
	#optinal
	sudo apt-get update -y
	sudo apt-get upgrade
	
	#required
	curl -fsSL https://get.docker.com -o get-docker.sh
	sudo sh get-docker.sh
	sudo usermod -aG docker ubuntu
	newgrp docker
	
7. Configure EC2 as self-hosted runner

setting>actions>runner>new self hosted runner> choose os> 
then run command one by one

8. Setup github secrets

AWS_ACCESS_KEY_ID=

AWS_SECRET_ACCESS_KEY=

AWS_REGION=ap-south-1

AWS_ECR_LOGIN_URI=566373416292.dkr.ecr.ap-south-1.amazonaws.com

ECR_REPOSITORY_NAME=sensor-fault

MONGO_DB_URL=




## Results
The entire pipeline developed helped to reduce the burden of frequent setup. The installation costs went down by almost 30%