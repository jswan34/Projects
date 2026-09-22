
## Attempting lab ToolsRus on THM

Practice using tools such as dirbuster, hydra, nmap, nikto and metasploit

Your challenge is to use the tools listed below to enumerate a server, gathering information along the way that will eventually lead to you taking over the machine.

This room will introduce you to the following tools: 

Dirbuster
Hydra
Nmap
Nikto
Metasploit

Questions:
##
1.) What directory can you find, that begins with a "g"?

Scan with DirBuster, where -u = target -w = wordlist to use
![image.png](https://share.jotbird.com/images/e3914008-9028-4c66-8d02-323c7868e0ad.png)
Found Guidelines

2.) Whose name can you find from this directory?

Pull the website with guidelines subdomain via wget
![image.png](https://share.jotbird.com/images/040f0f68-6a22-470a-aa11-4198c2b731ba.png)
Found the name Bob

3.) What directory has basic authentication?

From Q1 screenshot we know that the "protected" subdomain has authentication. Confirmed by trying to access website
![image.png](https://share.jotbird.com/images/f5451ac5-82b6-4c9c-9791-07e25caa212f.png)

4.) What is bob's password to the protected part of the website?

Can brute force the password with hydra

-l = username, -P = password list to reference, /protected = subdomain we want
![image.png](https://share.jotbird.com/images/ca54fd77-3928-4e14-a14b-780d6c5ee389.png)
Password for Bob is "bubbles"

5.) What other port that serves a webs service is open on the machine?

Search the website via Nmap to see what ports are open
-sV = tells us service and version on ports, -p- = full port scan, not just commonly used
![image.png](https://share.jotbird.com/images/1f347a74-11e0-4157-b14a-1bd5b130c641.png)
Can see that port 1234 is open

6.) What is the name and version of the software running on the port from question 5?

![image.png](https://share.jotbird.com/images/b2df7139-a0d2-499e-8696-2eb096d59fc3.png)
Apache Tomcat/7.0.88

7.) Use Nikto with the credentials you have found and scan the /manager/html directory on the port found above. How many documents?

-o = output saved to .txt document for easier readability
![image.png](https://share.jotbird.com/images/1675cc8c-8b1b-4d49-bc5f-3cc4b1e99021.png)
##### I found 4 services outlined with the 397, 5646, 3092, 3233 responses. However this wasn't registering as the correct answer. After digging into other's write-ups, I found that the installed version of Nikto on this VM isn't able to detect the last one.


8.) What is the server version?

 ![image.png](https://share.jotbird.com/images/cd6837ea-aa27-42dc-aaa7-f6346d967d6b.png)
 Apache/2.4.18
 
9.) What version of Apache-Coyote is this service using?

Same Nmap scan as last question, 1.1

10.) Use Metasploit to exploit the service and get a shell on the system. What user did you get a shell as?

First we need to establish what exploit we're going to use. Since this is a Tomcat server we're attacking at port 1234, we're looking for Tomcat in the listing
![image.png](https://share.jotbird.com/images/364d98d0-4cb5-45bd-a00d-df3817198911.png)
#### 75 total exploits would be a lot to sift through and try, however the write-up I referenced earlier linked to an article that recommended exploit #13 for this scenario. https://www.rapid7.com/db/modules/exploit/multi/http/tomcat_mgr_deploy/
Load the payload #18, then set the target http, port, username, password, and source IP
![image.png](https://share.jotbird.com/images/1d90818e-6d47-4dfe-9adb-6b06d3c307b2.png)
Server username: root
![image.png](https://share.jotbird.com/images/4301d81e-c460-4c1d-81f6-1573c1bd3d55.png)

11.) What flag is found in the root directory?

![image.png](https://share.jotbird.com/images/96f1514a-e197-4b96-8300-398ed10c55bf.png)
flag = ff1fc4a81affcc7688cf89ae7dc6e0e1

#### And we're done!
