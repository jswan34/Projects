Q1 - How many services are running under port 1000?

We'll do a quick nmap scan to see what ports are open for us.
![image.png](images/img_1791862620570_c477e37494dd48.png)
Looks like 21, 80, and 2222 are open. So 2 ports below 1000.
Answer: 2

Q2 - What is running on the higher port?
Should be ftp but the room registers it as ssh
Answer: ssh

Q3 - What's the CVE you're using against the application?

Next we'll see what other sites are hiding on the target IP. Gobuster works great for this.
# NOTE: Had to reboot the target machine after it kept crashing hence the different IP.
![image.png](images/img_1791863304185_77f9d51bb8a4d.png)
So now we have another directory in the form of /simple. Going to the site leads us to a site talking about pen-testing. The major note is hiding at the bottom left corner - the server is hosted on a CMS Made Simple v2.2.8 server - which a quick google search shows is vulnerable to a specific script injection.
![image.png](images/img_1791863474227_e9489f0a4f95f8.png)

https://nvd.nist.gov/vuln/detail/cve-2019-9053

https://packetstorm.news/files/id/152356

Q4 - To what kind of vulnerability is the application vulnerable?

Answer: CVE-2019-9053

Q5 - What's the password?

Using that info we can plug the script we found above into a python script to run. Note this did take a bit of modification that I had to look up to prevent the script from crashing out of the box.
![image.png](images/img_1791863832092_11037bb1ba8d38.png)

While we didn't get the password, we did get a username. Hydra to the rescue.
![image.png](images/img_1791864114121_a09e6873bb5138.png)

And now we've got a full login. Time to remote shell into the the machine.
Answer: secret

Q6 - Where can you login with the details obtained?

Answer: ssh

Q7 - What's the user flag?

![image.png](images/img_1791864237670_767e1548ef16.png)
It's good to remember that we're using port 2222 rather than the traditonal port 22
![image.png](images/img_1791864333358_affe3a043cc44.png)

Answer: G00d j0b, keep up!

Q8 - Is there any other user in the home directory? What's its name?
![image.png](images/img_1791864423442_d5089f2693d92.png)

Answer: sunbath

Q9 - What can you leverage to spawn a privileged shell?

First we'll check what we have access to as our current user. "sudo -l" gives us a list of all available root commands for us. Which leaves us vim, a text editor.
![image.png](images/img_1791864594523_26db12f023dd3.png)

Answer: vim

Q10 - What's the root flag?

When launching vim we can use the -c flag to run any system commands we give it prior to opening the editor, and since our user has root access with vim we can put ourselves into the root folders.
![image.png](images/img_1791864709360_7d08524d40e25.png)

![image.png](images/img_1791864921785_de3f20376b1d08.png)

Finally we check the root directory for our flag.
Answer: W3ll d0n3. You made it!

And that concludes this room!
