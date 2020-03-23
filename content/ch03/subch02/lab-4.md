# Lab 4: Forwarding Packets

## Overview

This is the second in a set of exercises that have the ultimate goal of
creating the "brains" for an IPv4 router. The basic functions of an
Internet router are to:

1.  Respond to ARP (address resolution protocol) requests for addresses
    that are assigned to interfaces on the router. (Remember that the
    purpose of ARP is to obtain the Ethernet MAC address associated with
    an IP address so that an Ethernet frame can be sent to another host
    over the link layer.)
2.  Receive and forward packets that arrive on links and are destined to
    other hosts. Part of the forwarding process is to perform address
    lookups ("longest prefix match" lookups) in the forwarding table. We
    will just use "static" routing in our router rather than implement a
    dynamic routing protocol like RIP or OSPF.
3.  Make ARP requests for IP addresses that have no known Ethernet MAC
    address. A router will often have to send packets to other hosts,
    and needs Ethernet MAC addresses to do so.
4.  Respond to ICMP messages like echo requests ("pings").
5.  Generate ICMP error messages when necessary, such as when an IP
    packet's TTL (time to live) value has been decremented to zero.

The goal of this stage is accomplish items 2 and 3 above.

## Your Tasks

After Lab 3, you have implemented the response to ARP on the starter template: `myrouter.py`. Now, on the basis of Lab 3, we continue to improve the router to implement the function of packets forwarding.

The main task for this exercise is to modify the Router class to do the following:

> [!NOTE]
> The sentences marked with ✅ are related to the content of your report. Please pay attention.

### Task 1: Preparation

Initiate your project with our template.

[Start the task here](preparation.md)

### Task 2: IP Forwarding Table Lookup

Build a forwarding table and match the destination addresses.

[Start the task here](forwarding-table-lookup.md)

### Task 3: Forwarding the Packet and ARP

Send an ARP query to create a new Ethernet header and forward the packet.

[Start the task here](make-arp-request.md)

## Handing it in

### Report

We will provide a template of your lab assignment report [here](https://box.nju.edu.cn/d/123a70ac8ff34595b18f/). You need to submit the report in your repository named `<学号><姓名>_lab_4`. The format of your report can be Microsoft Doc or PDF. An example is `123456789拾佰仟_lab_4.docx`.

### Submit to NJU GitLab

To submit your work, you need to do the following things.

1. Modify your code and complete your report.

2. When you have done your work, put your report and code in the folder `lab_4` then commit them. Tag the commit named `<学号/lab_4>` which you want to submit. An example is `123456789/lab_4`. Finally your project will look like

   ```
   switchyard
     ├─docs/
     ├─.../
   + ├─lab_4/
   + │ ├─myrouter.py
   + │ ├─forwarding_table.txt
     │ ├─...
   + │ └─start_mininet.py
     ├─.gitignore
     └─...
   ```

  > [!WARNING]
  > The file names in your submission have to **exactly** match the file names above. Otherwise, you will lose points!

3. Submit your work by pushing your local repository to your remote repository **with your tags** by running the command `git push origin --tags`.

  > [!WARNING]
  > **Only** commit your **source code** to your local repository. If there are some generated files that are not source code, ignore them by adding them in the file `.gitignore`.
