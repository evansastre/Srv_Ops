# DNS

## 1. Change DNS config

```text
vim /etc/resolv.conf 
vim  /etc/sysconfig/network-scripts/ifcfg-eth0
```

## 2.Check dns server

```text
nslookup domain.com
nslook www.youtube.com


dig @DNSip http://domain.com
dig @8.8.8.8 www.youtube.com
```

## 3. Record

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

  


## 4.When will use TCP in DNS?

Data is over 512 bit  or  zone transfer 



DNS 是互联网核心协议之一。不管是上网浏览，还是编程开发，都需要了解一点它的知识。

本文详细介绍DNS的原理，以及如何运用工具软件观察它的运作。我的目标是，读完此文后，你就能完全理解DNS。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCBEGWsdoMicuLwsTiav5th0J0SYZ1oGSyAqgn9JhY0WY8zcIKMib9Oia2og/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

###  

### **一、DNS 是什么？**

DNS （Domain Name System 的缩写）的作用非常简单，就是根据域名查出IP地址。你可以把它想象成一本巨大的电话本。

举例来说，如果你要访问域名math.stackexchange.com，首先要通过DNS查出它的IP地址是151.101.129.69。

如果你不清楚为什么一定要查出IP地址，才能进行网络通信，建议先阅读我写的 《互联网协议入门》 。

### **二、查询过程**

虽然只需要返回一个IP地址，但是DNS的查询过程非常复杂，分成多个步骤。

工具软件dig可以显示整个查询过程。

```text
$ dig math.stackexchange.com
```

上面的命令会输出六段信息。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCc9Kdepbyq4FJhpFFhtIG1ZK7YPLzkIu2bEw2pP1hYYcK3PDGBh5Dwg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

第一段是查询参数和统计。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZC3ENwbTaFm5pvrzzibgfzgsVkRov15wFvgvZROUVcPEJSzDbicgicWZ3Uw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

第二段是查询内容。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCGaMqcZta7UPXVnyo6sNkxQVnSOmxzVmzFkxXF7qIjy1f2hZGY4dlgA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面结果表示，查询域名math.stackexchange.com的A记录，A是address的缩写。

第三段是DNS服务器的答复。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCiaFFicQBcPAGqaoyxywDbCP4d0Knt7ZNiceib4j2FDr2732SKyAm8Tcglg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面结果显示，math.stackexchange.com有四个A记录，即四个IP地址。600是TTL值（Time to live 的缩写），表示缓存时间，即600秒之内不用重新查询。

第四段显示stackexchange.com的NS记录（Name Server的缩写），即哪些服务器负责管理stackexchange.com的DNS记录。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCtaWibPOFgqVYFWSNwKKIoa3f2icTwTDEkVuvWcMNyF7jS1fSiaarPNRDQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面结果显示stackexchange.com共有四条NS记录，即四个域名服务器，向其中任一台查询就能知道math.stackexchange.com的IP地址是什么。

第五段是上面四个域名服务器的IP地址，这是随着前一段一起返回的。

第六段是DNS服务器的一些传输信息。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCnicQtMLiceT5agmsVMF65env80ibEI7vRUDhD3vHsZqpWqbc98Cj5QJ3A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面结果显示，本机的DNS服务器是192.168.1.253，查询端口是53（DNS服务器的默认端口），以及回应长度是305字节。

如果不想看到这么多内容，可以使用+short参数。

```text
$ dig +short math.stackexchange.com

151.101.129.69
151.101.65.69
151.101.193.69
151.101.1.69
```

上面命令只返回math.stackexchange.com对应的4个IP地址（即A记录）。

### **三、DNS服务器**

下面我们根据前面这个例子，一步步还原，本机到底怎么得到域名math.stackexchange.com的IP地址。

首先，本机一定要知道DNS服务器的IP地址，否则上不了网。通过DNS服务器，才能知道某个域名的IP地址到底是什么。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCBtzicpiaOu1ia3NViaxSxGnNLm3YG8DzXSmebmic52lkfKwkJWWxj25GuSg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

DNS服务器的IP地址，有可能是动态的，每次上网时由网关分配，这叫做DHCP机制；也有可能是事先指定的固定地址。Linux系统里面，DNS服务器的IP地址保存在/etc/resolv.conf文件。

上例的DNS服务器是192.168.1.253，这是一个内网地址。有一些公网的DNS服务器，也可以使用，其中最有名的就是Google的8.8.8.8和Level 3的4.2.2.2。

本机只向自己的DNS服务器查询，dig命令有一个@参数，显示向其他DNS服务器查询的结果。

```text
$ dig @4.2.2.2 math.stackexchange.com
```

上面命令指定向DNS服务器4.2.2.2查询。  


### 四、域名的层级

DNS服务器怎么会知道每个域名的IP地址呢？答案是分级查询。

请仔细看前面的例子，每个域名的尾部都多了一个点。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCGaMqcZta7UPXVnyo6sNkxQVnSOmxzVmzFkxXF7qIjy1f2hZGY4dlgA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

比如，域名math.stackexchange.com显示为math.stackexchange.com.。这不是疏忽，而是所有域名的尾部，实际上都有一个根域名。

举例来说，www.example.com真正的域名是www.example.com.root，简写为www.example.com.。因为，根域名.root对于所有域名都是一样的，所以平时是省略的。

根域名的下一级，叫做”顶级域名”（top-level domain，缩写为TLD），比如.com、.net；再下一级叫做”次级域名”（second-level domain，缩写为SLD），比如www.example.com里面的.example，这一级域名是用户可以注册的；再下一级是主机名（host），比如www.example.com里面的www，又称为”三级域名”，这是用户在自己的域里面为服务器分配的名称，是用户可以任意分配的。

总结一下，域名的层级结构如下。

```text
主机名.次级域名.顶级域名.根域名
# 即
host.sld.tld.root
```

### **五、根域名服务器**

DNS服务器根据域名的层级，进行分级查询。

需要明确的是，每一级域名都有自己的NS记录，NS记录指向该级域名的域名服务器。这些服务器知道下一级域名的各种记录。

所谓”分级查询”，就是从根域名开始，依次查询每一级域名的NS记录，直到查到最终的IP地址，过程大致如下。

1. 从”根域名服务器”查到”顶级域名服务器”的NS记录和A记录（IP地址）
2. 从”顶级域名服务器”查到”次级域名服务器”的NS记录和A记录（IP地址）
3. 从”次级域名服务器”查出”主机名”的IP地址

仔细看上面的过程，你可能发现了，没有提到DNS服务器怎么知道”根域名服务器”的IP地址。回答是”根域名服务器”的NS记录和IP地址一般是不会变化的，所以内置在DNS服务器里面。

下面是内置的根域名服务器IP地址的一个例子。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCdmp7Eu6tZ1nicCw2qCiaFGB1VnFPtsqYdJMx9OlicicfoGFibtxKX30tmzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面列表中，列出了根域名（.root）的三条NS记录A.ROOT-SERVERS.NET、B.ROOT-SERVERS.NET和C.ROOT-SERVERS.NET，以及它们的IP地址（即A记录）198.41.0.4、192.228.79.201、192.33.4.12。

另外，可以看到所有记录的TTL值是3600000秒，相当于1000小时。也就是说，每1000小时才查询一次根域名服务器的列表。

目前，世界上一共有十三组根域名服务器，从A.ROOT-SERVERS.NET一直到M.ROOT-SERVERS.NET。

### **六、分级查询的实例**

dig命令的+trace参数可以显示DNS的整个分级查询过程。

```text
$ dig +trace math.stackexchange.com
```

上面命令的第一段列出根域名.的所有NS记录，即所有根域名服务器。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCLsEqCapqHl5GYIxvrWeonDR60XvatMP8HEg5at4OOVCic6OoRulct3g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

根据内置的根域名服务器IP地址，DNS服务器向所有这些IP地址发出查询请求，询问math.stackexchange.com的顶级域名服务器com.的NS记录。最先回复的根域名服务器将被缓存，以后只向这台服务器发请求。

接着是第二段。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCXh9cBsoUWBNcmd1d1iaapzM4hgvYaic6HGCOqlddS173sl7TAhbHBaJg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面结果显示.com域名的13条NS记录，同时返回的还有每一条记录对应的IP地址。

然后，DNS服务器向这些顶级域名服务器发出查询请求，询问math.stackexchange.com的次级域名stackexchange.com的NS记录。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCKpqAXO7rhg4Rrkxv6a8e7FNnN1cz8Ev7aCiblpT9bicSsCr4Uicym3icRw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面结果显示stackexchange.com有四条NS记录，同时返回的还有每一条NS记录对应的IP地址。

然后，DNS服务器向上面这四台NS服务器查询math.stackexchange.com的主机名。

![](https://mmbiz.qpic.cn/mmbiz/9aPYe0E1fb0nmRUaVrbsUvt6LtTMEbZCcXHEj574PmozRHs4mD8opcSMOpbrEz4z52WSQ52Xe6ljVGCE8ekz9g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面结果显示，math.stackexchange.com有4条A记录，即这四个IP地址都可以访问到网站。并且还显示，最先返回结果的NS服务器是ns-463.awsdns-57.com，IP地址为205.251.193.207。

### **七、NS 记录的查询**

dig命令可以单独查看每一级域名的NS记录。

```text
$ dig ns com
$ dig ns stackexchange.com
```

+short参数可以显示简化的结果。  


```text
$ dig +short ns com
$ dig +short ns stackexchange.com
```

### **八、DNS的记录类型**

域名与IP之间的对应关系，称为”记录”（record）。根据使用场景，”记录”可以分成不同的类型（type），前面已经看到了有A记录和NS记录。

常见的DNS记录类型如下。

  
（1） A：地址记录（Address），返回域名指向的IP地址。

（2） NS：域名服务器记录（Name Server），返回保存下一级域名信息的服务器地址。该记录只能设置为域名，不能设置为IP地址。

（3）MX：邮件记录（Mail eXchange），返回接收电子邮件的服务器地址。

（4）CNAME：规范名称记录（Canonical Name），返回另一个域名，即当前查询的域名是另一个域名的跳转，详见下文。

（5）PTR：逆向查询记录（Pointer Record），只用于从IP地址查询域名，详见下文。  
  


一般来说，为了服务的安全可靠，至少应该有两条NS记录，而A记录和MX记录也可以有多条，这样就提供了服务的冗余性，防止出现单点失败。

CNAME记录主要用于域名的内部跳转，为服务器配置提供灵活性，用户感知不到。举例来说，facebook.github.io这个域名就是一个CNAME记录。

```text
$ dig facebook.github.io
...
;; ANSWER SECTION:
facebook.github.io. 3370    IN  CNAME   github.map.fastly.net.
github.map.fastly.net.  600 IN  A   103.245.222.133
```

上面结果显示，facebook.github.io的CNAME记录指向github.map.fastly.net。也就是说，用户查询facebook.github.io的时候，实际上返回的是github.map.fastly.net的IP地址。这样的好处是，变更服务器IP地址的时候，只要修改github.map.fastly.net这个域名就可以了，用户的facebook.github.io域名不用修改。  


由于CNAME记录就是一个替换，所以域名一旦设置CNAME记录以后，就不能再设置其他记录了（比如A记录和MX记录），这是为了防止产生冲突。举例来说，foo.com指向bar.com，而两个域名各有自己的MX记录，如果两者不一致，就会产生问题。由于顶级域名通常要设置MX记录，所以一般不允许用户对顶级域名设置CNAME记录。

PTR记录用于从IP地址反查域名。dig命令的-x参数用于查询PTR记录。

```text
$ dig -x 192.30.252.153
...
;; ANSWER SECTION:
153.252.30.192.in-addr.arpa. 3600 IN    PTR pages.github.com.
```

上面结果显示，192.30.252.153这台服务器的域名是pages.github.com。  


逆向查询的一个应用，是可以防止垃圾邮件，即验证发送邮件的IP地址，是否真的有它所声称的域名。

dig命令可以查看指定的记录类型。

```text
$ dig a github.com
$ dig ns github.com
$ dig mx github.com
```

###  

### **九、其他DNS工具**

除了dig，还有一些其他小工具也可以使用。

**（1）host 命令**

host命令可以看作dig命令的简化版本，返回当前请求域名的各种记录。

```text
$ host github.com

github.com has address 192.30.252.121
github.com mail is handled by 5 ALT2.ASPMX.L.GOOGLE.COM.
github.com mail is handled by 10 ALT4.ASPMX.L.GOOGLE.COM.
github.com mail is handled by 10 ALT3.ASPMX.L.GOOGLE.COM.
github.com mail is handled by 5 ALT1.ASPMX.L.GOOGLE.COM.
github.com mail is handled by 1 ASPMX.L.GOOGLE.COM.

$ host facebook.github.com

facebook.github.com is an alias for github.map.fastly.net.
github.map.fastly.net has address 103.245.222.133
```

host命令也可以用于逆向查询，即从IP地址查询域名，等同于dig -x 。  


```text
$ host 192.30.252.153
153.252.30.192.in-addr.arpa domain name pointer pages.github.com.
```

**（2）nslookup 命令**  


nslookup命令用于互动式地查询域名记录。

```text
$ nslookup

> facebook.github.io
Server:     192.168.1.253
Address:    192.168.1.253#53

Non-authoritative answer:
facebook.github.io  canonical name = github.map.fastly.net.
Name:   github.map.fastly.net
Address: 103.245.222.133
>
```

**（3）whois 命令**

whois命令用来查看域名的注册情况。

```text
$ whois github.com
```

## **十、参考文章**

* DNS: The Good Parts, by Pete Keen
* DNS 101, by Mark McDonnell

**附：DNS百科**

DNS（Domain Name System，域名系统），因特网上作为域名和IP地址相互映射的一个分布式数据库，能够使用户更方便的访问互联网，而不用去记住能够被机器直接读取的IP数串。通过主机名，最终得到该主机名对应的IP地址的过程叫做域名解析（或主机名解析）。DNS协议运行在UDP协议之上，使用端口号53。在RFC文档中RFC 2181对DNS有规范说明，RFC 2136对DNS的动态更新进行说明，RFC 2308对DNS查询的反向缓存进行说明。

**DNS功能**  


每个IP地址都可以有一个主机名，主机名由一个或多个字符串组成，字符串之间用小数点隔开。有了主机名，就不要死记硬背每台IP设备的IP地址，只要记住相对直观有意义的主机名就行了。这就是DNS协议所要完成的功能。

主机名到IP地址的映射有两种方式：

1）静态映射，每台设备上都配置主机到IP地址的映射，各设备独立维护自己的映射表，而且只供本设备使用；

2）动态映射，建立一套域名解析系统（DNS），只在专门的DNS服务器上配置主机到IP地址的映射，网络上需要使用主机名通信的设备，首先需要到DNS服务器查询主机所对应的IP地址。

通过主机名，最终得到该主机名对应的IP地址的过程叫做域名解析（或主机名解析）。在解析域名时，可以首先采用静态域名解析的方法，如果静态域名解析不成功，再采用动态域名解析的方法。可以将一些常用的域名放入静态域名解析表中，这样可以大大提高域名解析效率。

**DNS安全问题**

1.针对域名系统的恶意攻击：DDOS攻击造成域名解析瘫痪。

2.域名劫持：修改注册信息、劫持解析结果。

3.国家性质的域名系统安全事件：“.ly”域名瘫痪、“.af”域名的域名管理权变更。

4.系统上运行的DNS服务存在漏洞，导致被黑客获取权限，从而篡改DNS信息。

5.DNS设置不当，导致泄漏一些敏感信息。提供给黑客进一步攻击提供有力信息

