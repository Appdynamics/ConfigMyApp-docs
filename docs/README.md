<p><img align="right" width="100" height="60" src="https://user-images.githubusercontent.com/2548160/68075860-ba631e80-fda5-11e9-8457-07859944ae08.png"></p><strong>ConfigMyApp</strong>

# Introduction

ConfigMyApp is a <b>monitoring-as-a-service</b> solution that automates the configuration of AppDynamics business applications, Server Viz, dashboarding, etc  without the need to manaully login to the controller. Automated configuration saves time, hassle and cost; it decreases human error and maintains consistency of thresholds and naming conventations accross a customer's estate. 

The design of ConfigMyApp is based on the DevOps configuration-as-code paradigm. It enhances medium and large scale application configuration and dashboarding with a specific objective in mind - the ability to plug it into customers' Continous Integration and Deployment (CI/CD) pipelines - such as Jenkins, Harness, TeamCity, GitLab, Bamboo, etc.  

Being able to remotely create and update configurations in AppDynamics will significantly enhance user adoption and time to value. In addition, configuraion-as-code is a concept that will appeal to the DevOps team. 

# Supported Components 

ConfigMyApp supports the configuration of the following AppDynamics components: 

 - Business transactions detection rules <br> 
   Include and Exclude Rules for the following transactions: 
    - POCOs 
    - POJOs 
    - Servlets 
    - ASPs
 - Server Visibility 
 - Business Application 
 - DB Monitoring
 - Custom dashboard with support for custom logo and background images.
 
 # Prequisites 
 The following requirments must be met to run ConfigMyApp: 

 1. It's only supported on Linux/Unix and MacOS. Tested on Ubuntu, CentOS and MacOS
 2. `jq` must be installed on your machine 
 3. `awk` must be installed on the machine 
 4. `sed` must be installed on the machine 
 
Please do not proceed if any of the aforementioned prerequisites are not met.

 # How it works 
 
This is is higlevel flow digram on how ConfigMyApp works. 

![How it works](https://user-images.githubusercontent.com/2548160/79471051-03c4c480-7ffa-11ea-9405-133f9e9ee4eb.png)
 
## Configuring input parameters

ConfigMyApp accepts arguments from 3 sources,  where parameters configured ar runtime takes precedence over environment variables, and environment variables over configuration json file.  The order of parameter definition priority is as follows: 

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

| Section       | Parameter  | Description  | <div style="width:100px">Mandatory parameter</div>  |
| ------ |:------- | :--------- |  :----: |
| Connection | `-c, --controller-host` | controller host (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Connection | `-P, --controller-port` | controller port (8090 by default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Connection | `--use-https, --no-use-https` | if true, specifies that the agent should use SSL (false by default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Account | `--account` | account name (customer1 by default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `-u, --username` | appd user username (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `-p, --password` | appd user password (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `--use-encoded-credentials, --no-use-encoded-credentials` | use base64 encoded credentials (false by default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `--use-proxy, --no-use-proxy` | use proxy optional argument (false by default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `--proxy-url` | proxy url (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `--proxy-port` | proxy port (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `--use-branding, --no-use-branding` | enable branding (true by default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `--logo-name` | logo image file name (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `--background-name` | background image file name (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `-a, --application-name` | application name (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Application | `--include-database, --no-include-database` | include database (false by default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `-d, --database-name` | database name, mandatory if include-database set to true (no default) |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `-s, --include-sim` | include server visibility (false by default) |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `-b, --configure-bt` | configure busness transactions (false by default) |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `--overwrite-health-rules` | overwrite health rules (true by default) |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `--bt-only, --no-bt-only` | configure business transactions only  |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |

Please note that you can run the script in debug mode by using `--debug` flag, in which case the connection and other parameters used are going to be printed out in the console in order to help setting up the environment. We do not recommend using this flag in production, and it is set to `false` by default.

## Environment variables

Environment variabels used by ConfigMyApp start with `CMA_` and if not empty, will be used to fill-in parameters values not explicitly set in runtime. List of the environment variables currently used is the following:

| Section       | Environment Variable  | Description  | Mandatory parameter |
| ------ |:------- | :--------- |  :----: |
| Connection | `CMA_CONTROLLER_HOST` | controller host | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Connection | `CMA_CONTROLLER_PORT` | controller port | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Connection | `CMA_USE_HTTPS` | if true, specifies that the agent should use SSL | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Account | `CMA_ACCOUNT` | account name | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `CMA_USERNAME` | appd user username | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `CMA_PASSWORD` | appd user password (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `CMA_USE_ENCODED_CREDENTIALS` | use base64 encoded credentials  | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `CMA_USE_PROXY` | use proxy | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `CMA_PROXY_URL` | proxy url | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `CMA_PROXY_PORT` | proxy port | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `CMA_USE_BRANDING` | enable branding | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `CMA_LOGO_NAME` | logo image file name |<img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `CMA_BACKGROUND_NAME` | background image file name | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `CMA_APPLICATION_NAME` | application name | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Application | `CMA_INCLUDE_DATABASE` | include database | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `CMA_DATABASE_NAME` | database name, mandatory if include-database set to true |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `CMA_INCLUDE_SIM` | include server visibility |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `CMA_CONFIGURE_BT` | configure busness transactions |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `CMA_OVERWRITE_HEALTH_RULES` | overwrite health rules |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `-` | configure business transactions only | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
 

## Configuration file

Configuration file used by ConfigMyApp can be found in the root of the project: `config.json`, and contains configuration that is going to be used in case when runtime parameter is not specified and environment variable for the parameter does not exist. The following table contains details of the JSON configuration:

| Section       | JSON path  | Description  | Mandatory parameter |
| ------ |:------- | :--------- |  :----: |
| Connection | `.controller_details[].host` | controller host | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Connection | `.controller_details[].port` | controller port | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Connection | `.controller_details[].use_https` | if true, specifies that the agent should use SSL | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Account | `.controller_details[].account` | account name | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `.controller_details[].username` | appd user username | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `.controller_details[].password` | appd user password (no default) | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Account | `.are_passwords_encoded` | use base64 encoded credentials  | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `.controller_details[].use_proxy` | use proxy | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `.controller_details[].proxy_url` | proxy url | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Proxy | `.controller_details[].proxy_port` | proxy port | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `.branding[].enabled` | enable branding | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `.branding[].logo_file_name` | logo image file name | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Branding | `.branding[].background_file_name` | background image file name | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `.configuration[].application_name` | application name | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2714.png" width="20" height="20"> |
| Application | `.configuration[].include_database` | include database | <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `.configuration[].database_name` | database name, mandatory if include-database set to true |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `.configuration[].include_sim` | include server visibility |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `.configuration[].configure_bt` | configure busness transactions |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |
| Application | `.overwrite_health_rules` | overwrite health rules |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20">|
| Application | `-` | configure business transactions only  |  <img src="https://github.githubassets.com/images/icons/emoji/unicode/2716.png" width="20" height="20"> |


# Running a script

This section contains examples of running a ConfigMyApp script, it should be adjusted to fit your use-case and here are some of the common ones:

> Server visibility

```
./start.sh --application-name <app-name> --include-sim
```

> Database visibility

```
./start.sh --application-name <app-name> --include-database  ---database=’DB collector name’
```

> Health rules

```
./start.sh --application-name <app-name>  --no-overwrite-health-rules
```

> Business transactions

```
./start.sh --application-name <app-name>  --configure-bt
```
```
./start.sh --application-name <app-name>  ---bt-only
```

> Full configuration parameters

```
./start.sh --application-name <app-name>  \ 
                     -c "http://customer1.saas.appdynamics.com" \ 
                     -P “8090” \ 
                      --account customer1 \
                     -p "<password>" \ 
                     -u "username" \ 
                    --no-configure-bt \
                    --include-database \
                    --database-name ’DB Collector Name’ \
                    --include-sim  \ 
                    --use-https  \ 
                    --proxy-url localhost  \
                    --proxy-port 3303  \ 
                    --overwrite-health-rules \ 
                    --use-encoded-credentials
```


# Integrations 

<p><img align="right" width="200" height="60" src="https://user-images.githubusercontent.com/23483887/87051577-a9ea2a00-c1f7-11ea-9ab8-4781d043e9bc.png"></p>

## Harness.io

Harness is a Continuous Delivery as a Service enterprise platform for automation of application and micro-service deployments.

The Harness Delegate is a service you run in your local network or VPC to connect your artifact servers, and your infrastructure, collaboration, and verification providers, with the Harness Manager.

Where delagate and Manager are in the overall Harness Arcitecture, can be seen in the diagram below:

![harness_delegate](https://user-images.githubusercontent.com/23483887/87052304-8a073600-c1f8-11ea-9eb0-bc92f93fd245.png)

### Run Harness.io Delegate as Docker Constainer

Navigate to Harness.io integration folder and run a start script:

```
cd integrations/Harnessio/harness-delegate-docker/
./launch-harness-delegate.sh
```

This command is starting a Docker container that contains your delegate and that you can see by using following command:
```
docker ps
```

In the Harness.io UI delegate appears as active, and you can access it at Setup/Delegates section:

![harness_delegate_ui](https://user-images.githubusercontent.com/23483887/87037486-34c12980-c1e4-11ea-8814-68b98e68aee3.png)

Now when a delegate is available, you can run a defined application pipeline or workflow in order to deploy your configuration to controller.

<p><img align="right" width="200" height="60" src="https://user-images.githubusercontent.com/23483887/87051994-33016100-c1f8-11ea-847f-38da20685581.png"></p>

## Jenkins

Jenkins is a free and open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery.

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
In order to show running containers, use the following command:
```
docker ps
```
Jenkins is running on `localhost:8080` and you can access it in the browser.

Since volumes are mounted, note that all of your data configurations, plugins, pipelines, passwords, etc. will be persisted on the machine where containers are stared from.

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

