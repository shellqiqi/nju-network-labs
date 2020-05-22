# Task 5: Testing

##  Testing your code 

There is a Switchyard test script available for basic firewalling
capabilities (i.e., permit and deny rules without any rate limits or
impairment). The source code for this test scenario is available in the project repo as firewalltests.py. The test source is given since you may
find it helpful to add new tests or modify existing tests as you develop
your code. As usual, you can test your code using a command line like:

    $ swyard -t firewalltests.py firewall.py

There are minimal automated tests for the rate limitation features, and
there are no automated tests for your impairment "feature". The minimal
rate limitation tests just check whether at least one packet is
permitted by your firewall: these should all definitely pass. There are
no sophisticated tests for checking whether you impose the right rate
limit on a flow. To do that, you can use Mininet as described below.

✅ In the report, show the test result.

To test your impairment feature, you can either construct a Switchyard
test (or set of tests) or test your impairment feature in Mininet
(somehow).  
(Optional) There is a file `impairmenttest.py` in the project directory
that you can modify for testing your impairment feature with Switchyard
if you wish. There is some Switchyard documentation available to
describe the meaning of various API calls in test scenario creation.

To try your firewall in Mininet, you can do the following:

    $ sudo python start_mininet.py

Once Mininet is started, open an xterm on the node named "firewall", and
then start the firewall:

    mininet> xterm firewall

and on the firewall node:

    firewall# swyard firewall.py

There are two other hosts in the Mininet setup: one named "internal" and
another named "external".


## Testing rate limitation in Mininet

To test rule 13 (`permit icmp src any dst any ratelimit 150`), you can
use the following ping command within Mininet:

    mininet> internal ping -c10 -s72 192.168.0.2

This command will cause the "internal" host to send an ICMP echo request
(ping) to the "external" host, through the firewall device. There will
be 10 echo request packets sent, once per second, and the size of each
packet (from IP header through the end of the packet) will be 20 bytes
(IP) + 8 bytes (ICMP header) + 72 bytes (the -s72 flag) of "data",
resulting in a 100 byte packet. The echo reply will also be exactly 100
bytes.

The "steady-state" effect of this ping command line and the rate
limitation should be that every other ICMP echo request should be
allowed. (Think about why this is the case. You'll likely allow the
first couple echo request/replies, but then the every-other regime
should take hold.)

There are two other rate limitation rules: rules 7 and 8 (replicated
below):

    # rule 7
    permit tcp src 192.168.0.0/16 srcport any dst any dstport 80 ratelimit 12500
    # rule 8 
    permit tcp src any srcport 80 dst 192.168.0.0/16 dstport any ratelimit 12500

To test these rules you can generate some HTTP traffic over port 80
using some simple command-line tools. Note that these rules apply
separate rate limits to each direction of the TCP connection and that
the limit is equivalent to 100Kbits/sec. To generate HTTP/port 80
traffic to exercise these limits, do the following. On the host
"external", start a server:

    mininet> external ./www/start_webserver.sh

Besides starting up a simple Python-based webserver, this script creates
a file (called "bigfile", although it's actually pretty small) to
transfer so that we can exercise the rate limit.

Now, on the internal host, make a request using the program `wget`:

    mininet> internal wget http://192.168.0.2/bigfile -O /dev/null

(The `-O /dev/null` command-line parameter just says to save the
response in `/dev/null`, which is just a virtual wastebasket for bits.)

One other note regarding rate-limit testing: you shouldn't expect the
rate limitation to work especially well in Mininet. Your mileage may
vary, but don't be surprised if you get very poor throughput with the
firewall (and much less than the specified rate limit).

Your task is: test rate limitation in Mininet as described above. 
✅ Write the procedure and analysis in your report with screenshots.


## Testing impairments in Mininet

Testing your impairment capability depends on what you implemented. One
way to generate traffic (at least TCP traffic) for testing the
impairment is to use the http server used for testing rate limits. The
rules for the impairment is as follows (see also firewall\_rules.txt):

    # rule 11 
    permit tcp src 192.168.0.0/24 srcport any dst any dstport 8000 impair
    # rule 12
    permit tcp src any srcport 8000 dst 192.168.0.0/24 dstport any impair

To start the webserver so that it listens on port 8000 (which is the
port specified in the impair rule), you can say:

    mininet> external ./www/start_webserver.sh 8000

To generate traffic from internal to trigger the impair rule, you can
use the `wget` program again:

    mininet> internal wget http://192.168.0.2:8000/filename

The filename you use can either be "bigfile" (i.e., the same file used
in the rate limit tests) or it can be any file you construct. If your
impairment depends on certain application payload contents (e.g., you
search packets to see whether the string "sneaky crackers" is present)
you can craft files that have the desired contents. If you save them in
the www folder (directly within the project repo folder) you can use the
wget program as above to request those files and trigger your
impairment.

Your task is: test impairments in Mininet as described above. 
✅ Write the procedure and analysis in your report with screenshots.