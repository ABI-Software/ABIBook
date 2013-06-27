.. _PMR-glossary:

============
PMR glossary
============

.. glossary::
   :sorted:

   Clone
      Clone is a Mercurial term that means to make a complete copy of a Mercurial repository. This is done in order to have a local copy of a repository to work in.

   Embedded workspace
   Embedded workspaces
      A Mercurial concept that allows workspaces to be nested within other workspaces.

   Exposure
   Exposures
      A publicly available page that provides access to and information about a specific revision of a workspace. Exposures are used to publish the contents of workspaces at points in time where the model(s) contained are considered to be useful.

      Exposures are created by the PMR software, and offer views appropriate to the type of model being exposed. CellML files for example are presented with options such as code generation and mathematics display, whereas FieldML models might offer a 3D view of the mesh.

   Fork
      A copy of the workspace which includes all the original version history, but is owned by the user who created the fork.

   Synchronize
      Used to pull the contents or changes from other :term:`Mercurial` repositories into a workspace via a URI.

   Workspace
   Workspaces
      A `Mercurial` repository hosted on the Physiome Model Repository. This is essentially a folder or directory in which files are stored, with the added feature of being version controlled by the distributed version control system called `Mercurial <http://mercurial.selenic.com/>`_.

   Mercurial
      `Mercurial <http://mercurial.selenic.com/>`_ is a distributed version control system, used by the Physiome Model Repository software to maintain a history of changes to files in :term:`workspaces`.
