# Orange_Task

### Task 1

## K8s instance will have three Namespaces: Build, Dev and Test.
kubectl create ns build
kubectl create ns dev
kubectl create ns test

## Build namespace will have two pods: one for Jenkins and another for Nexus Repository OSS

cd helm/
helm install nexus sonatype/nexus-repository-manager -f nexus.yaml -n build
helm install jenkins jenkins/jenkins -f jenkins.yaml -n build

## Dev and Test instances will run two pods: one for Spring Boot application and another for MySQL DB

cd Toy0Store/

mvn mvn clean package

docker build -t <image name> .

Note: please replace image name in app.yaml

cd deployment/

minikube start --vm-driver=none

kubectl create secret generic mysql-root-pass --from-literal=password=R00t

kubectl create secret generic mysql-user-pass --from-literal=username=callicoder --from-literal=password=Admin@12

kubectl create secret generic mysql-db-url --from-literal=database=toystore --from-literal=url='jdbc:mysql://toystore-app-mysql:3306/toystore?useSSL=false&serverTimezone=UTC&useLegacyDatetimeCode=false'

kubectl get secrets

kubectl describe secrets mysql-user-pass

kubectl apply mysql.yaml

kubectl get pv

kubectl get pvc

kubectl get svc

kubectl get deployments

kubectl get pods

kubectl apply app.yaml

kubectl get pods

## to test

minikube service toystore-app-server --url

## Create a Jenkins pipeline job to do the following:
a- Allow user to choose commit to build using Github plugin
b- Checkout code from https://github.com/ahmedmisbah-ole/Devops-Orange
c- Build spring boot project using Maven (clean package)
d- Create a Docker image from JAR file
e- Upload Docker image to Nexus

in jenkinsfile





























