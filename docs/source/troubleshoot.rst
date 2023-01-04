Troubleshooting
===============

Step by step
------------

You have built and launched the EFU and you believe that data should be
flowing through it but you do not 'see' [#f1]_ any. Now what?

In this case the first steps are to check that the EFU is running and reachable.

Is the EFU process running?
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

    $ ps aux | grep bifrost
    username 54703  18.6  0.1 34604200  18724 s002  S+   12:39PM   0:02.06 ./bin/bifrost -f ../src/modules/bifrost/configs/bifrost.json --nohwcheck


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
    identitys  1062 mortenchristensen   23u  IPv4 0x223fceca89ffbf07      0t0  UDP *:*
    identitys  1062 mortenchristensen   28u  IPv4 0x223fceca8948d527      0t0  UDP *:*
    rapportd   1070 mortenchristensen    3u  IPv4 0x223fceca8a705b47      0t0  UDP *:*
    ...
    ControlCe  1109 mortenchristensen    8u  IPv4 0x223fceca894a43c7      0t0  UDP *:*
    bifrost   54703 mortenchristensen    3u  IPv4 0x223fceca894793c7      0t0  UDP *:9000

Here we see that bifrost is the one listening on UDP port 9000.

At this stage we are pretty sure that the EFU is up and running, listening for data
(and commands) on the expected ports. It is pretty likely that the problem is that
it is either not receiving any data or is discarding the received data (due to
misconfiguration).

Finally we can use the output of :ref:`efustat` to distinguish between these two
scenarios:

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

The typical investigation approaches this starting from the end of the list.








.. rubric:: Footnotes

.. [#f1] For example there is no data on the Grafana dashboard or no data in the file generated downstream of Kafka (by the ESS FileWriter).
