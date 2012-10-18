.. _OpenCMISS-cellml:

.. highlight:: Fortran

.. the above sets the default highlighting to be Fortran, but the code-blocks can override this so that we can have examples in Fortran, C, and Python.


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

The OpenCMISS type for the CellML environment is ``CMISSCellMLType``. As with most OpenCMISS types, a user-number is provided to uniquely identify this CellML environment to the user. The basic creation block is given below. 

.. code-block:: Fortran

  ! declare the user number for the CellML environment we want to create
  INTEGER(CMISSIntg), PARAMETER :: CellMLUserNumber=10
  ! and the actual handle for the CellML environment
  TYPE(CMISSCellMLType) :: CellML
  .
  .
  ! We first initialise the CellML environment
  CALL CMISSCellML_Initialise(CellML,Err)
  ! and then we are able to trigger the start of creation
  CALL CMISSCellML_CreateStart(CellMLUserNumber,Region,CellML,Err)
  
  ! import models
  
  ! flag variables
  
  ! terminate the creation process
  CALL CMISSCellML_CreateFinish(CellML,Err)
  
It is important to note that all required models must be imported and all desired variables flagged before terminating the CellML environment creation process. This is because the create finish method will proceed to make use of OpenCMISS(cellml) to instantiate each of the imported CellML models into executable code, and the generation of that executable code requires all knowledge of the flagged variables.
 
Models are imported into the CellML environment with the code shown below.

.. code-block:: Fortran

  INTEGER(CMISSIntg) :: modelIndex
  
  ! Import the specified model into the CellML environment
  CALL CMISSCellML_ModelImport(CellML,"model.xml",modelIndex,Err)

In this example, the CellML model ``model.xml`` is imported into the CellML environment and on successful return the variable ``modelIndex`` will be set to the index for this specific model in the CellML environment. The CellML model to import is specified by URL, and can be either absolute (e.g., ``http://example.com/coolest/model/ever.xml``) or relative (e.g., ``coolest/model/ever.xml``). If a relative URL is specified, it will be resolved relative to the current working directory (CWD) of the executed application. (It is anticipated that application developers would use their own logic to provide absolute URLs to define CellML models in OpenCMISS.)

Flagging variables
------------------

As mentioned above, all variables of interest in the imported CellML models must be flagged prior to terminating the CellML environment creation process. Variables in CellML models can be flagged as either *known* or *wanted*. Flagging variables in a model will inform OpenCMISS(cellml) that the given variable(s) need to be available for use by OpenCMISS(cm), and hence the executable code generated when the models are instantiated is required to provide this access. The process for flagging variables is shown below.

.. code-block:: Fortran

  ! Flag a variable as known
  CALL CMISSCellML_VariableSetAsKnown(CellML,modelIndex,"fast_sodium_current/g_Na ",Err)
  ! Flag a variable as wanted
  CALL CMISSCellML_VariableSetAsWanted(CellML,modelIndex,"membrane/i_K1",Err)

Details on how to identify specific variables in a CelLML model are given below. The ``modelIndex`` should be the index of the desired model in the CellML environment, as returned by the model import described above.

Flagging a variable as *known* indicates that the OpenCMISS user wants to control the value of the specified variable, thus taking ownership of the variable from the CellML model. Currently, only CONSTANT variables in CellML models can be flagged as known (see the `Variable Evaluation Types`_ in the CellML API documentation). This is typically used when parameters in the CellML model are to have their values defined by OpenCMISS fields.

Flagging a variable as *wanted* indicates that the OpenCMISS user wants to obtain the value of the specified variable from the CellLML model. Currently, CONSTANT, PSEUDOSTATE_VARIABLE, and ALGEBRAIC variables in CellML models can be flagged as wanted ((see the `Variable Evaluation Types`_ in the CellML API documentation). In order to be able to save the state of CellML models during integration steps, all state variables in models are automatically flagged as wanted. Depending on how the CellML model is being applied in the OpenCMISS simulation, variables that are considered CONSTANT by the CelLML API will actually be the variables of interest to the OpenCMISS user - commonly the case for mechanical constitutive relationships where the *wanted* strain energy components are algebraically related to the *known* strain components.

.. _Variable Evaluation Types: http://cellml-api.sourceforge.net/1.12/namespacecellml__services.html#a572d2854ecc95d68471347241a678c8f

Identifying CellML variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When identifying variables from CellML models in OpenCMISS, the convention is to address them with a string consisting of the variable's name and the name of the parent component, as demonstrated below.

.. code-block:: xml

  <model ...>
    .
    .
    <component name="membrane">
      <variable name="i_K1" .../>
      <variable name="i_stimulus" .../>
      .
      .
    </component>
    <component name="temperature">
      <variable name="temperature" units="K" initial_value="310.0" public_interface="out"/>
    </component>
    .
    .
  </model>

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