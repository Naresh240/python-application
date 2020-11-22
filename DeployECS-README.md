# Deploy Python Application using ECS
# Pre-Requisites
    - Git
    - Docker
# Provide "aws configure"
# Create ECR repo using below command
    aws ecr create-repository --repository-name python-ecs
# ECR Login
    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 901129798636.dkr.ecr.us-east-1.amazonaws.com
# Build docker image
    docker build -t python-ecs .
# Docker tag
    docker tag python-ecs:latest 901129798636.dkr.ecr.us-east-1.amazonaws.com/python-ecs:latest
# Docker push
    docker push 901129798636.dkr.ecr.us-east-1.amazonaws.com/python-ecs:latest
# ECS Fargate cluster
  Now let's create our tasks and services. Go to the ECS console. Click on "Get Started" which should be right in the middle of the page. If we already have clusters within ECS then it will be in grey next to "Create Cluster."
  
  ![image](https://user-images.githubusercontent.com/58024415/99899614-b7004500-2cd0-11eb-9de0-771adc1b7c70.png)

CLick on "Configure" and Provide as shown below

  ![image](https://user-images.githubusercontent.com/58024415/99899638-ed3dc480-2cd0-11eb-8211-a4ce3f3d2e02.png)
 
 Click on "update"
 
   ![image](https://user-images.githubusercontent.com/58024415/99899669-14949180-2cd1-11eb-9f88-f1f8186a793b.png)

Click on "Next"
Select "Application Load Balancer"

  ![image](https://user-images.githubusercontent.com/58024415/99899681-2d04ac00-2cd1-11eb-8e51-e1e05354f1b4.png)

Click on "Next"

  ![image](https://user-images.githubusercontent.com/58024415/99899699-51608880-2cd1-11eb-8426-98696685be0f.png)

Click on "Next" and then click on "Create"

  ![image](https://user-images.githubusercontent.com/58024415/99899761-de0b4680-2cd1-11eb-9234-d21cffc15458.png)

Click on "View Service"
  
  ![image](https://user-images.githubusercontent.com/58024415/99899786-009d5f80-2cd2-11eb-8cf9-bacc389b8a86.png)

Click on "Tasks"

  ![image](https://user-images.githubusercontent.com/58024415/99899795-17dc4d00-2cd2-11eb-88bc-72116ef6e127.png)

Check wether task status showing in Running or not. Once it came to running state, go to LoadBalancer and copy DNS name and check in UI
  http://ec2co-ecsel-741yddgo2qum-1160302159.us-east-1.elb.amazonaws.com:5000/

    ![image](https://user-images.githubusercontent.com/58024415/99899863-5bcf5200-2cd2-11eb-85a6-3ecd8e7e5702.png)

# Update service
  Configure service: we want to change the "Number of tasks" to 2:
  
  ![image](https://user-images.githubusercontent.com/58024415/99899955-eadc6a00-2cd2-11eb-8e1b-7c4739ad4113.png)

Set Number of tasks from 1 to 2

Configure network: leave it untouched.

  ![image](https://user-images.githubusercontent.com/58024415/99899994-54f50f00-2cd3-11eb-92d3-35b14cd2ab38.png)

Select Service Autoscaling as "Configure Service Auto Scaling to adjust your service’s desired count" and Click on "Add Autoscaling"

  ![image](https://user-images.githubusercontent.com/58024415/99900125-06944000-2cd4-11eb-8c0a-c141579932e0.png)

Click "Update Service". It should go through and give us green check marks on our updates. Now if we click on the "Tasks" tab in our service we should see 2. They may be spinning up and in a pending state but give it a few minutes.

  ![image](https://user-images.githubusercontent.com/58024415/99900153-34798480-2cd4-11eb-913a-bc03776e0241.png)

Then, we will see them all running.

  ![image](https://user-images.githubusercontent.com/58024415/99900215-5b37bb00-2cd4-11eb-92e7-ba801f3d8b84.png)

# Check Output:
  ![image](https://user-images.githubusercontent.com/58024415/99900232-6db1f480-2cd4-11eb-9cc3-7a8fc1c2829f.png)

# Clean up
    To clean up the resources we created, we can just delete the cluster.
