# Task 4: Implement some other type of network impairment

## Details

Rules that permit traffic may specify that the traffic flow should be
impaired in some way. A rule that specifies that traffic should be
impaired should simply have the keyword impair as the last item in a
rule. For example:

    # allow, but degrade the service given to packets
    # from source 10.0.0.1 destined to any host in
    # 192.168.0.0/16.  
    permit ip src 10.0.0.1 dst 192.168.0.0/16 impair

You can choose exactly how flows should be impaired. Here are some fun
options:

-   Randomly drop some fraction of the packets belonging to the flow.
-   Rewrite/overwrite the TCP advertised window to make it smaller.
-   Rewrite/overwrite the application payload contents of packets.
-   Randomly inject TCP RST packets to reset (and take down) traffic
    flows.

Lastly, note that a given permit rule may specify a rate limit, that
impairment should be applied, or that the traffic should simply be
permitted. A rule may not specify both a rate limit and impairment.


## Coding

Your task is to implement the logic described above. The start file is named `lab_7/firewall.py`.

✅ In the report, show how you implement the impairment.
