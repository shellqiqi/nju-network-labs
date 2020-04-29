# FAQ

1. **Q:** How can the blaster, blastee and middlebox know the MAC and IP addresses of each other's ports? 

   **A:** You will use the addresses that are specified in start_mininet.py file. You can hard code the addresses in your code.

2. **Q:** Where do the .txt files, which are used to pass parameters to your agents, come from?

   **A:** You will create these .txt files with parameters of your choice.

3. **Q:** How does the dropping of packets work? 

   **A:** You will use the drop_rate parameter at your middlebox for deciding whether you should drop the packet or not. You can use the RNG function in Python to obtain a value (between 0 and 1) and then compare it against the drop_rate to decide what to do with the packet.

4. **Q:** Are we supposed to maintain a timer for each outstanding packet? 

   **A:** Coarse timeout applies to the whole sender window, therefore you don't need to maintain a separate timer for each outstanding packet. You will reset your timer whenever you move LHS. If the LHS value doesn't change for the duration of timeout then you will retransmit every non-ACKd packet in that window. 

5. **Q:** Can you give us an example for the coarse timeouts?  

   **A:** Let's say the sender_window is 4 and the timeout is 1 second. Initially, blaster sends packets 1,2,3 and 4. Blaster receives the ACK for 2 at 300 ms into the coarse timeout (can't move LHS or RHS since packet 1 not ACKd yet). Then it receives the ACK for 1 at 500 ms. Now, blaster will move its LHS to point at 3, reset its timer (since LHS changed), send out packets 5 and 6, move RHS to 6 (RHS(6) - LHS(3) + 1 ≤ SW(4)). Even though packet 3 and 4 were sent in the previous sender window, they will not carry their timer values to the new window. Now let's say packets 4 and 5 are immediately ACKd (around ~500 ms since the initialization of the system) by the blastee and the blaster doesn't receive the ACK for packet 3 before the coarse timeout occurs. Now the system time will roughly be at 1.5 seconds(as timeout = 1 second) and since the coarse timeout occurred, blaster will retransmit packets 3 and 6.

6. **Q:** Can I assume that the .txt files will have the parameters in the same order as illustrated above?  

   **A:** Yes, you can safely assume that.


7. **Q:** Can recv_timeout be greater than timeout? 

   **A:** No, you can safely assume that recv_timeout < timeout. If you think about it would be weird to have it the other way around as it would prevent the blaster from timing out in a timely manner. 

8. **Q:** Can we send multiple packets from the blaster at each recv_timeout loop? Or do we have to send a single packet at each loop (because recv_timeout is a pseudo-rate controller)? How about the retranmissions?

   **A:** You should be sending a single packet per each recv_timeout loop. As I mentioned in the specification, recv_timeout will work as a pseudo-rate controller. Recall that you pass recv_timeout to the recv_packet function in Switchyard and this determines how long this function will block before timing out. I use the word pseudo on purpose because your blaster can receive ACKs fast enough (and without many losses) that the recv_packet call would never time out and your blaster can send packets at a faster rate. You should follow the same logic in retransmissions.

9. **Q:**  I'm recieving this warning upon starting a device in mininet:   
WARNING **: Couldn't connect to accessibility bus: Failed to connect to socket /tmp/dbus-wYnBIGP0fz: Connection refused

   **A:** You can ignore that warning, it should not disrupt the execution of your program.