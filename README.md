# AWS EKS PROJECT

                   

1.This Project is about Deploying   nginx  web application application using using AWs kubernetes service.
AWS EKS- Aws eks is a service which is provided by Amazon Web Services for Kubernetes .This service is fully managed by AWS itself. The main        purpose of this service is to provide support for Deploying applications on internet.

In this service we can launch an a server and assaign Networks, Subnets ,and create Pods, assign security groups ,can attach multiple              loadbalancers depending upon application requirements.

 In this service we use tools like AWS cloud watch,Loadbalancers and so on .

2.WHY AWS EKS CLUSTER?
     Because now a days all the projects using this service because it provides services in such a  way that we can deploy,scale,rollout,and            can monitor our project/application very easily. How  ever there are other compitetors are there in the market for EKS service, these              are  different from person/ person or ganizations.

3.I prefer AWs Eks cluster because as a user i feel like it provides me with good user interface and godd services. Other EKS providers in              market are i) Google Kubernetes Engine (GKE)
                  ii) Microsoft Azure Kubernetes Service (AKS)
                 iii)  and Red Hat OpenShift.

 This is a project aimed to deploy my sample application using AWS EKS .


4.AWS EKS PROCESS:     
  1.Go to AWS Console--Select AWS EKS Service.--Click on Add Cluster--     create-- and Give name--select version--Cluster service role--(generally    cluster generally have  two roles 1.Master to manage 
                                  2.nodes. also called as workers).
                                  
![Screenshot (11)](https://user-images.githubusercontent.com/114085306/226707192-69ab60bd-b9ae-4a56-b1cc-1b3d49ad6546.png)

 Cluster require access to services like ECS, ECR,and others. so For that we create cluster service role.

5.After creating Eks cluster we need to create Node group and select it.

Node IAM role 
Create roles in that for IAM.
 Under use case choose EC2 and click next. 
give the fallowing permission for roles like 1.Amazon EKSWorker node policy.
                                             2.AmazonEC2ContainerRegistryReadOnly.
                                             3.Amazon EKS_CNI_policy

![Screenshot (27)](https://user-images.githubusercontent.com/114085306/226707347-176285b8-f19f-4cee-9e14-98bfc0571560.png)

 provide name and hit create a node and select node group policy under it.
 In nod egroup configurataion it asks about AMI type,Capacity type, Instance types, Disk sizes etc give all of them.

![Screenshot (29)](https://user-images.githubusercontent.com/114085306/226707566-62645e44-9714-49f7-9bec-55c6b61bff70.png)

6.In node group scaling configuration you can select Desired size,Minimum size,Maximum size of nodes.
 In network configuration select same subnets you configured to VPC.
  If you want yonu can select ssh keypair for trouble shooting.I havent done that.


#Accessing to Eks cluster.

Without having EKS cluster access you cant deploy or monitor cluster.so, it depends on requirements of the project.

ACCESSING EKS CLUSTER.
  1.  Kubectl installation is required.
  2.AWS CLI is required to configure access and we need to configure keys and permission to it.
      configure authentication.
  3. Go to IAM Dash board
         a.generate keys for the user throug which you have created  EKS cluster.
         b. click on manage access keys.

![Screenshot (32)](https://user-images.githubusercontent.com/114085306/226707851-0a88cb99-8b49-44b1-acbe-e00dd1fed925.png)

        aws configure = It asks for Access key id
        can use this as well  aws sts get-caller-identity.  This shows which local user configured to it.
        aws eks update-kubeconfig --region region-code --name my-cluster.
        
        ![Screenshot (33)](https://user-images.githubusercontent.com/114085306/226707955-e8f8bf0a-5ba7-43a6-9041-fe5f8af27056.png)

It adds new file (for what we done)and can see it by doing cat command.
Then we can use kubectl get nodes
#Kubectl get nodes- This command shows the nodes whixh are ready and up.
![Screenshot (34)](https://user-images.githubusercontent.com/114085306/226708064-4183f119-095a-48e8-8115-0a6186518059.png)

After that we go and create services , we can create services in Visual studio code. 
In that we use YAML documents to write Kubernetes manifest files.They are like below.
![Screenshot (38)](https://user-images.githubusercontent.com/114085306/226709739-36ab98b6-18b4-4b7b-830d-f7795472ab38.png)
 
This is a service pod in which is useful in exposing pods to internet, because by default pods are private to the network if we want to expose them to internet, we first create a service and configure name and TYPE=Loadbalancer.Then it should be given in Deployment-nginx also.If you dont put load balancer or different proxys we can deploy them.



1.apiVersion: apps/v1: This specifies the API version used for the Deployment object. In this case, it's the "apps/v1" version of the Kubernetes API.

2.kind: Deployment: This indicates that the kubernetes object being created is a deployment.

3.metadata: It contains metadata regarding the deployment object, like its name.

4.spec: It defines the desired type of the deployment object, including the no.of replicas, update strategy, and the neede pod templates.

5.replicas: 5: This specifies the desired number of replicas for the deployment, in which here it is 5.

6.strategy: This mentions the update strategy for the deployment.

7.type: RollingUpdate: Here this indicates that the deployment should use a rolling update strategy type.

8.rollingUpdate: This specifies the rolling update configuration, including the highest number of unavailable replicas and the maximum number of latest replicas that can be created during the update.

9.maxSurge: 25%: It specifies that  25% of additional replicas can be created during an update.

10.maxUnavailable: 25%: This specifies that up to 25% of existing replicas can be can't use during an update.

11.selector: This tells the labels used to select the pods that the Deployment should manage.

12.matchLabels: This tells the label selector is used to match the pods, which in here is the name: proxy label.

13.template: This specifies the pod template that is used to create the pods managed by the deployment.

14.metadata: This have metadata about the pod template, like its labels.

15.spec: This describes the desired state of the pod template, including the containers running in the pod.

16.Containers: This specifies the containers running in the pod, here it is a single container running the nginx image.

17.name: nginx: This tells the name of the container.

18.image: kammana/nodeapp:v3: This specifies the docker image used here in the container.

19.resources: This specifies the  available resource requests and limits for the container, this also includes memory & CPU.

20.Ports: Here it specifies the container port used to expose the application running in  container. Here, it  is port no 8080.

 
By above we can understand that this manifest file is having 5 replicas of a nginx webapplication.with resources and some rolling updates and surges.

![Screenshot (39)](https://user-images.githubusercontent.com/114085306/226710645-88b336a3-e823-4de4-bc6c-e23d1e9655fc.png)


![Screenshot (37)](https://user-images.githubusercontent.com/114085306/226709134-8265da13-a0a5-49e1-a85f-6ee4737de10e.png)

After creating services service like that , by using kubectl create command we can create svc and use kubectl get svc command to see it.
And if you copy that address and hit it on internet you can see the out put like below.
![Screenshot (36)](https://user-images.githubusercontent.com/114085306/226711430-93ac93a9-0cf0-4c4d-8f32-1ff18f58ddaa.png)

Here we can see the sample web application deployed on internet successfully.

There are several services used in project like
container,

memory,

replica set,

cpu,

ImageContainer portno etc..

Here all these are used because these all are part of application, these specify the applications status and etc.Without these, application can't be deployed on to the internet.

## The other procedures used in project are as fallows.

Troble shooting Pods if pod fails.
these methods involves commands like       

#kubectl logs <pod-name>
  
kubetcl describe pod<pod name>
  
  ![Screenshot (41)](https://user-images.githubusercontent.com/114085306/226715309-ac68200d-d064-46da-966e-d19026922780.png)

  Here we can see pods status from starting,like tis there are some methods through which we can troubleshoot pods.
  
 # some times we get some update issues and we want to trouble shoot the problem, at that like times we generally rollback to previous deployments.
  
Here we can see some commands related that issue in my project.  
  
1.  ![Screenshot (45)](https://user-images.githubusercontent.com/114085306/226718848-7bf1a1bd-8ae0-4ee6-90a0-51141d99ecf8.png)

like in above picture we can delete a service and deploy previous version.
  
The results will be like fallows.
  
  ![Screenshot (46)](https://user-images.githubusercontent.com/114085306/226719207-6fc98a89-e1dd-4669-81e6-acc648983b76.png)
  
  
 Some other methods by which we can undo deployment rollouts are by using some commands like fallows
  
1.Kubectl rollout undo deployment.---> This will directs to previous version of application.
  
2.kubectl rollout status deploymentnginx---.This is to see rollout deployment status.
  
#ADDING VOLUMES TO THE CREATED SUBNETS.
  
1.We can add volumes to the specific servers in case if the application required more volume.
  
  ![Screenshot (51)](https://user-images.githubusercontent.com/114085306/226729092-51e7bc89-1cb9-4217-8330-7e7101eef2cd.png)
like above we can select the node and add volume to it. 
  
  

![Screenshot (52)](https://user-images.githubusercontent.com/114085306/226729327-941d05d5-f19a-415d-bfc2-d2c539e7f348.png)

by selecting the option we can configure required volume to a node. and also can add Snapshot life cycle to the volumes we created.This is for not loosing any data or memory, simply we can say for data backups.
  
  ![Screenshot (53)](https://user-images.githubusercontent.com/114085306/226729783-e67b3e21-5895-4c8b-9103-4576c49369d7.png)

  So, this is my project regarding AWS EKS deployment.In this document i have mentioned all the process done in the project one after one. 
  
  # THANK YOU FOR VISITING
  
    IF YOU FEEL LIKE TELLING ANYTHING REGARDING DOCUMENTATION OR SUGGESTIONS PLEASE CONTACT ME THROUGH MY SOCIAL MEDIA ACCOUNTS.
  
<img align="centre" height="100" width="300" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTJU6b8T45sU0zhdLbXY-QSDXTibMTSw7LwxQ&usqp=CAU">                                                  
