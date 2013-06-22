.. _OpenCOR-cli:

============================
Command Line Interface (CLI)
============================

.. note::

    The CLI version of OpenCOR currently offers a limited number of features. You might therefore want to use its :ref:`OpenCOR-gui` version instead.

Help
----

::

    $ ./OpenCOR -h
    Usage: OpenCOR [-a|--about] [-c|--command [<plugin>::]<command> <options>] [-h|--help] [-p|--plugins] [-v|--version] [<files>]
     -a, --about     Display some information about OpenCOR
     -c, --command   Send a command to one or all the plugins
     -h, --help      Display this help information
     -p, --plugins   Display the list of plugins
     -v, --version   Display the version of OpenCOR

Version
-------

::

    $ ./OpenCOR -v
    OpenCOR [2013-06-22] (32-bit)

About
-----

::

    $ ./OpenCOR -a
    OpenCOR [2013-06-22] (32-bit)
    GNU/Linux 3.5.0-34-generic
    Copyright 2011-2013

    OpenCOR is a cross-platform CellML-based modelling environment which can be
    used to organise, edit, simulate and analyse CellML files.

Plugins
-------

::

    $ ./OpenCOR -p
    The following plugin is loaded:
     - CellMLTools: a plugin to access various CellML-related tools.

Command
-------

::

    $ ./OpenCOR -c help
    Commands supported by CellMLTools:
     * Display the commands supported by CellMLTools:
          help
     * Export <in_file> to <out_file> using <format> as the destination format:
          export <in_file> <out_file> <format>
       <format> can take one of the following values:
          cellml_1_0: to export a CellML 1.1 file to CellML 1.0
    $ ./OpenCOR -c CellMLTools::export in.cellml out.cellml cellml_1_0
