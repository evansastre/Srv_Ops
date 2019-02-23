# Ports

**AD域控制器所有使用的端口明细列表**  
  
  
端口 协议 应用程序协议 系统服务名称   
n/a GRE GRE（IP 协议 47） 路由和远程访问   
n/a ESP IPSec ESP（IP 协议 50） 路由和远程访问   
n/a AH IPSec AH（IP 协议 51） 路由和远程访问   
7 TCP Echo 简单 TCP/IP 服务   
7 UDP Echo 简单 TCP/IP 服务   
9 TCP Discard 简单 TCP/IP 服务   
9 UDP Discard 简单 TCP/IP 服务   
13 TCP Daytime 简单 TCP/IP 服务   
13 UDP Daytime 简单 TCP/IP 服务   
17 TCP Quotd 简单 TCP/IP 服务   
17 UDP Quotd 简单 TCP/IP 服务   
19 TCP Chargen 简单 TCP/IP 服务   
19 UDP Chargen 简单 TCP/IP 服务   
20 TCP FTP 默认数据 FTP 发布服务   
21 TCP FTP 控制 FTP 发布服务   
21 TCP FTP 控制 应用程序层网关服务   
23 TCP Telnet Telnet   
25 TCP SMTP 简单邮件传输协议   
25 UDP SMTP 简单邮件传输协议   
25 TCP SMTP Exchange Server   
25 UDP SMTP Exchange Server   
42 TCP WINS 复制 Windows Internet 名称服务   
42 UDP WINS 复制 Windows Internet 名称服务   
53 TCP DNS DNS Server   
53 UDP DNS DNS Server   
53 TCP DNS Windows 防火墙/Internet 连接共享   
53 UDP DNS Windows 防火墙/Internet 连接共享   
67 UDP DHCP 服务器 DHCP 服务器   
67 UDP DHCP 服务器 Windows 防火墙/Internet 连接共享   
69 UDP TFTP 普通 FTP 后台程序服务   
80 TCP HTTP Windows 媒体服务   
80 TCP HTTP 万维网发布服务   
80 TCP HTTP SharePoint Portal Server   
88 TCP Kerberos Kerberos 密钥分发中心   
88 UDP Kerberos Kerberos 密钥分发中心   
102 TCP X.400 Microsoft Exchange MTA 堆栈   
110 TCP POP3 Microsoft POP3 服务   
110 TCP POP3 Exchange Server   
119 TCP NNTP 网络新闻传输协议   
123 UDP NTP Windows 时间   
123 UDP SNTP Windows 时间   
135 TCP RPC 消息队列   
135 TCP RPC 远程过程调用   
135 TCP RPC Exchange Server   
135 TCP RPC 证书服务   
135 TCP RPC 群集服务   
135 TCP RPC 分布式文件系统   
135 TCP RPC 分布式链接跟踪   
135 TCP RPC 分布式事务处理协调器   
135 TCP RPC 事件日志   
135 TCP RPC 传真服务   
135 TCP RPC 文件复制   
135 TCP RPC 本地安全机构   
135 TCP RPC 远程存储通知   
135 TCP RPC 远程存储服务器   
135 TCP RPC Systems Management Server 2.0   
135 TCP RPC 终端服务授权   
135 TCP RPC 终端服务会话目录   
137 UDP NetBIOS 名称解析 计算机浏览器   
137 UDP NetBIOS 名称解析 服务器   
137 UDP NetBIOS 名称解析 Windows Internet 名称服务   
137 UDP NetBIOS 名称解析 Net Logon   
137 UDP NetBIOS 名称解析 Systems Management Server 2.0   
138 UDP NetBIOS 数据报服务 计算机浏览器   
138 UDP NetBIOS 数据报服务 Messenger   
138 UDP NetBIOS 数据报服务 服务器   
138 UDP NetBIOS 数据报服务 Net Logon   
138 UDP NetBIOS 数据报服务 分布式文件系统   
138 UDP NetBIOS 数据报服务 Systems Management Server 2.0   
138 UDP NetBIOS 数据报服务 许可证记录服务   
139 TCP NetBIOS 会话服务 计算机浏览器   
139 TCP NetBIOS 会话服务 传真服务   
139 TCP NetBIOS 会话服务 性能日志和警报   
139 TCP NetBIOS 会话服务 后台打印程序   
139 TCP NetBIOS 会话服务 服务器   
139 TCP NetBIOS 会话服务 Net Logon   
139 TCP NetBIOS 会话服务 远程过程调用定位器   
139 TCP NetBIOS 会话服务 分布式文件系统   
139 TCP NetBIOS 会话服务 Systems Management Server 2.0   
139 TCP NetBIOS 会话服务 许可证记录服务   
143 TCP IMAP Exchange Server   
161 UDP SNMP SNMP 服务   
162 UDP SNMP 陷阱出站 SNMP 陷阱服务   
389 TCP LDAP 服务器 本地安全机构   
389 UDP LDAP 服务器 本地安全机构   
389 TCP LDAP 服务器 分布式文件系统   
389 UDP LDAP 服务器 分布式文件系统   
443 TCP HTTPS HTTP SSL   
443 TCP HTTPS 万维网发布服务   
443 TCP HTTPS SharePoint Portal Server   
445 TCP SMB 传真服务   
445 TCP SMB 后台打印程序   
445 TCP SMB 服务器   
445 TCP SMB 远程过程调用定位器   
445 TCP SMB 分布式文件系统   
445 TCP SMB 许可证记录服务   
445 TCP SMB Net Logon   
500 UDP IPSec ISAKMP 本地安全机构   
515 TCP LPD TCP/IP 打印服务器   
548 TCP Macintosh 文件服务器 Macintosh 文件服务器   
554 TCP RTSP Windows 媒体服务   
563 TCP NNTP over SSL 网络新闻传输协议   
593 TCP HTTP 上的 RPC 远程过程调用   
593 TCP HTTP 上的 RPC Exchange Server   
636 TCP LDAP SSL 本地安全机构   
636 UDP LDAP SSL 本地安全机构   
993 TCP SSL 上的 IMAP Exchange Server   
995 TCP SSL 上的 POP3 Exchange Server   
1270 TCP MOM-Encrypted Microsoft Operations Manager 2000   
1433 TCP TCP 上的 SQL Microsoft SQL Server   
1433 TCP TCP 上的 SQL MSSQL$UDDI   
1434 UDP SQL Probe Microsoft SQL Server   
1434 UDP SQL Probe MSSQL$UDDI   
1645 UDP 旧式 RADIUS Internet 身份验证服务   
1646 UDP 旧式 RADIUS Internet 身份验证服务   
1701 UDP L2TP 路由和远程访问   
1723 TCP PPTP 路由和远程访问   
1755 TCP MMS Windows 媒体服务   
1755 UDP MMS Windows 媒体服务   
1801 TCP MSMQ 消息队列   
1801 UDP MSMQ 消息队列   
1812 UDP RADIUS 身份验证 Internet 身份验证服务   
1813 UDP RADIUS 计帐 Internet 身份验证服务   
1900 UDP SSDP SSDP 发现服务   
2101 TCP MSMQ-DCs 消息队列   
2103 TCP MSMQ-RPC 消息队列   
2105 TCP MSMQ-RPC 消息队列   
2107 TCP MSMQ-Mgmt 消息队列   
2393 TCP OLAP Services 7.0 SQL Server：下层 OLAP 客户端支持   
2394 TCP OLAP Services 7.0 SQL Server：下层 OLAP 客户端支持   
2460 UDP MS Theater Windows 媒体服务   
2535 UDP MADCAP DHCP 服务器   
2701 TCP SMS 远程控制（控件） SMS 远程控制代理   
2701 UDP SMS 远程控制（控件） SMS 远程控制代理   
2702 TCP SMS 远程控制（数据） SMS 远程控制代理   
2702 UDP SMS 远程控制（数据） SMS 远程控制代理   
2703 TCP SMS 远程聊天 SMS 远程控制代理   
2703 UPD SMS 远程聊天 SMS 远程控制代理   
2704 TCP SMS 远程文件传输 SMS 远程控制代理   
2704 UDP SMS 远程文件传输 SMS 远程控制代理   
2725 TCP SQL 分析服务 SQL 分析服务器   
2869 TCP UPNP 通用即插即用设备主机   
2869 TCP SSDP 事件通知 SSDP 发现服务   
3268 TCP 全局编录服务器 本地安全机构   
3269 TCP 全局编录服务器 本地安全机构   
3343 UDP 群集服务 群集服务   
3389 TCP 终端服务 NetMeeting 远程桌面共享   
3389 TCP 终端服务 终端服务   
3527 UDP MSMQ-Ping 消息队列   
4011 UDP BINL 远程安装   
4500 UDP NAT-T 本地安全机构   
5000 TCP SSDP 旧事件通知 SSDP 发现服务   
5004 UDP RTP Windows 媒体服务   
5005 UDP RTCP Windows 媒体服务   
42424 TCP ASP.Net 会话状态 ASP.NET 状态服务   
51515 TCP MOM-Clear Microsoft Operations Manager 2000  
本文的“系统服务端口”部分包含对每个服务的简短说明，显示该服务的逻辑名称，并指出每个服务进行正确操作所需的端口和协议。使用此部分可帮助识别特定的服务所使用的端口和协议。   
本文的“端口与协议”部分中包括一个表，其中总结了“系统服务端口”部分中的信息。这个表是按端口号排序的，而不是按服务名称排序的。使用此部分可以迅速确定哪些服务侦听特定的端口。   
本文在某些术语的使用上采用了特定的方式。为了避免混淆，请确保对本文使用这些术语的方式有所了解。下表对这些术语进行了说明：   
系统服务：Windows 服务器系统包括许多产品，如 Microsoft Windows Server 2003 系列、Microsoft Exchange 2000 Server 和 Microsoft SQL Server 2000。所有这些产品都包括许多组件，系统服务就是这些组件之一。特定计算机所需的系统服务或者由操作系统在启动期间自动启动，或者根据需要在典型操作 期间启动。例如，在运行 Windows Server 2003 企业版的计算机上，一些可用的系统服务包括服务器服务、后台打印程序服务以及万维网发布服务。每个系统服务都有一个好记的服务名称和一个服务名称。好记的 服务名称是图形管理工具（如“服务”Microsoft 管理控制台 \(MMC\) 管理单元）中出现的名称。服务名称是用于命令行工具以及许多脚本语言的名称。每个系统服务可以提供一项或多项网络服务。   
应用程序协议：在本文中，应用程序协议是指使用一个或多个 TCP/IP 协议和端口的高级网络协议。应用程序协议的实例包括超文本传输协议 \(HTTP\)、服务器消息块 \(SMB\) 和简单邮件传输协议 \(SMTP\)。   
协议：TCP/IP 协议在低于应用程序协议的级别上运行，它是网络上的设备之间进行通信的标准格式。TCP/IP 协议套件包括 TCP、用户数据报协议 \(UDP\) 以及 Internet 控制消息协议 \(ICMP\)。   
端口：这是系统服务侦听传入的网络通信的网络端口。   
本文没有指定哪些服务依赖于其他服务进行网络通信。例如，许多服务依赖 Microsoft Windows 中的远程过程调用 \(RPC\) 功能或 DCOM 功能为它们分配动态 TCP 端口。远程过程调用服务通过其他使用 RPC 或 DCOM 与客户计算机通信的系统服务来协调请求。许多其他服务依赖于网络基本输入/输出系统 \(NetBIOS\)、SMB、协议（实际上是由服务器服务提供的）。其他服务依赖于 HTTP 或安全超文本传输协议 \(HTTPS\)。这些协议是由 Internet 信息服务 \(IIS\) 提供的。有关 Windows 操作系统基础结构的完整讨论已超出本文讨论的范围。不过，在 Microsoft TechNet 和 Microsoft Developer Network \(MSDN\) 上可以获得有关此主题的详细文档。虽然许多服务可能都依赖于某个特定的 TCP 端口或 UDP 端口，但仅有一个服务或进程可以随时主动侦听此端口。   
  
将 RPC 与 TCP/IP 或 UDP/IP 一起用于传输时，入站端口常常按照需要动态分配给系统服务；使用高于端口 1024 的 TCP/IP 端口和 UDP/IP 端口。这些端口常常被非正式地称为“随机 RPC 端口”。在这些情况下，RPC 客户端依赖 RPC 终结点映射器通知它们哪个（些）动态端口分配给了服务器。对于某些基于 RPC 的服务，您可以配置一个特定的端口而不是让 RPC 动态分配端口。另外，无论对于什么服务，都可以将 RPC 动态分配的端口范围限制为一个小范围。有关此主题的更多信息，请参见本文的“参考”部分。   
  
本文包含有关本文结尾的“适用于”部分中所列出的 Microsoft 产品的系统服务角色和服务器角色的信息。虽然此信息可能同样适用于 Microsoft Windows XP 和 Microsoft Windows 2000 Professional，但本文主要集中讨论服务器类操作系统。因此，本文介绍了服务侦听的端口，而没有介绍客户端程序用来连接到远程系统的端口。   
  
返回页首   
系统服务端口   
本部分提供对每个系统服务的说明，包括与系统服务相对应的逻辑名称，还显示了每个服务所需的端口和协议。   
应用程序层网关服务   
Internet 连接共享 \(ICS\)/Windows 防火墙服务的这个子组件对允许网络协议通过防火墙并在 Internet 连接共享后面工作的插件提供支持。应用程序层网关 \(ALG\) 插件可以打开端口和更改嵌入在数据包内的数据（如端口和 IP 地址）。文件传输协议 \(FTP\) 是唯一具有 Windows Server 2003 标准版和 Windows Server 2003 企业版附带的一个插件的网络协议。ALG FTP 插件旨在通过这些组件使用的网络地址转换 \(NAT\) 引擎来支持活动的 FTP 会话。ALG FTP 插件通过重定向所有通过 NAT 的流量和发送到通向环回适配器上 3000 到 5000 范围内的专用侦听端口的端口 21 的流量来支持这些会话。ALG FTP 插件随后监视并更新 FTP 控制通道流量，以便 FTP 插件能够通过 FTP 数据通道的 NAT 转发端口映射。FTP 插件还更新 FTP 控制通道流中的端口。   
  
系统服务名称：ALG 应用程序协议 协议 端口   
FTP 控制 TCP 21   
  
ASP.NET 状态服务   
ASP.NET 状态服务支持 ASP.NET 进程外会话状态。ASP.NET 状态服务在进程外存储会话数据。此服务使用套接字与 Web 服务器上运行的 ASP.NET 通信。   
  
系统服务名称：aspnet\_state 应用程序协议 协议 端口   
ASP.NET 会话状态 TCP 42424   
  
证书服务   
证书服务是核心操作系统的一部分。使用证书服务，企业可以充当它自己的证书颁发机构 \(CA\)。通过这种方法，企业可以颁发和管理程序和协议（如安全/多用途 Internet 邮件扩展 \(S/MIME\)、安全套接字层 \(SSL\)、加密文件系统 \(EFS\)、IPSec 以及智能卡登录）的数字证书。证书服务使用高于端口 1024 的随机 TCP 端口，依赖 RPC 和 DCOM 与客户机通信。   
  
系统服务名称：CertSvc 应用程序协议 协议 端口   
RPC TCP 135   
随机分配的高 TCP 端口 TCP 随机端口号   
  
群集服务   
“群集”服务控制服务器群集操作并管理群集数据库。群集是充当单个计算机的独立计算机的集合。管理员、程序员和用户将群集看作一个系统。此软件在群集节点 之间分发数据。如果一个节点失败了，其他节点将提供原来由丢失的节点提供的服务和数据。当添加或修复了某个节点后，群集软件将一些数据迁移到此节点。   
  
系统服务名称：ClusSvc 应用程序协议 协议 端口   
群集服务 UDP 3343   
RPC TCP 135   
随机分配的高 TCP 端口 TCP 随机端口号   
  
计算机浏览器   
“计算机浏览器”系统服务维护网络上的最新计算机列表，并应程序的请求提供此列表。基于 Windows 的计算机使用“计算机浏览器”服务来查看网络域和资源。被指定为浏览器的计算机维护浏览列表，这些列表中包含网络上使用的所有共享资源。Windows 程序的早期版本（如“网上邻居”、net view 命令以及 Windows 资源管理器）都需要浏览功能。例如，当您在一台运行 Microsoft Windows 95 的计算机上打开“网上邻居”时，就会出现域和计算机的列表。为了显示此列表，计算机从被指定为浏览器的计算机上获取浏览列表的副本。   
  
系统服务名称：Browser 应用程序协议 协议 端口   
NetBIOS 数据报服务 UDP 138   
NetBIOS 名称解析 UDP 137   
NetBIOS 会话服务 TCP 139   
  
DHCP 服务器   
“DHCP 服务器”服务使用动态主机配置协议 \(DHCP\) 自动分配 IP 地址。使用此服务，可以调整 DHCP 客户机的高级网络设置。例如，可以配置诸如域名系统 \(DNS\) 服务器和 Windows Internet 名称服务 \(WINS\) 服务器之类的网络设置。可以建立一个或更多的 DHCP 服务器来维护 TCP/IP 配置信息并向客户计算机提供此信息。   
  
系统服务名称：DHCPServer 应用程序协议 协议 端口   
DHCP 服务器 UDP 67   
MADCAP UDP 2535   
  
分布式文件系统   
“分布式文件系统 \(DFS\)”服务管理分布在局域网 \(LAN\) 或广域网 \(WAN\) 上的逻辑卷，它对 Microsoft Active Directory 目录服务 SYSVOL 共享是必需的。DFS 是将不同的文件共享集成为一个逻辑命名空间的分布式服务。   
  
系统服务名称：Dfs 应用程序协议 协议 端口   
NetBIOS 数据报服务 UDP 138   
NetBIOS 会话服务 TCP 139   
LDAP 服务器 TCP 389   
LDAP 服务器 UDP 389   
SMB TCP 445   
RPC TCP 135   
随机分配的高 TCP 端口 TCP 随机端口号   
  
分布式链接跟踪服务器   
“分布式链接跟踪服务器”系统服务存储信息，使得在卷之间移动的文件可以跟踪到域中的每个卷。“分布式链接跟踪服务器”服务运行在一个域中的所有域控制器 上。此服务启用“分布式链接跟踪服务器客户机”服务以跟踪已移动到同一个域中另一个 NTFS 文件系统中某个位置的链接文档。   
  
系统服务名称：TrkSvr 应用程序协议 协议 端口   
RPC TCP 135   
随机分配的高 TCP 端口 TCP 随机端口号   
  
分布式事务处理协调器   
“分布式事务处理协调器 \(DTC\)”系统服务负责协调跨计算机系统和资源管理器分布的事务，如数据库、消息队列、文件系统和其他事务保护资源管理器。如果事务性组件是通过 COM+ 配置的，就需要 DTC 系统服务。消息队列（也称作 MSMQ）中的事务性队列和 SQL Server 跨多系统运行也需要 DTC 系统服务。   
  
系统服务名称：MSDTC 应用程序协议 协议 端口   
RPC TCP 135   
随机分配的高 TCP 端口 TCP 随机端口号   
  
DNS Server   
“DNS 服务器”服务通过应答有关 DNS 名称的查询和更新请求来启用 DNS 名称解析。查找使用 DNS 标识的设备和服务以及在 Active Directory 中查找域控制器都需要 DNS 服务器。   
  
系统服务名称：DNS 应用程序协议 协议 端口   
DNS UDP 53   
DNS TCP 53   
  
事件日志   
“事件日志”系统服务记录由程序和 Windows 操作系统生成的事件消息。事件日志报告中包含对诊断问题有用的信息。在事件查看器中查看报告。事件日志服务将程序、服务以及操作系统发送的事件写入日志文 件。这些事件中不仅包含特定于源程序、服务或组件的错误，还包含诊断信息。日志可以通过事件日志 API 或通过 MMC 的管理单元中的事件查看器以编程方式查看。   
  
系统服务名称：Eventlog 应用程序协议 协议 端口   
RPC TCP 135   
随机分配的高 TCP 端口 TCP 随机端口号   
  
Exchange Server   
Microsoft Exchange Server 包括几个系统服务。当 MAPI 客户机（如 Microsoft Outlook）连接到 Exchange Server 时，客户机先连接到 TCP 端口 135 上的 RPC 终结点映射器（RPC 定位器服务）。RPC 终结点映射器告诉客户机使用哪些端口连接到 Exchange Server 服务。这些端口是动态分配的。Microsoft Exchange Server 5.5 使用两个端口：一个用于信息存储，一个用于目录。Microsoft Exchange 2000 Server 和 Microsoft Exchange Server 2003 使用三个端口：一个用于信息存储，两个用于系统助理。通过使用 HTTP 上的 RPC，还可以使用 Microsoft Office Outlook 2003 连接到运行 Exchange Server 2003 的服务器。Exchange 服务器还支持其他协议，如 SMTP、邮局协议 3 \(POP3\) 以及 IMAP。   
  
应用程序协议 协议 端口   
IMAP TCP 143   
SSL 上的 IMAP TCP 993   
POP3 TCP 110   
SSL 上的 POP3 TCP 995   
随机分配的高 TCP 端口 TCP 随机端口号   
RPC TCP 135   
HTTP 上的 RPC TCP 593   
SMTP TCP 25   
SMTP UDP 25   
  
传真服务   
传真服务、符合 Telephony API \(TAPI\) 的系统服务，提供传真功能。使用传真服务，用户可以使用本地传真设备或共享的网络传真设备，从他们的桌面程序发送和接收传真。   
  
系统服务名称：Fax 应用程序协议 协议 端口   
NetBIOS 会话服务 TCP 139   
RPC TCP 135   
随机分配的高 TCP 端口 TCP 随机端口号   
SMB TCP 445   
  
文件复制   
文件复制服务 \(FRS\) 允许同时在许多服务器上自动复制和维护文件。FRS 是 Windows 2000 和 Windows Server 2003 中的自动文件复制服务，其功能是将 SYSVOL 共享复制到所有的域控制器。此外，还可以将 FRS 配置为在与容错 DFS 关联的备用目标之间复制文件。   
  
系统服务名称：NtFrs 应用程序协议 协议 端口   
RPC TCP 135   
随机分配的高 TCP 端口 TCP 随机端口号   
  
Macintosh 文件服务器   
使用“Macintosh 文件服务器”系统服务，Macintosh 计算机用户可以在运行 Windows Server 2003 的计算机上存储和访问文件。如果此服务被关闭或被禁止，Macintosh 客户机将无法在此计算机上访问或存储文件。   
  
系统服务名称：MacFile 应用程序协议 协议 端口   
Macintosh 文件服务器 TCP 548   
  
FTP 发布服务   
FTP 发布服务提供 FTP 连接。默认情况下，FTP 控制端口为 21。不过，通过“Internet 信息服务 \(IIS\) 管理器”管理单元可以配置此系统服务。默认数据端口（即主动模式 FTP 使用的端口）自动设置为比控制端口低一个端口。因此，如果将控制端口配置为端口 4131，则默认数据端口为端口 4130。大多数 FTP 客户机都使用被动模式 FTP。这表示客户机最初使用控制端口连接到 FTP 服务器，FTP 服务器分配一个介于 1025 和 5000 之间的高 TCP 端口，然后客户机打开另一个 FTP 服务器连接以传递数据。可以使用 IIS 元数据库配置高端口的范围。   
  
系统服务名称：MSFTPSVC 应用程序协议 协议 端口   
FTP 控制 TCP 21   
FTP 默认数据 TCP 20   
随机分配的高 TCP 端口 TCP 随机端口号   
  
HTTP SSL   
HTTP SSL 系统服务使 IIS 能够执行 SSL 功能。SSL 是一个开放式标准，用于建立加密的通信通道以帮助防止拦截重要信息（如信用卡号码）。尽管此服务旨在处理其他 Internet 服务，但它主要用于启用万维网 \(WWW\) 上的加密电子金融交易。通过“Internet 信息服务 \(IIS\) 管理器”管理单元可以配置用于此服务的端口。   
  
系统服务名称：HTTPFilter 应用程序协议 协议 端口   
HTTPS TCP 443   
  
Internet 身份验证服务   
Internet 验证服务 \(IAS\) 对正在连接到网络的用户执行集中式身份验证、授权、审核以及计帐。这些用户可以在 LAN 连接上，也可以在远程连接上。IAS 实现 Internet 工程任务组 \(IETF\) 标准远程身份验证拨入用户服务 \(RADIUS\) 协议。   
  
系统服务名称：IAS 应用程序协议 协议 端口   
旧式 RADIUS UDP 1645   
旧式 RADIUS UDP 1646   
RADIUS 计帐 UDP 1813   
RADIUS 身份验证 UDP 1812   
  
Windows 防火墙/Internet 连接共享 \(ICS\)   
此系统服务为家庭网络或小型办公室网络上的所有计算机提供 NAT、寻址以及名称解析服务。当启用 Internet 连接共享功能时，您的计算机就变成网络上的“Internet 网关”，然后其他客户计算机可以共享一个 Internet 连接，如拨号连接或宽带连接。此服务提供基本的 DHCP 服务和 DNS 服务，但它也适用于功能完备的 Windows DHCP 服务或 DNS 服务。当 ICF 和 Internet 连接共享充当网络上其他计算机的网关时，它们在内部网络接口上为专用网络提供 DHCP 服务和 DNS 服务。它们不在面向外部的接口上提供这些服务。   
  
系统服务名称：SharedAccess 应用程序协议 协议 端口   
DHCP 服务器 UDP 67   
DNS UDP 53   
DNS TCP 53   
  
Kerberos 密钥分发中心   
当您使用 Kerberos 密钥分发中心 \(KDC\) 系统服务时，用户可以使用 Kerberos 版本 5 身份验证协议登录到网络。与在 Kerberos 协议的其他实现中一样，KDC 是一个提供两个服务的进程：身份验证服务和票证授予服务。身份验证服务颁发票证授予票证，票证授予服务颁发用于连接到自己的域中的计算机的票证。   
  
系统服务名称：kdc 应用程序协议 协议 端口   
Kerberos TCP 88   
Kerberos UDP 88   
  
许可证记录   
“许可证记录”系统服务是一个工具，当初设计它是为了帮助用户管理服务器客户机访问许可证 \(CAL\) 模型中授权的 Microsoft 服务器产品的许可证。许可证记录是随 Microsoft Windows NT Server 3.51 引入的。默认情况下，在 Windows Server 2003 中“许可证记录”服务是禁用的。由于原始设计的限制和许可协议条款和条件发展的原因，“许可证记录”可能不会提供一个购买的 CAL 总数与在一个特定服务器上或在企业范围内使用的 CAL 总数相比较的精确视图。“许可证记录”报告的 CAL 可能会与“最终用户许可协议 \(EULA\)”的解释和“产品使用权 \(PUR\)”相冲突。Windows 操作系统的将来版本中将不包括许可证记录。Microsoft 仅建议 Microsoft Small Business Server 系列操作系统的用户在服务器上启用此服务。   
  
系统服务名称：LicenseService 应用程序协议 协议 端口   
NetBIOS 数据报服务 UDP 138   
NetBIOS 会话服务 TCP 139   
SMB TCP 445

