# ComputerNetworks-SIM08
Adding alternative backoff feature in ECN Algorithm


ECN 

Conventionally, TCP/IP networks signal congestion by dropping packets. 
What is the effect of the loss of packets?

The protocol must realise there was a packet loss and it must wait for a timeout or a duplicate acknowledgment for this to occur. It copes with the loss of a packet through retransmission. In the TCP protocol, when there is a retransmission, the transmission rate is halved and is increased later in small steps (slow start) during the transmission. So a packet loss can lead to deadlocks also for a few seconds in the transmission.

Explicit Congestion Notification is a mechanism for managing congestion without drastically affecting the throughput of the transmission. ECN is an extension to TCP and IP.  ECN allows end-to-end notification of network congestion without dropping packets. ECN is an optional feature that may be used between two ECN-enabled endpoints when the underlying network infrastructure also supports it. The network apparatuses (routers) ask for help by raising a flag that’s equivalent to telling the sender of the packets to slow down the transmission. If the sender receives these notifications, the transmission rate will be reduced. If the receiver receives these packets with the help notification it will send a request to the sender to reduce the transmission rate. If all goes well the rate of transmission is reduced and the network apparatus (router) can exit the critical state without issues regarding throughput and timeout.

ECN requires support from both the internet and transport layer as routers operate in the internet layer and transmission rate is handled by the endpoints at the transport layer. With ECN, the congestion is indicated by setting the ECN field within an IP packet to CE and is echoed back by the receiver to the transmitter by setting proper bits in the header of the transport protocol.

Working of ECN : 
    1. With IP
		Uses the two LSB of DiffServ field in the IPv4 or IPv6 header.
		The 4 code points for this field are
		00 -  Non ECN-Capable Transport, Non-ECT
		10 -  ECN Capable Transport, ECT(0)
		01 - ECN Capable Transport, ECT(1)
		11 - Congestion Encountered, CE.

If the packet encounters congestion as it traverses an AQM and the router supports ECN, then code point changes to CE in the packet. This is called marking and it is intended to inform the endpoints of the impending congestion. The receiving end point transfers this marked packet to the above layers and the message is echoed back to the transmitting end point that uses it as a signal to reduce transmission rate.

In order to convey the message if congestion to the transmitting end point, the receiving end point requires support from upper  layers.

2. With TCP
Three flags in the TCP header are provided for ECN support.
Nonce Sum - Used to protect against accidental or malicious concealment of marked packets from the TCP sender.
ECN-Echo(ECE) - indicates congestion and signals sender to decrease transmission rate.
Congestion Window Reduced(CWR) - used to acknowledge congestion indication echoing was done.

Utilisation of ECN with TCP is optional. With suitable SYN and SYN-ACK segments, a connection using ECN is established. All the IP packets are marked with ECT to indicate the transport is ECN capable. When the routers see the ECT bit set, they can indicate congestion using CE  instead of dropping of packets. Upon receiving the IP packet with CE set, the receiver echoes back the congestion indication using ECE flag in the TCP header. Upon receiving a TCP segment with ECE bit set at the transmitting node congestion window is reduced. It then acknowledges the congestion indication by sending a segment with the CWR bit set.

