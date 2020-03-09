# IPv4 Router

## Overview

Now that you have built a simple learning Ethernet switch and feel more comfortable with the Switchyard framework, you will get to do even more cool stuff using it. In these assignment from lab 3 to lab 5, you are going to complete a series of tasks to eventually create a fully functional IPv4 router. At a high level, your router will have the following capabilities:

- Responding to/Making ARP requests
- Receiving packets and forwarding them to their destination by using a lookup table
- Responding to/Generating ICMP messages

## Details

In order to create this cool router with the aforementioned capabilities, you will implement 5 main functionalities:

1. Respond to ARP (Address Resolution Protocol) requests for addresses that are assigned to interfaces on the router.
2. Make ARP requests for IP addresses that have no known Ethernet MAC address. A router will often have to send packets to other hosts, and needs Ethernet MAC addresses to do so.
3. Receive and forward packets that arrive on links and are destined to other hosts. Part of the forwarding process is to perform address lookups ("longest prefix match" lookups) in the forwarding information base. You will eventually just use "static" routing in your router, rather than implement a dynamic routing protocol like RIP or OSPF.
4. Respond to Internet Control Message Protocol (ICMP) messages like echo requests ("pings").
5. Generate ICMP error messages when necessary, such as when an IP packet's TTL (time to live) value has been decremented to zero.

## Notes

### Address Resolution Protocol (ARP) Review

ARP is a protocol used for resolving IP addresses to MAC addresses. The main issue is that although IP addresses are used to forward IP packets across networks, a link-level address of the host or router to which you want to send the packet is required in a particular physical network. Therefore, hosts in the network need to keep a mapping between IP and link-layer addresses. Hosts can use ARP to broadcast query messages for a particular IP address in their physical networks so that the appropriate host can reply this query with its link-layer address.

### Internet Control Message Protocol (ICMP) Review

ICMP is one of the main protocols that allows routers to closely monitor the operation of the Internet. ICMP messages are used by network devices (e.g routers) for sending error messages to indicate various issues, such as unreachable destination host/network or expired TTL for a packet. ping is a very commonly used network administration utility that uses ICMP Echo Request/Reply packets to validate the reachability of a host and also collect information about the status of the network (e.g average RTT, % of packet loss, etc.).

### Testing Your Code

Just like the previous assignment, you should test the correctness of your implementation by writing your own test cases. As your friendly TA, I should warn you that in this assignment you will be implementing more functionalities and your router will be handling more events concurrently compared to the previous assignment. Therefore, you should think about reasonable ways to test the correctness of your implementation. One thing you can do is create test separate test cases that only tests certain functionalities. This will allow you to see whether the individual parts of your router is working properly. Then, you can generate larger test cases to make sure that the separate modules work together properly without breaking each other. As always, do not forget to consider corner cases.

## Helpful Materials

- [Switchyard API Documentation](https://shellqiqi.gitee.io/switchyard/reference.html)
- [Switchyard Test Scenario Creation](https://shellqiqi.gitee.io/switchyard/test_scenario_creation.html)