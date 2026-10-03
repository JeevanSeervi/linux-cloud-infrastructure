Module 2 – Linux Basics
Linux CLI Operations, Files & Permissions, Users, Groups, Processes, Services and SSH Keys
1. Linux CLI Operations
CLI (Command Line Interface) allows us to interact with Linux by typing commands in the terminal.
Important commands:
• pwd – Shows the current directory
• ls – Lists files and folders
• cd – Changes directory
• mkdir – Creates a directory
• touch – Creates a file
• cat – Displays file contents
• cp – Copies a file
• mv – Moves or renames a file
• rm – Deletes a file
• clear – Clears the terminal
• whoami – Shows the current user
Example:
mkdir project
cd project
touch test.txt
echo "Hello Linux" > test.txt
cat test.txt
2. Files and Permissions
Linux controls access to files using permissions.
Permissions:
• r – Read
• w – Write
• x – Execute
Permission categories:
• Owner – User who owns the file
• Group – Users belonging to the file's group
• Others – Everyone else
Check permissions:
ls -l
Example:
-rw-r--r--
This means:
Owner → rw-
Group → r--
Others → r--




chmod:
chmod changes file permissions.


Example:
chmod 644 test.txt
Permission values:
7 = rwx
6 = rw-
5 = r-x
4 = r--
0 = ---
chown:
chown changes file ownership.
Example:
sudo chown ubuntu test.txt
3. Linux Users
Linux supports multiple users.
Check the current user:
whoami

Get user information:
id
Root user:
root is the administrator account. Administrative commands are commonly executed using sudo.
Example:
sudo apt update
Create a user:
sudo adduser student
Check the user:
id student
4. Linux Groups
A group is a collection of users. Groups make it easier to manage permissions for multiple users.
Create a group:
sudo groupadd developers
Add a user to a group:
sudo usermod -aG developers student
Check groups:
groups student

5. Process Management
A process is a running program.
View processes:
ps
Detailed process list:
ps aux
Real-time monitoring:
top
Press q to exit top.
Process ID:
Every process has a unique PID (Process ID).
Find a process:
pgrep nginx
Stop a process:
kill PID
Example:
kill 1234

6. Linux Services
A service is a program that runs in the background and provides functionality to the system.
Linux commonly uses systemctl to manage services.
Check service status:
sudo systemctl status nginx
Start a service:
sudo systemctl start nginx
Stop a service:
sudo systemctl stop nginx
Restart a service:
sudo systemctl restart nginx
Enable a service at startup:
sudo systemctl enable nginx
7. SSH Keys
SSH (Secure Shell) allows you to securely connect to a remote Linux server.
Basic connection:
Your Computer → SSH → Linux Cloud Server
SSH authentication can use a key pair:
• Public key – Stored on the server
• Private key – Kept securely on your computer
Never share your private SSH key.
For example, AWS may provide a private key file such as:
server.pem
Typical SSH connection:
ssh -i server.pem ubuntu@SERVER_IP
SSH normally uses:
Port 22
Practical Checklist
For this part of Module 2, you should be able to demonstrate:
☑ Linux CLI commands
☑ Create and manage files
☑ File permissions
☑ chmod
☑ chown
☑ Users
☑ sudo
☑ Groups
☑ Processes
☑ Services
☑ SSH
☑ SSH keys
This is enough for the specific Linux requirement in Module 2. Advanced Linux topics are not required for this section.

Module 2 – Linux, Networking & Cloud Infrastructure
Networking Notes: IP Addressing, DNS, Ports, Firewalls & AWS Security Groups
Purpose: Beginner-friendly notes for understanding and practicing the networking concepts required in Module 2.
1. IP Addressing
An IP (Internet Protocol) address is a numerical address used to identify a device or network interface and allow devices to communicate over a network.
1.1 IPv4
IPv4 uses 32 bits and is normally written as four decimal numbers separated by dots.
Example: 192.168.1.10
    • Each number is called an octet and normally ranges from 0 to 255.
    • IPv4 is still widely used for servers, computers and network devices.
1.2 IPv6
IPv6 is the newer IP protocol. It uses 128-bit addresses and was designed to provide a much larger address space.
Example: 2001:db8::1
    • IPv6 addresses are written using hexadecimal characters.
    • For this beginner module, focus mainly on understanding IPv4.
1.3 Public vs Private IP
    • Private IP: Used inside a private network and normally cannot be reached directly from the public Internet.
    • Public IP: Used for Internet-facing communication.
Private examples: 10.0.0.10, 172.16.0.10, 192.168.1.10
In AWS, an EC2 instance can have a private IP inside its VPC and may also have a public IPv4 address for Internet access.
1.4 Subnet and CIDR Basics
A subnet divides a larger network into smaller network ranges. CIDR notation describes the network range using a prefix length.
10.0.0.0/16
192.168.1.0/24
    • /24 means the first 24 bits identify the network.
    • You should understand the idea of network ranges before moving to advanced subnet calculations.
2. DNS – Domain Name System
DNS translates human-readable domain names into IP addresses. This lets users access services using names instead of remembering numerical IP addresses.


User enters: example.com
        ↓
DNS lookup
        ↓
IP address returned
        ↓
Client connects to the server
2.1 Common DNS Records
Record
Purpose
A
Maps a domain name to an IPv4 address.
AAAA
Maps a domain name to an IPv6 address.
CNAME
Points one domain name to another domain name.
MX
Specifies mail servers for a domain.
TXT
Stores text information, often used for verification and email security.
2.2 DNS Commands
nslookup google.com
dig google.com
ping google.com
curl https://google.com
nslookup and dig are useful for checking DNS resolution. ping tests basic network reachability when ICMP is permitted. curl tests HTTP/HTTPS communication.
3. Network Ports
A port is a logical communication endpoint used by network services. An IP address identifies the host, while a port helps identify the service on that host.
IP address = Building
Port       = Room
Service    = Business inside the room
Port
Protocol/Service
Common Use
22
SSH
Secure remote Linux administration
53
DNS
Domain name resolution
80
HTTP
Websites without TLS encryption
443
HTTPS
Secure web traffic
21
FTP
File transfer
25
SMTP
Email transfer
3306
MySQL
MySQL database
5432
PostgreSQL
PostgreSQL database


3.1 TCP vs UDP
    • TCP is connection-oriented and provides reliable, ordered delivery.
    • UDP is connectionless and has lower overhead but does not provide TCP-style delivery guarantees.
For this module, know that network services use protocols and ports, and firewall rules can control traffic to those ports.
4. Firewalls
A firewall controls network traffic according to rules. It can allow or block traffic based on factors such as source, destination, protocol and port.
Internet → Firewall → Server
Example policy:
22  → ALLOW (SSH)
80  → ALLOW (HTTP)
443 → ALLOW (HTTPS)
3306 → BLOCK / not publicly exposed
Only expose ports that are actually required. Database ports should generally not be opened to the whole Internet for a basic learning server.
4.1 Linux UFW
Ubuntu commonly uses UFW (Uncomplicated Firewall) as a simple interface for firewall configuration.
sudo ufw status
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
Important: when working over SSH, make sure SSH access is permitted before enabling or changing firewall rules. Otherwise, you can lock yourself out of the server.
5. AWS Security Groups
An AWS Security Group is a virtual firewall associated with resources such as EC2 instances. It controls network traffic using rules.
Internet → Security Group → EC2 Linux Server
5.1 Inbound Rules
Inbound rules control traffic coming into the resource.
Your computer → TCP 22 → EC2
For a basic Linux server, SSH on port 22 is commonly required for administration. If you deploy a web server, HTTP port 80 or HTTPS port 443 may also be needed.

5.2 Outbound Rules
Outbound rules control traffic leaving the resource.
EC2 → Internet
For learning, understand the difference between inbound and outbound traffic rather than changing default rules unnecessarily.
5.3 Example Security Group Rules
Type
Protocol
Port
Typical Source
SSH
TCP
22
Your IP / restricted source
HTTP
TCP
80
Internet, if hosting a public web service
HTTPS
TCP
443
Internet, if hosting a public HTTPS service
6. Practical Commands for Your EC2 Linux Server
After connecting to the Linux server through SSH, practice the following commands.
6.1 Check the Current User
whoami
6.2 Check Hostname
hostname
6.3 Check IP Information
ip addr
hostname -I
6.4 Test DNS
nslookup google.com
ping google.com
curl https://google.com
6.5 Check Listening Ports
sudo ss -tulpn
This command helps identify services that are listening for network connections. A result containing :22 commonly indicates an SSH service listening on port 22.
7. Recommended Module 2 Networking Practical
    1. Connect to your AWS Linux EC2 instance using SSH.
    2. Run whoami and hostname to confirm the server connection.
    3. Run ip addr or hostname -I to inspect IP information.
    4. Use nslookup google.com to verify DNS resolution.
    5. Use curl https://google.com to test outbound HTTPS connectivity.
    6. Run sudo ss -tulpn to inspect listening services and ports.
    7. Open the EC2 Security Group and inspect its inbound rules.
    8. Confirm that SSH (TCP 22) is available from an appropriate source.
    9. If you deploy a web service, add HTTP (TCP 80) only when needed.
    10. Test the service from your browser or with curl.
    11. Document screenshots and commands for your internship submission.

8. Key Differences to Remember
Concept
Remember
IP Address
Identifies a host/network interface.
DNS
Translates names such as example.com into IP addresses.
Port
Identifies a network service endpoint on a host.
Firewall
Allows or blocks network traffic according to rules.
Security Group
AWS virtual firewall controlling traffic to/from supported resources.
Inbound
Traffic coming into the server/resource.
Outbound
Traffic leaving the server/resource.
9. Important Questions for Viva / Internship
What is an IP address?
A numerical address used to identify a device or network interface and enable network communication.
What is DNS?
A system that translates domain names into IP addresses.
What is a port?
A logical endpoint used by network services for communication.

What is port 22 used for?
SSH, commonly used for secure remote administration of Linux servers.
What is port 80 used for?
HTTP web traffic.
What is port 443 used for?
HTTPS web traffic.
What is a firewall?
A system that controls network traffic using security rules.
What is an AWS Security Group?
A virtual firewall that controls network traffic for resources such as EC2 instances.
What is inbound traffic?
Traffic entering a server or resource.
What is outbound traffic?
Traffic leaving a server or resource.
Why should unnecessary ports not be exposed?
Reducing exposed services reduces the server's attack surface and unnecessary network access.
10. Quick Revision
    • IP = address of the host/interface.
    • DNS = name-to-IP resolution.
    • Port = service endpoint.
    • Firewall = traffic control.
    • Security Group = AWS virtual firewall.
    • SSH = TCP 22.
    • HTTP = TCP 80.
    • HTTPS = TCP 443.
    • Use restricted sources for administration whenever practical.
Do not expose database services publicly unless there is a specific, controlled requirement.
