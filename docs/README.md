<p><img align="right" width="100" height="60" src="https://user-images.githubusercontent.com/2548160/68075860-ba631e80-fda5-11e9-8457-07859944ae08.png"></p><strong>ConfigMyApp</strong>

# Introduction

Monitoring as a service (MaaS) is one of many cloud delivery models under anything as a service (XaaS). It is a framework that facilitates the deployment of monitoring functionalities for various other services and applications within the cloud, usually via a CI/CD pipeline. ConfigMyApp was built to enable AppDynamics customers actualise thier MaaS objectives.

ConfigMyApp design is based on the DevOps configuration-as-code paradigm. It is primarily built to enhance medium and large scale application configuration and dashboarding with a specific objective in mind - the ability to plug it into customers' Continous Integration and Deployment pipelines - such as Jenkins, Harness, TeamCity, GitLab, Bamboo, etc. 

# How it works 

![How it works](https://user-images.githubusercontent.com/2548160/79471051-03c4c480-7ffa-11ea-9405-133f9e9ee4eb.png)
 
ConfigMyApp currently supports the following configurations (as-code): 
 
1) Business transactions detection rules - for  POCOs, POJOs, Servlets and ASPs transactions 
2) Server Viz Health Rules   
3) Application Health Rules  
4) DB Monitoring 
6) Custom dashboard branding 
5) and finally, ConfigMyApp dynamically pulls all the configurations into a dynamic dashboard. 

# Prerequisites

3) Before the extension is installed, the generic AppDynamics extension prerequisites mentioned [here](https://community.appdynamics.com/t5/Knowledge-Base/Extensions-Prerequisites-Guide/ta-p/35213) need to be met. 

Please do not proceed with the extension installation if any of the aforementioned prerequisites are not met.

# Installation

## ConfigMyApp Configuration Setting

## Environment variables setting

# Run-time parameters  

# Integrations 

## Harness

## Jenkins

### Prerequisite 
Verify that you are having Docker Compose installed:
```
docker-compose --version
```
### Run Jenkins as Docker Constainer
To start a local Jenkins server navigate to Jenkins folder and start the containers defined in docker-compose.yaml file: 
```
cd /integrations/Jenkins
docker-compose up -d
```
In order to show running containers, use the follwoing command:
```
docker ps
```
Jenkins is running on localhost:8080 and you can access it in the browser.

Since volumes are mounted, note that all of your data configurations, plugins, pipelines, passwords, etc. will be persisted on the machine where conatainers are stared from.

More information about running Jenkins in Docker container can be found in the official documentation:
https://www.jenkins.io/doc/book/installing/#downloading-and-running-jenkins-in-docker

### Unlock jenkins
If you are starting the Jenkins container for the first time, in order to check for your password, access the container logs in the following way:
```
docker logs CONTAINER_ID
```
And copy and paste the password from container to a Jenkins web form input field when prompted.

More details about Unlocking Jenkins can be found here:
https://www.jenkins.io/doc/book/installing/#unlocking-jenkins


## Docker
