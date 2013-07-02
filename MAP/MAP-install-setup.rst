.. _MAP-install-setup:

================================
MAP Installation and Setup Guide
================================

This document describes how to install and setup the MAP software for use on your machine.  The MAP software is a Python application that uses the PySide Qt library bindings.  The instructions in this document cover the installation and setup on a Windows based operating system.  The instructions for GNU/Linux and OS X are similar and should be extrapolated from these instructions.  There are some side notes for these other operating systems to help, but not full or dedicated instructions.  If for any reason you get stuck and cannot complete the instructions please `contact us <https://launchpad.net/mapclient>`_.

MAP
===

The MAP framework is written in :term:`Python` and is designed to work with Python 2 and Python 3.  The MAP application is tested against Python2.6, Python2.7 and Python3.3 and should work with any of these Python libraries.  Currently the MAP framework is not packaged as an application, requiring the user to set up the environment prior to launching the ``mapclient.py`` executable Python script.

The MAP application consists of the framework and various tools, by itself it can do very little.  It is the job of the plugins to provide functionality.  The MAP application as referred to in this section of the instructions may be described as the barebones application for this reason.

To execute the barebones application we need to first install some dependencies:

 #. `Python <http://python.org/>`_ (and make sure to add the ``Python`` and ``Python\Scripts`` folders to your system ``PATH``).
 #. `PySide <http://qt-project.org/wiki/PySide>`_ (PySide and PyQt4 are virtually interchangeable but currently this would require some textual changes)
 #. `Python setup tools <https://pypi.python.org/pypi/setuptools/0.7.5#id73>`_ and then using ``easy_install.exe`` to install:
 
   #. `Requests <http://docs.python-requests.org/en/latest/>`_ Python library (``easy_install requests``)
   #. `OAuthlib <https://oauthlib.readthedocs.org/en/latest/index.html>`_ Python library (**not** the OAuth Python library) (``easy_install oauthlib``). 
 
Also, if we wish to interact with the Physiome Model Repository (PMR) we need:

 #. :term:`Mercurial`
 
We can now install the barebones `MAP client application <https://launchpad.net/mapclient/+download>`_. The barebones application can be launched via the command window with the following command in the extracted ``mapclient/src`` folder::

   mapclient.py
   
which should result in an application window similar to that shown below.

.. figure:: images/mapClientBarebones.png
   :align: center
   :width: 80%
   
Now that the barebones MAP application is installed and running we can move on to some useful plugins.

MAP Plugins
===========

Zinc and PyZinc
===============

Zinc is an advanced visualisation library and PyZinc is the Python bindings for this library.  Binaries are available from `Physiome Zinc Downloads`_ and `Physiome PyZinc Downloads`_.  

Which Binary?
-------------

There are a number of binaries available for any given platform and you must match the package description with your system setup.  The package description contains the package name, package version, package architecture, package operating system and in the case of PyZinc the package Python version.  The package extension indicates the type of package and they come in two main flavours: installer/package manager; archive.

Additionally the version of the PyZinc binaries you download must match the version of the Zinc library binaries.

