# DNS

1. Change DNS config

```text
vim /etc/resolv.conf 
vim  /etc/sysconfig/network-scripts/ifcfg-eth0
```

2.Check dns server

```text
nslookup domain.com
nslook www.youtube.com


dig @DNSip http://domain.com
dig @8.8.8.8 www.youtube.com
```

3. Record

```text
A  hostname to IP, IPv4
AAA  hostname to IP, IPv6
CNAME  domainname1 to domainname2, redirect
MX   mail exchange

```

Zone DNS database is a collection of resource records and each of the records provides information about a specific object. A list of most common records is provided below:

* [Address Mapping records](http://tools.ietf.org/html/rfc1035#page-12) \(A\)

  The record A specifies IP address \(IPv4\) for given host. A records are used for conversion of domain names to corresponding IP addresses.

* [IP Version 6 Address records](http://tools.ietf.org/html/rfc3596#page-3) \(AAAA\)

  The record AAAA \(also quad-A record\) specifies IPv6 address for given host. So it works the same way as the A record and the difference is the type of IP address.

* [Canonical Name records](http://tools.ietf.org/html/rfc1035#page-14) \(CNAME\)

  The CNAME record specifies a domain name that has to be queried in order to resolve the original DNS query. Therefore CNAME records are used for creating aliases of domain names. CNAME records are truly useful when we want to alias our domain to an external domain. In other cases we can remove CNAME records and replace them with A records and even decrease performance overhead.

* [Host Information records](http://tools.ietf.org/html/rfc1035#page-14) \(HINFO\)

  HINFO records are used to acquire general information about a host. The record specifies type of CPU and OS. The HINFO record data provides the possibility to use operating system specific protocols when two hosts want to communicate. For security reasons the HINFO records are not typically used on public servers.

  **Note:** Standard values in [RFC 1010](http://tools.ietf.org/html/rfc1010)

* [Integrated Services Digital Network records](http://tools.ietf.org/html/rfc1183#section-3.2) \(ISDN\)

  The ISDN resource record specifies ISDN address for a host. An ISDN address is a telephone number that consists of a country code, a national destination code, a ISDN Subscriber number and, optionally, a ISDN subaddress. The function of the record is only variation of the A resource record function.

* [Mail exchanger record](http://tools.ietf.org/html/rfc1035#section-3.3.9) \(MX\)

  The MX resource record specifies a mail exchange server for a DNS domain name. The information is used by Simple Mail Transfer Protocol \(SMTP\) to route emails to proper hosts. Typically, there are more than one mail exchange server for a DNS domain and each of them have set priority.**Example:**

  ```text
  msn.com MX preference = 5, mail exchanger = mx2.hotmail.com
  msn.com MX preference = 5, mail exchanger = mx3.hotmail.com
  msn.com MX preference = 5, mail exchanger = mx4.hotmail.com
  msn.com MX preference = 5, mail exchanger = mx1.hotmail.com

  msn.com nameserver = ns3.msft.net
  msn.com nameserver = ns5.msft.net
  msn.com nameserver = ns4.msft.net
  msn.com nameserver = ns1.msft.net
  msn.com nameserver = ns2.msft.net
  mx1.hotmail.com internet address = 65.55.92.184
  mx1.hotmail.com internet address = 65.54.188.72
  mx1.hotmail.com internet address = 65.54.188.94
  mx1.hotmail.com internet address = 65.54.188.110
  mx1.hotmail.com internet address = 65.54.188.126
  mx1.hotmail.com internet address = 65.55.37.72
  mx1.hotmail.com internet address = 65.55.37.88
  mx1.hotmail.com internet address = 65.55.37.104
  mx1.hotmail.com internet address = 65.55.37.120
  mx1.hotmail.com internet address = 65.55.92.136
  mx1.hotmail.com internet address = 65.55.92.152
  mx1.hotmail.com internet address = 65.55.92.168
  ```

* [Name Server records](http://tools.ietf.org/html/rfc1035#section-3.3.11) \(NS\)

  The NS record specifies an authoritative name server for given host.

* [Reverse-lookup Pointer records](http://tools.ietf.org/html/rfc1035#section-3.3.12) \(PTR\)

  As opposed to forward DNS resolution \(A and AAAA DNS records\), the PTR record is used to look up domain names based on an IP address.

* [Start of Authority records](http://tools.ietf.org/html/rfc1035#section-3.3.13) \(SOA\)

  The record specifies core information about a DNS zone, including the primary name server, the email of the domain administrator, the domain serial number, and several timers relating to refreshing the zone.

* [Text records](http://tools.ietf.org/html/rfc1035#section-3.3.14) \(TXT\)

  The text record can hold arbitrary non-formatted text string. Typically, the record is used by [Sender Policy Framework](http://en.wikipedia.org/wiki/Sender_Policy_Framework) \(SPF\) to prevent fake emails to appear to be sent by you.

TOP 10 Tools

1. [Blacklist Checker \(9943821x\)](http://mail-blacklist-checker.online-domain-tools.com/)
2. [Blacklist Monitor \(9537555x\)](http://mail-blacklist-monitor.online-domain-tools.com/)
3. [Symmetric Ciphers \(3935687x\)](http://symmetric-ciphers.online-domain-tools.com/)
4. [Email Verifier \(2721261x\)](http://email-verifier.online-domain-tools.com/)
5. [Encoders and Decoders \(1723070x\)](http://encoders-decoders.online-domain-tools.com/)
6. [Whois \(1583099x\)](http://whois.online-domain-tools.com/)
7. [DNS Record Viewer \(1519512x\)](http://dns-record-viewer.online-domain-tools.com/)
8. [MX Lookup \(832438x\)](http://mxlookup.online-domain-tools.com/)
9. [Reverse Hash Lookup \(820836x\)](http://reverse-hash-lookup.online-domain-tools.com/)
10. [Nmap \(379310x\)](http://nmap.online-domain-tools.com/)

Advertisement

News

* **07.11.2017** – We have updated and extended our WHOIS record parsers that are used by [Bulk Whois API](https://bulk-whois-api.com/) project as well as our [Whois Online tool](http://whois.online-domain-tools.com/). Us… [&gt;&gt;](http://online-domain-tools.com/news)
* **20.08.2017** – We have removed dysfunctional blacklists from our database and we have added new blacklists as well. This database is used by our … [&gt;&gt;](http://online-domain-tools.com/news)

[![](http://dns-record-viewer.online-domain-tools.com/images/BC_Rnd_94px_2.png)](http://blog.online-domain-tools.com/2014/06/01/server-monitoring-for-bitcoins/?ref=bb)Social Networks

  


4.When will use TCP in DNS?

Data is over 512 bit  or  zone transfer 

5.

