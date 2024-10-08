Utilities
=========

.. _efustat:

efustat
-------

The EFU has several 64bit counters for its internal processing state. These
are normally published to Grafana, where they are rendered as time-series data
graphs.

The runtime counters can be queried via the EFU command interface using a
python tool (utils/efushell/efustats.py). It will provide a list of the
Grafana metric name and values.

.. code-block:: console

    $ python3 efustat.py -i 10.0.0.1 -p 8888

    Available stats (43):
    STAT_GET efu.bifrost.0.receive.packets 0
    STAT_GET efu.bifrost.0.receive.bytes 0
    STAT_GET efu.bifrost.0.receive.dropped 0
    STAT_GET efu.bifrost.0.receive.fifo_seq_errors 0
    ...
    STAT_GET efu.bifrost.0.events.count 0
    STAT_GET efu.bifrost.0.events.pixel_errors 0
    STAT_GET efu.bifrost.0.thread.input_idle 41
    STAT_GET efu.bifrost.0.thread.processing_idle 246658
    STAT_GET efu.bifrost.0.transmit.bytes 0
    ...
    STAT_GET efu.bifrost.0.main.uptime 4
    $


efustatus
---------

There is also a status command (utils/efushell/efustatus.py) that returns
additional information such as build information, detector module, available
commands, etc.

.. code-block:: console

    $ python3 efustatus.py -i 10.0.0.1 -p 8888

    EFU Stats:
    Connection info. ip address: 127.0.0.1, tcp port: 8888
    b'RUNTIMESTATS 0'
    b'VERSION_GET master-bd467ae0 2023-01-04 11:06:00 [CI0021388:mortenchristensen] [21.6.0] bd467ae0'
    b'DETECTOR_INFO_GET bifrost'
    Available commands: (CMD_GET 1 - 8)
    b'CMD_GET'
    b'CMD_GET_COUNT'
    b'DETECTOR_INFO_GET'
    b'EXIT'
    b'RUNTIMESTATS'
    b'STAT_GET'
    b'STAT_GET_COUNT'
    b'VERSION_GET'
    Available stats: (STAT_GET 1 - 43)
    b'efu.bifrost.0.receive.packets'
    b'efu.bifrost.0.receive.bytes'
    b'efu.bifrost.0.receive.dropped'
    ...
    $


qtefu
--------

A Qt GUI (utils/qtrunefu/qtefu.py) to launch EFUs providing different configurations
and quick launch.

.. figure:: images/qtefu.png
  :width: 800
  :align: center

  Qt based EFU launcher.
