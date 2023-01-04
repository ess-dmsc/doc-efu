Network utilities
=================

This is a messy collection of commands and utilities that can be of use for
troubleshooting network issues.

Network interfaces
------------------


ifconfig
^^^^^^^^

To list all interfaces on your system and show their name,
IP address and MAC address:

.. code-block:: console

    $ ifconfig | grep -e '^[a-z]\|inet \|ether'

    lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
    	inet 127.0.0.1 netmask 0xff000000
    ...
    en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
    	ether f8:ff:c2:5d:02:a7
    	inet 192.168.1.119 netmask 0xffffff00 broadcast 192.168.1.255
    ...


Set the MTU of an interface:

.. code-block:: console

    $ ifconfig en1 mtu 9000



netstat
^^^^^^^

Check for udp services (ports that are in use):

.. code-block:: console

    $ netstat -anp udp
    ...


Show protocol stack counters for udp

.. code-block:: console

    $ netstat -s -p udp
    ...

Network capture
---------------

With packet capture tools you can capture the raw network data - including
some that would be dropped by the Operating System's protocol stack.


tcpdump
^^^^^^^
A command line based capturing tool.

To capture to console in increasing order of specificity:

.. code-block:: console

    $ tcpdump -i lo0
    $ tcpdump -i lo0 udp
    $ tcpdump -i lo0 udp port 9000
    $ tcpdump -i lo0 udp port 9000 and greater 7000


To capture a specific number of packets and write them to file:

.. code-block:: console

    $ tcpdump -i lo0 udp port 9000 -c 1000 -w capture.pcap


Wireshark
^^^^^^^^^

Wireshark is a GUI based network capture tool. It can be loaded with custom made
plugins for specific protocols/data formats. This makes it valuable for advanced
debugging.

It does however, require a graphical desktop environment and may not always be
available. Hence for simply capturing traffic that need to be emailed for
support we recommend using tcpdump.
