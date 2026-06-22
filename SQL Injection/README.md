                                             SQL Injection


# Overview 

In this lab, I explored SQL Injection vulnerabilities using the Metasploitable 2 virtual machine and two intentionally vulnerable web applications: DVWA (Damn Vulnerable Web Application) and Mutillidae. The objective was to understand how SQL Injection attacks work, observe their effects on web applications, and use automated tools such as SQLMap to identify and exploit SQL Injection vulnerabilities.


## Step 1: Log in to Kali Linux and Metasploitable 2

I started both the Kali Linux and Metasploitable 2 virtual machines. I logged into Metasploitable 2.


## Step 2: Verify Network Connectivity

I used the ifconfig command on Metasploitable 2 to determine its IP address. After obtaining the IP address, I used the ping command from Kali Linux to verify connectivity between the two virtual machines.


<img width="496" height="243" alt="image" src="https://github.com/user-attachments/assets/8e40564b-1c33-420c-92b8-82210434dd9a" />



## Step 3: Verify Firefox Proxy Settings

Before accessing the vulnerable web applications, I ensured that no proxy settings were configured in Firefox on Kali Linux.


## Step 4: Access DVWA

I opened Firefox and navigated to:

* https://<Metasploitable-IP>/dvwa/login.php


## Step 5: Log in to DVWA

I logged into DVWA using the following credentials:

Username: admin
Password: password

<img width="452" height="257" alt="image" src="https://github.com/user-attachments/assets/425227b7-63ac-4c04-9602-1c50cd696f1a" />


## Step 6: Perform SQL Injection in DVWA

I selected the SQL Injection module from the DVWA menu and entered an invalid User ID value.

When a normal invalid value is submitted, the application should not return valid user information. However, SQL Injection can manipulate the underlying query to return all records.

A common SQL Injection payload is:

2' OR '1'='1

This modifies the application's SQL statement to create a condition that is always true.

Example vulnerable query:

SELECT first_name, last_name
FROM users
WHERE user_id = '2' OR '1'='1';

Since '1'='1' always evaluates to true, the database returns all available records.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/00f8e4dd-4a49-4b65-8052-a26b0cd6e8d8" />




## Step 7: Explore Mutillidae Security and Hint Settings

I navigated to:

http://<Metasploitable-IP>/mutillidae/

I repeatedly clicked Toggle Security and Toggle Hints to observe how the application behavior changed.

Toggle Security

The application cycles through several security levels:

Level 0 (Hosed) – Completely vulnerable
Higher levels progressively implement security controls

At lower levels, attacks such as SQL Injection are easier to perform because little or no input validation exists. Higher levels introduce filtering and validation mechanisms to reduce vulnerabilities.

Toggle Hints

The hint feature displays educational guidance that helps users identify vulnerabilities and understand exploitation techniques. When disabled, the application no longer provides these clues.


<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/d7724f1c-106b-4b93-9d72-c03f573c6a7f" />



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/829db350-fd05-4225-8ffd-1686d677c148" />




## Step 8: Access User Information Page

I navigated through:

OWASP Top 10 → A1 - Injection → SQLi - Extract Data → User Info

I entered:

Name: admin
Password: cyse-450

Then I selected View Account Details.



## Step 9: Analyze the SQL Query and Error Message

After submitting the information, I examined the SQL query displayed by the application. The application generated an error because it attempted to query a database table that does not exist. Specifically, it referenced the table:

metasploit.accounts

Since the table is missing, the database server returns an SQL error instead of account information. Another observation was that the application displayed a sample query using the password value "password" rather than the password I entered ("cyse-450"). This occurs because Mutillidae intentionally shows predefined example queries for educational purposes.



<img width="815" height="458" alt="image" src="https://github.com/user-attachments/assets/518a408d-a940-42e5-9e89-d08d9080e454" />



## Step 10: Run SQLMap

I executed the provided SQLMap command in the Kali Linux terminal.

SQLMap automatically tested the target application for SQL Injection vulnerabilities and attempted to identify database information.

The tool demonstrated how automated vulnerability assessment tools can significantly speed up the discovery and exploitation of SQL Injection flaws.

SQLMap command execution
SQLMap findings and results


## Step 11: Compare Mutillidae and DVWA

Both DVWA and Mutillidae are intentionally vulnerable web applications designed for cybersecurity education, but they provide different learning experiences.

DVWA
Focuses on common web vulnerabilities.
Provides a straightforward interface.
Includes security levels to demonstrate how defenses affect attacks.
Ideal for practicing individual vulnerability categories.

Mutillidae
Offers a larger variety of attack scenarios.
Includes detailed hints and educational guidance.
Provides multiple security levels that can be changed dynamically.
Creates a more interactive and guided learning environment.
Comparison

DVWA is simpler and more focused on practicing specific web application attacks, making it excellent for beginners learning individual vulnerabilities. Mutillidae offers a broader range of exercises and educational features, making it more interactive and suitable for deeper exploration of web application security concepts. Both applications are valuable learning tools and complement each other well in penetration testing training environments.




# Lessons Learned

This lab helped me understand how SQL Injection vulnerabilities occur when user input is not properly validated before being included in SQL queries. I learned that attackers can manipulate database queries by inserting malicious input that changes the intended logic of the application. Through DVWA and Mutillidae, I observed how security controls such as input validation and filtering can reduce the effectiveness of these attacks. I also gained experience using SQLMap, which demonstrated how automated tools can quickly identify and exploit SQL Injection vulnerabilities. Finally, I learned the importance of secure coding practices and proper database security measures to protect web applications from injection attacks and unauthorized access to sensitive information.
