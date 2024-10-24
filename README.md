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

 At this point, I was able to access the directory as the root user. After gaining access, I listed the contents using the ![image](https://github.com/user-attachments/assets/17765708-00bb-44a5-82c4-f43d9de0867a)
command and found several ![image](https://github.com/user-attachments/assets/203cbf94-1b6e-45c6-8178-0478a93053fe) files. Since several of the files were empty, I used the ![image](https://github.com/user-attachments/assets/c37d57b0-efd6-49b9-becb-93813c7b9a13) command to attempt reading all the files at once. Results now displayed new credentials.

#### Example:
![image](https://github.com/user-attachments/assets/cc0ecaa2-f211-49b7-8045-403cf22ab809)

 At this stage, I used ![image](https://github.com/user-attachments/assets/8f7694df-9099-4d90-b8ce-d7d995582df9) with the new credentials to check for available shares. After the results were displayed, I noticed that the ![image](https://github.com/user-attachments/assets/6fcf2198-6bd8-47aa-8b54-11c9d177135a) disk type was available under ![image](https://github.com/user-attachments/assets/3fa0bfbf-cc52-4580-8fdb-df1d77889dd6). I then use the ![image](https://github.com/user-attachments/assets/56117e5b-5ddc-49b9-96ac-578c3308adb8) command to further explore the share. 

#### Example:
![image](https://github.com/user-attachments/assets/899a5776-b703-4eff-9ae5-9ba363a9fa41)

 At this point, I used the ![image](https://github.com/user-attachments/assets/c02a2bf3-221a-4e30-9368-5fc17a35c154) command within the SMB share, which revealed an ![image](https://github.com/user-attachments/assets/1f55ee56-5f3f-4c52-b04b-0bf624a6933f) file. I then used the ![image](https://github.com/user-attachments/assets/a1dfd824-5a5b-4a44-8229-0fdd5651257c) file command to read the file, which provided a different set of login credentials.

 #### Example:
 ![image](https://github.com/user-attachments/assets/e026fc0b-251a-4e1d-bf62-b27e1b40240b)

 Lastly I used ![image](https://github.com/user-attachments/assets/56a4de20-f287-4289-8db2-628f36f4c4f7) command-line which allows me to access Windows desktops and applications remotely from various platforms. 

#### Example: 
![image](https://github.com/user-attachments/assets/70ab544c-fb88-4d15-abe5-ab6bdb289000)

 At this point, using the last retrieved credentials, I opened MSSQL with administrator privileges by right-clicking the icon and selecting 'Run as administrator.' With the final login credentials I received, I successfully gained access. From there, I navigated to 'Database,' then 'Accounts,' to view the 'Tables' folder. Once I reached that folder, I right-clicked on 'dbo.devsacc' and selected 'Edit Top 200 Rows". 

#### Example:
![image](https://github.com/user-attachments/assets/68f3dae5-72b8-48aa-a757-7084f009b161)


 From this point, all credentials are displayed. After a few seconds of scrolling, I found the credentials for "Papa Bear", which were created by the client for this vulnerability check.
##### Example:
![image](https://github.com/user-attachments/assets/71b4939e-5c80-43b3-8079-a797e8f13f7f)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Server 3:
 As before, I began by using Nmap with the command ![image](https://github.com/user-attachments/assets/58811810-e3dc-4938-a29d-86f00c0727ce) to check for open ports. While I found a few open ports, none provided useful information. I then decided to explore other options, and the UDP scan revealed more valuable insights.

#### Example:
![image](https://github.com/user-attachments/assets/ded1ab5e-b0ba-4c00-8ce0-62ab1c830e72)

 Next, I began enumerating ![image](https://github.com/user-attachments/assets/368f98b1-2924-43f7-bd38-e7081fe8e758) using the command ![image](https://github.com/user-attachments/assets/e6b35b59-df13-422d-b474-0ad72cb9c4a4). This command provide me with login credentials that I could use.

#### Example: 
![image](https://github.com/user-attachments/assets/9ac5d15a-7740-4c72-a0e0-a1506fd89ba5)

Using the credentials, I intially tried enumerating with ![image](https://github.com/user-attachments/assets/3e44f4e2-b902-4372-ae07-a6329cc943c8), but that was unsuccessful. I then switched to ![image](https://github.com/user-attachments/assets/1f1ff001-28a7-47b7-bf42-a65a17ca4523) using the command ![image](https://github.com/user-attachments/assets/35d7c6fd-5775-4b97-a379-ed00cbbe3536). After running several commands, I was able to retrieve the ![image](https://github.com/user-attachments/assets/810e7642-d555-487b-b38a-669a698655aa).

#### Example:
![image](https://github.com/user-attachments/assets/c11c1453-94af-47bd-8c57-e352a9878876)


I used ![image](https://github.com/user-attachments/assets/686510a3-2d5e-4e11-a377-de16289061f6) command to save the ![image](https://github.com/user-attachments/assets/3a3dcfcb-17d1-4221-b406-79156fd2452a). After saving it, I ran ![image](https://github.com/user-attachments/assets/87026b59-e18b-480b-89a0-a3a4693b442d), which allowed me to follow up the command ![image](https://github.com/user-attachments/assets/23151189-d3fb-4bc6-963e-177ef7a0ff9f). This granted me access with the credetials I had obtained earlier. During enumeration, I discovered the ![image](https://github.com/user-attachments/assets/4fd5f8c7-a5a0-47d5-8ca8-ad654b54d3aa) file. Upon reviewing the file, I found that the user I logged in as had previously used ![image](https://github.com/user-attachments/assets/01c0d965-026f-4bf1-b6fe-3a0711c16e63). 

#### Example:
![image](https://github.com/user-attachments/assets/d5eb3719-aa2e-4bf4-9d49-d9d0f699bf02)

Since I already had the credentials, I could now delve deeper into the history to enumerate SQL queries and uncover the ![image](https://github.com/user-attachments/assets/181cd0e7-2bc9-4917-8bd9-8f6b2cb23db7) credentials by executing a few additional commands. 

#### Example:
![image](https://github.com/user-attachments/assets/d94376cb-2cdb-4d3f-9864-80b7c707e92d)







