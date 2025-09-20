# LAB 2 
## On-permises infrastructure


```mermaid
flowchart TB
    %% Utilisateur
    User([User]) --> FW[Firewall]

    %% Load Balancers
    FW --> LB[Load balancer VM]
    FW --> BkpLB[Backup load balancer VM]
    subgraph LoadBalancers [Load Balancers]
        LB
        BkpLB
    end

    %% Flask App
    LB --> Flask1[Flask server VM]
    LB --> Flask2[Flask server VM]
    LB --> Flask1
    LB --> Flask2

    subgraph FlaskApp [Flask App]
        Flask1
        Flask2
    end
    DB[(PostgreSQL database VM)]
    Flask1 --> DB
    Flask2 --> DB

    %% React App
    LB --> React1[React server VM]
    LB --> React2[React server VM]
    LB --> React1
    LB --> React2

    subgraph ReactApp [React App]
        React1
        React2
    end
```
### Description
For on-permises infrastructure, we can : 
- Deploy a VMWare VSphere to host the Virtual machines hosting every apps, databases and load balancers. We deploy many of each in case of failover.
- Install a Firewall to protect the Virtual machines. The user access the apps through the firewall.
- use the load balancers to balance between the apps depending on their availability. The load balancers are installed in virtual machines.
- Only the backend Flask app can communicate with the database.

## Cloud using IaaS infrastructure
```mermaid
flowchart TB
    %% Utilisateur
    User([User]) --> LB[Load balancer service]

    %% Flask App
    LB --> Flask1[Flask server VM]
    LB --> Flask2[Flask server VM]

    subgraph FlaskApp [Flask App]
        Flask1
        Flask2
    end
    DB[(PostgreSQL database VM)]
    Flask1 --> DB
    Flask2 --> DB

    %% React App
    LB --> React1[React server VM]
    LB --> React2[React server VM]

    subgraph ReactApp [React App]
        React1
        React2
    end
```

### Description
For cloud using IaaS infrastructure, we can :
- Use the cloud load balancer technology as a load balancer. 
- Deploy the virtual machines for the database, the React and the Flask app
- Use the same communication rules as the on-permise infrastructure.

## Cloud using PaaS
```mermaid
flowchart TB
    %% Utilisateur
    User([User]) --> LB[Load balancer Service]

    %% Flask App Service
    LB --> Flask[App Service Flask]
    Flask --> DB[(PostgreSQL database Service)]

    %% React App Service
    LB --> React[App Service React]
```
### Description
For cloud using PaaS infrastructure, we can :
- Deploy only the code using the cloud app services (AWS Elastic Beanstalk, Azure App Service or Google Cloud Run)
- Use the PostGreSQL database service of the cloud 
- Use the cloud load balancer service

