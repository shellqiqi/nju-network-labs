# Task 3: Timeouts

## Timeout Mechanism

Real learning switches remove forwarding table entries after some number of seconds have elapsed so that a learning switch can adapt to changes in network topology. Implement a timeout feature in your learning switch. Choose some reasonable value for a timeout (e.g., 10 seconds).

The following flowchart summarizes the algorithm described above.

![flowchart](./assets/to_flow.jpg)

Your switch may have a table like:

| MAC Address       | Interface   | Timestamp     |
| ----------------- | ----------- | ------------- |
| ab:cd:ef:fe:cd:ba | interface-0 | 123456.123456 |
| ...               | ...         | ...           |

## Coding

Your task is to implement the logic in the above flowchart, using the Switchyard framework. You can start with copying the content of `lab_2/myswitch.py` to `lab_2/myswitch_to.py`, which is the only file you'll need to modify.
