---
layout: post
title: Dissection of a Client-Side Attack / Broken IAM
---
![](/images/2021-3-22-ClientSA/0.png)

I have seen a recent trend in applications lacking server-side validation, and obscuring things assuming nobody will find out. The purpose of this article is to show how it is possible to evade these techniques, and find hidden paths and parameter through enumerations, which will lead to compromise of integrity, confidentiality, and availability.     

Client-side controls of this kind are usually easy to circumvent; it is possible to enter a benign value, intercept the submission with a proxy, and modify the data, and perform enumeration to bypass controls and compromise data. I will use example from couple of recent penetration tests I have performed.

**Case 1:**

***Background***

The penetration testing was performed on production environment with restricted access for my user account. 

Proof of Concept

I always emphasize the importance of enumeration and you will see why in a second.

I started off by brute forcing directory with a small word list to keep the noise down, since it is a production server. 

By default all directory brute forcing tool uses GET request to find out if there are directories in the provided URL with the help of a word list by returning status code (200 – success, 302 – redirection, 404 – not found etc.). 

![](/images/2021-3-22-ClientSA/1.png)

As you can see above, the index.aspx returned 500 internal error, which essentially means the server didn’t like something we sent. So, In BurpSuite, I changed the request method of “index” to POST and forwarded the request:

![](/images/2021-3-22-ClientSA/2.png)

Now the server says, the request is good but not good enough.

So, I decided to enumerate through the webapp, and I found my user id. I used my user ID as a parameter body in the POST request, which returns a 302 status, and redirected me to my session

![](/images/2021-3-22-ClientSA/3.png)

So why don’t we change the user ID value to something random? Yes, you guessed it, due to broken IAM, I can use this parameter pollution vulnerability to hijack user accounts by enumerating the “userID” parameter.

![](/images/2021-3-22-ClientSA/4.png)
![](/images/2021-3-22-ClientSA/5.png)
![](/images/2021-3-22-ClientSA/6.png)

As seen above, all users accounts can be hijacked, this possess tremendous confidently and integrity issues, and if an attacker changes the user password somehow, then this can cause availability issue as well.


**Case 2:**

***Background***

The Penetration Test was performed on an externally available web application that executes financial transactions. This specific application has two roles:
1.	Impersonation Account (readOnly for customer service people to see customer’s account, this account should not be able to execute transaction’s) 
2.	Regular Account (Normal user account which can execute transaction’s) 

I was given an impersonation account to test and make sure that this account cannot execute any transactions

Proof of Concept:

At the first glance, the application had everything hidden/disabled on the account. I couldn’t do anything really, but like “offensive Security” always say “try harder”;

My main objective in this small project is to bypass the control in place.


![](/images/2021-3-22-ClientSA/7.png)

This is the page where I can put contribution amount; However, the submit button is missing. So how do we invoke this request?

I need the help of keyboard; I just need to put the amount in and click “Enter”, that will invoke a validation request:


![](/images/2021-3-22-ClientSA/8.png)

And we land in this page:

![](/images/2021-3-22-ClientSA/9.png)

This page is missing some buttons, where we can click and confirm to invoke another request to “confirm” all the details.

I was really stuck at this point; how can I possibly invoke the next request? if I refresh, I can only invoke the same request with “GET” method.

I decided to look what is happening under the hood. I noticed the next request is a POST request to “confirmation.do”, the question remained same, “how can I invoke it”.



![](/images/2021-3-22-ClientSA/10.png)

Maybe, I can create a submit button?

Inject the payload: 

```
“<input type="submit" tabindex="2" value="Submit"
class="button">” 
```

![](/images/2021-3-22-ClientSA/10.png)

Now is the easy part, click on submit:

![](/images/2021-3-22-ClientSA/12.png)


![](/images/2021-3-22-ClientSA/13.png)
![](/images/2021-3-22-ClientSA/14.png)

This is a clear case of access control bypass leading to integrity issues. The developer tried to hide the submit/confirm button from the user, so the end user won’t be executing the transaction. The lack of server-side validation is the main reason why this bypass is possible. 


Conclusion 

Client-side validation and obscuring etc. are good as long as server-side validation is executed after client-side validation. A user or hacker can submit the data through different channels, as we saw in case 2. These cases have huge impact on confidently, integrity and availability. 
 

