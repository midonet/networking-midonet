==================
networking-midonet
==================

This is the official Midonet Neutron plugin.


How to Install
--------------

Run the following command to install the plugin in the system::

    $ sudo python setup.py install


The following entry in ``neutron.conf`` enables MidoNet as the Neutron plugin.
There are two Kilo plugins to choose from.

Kilo plugin v1, which is compatible with MidoNet v2015.03 and v2015.06::

    core_plugin = neutron.plugins.midonet.plugin.MidonetPluginV2


Kilo plugin v2, which is compatible with MidoNet v2015.09 and beyond::

    core_plugin = midonet.neutron.plugin_v2.MidonetPluginV2


LBaaS
-----

Starting in Kilo, MidoNet plugin implements LBaaS v1 following the advanced
service driver model.  To configure MidoNet as the LBaaS driver, set the
following entries in the Neutron configuration file
``/etc/neutron/neutron.conf``::

    [DEFAULT]
    service_plugins = lbaas

    [service_providers]
    service_provider=LOADBALANCER:Midonet:midonet.neutron.services.loadbalancer.driver.MidonetLoadbalancerDriver:default


Tests
-----

You can run the unit tests with the following command::

    $ ./run_tests.sh -f -V

``run_tests.sh`` installs its requirements to ``.venv`` on the initial run.
``-f`` forces a clean re-build of the virtual environment. If you just make
changes on the working tree without any change on the dependencies, you can
ignore ``-f`` switch.

``-V`` or ``--virtual-env`` is specified to use virtualenv and this should be
always turned on.


To know more detail about command options, please execute it with ``--help``::

    $ ./run_tests.sh --help


Creating Packages
-----------------

Run the following command to generate both both the RPM and Debian packages
with the provided version::

    $ ./package.sh some_version


HACKING
-------

To contribute to this repo, please go through the following steps.

1. Keep your working tree updated
2. Make modifications on your working tree
3. Run tests
4. If the tests pass, submit patches to our Gerrit server to get them reviewed
