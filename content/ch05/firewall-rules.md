# Task 2: Implement firewall rules 

## Details

We will use a fairly basic syntax, with no "stateful" rules. All rules
will be loaded from a text file named `firewall_rules.txt`. The syntax
and semantics of the firewall rules are described in detail below. As a
preview and example, however, here is a rule that denies IP traffic
(with any transport protocol) with source address 10.0.0.1 and any
destination address:

    # block any packets with source address 10.0.0.1
    deny ip src 10.0.0.1 dst any

(Note that the lines beginning with \# are just comments.)

The rules should be applied to packets just after they have been
received at the firewall. The firewall should apply just to IPv4 packets
(not to ARP, IPv6, or any other type of packet). In particular, non-IPv4
packets should *all be permitted*. As described in detail below, rules
can either permit or deny packets. For packets that are permitted, they
should simply be forwarded out the "other" interface by the firewall.
For any denied packets, they should be dropped/ignored and no further
processing should be done on them.

Again, the syntax and meaning of the firewall rules is described below
in detail.

## Firewall rule specification and syntax

The firewall rules to be loaded by the router must be included in a text
file named `firewall_rules.txt`. The allowable syntax for rules is as
follows:

    [permit|deny] ip src [srcnet|any] dst [dstnet|any]
    [permit|deny| icmp src [srcnet|any] dst [dstnet|any]
    [permit|deny] [udp|tcp] src [srcnet|any] srcport [portno|any] dst [dstnet|any] dstport [portno|any]

Note that items in square braces indicate items to be made concrete in a
specific rule. For example, a valid rule is:

    permit ip src 10.0.0.1 dst any

which would allow any IP packets (any protocol) with source address
10.0.0.1 and any destination address.

Note that the `srcnet` or `dstnet` values may either be an exact IP
address, or an IP prefix indicating a subnet of addresses. Also,
`portno` should be specified as a single integer between 0 and 65535.
`any`, somewhat obviously, should match anything.

Here is another example:

    deny tcp src 1.2.3.0/24 srcport any dst any dstport 80

This rule blocks any TCP traffic with source address in the range
1.2.3.0-255, with any source TCP port, any destination IP address, and a
destination port of 80.

It is straightforward to access TCP and UDP port numbers using the
Switchyard packet library. See the [Switchyard documentation](https://shellqiqi.gitee.io/switchyard/reference.html#udp-user-datagram-protocol-header) for details
and examples.

You may also find the `IPv4Network` class useful (it is built in to the
ipaddress module in Python 3.4). You can instantiate an `IPv4Network`
object by passing in a network address (with prefix) as a string. On
that object, you can get the prefix length as an integer, convert the
address to an integer (to be able to bitwise operations), and other
useful operations. See the standard Python documentation for full
details on the `ipaddress` module.

    >>> from ipaddress import IPv4Network, IPv4Address
    >>> net1 = IPv4Network('149.43.80.0/22')
    >>> net2 = IPv4Network('149.43.0.0/16')
    >>> net3 = IPv4Network('149.43.80.25', strict=False)
    >>>   # for above, if you don't have a prefix at the end of an address
    >>>   # you'll get an exception unless you say strict=False
    >>>   # w/o a prefix length, it assumes 32 bit prefix
    >>> net1.prefixlen
    22
    >>> net2.prefixlen
    16
    >>> net3.prefixlen
    32
    >>> net1.network_address
    IPv4Address('149.43.80.0')
    >>> int(net1.network_address)
    2502643712
    >>> net2.network_address
    IPv4Address('149.43.0.0')
    >>> int(net2.network_address)
    2502623232
    >>> int(net2.network_address) & int(net3.network_address) == int(net2.network_address)
    True
    >>> # of course, the above should be true because we're basically checking
    >>> # whether 149.43.80.25 is contained within the network 149.43.0.0
    >>> # by doing the bitwise & (AND) operation
    >>> 

Blank lines are allowed in the `firewall_rules.txt` file, and any line
on which the first non-whitespace character is \# should be ignored.
Thus, you should allow Python-like comments, but you do not need to
handle the situation where a comment and a rule appear on the same line
--- comments will always appear separately.

Rule order matters! Packets should be checked against the rules in the
same order as the rules are listed in firewall\_rules.txt. When a
matching rule is found, the action (permit/deny) according to the rule
should apply, and no more rules should be checked. If no rules match,
then the default action should be to permit the packet. Note that in the
example rule set below, the last rule explicitly drops all packets but
your firewall should handle any reasonable rule set.

Rate limits (details can be found in [Task 3](token-bucket.md)) can be applied to any "permit" rule. To specify a rate
limit, the syntax is "ratelimit [bytessec]", included at the end of a
rule. The rate limit accounting should apply to the entire packet except
the Ethernet header (i.e., the packet size used for rate limit
accounting should just include the IP header and beyond).

Impairment (details can be found in [Task 4](impairment.md)) can be applied to any "permit" rule (although rate limits and
impairment cannot be applied to the same rule). The only additional
syntax is the inclusion of the keyword impair at the end of the rule.

The project folder includes a `firewall_rules.txt` file. I'd recommend
reading through this file to get familiar with the types of rules
included in order to get a sense for how your firewall should behave.


## Coding

Your task is to implement the logic described above. The start file is named `lab_7/firewall.py`.

✅ In the report, show how you implement the firewall rules.
