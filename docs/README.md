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

Note that mandatory parameters need to be provided in any (and not all) of the available ways of configuration listed above in order for ConfigMyApp to be able to start.

## Runtime parameters  

To get all of the parameters available to pass in runtime, you can use the help command of the `start.sh` script:
```
./start.sh --help
```

It is going to print out all the flags available to use. Current list of parameters is the following:

| Section       | Parameter  | Description  | Mandatory parameter |
| ------ |:------- | :--------- |  :----: |
| Connection | `-c, --controller-host` | controller host (no default) | :heavy_check_mark: |
| Connection | `-P, --controller-port` | controller port (8090 by default) | :heavy_multiplication_x: |
| Connection | `--use-https, --no-use-https` | if true, specifies that the agent should use SSL (false by default) | :heavy_multiplication_x: |
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

Environment variabels used by ConfigMyApp start with `CMA_` and if not empty, will be used to fill-in parameters values not explicitly set in runtime. List of the environment variables currently used is the following:

| Section       | Environment Variable  | Description  | Mandatory parameter |
| ------ |:------- | :--------- |  :----: |
| Connection | `CMA_CONTROLLER_HOST` | controller host | :heavy_check_mark: |
| Connection | `CMA_CONTROLLER_PORT` | controller port | :heavy_multiplication_x: |
| Connection | `CMA_USE_HTTPS` | if true, specifies that the agent should use SSL | :heavy_multiplication_x: |
| Account | `CMA_ACCOUNT` | account name | :heavy_check_mark: |
| Account | `CMA_USERNAME` | appd user username | :heavy_check_mark: |
| Account | `CMA_PASSWORD` | appd user password (no default) | :heavy_check_mark: |
| Account | `CMA_USE_ENCODED_CREDENTIALS` | use base64 encoded credentials  | :heavy_multiplication_x: |
| Proxy | `CMA_USE_PROXY` | use proxy optional argument | :heavy_multiplication_x: |
| Proxy | `CMA_PROXY_URL` | proxy url | :heavy_multiplication_x: |
| Proxy | `CMA_PROXY_PORT` | proxy port | :heavy_multiplication_x: |
| Branding | `CMA_USE_BRANDING` | enable branding | :heavy_multiplication_x: |
| Branding | `CMA_LOGO_NAME` | logo image file name | :heavy_multiplication_x: |
| Branding | `CMA_BACKGROUND_NAME` | background image file name | :heavy_multiplication_x: |
| Application | `CMA_APPLICATION_NAME` | application name | :heavy_check_mark: |
| Application | `CMA_INCLUDE_DATABASE` | include database | :heavy_multiplication_x: |
| Application | `CMA_DATABASE_NAME` | database name, mandatory if include-database set to true |  :heavy_multiplication_x: |
| Application | `CMA_INCLUDE_SIM` | include server visibility |  :heavy_multiplication_x: |
| Application | `CMA_CONFIGURE_BT` | configure busness transactions (false by default) |  :heavy_multiplication_x: |
| Application | `CMA_OVERWRITE_HEALTH_RULES` | overwrite health rules (true by default) |  :heavy_multiplication_x: |
| Application | `-` | configure business transactions only  |  :heavy_multiplication_x: |
 

## Configuration file

Configuration file used by ConfigMyApp can be found in the root of the project: `config.json`, and contains configuration that is going to be used in case when runtime parameter is not specified and environment variable for the parameter does not exist. The following table contains details of the JSON configuration:

| Section       | JSON path  | Description  | Mandatory parameter |
| ------ |:------- | :--------- |  :----: |
| Connection | `.controller_details[].host` | controller host | :heavy_check_mark: |
| Connection | `.controller_details[].port` | controller port | :heavy_multiplication_x: |
| Connection | `.controller_details[].use_https` | if true, specifies that the agent should use SSL | :heavy_multiplication_x: |
| Account | `.controller_details[].account` | account name | :heavy_check_mark: |
| Account | `.controller_details[].username` | appd user username | :heavy_check_mark: |
| Account | `.controller_details[].password` | appd user password (no default) | :heavy_check_mark: |
| Account | `.are_passwords_encoded` | use base64 encoded credentials  | :heavy_multiplication_x: |
| Proxy | `.controller_details[].use_proxy` | use proxy optional argument | :heavy_multiplication_x: |
| Proxy | `.controller_details[].proxy_url` | proxy url | :heavy_multiplication_x: |
| Proxy | `.controller_details[].proxy_port` | proxy port | :heavy_multiplication_x: |
| Branding | `.branding[].enabled` | enable branding | :heavy_multiplication_x: |
| Branding | `.branding[].logo_file_name` | logo image file name | :heavy_multiplication_x: |
| Branding | `.branding[].background_file_name` | background image file name | :heavy_multiplication_x: |
| Application | `.configuration[].application_name` | application name | :heavy_check_mark: |
| Application | `.configuration[].include_database` | include database | :heavy_multiplication_x: |
| Application | `.configuration[].database_name` | database name, mandatory if include-database set to true |  :heavy_multiplication_x: |
| Application | `.configuration[].include_sim` | include server visibility |  :heavy_multiplication_x: |
| Application | `.configuration[].configure_bt` | configure busness transactions (false by default) |  :heavy_multiplication_x: |
| Application | `.overwrite_health_rules` | overwrite health rules (true by default) |  :heavy_multiplication_x: |
| Application | `-` | configure business transactions only  |  :heavy_multiplication_x: |


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
