# Domain Name Systems (DNS)

DNS translates domain names to IP addresses so browsers can load Internet resources. [domain.com -> IP address]

Process of translation and lookup is called **DNS resolution**.

Basic DNS resolution steps:

0. Browser checks in computer's local DNS cache database for that domain name. Found? Skip to step 6. Not Found? Continue.
1. Browser (www.example.com) -> DNS recursive resolver
2. The resolver queries a DNS root nameserver. Root server responds to resolvers address of Top Level Domain (TLD) DNS server - like .com, .net - which stores information about its domains.
3. Resolver makes request to .com TLD server. It responds to resolver with IP address of domain's nameserver (example.com)
4. Resolver sends a query to domain's nameserver. It returns IP address of the domain to resolver.
5. DNS Resolver responds to web browser with the IP address.
6. Browser makes http request to IP address. Server at that IP returns web page to browser. 


![](https://miro.medium.com/max/1400/0*Pr-60siIK-kubPqj.png)

## DNS server types

1. Recursive resolver server 
2. Root name server - [reponds with .com .net server IP]
3. TLD (Top Level Domain) server - [responds with domain.com IP]
4. Authoritative name server - [reponds with server IP that will handle the request]

## Common DNS records:

1. A record -  IPv4 address of a domain
2. AAA record -  IPv6 address of a domain
3. CNAME record -  forwards one domain or subdomain to another domain
4. TXT record - lets an admin store text notes in the record

## DNS caching

- DNS resolver save responses to IP address for a certain amount of time.
- Faster response from the resolver, lesser number of request/response. 
- Save IP addresses in cache according to designated time to live (TTL) associated with that IP address allows them 

## DNS security

- Major DNS security issue is user privacy. **DNS queries are not encrypted**. *DNS over TLS* and *DNS over HTTPS* are two standards for encrypting DNS queries to prevent external parties from reading them. 

Common attacks using DNS:

- **DNS spoofing/cache poisoning** - Attack where forged DNS data is inserted in DNS resolver's cache so it returns the wrong IP address for a domain. 
- **DNS tunneling** - This attack uses other protocols to tunnel through DNS queries and responses.  Attackers can use SSH, TCP, or HTTP to pass malware or stolen information into DNS queries, undetected by most firewalls.
- **DNS hijacking** - Attacker redirects queries to a different domanin nameserver.  It targets DNS record of the domain's nameserver, indead of resolver's cache (like in spoofing). 
- **NXDOMAIN attack** - DNS flood attack where attacker floods a DNS server with requests, asking for records that do not exist, to cause a *denial-of-service ([DoS Attack](https://www.cloudflare.com/learning/ddos/glossary/denial-of-service/))* for legitimate traffic. It can also target DNS resolver by filling the cache with junk requests.
- **Phantom domain attack** - Attacker sets up ghost domain server that respond to requests really slowly or not at all. DNS resolver is flooded with request of this server and it gets tied up waiting for responses, leading to DoS or slow performance. 
- **Random subdomain attack** - Attacker sends DNS queries to non-existant subdomains of a legitimate site. Goal is to create DoS for domain's nameserver. Attacker's IPS  will also be affected as their resolver cache will loaded with bad requests. 
- **Domain lock-up attack** - Attackers setup special domian and resolvers to create connection with legitimate resolvers. When legit resolvers send requests, these special resolvers send back slow stream of data blocking resolver. 
- **Botnet-based CPE attack**


## References:

- [Cloudflare - What is DNS?](https://www.cloudflare.com/en-in/learning/dns/what-is-dns/)
- [Cloudflare - DNS server types](https://www.cloudflare.com/learning/dns/dns-server-types/)
- [Cloudflare - DNS records](https://www.cloudflare.com/learning/dns/dns-records/)
- [Cloudflare - Security and attacks](https://www.cloudflare.com/en-in/learning/dns/dns-security/)
- [DNS security](https://www.checkpoint.com/cyber-hub/network-security/what-is-dns-security/)


