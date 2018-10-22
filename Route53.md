Route53
----------

* What is DNS
  * If you've used the internet, you've used DNS. DNS is used to convert human friendly domain names into Internet Protocol (IP) addresses
  * IP addresses are commonly used by computers to identify each other on the network
  * IP addresses commonly come in 2 different forms, IPv4 and IPv6
* IPv4 vs IPv6
  * The IPv4 space is a 32 bit field and has over 4 billion different addresses (4,294,967,296 to be precise)
  * IPv6 was created to solve this depletion issue and has an address space of 128bits which in theory is 340,282,366,920,938,463,463,374,607,431,768,211,456 addresses or 340 undecillion addresses
* Top level domains
  * If we look at common domain names such as google.com, bbc.co.uk, etc. you will notice a string of chars separated by dots (periods). The last word in a domain name represents the "top level domain". The second word in a domain name is known as a second level domain name (this is optional though and depends on the domain name).
  * e.g. .com, .edu, .gov, .co.uk, .gov.uk, .com.au
  * These top level domain names are controlled by the Internet Assigned Number Authority (IANA) in a root zone database which is essentially a database of all availabe top level domains. You can view this database by visiting: http://www.iana.org/domains/root/db
* Domain Registrars
  * Because all of the names in a given domain have to be unique there needs to be a way to organize this all so that domain names aren't duplicated. This is where domain registrars come in. A registrar is an authority that can assign domain names directly under one or more top-level domains. These domains are registered with InterNIC, a service of ICANN, which enforces uniqueness of domain names across the Internet. Each domain name becomes registered in a central database known as WhoIS database.
  * Popular domain registrars include: GoDaddy.com, 123-reg-co.uk etc
  * Route53 got it's name because DNS runs on port 53
* DNS 101
  * Start of Authority Record (SOA)
    * The SOA record stores information about:
      * The name of the server that supplied the data for the zone.
      * The administrator of the zone.
      * The current version of the data file.
      * The default number of seconds for the time-to-live file on resource records.
  * NS Records
    * NS stands for Name Server records. They are used by Top Level Domain server to direct traffic to the Content DNS server which contains the authoritative DNS records.
  * A Records
    * An "A" record is the fundamental type of DNS record. The "A" in A record stands for "Address". The A record is used by a computer to translate the name of the domain to an IP address. For example, http://www.acloud.guru might point to http://123.10.10.80.
  * TTL - the length that a DNS record is cached on either the Resolvign Server or the users own local PC is equal to the value of the "Time to Live" (TTL) in seconds. The lower the time to live, the faster changes to DNS records take the propogate throughout the internet.
  * Alias records - unique to Route53
    * Aias records are used to map resource records sets in your hosted zone to Elastic Load balancers, CloudFront distributions, or S3 buckets that are configured as websites.
    * Alias records work like a CNAME record in that you can map one DNS name (www.example.com) to another 'target' DNS name (elb1234.elb.amazonaws.com).
    * Key difference - A CNAME can't be used for naked domain names (zone apex record.) You can't have a CNAME for http://mywebsite.com, it must be either an A record or an Alias.
  * Exam tips - DNS
    * ELBs do not have pre-defined IPv4 addresses; you resolve them using a DNS name.
    * Understand the different between an Alias Record and a CNAME.
    * Given the choise, always choose the Alias record over a CNAME.
    * SOA Records
      * A start of authority (SOA) record is information stored in a DNS zone about that zone. A DNS zone is the part of the domain for which an individual DNS server is reponsible (i.e. the bit that you store A records, C-names etc). Each zone contains a single SOA record.
    * Alias records
      * Alias record sets can save you time becuase Amazon Route 53 automatically recognizes changes in the record sets that the alias resource record set refers to. For example, suppose an alias resource record set for example.com points to an ELB load balancer at lb1-1234.us-east-1.elb.amazonaws.com. If the IP address of the load balancer changes, Amazon Route 53 will automatically reflect those changes in DNS answers for example.com without any changes to the hosted zone that contains resource record sets for example.com.
      * Bottom line: this is for pointing your domain to ELB's since ELB's can change IP's dynamically
    * Common DNS types (won't be on exams)
      * SOA records
      * NS records
      * A records
      * CNAMES
      * MX records - mail records - use case: point your email to gmail
      * PTR records
    * Know different types of routing
* Routing Policies Available on AWS
  * Simple routing
  * Weighted Routing
  * Latency-based Routing
  * Failover routing
  * geolocation routing
  * multivalue answer routing
* Simple Routing Policy
  * If you choose the simple routing policy you can only have one record with multiple IP addresses. If you specify multiple values in a record, Route 53 returns all values to the user in a random order.
* Weighted Routing Policy
  * Weighted Routing policies let you split your traffic based on different weights assigned.  
  * e.g. 20% of traffic to us-east-1 and 80% of the traffic to us-west-1
* Latency based routing
  * Latency based routing allows you to route your traffic based on the lowest network latency for your end user (ie which region will give them the fastest response time). To use latency-based routing, you create a latency resource record set for the Amazon EC2 (or ELB) resource in each region that hosts your website. When Amazon Route 53 receives a query for your site, it selects the latency resource record set for the region that gives the user the lowest latency. Route 53 then reponds with the value associated with that resource record set.
* Failover
  * Failover routing policies are used when you want to create an active/passive set up. For example, you may want your primary site to be in EU-WEST-2 and your secondary DR Site in AP-SOUTHEAST-2.
  * Route53 will monitor the health of your pirmary site using a health check.
  * A health check monitors the health of your endpoints.
* Geolocation Routing Policy
  * Geolocation routing lets you choose where your traffic will be sent based on the geographic location of your users (ie the location from which DNS queries originate). For example, you might want all queries from Europe to be routed to a fleet of EC2 instances that are specifically configured for your European customers. These servers may have the local language of your European customers and all prices are displayed in Euros.
* Multivalue
  * If you want to route traffic approximately randomly to multiple resources, such as web servers, you can create one multivalue answer record for each resource and, optionally, associate an Amazon Route 53 health check with each record. For example, suppose you manage an HTTP web service with a dozen web servers that each have their own IP address. No one web server could handle all of the traffic, but if you create a dozen multivalue records, Amazon Ruote 563 reponds to DNS queries with up to eight healthy records in reponse to each DNS query. Amazon Route 53 gives different answers to different DNS resolvers. If a web server becomes unavailable after a resolver caches a reponse, client software can try another IP address in the reponse.
* Route53 notes
  * Only 50 domain names are available by default, however this is a soft limit and can be raised by contacting AWS support.
