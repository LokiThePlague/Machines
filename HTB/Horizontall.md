----
- Tags: #temp
----

# Exploitation

Let's start by checking if we have connectivity with the machine:

```bash
ping -c 1 10.129.139.76
```

We are going to perform our first scan with nmap and save our output in grep format:

```bash
nmap -sS --min-rate 5000 --open -vvv -n -Pn -p- 10.129.139.76 -oG first_scan
```

Now we will proceed to extract the first_scan ports:

```
extractPorts first_scan
```

```
[*] Extracting information...

    [*] IP Address: 10.129.139.76
    [*] Open ports: 22,80

[*] Ports copied to clipboard
```

We are going to perform a deeper scan with nmap to see the open port services, launching basic reconnaissance scripts:

```
nmap -sCV -p22,80 10.129.139.76 -oN first_services_scan
```

```
# Nmap 7.93 scan initiated Sat Jul 22 17:36:44 2023 as: nmap -sCV -p22,80 -oN first_services_scan 10.129.139.76
Nmap scan report for horizontall.htb (10.129.139.76)
Host is up (0.034s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 ee774143d482bd3e6e6e50cdff6b0dd5 (RSA)
|   256 3ad589d5da9559d9df016837cad510b0 (ECDSA)
|_  256 4a0004b49d29e7af37161b4f802d9894 (ED25519)
80/tcp open  http    nginx 1.14.0 (Ubuntu)
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: horizontall
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Jul 22 17:36:52 2023 -- 1 IP address (1 host up) scanned in 7.98 seconds
```

# Privilege Escalation