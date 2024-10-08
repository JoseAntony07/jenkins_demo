

# Jenkins setup in ubuntu (refer jenkins_setup_in_ubuntu.txt in docs)

#  Dockerize the fastAPI application

1) Create a Dockerfile 
2) Build and Test the Docker Image
   - docker build -t jenkins_demo .
   - docker run -p 8000:80 jenkins_demo
3) Push Docker Image to Docker Hub
  - docker login
  - docker tag jenkins_demo joseantony07/jenkins_demo
  - docker push joseantony07/jenkins_demo

# Setup jenkins pipeline

1) Create a New Pipeline Job
   - Go to New Item, enter a name(jenkins_demo), select Pipeline, and click OK.
2) Configure the Pipeline
   - dashboard -> jenkins_demo -> configure -> pipeline
3) Refer script (jenkins_script.txt in project folder)

# permission denied while trying to connect to the Docker daemon socket

- sudo usermod -aG docker jenkins
- sudo systemctl restart jenkins
- sudo systemctl restart docker

# Verify Docker Access

- sudo su - jenkins
- docker ps

# Create Docker Hub Credentials in Jenkins

- Dashboard -> Manage Jenkins -> Credentials -> System -> Global credentials (unrestricted) -> Add Credentials

Kind: Username with password
Scope: Global (or as needed)
Username: joseantony333.jan@gmail.com
Password: JayaJohn07
ID: docker-hub-credentials (mentioned in jenkins_script.txt - must match the ID used in your pipeline)
Description: Docker Hub credentials

# Setup Minikube (https://docs.google.com/document/d/1l-0fGQ20RdFZGj-3LP68T6gXhrcptaAG3A69nooQowc/edit)

1) Create kubernetes deployment file(jenkins_demo_kubernetes.yaml)
2) Apply the deployment
   - kubectl apply -f jenkins_demo_kubernetes.yaml
3) Access the application
   - minikube service jenkins-demo -n jenkins
4) Commands
  - minikube start
  - kubectl create namespace jenkins
  - kubectl apply -f jenkins_demo_kubernetes.yaml
  - kubectl delete -f jenkins_demo_kubernetes.yaml
  - minikube service jenkins-demo -n jenkins   - to get server url (http://192.168.49.2:31364/docs - fastapi application)
  - minikube dashboard - to see kube dashboard contains all service status(select jenkins in above dropdown)

# Reference

- https://www.youtube.com/watch?v=Sl94H5e7MPw
- https://www.youtube.com/watch?v=leDt90jW_Gw
- https://github.com/net-vinothkumar/cicd-k8s-demo/tree/master

# Pending 

- add kube process in jenkins pipeline script
- automate the whole process(code -> git hub -> jenkins -> dockerhub -> minikube)


(.venv) jose-antony@joseantony-Latitude-5400:~/new projects/jenkins_demo$ minikube service jenkins-demo -n jenkins
|-----------|--------------|-------------|---------------------------|
| NAMESPACE |     NAME     | TARGET PORT |            URL            |
|-----------|--------------|-------------|---------------------------|
| jenkins   | jenkins-demo |          80 | http://192.168.49.2:31909 |
|-----------|--------------|-------------|---------------------------|
🎉  Opening service jenkins/jenkins-demo in default browser...
(.venv) jose-antony@joseantony-Latitude-5400:~/new projects/jenkins_demo$ Opening in existing browser session.


- Hit url in browser -> http://192.168.49.2:31909/docs
