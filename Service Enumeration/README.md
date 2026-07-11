## Service Enumeration

## Objective

Identify running services on Ubuntu and compare local results with remote Nmap scans.

## Lab Environment

Machine	IP Address
Ubuntu	10.0.2.4
Kali Linux	10.0.2.15

## Tools Used

ss
Nmap

## Commands Used
ss -tuln
sudo ss -tulpn 

## On Kali:
nmap -sV 10.0.2.4
 
## Screenshots

ss output
![Description of screenshot](images/ubuntu_services.png)
Nmap scan results

## Findings

Compared locally running services with those detected remotely by Nmap.

## Lessons Learned

Difference between local service inspection and remote enumeration.
Understanding listening ports.

Conclusion

Confirmed that Nmap accurately detected exposed services.
