---
layout: post
title: Recon - Azure Pentesting!
---
![](/images/2021-12-30-AzureRecon/0.png)


The Azure Kill Chain consist of multiple phases:
•	Recon
•	Initial Access 
•	Enumeration 
•	Privilege escalation 
•	Defense evasion 
•	Lateral Movement 
•	Persistence 
•	Data Exfiltration 

This writeup will be about the Recon phase:

Once we start an assessment, some of the things we want to know are if the org uses azure tenant, if they do, the name, ID, Authentication type, Domains, services used by the org etc.
So, how do we know if the target organization is using Azure tenant? the simple answer is by knowing the name of the org or the domain.
We can use this link to check if company “san” is using azure AD
[https://login.microsoftonline.com/getuserrealm.srf?login=USERNAME@san.onmicrosoft.com&xml=1](https://login.microsoftonline.com/getuserrealm.srf?login=USERNAME@san.onmicrosoft.com&xml=1):

![](/images/2021-12-30-AzureRecon/2.png)

Now since it says “Managed” we know this organization is using azure AD, now we you replace “san” with an org that does not use we get the below:

![](/images/2021-12-30-AzureRecon/3.png)

This can also be achieved from a tool called ADDInternals  [https://github.com/Gerenios/AADInternals]( https://github.com/Gerenios/AADInternals)

We can use this tool to get further information
```
Import-Module ADDInternals.psd1 -Verbose
```
•	Get tenant name, authentication, brandname etc:
```
Get-ADDIntLoginInformation -Username root@san.onmicrosoft.com
```
•	Get tenant ID

```
Get-ADDIntTenantID -Domain san.onmicrosoft.com 
````

•	Get all the Information’s:
```
Invoke-AADIntReconAsOutsider -DomainName san.onmicrosoft.com
```

Another amazing tool that I use often for security assessment in azure is [MicroBurst]( https://github.com/NetSPI/MicroBurst).

This tool uses AzureAD, AZ, AzureRM and additional RestAPI calls!

If you want to enumerate services in azure you can use this tool, what the tool does is finding DNS records for permutations on a base word that you provide.

For example:
```
Invoke-EnumerateAzureSubDomains -Base san -Verbose
```
The above command will use san as a subdomain and run it against azure service such as: azurewebsites.net, scm.azurewebsites.net, p.azurewebsites.net	, cloudapp.net, file.core.windows.net, blob.core.windows.net	etc.

There are times when you will run into a dev site, or a pre-production site that was not meant to be exposed to the internet. Here, you may have luck finding application security issues, or sensitive information that is not supposed to be internet facing. There are other instances where you will be able to find public facing storage accounts with sensitive information’s, or SharePoint, Email, or hosted domain.


