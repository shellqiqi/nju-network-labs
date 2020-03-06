# Task 3: Modification

## Preparation

Let's start with our example files.

Create a directory named `lab_1` in `~/switchyard`. Your should start by copying the template files `examples/start_mininet.py`, `examples/myhub.py` and `examples/hubtests.py` into `lab_1`. And your project will look like

```
switchyard/
  ├─docs/
  ├─.../
+ ├─lab_1/
+ │ ├─hubtests.py
+ │ ├─myhub.py
+ │ └─start_mininet.py
  ├─.gitignore
  └─...
```

## Play the Tutorial Again

You have done the tutorial. However it is necessary to work by yourself. So modify our examples files.

> [!TIP]
> We suggest that you can commit in Git when you complete one step.

<div></div>

> [!WARNING]
> All of your modifications should be done on the files under your directory `lab_1`. We will check and compare the **git commits** to judge the originality of your work. So remember to commit every time you complete one small task.

### Step 1: Modify the Mininet topology

In the section [Mininet](mininet.md), we introduced how to construct a topology. So here we have two options for you, choose **one** to implement. Then show the details of how you build the topology in your report.

- Delete `server2` in the topology,
- Or create a different topology containing 6 nodes using hosts and hubs (don't use other kinds of devices).

The file you need to modify is `lab_1/start_mininet.py`.

### Step 2: Modify the logic of a device

In the section [Switchyard](switchyard.md), we introduced how to program a device. Your task is to count how many packets pass through a hub in and out. You need to log the statistical result every time you receive one packet with the format of each line `in:<ingress packet count> out:<egress packet count>`. For example, if there is a packet that is not addressed to the hub itself, then the hub may log `in:1 out:2`. Then show the log of your hub when running it in Mininet and how you implement it in your report.

> [!NOTE]
> In the old version we need you to print the timestamp then we remove it. So many students ask why because there is a function `log_info` which prints the time of log output. However we want you to log the packet arrival time which is different from output time.
>
> Because our explanation is late, if you have implemented it in another way, you do **not** need to change.

The file you need to modify is `lab_1/myhub.py`.

### Step 3: Modify the test scenario of a device

In the section [Switchyard](switchyard.md), we introduced how to write the test case. So here we have two options for you, choose **one** to implement. Then show the details of your test cases in your report.

- Create one test case by using the given function `mk_pkt` with different arguments,
- Or create one test case with your handmade packet.

The file you need to modify is `lab_1/hubtests.py`.

### Step 4: Run your device in Mininet

In the section [Switchyard](switchyard.md), we introduced how to run Switchyard programs in Mininet. So run your new hub in your new topology and make sure it works. Show the procedure in your report.

### Step 5: Capture using Wireshark

Both in section [Wireshark](wireshark.md) and [Switchyard](switchyard.md), we introduced how to capture packets. In your own topology, capture packets on one host (no hub) while creating some traffic. **Save your capture file** and submit it with your report and code. Also you need to describe the details of your capture file.
