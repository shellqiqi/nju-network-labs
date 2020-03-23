# FAQ

1. **Q:** What should the router do in the following scenario? Packet for a certain IP address arrives at the router and it sends an ARP request to find the MAC address. Before receiving the ARP reply, the router receives another packet (non-ARP) for the same IP address, does it send an ARP request again?

   **A:** No, in this case you do not retransmit the ARP request for the second packet. More generally, your router might receive many packets for a certain IP address while there is an outstanding ARP request for that IP address. In this case, your router should not send out any new ARP requests or update the timestamp of the initial ARP request. However, your router should buffer the new data packets so that it can transmit them to the destination host once it receives the ARP reply. IMPORTANT: If your router buffers multiple packets for a destination host that has an outstanding ARP request, upon receiving the corresponding ARP reply these packets has to be forwarded to the destination host in the order they arrived to the router!

2. **Q:** When an ARP request arrives at the router for a destination IP address that is not assigned to one of the router's interfaces, does the router need to flood the ARP request? Or just drop it?

   **A:** Your router should drop the packet in this case. Note: In stage 1, you should be checking to see if the destination IP address is an IP address assigned to one of the router's interfaces. However, for stage two and three, check to see if the destination IP address is an IP address in the ARP table

3. **Q:** When the router needs to make an ARP request for the next hop IP address (which is obtained after the longest prefix match lookup), should it flood the request on all ports?

   **A:** The router does not flood the ARP request on all ports. The ARP query is merely broadcast on the port obtained from doing a longest prefix match lookup. The response ARP query *should* come back on the same port but it doesn't actually need to (and it doesn't matter for the purposes of forwarding the packet or sending out the ARP request).

4. **Q:** When sending ICMP echo replies or error messages, does the router need to do table lookup & send ARP requests if needed? Can the router send the ICMP messages back on the interface through which the IP packet was received?

   **A:** The router will still need to do an ARP query as it normally does for forwarding an IP packet. It doesn't matter that an echo request arrives on, say port 0. The echo reply may end up going out on a different port depending on the forwarding table lookup. The entire lookup and ARP query process should be the same as forwarding an IP packet, and will always behave exactly this way.

5. **Q:** How many error messages will be generated if a packet has TTL expired and network unreachable errors at the same time?

   **A:** Your router will only generate a network unreachable error in this case. Since the router decrements the TTL field after doing a lookup, if the lookup fails then your router will not reach at decrementing the TTL value.

6. **Q:** Following up from Q1: if there are multiple packets buffered for the same destination host or next hop and the router doesn't receive an ARP reply after sending 5 retransmissions of ARP requests what should the router do?

   **A:** As it is explained in the part 3 of the project, your router will send an ICMP destination host unreachable message back to the host referred to by the source address in the IP packet. When there are multiple packets buffered for the same destination address, the router will send an ICMP error message to each source host of these packets (even if the same source host sent multiple packets).

7. **Q:** Part of the instructions say if the packet is for us (i.e. it's destination ipaddr is in net.interfaces) then drop it. But later on, the instructions say that if the packet is meant for one of our directly connected neighbors then we forward it. How is net.interfaces() different than the directly connected networks.

   **A:** The net.interfaces() is the information for the interfaces on the router itself. For example, eth1 might have an ipaddr of 192.168.1.1. However, from these interfaces you can use the ipaddr and netmask to get the subnet that the interface is directly connected to. So if the netmask of 255.255.255.0 for the same eth1, then the subnet would be the mask applied to the ipaddr which is 192.168.1.0. So, if a packet came to the router destined for an ip address like 192.168.1.100, then you would find a match in the forwarding table and end up forwarding the packet out eth1. But if a packet came to the router destined for 192.168.1.1, then you would drop it, since that is the exact ip address of the interface.

8. **Q:** In the instruction of our project, we are told that the echo reply may end up going out on a different port depending on the forwarding table lookup. What does this mean?

   **A:** The source ip address of the ICMP response does not necessarily need to be the ip address of the interface that you are sending the reply packet out of. The ICMP reply should have an ip.src and ip.dst that are the the ip.dst and ip.src of the ICMP request respectively (that is just switch them around). However, the destination address is looked up in the forwarding table to determine what port to send the reply out of. So the src ip address and the port of the ICMP reply may not match up to the same interface.
