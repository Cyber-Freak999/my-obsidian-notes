## Web Timing and Race Conditions

Conventional web applications are relatively easy to understand, identify, and exploit. If there is an issue in the code of the web application, we can force the web application to perform an unintended action by sending specific inputs. These are easy to understand because there is usually a direct relationship between the input and output. We get bad output when we send bad data, indicating a vulnerability. But what if we can find vulnerabilities using only good data? What if it isn't about the data but how we send it? This is where web timing and race condition attacks come into play! Let's dive into this crazy world and often hidden attack surface!   

In its simplest form, a web timing attack means we glean information from a web application by reviewing how long it takes to process our request. By making tiny changes in what we send or how we send it and observing the response time, we can access information we are not authorised to have.

Race conditions are a subset of web timing attacks that are even more special. With a race condition attack, we are no longer simply looking to gain access to information but can cause the web application to perform unintended actions on our behalf.  

Web timing vulnerabilities can be incredibly subtle. Based on the following [research](https://portswigger.net/research/listen-to-the-whispers-web-timing-attacks-that-actually-work), response time differences ranging from 1300ms to 5ns have been used to stage attacks. Because of their subtle nature, they can also be hard to detect and often require a wide range of testing techniques. However, with the increase in adoption of HTTP/2, they have become a bit easier to find and exploit.

## The Rise of HTTP/2

HTTP/2 was created as a major update for HTTP, the protocol used for web applications. While most web applications still use HTTP/1.1, there has been a steady increase in the adoption of HTTP/2, as it is faster, better for web performance, and has several features that elevate the limitations of HTTP/1.1. However, if implemented incorrectly, some of these new features can be exploited by threat actors using new techniques.

A key difference in web timing attacks between HTTP/1.1 and HTTP/2 is that HTTP/2 supports a feature called single-packet multi-requests. Network latency, the amount of time it takes for the request to reach the web server, made it difficult to identify web timing issues. It was hard to know whether the time difference was due to a web timing vulnerability or simply a network latency difference. However, with single-packet multi-requests, we can stack multiple requests in the same TCP packet, eliminating network latency from the equation, meaning time differences can be attributed to different processing times for the requests. This is explained more in the animation below:

![an animation showing how HTTP/1 and HTTP/2 deal with timing differences](https://assets.tryhackme.com/additional/aoc2024/gifs/Webtiming2.gif)

With network latency a thing of the past, only server latency remains, making it significantly easier to detect timing issues and exploit them to recover sensitive information.  

## Typical Timing Attacks

Timing attacks can often be divided into two main categories:

- Information Disclosures

Leveraging the differences in response delays, a threat actor can uncover information they should not have access to. For example, timing differences can be used to enumerate the usernames of an application, making it easier to stage a password-guessing attack and gain access to accounts.

- Race Conditions

Race conditions are similar to business logic flaws in that a threat actor can cause the application to perform unintended actions. However, the issue's root cause is how the web application processes requests, making it possible to cause the race condition. For example, if we send the same coupon request several times simultaneously, it might be possible to apply it more than once.

For the rest of this task, we will focus on race conditions. We will take a look at a `Time-of-Check to Time-of-Use (TOCTOU)` flaw. Let's use an example to explain this, as shown in the animation below:

![Demonstrating a Time of Check to Time of Use vulnerability caused by a race condition](https://assets.tryhackme.com/additional/aoc2024/gifs/Webtiming3.gif)

When the user submits their coupon code, in the actual code of the web application, at some point, we perform a check that the coupon is valid and hasn't been used before. We apply the discount, and only then do we update the coupon code to indicate that it has already been used. In this example, between our check if the coupon is valid and our update of the coupon being used, there are a couple of milliseconds where we apply the coupon. While this might seem small, if a threat actor can send two requests so close together in time, it might happen that before the coupon is updated in request 1, it has already been checked in request 2, meaning that both requests will apply the coupon!  

## Winning the Race

Now that you understand basic concepts related to race conditions, let's explore how this vulnerability occurs in a real-world scenario. For this, we will take the example of the Warville banking application hosted on `http://MACHINE_IP:5000/`. This application allows users to log in and transfer funds between accounts.

## Intercepting the Request

Before we start intercepting requests, we need to configure the environment so that, as a pentester, all web traffic from our browser is routed through Burp Suite. This allows us to see and manipulate the requests as we browse. 

We will use Burp Suite, a powerful web vulnerability scanner, to intercept and modify requests for this exploitation. You can access Burp Suite in the `AttackBox`. On the desktop of the AttackBox, you will see a Burp Suite icon as shown below:

![Burp suite icon](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728456762740.png)  

Once you click the icon, Burp Suite will open with an introductory screen. You will see a message like "**Welcome to Burp Suite**".  Click on the `Next` button. 

![Burp suite splash screen](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728457165300.png)  

On the next screen, you will have the option to `Start Burp`. Click on the `Start Burp` button to start the tool.

![Burp suite startup setting screen](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728457184817.png)  

Once Burp Suite has started, you will see its main interface with different tabs, such as `Proxy`, `Intruder`, `Repeater` and others.

![burp suite dashboard with options](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728630460840.png)  

Inside Burp Suite, click the `Settings` tab at the top right. You will see Burp's browser option available under the `Tools`. Enable `Allow Burp's browser to run without a sandbox option` and click on the **close icon** on the top right corner of the `Settings` tab as shown below:

![Enabling Burp browser settings](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728459438650.png)  

After allowing the browser to run without a sandbox, we would now be able to start the browser with pre-configured Burp Suite's proxy. Open the browser by clicking the `Open browser` located in the `Proxy` -> `Intercept` tab and browse to the URL `http://MACHINE_IP:5000`, so that all requests are intercepted: 

![opening browser with in Burp suite](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728625481652.png)  

Once you browse the URL, all the requests are intercepted and can be seen under the `Proxy->HTTP history` tab.

![bank app login page](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728626881220.png)  

## Application Scanning

As a penetration tester, one key step in identifying race conditions is to validate functions involving multiple transactions or operations that interact with shared resources, such as transferring funds between accounts, reading and writing to a database, updating balances inconsistently, etc.

For this example, we will log in to the Warville banking application using the credentials:

![THM key](https://tryhackme-images.s3.amazonaws.com/user-uploads/63588b5ef586912c7d03c4f0/room-content/be629720b11a294819516c1d4e738c92.png)

|   |   |
|---|---|
|**Account No**|110|
|**Password**|tester|

Once logged in, you will see the following dashboard that will contain the following two primary functions:

![bank app dashboard showing balance](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728625199276.png)  

You will see two functionalities: **logout**, which probably does not involve simultaneous tasks. The next is **fund transfer**, which includes deducting funds from the account and adding them to the other account. As a pentester, this could be an opportunity for an attack.  We will see in detail how, as a pentester, you can test/exploit the vulnerability.  

## Verifying the Fund Transfer Functionality

We will browse the bank application and perform a sample transaction inside the browser. This will generate multiple `GET` and `POST` requests, and whatever request we make will be passed through the Burp Suite. As shown in the figure, our current balance is `$1000`. We will send `$500` to another bank account with the account number `111`, and while doing that, all our requests will be captured in the Burp Suite. 

![bank app transfer fund form](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728627164798.png)  

Click on the Transfer button, and you will see the following message indicating that the amount has been transferred: 

![bank app displaying message after successful transfer](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1733857967255.png)  

Now, let's review the fund transfer `HTTP POST` request logged in the Burp Suite's `HTTP history` option under the `Proxy` tab. 

![Burp suite with intercepted requests](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728627561119.png)  

The above figure shows that the `/transfer` endpoint accepts a POST request with parameters `account_number` and `amount`. The Burp Suite tool has a feature known as `Repeater` that allows you to send multiple HTTP requests. We will use this feature to duplicate our `HTTP POST` request and send it multiple times to exploit the race condition vulnerability. Right-click on the POST request and click on `Send to Repeater`.

![Burp suite with option to send request to repeater](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728627690791.png)

Now, navigate to the `Repeater` tab, where you will find the `POST` request that needs to be triggered multiple times. We can change the `account_number`, from `111`, and the `amount` value from `500` to any other value in the request as well, as shown below:

![Repeater option in Burp Suite](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728627837373.png)  

Place the mouse cursor inside the request inside the Repeater tab in Burp Suite and press `Ctrl+R` to duplicate the tab. Press `Ctrl+R` ten times to have 10 duplicate requests ready for testing.

![duplicate requests in Burp suite](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728628298525.png)  

Now that we have 10 requests ready, we want to send them simultaneously. While one option is to manually click the `Send` button in each tab individually, we aim to send them all in parallel. To do this, click the `+` icon next to `Request #10` and select Create tab group. This will allow us to group all the requests together for easier management and execution in parallel.

![Creating tab group in Burp suite](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728628589380.png)  

After clicking the `Create tab group`, a dialogue box will appear asking you to name the group and select the requests to include. For this example, we will name the group `funds`, select all the requests, and then click the `Create` button, as shown below.

![naming tab group in Burp suite](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728629060003.png)  

Now, we are ready to launch multiple copies of our HTTP POST requests simultaneously to exploit the race condition vulnerability. Select `Send group in parallel (last-byte sync)` in the dropdown next to the `Send` button. Once selected, the `Send` button will change to `Send group (parallel)`. Click this button to send all the duplicated requests in our tab group at the same time, as shown below:

![sending parallel requests in Burp suite](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728629349449.png)  

Once all the requests have been sent, navigate to the `tester` account in the browser and check the current balance. You will notice that the tester's balance is negative because we successfully transferred more funds than were available in the account, exploiting the race condition vulnerability.

![dashboard showing negative balance in bank app](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728629858556.png)  

By duplicating ten requests and sending them in parallel, we are instructing the system to make ten simultaneous requests, each deducting $500 from the `tester` account and sending it to account `111`. In a correctly implemented system, the application should have processed the first request, locked the database, and processed the remaining requests individually. However, due to the race condition, the application handles these requests abruptly, resulting in a negative balance in the tester account and an inflated balance in account `111`.  

## Verifying Through Source Code

Suppose you are a penetration tester with access to the application's source code (as in a white-box testing scenario). In that case, you can identify potential race condition vulnerabilities through a code review. By analysing the code, you can pinpoint areas where multiple database operations are performed without proper transaction handling. Below is the Python code that handles the fund transfer:

```python
 if user['balance'] >= amount:
        conn.execute('UPDATE users SET balance = balance + ? WHERE account_number = ?', 
                     (amount, target_account_number))
        conn.commit()

        conn.execute('UPDATE users SET balance = balance - ? WHERE account_number = ?', 
                     (amount, session['user']))
        conn.commit()
```

  

In the above code, if `user['balance'] >= amount`, the application first updates the recipient's balance with the command `UPDATE users SET balance = balance + ? WHERE account_number = ?`, followed by a commit. Then, it updates the sender’s balance using `UPDATE users SET balance = balance - ? WHERE account_number = ?` and commits again. Since these updates are committed separately and not part of a **single atomic transaction**, there’s no locking or proper synchronisation between these operations. This lack of a **transaction or locking mechanism** makes the code vulnerable to race conditions, as concurrent requests could interfere with the balance updates.