# Lab 3: Respond to ARP

## Overview

This is the first in a series of exercises that have the ultimate goal of creating an IPv4 router. The basic functions of an Internet router are to:

1. Respond to ARP (Address Resolution Protocol) requests for addresses that are assigned to interfaces on the router.
2. Make ARP requests for IP addresses that have no known Ethernet MAC address. A router will often have to send packets to other hosts, and needs Ethernet MAC addresses to do so.
3. Receive and forward packets that arrive on links and are destined to other hosts. Part of the forwarding process is to perform address lookups ("longest prefix match" lookups) in the forwarding information base. You will eventually just use "static" routing in your router, rather than implement a dynamic routing protocol like RIP or OSPF.
4. Respond to Internet Control Message Protocol (ICMP) messages like echo requests ("pings").
5. Generate ICMP error messages when necessary, such as when an IP packet's TTL (time to live) value has been decremented to zero.

The goal of this first stage of building the router is to accomplish item **#1** above: respond to ARP requests.

## Your Tasks

In the source directory for this exercise, there is a Python file to use as a starter template: `myrouter.py`. This file contains the outline of a Router class, and currently contains a constructor (`__init__`) method and a `router_main` method. This is just a starter template: you can refactor and redesign the code in any way you like.

The main task for this exercise is to modify the Router class to do the following:

> [!NOTE]
> The sentences marked with ✅ are related to the content of your report. Please pay attention.

### Task 1: Preparation

Initiate your project with our template.

[Start the task here](preparation.md)

## Handing it in

### Report

We will provide a template of your lab assignment report [here](https://box.nju.edu.cn/d/123a70ac8ff34595b18f/). You need to submit the report in your repository named `<学号><姓名>_lab_3`. The format of your report can be Microsoft Doc or PDF. An example is `123456789拾佰仟_lab_3.docx`.

### Submit to NJU GitLab

<!-- TODO: Update the folder tree for this assignment. -->

To submit your work, you need to do the following things.

1. Modify your code and complete your report.

2. When you have done your work, put your report and code in the folder `lab_3` then commit them. Tag the commit named `<学号/lab_3>` which you want to submit. An example is `123456789/lab_3`. Finally your project will look like

  ```
    switchyard/
      ├─docs/
      ├─.../
    m ├─lab_3/
    + │ ├─123456789拾佰仟_lab_3.docx
    m │ ├─myswitch.py
    m │ ├─myswitch_to.py
    m │ ├─myswitch_lru.py
    m │ ├─myswitch_traffic.py
      │ ├─...
    m │ └─start_mininet.py
      ├─.gitignore
      └─...
  ```

  > [!WARNING]
  > The file names in your submission have to **exactly** match the file names above. Otherwise, you will lose points!

3. Submit your work by pushing your local repository to your remote repository **with your tags** by running the command `git push origin --tags`.

  > [!WARNING]
  > **Only** commit your **source code** to your local repository. If there are some generated files that are not source code, ignore them by adding them in the file `.gitignore`.
