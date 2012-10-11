.. _PMR2-exposing-cellml:

Creating CellML exposures
=========================

CellML models in PMR2 are presented through *exposures*. An exposure is a view of a particular revision of a workspace, and is quite flexible in terms of what it can present. A workspace may contain one or more models, and any number of models may be presented in a single exposure. Exposures generally take the form of some documentation about the model(s), a range of ways of looking at the model(s) or their metadata, and links to download the model(s). 

The example below shows the main exposure page for the Bondarenko *et al.* 2004 workspace. This workspace contains two models, which can be viewed via the **Navigation** pane on the right hand side of the page.

.. figure:: /PMR2/images/PMR2-exposureeg1.png
   :align: center
   
   **Example of an exposure page**

If you click on one of the model navigation links, it will take you to the page for that particular model. Note that most exposures contain a single model.
   
.. figure:: /PMR2/images/PMR2-exposureeg2.png
   :align: center
   
   **Example of a model exposure page**
   
Most of the CellML exposures in the repository are of this type, with a main documentation page containing navigation links to the model or models themselves. The model pages then contain links that enable the user to do things like view the model equations, look at the citation information, or run the model as an interactive session using the OpenCell application.

This tutorial contains instructions on how to create one of these standard CellML exposures, as well as information about how to create other alternative types of exposure.

Creating standard CellML exposures
----------------------------------

..note:: This tutorial assumes that you have logged in to the `model repository`_ and have sufficient privileges in the workspace you wish to expose.

As an exposure is created to present a particular revision of a workspace, the first thing to do is to navigate to the correct revision of the workspace you wish to expose. To do this, first find the workspace - if this is your own workspace, you can click on the **My Workspaces** button in the navigation bar of the repository and find the workspace of interest in the listing displayed.

In my example, I will use a *fork* of the the Beeler Reuter 1977 workspace 






.. _model repository: http://models.cellml.org
