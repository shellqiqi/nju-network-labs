# FAQ

1. **Q:** When sending ICMP echo replies or error messages, does the router
need to do a forwarding table lookup and send ARP requests if needed?
Can't the router just send the ICMP messages back on the interface
through which the IP packet was received?

   **A:** The router will still need to do an ARP query as it normally does
   for forwarding an IP packet. It doesn't matter that an echo request
   arrives on, say port eth0. The echo reply may end up going out on a
   different port depending on the forwarding table lookup. The entire
   lookup and ARP query process should be the same as forwarding an IP
   packet, and will always behave exactly this way.

2. **Q:** How many error messages should be generated if a packet has TTL
expired and network unreachable errors at the same time?

   **A:** Your router will only generate a network unreachable error in this
   case. Since the router decrements the TTL field after doing a lookup,
   if the lookup fails then your router will not reach at decrementing
   the TTL value.

3. **Q:** If there are multiple packets buffered for the same destination
host or next hop and the router doesn't receive an ARP reply after sending 5
retransmissions of ARP requests what should the router do?

   **A:** Your router should send an ICMP destination host unreachable
   message back to the host referred to by the source address in the IP
   packet. When there are multiple packets buffered for the same
   destination address, the router will send an ICMP error message to
   each source host of these packets (even if the same source host sent
   multiple packets).
