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

 With port 22 open, I was able to access the SSh service and subsequently obtained the SSh private key. I then proceed with ![image](https://github.com/user-attachments/assets/332412b7-468d-4a9f-ba11-39d27f3f9075) command to set permissions for the ![image](https://github.com/user-attachments/assets/8d04228f-2051-4bd1-b9c4-b11a3b1ec405) file. 
 - ![image](https://github.com/user-attachments/assets/99e2ceda-a346-43d6-bfeb-907621cb1bf2) is the command that will change the file permission(s)
 - ![image](https://github.com/user-attachments/assets/40ccca80-30a9-415d-96c8-04634e3cfd05) will set the permission(s) in order for the owner (me) to read and write the file, but no one else can access.
   - Owner: Read and write permission ![image](https://github.com/user-attachments/assets/c696e0df-747f-4f51-ab36-50e29c6e4067)
   - Group: No permission ![image](https://github.com/user-attachments/assets/f29aa300-0f6c-443c-add0-90db53339c85)
   - Others: No permission ![image](https://github.com/user-attachments/assets/4f1a6d6d-e1b4-4dee-a7ae-ab379677e1af)

 Now that permission has been established, I then proceeded with a simple enumeration to obtain files that could be used againsted the company. 

 #### Example:
 ![image](https://github.com/user-attachments/assets/db0196c0-dece-4475-8cd1-9777eb9b4ad1)

 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Server 2:
 As previously with the first server, I began using Nmap to enumerate the second server with the ![image](https://github.com/user-attachments/assets/8839d508-0597-4b17-8a66-d6de516ef59c) command to identify open ports. I identified several open ports, and upon closer inspection, observed that multiple services were running, including RPC, SMB, and NFS.

 #### Example:
![image](https://github.com/user-attachments/assets/6ca57bc7-b997-4a5b-b2aa-3b8f61e89571)

 
 I decided to focus on the NFS service and proceeded by utilizing the ![image](https://github.com/user-attachments/assets/1909f6ba-26f9-4c95-8f0b-7010e8391dfb) command. Result displayed a share named ![image](https://github.com/user-attachments/assets/5fb37c76-efcd-456d-9440-c41e38063cd7). For mounting the share, I created a directory with the ![image](https://github.com/user-attachments/assets/2b219220-2e7d-4494-aeef-4f5bc49bcc72) command and then proceeded using the ![image](https://github.com/user-attachments/assets/459fa55b-19af-4152-adf5-99542267c791) command.

#### Example:
![image](https://github.com/user-attachments/assets/00b5cf8c-f04d-4d71-87fe-ca3c261c92ea)



#### Example:
![image](https://github.com/user-attachments/assets/68f3dae5-72b8-48aa-a757-7084f009b161)

##### Example:
![image](https://github.com/user-attachments/assets/71b4939e-5c80-43b3-8079-a797e8f13f7f)


