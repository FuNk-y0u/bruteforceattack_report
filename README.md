
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

| Step | Action | Description | Purpose | Command / Image |

| :---: | :--- | :--- | :--- | :---: |

| **1** | **Setup Burp Suite** | Open browser through Burp Suite and forward any unwanted requests. | To intercept the login packet. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step1.png" alt="Burp Proxy Setup" width="100"/> |

| **2** | **Initial DVWA Login** | Log in to the DVWA dashboard with valid credentials (`admin`, `password`) to gain access. | To access the Brute Force section of the admin panel. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step2.png" alt="DVWA Login Page" width="100"/> |

| **3** | **Navigate & Intercept** | Navigate to the **"Brute Force"** tab and input the username (`admin`) and a random password into the login form. | To capture the target login packet for the attack. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step3.png" alt="Intercepting Login" width="100"/> |

| **4** | **Test in Repeater** | Send the intercepted packet to **Repeater** to test the request and observe the server's typical "Login failed" response. | To test the login packet and understand the structure of the server's response. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step4.png" alt="Packet in Repeater" width="100"/> |

| **5** | **Send to Intruder** | Send the request from Repeater to **Intruder**. | To prepare for replicating and performing the brute force attack. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step5.png" alt="Sending to Intruder" width="100"/> |

| **6** | **Define Payload Position** | In the Intruder **"Positions"** tab, select the value for the **"password"** field and set it as the payload marker. | To instruct Burp Suite which value to change and iterate over. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step6.png" alt="Intruder Position Set" width="100"/> |

| **7** | **Configure Payload** | Navigate to the **"Payloads"** tab and paste the compromised password list from the **SecLists** repository. | To utilize common passwords for the dictionary-based brute force attack. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step7.png" alt="Loading SecLists Payload" width="100"/> |

| **8** | **Analyze Response Length** | Start the attack and analyze the **Length** column in the results. Identify the anomalous length (**~50 bytes**), which is significantly smaller than the failed responses (**~2,000 bytes**). | To quickly identify the entry that caused a different server reaction, indicating a possible successful login. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step8.png" alt="Analyzing Response Length" width="100"/> |

| **9** | **Verify Success** | Click on the anomalous response and inspect the body/headers for text that confirms successful login or redirection. | To verify that the discovered password is the correct credential. | <img src="https://raw.githubusercontent.com/FuNk-y0u/bruteforceattack_report/refs/heads/main/images/step9.png" alt="Verifying Successful Login" width="100"/> |
