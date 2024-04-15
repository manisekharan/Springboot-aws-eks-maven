# springboot-eks (SpringBoot App -> Docker -> ECR -> EKS)

1. Pull Git repository - SpringBoot application with Maven
2. Open in Intellij as Maven project
3. Maven install the project to create jar
4. Create Docker image
      docker build -t springboot-eks .
      Push docker image to AWS ECR (Elastic Container Registry)
      Create a new AWS ECR Repository with repository name (springboot-eks)
      aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 159205870343.dkr.ecr.us-east-1.amazonaws.com
      docker build -t springboot-eks .
      docker tag springboot-eks:latest 159205870343.dkr.ecr.us-east-1.amazonaws.com/springboot-eks:latest
      docker push 159205870343.dkr.ecr.us-east-1.amazonaws.com/springboot-eks:latest
6. Note: System should have aws-cli installed.
   once pushed the image, copy URI for k8s deployment url.

# Create EKS Cluster

```eksctl create cluster --name my-demo-cluster --version 1.28 --nodes=1 --node-type=t2.small --region us-east-2```

# Configure kubectl to Use the EKS Cluster

```aws eks --region us-east-2 update-kubeconfig --name my-demo-cluster```
