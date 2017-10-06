%title: IPv6 - Future Is There 
%author: masterzen
%date: 2017-09-29





-> IPv6 <-
===========

-------------------------------------------------
-> # What's wrong with IPv4 <-

* address scarcity (2^32 vs IoT)
^
* poorly allocated (in 2011 14% only)
^
* convoluted hacks (NAT)
^
* routing issues (even with CIDR)
^
* CIDR: losing some IP addresses (network/broadcast)
^
* no automatic client/router configuration (needs stateful DHCP)
^
* multicast hard
^
* broadcast issues

-------------------------------------------------
-> # Subnetting <-

* allows efficient hierarchical routing
* ex: ISP advertises 1 route /20 to the exterior world
* and allocates 1 /29 per customer, routes internally

-------------------------------------------------
-> # Example <-

* 87.98.213.64/27

87.98.213.64    01010111.01100010.11010101.010 00000
255.255.255.224 11111111.11111111.11111111.111 00000

87.98.213.65 -> 87.98.213.94
87.98.213.64 is lost: network
87.98.213.95 is lost: broadcast

-------------------------------------------------
-> # IPv6 <-

* standard by the IETF
* IPv6 was introduced in 1999 (discussion started
around 90s)
* not interoperable with IPv4: 2 internets!
* real hierarchical subnetting
* no broadcast -> multicast!
* autoconfiguration
* security (ipsec was mandatory)
* mobile (triangular routing)
* efficient for routers (header alignment, no fragmentation)

-------------------------------------------------
-> # And Ipv5? <-

* experimental streaming protocol, circa 1990
* RFC1190
* abandoned
* so ipv6 to prevent confusion

-------------------------------------------------
-> # More addresses! <-

* 128 bits address scheme
* means 2^128=3.4×10^38 IP addresses
* or 7.9×10^28 more than IPv4
* is it enough? 
  * currently allocated 1/8 -> exhausted by 2158
  * still 5/8 not allocated

-------------------------------------------------
-> # Longer addresses! <-

* written as blocks of 4 hex digits:
2001:abcd:3456:1234:0bad:dead:babe:cafe
* simplification rules:
** elision of 0s with ::
** trim leading zeros

   2001:abcd:0023:0000:0000:0000:0000:00ff
-> 2001:abcd:23::ff

* loopback: ::1

-------------------------------------------------
-> # Anatomy <-

64bits+            16bits-         64bits
routing prefix     subnet          interface id

-------------------------------------------------
-> # Subnetting <-

* simpler: allowed only on a 8 bits boundary
* minimum subnet /64 -> 2^64 hosts
* all addresses usable in a subnet
* residential gets a /56
* professional a /48
* ISP a /32
* some prefixes reserved

-------------------------------------------------
-> # Subnetting <-

* we got 2001:920:700e::/48 (prefix)
* 2001:920:700e:0::/64 is used to interconnect
* 2001:920:700e:1::/64 is our LAN

2001:920:700e:1:0:0:0:0 
to
2001:920:700e:1:ffff:ffff:ffff:ffff 
The entire IPv4 fits 2^32 times!

-------------------------------------------------
-> # Address types <-

* unicast
* anycast
* multicast

-------------------------------------------------
-> # Address scopes <-

* unicast:
  * link-local (out of fe80::/10)
  * global (including private fc00::/7)
* multicast, 7 scopes defined.

-------------------------------------------------
-> # Autoconfiguration <-

* called SLAAC (Stateless Address AutoConfiguration)
* interface computes a link-local (based on MAC: EUI-64)
* checks for duplicate address (Neighbor Discovery)
* if good, proceeds to listen to Router Advertisement (or to speed up sends 
a Router Solicitation)
* once prefix is known, form global IPv6 with EUI-64 interface id.
* checks for duplicate address

-------------------------------------------------
-> # Stateless? <-

* so many addresses, stateful would not work
* but no room for finding:
  * DNS servers
  * WINS servers
  * ...
* this can be done by DHCPv6 (also in SLAAC too, but not supported by most host)

-------------------------------------------------
-> # ICMPv6 <-

* in IPv4:
  * ARP (MAC resolution)
  * ICMP ("errors")
  * IGMP (multicast)
* replaced by ICMPv6 (ND, RA, etc)

-------------------------------------------------
-> # Big Brother is watching you <-

* MAC is unique
* used in SLAAC interface id
* when moving only prefix changes -> tracking
* solution: use random inteface id

-------------------------------------------------
-> # DNS <-

* new RR: AAAA to host ipv6 addresses:
% dig +noall +answer AAAA www.google.com
www.google.com.   46  IN  AAAA  2a00:1450:4006:803::2004

* new ip6.arpa (1 nibble per label)
% host 2a00:1450:4006:803::2004
4.0.0.2.0.0.0.0.0.0.0.0.0.0.0.0.3.0.8.0.6.0.0.4.0.5.4.1.0.0.a.2.ip6.arpa domain name pointer mrs04s09-in-x04.1e100.net

-------------------------------------------------
-> # Firewall <-

* NAT = false sense of security
* firewall is needed to prevent exterior network to reach inside hosts

-------------------------------------------------
-> # Fun! <-

* 1337 speak:
% dig +short AAAA www.v6.facebook.com
2a03:2880:20:cf04:face:b00c::12c
%  host -t AAAA bbc.co.uk
bbc.co.uk has IPv6 address 2001:41c1:4008::bbc:2

-------------------------------------------------
-> # Demo Time <-

