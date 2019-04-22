# BGP

{% embed url="https://searchnetworking.techtarget.com/feature/BGP-tutorial-The-routing-protocol-that-makes-the-Internet-work" %}



{% embed url="https://searchnetworking.techtarget.com/definition/BGP-Border-Gateway-Protocol" %}



BGP \(Border Gateway Protocol\) is [protocol](https://searchnetworking.techtarget.com/definition/protocol) that manages how packets are routed across the internet through the exchange of routing and reachability information between [edge routers](https://searchsdn.techtarget.com/definition/edge-router). BGP directs packets between autonomous systems \([AS](https://searchnetworking.techtarget.com/definition/autonomous-system)\) -- networks managed by a single enterprise or service provider. Traffic that is routed within a single network AS is referred to as internal BGP, or iBGP. More often, BGP is used to connect one AS to other autonomous systems, and it is then referred to as an external BGP, or eBGP.  


If you have to explain what BGP is to someone new to the service provider environment, the best definition is that it's the routing protocol that makes the internet work. As the address allocation in the internet is not nearly as hierarchical as the telephone dialing plan, most of the routers in service providers' core networks need to exchange information about several hundred thousand IP prefixes. BGP is still able to accomplish that task, which is proof it's a highly scalable routing protocol.

BGP routing information is usually exchanged between competing business entities in the form of internet service providers \([ISPs](https://searchwindevelopment.techtarget.com/definition/ISP)\) in an open, hostile environment -- the public internet. BGP is very security-focused -- for example, all adjacent routers have to be configured manually -- and decent BGP implementations provide a rich set of route filters to allow ISPs to defend their networks and control what they advertise to their competitors.

#### How BGP works

In [BGP](https://searchnetworking.techtarget.com/news/450425946/VMware-network-security-improves-with-AppDefense-launch) terminology, an independent routing domain, which almost always means an ISP network, is called an [autonomous system](https://searchnetworking.techtarget.com/definition/autonomous-system).

BGP is always used as the routing protocol of choice between ISPs \(known as external BGP\), but also as the core routing protocol within large ISP networks \(known as internal BGP\).

All other routing protocols are concerned solely with finding the optimal path toward all known destinations. BGP cannot take this simplistic approach because the [peering](https://searchtelecom.techtarget.com/definition/peering) agreements between ISPs almost always result in complex routing policies. To help network operators implement these policies, BGP carries a large number of attributes with each IP prefix, for example:

* **Autonomous system \(AS\) path** -- the complete path documenting which autonomous systems a packet would have to travel through to reach the destination.
* **Local preference** -- the internal cost of a destination, which is used to ensure AS-wide consistency.
* **Multi-exit discriminator** -- this attribute gives adjacent ISPs the ability to prefer one peering point over another.
* **Communities** -- a set of generic tags that can be used to signal various administrative policies between BGP routers.

Because the focus of BGP design and implementation was always on security and scalability, it is harder to configure than other routing protocols, more complex -- more so when you start configuring various routing policies -- and one of the slowest converging routing protocols.

The slow BGP convergence dictates a two-protocol design of an ISP network:

* An internal routing protocol -- most often, Open Shortest Path First \([OSPF](https://searchenterprisewan.techtarget.com/definition/OSPF)\) or Intermediate System to Intermediate System \([IS-IS](https://searchnetworking.techtarget.com/definition/IS-IS)\) -- is used to achieve fast convergence for internal routes, including IP addresses of BGP routers.
* BGP is used to exchange internet routes.

A failure within the core network would thus be quickly bypassed, thanks to fast convergence of OSPF or IS-IS, whereas BGP on top of an internal routing protocol would meet the scalability, security and policy requirements. Even more, if you migrate all your customer routes into BGP, the customer problems -- for example, link flaps between your router and customer's router -- will not affect the stability of your core network.

Because of BGP's inherent complexity, customers and small ISPs would deploy BGP only where needed -- for example, on peering points and on a minimal subset of core routers \(the ones between the peering points\), as shown in the following diagram.![BGP peering points](https://cdn.ttgtmedia.com/digitalguide/images/Misc/intro_bgp_1.gif)Minimal BGP deployment

The BGP-speaking routers would also have to generate a default route into the internal routing protocol to attract the traffic for internet destinations not known to other routers in your network.

As your ISP business grows, however, your customers will start requiring BGP connectivity -- any customer who wants to achieve truly redundant internet access has to have its own [autonomous system](https://searchnetworking.techtarget.com/definition/autonomous-system) and exchange BGP information with its ISPs -- and you'll be forced to deploy BGP on more and more core and edge routers \(see the following diagram\). It is, therefore, best you include BGP on all core and major edge routers as part of your initial network design. Even though you might not deploy it everywhere with the initial network deployment, having a good blueprint will definitely help you when you have to scale the BGP-speaking part of your network.![BGP on core and edge routers](https://cdn.ttgtmedia.com/digitalguide/images/Misc/intro_bgp_2.gif)BGP included in network design

BGP requires a full mesh of internal BGP sessions -- sessions between routers in the same autonomous system. You could use BGP route reflectors or BGP confederations to make your network scalable.

Another excellent reason why you'd want to deploy BGP throughout your network is because MPLS-based [virtual private networks](https://searchnetworking.techtarget.com/definition/virtual-private-network), large-scale [quality-of-service](https://searchunifiedcommunications.techtarget.com/definition/QoS-Quality-of-Service) deployments or large-scale differentiated web caching implementations rely on BGP to transport the information they need.  

BGP is, without doubt, the most complex IP routing protocol currently deployed in the internet. Its complexity is primarily due to its focus on security and routing policies -- BGP is used to exchange cooperative information \(internet routes\) between otherwise competing entities \(service providers\), and it has to be able to implement whatever has been agreed upon in interprovider peering agreements. These agreements often have little to do with technically optimum services.

A structured approach to BGP troubleshooting, however, as illustrated in this and the next section, can quickly lead you from initial problem diagnosis to the solution. Here, we focus on a simple scenario with a single BGP-speaking router in your network \(see the following diagram\). Similar designs are commonly used by multihomed customers and small internet service providers that do not offer BGP connectivity to their customers.![BGP troubleshooting](https://cdn.ttgtmedia.com/digitalguide/images/Misc/bgp_ts.gif)Troubleshooting BGP problems

#### Identifying a BGP problem

Before jumping into BGP troubleshooting, you have to identify the source of the connectivity problem you're debugging -- usually, you suspect that BGP might be involved if one of your customers reports limited or no internet connectivity beyond your network. Perform a [traceroute](https://whatis.techtarget.com/definition/traceroute)from a workstation on the problematic local area network \([LAN](https://searchnetworking.techtarget.com/definition/local-area-network-LAN)\). If the trace reaches the first BGP-speaking router -- or, even better, if it gets beyond the edge of your network -- you're probably dealing with a BGP issue. Otherwise, check whether the BGP-speaking router advertises a default route into your network -- without a default route, other routers in your network cannot reach the internet destinations.

If you don't have access to a LAN-attached workstation, you can perform the traceroute from the customer-premises router, but you have to ensure the source IP address used in the traceroute packets is the router's LAN address.

#### Troubleshooting adjacent BGP router issues

BGP has to establish a [TCP](https://searchnetworking.techtarget.com/definition/TCP-IP) session between adjacent BGP routers before they can exchange routes. The first check is thus the status of the BGP sessions between the routers.

The BGP neighbors are configured manually, and the two most probable configuration errors are:

* **Neighbor IP address mismatch:** The destination IP address configured on one BGP neighbor has to match the source IP address -- or the IP address of the directly connected interface -- configured on the other.
* **AS number mismatch:** The neighbor AS number configured on one side of the BGP session has to match the actual BGP AS number used by the neighbor.

You could also have a problem with packet filters deployed on the BGP-speaking router. These filters have to allow packets to and from TCP port 179.

#### Troubleshooting BGP route propagation

If your users want to receive traffic from the internet, the IP prefix assigned to your network must be visible throughout the internet. To get there, three steps are needed:

* Your BGP router must insert your IP prefix into its BGP table.
* The IP prefix must be advertised to its BGP neighbors.
* The IP prefix must be propagated throughout the internet.

**Is the route inserted into BGP?** Most routing protocols automatically insert directly connected [IP subnets](https://searchnetworking.techtarget.com/tutorial/IP-addressing-and-subnetting-fundamentals) into their routing tables or databases. Due to security requirements, BGP is an exception. It will originate an IP prefix only if it's manually configured to do so -- for example, Cisco routers use the network statement to configure advertised IP prefixes. Another option is route redistribution, which is highly discouraged in the internet environment.

Furthermore, to avoid attracting unroutable traffic, BGP will announce a configured IP prefix only if there's a matching route in the IP routing table. You could generate the matching IP route through route summarization, but it's usually best to configure a static route pointing to a null interface -- or its equivalent.

To check whether your IP prefix is in your BGP routing table, use a BGP show command -- for example, show ip bgp prefix mask on a Cisco router.

**Is the route advertised to your neighbors?** By default, all IP prefixes residing in the BGP table are announced to all BGP neighbors. Owing to security and routing policy requirements, the default behavior is usually modified with a set of output and input filters. If you have applied output filters toward your BGP neighbors, you have to check whether these filters allow your IP prefix to be propagated to the external BGP neighbors. The command to display routes advertised to a BGP neighbor on a Cisco router is: show ip bgp neighbor ip-address advertised.

**Is the route visible throughout the internet?** Even if you have successfully announced your IP prefix to your BGP neighbors, it might still not be propagated throughout the internet. It's hard to figure out exactly what is propagated beyond the boundaries of your network. The tools that can help you are called BGP [looking glasses](http://www.bgp4.as/looking-glasses). Using these tools, you can inspect BGP tables at various points throughout the internet and check whether your IP prefix has made it to those destinations.

A few factors could cause your IP prefix to be blocked somewhere in the internet. The most common one is BGP route flap dampening: If an IP prefix flaps, or disappears and reappears, too often in a short period of time -- for example, if you clear your BGP sessions or change your BGP configuration -- the prefix gets blocked for an extended period of time \(by default, up to an hour\). If your IP prefix is dampened, there's nothing you can do except wait it out. You could also have an invalid, or missing, entry in IP routing registries, or there may be inbound filters at one of the upstream ISPs. In all of these cases, it's best if your upstream ISP can help you resolve the problem -- which is, at this point, beyond the scope of technical BGP troubleshooting.

#### Advanced BGP troubleshooting

In the previous section of this e-guide, we addressed some basic BGP troubleshooting skills:

* How to identify whether a routing problem is a BGP problem;
* How to troubleshoot BGP sessions; and
* How to troubleshoot IP route origination and propagation.

Now, let's focus on a more advanced scenario: transit ISP networks \(see diagram below\).![BGP ISP peering](https://cdn.ttgtmedia.com/digitalguide/images/Misc/ts_bgp_1.gif)Advanced BGP troubleshooting

To establish end-to-end connectivity across a service provider network, the ISP has to receive customers' IP prefixes via BGP and announce them to other ISPs. The same process has to happen in reverse direction -- or, at least, the default route has to be announced to the customer. The networkwide BGP troubleshooting is thus composed of three steps:

* [Prev](https://searchnetworking.techtarget.com/feature/BGP-tutorial-The-routing-protocol-that-makes-the-Internet-work#prev)
* [Next](https://searchnetworking.techtarget.com/feature/BGP-tutorial-The-routing-protocol-that-makes-the-Internet-work#next)
* [![](https://cdn.ttgtmedia.com/rms/contributors/ipepelnjak-sm.jpg)](https://www.techtarget.com/contributor/Ivan-Pepelnjak)

  [Ivan Pepelnjak](https://www.techtarget.com/contributor/Ivan-Pepelnjak) asks:

  **In understanding how BGP works, what kind of troubleshooting approach did you take to solving problems?**

  [Join the Discussion](https://searchnetworking.techtarget.com/feature/BGP-tutorial-The-routing-protocol-that-makes-the-Internet-work#commenting)

* [Prev](https://searchnetworking.techtarget.com/feature/BGP-tutorial-The-routing-protocol-that-makes-the-Internet-work#prev)
* [Next](https://searchnetworking.techtarget.com/feature/BGP-tutorial-The-routing-protocol-that-makes-the-Internet-work#next)
* [![](https://cdn.ttgtmedia.com/rms/contributors/ipepelnjak-sm.jpg)](https://www.techtarget.com/contributor/Ivan-Pepelnjak)

  [Ivan Pepelnjak](https://www.techtarget.com/contributor/Ivan-Pepelnjak) asks:

  **In understanding how BGP works, what kind of troubleshooting approach did you take to solving problems?**

  [Join the Discussion](https://searchnetworking.techtarget.com/feature/BGP-tutorial-The-routing-protocol-that-makes-the-Internet-work#commenting)

  * 1
  * 2

* Receiving the IP prefix;
* Propagating the IP prefix across our network; and
* Sending the IP prefix to external BGP neighbors at the other edge of the network.

**Have we received the prefix?** Troubleshooting inbound BGP problems is the toughest part of BGP troubleshooting you will encounter. The two potential reasons an IP prefix is not in your BGP table as you would expect it to be are:

* The neighbor is not sending the prefix.
* Your inbound filters are blocking the prefix.

The only tool that can help you identify the problem is the debugging facility on your edge router -- as you normally don't have access to the other BGP neighbor. When doing BGP debugging, be aware a BGP neighbor can send you several hundred thousand routes, so you have to ensure the debugging output produced by the troubleshooting session does not overwhelm the router. Furthermore, the BGP prefixes are sent only when they change, not on a periodic basis, like RIP updates or OSPF LSA floods. Your debugging tool will thus not show you an IP prefix until it has actually changed, or you've cleared the BGP session with your neighbor.

Some BGP routers have the ability to store a separate copy of all routes sent by a neighbor into a parallel BGP table. To enable this functionality on Cisco IOS, you have to configure soft-reconfiguration in for a BGP neighbor. With the parallel per-neighbor table, you can pinpoint exactly what the neighbor has sent you \(the content of the parallel table\) and the routes that have passed your input filters \(the contents of the main BGP table\). But, of course, the parallel per-neighbor table consumes a large amount of memory.

**Is the IP prefix propagated across our network?** Even when an edge router receives an IP prefix via BGP, it may not be propagated to the other end of your network. To start with, internal BGP -- BGP within a single autonomous system -- requires a full mesh of BGP sessions among all BGP routers. As every router between every pair of edge routers has to run BGP -- otherwise, the traffic could be dropped inside your network -- the number of BGP sessions could become excessively large. The following diagram illustrates the BGP sessions needed in a small four-router network.![Internal BGP routing](https://cdn.ttgtmedia.com/digitalguide/images/Misc/ts_bgp_2.gif)Full-mesh internal BGP

Two tools -- BGP route reflectors and BGP confederations -- can help you keep the number of BGP sessions to a sensible level, with BGP route reflectors being the most commonly used.

The BGP route reflector rules are quite simple:

* Whatever is received from a route-reflector client or an external BGP peer will be sent to every other BGP peer.
* Whatever is received from a router that is not a route-reflector client will be sent only to clients and external BGP peers.

With these rules in hand, you have to step through the graph of BGP sessions in your network, checking every BGP router on the way and ensuring the route-reflector rules are not violated -- and, using the rules, the BGP prefixes get from every edge router to all other routers.

Another common reason an IP prefix is not propagated across your network is the external subnets on the edge of your network are not advertised to your core routers.

The IP address of the next-hop router is not changed when an IP prefix is sent to an internal BGP neighbor. The IP next-hop of an external route is thus always the IP address of a router one hop beyond the edge of your autonomous system. The IP subnets connecting your edge routers to their external neighbors thus have to be inserted into your internal routing protocol -- for example, OSPF or IS-IS -- otherwise, some internal BGP router will decide that the BGP next-hop is not reachable and ignore the IP prefix. It will appear in the BGP table, but will not be used or propagated to other BGP peers.

**Is the prefix sent to external neighbors?** As the last step in troubleshooting BGP route propagation, you have to check whether the IP prefixes transported across your network are announced to your external BGP peers. The techniques for troubleshooting outbound BGP route propagation are explained in the [Border Gateway Protocol \(BGP\) troubleshooting: Simple approach](https://searchtelecom.techtarget.com/tip/Border-Gateway-Protocol-BGP-troubleshooting-Simple-approach) article.

**Is the traffic traversing the network?** Even if your BGP route propagation works flawlessly, the IP packets may not be able to traverse your network. Remember, we're talking about pure IP networks here; things change a bit if you add [MPLS](https://searchnetworking.techtarget.com/definition/Multiprotocol-Label-Switching-MPLS) to the mix. The most common cause of a black hole in your network is a router in the transit path that does not run BGP and consequently has no idea how to route the received IP packet toward the destination network.

IP routing works hop by hop. Even though the ingress edge router knows exactly which egress edge router to use and how to get there, it cannot pass that information to the intermediate routers. All of them must, therefore, run BGP as well.

To identify a black hole in your network, perform a traceroute from your customer's network to a destination in the internet. The last router responding to the traceroute is one hop before the black hole.

Even though all core routers in your network have to run BGP, the internal BGP sessions don't have to follow the physical structure of the network. For example, you could have a few central routers acting as BGP route reflectors for all BGP routers in your network.

