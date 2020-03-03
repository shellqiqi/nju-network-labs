# Lab 2: Learning Switch

## Overview

In this assignment, you are going to implement the core functionalities of an Ethernet learning switch using the [Switchyard framework](https://gitee.com/shellqiqi/switchyard). An Ethernet switch is a layer 2 device that uses packet switching to receive, process and forward frames to other devices (end hosts, other switches) in the network. A switch has a set of interfaces (ports) through which it sends/receives Ethernet frames. When Ethernet frames arrive on any port, the switch process the header of the frame to obtain information about the destination host. If the switch knows that the host is reachable through one of its ports, it sends out the frame from the appropriate output port. If it does not know where the host is, it floods the frame out of all ports except the input port.

## Details

Your task is to implement the logic that is described in the flowchart [here]. As it is described in the last paragraph of the "Ethernet Learning Switch Operation" section, your switch will also handle the frames that are intended for itself and the frames whose Ethernet destination address is the broadcast address `FF:FF:FF:FF:FF:FF`.

In addition to these, you will also implement three different mechanisms to purge the outdated/stale entries from the forwarding table. This will allow your learning switch to adapt to changes in the network topology.

These mechanisms are:

- Remove an entry from the forwarding table after 10 seconds have elapsed.

- Remove the least recently used (LRU) entry from the forwarding table. For this functionality assume that your table can only hold 5 entries at a time. If a new entry comes and your table is full, you will remove the entry that has not been matched with a Ethernet frame destination address for the longest time.

- Remove the entry that has the least traffic volume. For this functionality assume that your table can only hold 5 entries at a time. Traffic volume for an entry is the number of frames that the switch received where `Destination MAC address == MAC address of entry`.

You will implement these mechanisms in three separate Python files. The core functionalities that are explained above will be the same for these implementations.

> [!NOTE]
> There is an example of a switch without learning implemented in `switchyard-master/examples/exercises/learning_switch/` which will likely be useful to get you started.

<div></div>

> [!WARNING]
> Please carefully read the FAQ section below, especially the flowcharts, for more specific details regarding the implementations

## Handing it in

### Report

We will provide a template of your lab assignment report [here](https://box.nju.edu.cn/d/123a70ac8ff34595b18f/). You need to submit the report in your repository named `<学号><姓名>_lab_2`. The format of your report can be Microsoft Doc or PDF. An example is `123456789拾佰仟_lab_2.docx`.

### Submit to NJU GitLab

To submit your work, you need to do the following things at the first time

1. Create a directory named `lab_2` in `switchyard`. Your should start by copying the template files `examples/exercises/learning_switch/switchtopo.py`, `examples/exercises/learning_switch/myswitch.py` into `lab_2`. And your project will look like

  ```
    switchyard
      ├─docs/
      ├─.../
    + ├─lab_2
    + │ ├─myswitch.py
    + │ └─switchtopo.py
      ├─.gitignore
      └─...
  ```

Then complete your switch. When you are ready to submit, do the following.

1. Modify your code and complete your report.

  > [!WARNING]
  > All of your modifications should be done on the files under your directory `lab_2`. We will check and compare the **git commits** to judge the originality of your work. So remember to commit every time you complete one small task.

2. When you have done your work, put your report and code in the folder `lab_2` then commit them. Tag the commit named `<学号/lab_2>` which you want to submit. An example is `123456789/lab_2`. Finally your project will look like

  ```
    switchyard/
      ├─docs/
      ├─.../
    m ├─lab_2/
    + │ ├─123456789拾佰仟_lab_2.docx
    m │ ├─myswitch.py
    m │ └─switchtopo.py
      ├─.gitignore
      └─...
  ```

  > [!WARNING]
  > The file names in your submission have to **exactly** match the file names above. Otherwise, you will lose points!

3. Submit your work by pushing your local repository to your remote repository **with your tags** by running the command `git push origin --tags`.

  > [!WARNING]
  > **Only** commit your **source code** to your local repository. If there are some generated files that are not source code, ignore them by adding them in the file `.gitignore`.
