.. _ABIBook-tutorial-embc13:

==========================================
Developing the Virtual Physiological Human
==========================================

This tutorial will demonstrate tools, techniques and best practices that aid scientists in the development and application of computational models and simulation experiments in their work toward the creation of a virtual physiological human. The Physiome Model Repository (PMR) provides a framework for the storage, curation and exchange of data. By using standards suitable to their data, scientists maximise their ability to reuse existing knowledge and enable others to make use of their achievements in novel work. Annotations ensure scientists are able to find existing data and are also able to correctly interpret and apply the data in their own work. These tutorials are designed to help demonstrate and promote practices which will aid attendees in their own work. Attendees are encouraged to raise issues specifically related to their work with the tutors.

Documentation for the software used in this tutorial is available `online <https://abibook.readthedocs.org/en/EMBC-2013-tutorial/>`_, including the most recent version of `this tutorial itself <http://abibook.readthedocs.org/en/EMBC-2013-tutorial/tutorials/embc13/index.html>`_. This tutorial guides the particpant through three common computational modelling scenarios faced by scientists working toward the virtual physiologial human. We use these scenarios to achieve scientific outputs using the covered tools tools and demonstrating practices we believe will help ensure reproducible and reusable science. Each of the scenarios listed below should be worked through in order and in each scenario we provide examples using either :ref:`OpenCOR <OpenCOR-index>` or the :ref:`MAP <MAP-feature-demonstration>` workflow tool.

When interacting directly with :term:`Mercurial`, this tutorial demonstrates how to work with the Physiome model repository using `TortoiseHg <http://tortoisehg.bitbucket.org/>`_, which provides a Windows explorer integrated system for working with Mercurial repositories.

::

  Brief mention of the equivalent command line versions of the TortoiseHg
  actions will also be mentioned, so that these ideas can also be used without
  a graphical client, and on Linux or OS X and similar systems. These will be denoted
  by boxes like this.

This tutorial requires you to have:

* A Mercurial client such as `TortoiseHg <http://tortoisehg.bitbucket.org/>`_ or `Mercurial <http://mercurial.selenic.com/>`_ installed;
* The :ref:`OpenCOR <OpenCOR-downloadLinks>` CellML modelling environment and/or the :ref:`MAP <MAP-install-setup>` workflow tool installed;
* A text editor such as `Notepad++ <http://notepad-plus-plus.org/>`_ or `gedit <http://projects.gnome.org/gedit/>`_

.. toctree::
   :maxdepth: 5

   scenario1/index
   scenario2/index
   scenario3/index
