# Overview
***
1. The Architect's Mindset
2. The Architecture Process
3. Working with System Requirements
4. Types of Applications
5. Selecting Technology Stack 
6. Meet the *-ilities
7. Component's Architecture
8. Design Patterns 101
9. System Architecture
10. External Considerations 
11. Architecture Document 
12. Case Study
13. Advanced Architecture Topics
14. Soft Skills
***

## What is a Software Architect 
***
- Infrastructure Architect ( Servers, VMs, Network, Storage)
- Software Architect, Solution Architect or System architect ( to be discussed later)
- Enterprise Architect ( Works with CEO,CIO.... Streamlines the IT to support business)
***
  
Developers Knows What CAN Be Done  
Architect Knows What SHOULD Be Done. 

***
Baseline Requirements: 
- Fast (Throughput)
- Secure (Security) 
- Reliable ( No single point of failure)
- Easy to maintain (Scalability)
***

## Organization Chart 
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/softwareOrgChart.png)

## The Architect's Process
***
- Understand the System's Requirements 
(What should the system do?)

- Understand the Non-Functional Requirements 
(Define Technical & Service Level Attributes # of Users,Loads,Volumes,Performance)

- Map the Componenets
(Represent the Tasks of the System. 2 Goals - System Functionality, Communicate your undertanding to the client, Non-Technical)

- Select the Technology Stack
(Back End, FrontEnd , Data Store)

- Design the Architecture
- Write the Architecture Document
- Support the Team
***

## Understanding System Requirements
***
- what the system should do (Funcional requirements).  
-- business flow.  
-- business services.  
-- user interfaces.  

- what should the system deal with.(Non-functional Requirements).  
-- Performance.  
-- Load   
-- Data Volume.   
-- Concurrent Users.    
-- SLA.   
***
## Non-Functional requirements
### Performance 
What is the required performane for this system? Fast...
***
- Latency.  
-- How much time does it take to perform a single task (1 second).  
- Through put   
-- how many users can be saved in the database in a minute. (well designed app -1000usrs/min).  
- Load   
-- Quantity of work without crashing. ( 5000 usrs without crashing) 
- Data Volume 
-- 
***
