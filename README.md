                                                              # AWS-EKS-Project

                   

1.This Project is about Deploying Kubernetes application using using AWs kubernetes service.
AWS EKS- Aws eks is a service which is provided by Amazon Web Services for Kubernetes .This service is fully managed by AWS itself. The main        purpose of this service is to provide support for Deploying applications on internet.

In this service we can launch an a server and assaign Networks, Subnets , and create Pods, assign security groups ,can attach multiple              loadbalancers depending upon application requirements.

 In this service we use tools like AWs cloud watch,Loadbalancers and so on .

2.WHY AWS EKS CLUSTER?
     Because now a days all the projects using this service because it provides services in such a      way that we can deploy,scale,rollout,and        can monitor our project/application very easily. How       ever there are other compitetors are there in the market for EKS service, these          services are  different from person/ person or ganizations.

3.I prefer AWs Eks cluster because as a user i feel like it provides me with good user interface and godd services. Other EKS providers in              market are i) Google Kubernetes Engine (GKE)
                  ii) Microsoft Azure Kubernetes Service (AKS)
                 iii)  and Red Hat OpenShift.

 This is a project aimed to deploy my sample application using AWS EKS .


4.AWS EKS PROCESS:     
  1.Go to AWS Console--Select AWS EKS Service.--Click on Add Cluster--     create-- and Give name--select version--Cluster service role--(generally    cluster generally have  two roles 1.Master to manage 
                                  2.nodes. also called as workers).

 Cluster require access to services like ECS, ECR,and others. so For that we create cluster service role.

5.After creating Eks cluster we need to create Node group and select it.

Node IAM role 
Create roles in that for IAM.
 Under use case choose EC2 and click next. 
give the fallowing permission for roles like 1.Amazon EKSWorker node policy.
                                             2.AmazonEC2ContainerRegistryReadOnly.
                                             3.Amazon EKS_CNI_policy

 provide name and hit create a node and select node group policy under it.
 In nod egroup configurataion it asks about AMI type,Capacity type, Instance types, Disk sizes etc give all of them.

6.In node group scaling configuration you can select Desired size,Minimum size,Maximum size of nodes.
 In network configuration select same subnets you configured to VPC.
  If you want yonu can select ssh keypair for trouble shooting.I havent done that.


#Accessing to Eks cluster.

Without having EKS cluster access you cant deploy or monitor cluster.so, it depends on requirements of the project.

ACCESSING EKS CLUSTER.
  1.  Kubectl installation is required.
  2.AWS CLI is required to configure access and we need to configure keys and permission to it.
      configure authentication.
  3. Go to Iam Dash board
         a.geerate keys for the user throug which you have created  EKS cluster.
         b. click on manage access keys

        aws configure = It asks for Access key id
        can use this as well  aws sts get-caller-identity.  This shows which local user configured to it.
        aws eks update-kubeconfig --region region-code --name my-cluster.
It adds new file (for what we done)andcan see it by doing cat command.
Then we can use kubectl get nodes
Kubectl get nodes-This command shows the nodes whixh are ready and up.
 
