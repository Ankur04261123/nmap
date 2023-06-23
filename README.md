# nmap

Different Approaches NMAP Uses to discover live Hosts:
1. ARP Scan - This scan uses ARP requests to discover live hosts
2. ICMP scan - This scan uses ICMP requests to identify live hosts
3. TCP/UDP ping scan -  This scan sends packets to TCP and UDP ports to determine live hosts.

We can provide the list, range and subnet for scanning to NMAP

list: MACHINE_IP scanme.nmap.org example.com will scan 3 IP addresses.
range: 10.11.12.15-20 will scan 6 IP addresses: 10.11.12.15, 10.11.12.16,… and 10.11.12.20.
subnet: MACHINE_IP/30 will scan 4 IP addresses.

You can also provide a file as input for your list of targets, Nmap -iL list_of_hosts.txt

If you want to check the list of hosts that Nmap will scan, you can use Nmap -sL TARGETS. This option will give you a detailed list of the hosts that Nmap will scan without scanning them; however, Nmap will attempt a reverse DNS resolution on all the targets to obtain their names. Names might reveal various information to the pentester. (If you don’t want Nmap to the DNS server, you can add -n.)

If you want to use Nmap to discover online hosts without port-scanning the live systems, you can issue nmap -sn TARGETS

If you want Nmap only to perform an ARP scan without port-scanning, you can use nmap -PR -sn TARGETS, where -PR indicates that you only want an ARP scan

arp-scan --localnet or arp-scan -l - This command will send ARP queries to all valid IP addresses on your local networks.

sudo arp-scan -I eth0 -l - will send ARP queries for all valid IP addresses on the eth0 interface.

#Instsall arp-scan
apt install arp-scan

nmap -PE -sn MACHINE_IP/24 - To use ICMP echo request to discover live hosts. -sn (no port scan)

#Because ICMP echo requests tend to be blocked, you might also consider ICMP Timestamp or ICMP Address Mask requests to tell if a system is online. Nmap uses timestamp request (ICMP Type 13) and checks whether it will get a Timestamp reply (ICMP Type 14).
-PP option tells Nmap to use ICMP timestamp requests.

To discover live hosts using ICMP address mask queries, we run the command nmap -PM -sn MACHINE_IP/24

#TCP SYN Ping
If you want Nmap to use TCP SYN ping, you can do so via the option -PS followed by the port number, range, list, or a combination of them. For example, -PS21 will target port 21, while -PS21-25 will target ports 21, 22, 23, 24, and 25. Finally -PS80,443,8080 will target the three ports 80, 443, and 8080.

#TCP ACK Ping
By default, port 80 is used. The syntax is similar to TCP SYN ping. -PA should be followed by a port number, range, list, or a combination of them. For example, consider -PA21, -PA21-25 and -PA80,443,8080. If no port is specified, port 80 will be used.

#UDP Ping
Nmap uses -PU for UDP ping

#Masscan
masscan MACHINE_IP/24 -p443
masscan MACHINE_IP/24 -p80,443
masscan MACHINE_IP/24 -p22-25
masscan MACHINE_IP/24 ‐‐top-ports 100

To install masscan:
apt install masscan

#Reverse DNS lookup
-n to skip the reverse DNS loopkup
option -R to query the DNS server even for offline hosts
If you want to use a specific DNS server, you can add the --dns-servers DNS_SERVER

#NMAP six states:
1. Open: indicates that a service is listening on the specified port.
2. Closed: indicates that no service is listening on the specified port, although the port is accessible. By accessible, we mean that it is reachable and is not blocked by a firewall or other security appliances/programs.
3. Filtered: means that Nmap cannot determine if the port is open or closed because the port is not accessible. This state is usually due to a firewall preventing Nmap from reaching that port. Nmap’s packets may be blocked from reaching the port; alternatively, the responses are blocked from reaching Nmap’s host.
4. Unfiltered: means that Nmap cannot determine if the port is open or closed, although the port is accessible. This state is encountered when using an ACK scan -sA.
5. Open|Filtered: This means that Nmap cannot determine whether the port is open or filtered.
6. Closed|Filtered: This means that Nmap cannot decide whether a port is closed or filtered.




