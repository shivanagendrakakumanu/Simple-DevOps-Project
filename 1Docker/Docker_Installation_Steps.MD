# Installing Docker on Amazon Linux server

### Pre-requisites
1. Amazon Linux EC2 Instance

## Installation Steps

1. Install docker and start docker services
   ```sh 
   yum install docker -y
   docker --version 
   
   # start docker services
   service docker start
   service docker status
   ```
1. Create a user called dockeradmin
   ```sh
   useradd dockeradmin
   passwd dockeradmin
   id dockeradmin
   ```
1. add a user to docker group to manage docker 
   ```
   usermod -aG docker dockeradmin
   ```
### Validation test
1. Create a tomcat docker container by pulling a docker image from the public docker registry
   ```sh
   docker pull tomcat
   docker images
   docker run -d --name tomcat-contianer -p 8090:8080 tomcat:latest
   docker exec -it tomcat-contianer /bin/bash
   ```

## Docker to jenkins 

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