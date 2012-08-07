.. _OpenCMISS-basisfunctions

Basis Functions
===============

Basis functions are the key item to specify the field approximation/interpolation and the linking of nodes and elements to form a mesh. Currently, it has two types: Lagrange-Hermite tensor product and Simplex. Lagrange-Hermite tensor product can be further divided into linear to cubic lagrange, cubic and quadratic hermite. It can be arbitrarily collapsed (two or more nodes in the same location) in any one direction or in any two directions to give a degenerate basis. Simplex basic functions could contain line, triangular and tetrahedral elements. It could be linear, quadratic or cubic. Arbitrary Gaussian quadrature can integrate from 1st to 5th order (3rd order for lines at the moment). Can only have the same order in each direction at the moment. Specifying a basis function automatically generates all necessary line and face basis functions as sub-bases of the basis function.

Basis function has the following attributes:

* User number
* Global number
* Family number
* Finished tag
* Type
* Is Hermite
* Number of XI
* Number of XI coordinates
* ...

