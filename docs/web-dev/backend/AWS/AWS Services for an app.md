[AWS In Plain English](https://expeditedsecurity.com/aws-in-plain-english/)

[notes/AWSArch.drawio](https://github.com/Fullchee/notes/blob/main/docs/web-dev/backend/AWS/AWSArch.drawio)

![[AWSArch.drawio.png]]



Cloudfront (CDN)
- has resources like favicons

Elastic Load Balancer

AWS Batch
- weekly database backups

AWS Batch vs AWS Lambda
- lambda has a 15 minute limit
- lambda is more performant????

AWS EventBridge
- trigger an Batch or Lambda job

### Route 53
- DNS

## [[AWS S3]]

## EC2

-   virtual machine

### EC2 vs LightSail

-   Lightsail is like Digital Ocean's $5/month
-   EC2 can have more bad-ass servers
	- these servers are more temporary

## ECS

-   basically a lightweight Kubernetes?
    -   where you manage some EC2 instances

## Fargate

-   level of abstraction that's higher than ECS
-   idea of `tasks` which could be a group of EC2 instances

## WAF

-   Web Application Firewall
	- protects all AWS services
	- not just the frontend
- we used to use Sqreen
	- got bought by Datadog
	- they jacked up the price

## Kinetic

-   like Apache Kafka
-   for streaming content like logs or videos
    -   example: sending logs to DataDog


## Bastion Host

- Machine in the Virtual Private Cloud (VPC)
- always running
	- unlike EC2 instances
- lets you port forward or ssh into EC2 instances easily


## AWS ECS

### ECS vs Kubernetes

- ECS is like simple Kubernetes for EC2 only clusters  
- ECS orchestrates docker containers on EC2 clusters  
- ECS manages a lot for you so it's simpler than Kubernetes  
- Kubernetes is portable
	- if you want to move to Azure, GCP

### AWS Fargate vs AWS ECS

ECS manages EC2 instances  
  
Fargate is a level of abstraction higher  
  
You manage tasks (2+ containers working together like backend and frontend container)   
  
Containers in the same task can communicate with each other via localhost


AWS Elasticache is used to host Redis

AWS Code Artifacts for databricks????



## AWS CloudWatch

![[image-20221130181035190.png]]

