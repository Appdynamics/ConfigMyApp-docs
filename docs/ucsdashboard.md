
<p><img align="right" width="100" height="60" src="https://user-images.githubusercontent.com/2548160/68075860-ba631e80-fda5-11e9-8457-07859944ae08.png"> </p><strong> Cisco UCS Monitoring Extension</strong>

# Required Tool

Config Exporter - Ask your AppDynamics representative to give you the Config Exporter tool if you don't already have it. Config exporter be used to migrate configuration between controllers or applications. The configuration can be imported directly into another controller/application or it can be download as a file. 

We will use config exporter in this section to import application configurations and health rules into controller. 

# Create Analytics Metrics 

Copy the queries from this <a href="https://gist.github.com/iogbole/961a3ab20503a1c90b9ac9896822e6a7#file-queries-txt" target="_blank"> GitHub gist file </a> and create analytics metrics from them. The metric name should exactly be the same as the value in the gist - 


Refer to the <a href="https://docs.appdynamics.com/display/latest/Create+Analytics+Metrics+From+Scheduled+Queries"> Create Analytics Metrics From Scheduled Queries</a> documentation for details on how to do this. 


# Monitor the monitor 

UCS Monitoring extension performs a health check on itself, ServiceNow connectivity (if in use) and connectivity to UCS Manager. 

Navigate to the application that contains the tier ID you provided in the config.json file and the create the following health rules using exact name: 

**SNOW Connectivity Health**

 *Health Rule Name:  SNOW Connectivity Health*

 ![SNOW](https://user-images.githubusercontent.com/2548160/68711065-c793c080-0590-11ea-8b9a-30914ac72380.png)

  *Condition* 
  - No warning condition 
  - A metric value of 1 indicates failure 
  
 ![condition](https://user-images.githubusercontent.com/2548160/68712168-0cb8f200-0593-11ea-9494-1cda611080b7.jpg)

**UCS Connectivity Health**

 *Health Rule Name: UCS Connectivity Health*
 
  ![UCS](https://user-images.githubusercontent.com/2548160/68712728-3c1c2e80-0594-11ea-9226-33ac014273d9.png)
 
 *Condition* 
  - No warning condition 
  - A metric value of 1 indicates failure 
  
  ![UCS1](https://user-images.githubusercontent.com/2548160/68712882-8d2c2280-0594-11ea-9e9d-b9c11e4d9e86.png)

**UCS Machine Availability Health**

 *Health Rule Name: UCS Machine Availability Health*
 
 ![Screenshot 2019-11-12 at 21 42 03](https://user-images.githubusercontent.com/2548160/68713370-95d12880-0595-11ea-9f38-658b8feb935e.png)
 
*Condition* 
  - No warning condition 
  - A metric value of 1 indicates success 
![112](https://user-images.githubusercontent.com/2548160/68713582-198b1500-0596-11ea-88ef-78717f7d908c.jpg)





[DRAFT MODE]

1. Create Analytics Queries 
2. Import 
3. Import ucs-monitor application 
4. Import Dashboard JSON 
5. Configure RBAC
