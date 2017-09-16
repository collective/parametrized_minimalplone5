minimalplone5
=============

This is an example for parametrized zope instances.

The instance created by this buildout script needs two environment variables
and a directory that must be created by yourself::

    $ export INSTANCE_PORT=12345
    $ mkdir -p instance_$INSTANCE_PORT
    $ CLIENT_HOME=$(pwd)/instance_${INSTANCE_PORT} ./bin/instance fg


Prerequisites
-------------
- Python 2.7
- Python Virtualenv
- Git


Install
-------

For the default configuration with the latest Plone 5 release::

    $ git clone git@github.com:collective/minimalplone5.git
    $ ./bootstrap.sh

If you want to install the development version of Plone based buildout.coredev::

    $ ./bootstrap.sh -c coredev.cfg

Or if you want to use the ZEO configuration::

    $ ./bootstrap.sh -c zeo.cfg

In any case you will be asked for an administrative username and password.

Fire up Zope and maybe the ZEO Server::

    $ ./bin/zeoserver start
    $ ./bin/instance start

Point your webbrowser to http://localhost:8080 (username admin, password admin)
and install a Plone instance.

That's all, folks.


Extend the config
-----------------

For your own projects, you might extend the configuration. Use a different
PORT, add some more eggs, like::

    [buildout]
    extends = zeo.cfg

    [zeoserver]
    zeo-address = 8100

    [instance]
    http-address = 8080
    zeo-address = ${zeoserver:zeo-address}
    eggs +=
        plone.app.debugtoolbar
        plone.app.widgets

