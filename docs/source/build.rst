Installation
============

Building the EFU involves the use of conan and cmake and the availability of
specific (Unix) tools and system settings.

We deploy the EFU on servers that have been automatically provisioned via Ansible.

The description of prerequisites below may be viewed as necessary but not
sufficient for successfully building the EFU software.

Prerequisites
-------------

Conan, CMake - latest versions


Build
-----

.. code-block:: console

    $ clone https://github.com/ess-dmsc/event-formation-unit.git
    $ mkdir -p event-formation-unit/build
    $ cd event-formation-unit/build
    $ cmake ..
    $ make

This will build the EFU detector implementations and data generators.
