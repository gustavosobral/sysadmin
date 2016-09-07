# Sysadmin
Useful commands and scripts for sysadmin basic tasks.

Optional line arguments are surronded by square brackets [], and example arguments are surrondend by <>.

## SSH
Configuration file `/etc/ssh/sshd_config`

* 'Port' - Default SSH port (Change)
* 'PermitRootLogin' - Root login allowed ways (Change from 'yes' to 'without-password' to only allow root connection with public key authentication)

## Firewall
Commands to list, add and remove rules on Iptables program.

```
$ iptables -S
$ iptables -nL --line-numbers
$ iptables -I <INPUT [line-number] -p tcp -m tcp --dport 80 -j ACCEPT>
$ iptables -D <INPUT -i lo -j ACCEPT>
```

To persist the Iptables modified rules, I use `iptables-persistent` utilitary. After change a rule, just exec `invoke-rc.d iptables-persistent save` to save modifications.

My common Iptables configuration:

![Iptables](assets/iptables.png)

## Netstat
Print network connections

List tcp connections (t), without resolving ip addresses (n) and showing the process pid (p). To show the process pid (p) you may need to run as `root`.
```
$ netstat -tnp
```

![Netstat](assets/netstat.png)

* Useful tips:

Filter by port
```
$ netstat -tnp | grep :80
```

## nmap
Network mapping. Scan hosts or IP address. Along with many purposes, `nmap` can be used to scan open ports in a remote host.

Scan a host or IP address. Use `-6` to scan an IPv6 address
```
$ nmap [-6] host_or_address
```

Scan multiple IP address or subnet (IPv4)
```
$ nmap 192.168.1.1 192.168.1.2 192.168.1.3
## works with same subnet i.e. 192.168.1.0/24
$ nmap 192.168.1.1,2,3
```
IPv6 could take years to scan a normal subnet /64. Use with caution.

Scan IPs from a file
```
$ nmap -iL /tmp/address_list.txt
```

Turn on OS detection
```
# IPv4
$ nmap -A 192.168.1.1
# IPv6
$ nmap -A -6 ::1
```

Scan a host for UDP services (UDP scan)
```
$ nmap -sU 192.168.1.1
```

## Users and groups
Basic commands to handle user attributes (Passsword, groups, etc):

```
$ adduser <username>
$ adduser <username> <group>
$ useradd <username>
$ passwd <username>
$ deluser <username>
```

Auditing commands:
```
$ w
$ last
$ lastlog
```

## Tools
Useful tools

* vim - Text editor
* htop - Interactive process viewer
