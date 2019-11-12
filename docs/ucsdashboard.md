
<p><img align="right" width="100" height="60" src="https://user-images.githubusercontent.com/2548160/68075860-ba631e80-fda5-11e9-8457-07859944ae08.png"> </p><strong> Cisco UCS Monitoring Extension</strong>

# Required Tool

Config Exporter - Ask your AppDynamics representative to give you the Config Exporter tool if you don't already have it. Config exporter be used to migrate configuration between controllers or applications. The configuration can be imported directly into another controller/application or it can be download as a file. 

We will use config exporter in this section to import application configurations and health rules into controller. 

# Monitor the monitor 

UCS Monitoring extension performs a health check on itself, ServiceNow connectivity (if in use) and connectivity to UCS Manager. 

Navigate to the application that contains the tier ID you provided in the config.json file and the create the following health rules using exact name: 

**SNOW Connectivity Health**

 Health Rule Name: SNOW Connectivity Health
 
 ![SNOW](https://user-images.githubusercontent.com/2548160/68711065-c793c080-0590-11ea-8b9a-30914ac72380.png)

  Conditition 
  - No warning condition 
  - A metric value of 1 indicates failure 
 ![condition](https://user-images.githubusercontent.com/2548160/68712168-0cb8f200-0593-11ea-9494-1cda611080b7.jpg)







[DRAFT MODE]

1. Create Analytics Queries 
2. Import Analytics Health Rules 
3. Import ucs-monitor application 
4. Import Dashboard JSON 
5. Configure RBAC
