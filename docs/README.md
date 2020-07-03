

<p><img align="right" width="100" height="60" src="https://user-images.githubusercontent.com/2548160/68075860-ba631e80-fda5-11e9-8457-07859944ae08.png"> </p><strong> ConfigMyApp</strong>

# Introduction

Monitoring as a service (MaaS) is one of many cloud delivery models under anything as a service (XaaS). It is a framework that facilitates the deployment of monitoring functionalities for various other services and applications within the cloud, usually via a CI/CD pipeline. 

ConfigMyApp was built to enable AppDynamics customers actualise thier MaaS objectives. ConfigMyApp is designed based on the DevOps configuration-as-code paradigm. It is primarily built to enhance large scale application configuration and dashboarding with a specific objective in mind - the ability to plug it into customers' Continous Integration and Deployment pipelines - such as Jenkins, Harness, TeamCity, GitLab, Bamboo, etc. 
 
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

**ConfigMyApp Configuration Settings**

**Environment variables settings**

# Run-time parameters  

# Integrations 

**Harness** 
**Jenkins**
**Docker**

| **Config Property Name** | **Description** |
| --- | --- |
| UCSPasswordEncyptionKey  | Any string of your choice. This key is used to encrypt and decrypt UCS connection details. |
| UCSURL  | Specify the IP Address or domain name of UCS manager. Please do not include the http/s bit |
| analyticsEndpoint  | This is the analytics endpoint of your controller. This differs depending on the location of your controller. Please refer to this [doc](https://docs.appdynamics.com/display/PAA/SaaS+Domains+and+IP+Ranges). |
| X-Events-API-AccountName  | You can get the global account name to use from the [License page](https://docs.appdynamics.com/display/latest/License+Management)  |
| X-Events-API-Key  | Create the analytics API Key by following the instruction in this[doc](https://docs.appdynamics.com/display/latest/Managing+API+Keys).  Grant Manage, Query and Publish permissions to Custom Analytics Events. |
| EnableServiceNow  | Set to &#39;yes&#39; or &#39;no&#39;. Other ServiceNOW properties are required if set to yes, else, ignore them. |
| tierID  | This is required to monitor the health of the UCS monitoring extension i.e connectivity to AppDynamics, UCS and SNOW.Follow the instructions in this [doc](https://community.appdynamics.com/t5/Knowledge-Base/How-do-I-troubleshoot-missing-custom-metrics-or-extensions/ta-p/28695#Configuring%20an%20Extension) to acquire the component (or tier) ID. |

