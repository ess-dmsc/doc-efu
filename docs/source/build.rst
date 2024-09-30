Installation
============

Building the EFU involves the use of conan and cmake and the availability of
specific (Unix) tools and system settings.

We deploy the EFU on servers that have been automatically provisioned via Ansible.

The description of prerequisites below may be viewed as necessary but not
sufficient for successfully building the EFU software.

Prerequisites
-------------

  * Conan - latest version less than 2.0
  * CMake - latest version
  * GCC - known to work with 11.2 and possible >= 8


Build
-----

.. code-block:: console

    $ clone https://github.com/ess-dmsc/event-formation-unit.git
    $ mkdir -p event-formation-unit/build
    $ cd event-formation-unit/build
    $ cmake ..
    $ make

This will build the EFU detector executables (**bin/**) and data generators
(**generators/**).

Unit tests
----------

For building and running the unit tests

.. code-block:: console

    $ make unit_tests

Unit test executables are located in **unit_tests/** and can be run individually
or via the **runtest** target

.. code-block:: console

    $ make runtest               # or for example
    $ ./unit_tests/Cluster2DTest
