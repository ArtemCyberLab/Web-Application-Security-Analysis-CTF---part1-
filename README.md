 Project: Web Application Security Analysis (CTF) PART1
Description:
This project focuses on analyzing the security of a web application, including user registration and password hashing. The main goal was to examine the password generation scheme using MD5 and identify potential vulnerabilities related to predictable hashes.

 Technologies Used:

Kali Linux
CyberChef
MD5 hashing
Linux commands (bash, xclip, md5sum)
CTF platforms (TryHackMe, HackTheBox)
Main Steps:

User Registration

The password generation scheme was identified: md5(username + ddmm), where ddmm is the day and month of birth.
A user dan was registered with the birth date 02/02/2003.
The generated password: dan2003, with the MD5 hash: f80a9802806ebebac2482e4c81735863.
Password Verification and Login Attempt

Used CyberChef to hash dan0202.
Login attempt failed, suggesting a possible mismatch in the hashing method.
Terminal Commands in Kali Linux

Checked hashing using the command:
bash
Copy
Edit
echo -n 'dan0202' | md5sum | cut -d ' ' -f 1
Installed xclip to copy results:
bash
Copy
Edit
sudo apt install xclip -y
echo -n 'dan0202' | md5sum | cut -d ' ' -f 1 | xclip -selection clipboard
Compared the generated hash with the expected one.
 Bash Script for Automating Hash Generation:
bash
Copy
Edit
#!/bin/bash

read -p "Enter username: " username
read -p "Enter birth date (ddmm): " dob

password="${username}${dob}"
hash=$(echo -n "$password" | md5sum | cut -d ' ' -f 1)

echo "Generated MD5 hash for $password: $hash"
echo "$hash" | xclip -selection clipboard
echo "Hash copied to clipboard!"
 Findings and Recommendations:
Using predictable password hashing (md5(username+ddmm)) makes the system vulnerable to attacks.
It is recommended to use salted hashing (e.g., bcrypt, Argon2) instead of plain MD5.
Further analysis of the server-side hashing method is needed.
Next Steps: Explore other potential vulnerabilities and test more advanced attack methods.

