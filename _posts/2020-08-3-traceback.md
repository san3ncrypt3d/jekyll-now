---
layout: post
title: Traceback walkthrough HTB 
---


![](/images/2020-08-3-traceback/0.png)

Traceback is a vulnerable Linux box. 

Like usual, I spin up an ec2 instance and initiated an nmap scan:

![](/images/2020-08-3-traceback/1.png)


I see a webserver on port 80 so let’s use a browser to see what is on there.

![](/images/2020-08-3-traceback/2.png)

Let’s inspect the page source to see if we can find any hints:


![](/images/2020-08-3-traceback/3.png)


Haha, interesting !! let’s just google it :

![](/images/2020-08-3-traceback/4.png)



![](/images/2020-08-3-traceback/5.png)

We found a bunch of web shell. I am going to use the name of the webshell to do a directory brute force to find the hidden web shell.


![](/images/2020-08-3-traceback/6.png)


Use the custom made list to brute force.

![](/images/2020-08-3-traceback/7.png)


Okay, we found a webshell named “smevk.php” which have default username and password set to “admin”

![](/images/2020-08-3-traceback/8.png)


![](/images/2020-08-3-traceback/9.png)


Now, we can upload our public key using the webshell to ssh into the box since port 22 is open (ref: nmap scan)

![](/images/2020-08-3-traceback/10.png)


![](/images/2020-08-3-traceback/11.png)


![](/images/2020-08-3-traceback/12.png)


Now ssh into the box using the private key.

![](/images/2020-08-3-traceback/13.png)



As you can see, we are webadmin. We need to escalate our privilege to view the user flag.


In webadmin’s home directory, there are some files. We will check the content of the files for clues to escalate privilege. 
![](/images/2020-08-3-traceback/14.png)


![](/images/2020-08-3-traceback/15.png)




![](/images/2020-08-3-traceback/16.png)


From this we can see the user sysadmin uses lua, we can look for lua sudo abuse to escalate privilege.

https://gtfobins.github.io/gtfobins/lua/#sudo


![](/images/2020-08-3-traceback/17.png)


Now you can create a new *.lua script, and then imitate .bash_history to escalate privilege.execute the command

![](/images/2020-08-3-traceback/18.png)


We created a lua script named “hack.lua” and executed it as sysadmin


![](/images/2020-08-3-traceback/19.png)


Wooo !!! we got user.



Alright now let’s move on to hack the root user. After looking around for some time I used the pspy tool to monitor the programs being executed in the system and I found something interesting

![](/images/2020-08-3-traceback/20.png)

![](/images/2020-08-3-traceback/21.png)

/bin/sh -c sleep 30 ; /bin/cp /var/backups/.update-motd.d/* /etc/update-motd.d/

It can be seen that the system copies the files in /var/backups/.update-motd.d/ to /etc/update-motd.d/ every 30 seconds. After Googling the function of update-motd.d, I found that, after each successful SSH login, the command in the 00-header file will be executed. 


So now all we have to do is add the command to read the root.txt file on the 00-header and after a successful login, the root.txt file will be displayed.

![](/images/2020-08-3-traceback/22.png)

![](/images/2020-08-3-traceback/23.png)


![](/images/2020-08-3-traceback/24.png)


Now that we have added the command, lets log out of the system and ssh back in:

![](/images/2020-08-3-traceback/25.png)

8c3d9b75d897d321b9b13a19f6e5f6e1

Wooo there you go, we have rooted the machine successfully.
