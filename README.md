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

  `
  nslookup -type=A domain.com
  whois domain.com
  dig domain.com TYPE
  `
  -[Shodan.io](https://www.shodan.io/)
  
  Content discovery:
      -Robots.txt 
      -Favicon.ico [Favicon database](https://wiki.owasp.org/index.php/OWASP_favicon_database)
      -Sitemap.xml
      -HTTP headers
      -Wappalyzer [link](https://www.wappalyzer.com)
      -Wayback machine
      -S3 bucket
      -ffuf, dirb, gobuster
      `
      ffuf -w SecLists/Discovery/Web-Content/common.txt -u https://domain.com
      dirb https://domain.com SecLists/Discovery/Web-Content/common.txt
      gobuster dir --url http:s://domain.com -wSecLists/Discovery/Web-Content/common.txt
      `
      Seclists GitHub [page](https://github.com/danielmiessler/SecLists)
      
      
      
 

