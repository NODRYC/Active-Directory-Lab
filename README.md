# Active Directory Lab Setup

## Objective
 
The objective of this project was designed to simulate a virtual Windows Active Directory environment with the goal of creating users, host machines, a domain controller, and attacker/adversary machine. 

This project aimed to simulate a corporate network which included a setup of various security tools to generate telemetry, logs and re-create real world attack scenarios and patterns.

### Skills Learned/Used

Setting up Active Directory and Domain Services 
SIEM setup on both Windows and Linux servers 
Capturing telemetry and network logs for analysis 
Identifying threats and recognizing attack patterns from potential adversaries
Troubleshooting network and server issues with the use of critical thinking

### Tools Used

VirtualBox
Splunk (SIEM) for analysis (Windows Server, Linux Server)
Sysmon to generate logs and telemetry
Kali Linux for penetration testing
Atomic Red Team for adversary simulation for log activity

## Steps

1. Created a logical network diagram that includes the domain controller (AD) Server,  Splunk Server, host and attack machines

2. Installed VirtualBox and installed + setup 4 different virtual machines 
(Windows 10 , Windows Server, Kali and Linux Server (Splunk))

3. Created a NAT network and configured for all virtual machines the same as diagram.
- changed the IP for the splunk server to a static IP matching diagram 
[sudo nano /etc/netplan/50-cloud-init.yaml]
- installed splunk and guest addons for VirtualBox in linux server
- added shared folders in linux server and installed splunk also configured to run at every VM boot

4. Setting up Splunk forwarder and Sysmon on target machine and Windows Server
- changed the target machine name from default to target-PC
- downloaded and installed splunk universal forwarder onto target-PC
- downloaded and sysmon and olaf config
- installed config and sysmon via powershell
- created inputs.conf file for local folder
- restarted forwarder service when updating inputs.conf file and changed login accounts to local user
- logged into splunk to create new endpoint index
- solved issue regarding disk space on linux server for index storage 
- verified endpoint detection using index=endpoint
- repeated all steps above for windows server and have splunk detect both endpoints

5. Installed Active Directory Domain Services on Windows Server
- promoted server to domain controller and started the config wizard
- created a username and password and completed the configuration wizard
- restarted server 
- created mock users and Organizational Units (OUs) for AD
- logged into Windows 10 machine and configured it to join domain and pointed the DNS to server’s DNS address
- restarted computer and logged in as mock user

6. Started kali machine and prepared for brute force attack on target-PC
- configured the static IP and updated the repositories
- downloaded crowbar (brute force tool) and unzipped the rockyou wordlist and only grabbed the first 20 
- configured the target-PC to receive RDP connections and allowed both users to do solved
- prepared crowbar for bruteforce using correct syntax
- successfully established an RDP connection with correct username and password
- logged into splunk and query the affected user
- filter out event id 4625 and 4625 to view failed and successful logon attempts to isolate attacker machine

7. Prepared to install Atomic Red Team
- installed using powershell commands and url
- used ART to generate telemetry for an executed Persistence Technique that creates new local accounts
- used ART to execute an execution attack (command and scripting interpreter via powershell) to generate
telemetry to view in splunk








