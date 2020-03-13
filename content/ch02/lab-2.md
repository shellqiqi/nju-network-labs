# Lab 2: Learning Switch

## Overview

In this assignment, you are going to implement the core functionalities of an Ethernet learning switch using the [Switchyard framework](https://gitee.com/shellqiqi/switchyard). An Ethernet switch is a layer 2 device that uses packet switching to receive, process and forward frames to other devices (end hosts, other switches) in the network. A switch has a set of interfaces (ports) through which it sends/receives Ethernet frames. When Ethernet frames arrive on any port, the switch process the header of the frame to obtain information about the destination host. If the switch knows that the host is reachable through one of its ports, it sends out the frame from the appropriate output port. If it does not know where the host is, it floods the frame out of all ports except the input port.

## Details

Your task is to implement the logic of a switch. As it is described in the last paragraph of the "Ethernet Learning Switch Operation" section, your switch will also handle the frames that are intended for itself and the frames whose Ethernet destination address is the broadcast address `FF:FF:FF:FF:FF:FF`.

In addition to these, you will also implement three different mechanisms to purge the outdated/stale entries from the forwarding table. This will allow your learning switch to adapt to changes in the network topology.

These mechanisms are:

- Remove an entry from the forwarding table after 10 seconds have elapsed.

- Remove the least recently used (LRU) entry from the forwarding table. For this functionality assume that your table can only hold 2 entries at a time. If a new entry comes and your table is full, you will remove the entry that has not been matched with a Ethernet frame destination address for the longest time.

- Remove the entry that has the least traffic volume. For this functionality assume that your table can only hold 2 entries at a time. Traffic volume for an entry is the number of frames that the switch received where `Destination MAC address == MAC address of entry`.

You will implement these mechanisms in three separate Python files. The core functionalities that are explained above will be the same for these implementations.

> [!WARNING]
> Please carefully read the [FAQ](faq.md) section, for more specific details regarding the implementations

## Your Tasks

In these tasks, you will write the code to implement the core logic in an Ethernet learning switch using the Switchyard framework. Besides using Switchyard for developing and testing your switch, you can deploy it in Mininet to test it in a "live" setting. The code you'll need to add for the simplest version of this exercise should be less than 20 lines (and possibly quite a bit less depending on exactly how you write the code). There are extensions to the basic learning switch that could add quite a bit more code.

> [!NOTE]
> The sentences marked with ✅ are related to the content of your report. Please pay attention.

### Task 1: Preparation

Initiate your project with our template.

[Start the task here](preparation.md)

### Task 2: Basic Learning Switch

Start with the basic learning switch.

[Start the task here](basic-switch.md)

### Task 3: Timeouts

Implement timeouts based on the previous task.

[Start the task here](timeouts.md)

### Task 4: LRU Rule Replacement Algorithm

Implement LRU rule replacement algorithm based on Task 2.

[Start the task here](lru.md)

### Task 5: Least Traffic Volume Rule Replacement Algorithm

Implement least traffic volume rule replacement algorithm based on Task 2.

[Start the task here](ltv.md)

## Handing it in

### Report

We will provide a template of your lab assignment report [here](https://box.nju.edu.cn/d/123a70ac8ff34595b18f/). You need to submit the report in your repository named `<学号><姓名>_lab_2`. The format of your report can be Microsoft Doc or PDF. An example is `123456789拾佰仟_lab_2.docx`.

### Submit to NJU GitLab

To submit your work, you need to do the following things.

1. Modify your code and complete your report.

2. When you have done your work, put your report and code in the folder `lab_2` then commit them. Tag the commit named `<学号/lab_2>` which you want to submit. An example is `123456789/lab_2`. Finally your project will look like

   ```
   switchyard/
     ├─docs/
     ├─.../
   m ├─lab_2/
   + │ ├─123456789拾佰仟_lab_2.docx
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
