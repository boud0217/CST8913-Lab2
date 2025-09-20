# LAB 2 
## On-permises infrastructure
```mermaid
flowchart TD
    User([User]) --> Firewall{Firewall}
    
    Firewall --> LB[Load balancer (VM)]
    Firewall --> BLB[Backup load balancer (VM)]
    
    LB --> Flask1[Flask server (VM)]
    LB --> Flask2[Flask server (VM)]
    LB --> React1[React server (VM)]
    LB --> React2[React server (VM)]
    
    Flask1 --> DB[(Postgres database (VM))]
    Flask2 --> DB[(Postgres database (VM))]

