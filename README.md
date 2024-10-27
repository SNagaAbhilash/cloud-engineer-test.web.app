Objective: Deploy a basic web application using any platform or local server, using open-source tools and libraries.
--------------------------------------------------------------------------------------------------------------------------------
INTRODUCTION:
--------------------------------------------------------------------------------------------------------------------------------
This project is a simple Java web calculator application that can perform basic arithmetic operations.This README outlines the steps to deploy the application on an AWS EC2 instance.

Prerequisites
--------------------------------------------------------------------------------------------------------------------------------
Before you begin, ensure you have the following:

1.Aws account: sign up at aws account

2.Java Development Kit (JDK)(supports java based applications version 8 or higher)

3.Apache Maven installed locally (for building the JAVA languages)

4.Git (For cloning the repository).

Deployment Steps:
--------------------------------------------------------------------------------------------------------------------------------
1.LAUNCH AN EC2 INSTANCE
   
2.Log in to your AWS Management Console.

3.Navigate to the EC2 dashboard and click on "Launch Instance."

4.Choose an Amazon Machine Image (AMI). (e.g., Amazon Linux)

5.Select an instance type (e.g., t2.micro for free tier).

6.create vpc or you can use default vpc and subnets

7.Configure security group:
   Add a rule to allow SSH (port 22) from your IP.
   Add a rule to allow traffic on the port your application will run (e.g., port 8080 for tomcat).

8.Review and launch the instance.

9.Download the key pair (e.g., my-key.pem) when prompted.




2.CONNECT TO EC2 INSTANCE:
--------------------------------------------------------------------------------------------------------------------------------
open your instance and connect using SSH client:
                    
       ssh -i "web.pem" ec2-user@ec2-3-27-90-92.ap-southeast-2.compute.amazonaws.com


3.INSTALL JAVA,MAVEN AND GIT in your AWS EC2 INSTANCE:
-------------------------------------------------------------------------------------------------------------------------------
1.Install java by giving:- 

          sudo yum -y install java-11*

  check java version:

          java -version

2.Install maven (to build the java based applications we need pom.xml file which is present in java based applications, acts as meta data and by builiding the applications it provides artifacts WAR(deployment purpose,JAR(testing purpose) file):-

         sudo yum -y install maven

to check maven version:

           mvn -v

3.Install git (To clone pre-existing application or to use git based commands in the instance):

        -> sudo yum -y install git

        -> "git clone https://github.com/username/yourrepository.git"


4.CHANGE THE DIRECTORY TO BUILD THE MAVEN LIFE CYCLE:
-------------------------------------------------------------------------------------------------------------------------------
a. To change the directory:-

            cd simplewebcalculator(directory name)

   beacuse it contains pom.xml.without pom.xml we cant build using maven.


5.BUILD THE APPLICATION USING THE MAVEN LIFE CYCLE:
-------------------------------------------------------------------------------------------------------------------------------
a. mvn validate- it will validate the the language is compatable to build with maven or not

b.mvn compile- it will convert human readable to machine readable 

c.mvn test-to check if the application is converted to machine readable

d.mvn package- it will build the application and convert into WAR or JAR file.

note: 

      1.the errors we get while building the application is plugins and versions hence we have to update the plugins and versions

      2.after building the application it will create a directory called "target" inside it will create WAR OR JAR FILE.

6.INSTALL APACHE TOMCAT TO DEPLOY OR HOST JAVA BASED APPLICATIONS:
------------------------------------------------------------------------------------------------------------------------------------
a.to install tomcat from google to the ec2 instance use :-
       
       wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.96/bin/apache-tomcat-9.0.96.tar.gz  (tomcat 9 version)

b.after installing the tomcat we have to unzip the tar file so use:- 

         tar -xvf  apache-tomcat-9.0.96.tar.gz


7.START THE TOMCAT SERVER:
---------------------------------------------------------------------------------------------------------------------------------------
Go to the tomcat in the tomcat we have lot of files and folders

change to the bin folder by giving :
    
            cd bin/

in bin folder we have lot of configuration files so start or run the configuration file we use:- 
          
          ./startup.sh

8.Configure security group settings to allow inbound traffic on port 8080(tomcat port number).
----------------------------------------------------------------------------------------------
1.we are using public ip adress of the instance to open the tomcat page:- 

            https://3.27.90.92:8080

2.Ater giving ip address we can see the tomcat page in that we have to go to the manager app as it is a web application that is packaged with tomcat server in that only we can see all the
  
applications that we are deployed

3.Ensure the necessary configurations are set in your application

4.Modify context.xml available in managers in Tomcat to deploy application, you need to change the default settings 

5.edit the manager and host manager to deploy or host java based application(give permissions):-

            sudo vi /home/ec2-user/apache-tomcat-9.0.96/webapps/host-manager/META-INF/context.xml

            sudo vi /home/ec2-user/apache-tomcat-9.0.96/webapps/manager/META-INF/context.xml

6.after giving permsions go to the bin folder and restart the configuration file.

7.by opening the tomcat server we have to edit conf/tomcat-users.xml and give credentials to use webapp(it is a deployment directory for tomcat) 
 
  so go to the user conf folder and edit tomcat-users.xml :-

             sudo vi tomcat-users.xml

  in that give single user permsisions to enter into the tomcat phase:-

                    <role rolename="manager-gui"/>
           <user username="tomcat" password="abhilash" roles="manager-gui"/>

  so by changing these we can enter into the tomcat web application manager dashboard by giving username and passwords which we have given in the tomcat-users.xml


9.DEPLOY THE APPLICATION:
-------------------------------------------------------------------------------------------------------------------------------------------------
1.The deployment directory of tomcat is webapps so we have to deploy or move the war file in the webapps,so to run the java based application go to the target dir.

2.in the target dir which is present in tomcat we have to deploy or move the WAR file to the webapps by giving:

       sudo cp -r  WebCalculator-1.0-SNAPSHOT.war /home/ec2-user//apache-tomcat-9.0.96/webapps

3.Again restart the configuration file (./startup.sh) in the bin folder in tomcat we can get the application that has been deployed in the dashboard.


10.USING ELASTIC IP TO THE INSTANCE TO RUN 24/7:
-------------------------------------------------------------------------------------------------------------------------------------------------
Step 1: Allocate an Elastic IP Address
Log in to the AWS Management Console:

Go to AWS Management Console.
Navigate to the EC2 Dashboard:

Click on Services in the top menu.
Under the Compute section, select EC2.
Access Elastic IPs:

In the left sidebar, find the Network & Security section and click on Elastic IPs. 
Allocate a New Elastic IP:
Click the Allocate Elastic IP address button.

Step 2: Associate the Elastic IP with Your Tomcat Instance
Select the Elastic IP:
In the Elastic IPs section, find the Elastic IP you just allocated.
Associate the Elastic IP:
Select the Elastic IP address and click on the Actions button.
Choose Associate Elastic IP address from the dropdown menu.
Select Your Instance:

In the association dialog, select your running Tomcat instance from the drop-down menu.
If your instance has multiple network interfaces, you may need to specify the private IP address (usually the default is fine).
Confirm the Association:

Click Associate to link the Elastic IP to your instance.
Step 3: Configure Security Group
To allow traffic to your Tomcat application, ensure your instance's security group is configured properly.

Access Security Groups:

In the EC2 Dashboard, click on Security Groups in the left sidebar.
Select the Appropriate Security Group:

Find and select the security group associated with your Tomcat instance.
Edit Inbound Rules:

Click on the Inbound rules tab and then click Edit inbound rules.
Add a rule to allow traffic:
Type: Custom TCP Rule
Protocol: TCP
Port Range: 8080 (or the port your Tomcat server is running on, typically 8080)
Source: Anywhere (0.0.0.0/0) for public access, or restrict to a specific IP range as needed.
Click Save rules.
Step 4: Access Your Web Application
Open a Web Browser:

In your web browser, enter the Elastic IP address followed by the Tomcat port (e.g., http://<your-elastic-ip>:8080).
View Your Application:

If everything is set up correctly, you should see your Tomcat web application.
Conclusion
By following these steps, you have successfully allocated an Elastic IP address and associated it with your Tomcat instance, making your web application publicly accessible. Share the Elastic IP address with users who need access to your application.

           















