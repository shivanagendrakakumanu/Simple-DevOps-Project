# Setup Kubernetes on Amazon EKS

You can follow same procedure in the official  AWS document [Getting started with Amazon EKS – eksctl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)   

#### Pre-requisites: 
  - an EC2 Instance
  - [Install AWS CLI latest verison](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
  - **kubectl** CLI allows you to run commands against Kubernetes clusters. Use kubectl for working with kubernetes cluster to deploy applications, inspect and manage cluster resources, view logs.
  - **eksctl** CLI allows to create and manage k8s clusters on AWS EKS, Amazon will take responsibility for managing your Kubernetes Master Nodes. It uses AWS SDK and CloudFormation service,to create a EKS cluster in minutes with just one command.

1. Setup AWS   
   a. Download latest AWS cli    
   b. Unizip and install   
   c. to check version use :``` aws --version```
   ```sh
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   unzip awscliv2.zip
   sudo ./aws/install
   ```

1. Setup kubectl   
   a. Download kubectl version 1.21  
   b. Grant execution permissions to kubectl executable   
   c. Move kubectl onto /usr/local/bin   
   d. Test that your kubectl installation was successful    

   ```sh 
   curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl
   chmod +x ./kubectl
   mv ./kubectl /usr/local/bin 
   kubectl version --short --client
   ```

1. Setup eksctl   
   a. Download and extract the latest release   
   b. Move the extracted binary to /usr/local/bin   
   c. Test that your eksclt installation was successful   

   ```sh
   curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
   sudo mv /tmp/eksctl /usr/local/bin
   eksctl version
   ```
  
1. IAM user should have access to *IAM + EC2 + CloudFormation*    
   a. Create an IAM Role with full access    
   b. Attach it to EC2 instance  
   Note: Check eksctl documentaiton for [Minimum IAM policies](https://eksctl.io/usage/minimum-iam-policies/)
   
1. [Create your cluster and nodes](https://docs.aws.amazon.com/eks/latest/userguide/create-cluster.html)
   ```sh
   eksctl create cluster --name cluster-name  \
   --region region-name \
   --node-type instance-type \
   --nodes-min 2 \
   --nodes-max 2 \ 
   --zones <AZ-1>,<AZ-2>
    ```
   Create a cluster with two default nodes(ec2)
   ```sh
   eksctl create cluster --name shiva-cluster \
      --region us-east-1 \
      --node-type t2.small \

   kubectl get all # list all resources with different types.
   kubectl get nodes # gives nodes status (add '-o wide' to get more details)
   kubectl describe nodes # will show detail information of the nodes in the cluster

   eksctl delete cluster shiva-cluster --region us-east-1 # to delete the EKS clsuter 
   ```

1. Validate your cluster by creating by checking nodes and by creating a pod 
   ```sh 
   kubectl run webapp --image=httpd # Create and run a httpd image in a pod.
   kubectl get pods # gives pod status (add '-o wide' to get specific details)
   kubectl describe pod name_of_the_pod | grep -i image # state of a pods
   kubectl delete pod webapp # Delete the webapp Pod
   kubectl edit pods webapp # change the image on this pod to redis
   ```

1. Deploying Nginx Container  
   a. First create a deployment in which we will create two replicas(pods) to make sure it is available all the time.   
   b. To access application publicly create a servive by using `expose` cmd.  
   c. Through the service we can access and this will create an ELB in front of those 2 containers    
    ```sh
      kubectl create deployment  demo-nginx --image=nginx --replicas=2 --port=80
      kubectl expose deployment demo-ngnix --port=80 --type=LoadBalancer

      kubectl get deployment # gives list of deployments
      kubectl get replicaset # gives number of replicaset
      kubectl get pod
      kubectl get all
      
      kubectl expose deployment demo-nginx --port=80 --type=LoadBalancer
      # kubectl expose deployment regapp --port=8080 --type=LoadBalancer
      kubectl get services -o wide
      kubectl get all

      kubectl delete pod demo-nginx
      kubectl delete deployment demo-nginx
      kubectl delete service/demo-nginx
   ```

1. We should use manifest files whenever create kube containers   
   a. We should have seperate pod file(like demo1pod.yml)   
   b. We should have sepeate service file(like demo1service.yml)  
   c. Make sure labels in pod and selector in service are matching this how serivce knows to which pod it has to connect from a user(outside world)
   ```sh
   kubectl apply -f demo1pod.yml
   kubectl apply -f demo1service.yml
   
   kubectl describe service/demo-service
   ```

1.