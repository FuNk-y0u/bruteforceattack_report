
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

Step,Action,Description,Purpose
1,Setup Burp Suite,Open browser through Burp Suite and forward any unwanted requests.,To intercept the login packet.
2,Initial DVWA Login,"Login to DVWA dashboard at http://localhost/dvwa/login.php with ""admin"" and ""password"" to gain access.",To access the Brute Force section in the admin panel.
3,Navigate & Intercept,"Navigate to the ""Brute Force"" tab and input ""admin"" and a random password into the login form.",To capture the target login packet for the attack.
4,Test in Repeater,"Right-click the intercepted packet and choose ""Send to Repeater"" to test the login request.",To test the login packet and understand the structure of the server's response.
5,Send to Intruder,"Right-click the request in Repeater and choose ""Send to Intruder.""",To prepare for replicating and performing the brute force attack.
6,Define Position,"In the Intruder ""Positions"" tab, select the value for the ""password"" field and click ""Add \S"" to set the payload marker.",To instruct Burp Suite which value to change and iterate over during the attack.
7,Configure Payload,"Navigate to ""Payloads"" and paste the compromised password list from the SecLists repository.",To utilize common passwords for the dictionary-based brute force attack.
8,Analyze Response Length,"Start the attack and check the response length column. Identify the anomalous response length (e.g., 50 bytes), which is significantly smaller than failed attempts (~2000 bytes).","To quickly identify the entry that caused a different server reaction, indicating a possible successful login."
9,Verify Success,Click on the anomalous response and inspect the body/headers for text that confirms successful login or redirection.,To verify that the password identified is indeed the correct credential.
