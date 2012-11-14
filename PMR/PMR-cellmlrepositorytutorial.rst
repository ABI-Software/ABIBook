.. _PMR-cellmlrepositorytutorial:

================================
CellML Model Repository tutorial
================================

About this tutorial
===================

The CellML repository is powered by software called Physiome Model Repository (PMR). PMR currently relies on the distributed version control system Mercurial (Hg), which allows the repository to maintain a complete history of all changes made to every file it contains. This tutorial demonstrates how to work with the repository using TortoiseHg, which provides a Windows explorer integrated system for working with Mercurial repositories.

::

  Brief mention of the equivalent command line versions of the TortoiseHg
  actions will also be mentioned, so that these ideas can also be used without
  a graphical client, and on Linux and similar systems. These will be denoted
  by grayed boxes like this.

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

.. figure:: /PMR/images/PMR-tut1-mainscreen.png
   :align: center

   The front page of the Physiome model repository.

Model listings
--------------

Clicking on the main model listing or any of the category listings will take you to a page displaying a list of exposed models in that category. Click on electrophysiology for example, and a list of over 100 exposed models in that category will be displayed, as shown here.

Clicking on an item in the list will take you to the exposure page for that model.

Searching the repository
------------------------

You can search for the model that you wish to work on by entering a search term in the box at the top right of the page. Many of the models in the repository are named by the first author and publication date of the paper, so good search query might be something like "goldbeter 1991". A list of the results of your search will probably contain both workspaces and exposures - you will need to click on the workspace of the model you wish to work on. Workspaces can be identified because their links are pale blue and have no details line following the clickable link. In the following screenshot, the first two results are workspaces, and the remainder are exposures.

.. figure:: /PMR/images/PMR-tut1-searchresults.png
   :align: center

   A search results listing on the CellML repository site.

Click on an exposure result to view information about the model and to get links for downloading or simulating the model. Click on workspaces to see the contents of the model workspace and the revision history of the model.

Working with the repository using Mercurial
===========================================

This part of the tutorial will teach you how to clone a workspace from the model repository using a Mercurial client, create your own workspace, and then push the cloned workspace into your new workspace in the repository. We will be using a *fork* of an existing workspace, which provides you with a personal copy of a workspace that you can edit and push changes to.

Registering an account and logging in
-------------------------------------

First, navigate to the CellML model repository at `http://models.cellml.org<http://models.cellml.org>`_.

In order to make changes to models in the CellML repository, you must first register for an account. The *Log in* and *Register* links can be found near the top right corner of the page. Your account will have the appropriate access privileges so that you can push any changes you have made to a model back into the repository.

Click on the Register link near the top right, and fill in the registration form. Enter your username and desired password. After completing the email validation step, you can now log in to the repository. 

.. note::
   This username and password are also the credentials you use to interact with the repository via Mercurial.

Once logged in to the repository, you will notice that there is a new link in the navigation bar, My Workspaces. This is where all the workspaces you create later on will be listed. The Log in and Register links are also replaced by your username and a Log out link.

Mercurial username configuration
--------------------------------

.. important::
   **Username setup for Mercurial**
   
   Since you are about to make changes, your name needs to be recorded as part of the workspace revision history. When commit your changes using Mercurial, it is initially "offline" and independent of the central PMR2 instance.  This means that you have to set-up your username for the Mercurial client software, even though you have registered a username on the PMR2 site.

   You only need to do this once.

**Steps for TortoiseHg:**

* Right click on any file or folder in Windows Explorer, and select :menuselection:`TortoiseHg --> Global Settings`.
* Select *Commit* and then enter your name followed by your e-mail address in "angle brackets" (i.e. less-than "<" and greater-than ">").  Actually, you can enter anything you want here, but this is the accepted best practice.  Note that this information becomes visible publicly if the PMR2 instance that you push you changes to is public.

**Steps for command line:**

* Edit the config text file:
   * For per repository settings, the file in the repository: ``<repo>\.hg\hgrc``
   * System-wide settings for Linux: ``%USERPROFILE%\.hgrc``
   * System-wide settings for Windows: ``%USERPROFILE%\mercurial.ini``

* Add the following entry::

   [ui]
   username = Firstname Lastname <firstname.lastname@example.net>

Forking an existing workspace
-----------------------------

.. important::
   It is essential to use a Mercurial client to obtain models from the repository for editing. The Mercurial client is not only able to keep track of all the changes you make (allowing you to back-track if you make any errors), but using a Mercurial client is the only way to add any changes you have made back into the repository.

For this tutorial, we will *fork* an existing workspace. This provides you with a new workspace of your own, containing a copy of all the files in the workspace you forked, including their complete history. This is equivalent pushing the cloned contents of an existing workspace into a new workspace you have created.

Forking a workspace can be done using the Physiome model repository web interface. The first step is to find the workspace you wish to fork. We will use the Beeler, Reuter 1977 workspace which can be found by entering ``beeler reuter`` into the search box at the top right corner of the page. Click on the top result, which will take you to the exposure page for the Beeler Reuter 1977 model.

Now click on the *fork* option in the toolbar, as shown below.

.. figure:: /PMR/images/PMR-fork1.png
   :align: center

You will be asked to create a new ID for the workspace. Typically this is something like the existing workspace name plus initials, some text tag that indicates the purpose of the fork, or some other short addition to the original name. I creaked a fork called ``beeler_reuter_1977_djc``, for example.



**After the fork**

You can now clone your new workspace to your local drive, using the same method as shown before for the Beeler Reuter 1977 workspace. This now completes the process of getting your own full-access copy of the existing Beeler Reuter model for editing.

Making changes to workspace contents
------------------------------------

Your cloned workspace is now ready for you to edit the model file and make a commit each time you want to save the changes you have made. As an example, open the model file in Notepad++ and remove the paragraph which describes validation errors from the documentation section, as shown below:

.. figure:: /PMR/images/PMR-tut1-editcellmlfile.png
   :align: center

Save the file. If you are using TortoiseHg, you will notice that the icon overlay has changed to a red exclamation mark. This indicates that the file now has uncommitted changes. 

Committing changes
------------------

If you are using TortoiseHg, bring up the shell menu for the altered file and select :menuselection:`TortoiseHg --> Hg Commit`. A window will appear showing details of the changes you are about to commit, and prompting for a commit message. Every time you commit changes, you should enter a useful commit message with information about what changes have been made. In this instance, something like "Removed the paragraph about validation errors from the documentation" is appropriate.

Click on the Commit button at the far left of the toolbar. The icon overlay for the file will now change to a green tick, indicating that changes to the file have been committed.

.. figure:: /PMR/images/PMR-tut1-commitchanges.png
   :align: center

**Command line equivalent**::
   hg commit -m "Removed the paragraph about validation errors from the documentation"

Pushing changes to the repository
---------------------------------

Your cloned workspace on your local machine now has a small history of changes which you wish to *push* into the repository.

Right click on your workspace folder in Windows explorer, and select :menuselection:`TortoiseHg --> Hg Synchronize` from the shell menu. This will bring up a window from which you can manage changes to the workspace in the repository. Click on the Push button in the toolbar, and enter your username and password when prompted.

**Command line equivalent** ::
   hg push
   
   

