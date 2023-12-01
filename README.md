# Penetration-testing
Penetration testing flow:

  1. Planning and reconnaissance
     The first stage involves:

    Defining the scope and goals of a test, including the systems to be addressed and the testing methods to be used.
    Gathering intelligence (e.g., network and domain names, mail server) to better understand how a target works and its potential vulnerabilities.

  2. Scanning
The next step is to understand how the target application will respond to various intrusion attempts. This is typically done using:

    Static analysis – Inspecting an application’s code to estimate the way it behaves while running. These tools can scan the entirety of the code in a single pass.
    Dynamic analysis – Inspecting an application’s code in a running state. This is a more practical way of scanning, as it provides a real-time view into an application’s performance.

  3. Gaining Access


## Web penetration testing tools:
  ### Reconnaisance:
Outside of the site:
  -Dns dumpster [web site](https://dnsdumpster.com/), also finds subdomains
  -Whois records, DNS records, with nslookup get ip of domain name, dig
  | nslookup Query type | Description |
  | ----------- | ----------- |
  | A | IPv4 Address |
  | AAAA | IPv6 Address |
  | CNAME | Canonical Name |
  | MX | Mail Servers |
  | SOA | Start of Authority |
  | TXT | TXT Records |
  | ----------- | ----------- |

  ```
  nslookup -type=A domain.com
  whois domain.com
  dig domain.com TYPE
  ```
  -[Shodan.io](https://www.shodan.io/)
  ### Scanning:
In the site:
  -Content discovery:
      -Robots.txt 
      -Favicon.ico [Favicon database](https://wiki.owasp.org/index.php/OWASP_favicon_database)
      -Sitemap.xml
      -HTTP headers
      -Wappalyzer [link](https://www.wappalyzer.com)
      -Wayback machine
      -S3 bucket
      -ffuf, dirb, gobuster
      
```
ffuf -w SecLists/Discovery/Web-Content/common.txt -u https://domain.com
dirb https://domain.com SecLists/Discovery/Web-Content/common.txt
gobuster dir --url http:s://domain.com -wSecLists/Discovery/Web-Content/common.txt
```
      
  - Seclists GitHub [page](https://github.com/danielmiessler/SecLists)
Subdomain enumeration:
    -Sublist3r Github [page](https://github.com/aboul3la/Sublist3r)
    
 ```
python sublist3r.py -d example.com
 ```

### Gaining access:
Authentication bypass:
Username enumeration:

```
ffuf -w SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u https:://domain.org/customers/signup -mr "username already exists"
```

With the valid usernames, we can do login brute force:

``` 
ffuf -w valid_usernames.txt:W1,SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u https://domain.com/customers/login -fc 200
```

Hash breaking with hashcat and [cracking station](https://crackstation.net/)
 

## Systems penetration testing

### nmap commands
```
nmap -sV -sC -p- 10.20.30.40
```
-sV for version detection in ports
-sC scripts
-sS fast SYN scan
-A OS detect, version detect, script scan, traceroute
-p- for ports e.g -p-1-1000 

### Shells
Reverse shell in netcat
```
nc -lvnp <port-number>
```
in socat
```
socat TCP-L:<port> -
```

Bind shell in netcat
```
nc <target-ip> <chosen-port>
```

in socat
```
socat TCP:<TARGET-IP>:<TARGET-PORT> -
```
