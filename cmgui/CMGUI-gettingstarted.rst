.. _CMGUI-gettingstarted:

==========================
Getting started with CMGUI
==========================

This section will introduce you to the capabilities of CMGUI, as well as how to install and begin using the software.

Where to go for help
====================

There is a `large collection of examples <http://cmiss.bioeng.auckland.ac.nz/development/examples/a/index_thumbs.html>`_ which can be used to learn about the capabilites and operation of CMGUI.


Issues with the software can be reported and discussed on the tracker, which is found at `https://tracker.physiomeproject.org <https://tracker.physiomeproject.org>`_.

What is CMGUI and what can it do?
=================================

CMGUI is an advanced 3D visualization open source software package with modelling capabilities. It originated as part of CMISS, a collection of software for "Continuum Mechanics, Image processing, Signal processing and System identification".  CMISS includes cm, a closed-source application for finite element method computation and related computation.  Historically CMGUI has been mostly used in conjunction with cm.  OpenCMISS-Iron (www.opencmiss.org) is an open source project, currently under development, aiming to replace the closed source CMISS-cm.

A `gallery demonstrating some of the uses of CMGUI <http://cmiss.bioeng.auckland.ac.nz/development/examples/a/index_thumbs.html>`_ is available.

Some of the main areas of functionality of CMGUI are as follows:

* 3D visualization of finite element and boundary element meshes
* Mesh creation
* Mathematical field visualization and manipulation

CMGUI is mainly controlled from its built in "command line" interpreter. Usually script files are read or commands are typed in the CMGUI command window to read in your mesh, create a 3D visualisation and manipulate it. Many tasks can also be accomplished by using the mouse to select options from various menus and dialogs. CMGUI has a large amount of functionality but it can be difficult for a new user to figure out what command to use to accomplish exactly what they want to do. Fortunately there are a large number of examples demonstrating the use of various different commands.

CMGUI is also used as part of the Zinc extension to Mozilla Firefox. The Zinc extension allows users to view Zinc applications and visualizations in Firefox. A Zinc application uses CMGUI for visualization while providing a nice customized user interface for a specific task. For example Zinc applications have been written to do the following:

* Interactively explore Colon endoscopy
* Explore the Physiome eye model
* Create data points to give a digital description of a geometry based on medical images.

Note that Zinc is compiled as a separate application from CMGUI. You do NOT have to install CMGUI to use Zinc. For more information on Zinc see `http://www.cmiss.org/CMGUI/zinc <http://www.cmiss.org/CMGUI/zinc>`_.

Installation
============

CMGUI is currently available for download for a wide variety of platforms. You can download the appropriate executable for your operating system `from the release centre <http://www.cmiss.org/ReleaseCenter/CMGUI>`_.

CMGUI is quite a large application so the executable has been archived (tarred) and compressed (zipped) to make it faster to download. Once you have downloaded the executable all you need to do is untar and unzip it and it is ready to run. On Linux you can untar and unzip the tar.gz file with the command::

   tar -xf filename.tar.gz.

On Windows you will need `7Zip <http://www.7-zip.org/>`_ or something similar to unzip the file. You should now be able to run CMGUI by either clicking on the executable or by changing into the directory it is located in and then typing ./ followed by the name of the executable at the command prompt, eg. ``./CMGUI-wx``. This will bring up the CMGUI command window interface.

For convenience it is a good idea to place the directory containing CMGUI into your PATH environmental variable. That way you will be able to run CMGUI without having to be in the directory that contains the executable. To do this on a Linux system you can specify your PATH variable in your .profile file. On Windows you can edit your PATH variable by right clicking on my computer and then selecting: properties, advanced, environment variables. Ask your local system administrator if you do not know how to edit the PATH variable for your operating system.
