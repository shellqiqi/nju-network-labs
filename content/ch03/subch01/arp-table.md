# Task 3: Cached ARP Table

## Construct cached ARP Table

You'll eventually need to store a mapping in the Router between destination IP addresses and Ethernet MAC addresses (you can assume there is a one-to-one mapping). The reason is simple: when you send an IP packet to another host, you'll also need the Ethernet address associated with the destination IP address. If you "remember" any source IP/Ethernet MAC pairs from ARP requests that are received at the router, it may help you to avoid having to construct and send an ARP request to obtain the same information. This capability will likely be helpful to have in place for future stages of building the router.

The cache table is similar to the table used in Ethernet learning switch. For each entry there are two or more fields in which IP and MAC Address is required. The cached ARP table may look like:

| IP       | MAC Address       |
| -------- | ----------------- |
| 10.1.2.3 | 01:02:03:04:05:06 |
| ...      | ...               |

When the router receives a packet with ARP header, add or update an entry of the cached ARP table. For example, if there is an ARP request with the Ethernet source address `01:02:03:04:05:06` and the IP source address `10.1.2.3`, the router will *update* the entry whose key is `10.1.2.3` with the value `01:02:03:04:05:06`. You can also see here that the IP address is **unique** in the table.

Generally, the ARP table has a timeout mechanism. It indicates the time for which the MAC address in the ARP cache can reside. In this task, implementing this mechanism is optional.

## Coding

Modify `lab_3/myrouter.py` and add the cache table.

It is more convenient if you are familiar with Object-Oriented Programming (OOP). You can construct a class to maintain the ARP cache table. A brief tutorial of OOP in Python is [here](https://www.liaoxuefeng.com/wiki/1016959663602400/1017495723838528). Though OOP is no need in our lab assignments.

Another useful data structure in Python is `dict`. The data structure `dict` is a table. Each entry of the table contains one unique key and one value. The introduction of `dict` is [here](https://www.liaoxuefeng.com/wiki/1016959663602400/1017104324028448).

✅ In your report, show how you construct the ARP table.

## Testing

There are no test cases that can check the output of your router. So we decide you to print the cached ARP table when you update the table. You can log into the terminal or file.

✅ In your report, show the cached ARP table with screenshots. Explain how entries have changed.
