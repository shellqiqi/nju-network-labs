# Task 3: Implement the token bucket algorithm

## Details

Rules that permit traffic may optionally have rate limits specified, in
bytes per second. Here is the same example rule from above, but with a
rate limit specified as 1000 bytes per second:

    # allow, but rate-limit packets with src 10.0.0.1
    # destined to any address in the prefix 192.168.0.0/16
    # with limit as 1250 bytes/sec (10 kbit/s)
    permit ip src 10.0.0.1 dst 192.168.0.0/16 ratelimit 1000

When implementing the token bucket algorithm, you should do the
following:

-   Tokens should be semantically equated to some number of bytes
    allowed. Thus, if there are 100 tokens in the bucket, you should
    allow 100 bytes to be forwarded.
-   Tokens should be added to the bucket every 0.5 seconds. If the rate
    limit configured is r bytes per second, exactly r/2 tokens should be
    added to the bucket every 0.5 seconds. For the example above, you
    would add 500 tokens to the bucket every 0.5 seconds.

    > [!NOTE]
    > from your experience in operating systems, you should
    > know (or at least suspect) that OS timers are a wee bit
    > fickle. Just be aware of this fact and devise your code so
    > that it doesn't assume a perfect timer, because a perfect
    > timer doesn't exist. Remember that in the `net.recv_packet()`
    > call, there's a timeout value you can give in order not to
    > block on the call. In order to ensure you update the token
    > bucket every 0.5 seconds, just manipulate the timeout value.
    > You may even wish to update the token bucket more often than
    > 0.5 seconds; that's fine as long as you only add r/2 tokens
    > every 0.5 seconds.

-   The maximum number of tokens in the bucket is 2\*r, where r is the
    configured rate limit in bytes/second.
-   The minimum number of tokens in the bucket should be 0 (zero).
-   When a packet arrives that matches a rule with a rate limit
    configured, you should (a) determine the size of the packet in
    bytes, including everything from the IP header onward (i.e., include
    everything except the Ethernet header), (b) check whether the packet
    size is less than or equal to the number of tokens. If it is,
    subtract that number of tokens and allow the packet. Otherwise, the
    packet should be dropped.

To compute the packet size in bytes, you can get the size of the entire
packet by saying `len(packet)` (assuming the variable `packet` is an
instance of a `Packet`), then subtract the size of the Ethernet header
(`len(packet.get_header(Ethernet))`). Note that the last expression
assumes that the Ethernet header actually exists in the packet, but this
should normally be the case.

Note that with this algorithm, if the rate limit is set too low, you may
never allow any packets at all (e.g., if you set the limit to 15
bytes/sec, you'd never allow any TCP traffic since the smallest TCP
packet is 40 bytes, which is greater than 2\*15). Also note that the
rate limit you achieve is not expected to be exactly the specified rate
limit.


## Coding

Your task is to implement the logic described above. The start file is named `lab_7/firewall.py`.

✅ In the report, show how you implement the token bucket algorithm.
