.. _PMR-exposing-fieldml:

==========================
Creating FieldML exposures
==========================

.. sectionauthor:: Dougal Cowan

FieldML models in the Physiome Model Repository are presented through :term:`exposures`.  A FieldML exposure has some similarities to a CellML exposure - usually consisting of a main documentation page with some information about the model, accompanied by a range of different views of the model data and or metadata. FieldML exposures also allow the real-time three-dimensional display of model meshes within the browser through the use of the `Zinc plugin <http://www.cmiss.org/cmgui/zinc>`_.

The example screenshots below show the main documentation page view and the 3D visualization provided by the Zinc viewer.

.. figure:: /PMR/images/PMR-fieldmlexposureexample1.png
   :align: center
   
   The main documentation view of a FieldML exposure
   
.. figure:: /PMR/images/PMR-fieldmlexposureexample2.png
   :align: center
   
   The main Zinc viewer view of the same FieldML exposure

This is a paragraph

Creating the exposure files
===========================

To create a FieldML exposure, the following files will need to be stored in a workspace in PMR:

* The FieldML model file(s)
* An RDF file containing metadata about the model, and specifying the JSON file to be used for the visualization
* The JSON file that specifies the Zinc viewer visualization settings
* Optionally, documentation (HTML) and images (PNG, JPG etc) 

Example of the RDF file from Laminar Structure of the Heart workspace:

.. code-block:: xml
   :linenos:

   <?xml version="1.0" encoding="utf-8"?>
   <rdf:RDF
       xmlns="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
       xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
       xmlns:dc="http://purl.org/dc/elements/1.1/"
       xmlns:dcterms="http://purl.org/dc/terms/"
       xmlns:vCard="http://www.w3.org/2001/vcard-rdf/3.0#"
       xmlns:pmr2="http://namespace.physiomeproject.org/pmr2#">
     <rdf:Description rdf:about="">
       <dc:title>
         Laminar structure of the Heart: A mathematical model.
       </dc:title>
       <dc:creator>
         <rdf:Seq>
           <rdf:li>LeGrice, I.J.</rdf:li>
           <rdf:li>Hunter, P.J.</rdf:li>
           <rdf:li>Smaill, B.H.</rdf:li>
         </rdf:Seq>
       </dc:creator>
       <dcterms:bibliographicCitation>
         American Journal of Physiology 272: H2466-H2476, 1997.
       </dcterms:bibliographicCitation>
       <dcterms:isPartOf rdf:resource="info:pmid/9176318"/>
       <pmr2:annotation rdf:parseType="Resource">
         <pmr2:type 
             rdf:resource="http://namespace.physiomeproject.org/pmr2/note#json_zinc_viewer"/>
         <pmr2:fields>
           <rdf:Bag>
             <rdf:li rdf:parseType="Resource">
               <pmr2:field rdf:parseType="Resource">
                 <pmr2:key>json</pmr2:key>
                 <pmr2:value>heart.json</pmr2:value>
               </pmr2:field>
             </rdf:li>
           </rdf:Bag>
         </pmr2:fields>
       </pmr2:annotation>
     </rdf:Description>
   </rdf:RDF>

Example of the JSON file from Laminar Structure of the Heart workspace:

.. code-block:: js
   :linenos:

   {
       "View" : [
         {
         "camera" : [9.70448, -288.334, -4.43035],
         "target" : [9.70448, 6.40667, -4.43035],
         "up"     : [-1, 0, 0],
         "angle" : 40
         }
       ],
       "Models": [
           {
               "files": [
                   "heart.xml"
               ],
               "externalresources": [
                   "heart_mesh.connectivity",
                   "heart_mesh.node.coordinates"
               ],
               "graphics": [
                   {
                       "type": "surfaces",
                       "ambient" : [0.4, 0, 0.9],
                       "diffuse" : [0.4, 0,0.9],
                       "alpha" : 0.3,
                       "xiFace" : "xi3_1",
                       "coordinatesField": "heart.coordinates"
                   },
                   {
                       "type": "surfaces",
                       "ambient" : [0.3, 0, 0.3],
                       "diffuse" : [1, 0, 0],
                         "specular" : [0.5, 0.5, 0.5],
                       "shininess" : 0.5,
                       "xiFace" : "xi3_0",
                       "coordinatesField" : "heart.coordinates"
                   },
                   {
                       "type": "lines",
                       "coordinatesField" : "heart.coordinates"
                   }
               ], 
               "elementDiscretization" : 8,
               "region_name" : "heart",
               "group": "Structures", 
               "label": "heart",
               "load": true
           }
      ]
   }