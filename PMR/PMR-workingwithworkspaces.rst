.. _PMR-workingwithworkspaces:

===========================
Working with PMR workspaces
===========================

.. sectionauthor:: David Nickerson

.. _teaching instance: http://teaching.physiomeproject.org/

All models in the Physiome model repository exist in :term:`workspaces`, which are `Mercurial <http://mercurial.selenic.com/>`_ repositories that can be used to store any kind of file. Mercurial is a distributed version control system (DVCS).

In order to create your own workspaces, you will first need to create a repository account by registering at `models.physiomeproject.org <http://models.physiomeproject.org>`_. Near the top right of the repository page there will be links labelled *Log in* and *Register*. Click on the register link, and follow the instructions.

Workspaces in the physiome model repository are permanent once they are created. There is a `teaching instance`_ of the model repository which may be used for *experimenting* with PMR without worrying about creating permanent workspaces that might have errors in them. Users accounts from the main PMR instance will be copied to the `teaching instance`_ each time it is recreated, but users may register for an account just on the `teaching instance`_ if they prefer. Such accounts will need to be recreated each time the teaching instance is recreated.

.. include:: PMR-teaching-instance-warning.rst  

.. _PMR-creatingNewWorkspace:

Creating a new workspace
========================

Once a user is logged into an instance of PMR, they will be presented with a :guilabel:`My Workspaces` link in the top toolbar, as shown below:

.. figure:: /PMR/images/my-workspaces.png
   :align: center
   :width: 80%

The first paragraph includes a link to your dashboard to add a new workspace, shown below:

.. figure:: /PMR/images/add-workspace-dashboard.png
   :align: center
   :width: 80%
   
Currently :term:`Mercurial` is the only avialable option for the storage method for a new workspace, but this may be expanded to include other storage methods in future. A workspace should be given a meaningful title and a brief description to help locate the workspace using the repository search. Both these fields can be edited later, so don't worry if you don't get it perfect the first time.

Clicking the :guilabel:`Add` button with then create the workspace, which will initially be empty, as shown below:

.. figure:: /PMR/images/new-workspace.png
   :align: center
   :width: 80%
   
In the figure above, the URI of the newly created workspace has been highlighted. This is the URI that will be used when operating on the workspace using Mercurial. 

Uploading files to your workspace
=================================

* Clone new workspace
* Add files to cloned workspace
* Commit files (Hg)
* Push to repository (Hg)

Alternatively, use OpenCOR.

.. todo::
   Work on this section?