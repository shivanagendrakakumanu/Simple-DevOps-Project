# Project - with Ansible   
## In Docker instance
1. Create a user called ansadmin
   ```sh
   useradd ansadmin
   passwd ansadmin
   id dockeradmin
   sudo su -ansadmin
   ```
1. Provide root pivileges
   ```sh
   visudo
      ansadmin ALL=(ALL) NOPASSWD: ALL
   ```
1. By default EC2 instance doesnt allow password basesd authentication 
   ```
   vi /etc/ssh/sshd_config
      PasswordAuthenticaion yes
   service sshd reload 
   ```
# In Ansible instance
1. Create a user called ansadmin
   ```sh
   useradd ansadmin
   passwd ansadmin
   id dockeradmin
   sudo su -ansadmin
   ```
1. Provide root pivileges
   ```sh
   visudo
      ansadmin ALL=(ALL) NOPASSWD: ALL
   ```
1. By default EC2 instance doesnt allow password basesd authentication 
   ```sh
   vi /etc/ssh/sshd_config
      PasswordAuthenticaion yes
   service sshd reload 
   ```
1. Keyless SSH for ansadmin
   ```sh
   pwd #we should be in ansadmin dir
   ssh-keygen
   ls -a
   cd ./ssh
   ssh-copy-id anasdmin@docker_instance_ip_of_ansdmin
   ssh ansadmin@docker_instance_ip_of_ansdmin #w/o pwd it will login
   ```
## Setup Ansible
1. Install Ansible
   ```sh 
   amazon-linux-extras install ansible2
   python --version  #by default amazon OS will have python
   ansible --version
   ```
1. In inventory file add docker instance ip
   ```sh
   sudo vi etc/ansible/hosts
      docker_instance_ip_of_ansdmin
   ```
1. Validation test from ansible to docker
   ```sh
   ansible all -m ping #we should get succeful message
   ansible all -m command -a uptime
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
## Setup docker in ansible server
   - Follow the steps from docker dir
   - Dockerhub
      ```
         docker login
         docker push tomcat-login:latest
         docker images
         docker tag X new-repo:tagname # in place of X > local-image:tagname or imageId
         docker push new-repo:tagname
      ```
## Ansible playbooks and to push into docker hub
   - ansible-playbook ansible_push_hub.yml --check
   ```sh
      ---
      - hosts: ansiblehostip

      tasks:
      - name: create docker image
         command: docker build -t regapp:latest .
         args:
          chdir: /opt/docker

      - name: create tag to push image onto dockerhub
         command: docker tag regapp:latest valaxy/regapp:latest

      - name: push docker image
      command: docker push valaxy/regapp:latest      
   ```

   - ansible-playbook ansible_deploy_docker.yml --check
   ```sh
      ---
      - hosts: dockerhostip

      tasks:
      - name: stop if we have old docker container
       command: docker stop regapp-server
       ignore_errors: yes
      
      - name: remove stopped docker container
       command: docker rm regapp-server
       ignore_errors: yes
      
      - name: remove image
       command: docker rmi valaxy/regapp:latest
       ignore_errors: yes

      - name: create container
       command: docker run -d --name regapp-server -p 80802:8080 valaxy/regapp:latest
   ```

   ```sh
      # Option-2 : creating docker image using docker_image module 
      ---
      - hosts: all
        tasks:
         - name: building docker image
           docker_image:
            build:
              path: /opt/docker
              name: simple-devops-image
              tag: v1
              source: build
         
      # Option-2 : creating docker container using docker_container module 	
      ---
      - hosts: all
        tasks:
        - name: create simple-devops-container
          docker_container:
            name: simple-devops-container
            image: simple-devops-image
            state: present
            recreate: yes
            ports:
              - "8080:8080"
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

sudo chmod 777 /var/run/docker.sock
add ansible ip to hosts files
ansible all -a uptime
ansible -i hosts all -a uptime
ssh-copy-id localhost #during ansible to perform

```
   ---
   - hosts: all
   become: true
   tasks:
   - name: stop if we have old docker container
      command: docker stop simple-devops-container
      ignore_errors: yes

   - name: remove stopped docker container
      command: docker rm simple-devops-container
      ignore_errors: yes

   - name: remove current docker image
      command: docker rmi simple-devops-image
      ignore_errors: yes
   #    register: result
   #    failed_when:
   #      - result.rc == 0
   #      - '"docker" not in result.stdout'


   - name: building docker image
      command: docker build -t simple-devops-image .
      args:
         chdir: /opt/docker

   - name: creating docker image
      command: docker run -d --name simple-devops-container -p 8080:8080 simple-devops-image
```