.. _OpenCOR-pluginapproach:

===============
Plugin approach
===============

OpenCOR is a plugin-based application. This means that if no plugins are selected, then OpenCOR can do :ref:`next to nothing <OpenCOR-gui>`.

As can be seen by opening the Plugins dialog box (by selecting the ``Tools`` | ``Plugins...`` menu) and by unselecting ``Show only selectable plugins`` (if necessary), OpenCOR supports different types of plugins (Organisation, Editing, Simulation, Miscellaneous, API and Third-party; see below):

.. image:: /OpenCOR/images/PluginApproachScreenshot01.png
    :align: center
    :width: 360px
    :height: 353px
    :alt: Plugins window

You can select which plugins you want to use. However, plugins which are needed by other plugins (e.g. the Core plugin is needed by the :ref:`CellML model repository <OpenCOR-cellmlmodelrepositoryplugin>` plugin) cannot be directly selected. Instead, they will be automatically selected if and only if they are needed by at least one other plugin.

Most of the selectable plugins come with some kind of a :ref:`GUI <OpenCOR-gui>`:

* **Dockable window:** such a plugin (e.g. the :ref:`CellML model repository <OpenCOR-cellmlmodelrepositoryplugin>` and :ref:`help <OpenCOR-helpplugin>` plugins) can be docked around the central area, undocked or hidden, as illustrated :ref:`here <OpenCOR-gui>`.
* **View window:** such a plugin (e.g. the :ref:`CellML annotation view <OpenCOR-cellmlannotationviewplugin>` and :ref:`single cell view <OpenCOR-singlecellviewplugin>` plugins) is used to interact with a file, be it to edit it, simulate it or analyse it.

Organisation
------------

Organisation plugins are used to search, open, organise, etc. your files:

* **CellMLModelRepository:** a plugin to access the `CellML model repository <http://models.cellml.org/>`_.
* **FileBrowser:** a plugin to access your local files.
* **FileOrganiser:** a plugin to virtually organise your files.

Editing
-------

Editing plugins are used to edit part or all of your files using one of several possible views:

* **CellMLAnnotationView:** a plugin to annotate `CellML <http://www.cellml.org/>`_ files.

There are also some non-selectable Editing plugins:

* **CoreEditing:** the core editing plugin.
* **CoreCellMLEditing:** the core `CellML <http://www.cellml.org/>`_ editing plugin.

Simulation
----------

Simulation plugins are used to simulate your files:

* **CVODESolver:** a plugin which uses `CVODE <http://computation.llnl.gov/casc/sundials/description/description.html#descr_cvode>`_ to solve ODEs.
* **ForwardEulerSolver:** a plugin which implements the `Forward Euler method <http://en.wikipedia.org/wiki/Euler_method>`_ to solve ODEs.
* **FourthOrderRungeKuttaSolver:** a plugin which implements the fourth-order `Runge-Kutta method <http://en.wikipedia.org/wiki/Runge-Kutta_methods>`_ to solve ODEs.
* **HeunSolver:** a plugin which implements the `Heun method <http://en.wikipedia.org/wiki/Heun's_method>`_ to solve ODEs.
* **MidpointSolver:** a plugin which implements the `Midpoint method <http://en.wikipedia.org/wiki/Midpoint_method>`_ to solve ODEs.
* **IDASolver:** a plugin which uses `IDA <http://computation.llnl.gov/casc/sundials/description/description.html#descr_ida>`_ to solve DAEs.
* **KINSOLSolver:** a plugin which uses `KINSOL <http://computation.llnl.gov/casc/sundials/description/description.html#descr_kinsol>`_ to solve non-linear algebraic systems.
* **SecondOrderRungeKuttaSolver:** a plugin which implements the second-order `Runge-Kutta method <http://en.wikipedia.org/wiki/Runge-Kutta_methods>`_ to solve ODEs.
* **SingleCellView:** a plugin to run single cell simulations.

There is also a non-selectable Simulation plugin:

* **CoreSolver:** the core solver plugin.

Miscellaneous
-------------

Miscellaneous plugins are used for various purposes:

* **Help:** a plugin to provide help.

There are also some non-selectable Miscellaneous plugins:

* **Core:** the core plugin.
* **Compiler:** a plugin to support code compilation.
* **CellMLSupport:** a plugin to support `CellML <http://www.cellml.org/>`_.
* **CellMLTools:** a plugin to access various `CellML <http://www.cellml.org/>`_-related tools.

API
---

(Non-selectable) API plugins are used to provide access to external APIs:

* **CellMLAPI:** a plugin to access the `CellML API <http://cellml-api.sourceforge.net/>`_.

Third-party
-----------

(Non-selectable) third-party plugins are used to provide access to third-party libraries:

* **LLVM:** a plugin to access `LLVM <http://www.llvm.org/>`_ (as well as `Clang <http://clang.llvm.org/>`_).
* **SUNDIALS:** a plugin to access CVODE, IDA and KINSOL from the `SUNDIALS <http://computation.llnl.gov/casc/sundials/description/description.html>`_ library.
* **Qwt:** a plugin to access `Qwt <http://qwt.sourceforge.net/>`_.
