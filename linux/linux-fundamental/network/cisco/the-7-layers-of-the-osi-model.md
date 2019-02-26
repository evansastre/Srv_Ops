# The 7 Layers of the OSI Model



* [Layer 7 - Application](https://www.webopedia.com/quick_ref/OSI_Layers.asp#OSI-7)
* [Layer 6 - Presentation](https://www.webopedia.com/quick_ref/OSI_Layers.asp#OSI-6)
* [Layer 5 - Session](https://www.webopedia.com/quick_ref/OSI_Layers.asp#OSI-5)
* [Layer 4 - Transport](https://www.webopedia.com/quick_ref/OSI_Layers.asp#OSI-4)   
* [Layer 3 - Network](https://www.webopedia.com/quick_ref/OSI_Layers.asp#OSI-3)     Tcp/IP
* [Layer 2 - Data Link](https://www.webopedia.com/quick_ref/OSI_Layers.asp#OSI-2)    Switch link
* [Layer 1 - Physical](https://www.webopedia.com/quick_ref/OSI_Layers.asp#OSI-1)

![7 Layers of the OSI Diagram](https://www.webopedia.com/imagesvr_ce/8023/7-layers-of-osi-icon.jpg)

_**Did You Know...?** Most of the functionality in the OSI model exists in all communications systems, although two or three OSI layers may be incorporated into one. OSI is also referred to as the OSI Reference Model or just the OSI Model._

### Application \(Layer 7\)

OSI Model, Layer 7, supports [application](https://www.webopedia.com/TERM/A/application.html) and end-user processes. Communication partners are identified, quality of service is identified, user authentication and privacy are considered, and any constraints on data [syntax](https://www.webopedia.com/TERM/S/syntax.html) are identified. Everything at this layer is application-specific. This layer provides application services for file transfers, [e-mail](https://www.webopedia.com/TERM/E/e_mail.html), and other [network](https://www.webopedia.com/TERM/N/network.html) [software](https://www.webopedia.com/TERM/S/software.html) services. [Telnet](https://www.webopedia.com/TERM/T/Telnet.html) and [FTP](https://www.webopedia.com/TERM/F/ftp.html) are applications that exist entirely in the application level. Tiered application architectures are part of this layer.

 _Layer 7 Application examples include WWW browsers, NFS, SNMP, Telnet, HTTP, FTP_   


### Presentation \(Layer 6\)

This layer provides independence from differences in data representation \(e.g., [encryption](https://www.webopedia.com/TERM/E/encryption.html)\) by translating from application to network format, and vice versa. The presentation layer works to transform data into the form that the application layer can accept. This layer formats and encrypts data to be sent across a [network](https://www.webopedia.com/TERM/N/network.html), providing freedom from compatibility problems. It is sometimes called the syntax layer.

 _Layer 6 Presentation examples include encryption, ASCII, EBCDIC, TIFF, GIF, PICT, JPEG, MPEG, MIDI._

### Session \(Layer 5\)

This layer establishes, manages and terminates connections between [applications](https://www.webopedia.com/TERM/A/application.html). The session layer sets up, coordinates, and terminates conversations, exchanges, and dialogues between the applications at each end. It deals with session and connection coordination.

 _Layer 5 Session examples include NFS, NetBios names, RPC, SQL._

### Transport \(Layer 4\)

OSI Model, Layer 4, provides transparent transfer of data between end systems, or [hosts](https://www.webopedia.com/TERM/H/host.html), and is responsible for end-to-end error recovery and [flow control](https://www.webopedia.com/TERM/F/flow_control.html). It ensures complete data transfer.

 _Layer 4 Transport examples include SPX, TCP, UDP._

### Network \(Layer 3\)

Layer 3 provides [switching](https://www.webopedia.com/TERM/P/packet_switching.html) and [routing](https://www.webopedia.com/TERM/R/routing.html) technologies, creating logical paths, known as [virtual circuits](https://www.webopedia.com/TERM/V/virtual_circuit.html), for transmitting data from [node](https://www.webopedia.com/TERM/N/node.html) to node. Routing and forwarding are functions of this layer, as well as [addressing](https://www.webopedia.com/DidYouKnow/Internet/IPaddressing.asp), [internetworking](https://www.webopedia.com/TERM/I/internetworking.html), error handling, [congestion](https://www.webopedia.com/TERM/C/congestion.html) control and packet sequencing.

 _Layer 3 Network examples include AppleTalk DDP, IP, IPX._

### Data Link \(Layer 2\)

At OSI Model, Layer 2, data packets are [encoded](https://www.webopedia.com/TERM/E/encoding.html) and decoded into bits. It furnishes [transmission protocol](https://www.webopedia.com/TERM/T/TCP_IP.html)knowledge and management and handles errors in the physical layer, flow control and frame synchronization. The data link layer is divided into two sub layers: The Media Access Control \([MAC](https://www.webopedia.com/TERM/M/MAC_address.html)\) layer and the [Logical Link Control](https://www.webopedia.com/TERM/L/Logical_Link_Control_layer.html)\(LLC\) layer. The MAC sub layer controls how a computer on the network gains access to the data and permission to transmit it. The LLC layer controls frame [synchronization](https://www.webopedia.com/TERM/D/data_synchronization.html), flow control and error checking.

 _Layer 2 Data Link examples include PPP, FDDI, ATM, IEEE 802.5/ 802.2, IEEE 802.3/802.2, HDLC, Frame Relay._   


### Physical \(Layer 1\)

OSI Model, Layer 1 conveys the bit stream - electrical impulse, light or radio signal — through the [network](https://www.webopedia.com/TERM/N/network.html) at the electrical and mechanical level. It provides the [hardware](https://www.webopedia.com/TERM/H/hardware.html) means of sending and receiving data on a carrier, including defining cables, cards and physical aspects. [Fast Ethernet](https://www.webopedia.com/TERM/F/Fast_Ethernet.html), [RS232](https://www.webopedia.com/TERM/R/RS_232C.html), and [ATM](https://www.webopedia.com/TERM/A/ATM.html) are [protocols](https://www.webopedia.com/TERM/P/protocol.html) with physical layer components

