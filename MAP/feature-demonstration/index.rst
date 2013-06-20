.. _MAP-feature-demonstration:

==========================
MAP Features Demonstration
==========================

.. sectionauthor:: Hugh Sorby

.. _MAP: https://simtk.org/home/map
.. _launchpad project: http://launchpad.net/mapclient
.. _github project: https://github.com/mapclient-plugins
.. _physiome: http://physiomeproject.org/zinclibrary
.. _pyside: https://pypi.python.org/pypi/PySide
.. _project downloads: https://launchpad.net/mapclient/download

.. note::
   `MAP`_ is currently under active development, and this document will be updated to reflect any changes to the software or new features that are added. You can follow the development of MAP at the `launchpad project`_.

This document details some of the features of `MAP`_, a cross-platform framework for managing workflows. MAP is a plugin-based application that can be used to create workflows from a collection of workflow steps.

In order to go through this demonstration, you will need;

- version X.Y of MAP, available from the `project downloads`_.
- the plugins available from the `github project`_.
- the Zinc library and the PyZinc extension module from `physiome`_
- the PySide the Qt widget toolkit bindings

.. todo::
   Need to consolidate downloads somewhere convenient and maybe make a workspace in the repository for the demonstration models.

Install MAP, and get the MAP plugins.  See notes on MAP-install-setup_.

In this demonstration we will cover the features of MAP.  We will start with a quick tour and then create a new workflow that will help us segment a region of interest from a stack of images.

Quick Tour
==========

When you first load MAP, it will look something like this:

.. figure:: /MAP/feature-demonstration/images/blank_MAP_1.png
   :align: center
   :width: 80%

In the main window we can see three distinct areas that make up the workflow management side of the software.  These three areas are the menu bar (at the top), the step box (on the left) that contains steps that you can use to create your workflow and the workflow canvas (on the right) for constructing a workflow.

In the Step box we will only see two steps, this is because we have only loaded the default Steps.not loaded any of the external plugins that MAP can use.

Menu Bar
--------

The Menu bar provides a selection of drop down menus for accessing the applications functions.  The File menu provides access to opening, closing workspaces as well as quitting the application.  The Edit menu provides access to the undo/redo functionality.  The Tools menu provides access to the Plugin Manager tool, Physiome Model Repository (PMR) tool and the Annotation tool.  The Help menu provides access to the about box which contains information on contributors and the license that the MAP is released under.

Step Box
--------

The Step box provides a selection of steps that are available to construct a workflow from.  The first time we start the program only the default plugins are available.  To add more steps we can use the Plugin Manager tool.  To use a step in our workflow we drag the desired step from the step box onto the workflow canvas.

Workarea
--------

The workflow canvas is where we construct our workflow.  We do this by adding the steps to the workflow canvas from the step box that make up our workflow.  We then make connections between the workflow steps to define the complete workflow.

Getting Started
===============

To get started with MAP we need to create a new workflow.  To do this we use File -> New -> Workflow menu option (Ctrl-N shortcut).  This option will present the user with a directory selection dialog.  Use the dialog to select a directory where the workflow can be saved.  Once we have chosen a directory the step box and workflow canvas become enabled.

To create the intended workflow we will need to use some external plugins.  To load these plugins we will use the Plugin Manager tool.  The Plugin Manager tool can be found under the Tools menu.  Use the Plugin Manager to add the directory location of the MAP plugins. After confirming the changes to the Plugin Manager you should see a few new additions to the Step box. 

Creating the Workflow
=====================

Drag the steps `Image Source`, `Data Store` and `Segmentation` onto the workflow canvas.  All the steps will show a red cog this indicates that the step needs to be configured.  To configure a step we can right click on it to bring up a context menu and then from this menu select the configure option.


Configuring the Image Source Step
=================================

The Image Source step requires a location.  This location contains the images to import.  The location may be a directory on the local hard disk or a workspace on PMR.  Here we will show how to configure the Image Source step with images that have been stored in a workspace on PMR.

First each step requires a unique id.  This id is used to create a directory under the workflow project directory.  The step directory is used to hold input or output data, the step configuration information and any annotations XXXX.

Next change to the PMR tab and we will see an ellipses button for bringing up the PMR tool dialog.  

Physiome Model Repository (PMR) Tool
------------------------------------

The PMR tool uses webservices to communicate between itself (the consumer) and the PMR website (the server).  Using this tool we can search for and find suitable resources on PMR.

The PMR website uses OAuth to authenticate a consumer and determine consumer access privileges.  Here we will discuss the parts of OAuth that are relevant to getting you (the user) able to access resources on PMR.

In OAuth we have three players the server, the consumer and the user.  The server is providing a service that the consumer wishes to use.  It is up to the user to allow the consumer access to the servers resources and set the level of access to the resource.  For the the consumer to access privileged information of the user stored on the server the user must register the consumer with the server, this is done by the user giving the consumer a temporary access token.  This temporary access token is then used by the consumer to finalise the transaction and acquire a permanent access token.  The user can deny the consumer access at anytime by logging into the server and revoking the permanent access token.

If you want the PMR tool to have access to privileged information (your non-public workspaces stored on PMR) you will need to register the PMR tool with the PMR website.  We do this by clicking on the `register` link as shown in the figure below.  This does two things: it shows the Application Authorisation dialog; opens a webbrowser at the PMR website.  [If you are not logged on at the PMR website you will need to do so now to continue, instructions on obtaining a PMR account are availble here XXXXX].  On the PMR website you are asked to either accept or deny access to the PMR tool.  If you allow access then the website will display a temporary access token that you will need to copy and paste into the Application Authorisation dialog so that the PMR tool can get the permanent access token.

.. figure:: /MAP/feature-demonstration/images/PMRTool_1.png
   :align: center

  


MAP is not setup to work with streamed resources so we must download the workspace from PMR.

