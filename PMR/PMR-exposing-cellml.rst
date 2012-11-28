.. _PMR-exposing-cellml:

=========================
Creating CellML exposures
=========================

CellML models in PMR are presented through *exposures*. An :term:`exposure` is a view of a particular revision of a workspace, and is quite flexible in terms of what it can present. A workspace may contain one or more models, and any number of models may be presented in a single exposure. Exposures generally take the form of some documentation about the model(s), a range of ways of looking at the model(s) or their metadata, and links to download the model(s). 

The example below shows the main exposure page for the Bondarenko *et al.* 2004 workspace. This workspace contains two models, which can be viewed via the **Navigation** pane on the right hand side of the page.

.. figure:: /PMR/images/PMR-exposureeg1.png
   :align: center
   
   **Example of an exposure page**

If you click on one of the model navigation links, it will take you to the page for that particular model. Note that most exposures contain a single model.
   
.. figure:: /PMR/images/PMR-exposureeg2.png
   :align: center
   
   **Example of a model exposure page**
   
Most of the CellML exposures in the repository are currently of this type, with a main documentation page containing navigation links to the model or models themselves. The model pages then contain links that enable the user to do things like view the model equations, look at the citation information, or run the model as an interactive session using the OpenCell application.

This tutorial contains instructions on how to create one of these standard CellML exposures, as well as information about how to create other alternative types of exposure.

Creating standard CellML exposures
==================================

.. note:: This tutorial assumes that you have logged in to the `model repository`_ and have sufficient privileges in the workspace you wish to expose.

In this example I will use a :term:`fork` of the the Beeler Reuter 1977 workspace. Creating a *fork* of a workspace creates a *clone* of that workspace that you own, and can push changes to. You can *fork* any publicly available workspace in the Physiome model repository. For more information on this feature of PMR, refer to the information on features or collaboration.

Choose the revision to expose
-----------------------------

As an exposure is created to present a particular revision of a workspace, the first thing to do is to navigate to that revision. To do this, first find the workspace - if this is your own workspace, you can click on the *My Workspaces* button in the navigation bar of the repository and find the workspace of interest in the listing displayed. After navigating to your workspace, click on the *history* button in the menu bar.

.. note:: In order to create an exposure of a workspace, the workspace must be *published*. You will either need to have sufficient privileges on the repository site to publish your own workspace, or you will have to submit your workspace for publication and await review. It is not currently possible to create exposures in private workspaces.

.. figure:: /PMR/images/PMR-workspacehistory.png
   :align: center
   
   **The revision history of a fork of the Beeler Reuter 1977 workspace**

Now you can select the revision of the workspace you wish to expose by clicking on the *manifest* of that revision. Usually you will want to expose the latest revision, which appears at the top of the list.

After selecting the revision you wish to expose, click on the *workspace actions* menu at the far right end of the menu bar and select *create exposure*.

.. figure:: /PMR/images/PMR-revisioncreateexposure.png
   :align: center
   
   **Selecting the manifest of the revision to expose**

Building the exposure
---------------------

Selecting the *create exposure* option in the menu bar will bring you to the first page of the exposure *wizard*. This web interface allows you to select the model files, documentation files, and settings that will be used to create the exposure.

The initial page of the exposure creation wizard allows you to select the main documentation file and the first model file. Select the HTML annotator option and the HTML documentation file for the workspace in the *Exposure main view* section. For the *New Exposure File Entry* section, choose the CellML file you wish to expose, and select CellML as the file type.

.. figure:: /PMR/images/PMR-wizard1.png
   :align: center
   
   **Selecting the main documentation and the first CellML model file**

.. note:: Documentation should be written in HTML format. Some previous users of the CellML repository may be familiar with the tmpdoc style documentation, which has be deprecated. For an example of what a fairly standard HTML documentation file might look like, take a look at the `documentation for the Beeler Reuter 1977 model <http://models.cellml.org/workspace/beeler_reuter_1977/file/fdd29a005ffcf9a72d7ef2479cafb864ea1e887a/beeler_reuter_1977_documentation.html>`_.

Once you have selected the documentation and model files and their types, click on the *Add* button. This will take you to the next step of the wizard, where you can select various options for the model you have chosen to expose, and will allow you to add further model files to the exposure if desired.

The wizard shows a *subgroup* for each CellML file to be included in the exposure. For each CellML file, select the following options:

* Documentation
   * Documentation file - select the HTML file created to document the model
   * View generator - select HTML annotator option
* Basic Model Curation
   * Curation flags - CellML model repository curators may select flags according to the status of the model
* License and Citation
   * File/Citation format - select CellML RDF metadata to automatically generate a citation page using the model RDF
   * License - select Creative Commons Attributions 3.0 Unported
* Source Viewer
   * Language Type - select xml
* OpenCell Session Link
   * Session File - select the session.xml if it has been created

.. figure:: /PMR/images/PMR-wizard2.png
   :align: center
   
   **Selecting options for the model file subgroup**   

After selecting the subgroup options, you need to click the *Update* button to set the chosen options for the exposure builder. If you do not update the subgroup, the options you selected will be replaced by the default options when you click *Build*.
   
For exposures where you wish to expose multiple models, click on the *Add file* button at this stage to create another subgroup. You can then use this to set up all the same options listed above for the additional model file. Remember to click *Update* when you have completed selecting the options for each subgroup before adding another subgroup.
   
After setting all the options for the models you wish to expose, click on the *Build* button. The repository software will then create the exposure pages and display the main page of the exposure.

In order to make the exposure visible and searchable, you will need to publish it. You can choose to submit your exposure for review, or if you have sufficient privileges you can publish it directly.
   
.. figure:: /PMR/images/PMR-exposurepublish.png
   :align: center
   
   **Publish your exposure to make it visible to others.**

Other types of exposure
=======================

Because the exposure builder uses HTML documentation, it is possible to create customized types of exposure that differ from the standard type shown above. For example, you might want to create an exposure that simply documents and provides links to models in a PMR workspace that are encoded in languages other than CellML. You can also use the HTML documentation to provide tutorials or other documents, with resources stored in the workspace and linked to from the HTML.

**Examples of other exposure types:**

* `Andre's Hodgkin & Huxley CellML tutorial <http://models.cellml.org/e/e1>`_
* `Testing nested SED-ML proposals with CellML <http://models.cellml.org/e/c2>`_
* `Aslanidi *et al.* cardiac models encoded in C <http://models.cellml.org/e/ca>`_
   
.. _model repository: http://models.cellml.org
.. _example HTML: http://models.cellml.org/workspace/beeler_reuter_1977/file/fdd29a005ffcf9a72d7ef2479cafb864ea1e887a/beeler_reuter_1977_documentation.html

