# DevOps Project CI/CD
 
1. Project - an hello world code to be build with java
1. Project - with Jenkins to publish over container to host server
1. Project - with Docker 
1. Project - with Ansible
1. Project - with Kubernetes
1. Project - Build jenkins jobs for
    - java using tomcat
    - .net using .netCore SDK
    - to serve a angular application
    - create a DB

## Project - an hello world code to be build with java via jenkins    
  - Install git `yum install git -y`  
  - Install Jenkins, choose redhat: https://pkg.jenkins.io/redhat-stable/
  - Install Maven, choose bin : https://maven.apache.org/install.html    
  - Configure Java and maven:
      ```
          > find / -name jvm
          > cd /usr/lib/jvm
          > ls
          > find / -name java-11*
          > vi ~/.bash_profile
              M2_HOME=/opt/maven
              M2=/opt/maven/bin
              JAVA_HOME=java-11-openjdk-11.0.13.0.8-1.amzn2.0.3.x86_64
              PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2_HOME:$M2
      ```
  - Under ManagePlugin, install the below mentioned plugins
      - GitHub | Maven Integration | Deploy to container | Publish over SSH
  - Under Global Tool Configuration> set folder path of java, git, maven
  - Create build job for java app, required command `clean package` or `clean install` 
  - **Verify** the workspace and check webapp.war under target folder> `cd /var/lib/jenkins/workspace`
  * (X) Java : https://thenucleargeeks.com/2019/12/12/install-java-on-aws-ec2-instance/
  * (X) Jenkins:  https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/ 

## Project - with Jenkins to publish over container to tomcat host server
  - Install java from amazon-extras-linux, `amazon-linux-extras install java-openjdk11 -y`
  - Install tomcat server, choose core : https://tomcat.apache.org/download-90.cgi
  - To allow public access change and user login under conf> 
      - files of host-manager dir | manger dir `find / -name context.xml`,  comment out > allow 127 section
      - tomcat-users.xml file, add manager-gui and manager-script roler and admin user
  - Now under bin dir do> `./shutdown.sh and ./startup.sh`
  - In jenkins under Manage Credential > Jenkins > Global credentials > Add Credentials of **admin** which we mentioned in tomcat-sers.xml
  - In jenkins create a new build job under post build action choose> **Deploy war/ear to a container** and provide the tomcat instance ip url.
  - **Verify** in tomcat instance for webapp.war file, under /opt/tomcat/webapps. Now open the url to check java app.
  - (X) https://devops4solutions.com/installation-of-tomcat-on-aws-ec2-linux-integration-with-jenkins/

## Project - with Docker  
  - https://forums.docker.com/t/tomcat-give-error-404/95130/2
6.	
























<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>






Format:
# Create a First Maven Jenkins job to build hello-world project 
# *Jenkins Job name:* `My_First_Maven_Build`

We know how to use work with each and Git, Jenkins independently. What if you want to collaborate these two? that is where Simple DevOps project helps you. Follow the below steps if you are a new guy to DevOps. You love it. 


#### Pre-requisites

1. Jenkins server 


### Steps to create "My_First_Maven_Build" Jenkin job
1. Login to Jenkins console
1. Create *Jenkins job*, Fill the following details,
   - *Source Code Management:*
      - Repository: `https://github.com/yankils/hello-world.git`
      - Branches to build : `*/master`  
   - *Build:*
     - Root POM:`pom.xml`
     - Goals and options: `clean install package`