### Hack The Box - Cap Walkthrough

#### Step 1: Initial Scanning
- **Target IP:** 10.10.10.207
- **Run an Nmap scan to discover open ports:**
  ```bash
  nmap -sC -sV -oN cap_nmap 10.10.10.207
  ```
- **Results show:**
  - **Port 22 (SSH):** Open.
  - **Port 80 (HTTP):** Website running on Apache.

#### Step 2: Exploring the Website
- **Visit the website on Port 80:**
  - The site has a login page.
- **Use Gobuster to find hidden directories:**
  ```bash
  gobuster dir -u http://10.10.10.207 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ```
- **Find `/hidden` directory.**

#### Step 3: Exploiting Hidden Directory
- **Explore the `/hidden` directory:**
  - Find a file with sensitive information.
- **Use the information to gain further access.**

#### Step 4: Gaining Access
- **Look for vulnerabilities or misconfigurations in the file.**
- **Exploit these to get a shell or access other parts of the system.**

#### Step 5: Privilege Escalation
- **Find ways to escalate privileges:**
  - Check for misconfigured files or services.
- **Exploit to gain root access.**

#### Step 6: Capture the Flags
- **User Flag:** Found in the user’s home directory.
- **Root Flag:** Found in the root directory.
