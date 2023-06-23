# nmap

Different Approaches NMAP Uses to discover live Hosts:
1. ARP Scan - This scan uses ARP requests to discover live hosts
2. ICMP scan - This scan uses ICMP requests to identify live hosts
3. TCP/UDP ping scan -  This scan sends packets to TCP ports and UDP ports to determine live hosts.

We can provide the list, range and subnet for scanning to NMAP

list: MACHINE_IP scanme.nmap.org example.com will scan 3 IP addresses.
range: 10.11.12.15-20 will scan 6 IP addresses: 10.11.12.15, 10.11.12.16,… and 10.11.12.20.
subnet: MACHINE_IP/30 will scan 4 IP addresses.

You can also provide a file as input for your list of targets, nmap -iL list_of_hosts.txt

If you want to check the list of hosts that Nmap will scan, you can use nmap -sL TARGETS. This option will give you a detailed list of the hosts that Nmap will scan without scanning them; however, Nmap will attempt a reverse-DNS resolution on all the targets to obtain their names. Names might reveal various information to the pentester. (If you don’t want Nmap to the DNS server, you can add -n.)
