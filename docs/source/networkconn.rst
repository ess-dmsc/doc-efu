RM - EFU network connection
===========================

The connection between RM and EFU is via a standard Ethernet interface.

The RM must be configured with the following network parameters

 * source and destination MAC addresses (smac, dmac)
 * source and destination IP addresses (sip, dip)
 * source and destination UDP port (sport, dport)

The crucial point is that these must match the corresponding parameters on the
EFU server. The figure below shows an example of one good configuration (black line)
and one bad configuration (red line).

.. figure:: images/rm_efu_conn.png
  :width: 800
  :align: center

  Ethernet connection between RM and EFU.


Debugging
=========

To check/validate your configuration you can use **tcpdump** as shown in the
figure below.

.. figure:: images/nwparms.png
  :width: 1024
  :align: center

  Using tcpdump to prepare/validate network parameters


  The key point is
