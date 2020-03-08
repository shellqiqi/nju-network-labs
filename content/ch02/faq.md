# FAQ

1. **Q:** Let's assume that the table in my switch has 5 entries: `[h2, h3, h4, h5, h1]` where `h2` is the entry that has not been matched the longest while `h1` is the most recently matched entry. If a new packet `(src=h6, dest=h2)` arrives, how is my switch supposed to handle this packet in the LRU-based entry removal implementation (assuming that the network topology does not change)?

   **A:** Whenever you receive a new packet, you will assess the state of the switch as if you don't know about the new packet and make decisions accordingly. So when your switch receives `(h6, h2)`, it is going to add an entry for `h6` since it is not in the table. However, since the table is full (5 entries) it will need to remove the LRU entry, which is `h2`. So your table is going to look like this: `[h3, h4, h5, h1, h6]` and your switch will broadcast the incoming packets on all ports except for the incoming port since it does not have information about `h2` anymore. In other words, your switch (upon receiving the packet) is not going to update the table to `[h3, h4, h5, h1, h2]`, remove `h3` and add `h6` to get `[h4, h5, h1, h6, h2]` and output the packet on a single port, which goes to `h2`.

2. **Q:** How do the entry removal mechanisms work?

   **A:** Note that the flow chart for timeout based mechanism does not show when/how to purge the stale entries. Your implementation will obviously handle this as well. Keep in mind that there is not a limit on the number of entries that the table can hold for this mechanism.

3. **Q:** How would the table look for the following sequence of packets in the LRU-based implementation: `(h1,h4)`, `(h2,h1)`, `(h3,h1)`, `(h4,h1)`, `(h5,h1)`, `(h6.h7)`, `(h4,h5)`? (assuming that the network topology does not change)

   **A:** Assuming that the leftmost entry is the most recently used and the rightmost is the least recently used: `[h1] → [h1, h2] → [h1, h3, h2] → [h1, h4, h3, h2] → [h1, h5, h4, h3, h2] → [h6, h1, h5, h4, h3] → [h5, h6, h1, h4, h3]`

4. **Q:** Should our switch implementations be aware of changes in the topology?

   **A:** Your learning switch has to be aware of the changes in the topology. More specifically, if the switch receives a packet from host A on its interface 1 (`i1`) it will record this in its table `{a → i1}`. Later, if the switch receives another packet from host A but on a different interface (say `i2`), and if the entry `{a → i1}` is still present, it will be updated to `{a → i2}`. There will not be two different entries for the same host in your table! Reflecting the topological changes in your implementations will differ slightly:

   - Timeout-based: When updating the entry for a particular host, reset its timer to 0 (this will be equivalent to refreshing the entry for that host).

   - LRU-based: When updating the entry for a particular host, *do not* update its LRU information.

   - Traffic volume-based: When updating the entry for a particular host, keep the same traffic volume count for the host. *Do not* set it to 0.

5. **Q:** In traffic volume based entry removal, which entry should be removed if there are two entries with the lowest traffic volume?

   **A:** You can pick an entry randomly.
