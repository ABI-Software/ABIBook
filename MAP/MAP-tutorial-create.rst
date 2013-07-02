.. _MAP-tutorial-create:

==============================
MAP Tutorial - Create Workflow
==============================

.. sectionauthor:: Hugh Sorby

.. _launchpad project: http://launchpad.net/mapclient
.. _MAP: https://simtk.org/home/map

.. note::
   `MAP`_ is currently under active development, and this document will be updated to reflect any changes to the software or new features that are added. You can follow the development of MAP at the `launchpad project`_.

This document details takes the reader through the process of creating a workflow from existing MAP plugins.  Having a read through the :doc:`MAP-feature-demonstration` is a good way to become familiar with the features of the MAP application.

Getting Started
===============

To get started with MAP we need to create a new workflow.  To do this we use File -> New -> Workflow menu option (Ctrl-N shortcut).  This option will present the user with a directory selection dialog.  Use the dialog to select a directory where the workflow can be saved.  Once we have chosen a directory the step box and workflow canvas will become enabled.

To create a meaningful workflow we will need to use some external plugins.  To load these plugins we will use the Plugin Manager tool.  The Plugin Manager tool can be found under the Tools menu.  Use the Plugin Manager to add the directory location of the MAP plugins. After confirming the changes to the Plugin Manager you should see a few new additions to the Step box. 

Creating the Workflow
=====================

To create a workflow we use Drag 'n' Drop to drag steps from the Step box and drop the step onto the workflow canvas.  When steps are first dropped onto the canvas they show a red cog icon to indicate that the step is not configured.  At a minimum a step requires an identifier to be set before it can be used.
 
Drag the steps `Image Source`, `Data Store` and `Segmentation` onto the workflow canvas.  All the steps will show a red cog this indicates that the step needs to be configured.  To configure a step we can right click on it to bring up a context menu and then from this menu select the configure option.


Configuring the Image Source Step
---------------------------------

The Image Source step requires a location.  This location contains the images to import.  The location may be a directory on the local hard disk or a workspace on PMR.  Here we will show how to configure the Image Source step with images that have been stored in a workspace on PMR.

First each step requires a unique id.  This id is used to create a directory under the workflow project directory.  The step directory is used to hold input or output data, the step configuration information and any annotations.

Next change to the PMR tab and we will see an ellipses button for bringing up the PMR tool dialog.

MAP is not setup to work with streamed resources so we must download the workspace from PMR.

