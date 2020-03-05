# Testing & Deploying

## Test Your Switch

You should first develop your switch code using the Switchyard test framework. Assuming you have installed Switchyard in a Python virtual environment and have activated that venv, you should run:

```
(syenv) $ swyard -t lab_2/mytests.py lab_2/myswitch.py
```

The above command it will execute a series of test cases against your program and display whether the tests pass or fail. This time you need to test all your 4 types of switches.

In the report, explain your test scenarios. Make sure you have covered all aspects of your code for each type of your switches. Skip the test case of the same functionality among 4 types of switches. We do not want you to explain your implementing procedure but the meaning of your test scenarios.

Once you get the tests to pass, you can try running your code in Mininet.

## Run in Mininet

To run your switch in Mininet, run the `lab_2/start_mininet.py` custom topology script. It will create a small network consisting of a single switch with three hosts (client, server1, and server2) in the following configuration.

To start up Mininet using this script, just type:

```
$ sudo python lab_2/start_mininet.py
```

Once Mininet starts up, you should open a terminal window on the Mininet node named "switch":

```
mininet> xterm switch
```

In the window that opens, activate venv and run your switch in "real" (non-test) mode:

```
(syenv) # swyard myswitch.py
```

> [!NOTE]
> Note that to run `swyard` in Mininet in a root shell (such as the shell that is open in response to the `xterm` command), you will need to activate the Python virtual environment which has Switchyard installed in it. Refer to the Switchyard documentation for more information.

To examine whether your switch is behaving correctly, you can do the following:

1. Open terminals on client, server1 and server2 (`xterm client`, `xterm server1` and `xterm server2` from the Mininet prompt)
2. In the server1 and server2 terminal, run `wireshark`. Wireshark is a program that allows you to "snoop" on network traffic arriving on a network interface. We'll use this to verify that we see packets arriving at server1 and server2 from client.
3. In the terminal on the client node, type `ping -c 2 192.168.100.1`. This command will send two "echo" requests to the server1 node. The server1 node should respond to each of them if your switch is working correctly. You should see at the two echo request and echo replies in Wireshark running on server1, and you will probably see a couple other packets (e.g., ARP, or Address Resolution Protocol, packets).
4. If you run Wireshark on server2, you should **not** see the echo request and reply packets (but you will see the ARP packets, since they are sent with broadcast destination addresses).

Analyze the capture results in your report with screenshots. In the report you need to show just **one** implementation of your switch.
