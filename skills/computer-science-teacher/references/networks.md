# Playbook: computer networks

**Covers:** network models (TCP/IP and OSI), the physical and link layers (Ethernet, Wi-Fi, MAC addresses, ARP, switching), the network layer (IPv4, IPv6, addressing, subnetting, CIDR, NAT, ICMP, routing algorithms and protocols such as OSPF, RIP and BGP), the transport layer (UDP, TCP, reliability, flow control, congestion control, QUIC), the application layer (DNS, HTTP/1.1, HTTP/2, HTTP/3, TLS, email, DHCP), sockets, performance, and network security basics.

## What a complete answer contains

- **The layer view:** which layer the topic lives in, what it receives from the layer below, and what it provides to the layer above. Show encapsulation: each layer's header wrapped around the payload.
- **Exact header formats** as bit-field diagrams with real field widths. For example, the IPv4 header is 20 bytes without options, the TCP header is 20 bytes minimum, and the UDP header is 8 bytes. Explain what each field is for, and which design problem it solves.
- **A packet-level walk-through of a real event.** The classic one is "what happens when you type a URL and press Enter":
  1. DNS resolution (the recursive resolver and the root, TLD and authoritative servers, plus caching);
  2. ARP for the gateway's MAC address;
  3. the TCP three-way handshake, with actual sequence and acknowledgment numbers;
  4. the TLS 1.3 handshake;
  5. the HTTP request and response;
  6. routing hop by hop, and NAT rewriting addresses.
- **Sequence diagrams** with time flowing downward, showing RTTs, timeouts and retransmissions.
- **State machines:** the TCP connection states, including TIME_WAIT and why it exists.
- **Calculations worked step by step:**
  - transmission delay (L/R) versus propagation delay (d/s), plus queueing and processing delay;
  - throughput and the bandwidth-delay product, and window sizes;
  - utilization of stop-and-wait versus pipelined protocols;
  - subnetting in binary (network and broadcast addresses, usable hosts, CIDR aggregation);
  - the Internet checksum.
- **Algorithms in full:**
  - link-state routing (Dijkstra, as in OSPF);
  - distance-vector routing (Bellman-Ford, as in RIP) and count-to-infinity;
  - BGP path-vector routing and policy;
  - Go-Back-N versus Selective Repeat;
  - TCP congestion control: slow start, congestion avoidance (AIMD), fast retransmit and fast recovery, a cwnd-over-time graph, and modern variants (CUBIC, which is Linux's default, and BBR).
- **Standards cited by RFC number when you are sure of it.** Reliable anchors:

  | Protocol | RFC |
  |---|---|
  | IPv4 | 791 |
  | ICMP | 792 |
  | UDP | 768 |
  | TCP | 793 (1981), now consolidated as 9293 (2022) |
  | ARP | 826 |
  | DNS | 1034 and 1035 |
  | DHCP | 2131 |
  | IPv6 | 8200 (it replaced 2460) |
  | HTTP semantics | 9110 (HTTP/1.1 was first 2068, then 2616) |
  | HTTP/2 | 7540, now 9113 |
  | HTTP/3 | 9114 |
  | QUIC | 9000 |
  | TLS 1.3 | 8446 |
  | BGP-4 | 4271 |
  | OSPFv2 | 2328 |

- **Code:** socket programming in Python or C (a TCP echo server and client), so the student sees what the OS provides (`socket`, `bind`, `listen`, `accept`, `connect`, `send`, `recv`).

## Comparison dimensions

Connection-oriented versus connectionless, reliability and ordering guarantees, head-of-line blocking, overhead (header size, handshake RTTs), flow control versus congestion control, link-state versus distance-vector routing, circuit switching versus packet switching.

## Origins: key milestones

| When | Who | What |
|---|---|---|
| early 1960s | Paul Baran (RAND); Donald Davies (NPL, who coined "packet" around 1965) | Packet switching, developed independently. Leonard Kleinrock developed the queueing theory behind it |
| 1969 | Steve Crocker | RFC 1, starting the RFC series |
| October 29, 1969 | UCLA to SRI | The first ARPANET message ("LO", after the system crashed on "LOGIN") |
| 1973 | Bob Metcalfe (Xerox PARC) | Ethernet |
| 1974 | Vint Cerf and Bob Kahn | "A Protocol for Packet Network Intercommunication", which led to TCP/IP (Turing Award 2004) |
| January 1, 1983 | ARPANET | Flag day: the switch to TCP/IP |
| 1983 | Paul Mockapetris | DNS, replacing the single HOSTS.TXT file |
| 1984 | ISO | The OSI reference model |
| 1986 onward | The internet | Congestion collapses lead Van Jacobson to propose TCP congestion control (1988) |
| 1989 | IETF | BGP (RFC 1105), famously sketched on napkins |
| 1989–91 | Tim Berners-Lee (CERN) | The World Wide Web: HTTP, HTML, URLs (Turing Award 2016) |
| 1994–95 | IETF; Netscape | NAT to stretch IPv4 addresses (RFC 1631); SSL |
| 1997 | IEEE | 802.11, the original Wi-Fi standard |
| 1998 | IETF | IPv6 (RFC 2460) |
| 1999 | IETF | TLS 1.0 (RFC 2246) |
| around 2012 | Google | QUIC, standardized in 2021 as RFC 9000 and used by HTTP/3 |

## Canonical sources

- Kurose and Ross, *Computer Networking: A Top-Down Approach*
- Tanenbaum and Wetherall, *Computer Networks*
- Peterson and Davie, *Computer Networks: A Systems Approach* (free online)
- W. Richard Stevens, *TCP/IP Illustrated, Volume 1*
- The RFCs themselves, at rfc-editor.org

## Classic misconceptions

- "The internet runs on the OSI model." The internet runs on the TCP/IP stack. OSI is a teaching and reference model.
- "TCP guarantees delivery." TCP delivers bytes reliably and in order *or* reports that the connection failed. It can't guarantee delivery over a broken network.
- "UDP is unreliable, so it is useless." DNS, video calls, games and QUIC all use UDP, because they want control over reliability and latency.
- "Bandwidth is speed." Bandwidth is capacity. Latency usually dominates for small transfers.
- "HTTPS hides which site you visit." The server's IP address is visible, and so is the domain name through SNI, unless Encrypted Client Hello (ECH) is used.
- "MAC addresses are used end to end." They are rewritten at every IP hop; only IP addresses (before NAT) go end to end.
- "An IP address identifies one device." NAT, DHCP, anycast and load balancers break that assumption.
- "Flow control and congestion control are the same." Flow control protects the receiver; congestion control protects the network.

## Question patterns

- Compute the total delay to send this file over these links.
- Subnet this block for these department sizes.
- Draw the sequence diagram for this TCP exchange with loss. What are cwnd and ssthresh after each RTT?
- Run Dijkstra or distance vector on this topology, and show each router's table.
- Fill in the fields of this captured packet.
- Explain each step of loading a web page.
- Why does HTTP/2 still suffer head-of-line blocking over TCP, and how does HTTP/3 fix it?

## Tools and artifacts to show

Wireshark captures (showing the actual handshake bytes), `tcpdump`, `ping`, `traceroute` or `tracert`, `dig` and `nslookup`, `curl -v`, `openssl s_client`, `ss` and `netstat`, `ip addr` and `ip route`, and Python socket programs.
