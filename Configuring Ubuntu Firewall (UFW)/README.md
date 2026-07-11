## Configuring Ubuntu Firewall (UFW)

## Objective

To configure and manage the Ubuntu Uncomplicated Firewall (UFW) to secure the system and observe how firewall rules affect network scans.

## Lab Environment

Machine	IP Address
Kali Linux	10.0.2.15
Ubuntu	10.0.2.4

## Tools Used

Ubuntu
UFW
Nmap
VirtualBox

## Commands Used

sudo ufw status
sudo apt install ufw
sudo ufw allow ssh
sudo ufw allow 8000/tcp
sudo ufw enable
sudo ufw status verbose
## Screenshots

UFW status before configuration
Firewall enabled
![description of screenshot](images/ufw_conf.png)
Nmap scan before firewall
Nmap scan after firewall
![description of screenshot](images/ufw_conf2.png)
![description of screenshot](images/ufw_nmap.png)

## Findings

Configured UFW to protect Ubuntu while allowing SSH and the Python HTTP service. 
Compared Nmap scan results before and after enabling the firewall.

## Lessons Learned

Importance of host firewalls.
Managing firewall rules.
How firewall rules influence network reconnaissance.

Conclusion

This lab demonstrated how host-based firewalls reduce the attack surface by controlling network access.
