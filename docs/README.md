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

# Configuring input parameters

ConfigMyApp accepts arguments from 3 sources, where parameters configured in runtime takes precedence over environment variables, and environment variables over configuration json file. Therefore, priority order is the following:

1. Runtime parameters 
2. Environment variables 
3. Configuration file config.json 

## Runtime parameters  

To get all of the parameters available to pass in runtime, you can use the help command of the `start.sh` script:
```
./start.sh --help
```

It is going to print out all the flags available to use. Current list of parameters is the following:

| Section       | Parameter  | Description  | Mandatory |
| ------ |:------- | :--------- |  :----: |
| Connection | `-c, --controller-host` | controller host (no default) | :heavy_check_mark: |
| Connection | `-P, --controller-port` | controller port (8090 by default) | :heavy_multiplication_x: |
| Connection | `--use-https, --no-use-https` | if on, specifies that the agent should use SSL (false by default) | :heavy_multiplication_x: |
| Account | `--account` | account name (customer1 by default) | :heavy_check_mark: |
| Account | `-u, --username` | appd user username (no default) | :heavy_check_mark: |
| Account | `-p, --password` | appd user password (no default) | :heavy_check_mark: |
| Account | `--use-encoded-credentials, --no-use-encoded-credentials` | use base64 encoded credentials (false by default) | :heavy_multiplication_x: |
| Proxy | `--use-proxy, --no-use-proxy` | use proxy optional argument (false by default) | :heavy_multiplication_x: |
| Proxy | `--proxy-url` | proxy url (no default) | :heavy_multiplication_x: |
| Proxy | `--proxy-port` | proxy port (no default) | :heavy_multiplication_x: |
| Branding | `--use-branding, --no-use-branding` | enable branding (true by default) | :heavy_multiplication_x: |
| Branding | `--logo-name` | logo image file name (no default) | :heavy_multiplication_x: |
| Branding | `--background-name` | background image file name (no default) | :heavy_multiplication_x: |
| Application | `-a, --application-name` | application name (no default) | :heavy_check_mark: |
| Application | `--include-database, --no-include-database` | include database (false by default) | :heavy_multiplication_x: |
| Application | `-d, --database-name` | database name, mandatory if include-database set to true (no default) |  :heavy_multiplication_x: |
| Application | `-s, --include-sim` | include server visibility (false by default) |  :heavy_multiplication_x: |
| Application | `-b, --configure-bt` | configure busness transactions (false by default) |  :heavy_multiplication_x: |
| Application | `--overwrite-health-rules` | overwrite health rules (true by default) |  :heavy_multiplication_x: |
| Application | `--bt-only, --no-bt-only` | configure business transactions only  |  :heavy_multiplication_x: |

Please note that you can run the script in debug mode by using `--debug` flag, in which case the connection and other parameters used are going to be printed out in the console in order to help setting us the environment. We do not recommend using this flag in production, and it is set to `false` by default.


## Environment variables

## Configuration file



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
Jenkins is running on `localhost:8080` and you can access it in the browser.

Since volumes are mounted, note that all of your data configurations, plugins, pipelines, passwords, etc. will be persisted on the machine where conatainers are stared from.

For more information about running Jenkins in Docker container refer to the official documentation:
https://www.jenkins.io/doc/book/installing/#downloading-and-running-jenkins-in-docker

### Unlock Jenkins
If you are starting the Jenkins container for the first time, in order to check for your password, access the container logs in the following way:
```
docker logs CONTAINER_ID
```
And copy and paste the password from container to a Jenkins web form input field when prompted.

More details about Unlocking Jenkins can be found here:
https://www.jenkins.io/doc/book/installing/#unlocking-jenkins


## Docker
