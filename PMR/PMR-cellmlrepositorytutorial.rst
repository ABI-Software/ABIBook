.. _PMR-cellmlrepositorytutorial:

================================
CellML Model Repository tutorial
================================

About this tutorial
===================

The CellML repository is powered by software called Physiome Model Repository (PMR). PMR currently relies on the distributed version control system Mercurial (Hg), which allows the repository to maintain a complete history of all changes made to every file it contains. This tutorial demonstrates how to work with the repository using TortoiseHg, which provides a Windows explorer integrated system for working with Mercurial repositories.

::

  Brief mention of the equivalent command line versions of the TortoiseHg actions will also be mentioned, so that these ideas can also be used without a graphical client, and on Linux and similar systems. These will be denoted by grayed boxes like this.

This tutorial requires you to have:

* A Mercurial client such as TortoiseHg or Mercurial installed
* OpenCell
* A text editor such as Notepad++ or gedit
* User registration on the Physiome model repository site

PMR concepts
============

PMR and the CellML model repository use a certain amount of jargon - some is specific to the repository software, and some is related to distributed version control systems (DVCSs). Below are basic explanations of some of these terms as they apply to the repository.

Workspace
  A container (much like a folder or directory on your computer) to hold the files that make up a model, as well as any other files such as documentation or metadata, etc. In practical terms, each workspace is a Mercurial repository.

Exposure
  An exposure is a publically viewable presentation of a particular revision of a model. An exposure can present one or many files from your workspace, along with documentation and other information about your model.

The Mercurial DVCS has a range of terms that are useful to know, and definitions of these terms can be found in the Mercurial glossary: http://mercurial.selenic.com/wiki/Glossary. 

Working with the repository web interface
=========================================

This part of the tutorial will teach you how to find models in the CellML model repository `(http://models.physiomeproject.org) <http://models.physiomeproject.org>`_, how to view a range of information about those models, and how to download models. The first page in the repository consists of basic navigation, a link to the main model listing, a search box at the top right, and a list of model category links as shown below.

.. figure:: /images/pmr-tut1-mainscreen.png
   :align: center

   The front page of the Physiome model repository.

Model listings
--------------

Clicking on the main model listing or any of the category listings will take you to a page displaying a list of exposed models in that category. Click on electrophysiology for example, and a list of over 100 exposed models in that category will be displayed, as shown here.

Clicking on an item in the list will take you to the exposure page for that model.

Searching the repository
------------------------

You can search for the model that you wish to work on by entering a search term in the box at the top right of the page. Many of the models in the repository are named by the first author and publication date of the paper, so good search query might be something like "goldbeter 1991". A list of the results of your search will probably contain both workspaces and exposures - you will need to click on the workspace of the model you wish to work on. Workspaces can be identified because their links are pale blue and have no details line following the clickable link. In the following screenshot, the first two results are workspaces, and the remainder are exposures.

.. figure:: /images/pmr-tut1-searchresults.png
   :align: center

   A search results listing on the CellML repository site.

Click on an exposure result to view information about the model and to get links for downloading or simulating the model. Click on workspaces to see the contents of the model workspace and the revision history of the model.

Working with the repository using Mercurial
===========================================

This part of the tutorial will teach you how to clone a workspace from the model repository using a Mercurial client, create your own workspace, and then push the cloned workspace into your new workspace in the repository. We will be using a *fork* of an existing workspace, which provides you with a personal copy of a workspace that you can edit and push changes to.

Registering an account and logging in
-------------------------------------

First, navigate to the CellML model repository at `http://models.cellml.org <http://models.cellml.org>`_. 

In order to make changes to models in the CellML repository, you must first register for an account. The "Log in" and "Register" links can be found near the top right corner of the page. Your account will have the appropriate access privileges so that you can push any changes you have made to a model back into the repository.

Click on the Register link near the top right, and fill in the registration form. Enter your username and desired password. You can now log in to the repository. This username and password are also the credentials you use to interact with the repository via Mercurial. Note that compared to registering for the real CellML repository, this process is somewhat streamlined for the purposes of this tutorial – normally there is a validation step involved.

Once logged in to the repository, you will notice that there is a new link in the navigation bar, My Workspaces. This is where all the workspaces you create later on will be listed. The Log in and Register links are also replaced by your username and a Log out link.

Mercurial username configuration
--------------------------------

.. important::
   **Username setup for Mercurial**
   
   Since you are about to make changes, your name needs to be recorded as part of the workspace revision history. When commit your changes using Mercurial, it is initially "offline" and independent of the central PMR2 instance.  This means that you have to set-up your username for the Mercurial client software, even though you have registered a username on the PMR2 site.

   You only need to do this once.





