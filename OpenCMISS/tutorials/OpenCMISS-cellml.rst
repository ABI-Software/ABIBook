.. _OpenCMISS-cellml:

.. highlight:: cellml

=========================
Using CellML in OpenCMISS
=========================

The aim of this tutorial is to give the user a bit of help in using CellML models in OpenCMISS. `OpenCMISS(cellml)`_ is the code that provides the mapping from OpenCMISS(cm) (Fortran) to the `CellML API`_ (C++). The API exposed by the OpenCMISS(cellml) library is then wrapped by the OpenCMISS(cm) API, with documentation available in the OpenCMISS `programmer documentation`_. The programmer documentation provides the reference documentation for the OpenCMISS(cm) routines which are described in this tutorial. The `monodomain example`_ from the OpenCMISS examples repository provides a good demonstration of OpenCMISS+CellML in practice, while the `CellML examples`_ are used to perform functional testing of the OpenCMISS(cellml) library.

.. _OpenCMISS(cellml): https://github.com/OpenCMISS/cellml

.. _CellML API: http://cellml-api.sourceforge.net

.. _programmer documentation: http://cmiss.bioeng.auckland.ac.nz/OpenCMISS/doc/programmer/

.. _monodomain example: https://github.com/OpenCMISS/examples/blob/master/Bioelectrics/Monodomain/src/MonodomainExample.f90

.. _CellML examples: https://github.com/OpenCMISS/examples/blob/master/cellml

Overview
--------

OpenCMISS encapsulates all interaction with CellML models within a *CellML environment*. A CellML environment is specific to a region, but each region may contain zero or more CellML environments. Having created a CellML environment you are then able to import CellML models into the environment. Each CellML environment may import an arbitrary number of CellML models.  [TODO: what is a use-case for multiple CellML environments in a region?]

Variables in CellML models imported into a CellML environment are then able to flagged as *known* or *wanted* as desired by the user. Flagged variables are made available by the CellML environment for mapping to OpenCMISS fields, either for obtaining values from the CellML model (wanted) or setting values in the CellML model (known).

In order for the CellML environment to mange the computation of a CellML model, each environment requires the user to provide several fields suitable for such usage. These are the *models*, *state*, *intermediate*, and *parameters* fields. Typically the user will pass in empty fields and allow the CellML environment to create the fields appropriately.

With all desired fields set-up appropriately, the user then just needs to add their CellML environment(s) to the corresponding solver as part of their control loop set-up when defining the actual problem to solve.

.. the following is a sequence of the common use-cases that we'd expect users to perform.

The CellML environment
----------------------

Create an environment and import models.

Flagging variables
------------------

What is meant by known and wanted; mention that only top-level variables can be addressed; anything else?

Mapping between variables and fields
------------------------------------

More explanation on the process of mapping variables between CellML models and OpenCMISS fields.

CellML fields
-------------

The required fields and what you might want to do with them...

Evaluating CellML fields
------------------------

Do we want to describe how simple algebraic-type evaluation can be done independently of the whole solver/problem/equation set thingy? is that even possible?

Adding CellML models to your Problem set-up
-------------------------------------------

Really need a better title! Explain how CellML environments get added into control loops, etc. so that they get computed along with the rest of the model when performing a simulation.

Miscellaneous utilities
-----------------------

Collect all the other bits and pieces here? these are typically the OpenCMISS(cellml) functions that are used internally by OpenCMISS(cm) but maybe should be (and are?) exposed via the OpenCMISS(cm) API? 