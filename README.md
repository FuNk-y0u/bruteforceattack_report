
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

Setup Burp Suite
Action: Open the browser through Burp Suite and forward any unwanted requests.
Description: Configure Burp as your browser proxy so traffic from the target site is routed through Burp.
Purpose: To intercept the login packet.
Command / Image:
![Burp Proxy Setup](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step1.png)

Initial DVWA Login
Action: Log in to the DVWA dashboard with valid credentials (admin, password).
Description: Authenticate to gain access to the admin area.
Purpose: To access the Brute Force section of the admin panel.
Command / Image:
![DVWA Login Page](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step2.png)

Navigate & Intercept
Action: Go to the Brute Force tab and submit the username (admin) with a random password while intercept is on.
Description: Capture the login request that the web app sends.
Purpose: To capture the target login packet for the attack.
Command / Image:
![Intercepting Login](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step3.png)

Test in Repeater
Action: Send the intercepted login request to Repeater and send it repeatedly to observe responses.
Description: Inspect the server’s typical “Login failed” response and response structure.
Purpose: To test the login packet and understand how the server responds.
Command / Image:
![Packet in Repeater](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step4.png)

Send to Intruder
Action: From Repeater (or Proxy), send the request to Intruder.
Description: Prepare the captured request for automated payload insertion.
Purpose: To replicate and perform the brute-force attack.
Command / Image:
![Sending to Intruder](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step5.png)

Define Payload Position
Action: In Intruder → Positions, highlight the password value and set it as the payload marker.
Description: Tell Intruder which part of the request to vary.
Purpose: To instruct Burp which value to change and iterate over.
Command / Image:
![Intruder Position Set](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step6.png)

Configure Payload
Action: In Intruder → Payloads, load the compromised password list (e.g., from the SecLists repository).
Description: Provide the dictionary of candidate passwords for the attack.
Purpose: To use common passwords for a dictionary-based brute-force attempt.
Command / Image:
![Loading SecLists Payload](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step7.png)

Analyze Response Length
Action: Start the Intruder attack and watch the results table, especially the Length column.
Description: Compare response sizes to spot anomalies.
Purpose: To quickly identify an entry that causes an unusual server reaction (e.g., a ~50-byte response vs. ~2000 bytes for failures).
Command / Image:
![Analyzing Response Length](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step8.png)

Verify Success
Action: Click the anomalous response, inspect headers/body for success indicators (redirect, welcome text, different body).
Description: Confirm that the differing response corresponds to a successful login.
Purpose: To verify the discovered password is correct.
Command / Image:
![Verifying Successful Login](https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step9.png)
