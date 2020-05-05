# Task 3: Blastee

## Details

Blastee will receive data packets from the blaster and immediately ACK them. Blastee will extract the sequence number information from the received data packet and create an ACK packet with the same sequence number. Unlike TCP where sequence numbers work on bytes, your implementation will use sequence numbers at packet granularity.

### Parameters

The blastee should read a text file to get parameters. Parse this file to setup your device.

**blastee_params.txt** will contain the following line:

    -b <blaster_IP> -n <num> 

* *blaster_IP*: IP address of the blaster. This value has to match the IP address value in the `start_mininet.py` file
* *num*: Number of packets to be sent by the blaster

### Packet format

The packets will have 3 headers: Ethernet, IPv4, UDP. It's obvious why you will have the first 2 headers. UDP header will serve as a placeholder to prevent Switchyard from complaining. You can read about the parameters of UDP header [here](https://shellqiqi.gitee.io/switchyard/reference.html#udp-user-datagram-protocol-header). You can assign arbitrary values for the port values as you won't be using them. You will append your packet to this sequence of packets. I suggest you use the `RawPacketContents` header in Switchyard. It is just a packet header class that wraps a set of raw bytes. You can find some information about it on the same web site. You can also take a look at the source code to understand how it works. (You can find its source code at the bottom of [this page](https://shellqiqi.gitee.io/switchyard/_modules/switchyard/lib/packet/packet.html).) Or better, you can just test it on your own!

Here is how your ACK packet will look like:

    <------- Switchyard headers -----> <----- Your packet header(raw bytes) ------> <-- Payload in raw bytes --->
    -------------------------------------------------------------------------------------------------------------
    |  ETH Hdr |  IP Hdr  |  UDP Hdr  |          Sequence number(32 bits)          |      Payload  (8 bytes)    |
    -------------------------------------------------------------------------------------------------------------

Notice that the ACK packet will have a fixed size payload (8 bytes). You will populate these bytes from the first 8 bytes of the variable length payload of the blaster's packet that you received at the blastee. If the blaster's packet has a payload with less than 8 bytes, just pad the payload in ACK as you need.

You will need to encode the sequence number in to your packets, which will be in raw byte format. Encoding should use **big-endian** format! Python has built-in library calls to achieve this with minimum pain.

## Coding

Your task is to implement the logic described above. The start file is named `lab_6/blastee.py`.

✅ In the report, show how you implement the features of blastee.
