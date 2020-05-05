# Task 2: Middlebox

## Details

Even though it's called a middlebox, in practice this will be a very basic version of the router you implemented in Lab 3-5. Your middlebox will have two ports each with a single connection: one to the blaster and one for the blastee. You will do the same packet header modifications(i.e layer 2) as in  Lab 3-5. However instead of making ARP requests you will hard code the IP-MAC mappings into the middlebox code. This means, if the middlebox receives a packet from its eth0 interface(= from blaster), it will forward it out from eth1(= to blastee) and vice versa. This basic assumption also obviates the need to do forwarding table lookups. Regardless of the source IP address, just forward the packet from the other interface.

So far so good. Now comes the fun part of the middlebox! Besides a very dumb forwarding mechanism, your middlebox will also be in charge of probabilistically dropping packets to simulate all the evil things that can happen in a real network. Packet drops will only happen in one direction, from blaster to blastee (i.e do not drop ACKs). 

### Parameters

The middlebox should read a text file to get parameters. Parse this file to setup your device.

**middlebox_params.txt** will contain the following line:

    -d <drop_rate>

* *drop_rate*: Percentage of packets (non-ACK) that your middlebox is going to drop, 0 ≤ *drop_rate* ≤ 1

## Coding

Your task is to implement the logic described above. The start file is named `lab_6/middlebox.py`.

✅ In the report, show how you implement the features of middlebox.
