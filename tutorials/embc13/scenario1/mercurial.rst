
Working with the repository using Mercurial
===========================================

.. _teaching instance: http://teaching.physiomeproject.org

This part of the tutorial will teach you how to create a :term:`workspace` in the repository, :term:`clone` the workspace from the model repository using a :term:`Mercurial` client, add content to the workspace, and then push the cloned workspace to the repository.

Registering an account and logging in
-------------------------------------

First, navigate to the `teaching instance`_ of the Physiome Model Repository at `<http://teaching.physiomeproject.org/>`_.

.. include:: /PMR/PMR-teaching-instance-warning.rst

In order to make changes to models in the repository, you must first register for an account. For this, go to the `main repository site <http://models.physiomeproject.org/>`_, click on the *Register* link near the top right corner, and provide both a username and password. Once registered, go back to the `teaching repository <http://teaching.physiomeproject.org/>`_ site and log in to it by clicking on the *Log in* link (also near the top right corner). Your account has the appropriate access privileges so that you can push any changes you have made to a model back into the repository.

.. note::
   Your username and password are also the credentials you use to interact with the repository via Mercurial.

Once logged in to the repository, you will notice that there are a couple of new links in the navigation bar (*My Workspaces* and *Documentation*). The *My Worskpaces* link is where all the workspaces you create later on will be listed. The *Log in* link is also replaced by your username and a *Log out* link (which you can access by clicking on your username).

Mercurial username configuration
--------------------------------

.. important::
   **Username setup for Mercurial**

   Since you are about to make changes, your name needs to be recorded as part of the workspace revision history. When you commit your changes using Mercurial, it is initially "offline" and independent of the central PMR2 instance.  This means that you have to set-up your username for the Mercurial client software, even though you have registered a username on the PMR2 site.

   You only need to do this once. The MAP PMR tool will help complete these details for you automatically, but it is a good idea to ensure sensible default values are configured, just in case.

**Steps for TortoiseHg:**

* Right click on any file or folder in Windows Explorer, and select :menuselection:`TortoiseHg --> Global Settings`.
* Select *Commit* and then enter your name followed by your e-mail address in "angle brackets" (i.e. less-than "<" and greater-than ">").  Actually, you can enter anything you want here, but this is the accepted best practice as your email address provides a globally unique identifier.  Note that this information becomes visible publicly if the PMR2 instance that you push your changes to is public.

**Steps for command line:**

* Edit the config text file:
   * For per repository settings, the file in the repository: ``<repo>\.hg\hgrc``
   * System-wide settings for Linux / OS X: ``~/.hgrc``
   * System-wide settings for Windows: ``%USERPROFILE%\mercurial.ini``

* Add the following entry::

   [ui]
   username = Firstname Lastname <firstname.lastname@example.net>

