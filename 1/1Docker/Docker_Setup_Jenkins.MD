# Project - with Docker

## Install Docker

1. Install docker and start docker services
   ```sh 
   yum install docker -y
   docker --version 
   
   # start docker services
   service docker start
   service docker status
   ```
1. Validation test, create a tomcat docker container by pulling a docker image from docker hub/registry
   ```sh
   docker pull httpd
   docker images
   docker run -d --name docker-apache -p 80:80 -d httpd
   docker ps
   docker exec -it docker-apache /bin/bash
   ```
## Docker file to create a contianer 
1. DockerFile
   ```sh
      # Pull tomcat latest image from dockerhub 
      From tomcat:latest
      # change folder path 
      RUN cp -R /usr/local/webapps.dist/* /usr/local/tomcat/webapps
      # copy war file on to container 
      COPY ./*.war /usr/local/tomcat/webapps

2. Cmds to create a Container
   ```sh
      docker build -t demotomcat .
      docker images
      docker run -d --name demotomcat-container -p 8085:8080 demotomcat

## Create a dedicated user
1. Create a user called dockeradmin
   ```sh
   useradd dockeradmin
   passwd dockeradmin
   id dockeradmin
   usermod -aG docker dockeradmin #manage docker by adding to docker group
   ```
1. By default EC2 instance doesnt allow password basesd authentication 
   ```
   vi /etc/ssh/sshd_config
      PasswordAuthenticaion yes
   service sshd reload 
   ```
## Setup Publish Over SSH and connection establish
   - `Manage Jenkins` > `Manage Plugins` > `Available` > `Publish over SSH`
   - `Manage Jenkins` > `Configure System` > `Publish Over SSH` > `SSH Servers` 
      - SSH Servers:
         - Name: `docker-host`
         - Hostname:`<ServerIP>`
         - username: `dockeradmin`         
         -  `Advanced` > chose `Use password authentication, or use a different key`
         - password: `*******`
         - Now click 'Test Connection'
## Settings for Jenkins Job in Post-build Actions
   - Under Build Settings select > `Send build artifacts over SSH`
       - SSH Server : `docker-host`
       - `Transfers` >  `Transfer set`
            - Source files: `webapp/target/*.war`
	       - Remove prefix: `webapp/target`
	       - Remote directory: `//home//dockeradmin` or `.`
	       - Exec command: 
                ```sh 
                cd /home/dockeradmin;
                docker build -t simple-devops-image .; 
                docker stop simple-devops-container;
                docker rm simple-devops-container;
                docker run -d --name simple-devops-container -p 8083:8080
                ```
## (X)
1. Use SSH
   ```sh
     vi /etc/ssh/sshd_config
     reload sshd service
     dockeradmin@server_ip
     scp root@172.31.86.169:/var/lib/jenkins/workspace/first\ maven/webapp/target/webapp.war /home/dockeradmin
   ```

1. DockerFile
   ```sh
      FROM centos
      RUN yum install java -y
      RUN mkdir /opt/tomcat/
      WORKDIR /opt/tomcat
      ADD https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.54/bin/apache-tomcat-9.0.54.tar.gz /opt/tomcat
      RUN tar xvfz apache*.tar.gz
      RUN mv apache-tomcat-9.0.54/* /opt/tomcat 
      EXPOSE 8080
      CMD ["/opt/tomcat/bin/catalina.sh", "run"]
   ```

   chown -R dockeradmin:dockeradmin /opt/docker