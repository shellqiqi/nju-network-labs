# FAQ

1. **Q:** What should the router do in the following scenario: say a packet for
a certain IP address arrives at the router and it sends an ARP request
to obtain the corresponding MAC address. Before receiving the ARP reply,
the router receives another packet (non-ARP) for the same IP address,
should it send an ARP request again?

   **A:** No, in this case you should not retransmit the ARP request for the
   second packet. More generally, your router might receive many packets
   for a certain IP address while there is an outstanding ARP request for
   that IP address. In this case, your router should not send out any new
   ARP requests or update the timestamp of the initial ARP request.
   However, your router should buffer the new data packets so that it can
   transmit them to the destination host once it receives the ARP reply.
   IMPORTANT: If your router buffers multiple packets for a destination
   host that has an outstanding ARP request, upon receiving the
   corresponding ARP reply these packets has to be forwarded to the
   destination host in the order they arrived to the router!

2. **Q:** When an ARP request arrives at the router for a destination IP
address that is not assigned to one of the router's interfaces, does the
router need to flood the ARP request, or should it just drop the
request?

   **A:** Your router should drop the packet in this case.

3. **Q:** When the router needs to make an ARP request for the next hop IP
address (which is obtained after the longest prefix match lookup),
should it flood the request on all ports?

   **A:** The router does *not* flood the ARP request on all ports. The ARP
   query is merely sent to the broadcast Ethernet address on the port
   obtained from doing a longest prefix match lookup. The response ARP
   query *should* come back on the same port but it doesn't actually need
   to (and it doesn't matter for the purposes of forwarding the packet or
   sending out the ARP request).
