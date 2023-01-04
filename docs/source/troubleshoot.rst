Troubleshooting
===============

Step by step
------------

You have built and launched the EFU and you believe that data should be
flowing through it but you do not 'see' any [#f1]_ . Now what?

In this case the first steps are to check that the EFU is running and reachable.

Is the EFU process running?
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

    $ ps aux | grep bifrost
    username 54703  \.\.deleted info\.\. ./bin/bifrost -f ../src/modules/bifrost/configs/bifrost.json --nohwcheck

In this case it looks like EFU is running the BIFROST instrument.


Does it respond to commands?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use :ref:`efustat` to check that the EFU is accepting commands
and returning counter values.


Verify the data port
^^^^^^^^^^^^^^^^^^^^

When running the EFU should listen for detector data on UDP port 9000 (unless
you have configured it differently)

.. code-block:: console

    $ netstat -an | grep udp
    udp4       0      0  *.56174                *.*
    udp4       0      0  *.9000                 *.*
    udp4       0      0  192.168.1.119.50683    193.11.102.50.4501
    udp4       0      0  *.*                    *.*
    udp4       0      0  *.*                    *.*
    ...

Here the line with '*.9000' shows that 'something' is listening on UDP port 9000.
Let's identify the process.

.. code-block:: console

    $ lsof -Pni | grep -i udp
    identitys  1062 username   23u  IPv4 0x223cfeac89ffbf07      0t0  UDP *:*
    identitys  1062 username   28u  IPv4 0x223cfeac8948d527      0t0  UDP *:*
    rapportd   1070 username    3u  IPv4 0x223cfeac8a705b47      0t0  UDP *:*
    ...
    ControlCe  1109 username    8u  IPv4 0x223cfeac894a43c7      0t0  UDP *:*
    bifrost   54703 username    3u  IPv4 0x223cfeac894793c7      0t0  UDP *:9000

Here we see that bifrost is the process listening on UDP port 9000.

At this stage we are pretty sure that the EFU is up and running and listening
for data (and commands) on the expected ports. It is pretty likely that the
problem is that it is either not receiving any data or is discarding the
received data (due to misconfiguration).

To distinguish between these two scenarios we use :ref:`efustat`:

.. code-block:: console

    $ python3 efustat.py | grep receive
    STAT_GET efu.bifrost.0.receive.packets 0
    STAT_GET efu.bifrost.0.receive.bytes 0
    STAT_GET efu.bifrost.0.receive.dropped 0
    STAT_GET efu.bifrost.0.receive.fifo_seq_errors 0

If you repeat this a few times and still see a packet count of 0 then the problem
is likely that the EFU is not receiving any data on the UDP port. There can be a
number of reasons for this.

* No data is being sent to the EFU
* Data is being sent but dropped by intermediate network device (switch)
* Data is being sent - and dropped by the NIC/OS
* Data is being sent but EFU MTU is too small
* Data is being sent but to wrong UDP port

A typical investigation approaches this list in turn starting from the end of
the list.

However the last three can be checked in one go using network capture tools
such as Wireshark or tcpdump.

It is outside the scope of this document to provide a tutorial for these tools,
but the things to look out for when viewing the raw data are:

* Is UDP data being captured? If so to which destination port?
* What is the size of the data? (if > 1500 bytes, check MTU)
* Does the destination IP address match the IP address of the EFU?
* Is the source IP address valid?
* Does the destination MAC address match the MAC address of the EFU interface?
* Is the source MAC address valid?

If you can capture seemingly valid data with wireshark but still do not get
data into the EFU it could be because you have firewall rules causing the data
to be dropped.

.. rubric:: Footnotes

.. [#f1] For example there is no data on the Grafana dashboard or no data in the file generated downstream of Kafka (by the ESS FileWriter).
