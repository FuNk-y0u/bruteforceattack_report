
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

Step| Action | Command / Screen Shot| Description| Purpose | 
--- | --- | --- | --- |--- |--- |--- |--- |--- |--- |--- |---
1| Setup Burp Suite ||Open browser through burp suite & forward any unwanted request |To intercept login packet
2| Login to DVWA admin dashboard | |Login to DVWA dashboard through http://localhost/dvwa/login.php with "admin", "password" as username and password respectively.| To access brute force attack section in the admin panel
3| Navigate to 	"brute force" tab| |Navigate to brute force tab & add "admin" and a random password respectively on the login form| To intercept the login packet 
4| Send the captured packet to repeater| | Right click the packet and  choose "send to repeater" and identify the returned response| To test out the login packet
5| Send the packet to the intruder|  |Right click anywhere on the repeater tab and choose "send to intruder"| To replicate & perform brute force attack through intruder
6| Add positions in intruder| |Select the payload for "password" and click on add position| To make burp suite know which value to change and iterate over
7| Add in compromised passwords| | Navigate to "pay load configuration" and paste in your compromised password list from  [github danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)| To utilize common passwords for brute force attack
8| Check the length of response| |The response over here is 50, which is < 2000~ of other response, hence possible correct data | To identify which password is correct.
9| Check response of anomalous response| |Click on the response and check for any text to verify for correct password| To check whether the password is correct 
