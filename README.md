![Cap](https://github.com/user-attachments/assets/bf472287-3429-42be-b736-85800a03ba83)


CAP is a relatively beginner-friendly machine designed to help you brush up on fundamental penetration testing skills. The machine involves basic enumeration, exploiting vulnerabilities, and privilege escalation. The steps to solve CAP are methodical and educational, offering a good learning experience for those who are familiar with or new to penetration testing.
As usual, starting with NMAP gives you the following result.

1. Initial Enumeration

    Start with Nmap Scanning: Begin by scanning the machine to identify open ports and services. Use a command like:

    bash

nmap <target_ip>

This command runs a basic script scan and version detection to provide a good overview of the machine’s network services.

Review Nmap Results: In the output file (nmap_initial.txt), look for open ports and their associated services. CAP typically has a few common ports open, such as HTTP (80) or SSH (22).

![Screenshot from 2024-08-28 12-16-51](https://github.com/user-attachments/assets/72fd899a-13f1-48b1-841f-77e3024d6bce)

The scan result shows that FTP, SSH and a web server are running in this machine. Let’s take a look at the web application.

![Screenshot from 2024-08-28 11-24-59](https://github.com/user-attachments/assets/0d22fee0-5acc-4494-ac66-074b879f9fc1)

You've come across a monitoring application, which seems to be designed for tracking and displaying network metrics. The presence of a dashboard showing TCP and UDP packet information, along with a download button, is intriguing and could potentially be exploited for further investigation or gaining access.
1. Exploring the Dashboard

    Access the Dashboard: First, navigate to the dashboard section of the application using your web browser. Carefully observe the layout and content of the page.

    Analyze the Metrics: Take note of the metrics being displayed. This might include real-time data about network traffic, packet counts, source and destination addresses, or protocol-specific details.

    Investigate the Download Button: The download button is particularly interesting. It might offer an export of the data or logs that are being displayed. This could potentially provide valuable insights into the application’s internal workings or sensitive data
   The file downloaded seems to be a PCAP file. Though the initial PCAP file doesn’t seem to reveal any useful information, changing the number present in the end of the URL from 4 to 0 makes a change in the number of packet information in the dashboard.

   ![Screenshot from 2024-08-28 11-33-52](https://github.com/user-attachments/assets/6a04b581-7641-4d99-bfb8-05a9604b5758)
   
   
   Upon downloading the respective PCAP file and viewing it in Wireshark, we get the credentials for FTP.

   

   
![Screenshot from 2024-08-28 11-22-19](https://github.com/user-attachments/assets/b2b765f7-677a-4842-8144-5ce8bb4284e0)

![Screenshot from 2024-08-28 12-24-07](https://github.com/user-attachments/assets/7a216046-7467-4386-94a9-b2b287f31cda)

Login to FTP using the above credentials to find that the FTP server serves the SSH directory.



![Screenshot from 2024-08-28 11-35-31](https://github.com/user-attachments/assets/308eab34-5d86-41ef-9a7c-804a1b231922)


Logging into the FTP server with the obtained credentials reveals that the FTP server hosts the SSH directory.


![Screenshot from 2024-08-28 11-36-43](https://github.com/user-attachments/assets/4f6be681-c965-4568-af8c-b5671323cae7)

We login to SSH using the same FTP credentials and it does work.

Now for the Privilege escalation part, the result of LINPEAS shows an interesting finding about cap_setuid on Python 3.8’s binary and hence the machine’s name.

![Screenshot from 2024-08-28 11-40-37](https://github.com/user-attachments/assets/af8443f4-c426-42c1-b9a2-1cd555c1f202)




