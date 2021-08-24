# Multibranch Jenkins Docker App
This repository is to the build a multibranch Pipeline project.This uses the sample Spring Boot Java application 
with Maven as build tool.Its delivery will be different depending on the Git branch that Jenkins builds 
from. That is, the branch being built determines which delivery stage of your Pipeline is executed.I have used 
docker agent in the Jenkinfile to compile, build, test and package the application.

The root directory contains an example of the Jenkinsfile (i.e. Pipeline) and the scripts that contains shell scripts with commands that are executed 
when Jenkins processes either the "Deliver for development" or "Deploy for production" stages of your Pipeline (depending on
the branch that Jenkins builds from).

##Prerequisite
1. Docker
2. Goto [this repo](https://github.com/ga7uti/run-jenkins-in-docker.git) and follow the instructions


## Build Steps
1. Clone repository
```bash
git clone https://github.com/ga7uti/multibranch-jenkins-docker-app.git
cd multibranch-jenkins-docker-app
```
2. Create new branches dev and prod
```bash
git checkout -b dev
git push -u origin dev

git checkout -b prod
git push -u origin prod
```
3. Configure ssh remote details in the Jenkins file.


## Disclaimer
This repositories are not intended to provide complete applications,
basically they are sandboxes and pet projects to try different technologies and
techniques.
