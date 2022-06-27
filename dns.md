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
2. Root name server
3. TLD (Top Level Domain) server
4. Authoritative name server

## Common DNS records:

1. A record
2. AAA record
3. CNAME record 
4. TXT record

## DNS caching

## DNS security

- Important DNS security issue is user privacy. **DNS queries are not encrypted**. *DNS over TLS* and *DNS over HTTPS* are two standards for encrypting DNS queries to prevent external parties from reading them. 

Common attacks using DNS:

- **DNS spoofing/cache poisoning**
- **DNS tunneling**
- **DNS hijacking**
- **NXDOMAIN attack**
- **Phantom domain attack**
- **Random subdomain attack**
- **Domain lock-up attack**
- **Botnet-based CPE attack**


## References:

- [Cloudflare - What is DNS?](https://www.cloudflare.com/en-in/learning/dns/what-is-dns/)
- [Cloudflare - DNS server types](https://www.cloudflare.com/learning/dns/dns-server-types/)
- [Cloudflare - DNS records](https://www.cloudflare.com/learning/dns/dns-records/)
- [Cloudflare - Security and attacks](https://www.cloudflare.com/en-in/learning/dns/dns-security/)
- [DNS security](https://www.checkpoint.com/cyber-hub/network-security/what-is-dns-security/)


