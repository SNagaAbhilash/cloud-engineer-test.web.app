Objective: Deploy a basic web application using any platform or local server, using open-source tools and libraries.

INTRODUCTION:This project is a simple Java web calculator application that can perform basic arithmetic operations. This README outlines the steps to deploy the application on an AWS EC2 instance.

Prerequisites
Before you begin, ensure you have the following:

1.Any aws account

2.Java Development Kit (JDK) installed locally in the server(supports java based applications)

3.Apache Maven installed locally (for building the project)

Deployment Steps:

1.LAUNCH AN EC2 INSTANCE
   
a.Log in to your AWS Management Console.

b.Navigate to the EC2 dashboard and click on "Launch Instance."

c.Choose an Amazon Machine Image (AMI). (e.g., Amazon Linux, Ubuntu Server)

d.Select an instance type (e.g., t2.micro for free tier).

e.Configure security group settings to allow inbound traffic on port 80 (HTTP).

f.Launch the instance and download the key pair for SSH access.


2.CONNECT TO EC2 INSTANCE:

open your instance and connect using SSH client: ssh -i "web.pem" ec2-user@ec2-3-27-90-92.ap-southeast-2.compute.amazonaws.com


3.INSTALL JAVA,MAVEN AND GIT:

a.sudo yum -y install java-11* (supports java based applications)

b.sudo yum -y install maven  (to build the java based applications we need pom.xml file which is present in java based applications only acts as meta data and by builiding the applications it provides artifacts WAR(deployment purpose,JAR(testing purpose) file)

c.sudo yum - y install git (to clone pre -existing application- "git clone https://github.com/username/your repository.git")


4.GO THE DIRECTORY:

a. cd directoryname


5.BUILD THE APPLICATION USING THE MAVEN LIFE CYCLE:

a. mvn validate- it will validate the web application if pom.xml is present or not

b.mvn compile- it will convert human readable to machine readable 

c.mvn test-to check if the application is converted to machine readable

d.mvn package- it will build the application and convert into WAR or JAR file










