Running
=======

Once started, the EFU will not terminate on its own but will run indefinitely. At ESS
is will be launched as a systemd process running in the background.


Start
-----

An example of launching the EFU with the minimum required arguments would be something
like this

.. code-block:: console

    $ cd event-formation-unit/build
    $ ./bin/bifrost -f config.json --nohwcheck [more args]


However for real applications more is needed.

Arguments
---------

The most important command line arguments are listed below

.. list-table:: Command line arguments
   :widths: 25 100
   :header-rows: 1

   * - option
     - description
   * - -f file
     - configuration file
   * - -b broker
     - kafka broker ('10.0.0.1:9092')
   * - -g graphite
     - graphite server ip ('10.0.0.2')
   * - -p port
     - data port (UDP)
   * - -m port
     - command port (TCP)



To see all options for a given detector implementation

.. code-block:: console

    $ ./bin/bifrost -h

    Event formation unit (efu)
    Usage: ./bin/bifrost [OPTIONS]

    EFU Options:
      -h,--help                   Print this help message and exit
      --version                   Print version and exit
      -a,--logip TEXT=127.0.0.1   Graylog server IP address
      -b,--broker_addr TEXT=localhost
                                  Kafka broker address
      -t,--broker_topic TEXT      Kafka broker topic
      --kafka_config TEXT         Kafka configuration file
      -l,--log_level=Info         Set log message level. Set to 1 - 7 or one of
                                                                `Critical`, `Error`, `Warning`, `Notice`, `Info`,
                                                                or `Debug`. Ex: "-l Notice"
      --log_file TEXT             Write log messages to file.
      --nohwcheck                 Perform HW check or not
      -i,--dip TEXT=0.0.0.0       IP address of receive interface
      -p,--port UINT=9000         TCP/UDP receive port
      -m,--cmdport UINT=8888      Command parser tcp port
      -g,--graphite TEXT=127.0.0.1
                                  IP address of graphite metrics server
      -r,--region TEXT=region1    name of detector region covered by this pipeline
      -o,--gport UINT=2003        Graphite tcp port
      -s,--stopafter UINT=4294967295
                                  Terminate after timeout seconds
      --updateinterval UINT=1     Stats and event data update interval (seconds).
      --rxbuffer INT=2000000      Receive from detector buffer size.
      --txbuffer INT=9216         Transmit to detector buffer size.
      -f,--file TEXT              Detector configuration file (JSON)
      --calibration TEXT          Detector calibration file (JSON)
      --dumptofile TEXT           dump to specified file
      --udder                     Generate a test image
      --udder_usleep UINT=10      usleep between udder pixels


    MBCAEN:
      --multiblade-alignment      Enter alignment mode (2D)
