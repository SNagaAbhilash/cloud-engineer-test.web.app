Objective: Deploy a basic web application using any platform or local server, using open-source tools and libraries.
--------------------------------------------------------------------------------------------------------------------------------
INTRODUCTION:
--------------------------------------------------------------------------------------------------------------------------------
This project is a simple Java web calculator application that can perform basic arithmetic operations. This README outlines the steps to deploy the application on an AWS EC2 instance.

Prerequisites
--------------------------------------------------------------------------------------------------------------------------------
Before you begin, ensure you have the following:

1.Any aws account

2.Java Development Kit (JDK) installed locally in the server(supports java based applications)

3.Apache Maven installed locally (for building the project)

Deployment Steps:
--------------------------------------------------------------------------------------------------------------------------------
1.LAUNCH AN EC2 INSTANCE
   
2.Log in to your AWS Management Console.

3.Navigate to the EC2 dashboard and click on "Launch Instance."

4.Choose an Amazon Machine Image (AMI). (e.g., Amazon Linux)

5.Select an instance type (e.g., t2.micro for free tier).

6.Configure security group:
   Add a rule to allow SSH (port 22) from your IP.
   Add a rule to allow traffic on the port your application will run (e.g., port 8080).

7.Review and launch the instance.

8.Download the key pair (e.g., my-key.pem) when prompted.




2.CONNECT TO EC2 INSTANCE:
--------------------------------------------------------------------------------------------------------------------------------
open your instance and connect using SSH client:
                    
       ssh -i "web.pem" ec2-user@ec2-3-27-90-92.ap-southeast-2.compute.amazonaws.com


3.INSTALL JAVA,MAVEN AND GIT in your AWS EC2 INSTANCE:
-------------------------------------------------------------------------------------------------------------------------------
1.Install java by giving:- 

          sudo yum -y install java-11*

  check java version:

          java --version

2.install maven (to build the java based applications we need pom.xml file which is present in java based applications only acts as meta data and by builiding the applications it provides artifacts WAR(deployment purpose,JAR(testing purpose) file):-

         sudo yum -y install maven

to check maven version:

           mvn -v

3.install git and clone pre -existing application or to use git based commands in the instance):

         sudo yum -y install git

         "git clone https://github.com/username/yourrepository.git"


4.CHANGE THE DIRECTORY TO BUILD THE MAVEN LIFE CYCLE:
-------------------------------------------------------------------------------------------------------------------------------
a. change the directory:-

            cd simple web calculator


5.BUILD THE APPLICATION USING THE MAVEN LIFE CYCLE:
-------------------------------------------------------------------------------------------------------------------------------
a. mvn validate- it will validate the the language is compatable to build with maven or not

b.mvn compile- it will convert human readable to machine readable 

c.mvn test-to check if the application is converted to machine readable

d.mvn package- it will build the application and convert into WAR or JAR file.

note: 

      1.the errors we get while building the application is plugins and versions hence we have to update the plugins and versions

      2.after building the application it will create a directory called "target" inside ot will create WAR OR JAR FILE.

6.INSTALL APACHE TOMCAT TO DEPLOY OR HOST JAVA BASED APPLICATIONS:
------------------------------------------------------------------------------------------------------------------------------------
a.to install tomcat to the ec2 instance use :-
       
       wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.96/bin/apache-tomcat-9.0.96.tar.gz  (tomcat 9 version)

b.after installing the tomcat we have to unzip the file so use:- 

         tar -xvf  apache-tomcat-9.0.96.tar.gz


7.START THE TOMCAT SERVER:
---------------------------------------------------------------------------------------------------------------------------------------
go to the tomcat in the tomcat we have lot of files and floders

change to the bin folder by giving :
    
            cd bin/

in bin folder we have lot of configuration files so start the server by giving the command:- 
          
          ./startup.sh

Configure security group settings to allow inbound traffic on port 8080(tomcat port number) (HTTP).
----------------------------------------------------------------------------------------------
note:use public ip adress of the instance to open the tomcat page:- 

            https://3.27.90.92:8080


8.Configuration:
--------------------------------------------------------------------------------------------------------------------------
a.Ensure the necessary configurations are set in your application

b.Modify context.xml in Tomcat if you need to change the default settings 

c.edit the manager and host manager to deploy or host java based application(give permissions):-

            sudo vi /home/ec2-user/apache-tomcat-9.0.96/webapps/host-manager/META-INF/context.xml

            sudo vi /home/ec2-user/apache-tomcat-9.0.96/webapps/manager/META-INF/context.xml

d.after giving permsions go to the bin folder and restart the tomcat server.

e.by opening the tomcat server we have to edit conf/tomcat-users.xml and give user permissions 
 
  so go to the user conf folder and edit tomcat-users.xml :-

             sudo vi tomcat-users.xml

  in that give single user permsisions to enter into the tomcat phase:-

                    <role rolename="manager-gui"/>
           <user username="tomcat" password="abhilash" roles="manager-gui"/>

  so by changing these we can enter into the tomcat application manager dashboard by giving username and passwords


9.DEPLOY THE APPLICATION:
-------------------------------------------------------------------------------------------------------------------------------------------------
1.The deployment directory of tomcat is webapps so we have to deploy or move the war file in the webapps to run the java based application go to the target dir.

2.in the target we have to deploy or move the WAR file to the webapps by giving:

       sudo cp -r  WebCalculator-1.0-SNAPSHOT.war /home/ec2-user//apache-tomcat-9.0.96/webapps

3.again restart the server we can get the application in the dashboard.


           















