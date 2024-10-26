Objective: Deploy a basic web application using any platform or local server, using open-source tools and libraries.

INTRODUCTION:This project is a simple Java web calculator application that can perform basic arithmetic operations. This README outlines the steps to deploy the application on an AWS EC2 instance.

Prerequisites
Before you begin, ensure you have the following:
1.Any aws account

2.Java Development Kit (JDK) installed locally in the server(supports java based applications)

3.Apache Maven installed locally (for building the project)

Deployment Steps:
1. Launch an EC2 Instance
Log in to your AWS Management Console.
Navigate to the EC2 dashboard and click on "Launch Instance."
Choose an Amazon Machine Image (AMI). (e.g., Amazon Linux, Ubuntu Server)
Select an instance type (e.g., t2.micro for free tier).
Configure security group settings to allow inbound traffic on port 80 (HTTP).
Launch the instance and download the key pair for SSH access.

