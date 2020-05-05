# Task 5: Running your code 

##  Testing your code 

Good news: you aren't going to write test cases to test your implementation. Bad news: you still need to test your code. In order to make sure that your blaster, blastee and middlebox function correctly you will have to use Mininet. The process will be explained below. 

## Running your code 

Instead of running your implementations with test scenarios, you will be running the agents in Mininet. We are providing you with a topology file (`start_mininet.py`) in Mininet. Comments are added so please read them to understand the setup. Please do not change the addresses(IP and MAC) or node/link setup. We will be using the same topology file when testing your code (although we reserve the right to use different delay values). To spin up your agents in Mininet:

1. Open up a terminal and type the following command. This will get Mininet started and build your topology:

        $ sudo python start_mininet.py

2. Open up a xterm on each agent:

        mininet> xterm middlebox
        mininet> xterm blastee
        mininet> xterm blaster

3. Start your agents:

        middlebox# ./switchyard/swyard.py middlebox.py
        blastee# ./switchyard/swyard.py blastee.py
        blaster# ./switchyard/swyard.py blaster.py

You will need to specify some parameters for each agent when running them. To my knowledge, it is not possible to pass custom parameters to Switchyard (probably why you assumed there was a forwarding_table.txt file in your working directory in last project as well). However, this is not going to keep us from passing parameters to our agents. Just like in the previous project you will assume that there will be 3 files in your working directory: **blaster_params.txt**, **blastee_params.txt** and **middlebox_params.txt**.

Your task is: run your code in Mininet as described above. Using different parameters to get different results and analyze them. Using Wireshark on different agent to prove that your blaster, blastee and middlebox function correctly.

✅ Write the procedure and analysis in your report with screenshots.
