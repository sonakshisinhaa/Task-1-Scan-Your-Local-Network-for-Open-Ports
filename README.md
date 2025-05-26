Task-1-Scan-Your-Local-Network-for-Open-Ports
1. use ipconfig to discover the network
2. Use nmap -sS 192.168.1.0/24 for port scan
3. result are displayed 
4. result save in scan_result.txt

Result:

1. 192.168.1.1 (Likely Router)
Open Ports: 53 (DNS), 80 (HTTP), 443 (HTTPS)

Filtered Ports: 22 (SSH), 23 (Telnet)

| Port | State    | Service | Description               |
| ---- | -------- | ------- | ------------------------- |
| 22   | filtered | SSH     | Remote secure shell login |
| 23   | filtered | Telnet  | Remote login (insecure)   |
| 53   | open     | DNS     | Domain Name System        |
| 80   | open     | HTTP    | Unencrypted web server    |
| 443  | open     | HTTPS   | Secure web server         |


Risks:

Telnet is insecure — should be disabled.
HTTP is unencrypted — switch to HTTPS only.


2. 192.168.1.2 and 192.168.1.3
All ports closed.

Likely secure or not running any services.


3. 192.168.1.6 (Likely Windows PC or VM Host)
Open Ports: 135 (MSRPC), 902 (VMware), 912 (Unknown), 3306 (MySQL)

| Port | State | Service       | Description                          |
| ---- | ----- | ------------- | ------------------------------------ |
| 135  | open  | MSRPC         | Microsoft RPC (Windows services)     |
| 902  | open  | VMware Server | VMware ESXi Remote Console           |
| 912  | open  | Apex Mesh?    | Unknown; proprietary or internal use |
| 3306 | open  | MySQL         | MySQL Database Server                |


Risks:

MySQL open — restrict or secure with strong passwords.
MSRPC and VMware ports — may expose system to exploits.

| Port | Common Service | Description                                                                           |
| ---- | -------------- | ------------------------------------------------------------------------------------- |
|  22  | SSH            | Used for secure remote access. Filtered status suggests a firewall is blocking it.    |
|  23  | Telnet         | Legacy protocol for remote login. Not secure; sends data in plaintext.                |
|  53  | DNS            | Resolves domain names to IP addresses. Common on routers/DNS servers.                 |
|  80  | HTTP           | Unencrypted web traffic. Could be hosting a management interface.                     |
|  443 | HTTPS          | Encrypted web interface; likely a secure web admin panel.                             |
|  135 | MSRPC          | Used by Windows for remote procedure calls; often a target for exploits.              |
|  902 | VMware ESXi    | Port for remote management; if unused, should be closed.                              |
|  912 | Apex Mesh?     | Not a well-known port. Might be part of a proprietary or IoT system.                  |
| 3306 | MySQL          | Used by MySQL database; if exposed, could lead to SQL injection or brute force risks. |
