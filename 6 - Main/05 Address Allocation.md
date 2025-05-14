 2025-01-09 13:51

Status:
Tags: [[Advanced Networking]]

---
About how ethernet and ip addresses are allocated
Ethernet
--

AKA Mac Address is typically a fixed address on the device itself. 
It's 6 bytes with 3 bytes to identify manufacture, 3 to identify device.

IP Addresses
---

These are ***not*** typically built in to the device. 

Typically the IP comes from a pool of IP's from your ISP, who give you a small allocation. ==Or buy them which is incredibly expensive.==

These can be allocated ==locally==  in 4 different ways:

- Static Allocation - Stores the IP address in  some configuration file and constantly ==gets that== every time it boots, even it is wrong for the network. Often used for web servers that need to be fixed or for routes/infrastructure that need to be up soon after a power outage. ==Static Allocation might be duplicate or wrong for network, clash with other devices.==
- bootp (Bootstrap Protocol which is obsolete) - A device broadcasts it's MAC address and is assigned an address. Since it is static (they keep the address) you would need to manually update a file mapping MAC addresses to IP addresses
- DHCP/DHCPv6 (Dynamic Allocation) - 
- SLAAC  (Stateless Address Auto-Configuration) (IPv6 only) - 

DHCP
--
Dynamic Host Configuration Protocol which is the most popular option for LAN's and sort of continuation of bootp. Implements a ***lease*** system to pass the ip addresses to any new devices asking for an IP address.

A DHCP server also does passing routings for time servers, DNS, routers etc. So 2 different tasks.

==The allocation can be broken down into 4 steps:==
- ==**DHCP Discover** - Client broadcasts desire for IP address including some identifiable information like MAC Address==
- ==**DHCP Offer** - Servers reserve available IP number and broadcasts offer for it with it's least time.==
- ==**DHCP Request** - Client chooses amongst offers, and replies with chosen IP address==
- ==**DHC Pack/Acknowledge** - Server that offered it reserves it, and acknowledges.  Other servers unreserve their offer.==

==*NOTE: DHCP Request can either be done via client broadcasting with that IP address and server recognising the IP address and MAC Address, or client asking directly for a renewal on a leased IP.*== 

==Normally, renewal attempts happen after half the lease has passed.==

==DHCP Servers can either:==
- ==work like bootp, where it gives the same MAC address the previous IP address assigned to it before to configure static machines.==
- ==Manage pool of temporary addresses.==


==Smart DHCP servers can reallocate the same address from the pool (if available) and smarter one can also update DNS to record the name to this IP binding.== 

If DHCP Server goes down (maybe power outage or something), that causes a really big issue and is hard to fix, since it will struggle to manage leases assigned. New machines will be unable to boot (since it can't get an IP) and machines already running will slowly lose their IP address. If the DHCP in particular forgets it's state, it might give out duplicated IP addresses when starting up.

Setting up DHCP servers on a network can be a bit complicated, since multiple DHCP servers for each network increases the chance of failure (due to how complicated they already are) but also 1 DHCP server on a large network isn't feasible.


### ==DHCP Server Architecture==

==Main issues of DHCP is:==

- ==DHCP is had to debug==
- ==DHCP is very complex in complex networks==
- ==DHCP failure is a big problem==

==Due to DHCP having delicate states resulting in different choices of design:==

- ==Using higher-level redundancy protocols to have 1 virtual server==
- ==Complex failover protocol with 2 DHCP servers making same offer.==

==Standard solution is 1 DHCP server and a relay on each  network that unicasts requests on that network to the DHCP Server, with the relay address. Relay receives something, then relay shares response.==

==DHCP server can be industrial-strength in a secure data centre==

### ==DHCP Security==

==DHCP has various flaws or at the very least security considerations:==

- ==Need to have appropriate release periods in the case of attacker rapidly requesting leases and abandoning them, using up DHCP server address pool.==
- ==DHCP is unauthenticated? [TODO: Not sure what that means? Something to do with machine configuration]==
- ==Rouge DHCP server on a network can provide addresses of hacked DNS and router.==
- ==Users can make their own address, ignoring DHCP server. Made worse with also generating one-time MAC addresses.==
- ==Should have as few DHCP servers as possible.==

DHCPv6
---

==DHCP but for IPv6. So same issues as DHCPv4. Preferred method is static allocation for servers and SLAAC (Stateless Address Auto Configuration) for everything else.==

SLAAC
---
Ipv6 routers broadcast a RA or "router advertisement", just saying where it is ==and network configuration information needed for that network, both periodically and as reponse to soliciation messages==. New devices to this network send out a RS or (route solicitation ) asking for this, and it uses the ending of the RA as well as it's own MAC address to generate a globally random IP address (which is probably fine since it's unlikely to make a duplicate). Used for small home networks. So main advantage of SLAAC is being able to auto self-assign IP addresses which eliminates having a DHCP server generate it instead

Problems with SLAAC
----

Will not include ==DNS information like DNS Servers== without additional protocols. To get around this, the RA from the router can pass different option flags, like -M "Managed" and -O "Other". Where managed means just use DHCPv6 for me, but -O refers to using SLAAC or something for the IP allocation, but DHCPv6 for network configuration information.

Doesn't help that older networks may only have DHCPv4 servers that SLAAC had to accommodate for by getting DNS configuration from them.


Another issue being that your MAC address is used to generate the IP address, with the worry being this constant information being used by an attacker to track you across networks.

Privacy Addresses (RFC4941) proposes just generating a random IP address which is probably good enough.
Opaque Addresses (RFC7217) is better since it just proposes hashing some configuration information, e.g. the networks prefix and interface identity(Name, MAC address etc.) by just using a secret key initialised at OS installation 

==Again though, since it makes it harder to track across network, it makes debugging and logging harder, even if Opaque Addresses are the same in the local network (still different on other networks).== 

##### ==Advantages and disadvantages of SLAAC==

==Pros:==
- ==Self allocating is very convenient. Problems of DHCP not trivial.==
==Cons:==
- ==Unstable addresses make forensics, debugging and logging and much harder==



##### References


----

![[05 Address Allocation.pdf]]


