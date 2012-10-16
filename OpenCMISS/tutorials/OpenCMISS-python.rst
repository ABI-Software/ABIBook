.. _OpenCMISS-python:

.. highlight:: python

===========================
Using OpenCMISS from Python
===========================

In this tutorial we will walk through how to solve Laplace's equation on
a 2D geometry using the Python bindings to OpenCMISS.

Getting Started
---------------

The Python code given here follows the `Python Laplace example`_
found in the OpenCMISS examples repository. You can run the code
interactively by entering it directly into the Python interpreter,
which can be started by running ``python``.
Alternatively you can enter the code into a text file with a .py
extension and run it using the python command, eg::

    python LaplaceExample.py

.. _Python Laplace example: https://github.com/OpenCMISS/examples/blob/master/ClassicalField/Laplace/Laplace/Python/LaplaceExample.py

In order to use OpenCMISS we have to first import the ``CMISS`` module from
the ``opencmiss`` package::

    from opencmiss import CMISS

Assuming OpenCMISS has been correctly built with the Python bindings
by following the instructions in the `programmer documentation`_,
we can now access all the OpenCMISS functions, classes and constants under
the ``CMISS`` namespace.

.. _programmer documentation: http://cmiss.bioeng.auckland.ac.nz/OpenCMISS/doc/programmer/

Create a Coordinate System
--------------------------

First we construct a :ref:`coordinate system <OpenCMISS-coordinatesystems>`
that will be used to describe the geometry in our problem.
The 2D geometry will exist in a 3D space, so we
need a 3D coordinate system.

When creating an object in OpenCMISS there are at least three steps.
First we initialise the object::

    coordinateSystem = CMISS.CoordinateSystem()

This creates a thin wrapper that just points to the actual coordinate
system used internally by OpenCMISS, and initially the pointer is null.
Trying to use the coordinate system now would raise an exception.
To actually construct a coordinate system we call the ``CreateStart``
method and pass it a user number.
The user number must be unique between objects of the same type and
can be used to identify the coordinate system later.
Most OpenCMISS classes require a user number when creating them,
and many also require additional parameters to the ``CreateStart`` method::

    coordinateSystemUserNumber = 1
    coordinateSystem.CreateStart(coordinateSystemUserNumber)

We can now optionally set any properties on the object.
We will set the dimension so that the coordinate system is 3D::

    coordinateSystem.dimension = 3

And finally, we finish creating the coordinate system::

    coordinateSystem.CreateFinish()

Create a Region
---------------

Next we create a :ref:`region <OpenCMISS-regions>` that our fields will be defined on
and tell it to use the 3D coordinate system we created previously.
The ``CreateStart`` method for a region requires another region as a parameter.
We use the world region that is created by default so that our region
is a subregion of the world region.
We can also give the region a label::

    regionUserNumber = 1
    region = CMISS.Region()
    region.CreateStart(regionUserNumber, CMISS.WorldRegion)
    region.label = "LaplaceRegion"
    region.coordinateSystem = coordinateSystem
    region.CreateFinish()

Create a Basis
--------------

The finite element description of our fields requires a
:ref:`basis function <OpenCMISS-basisfunctions>` to interpolate field values
over elements, so we create a 2D basis with linear Lagrange interpolation
in both xi directions::

    basisUserNumber = 1
    basis = CMISS.Basis()
    basis.CreateStart(basisUserNumber)
    basis.type = CMISS.BasisTypes.LAGRANGE_HERMITE_TP
    basis.numberOfXi = 2
    basis.interpolationXi = [
        CMISS.BasisInterpolationSpecifications.LINEAR_LAGRANGE,
        CMISS.BasisInterpolationSpecifications.LINEAR_LAGRANGE,
    ]
    basis.quadratureNumberOfGaussXi = [2, 2]
    basis.CreateFinish()

When we set the basis type we select a value from the ``BasisTypes`` enum.
To get a list of possible basis types and interpolation types you can
use the ``help`` function in the python interpreter::

    help(CMISS.BasisTypes)
    help(CMISS.BasisInterpolationSpecifications)

Similarly, you can see what methods and properties are available for the
various CMISS classes and get help information for these::

    help(CMISS.Basis)
    help(CMISS.Basis.CreateStart)
    help(CMISS.Basis.interpolationXi)

Create a Decomposed Mesh
------------------------

In order to define a simple 2D geometry for our problem we can use
one of OpenCMISS's inbuilt generated meshes. We will create a 2D,
rectangular mesh with 10 elements in both the x and y directions
and tell it to use the basis we created previously::

    generatedMeshUserNumber = 1
    numberGlobalXElements = 10
    numberGlobalYElements = 10
    width = 1.0
    length = 1.0

    generatedMesh = CMISS.GeneratedMesh()
    generatedMesh.CreateStart(generatedMeshUserNumber, region)
    generatedMesh.type = CMISS.GeneratedMeshTypes.REGULAR
    generatedMesh.basis = [basis]
    generatedMesh.extent = [width, length, 0.0]
    generatedMesh.numberOfElements = [
        numberGlobalXElements,
        numberGlobalYElements]

When setting the ``basis`` property, we assign a list of
bases as we might want to construct a mesh with multiple
components using different interpolation schemes.

The generated mesh is not itself a mesh, but is used to create
a mesh. We construct the :ref:`mesh <OpenCMISS-regions-meshes>`
when we call the ``CreateFinish`` method of the generated mesh
and pass in the mesh to generate::

    meshUserNumber = 1
    mesh = CMISS.Mesh()
    generatedMesh.CreateFinish(meshUserNumber, mesh)

Here we have initialised a mesh but not called ``CreateStart``
or ``CreateFinish``, instead the mesh creation is done
when finishing the creation of the generated mesh.

Because OpenCMISS can solve problems on multiple computational
nodes, it must work with a :ref:`decomposed mesh <OpenCMISS-regions-decompositions>`.
We now decompose our mesh by getting the number of computational nodes
and creating a decomposition with that number of domains::

    decompositionUserNumber = 1
    decomposition = CMISS.Decomposition()
    decomposition.CreateStart(decompositionUserNumber, mesh)
    decomposition.type = CMISS.DecompositionTypes.CALCULATED
    decomposition.numberOfDomains = CMISS.ComputationalNumberOfNodesGet()
    decomposition.CreateFinish()

Note that even when we have just one computational node, OpenCMISS still
needs to work with a decomposed mesh, which will have one domain.

Defining Geometry
-----------------

Now that we have a decomposed mesh, we can begin defining the
:ref:`fields <OpenCMISS-regions-fields>` we need on it.
First we will create a geometric field to define our problem geometry::

    geometricFieldUserNumber = 1
    geometricField = CMISS.Field()
    geometricField.CreateStart(geometricFieldUserNumber, region)
    geometricField.meshDecomposition = decomposition
    geometricField.ComponentMeshComponentSet(CMISS.FieldVariableTypes.U, 1, 1)
    geometricField.ComponentMeshComponentSet(CMISS.FieldVariableTypes.U, 2, 1)
    geometricField.ComponentMeshComponentSet(CMISS.FieldVariableTypes.U, 3, 1)
    geometricField.CreateFinish()

The call to the ``ComponentMeshComponentSet`` method is not actually required
here as all field components will default to use the first mesh component, but
if we have defined a mesh that has multiple components (that use different interpolation
schemes) then different field components can use different mesh components.
For example, in a finite elasticity problem we could define our geometry using
quadratic Lagrange interpolation, and the hydrostatic pressure using linear Lagrange
interpolation.

We have created a field but all the field component values are currently set to zero.
We can define the geometry using the generated mesh we created earlier::

    generatedMesh.GeometricParametersCalculate(geometricField)

Setting up Equations
--------------------

Now we have a geometric field we can construct an
:ref:`equations set <OpenCMISS-regions-equations_sets>`.
This defines the set of equations that we wish to solve in our
problem on this region.
The specific equation set we are solving is defined by
the fourth, fifth and sixth parameters to the ``CreateStart``
method. These are the equations set class, type and subtype
respectively. In this example we are solving the standard Laplace
equation which is a member of the classical field equations set
class and the Laplace equation type.
When we create an equations set we also have to create an
equations set field, however, this is only used to identify
multiple equations sets of the same type on a region
so we will not use it::

    equationsSetUserNumber = 1
    equationsSetFieldUserNumber = 2
    equationsSetField = CMISS.Field()
    equationsSet = CMISS.EquationsSet()
    equationsSet.CreateStart(equationsSetUserNumber, region, geometricField,
            CMISS.EquationsSetClasses.CLASSICAL_FIELD,
            CMISS.EquationsSetTypes.LAPLACE_EQUATION,
            CMISS.EquationsSetSubtypes.STANDARD_LAPLACE,
            equationsSetFieldUserNumber, equationsSetField)
    equationsSet.CreateFinish()

Now we use our equations set to create a dependent field.
This stores the solution to our equations::

    dependentFieldUserNumber = 3
    dependentField = CMISS.Field()
    equationsSet.DependentCreateStart(dependentFieldUserNumber, dependentField)
    equationsSet.DependentCreateFinish()

We haven't used the ``Field.CreateStart`` method to construct
the dependent field but have had it automatically constructed by
the equations set.

We can initialise our solution with a value we think will
be close to the final solution. A field in OpenCMISS can contain multiple
:ref:`field variables <OpenCMISS-regions-field_variable>`,
and each field variable can have multiple
:ref:`components <OpenCMISS-regions-field_variable_component>`.
For the standard Laplace equation, the dependent field only has a ``U`` variable
which has one component. Field variables can also have different field
:ref:`parameter sets <OpenCMISS-regions-parameter_set>`,
for example we can store values at a previous time step in dynamic problems.
In this example we are only interested in the ``VALUES`` parameter set::

    componentNumber = 1
    initialValue = 0.5
    dependentField.ComponentValuesInitialiseDP(
        CMISS.FieldVariableTypes.U,
        CMISS.FieldParameterSetTypes.VALUES,
        componentNumber, initialValue)

Once the equations set is defined, we create the
:ref:`equations <OpenCMISS-regions-equations>`
that use our fields to construct equations matrices and vectors.
We will use sparse matrices to store the equations and
enable matrix output when assembling the equations::

    equations = CMISS.Equations()
    equationsSet.EquationsCreateStart(equations)
    equations.sparsityType = CMISS.EquationsSparsityTypes.SPARSE
    equations.outputType = CMISS.EquationsOutputTypes.MATRIX
    equationsSet.EquationsCreateFinish()

Defining the Problem
--------------------

Now that we have defined all the equations we will need we can create
our :ref:`problem <OpenCMISS-problems>` to solve.
We create a standard Laplace problem,
which is a member of the classical field problem class and
Laplace equation problem type::

    problemUserNumber = 1
    problem = CMISS.Problem()
    problem.CreateStart(problemUserNumber)
    problem.SpecificationSet(CMISS.ProblemClasses.CLASSICAL_FIELD,
        CMISS.ProblemTypes.LAPLACE_EQUATION,
        CMISS.ProblemSubTypes.STANDARD_LAPLACE)
    problem.CreateFinish()

The problem type defines a :ref:`control loop <OpenCMISS-problems-control_loop>`
structure that is used when solving the problem.
We may have multiple control loops with nested sub loops,
and control loops can have different types,
for example load incremented loops or time loops for dynamic problems.
In this example a simple, single iteration loop is created without any sub loops.
If we wanted to access the control loop and modify
it we would use the ``problem.ControlLoopGet`` method before
finishing the creation of the control loops, but we will just
leave it with the default configuration::

    problem.ControlLoopCreateStart()
    problem.ControlLoopCreateFinish()

Configuring Solvers
-------------------

After defining the problem structure we can create the
:ref:`solvers <OpenCMISS-problems-solvers>` that
will be run to actually solve our problem.
The problem type defines the solvers to be set up
so we call ``problem.SolversCreatStart`` to create the solvers and
then we can access the solvers to modify their properties::

    solver = CMISS.Solver()
    problem.SolversCreateStart()
    problem.SolverGet([CMISS.ControlLoopIdentifiers.NODE], 1, solver)
    solver.outputType = CMISS.SolverOutputTypes.SOLVER
    solver.linearType = CMISS.LinearSolverTypes.ITERATIVE
    solver.linearIterativeAbsoluteTolerance = 1.0e-10
    solver.linearIterativeRelativeTolerance = 1.0e-10
    problem.SolversCreateFinish()

Note that we initialised a solver but didn't create it directly
by calling its ``CreateStart`` method,
it was created with the call to ``SolversCreateStart`` and then we obtain
it with the call to ``SolverGet``. If we look at the help for the
``SolverGet`` method we see it takes three parameters:

controlLoopIdentifiers
    A list of integers used to identify the control loop to get a solver for.
    This always starts with the root control loop, given by ``CMISS.ControlLoopIdentifiers.NODE``.
    In this example we only have the one control loop and no sub loops.

solverIndex
    The index of the solver to get, as a control loop may have multiple solvers.
    In this case there is only one solver in our root control loop.

solver
    An initialised solver object that hasn't been created yet, and on return
    it will be the solver that we asked for.

Once we've obtained the solver we then set various properties before
finishing the creation of all the problem solvers.

After defining our solver we can create the equations for the solver
to solve by adding our equations sets to the solver equations.
In this example we have just one equations set to add but for coupled
problems we may have multiple equations sets in the solver equations.
We also tell OpenCMISS to use sparse matrices to store our solver equations::

    solverEquations = CMISS.SolverEquations()
    problem.SolverEquationsCreateStart()
    solver.SolverEquationsGet(solverEquations)
    solverEquations.sparsityType = CMISS.SolverEquationsSparsityTypes.SPARSE
    equationsSetIndex = solverEquations.EquationsSetAdd(equationsSet)
    problem.SolverEquationsCreateFinish()

Setting Boundary Conditions
---------------------------

The final step in configuring the problem is to define the boundary
conditions to be satisfied. We will set the dependent field value
at the first node to be zero, and at the last node to be 1.0. These
nodes will correspond to opposite corners in our geometry.
Because OpenCMISS can solve our problem on multiple computational nodes
where each computational node does not necessarily know about all nodes
in our mesh, we must first check that the node we are setting the
boundary condition at is in our computational node domain::

    nodes = CMISS.Nodes()
    region.NodesGet(nodes)
    firstNodeNumber = 1
    lastNodeNumber = nodes.numberOfNodes
    firstNodeDomain = decomposition.NodeDomainGet(firstNodeNumber, 1)
    lastNodeDomain = decomposition.NodeDomainGet(lastNodeNumber, 1)
    computationalNodeNumber = CMISS.ComputationalNodeNumberGet()

    boundaryConditions = CMISS.BoundaryConditions()
    solverEquations.BoundaryConditionsCreateStart(boundaryConditions)
    if firstNodeDomain == computationalNodeNumber:
        boundaryConditions.SetNode(
            dependentField, CMISS.FieldVariableTypes.U,
            1, 1, firstNodeNumber, 1,
            CMISS.BoundaryConditionsTypes.FIXED, 0.0)
    if lastNodeDomain == computationalNodeNumber:
        boundaryConditions.SetNode(
            dependentField, CMISS.FieldVariableTypes.U,
            1, 1, lastNodeNumber, 1,
            CMISS.BoundaryConditionsTypes.FIXED, 1.0)
    solverEquations.BoundaryConditionsCreateFinish()

When setting a boundary condition at a node we can use either the ``AddNode``
method or the ``SetNode`` method. Using ``AddNode`` will add the value
we provide to the current field value and set this as the boundary condition value,
but here we want to directly specify the value so we use the ``SetNode`` method.

The arguments to the ``SetNode`` method are the field, field variable type,
node version number, node user number, node derivative number, field component number,
boundary condition type and boundary condition value.
The version and derivative numbers are one as we aren't using versions and we are
setting field values rather than derivative values.
We can also only set derivative boundary conditions when using a Hermite basis type.
There are a wide number of boundary condition types that can be set but
many are only available for certain equation set types and in this example we
simply want to fix the field value.

When ``solverEquations.BoundaryConditionsCreateFinish()`` is called
OpenCMISS will construct the solver matrices and vectors.

Solving
-------

After our problem solver equations have been fully defined we are now ready
to solve our problem. When we call the ``Solve`` method of the problem it will
loop over the control loops and control loop solvers to solve our problem::

    problem.Solve()

Exporting the Solution
----------------------

Once the problem has been solved, the dependent field contains the solution
to our problem. We can then export the dependent and geometric fields to a
FieldML file so that we can visualise the solution using cmgui.
We will export the geometric and dependent field values to
a ``LaplaceExample.xml`` file.
Separate plain text data files will also be created::

    baseName = "laplace"
    dataFormat = "PLAIN_TEXT"
    fml = CMISS.FieldMLIO()
    fml.OutputCreate(mesh, "", baseName, dataFormat)
    fml.OutputAddFieldNoType(
        baseName + ".geometric", dataFormat, geometricField,
        CMISS.FieldVariableTypes.U, CMISS.FieldParameterSetTypes.VALUES)
    fml.OutputAddFieldNoType(
        baseName + ".phi", dataFormat, dependentField,
        CMISS.FieldVariableTypes.U, CMISS.FieldParameterSetTypes.VALUES)
    fml.OutputWrite("LaplaceExample.xml")
    fml.Finalise()
