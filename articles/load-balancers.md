# Load Balancers

Distribution of tasks over set of resources. 

Fundamental feature: distribute incoming requests over cluster of backend servers according to a scheduling algorithm

Features:
- acts as [reverse proxy](https://www.cloudflare.com/en-in/learning/cdn/glossary/reverse-proxy/) - not expose IPs of servers
- increase performance - faster response
- no single point of failure
- scability
- increase reliability - fault tolerence (makes possible to continue operating despite failures or malfunctions)
- better security 
- perform continous heath checks of servers (Two kinds: 1. Shallow: pings servers 2. Deep: health and status of server)
- caching and compression

### Types of Load Balancers - based on function:

#### 1. Network Load Balancer / Layer 4 (L4) Load Balancer:
- 4th OSI layer: only [IP address + port] known
- How it works: 1. client send request to balancer (request: client IP -> balancer IP) 2. balancer choses a server according to a scheduling algorithm 3. balancer changes the addresses of the request to (request: balancer IP -> server IP) with [NAT](https://avinetworks.com/glossary/network-address-translation/) 4. balancer sends the request to the server 5. connect made  
- single TCP connection made btw client and server (client->balancer->server)
- no data reading - only passes packets of data to destination according to IP address
- Pros:

    - simpler
    - efficient / faster
    - one TCP connection - one chain btw source and destination
- Cons:
    - no smart load balancing based on data type - because no data reading
    - not for microservices - xyz.com/service1 and xyz.com/service2 can be completely different services  
    - no caching - because no data reading 
- Implement with: [HA Proxy](https://www.haproxy.com/documentation/hapee/latest/high-availability/active-active/l4-load-balancing/)

#### 2. Application Load Balancer / Layer 7 (L7) Load Balancer:
- 7th OSI Layer: autherized to see the data
- How it works: 1. client sends a request to balancer 2. balancer decrypts data 3. balancer picks a server logically assigned to deal with that data 3. balaner encrypts and makes a connection request to the server (with maybe new headers) 4. connection made
- two connections btw client and server (client->balancer and balancer->server)
- Pros:

    - smart load balancing - look at data and send it to logcally assigned servers
    - great for microservices
    - caching possible
- Cons:

    - expensive
    - decrypts 

### Load Balancing Algorithms

![](https://www.dnsstuff.com/wp-content/uploads/2020/01/the-five-most-common-balancing-methods-1024x536.jpg)
- Round robin - requests are distributed across the group of servers sequentially
- Least connections - request sent to the server with the fewest current connections to clients
- Least Time - requests set to the server selected by a formula that combines the fastest response time and fewest active connections
- IP Hash - hashing of IP decides which server (needed when requests of same client needs to go to single server)

### Real-life implementation
- Good idea to have a back-up load balancer (so balancers don't become the single point of failure) using `floating IPs`. One active at a time. 
- Load balancers can be placed between: a) the user and the web server b) web servers and application servers/cache servers c) application servers and database

### More to know

- DNS load balancing
- Direct routing
- IP tunneling
- Weighted 

## References 
- [https://www.appviewx.com/education-center/load-balancer-and-types/](https://www.appviewx.com/education-center/load-balancer-and-types/)
- [https://www.thegeekstuff.com/2016/01/load-balancer-intro/](https://www.thegeekstuff.com/2016/01/load-balancer-intro/)
- [https://levelup.gitconnected.com/load-balancers-a-deep-dive-7d17067f5ff6](https://levelup.gitconnected.com/load-balancers-a-deep-dive-7d17067f5ff6)
- [Youtube - Load balancing in Layer 4 vs Layer 7 with HAPROXY Examples](https://www.youtube.com/watch?v=aKMLgFVxZYk)
- [Youtube - Load balancers vs Revserse Proxy](https://www.youtube.com/watch?v=S8J2fkN2FeI)