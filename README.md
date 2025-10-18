
# Brute force attack report

<b>Environment Used</b>: [XAMPP](https://www.apachefriends.org/) + [Damn Vulnerable ](https://github.com/digininja/DVWA) Web App (locally hosted)
<b>Tools Used</b>: [Burp Suite (free version)](https://portswigger.net/burp) 
<b>Additional Item used:</b> [github danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)

## Action Summary
I hosted a Damn Vulnerable Web App server using XAAMP, and performed a brute force password bypass attack locally. Which, utilized a common passwords list from danielmiessler's github repository "SecLists".

## Purpose & Objective
The main objective of this action was to understand how basic brute force attack works, using a personal sandbox, and how secured systems with a password can be compromised.

## Result Overview
The brute-force attack against the DVWA login form was **successful**, demonstrating the vulnerability of systems protected only by weak or common passwords and lacking basic defenses like rate limiting or account lockout.

## Steps I performed in exact chronological order

| Step(s) | Action Summary | Educational/Defensive Purpose |
| :---: | :--- | :--- |
| **1** | **Setup Burp Suite** | **Web Proxy Interception:** Understanding how a proxy like Burp Suite sits between the browser and the server to **inspect, modify, and capture** HTTP requests. This is the foundation for almost all web application security testing. |
| **2-3** | **Initial Login & Intercept** | **Identifying the Target Request:** Learning to recognize the specific HTTP request (the "login packet") that contains the vulnerable parameters (username and password). This packet is the **target** for automated testing. |
| **4-5** | **Test in Repeater & Send to Intruder** | **Request Analysis and Tool Setup:** Using **Repeater** confirms the request structure and allows the tester to observe the server's failure state response (e.g., "Login failed"). Sending to **Intruder** prepares the request for automated, high-volume testing. |
| **6-7** | **Define Payload & Configure Payload** | **Attack Configuration (Payloads and Positions):** This teaches how to precisely define the parts of the request (the **position**) that need to be systematically changed (the **payload**). Using a password list (**SecLists**) demonstrates a **dictionary attack**—a common real-world threat. |
| **8-9** | **Analyze & Verify Success** | **Identifying the Success Indicator:** The crucial learning point is how to reliably **differentiate a successful response from a failed one**. Attackers often rely on subtle differences, such as a change in **HTTP response length** or the presence of specific keywords/redirection headers, to automate the identification of a successful credential. |
