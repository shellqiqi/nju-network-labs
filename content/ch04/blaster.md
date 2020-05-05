# Task 4: Blaster

## Details

Blaster will send/receive variable size IP packets/ACKs to/from the blastee. As mentioned above, it will implement a fixed-size sender window (SW) at packet granularity and coarse timeouts. In order to clarify how SW will work, let's define two variables LHS and RHS(both always >= 1), where LHS and RHS (correspond to sequence numbers of 2 sent packets that have not been necessarily ACKd yet) indicate the current borders of the SW such that it always satisfies the following:

**C1:** RHS - LHS + 1 ≤ SW

SW effectively puts a limit on the maximum number of unACKd packets that can be in-flight between the blaster and blastee. Logic of changing the RHS is simple, as the blaster sends packets it will increment the RHS value without violating the previous condition. However, changing the LHS value is more tricky. LHS tells us the packet with the lowest sequence number S<sub>i</sub> such that:

**C2: Every packet** with sequence number S<sub>j</sub> < S<sub>i</sub> has been successfully ACKd.

Let's look at the following example to better understand this. Numbers in the boxes indicate the sequence number associated with each packet:

Suppose `SW=5`. Initially `LHS=1 and RHS=1`

    ---------------------
    | 1 | 2 | 3 | 4 | 5 |
    ---------------------
      ^
      |
     LHS
     RHS

Based on the explanations above, blaster will start sending packets and it will keep incrementing the RHS value. After sending the first 5 packets and not receiving any ACKs, the SW will look like this:

    ---------------------
    | 1 | 2 | 3 | 4 | 5 |
    ---------------------
      ^               ^
      |               |
     LHS             RHS


Note that we can't move the RHS any further otherwise we will violate C1. This also means that blaster can't send any new packet to the blastee until it starts receiving ACKs. Let's assume that ACKs for packets #1 and #2 arrive at the blaster. In this case LHS will point at #3 and therefore we can move the RHS to 7. 

    ---------------------
    | 3 | 4 | 5 | 6 | 7 |
    ---------------------
      ^               ^
      |               |
     LHS             RHS

Now let's assume that the middlebox dropped packets #3 and #4, which means the blastee won't be able to ACK them. After a while, ACKs for #5 and #6 arrive at the blaster. 

    -----------------------------------
    | 3 | 4 | 5(ack'd) | 6(ack'd) | 7 |
    -----------------------------------
      ^                             ^
      |                             |
     LHS                           RHS

Notice that even though the blaster received some ACKs for its outstanding packets, since C2 is not satisfied LHS can't be moved forward which also prevents RHS from moving forward (to not violate C1). As you can see unless we implement an additional mechanism, blaster will be stuck in this position forever. This is where the **coarse timeouts** come into play. Whenever LHS gets stuck at a position for longer than a certain amount of time, blaster will time out and retransmit every packet in the current window that hasn't been ACKd yet. So in the previous example if LHS doesn't change for the duration of the timeout period and only packets #5 and #6 are acknowledged in the meantime, blaster will retransmit #3, #4 and #7 upon timing out. Keep in mind that some weird things can happen in this process: 1) blaster can receive an ACK for the original tranmission of a packet after retranmsitting it or 2) blaster can receive duplicate ACKs. For this project you don't need to worry about these and just keep track of whether a packet is ACKd or not. 

### Parameters

The blaster should read a text file to get parameters. Parse this file to setup your device.

**blaster_params.txt** will contain the following line:

    -b <blastee_IP> -n <num> -l <length> -w <sender_window> -t <timeout> -r <recv_timeout>

* *blastee_IP*: IP address of the blastee. This value has to match the IP address value in the `start_mininet.py` file
* *num*: Number of packets to be sent by the blaster
* *length*: Length of the variable payload part of your packet in bytes, 0 ≤ *length* ≤ 65535
* *sender_window*: Size of the sender window in packets
* *timeout*: Coarse timeout value in milliseconds
* *recv_timeout*: `recv_packet` timeout value in **milliseconds**. Blaster will block on `recv_packet` for at most *recv_timeout*. This will be a pseudo-rate controller for the blaster

### Packet format

Here is how your data packet will look like:

    <------- Switchyard headers -----> <----- Your packet header(raw bytes) ------> <-- Payload in raw bytes --->
    -------------------------------------------------------------------------------------------------------------
    |  ETH Hdr |  IP Hdr  |  UDP Hdr  | Sequence number(32 bits) | Length(16 bits) |   Variable length payload  |
    -------------------------------------------------------------------------------------------------------------

You will need to encode the sequence number and/or length information in to your packets, which will be in raw byte format. Encoding should use **big-endian** format! Python has built-in library calls to achieve this with minimum pain.

### Printing stats

Once the blaster finishes transmission (which happens upon successfully receiving an ACK for every packet it sent to the blastee -- equals to num), it is going to print some statistics about the transmission:

* ***Total TX time (in seconds)***: Time between the first packet sent and last packet ACKd
* ***Number of reTX***: Number of retransmitted packets, this doesn't include the first transmission of a packet. Also if the same packet is retransmitted more than once, all of them will count.
* ***Number of coarse TOs***: Number of coarse timeouts
* ***Throughput (Bps)***: You will obtain this value by dividing the total # of sent bytes(from blaster to blastee) by total TX time. This will include all the retransmissions as well! When calculating the bytes, only consider the length of the variable length payload!
* ***Goodput (Bps)***: You will obtain this value by dividing the total # of sent bytes(from blaster to blastee) by total TX time. However, this will **NOT** include the bytes sent due to retransmissions! When calculating the bytes, only consider the length of the variable length payload!

## Coding

Your task is to implement the logic described above. The start file is named `lab_6/blaster.py`.

✅ In the report, show how you implement the features of blaster.
