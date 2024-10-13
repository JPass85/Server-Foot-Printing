# Server Foot-Printing

## Description
 Foot-printing a server is the process of gathering infomation about target server/network during the reconnaissance phase of a cybersecurity assessment or penetration test. It will involve the collection of data such as IP addresses, domain names, open ports, services, operating systems, and software versions that are running on the server. My goal is to create a detail map of target's structure, which can then be used to identify potentioal vulnerabilities for exploitation.

## Objective
 There's three different servers within client's internal network the I am commissioned to test. The client uses serveral different services that the security department felt performing a penetration test would be necessary to gain insight into the overall posture of their security.
 - The first server is an internal DNS server and the client would like to understand what information can be extracted from the services and how it could potentially be used against them. My goal is to gather as much information as possible about the servers and find ways to use that information against the client's company. The client has made it very clear that it's forbidden to aggressively attack services using exploits, as the services are currently in production. 
 - The second server is a service that everyone on the internal network has access to. During the preparatory meeting, I informed the client that these servers are often prime targets for threat actors and should be included in my scope of work (SOW). The client agreed, allowing me to proceed and add the server to the SOW. My objective remains the same: to gather as much information as possible about the server and identify ways to exploit it. To ensure proof and protect customer data, the client will create a user account named 'Papa Bear.' I will then need to obtain the credentials for 'Papa Bear' as part of the demonstration.
 - The third server functions as both an MX and management server for the internal network. Additionally, it serves as a backup server for the internal domain accounts. A user named "Papa Bear" has been created on this server, and we need to obtain its credentials.

## Approach

### Server 1:
 Through a basic social engineering approach, I successfully obtained credentials for one of the company's employees. Additionally, I found that other employees were discussing SSH keys on a forum. Using Nmap, I methodically enumerated the server with the ![image](https://github.com/user-attachments/assets/599d8713-eebc-40d3-81a4-c4c544da7df3) command to identify open ports. 
 
#### Example:
![image](https://github.com/user-attachments/assets/c30d7c81-2987-46d6-a8fd-cd24a10abe2d)

 The scan revealed serval open ports, including an FTP port (2121), which I was able to access using the credentials I had intially retrieved.
 
#### Example:
![image](https://github.com/user-attachments/assets/3e0e541f-bced-454d-a7b2-ce4c2b8d1e89)
