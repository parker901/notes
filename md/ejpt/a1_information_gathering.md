# Information Gathering

## Passive Information Gathering

### Website Recon & Foot printing

What to look for:

- IP addresses
- Directories hidden from search engine
- Names
- Email addresses
- Phone Numbers
- Physical Addresses
- Web technologies used

**DNS lookup**  
`host hackersploit.com`

**robot.txt**  
Specifying folders or files that should not be indexed by search engine.

**sitemap.xml**  
File in xml that is used to provide search engine and organised way to index a web page. Sitemap can sometimes reveal links that is not presented on the main web page.

**Web technology footprintin**

- builtwith: technology profiler, what web technology is running on the website
- Wappalyzer: technology profiler
- kali's `whatweb`

**Downloading a website**  
[https://httrack.com](https://httrack.com) - useful to analyse source code of the website.

### Whois Enumeration

Whois lookup - getting information about a domain. ls
Information to look for:

- Name Server
- Owner personal details - Registrar (Most case information will be redacted)
  e.g. `whois zonetransfer.me` or `whois 172.67.155.53` or [https://whois.org](https://whois.org)

### Footprinting with Netcraft

Use to gather information about the target domain. [https://www.netcraft.com/](https://www.netcraft.com/)
- Background
- Network
- SSL/TLS
- Hosting history
- Web trackers
- Site technology

### DNS Recon
Records associated with a domain.
Looking for:
- Nameserver
- A record
- AAAA record
- MX record

**dnsrecon**  
`dnsrecon -d zonetransfer.me`

**DNSdumpster**  
[https://dnsdumpster.com/](https://dnsdumpster.com/)

### WAF with wafwoof
Identify if web application is protected by a firewall.

```bash
# list out the WAF that the tool can detect
wafw00f -l

# testing single waf instance
wafw00f hackertube.net

# testing all waf instances
wafw00f hackertube.net -a
```

### Subdomain Enumeration with Sublist3r
```bash
sublist3r -d hackersploit.org -e google, yahoo

sublist3r -d hackersploit.org
```
*Note: there maybe no results because the search engines has rate limiting*

### Google Dorks
```
site:ine.com

site:ine.com inurl:admin

site:*.ine.com

site:*.ine.com intitle:admin

# directory listing
intitle: index of

cache:ine.com

inurl:auth_user_file.txt

inurl:wp-config.bak
```
[https://archive.org/web/](https://archive.org/web/)

[https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database)

### Email Harvesting with theHarvester
[https://github.com/laramies/theHarvester](https://github.com/laramies/theHarvester)
```
theHarvester -d hackersploit.org -b rapiddns
```

### Leaked Password Databases
[https://haveibeenpwned.com/](https://haveibeenpwned.com/)


## Active Information Gathering

### DNS Zone Transfers
DNS Server - Cloudflare(1.1.1.1), Google(8.8.8.8)
DNS Records - A, AAAA, NS, MX, CNAME, TXT, HINFO, SOA, SRC, PTR

**DNS interrogation** 
- Enumerating DNS records
- Probe DNS server to provide DNS records of specific domain

**DNS Zone Transfer**
[https://digi.ninja/projects/zonetransferme.php](https://digi.ninja/projects/zonetransferme.php).
DNS zone transfer uses the AXFR protocol, it copies DNS records to another DNS servers.
Security problems with DNS Zone Transfer such information can be leaked.

*Note*  
Zone transfer needs to be enabled.

```
# Getting a copy from the primary server
dig axfr @nsztm1.digi.ninja zonetransfer.me
```

* SOA - primary name server, contact details, serial number for the domain(if date is check regualarly a change could indicate some activitn in the company). 
* LOC - lcoation stored as latitude/longitude. Convert using [https://www.fcc.gov/media/radio/dms-decimal](https://www.fcc.gov/media/radio/dms-decimal).
* SRV - often used for VOIP setups to indicate SIP servers. 
* PTR - maps ip address back to domain

```
dnsenum zonetransfer.me
```


**Host files**  
```
/etc/hosts
```


### Host Discovery with Nmap

### Port Scanning with Nmap
