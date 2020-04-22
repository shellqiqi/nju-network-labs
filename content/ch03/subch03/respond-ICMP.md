# Task 2: Responding to ICMP echo requests

## Procedure

The first key task for this is for the router to respond to ICMP echo
request ("pings") sent to an address assigned to one of its interfaces.

Prior to making a forwarding decision for an incoming IP packet (i.e., a
forwarding table lookup), you should first check whether the IP
destination address is the same as one of the addresses assigned to one
of the router's interfaces. If the packet is also an ICMP echo request,
then you should construct an ICMP echo reply and send it back to the
original host that sent the ping. To do that, you should:

-   Construct an ICMP header + echo reply, correctly populating the
    fields in the header. See the Switchyard documentation for details
    on [ICMP packet headers](https://shellqiqi.gitee.io/switchyard/reference.html#icmp-internet-control-message-protocol-header-v4). When creating the EchoReply, do the
    following:
    -   Copy the EchoRequest sequence number into the EchoReply you
        make, and
    -   also copy the identifier in the EchoRequest into the EchoReply,
        and
    -   set the data field in the EchoReply to be the same as the data
        in the EchoRequest.
-   Construct an IP header, which should have the destination IP address
    set as the source address of the incoming ICMP echo request, and the
    IP source address set as the router's interface address. The next
    header in the packet should be the ICMP header that you created.
-   Send (forward) the packet you constructed. You should already have
    code from the previous stage of the router to do forwarding table
    lookups and ARP requests to handle this part. If you've designed
    this part of your router reasonably well, this should just be a
    method/function call for forwarding the echo response.


## Coding

Your task is to implement the logic described above. The start file is named `lab_5/myrouter.py`.

✅ In the report, show how you implement the logic of responding to ICMP echo requests.

## Testing

Wait until Task 3 is completed before testing.
