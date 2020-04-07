# Task 2: IP Forwarding Table Lookup

## IP Forwarding Table Build and Lookup

One of the key tasks to accomplish for this project is to perform the
fundamental thing that routers do: receive packets, match their
destination addresses against a forwarding table, and forward them out
the correct interface.

### Build Forwarding Table

You will need to implement some kind of forwarding table, with each
entry containing the following:

1.  A network prefix (e.g., `149.43.0.0`),
2.  A network "mask" (e.g., `255.255.0.0`),
3.  The "next hop" IP address, if the destination network prefix is not
    for a directly attached network, and,
4.  The network interface name through which packets destined to the
    given network should be forwarded.

You will need to build the forwarding table from two sources:

- the list of router interfaces you get through a call to the `net.interfaces()`
  (or `net.ports()`) method
- and by reading in the contents of a file
  named `forwarding_table.txt`.

An example forwarding table file is found
in the project directory, and is also recreated each time you either run
the test scripts or run your router in Mininet. Your code can
simply assume that a file named `forwarding_table.txt` exists in the
current working directory.

> [!NOTE]
> Your forwarding table *may* be different for the test scenario and for Mininet to help
> ensure that your router behaves in a *general* way and isn't written just
> to handle a specific set of forwarding table entries

Note that for each interface object in the list obtained from
`net.interfaces()` (or, equivalently, `net.ports()`), the IP address
assigned to the interface and the network mask are available (see the
Switchyard documentation on getting information about [interfaces/ports](https://shellqiqi.gitee.io/switchyard/reference.html#interface-and-interfacetype-reference)).

The file `forwarding_table.txt` can be assumed to exist in the same
directory where your router is starting up (again, this file is produced
by the Switchyard test scenario or by the Mininet startup script), and
is structured such that each line contains 4 space-separated items: the
network address, the subnet mask, the next hop address, and the
interface through which packets should be forwarded. Here are some
example lines:

```
172.16.0.0 255.255.255.0 192.168.1.2 router-eth0
192.168.200.0 255.255.255.0 192.168.200.1 router-eth1
```

In the first line, the network address is `172.16.0.0` and the subnet mask
is `255.255.0.0`. The next hop IP address is
`192.168.1.2`, and the interface through which to forward packets is named
`router-eth0`.

### Match Destination IP Addresses against Forwarding Table

After you build the forwarding table (which should be done once, upon
startup), destination addresses in IP packets received by the router
should be matched against the forwarding table. Remember that in case of
two items in the table matching, the longest prefix match should be
used.

Two special cases to consider:

1.  If there is no match in the table, just drop the packet. (We'll
    handle this better in a later stage of creating the router.)
2.  If packet is for the router itself (i.e., destination address is an
    address of one of the router's interfaces), also drop/ignore the
    packet. (We'll also handle this better at a later stage.)

## Coding

Your task is to implement the logic described above. The start file is named `lab_4/myrouter.py`.

There are a couple functions and methods in the [Python 3's `ipaddress` library](https://docs.python.org/3/library/ipaddress.html) (also available through Switchyard's IP address library) that
are helpful for building forwarding table entries and/or for matching
destination IP addresses against forwarding table entries:

- To find out the length of a subnet prefix, you can use the following
  code pattern:

  ```
  from switchyard.lib.address import *
  netaddr = IPv4Network('172.16.0.0/255.255.255.0')
  netaddr.prefixlen # -> 24
  ```

Note in the code above that you simply need to concatenate an IP address
with '/' and the netmask when constructing a `IPv4Network` object. The
resulting object can tell you the length of the prefix in bits, which
will be quite helpful.

- The `IPv4Address` class can be converted to an integer using the
  standard `int()` type conversion function. This function will return
  the 32-bit unsigned integer representation of an IP address.
  Remember that you can use bit-wise operations on Python integers
  (`&` is bitwise AND, `|` is bitwise OR, `~` is bitwise NOT, `^` is
  bitwise XOR). For example, if we wanted to check whether a given
  address matches a prefix, we might do something like this:

  ```
  prefix = IPv4Address('172.16.0.0')
  destaddr = IPv4Address('172.16.23.55')
  matches = (int(prefix) & int(destaddr)) == int(prefix)
  # matches -> True
  ```

You can also use capabilities in the `IPv4Network` class to do the same thing:

```
prefixnet = IPv4Network('172.16.0.0/16')
# same as IPv4Network('172.16.0.0/255.255.0.0')
matches = destaddr in prefixnet
# matches -> True
```

✅ In the report, show how you implement the logic of building IP forwarding table and matching the destination IP addresses.

## Testing

As the function has not been fully implemented, there is no test cases can check the output of your router.
