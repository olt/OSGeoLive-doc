:Author: OSGeo-Live
:Author: Pirmin Kalberer
:Author: Hamish Bowman
:Reviewer: Cameron Shorter, LISAsoft
:Version: osgeo-live7.9
:License: Creative Commons Attribution-ShareAlike 3.0 Unported  (CC BY-SA 3.0)

.. TBD: Cameron's review comments:
  This document is in "DRAFT" state until these comments have been removed.
  I've added a number of review comments, starting with TBD: ...
  Overall: Each section needs to explain what it is about to do and the
  benefits of it. (target audience is a new user).
  We also need screen shots after each significant step.
  Once these comments have been addressed, please remove my comment.

.. image:: ../../images/project_logos/logo-QGIS.png
  :scale: 100 %
  :alt: project logo
  :align: right
  :target: http://www.qgis.org


********************************************************************************
QGIS クイックスタート 
********************************************************************************

Quantum GIS (QGIS) は視覚化、管理、編集、データ解析、印刷できる地図作製に使える
ユーザフレンドリーなデスクトップ GIS クライアントです。

.. contents:: Contents


QGIS プロジェクトを編集する
================================================================================

既存の QGIS プロジェクト を開き、レイヤのオンとオフを切り替えるところから始めましょう。


.. TBD: Cameron's review comments:
  Screen shot here (showing menu selection with NaturalEarth highlighted)

#. :menuselection:`Geospatial --> Desktop GIS --> QGIS` から QGIS を起動し、メニューバーから :menuselection:`Project --> Open` を選択してください。

#. ファイル :file:`QGIS-NaturalEarth-Example.qgs` を選択し、 :guilabel:`Open` をクリックしてください。

   * 世界地図が表示されるはずです。

#. レイヤツリーから ``ne_10m_populated_places`` を選択してください

   * 人口の多い地域が、たくさんの緑のドットで表示されます:

     .. image:: ../../images/screenshots/1024x768/qgis.png
        :scale: 70 %

#. Try dragging layers up and down in the legend and see how that
   affects visibility of the layers below.

#. Have a look at the tools on the tool bar. Try panning, zooming in,
   and zooming back out to full extent again.  Find these tools next
   to the :guilabel:`hand` icon. If the toolbars seem cluttered you
   can drag them around and turn them on and off by right clicking.
   You can also zoom in and out with the mouse wheel, and pan with a
   left-click drag.

.. TBD: Cameron's review comments:
  Screen shot here, touched up with a red circle around the "hand" icon.
  http://wiki.osgeo.org/wiki/Live_GIS_Add_Project#Screen_Shot
  HB: toolbars are all on top of each other by default, it's not ideal..


Style a layer
================================================================================

Now let's try customising the style of the map.

.. TBD: Cameron's review comments:
  Screen shot or two here

#. 地図上で少しズームインし、レイヤツリーで ``ne_10m_rivers_lake_centerlines`` をダブルクリックしてください。


#. `Outline Options` で異なる色(ここでは黄色)に変更してください。

#. :guilabel:`OK` を押してください。

   * 川が選択した色で表示されます。


新規の QGIS プロジェクトを作成する
================================================================================

Let's now create a new QGIS project and load our own data.

#. メニューから :menuselection:`Project --> New` を選択してください。

#. :menuselection:`Layer --> Add Vector Layer...` をクリックしてください。

#. データセット :file:`/home/user/data/natural_earth2/ne_10m_admin_0_countries.shp` を選択してください。

#. :guilabel:`Open` を押し、再度 :guilabel:`Open` を押してください。

   * 世界の国が表示されます。

.. TBD: Cameron's review comments:
  Screen shot here


Connect to a PostGIS spatial database
================================================================================

.. TBD: Cameron's review comments:
  For Info of author: I've switched from OSM dataset to Natural Earth,
  as OSM extent changes between releases, which means screenshots from
  this quickstart would become dated.

Let's now include a layer from a Postgres database.

#. In the layer list on the left, untick the ``ne_10m_admin_0_countries`` visibility
   check box to temporarily hide it.

   .. image:: ../../images/screenshots/800x600/qgis_postgis_connect.png
      :scale: 70 %
      :alt: Connecting to a PostGIS DB
      :align: right

#. Choose :menuselection:`Layer --> Add PostGIS Layers...`.

   * Both Natural Earth and OpenStreetMap Postgis databases
     are already available; we will be using use the Natural Earth database.
     If you wanted to connect to a different database, you would select
     the :guilabel:`New` button and fill in the database parameters.

#. Select the "Natural Earth" connection and press :guilabel:`Connect`.

   * A list of database tables will appear.

#. Select ``ne_10_populated_places`` and click :guilabel:`Add`.

   * For more details about working with PostGIS databases see
     the :doc:`PostGIS Quickstart <postgis_quickstart>`.

#. Zoom in on the United States using the mouse wheel and left-click drag
   to navigate.

#. Right click on ``ne_10m_populated_places`` in the layer list to get a context
   menu, then select :menuselection:`Properties`.

#. Let's represent one of the database attributes in the data as a bubble plot.
   In the middle of the `Layer Properties` window, drag the Transparency
   slider to **50%**, press the :guilabel:`Advanced` button and select
   :menuselection:`Size scale field`, then choose **elevation** 
   (it's in about the middle of the list), and finally set the
   symbol `Size` scaling to **0.02**. Then click :guilabel:`Ok`.

#. You can then click on the query button on the toolbar (cursor arrow with
   a blue "i") and then on the map canvas bubbles to view information about
   the individual cities.


Using the GRASS Toolbox
================================================================================

There have been many plugins written for QGIS which extend QGIS's core
functionality. One of the more powerful is the GRASS plugin, which taps
into the hundreds of geospatial processing modules available
from :doc:`GRASS GIS <../overview/grass_overview>`.

.. TBD: Cameron's review comments:
  Screen shot here, show toolbox menu, which has been scrolled down to show GRASS, ticked.

#. Clear the slate with :menuselection:`Project --> New`.

#. Choose :menuselection:`Plugins --> Manage and Install Plugins...`, then scroll down or
   type ``grass`` into the Search box, and select the `GRASS` plugin.

   * Notice that a new GRASS icon has been added to the Toolbar, and
     a new `GRASS` menu item has been added to the `Plugins` menu.

#. Connect to an existing GRASS workspace with :menuselection:`Plugins --> GRASS --> Open mapset`.

   * The GRASS GIS data base (Gisdbase) has already been set to `~/grassdata` on
     the disc for you.

#. Within the central GRASS data base are a number of sample datasets. We'll
   load the Spearfish location, and the ``user1`` mapset within it. Choose
   the `spearfish60` Location and `user1` working mapset, then click :guilabel:`Ok`.

#. To add a map to the QGIS layer list, choose :menuselection:`Plugins --> GRASS --> Add GRASS raster layer`.

   * In the PERMANENT mapset select the `aspect` map and click :guilabel:`Ok`.

     .. image:: ../../images/screenshots/1024x768/qgis_grass_layers.jpg
       :scale: 50 %
       :alt: GRASS GIS layers loaded into QGIS
       :align: right

#. Add another GRASS raster layer, this time the `elevation.10m` map from the
   PERMANENT mapset.

   * Double click on the `elevation.10m` map in the QGIS layer list and in
     the Transparency tab set its global transparency to 50%.

#. To add a vector map, choose :menuselection:`Plugins --> GRASS --> Add GRASS vector layer`.

   * From the PERMANENT mapset select the `roads` map and click :guilabel:`Ok`.


The plugin also gives you access to many of the powerful GRASS analysis
modules and visualization tools:

.. HB: We could go through a grass processing module here (e.g. r.sun), but
  probably it gets too long and a fTools or SEXTANTE module could take on that
  role. Here we show off NVIZ as it brings 3D visualization capability to
  QGIS, and people do like the shiny. It is helpful to go through the g.region
  housecleaning step next, so for now we'll use that as the example of how to
  run a module.

#. From the top menu select :menuselection:`Plugins --> GRASS --> Open GRASS tools` and
   drag the edge to make the window a bit bigger.

   * A long list of analysis tools will appear. Go to the `Modules Tree` tab and
     select :menuselection:`Region settings --> g.region.multiple.raster`.
     Clicking on it will open a new tab. Simply type ``elevation.10m`` for the
     raster map name and press :guilabel:`Run`. The `elevation.10m` map will
     now have a thin red line around it, indicating the extent of
     GRASS's `computational region` bounds.

#. Back in the `Modules Tree` tab of the `GRASS Tools` window, go down
   to :menuselection:`3d Visualization` and select `NVIZ`. You may need to
   drag the corner of the toolbox window again to make it a bit larger to
   see all the options.

#. In the new module tab that pops open, select the `elevation.10m` map as the
   map for elevation. Then depress the rectangle with red corners button on
   the right of the map name to use the region bounds and resolution of that
   map. As mentioned earlier, the `computational region` is a core theme in
   GRASS raster processing.

#. Select `roads` for the vector overlay, then click :guilabel:`Run`.

#. Once the NVIZ 3D view opens, maximize the window and drag the positioning
   puck in the compass box on the left to a nice view.

#. Choose :menuselection:`Visualize --> Raster surfaces` and set the `fine` resolution
   to 1, then if needed click the green :guilabel:`DRAW` button in the top
   left and wait while it renders.


Using the Processing Toolbox
================================================================================

A core plugin for QGIS which opens the door to a large family of
processing tools is the Processing Toolbox (formerly named the SEXTANTE Toolbox).
It acts as a standardized wrapper around a number of other sets to tools.

.. TBD: Cameron's review comments:
  If we are to include Sextante, then we need to describe using one of the
  Sextane features.

#. Choose :menuselection:`Processing --> Toolbox`.

   * A new toolbar will open on the right side of the screen with many
     processing tools to choose from. Take some time and have a look around.


Importing OpenStreetMap data
================================================================================

.. TBD: Cameron comment
  Need a sentence here introducing what the OpenStreetMap tools provide.

#. Open the LX Terminal Emulator from the main :menuselection:`Accessories` menu.

   * Cut and paste the following commands into the Terminal window to create
     a working copy of the OSM data in the home directory:

     ::
     
       cp data/osm/feature_city_CBD.osm.bz2 .
       bzip2 -d feature_city_CBD.osm.bz2

#. In QGIS, choose :menuselection:`Project --> New`. If you had the
   Processing Toolbox open you might want to close it.


   .. image:: ../../images/screenshots/1024x768/qgis_osm_plugin.png
     :scale: 50 %
     :alt:  The OpenStreetMap plugin
     :align: right

#. Choose :menuselection:`Vector --> OpenStreetMap --> Import toplogy from XML`.

#. Click on the "..." button next to "Input XML file (.osm)" and select
   the `feature_city_CBD.osm` file you just copied into the home directory.
   The "Output SpatialLite DB file" name will be automatically set. Click
   :guilabel:`Ok` to convert the dataset to SpatiaLite format and create
   a connection to the SpatialLite DB within QGIS.

#. Next we need to extract points, lines, and areas, then add topology to
   each of these three new layers. To do this we need to run the tool three times.
   Select :menuselection:`Vector --> OpenStreetMap --> Export toplogy to SpatiaLite` and
   use the "..." button to select the newly created `feature_city_CBD.osm.db` file.
   The `Output layer name` will be automatically filled in for you depending
   on the `Export type` selected. Click the :guilabel:`Load from DB` button
   to load in the available tags. For the "points" layer tick the `amentity` box;
   for the "polylines" layer tick the `highway` layer; and for
   the "polygon" layer select the `building` layer. You may wish to change
   the `Output layer name` to reflect the feature tags that you've selected.
   When you are ready, press :guilabel:`Ok` to load in the layer. You will
   need to again press the :guilabel:`Load from DB` button after changing
   the export type from points to polylines, and polylines to polygons.

#. Once topology is loaded, you can also refine the SpatiaLite layer by
   querying just certain features from within it.
   Select :menuselection:`Layer --> Add SpatiaLite Layer...` from the
   menu and from the `Databases` list select `feature_city_CBD@...` and
   then click on :guilabel:`Connect`. Double click on
   the `feature_city_cbd_polylines` table and then double click on "highway"
   to start building your SQL query. Then click on the :guilabel:`=` button,
   then the :guilabel:`All` button, and double click on `motorway` from the
   Values list. Click the :guilabel:`Test` button to verify the result,
   and finally click on :guilabel:`Ok`. Back in the `Add SpatiaLite Table`
   window click :guilabel:`Add` to restrict the rendering to just major
   highways. You can repeat this process with new layers to render different
   road types with different widths and styles.

#. You can now explore this rich dataset. Use the ``i`` information cursor
   button in the QGIS toolbar to query individal map features.

Things to Try
================================================================================

* Try viewing data sources with the `QGIS Data Browser <http://planet.qgis.org/planet/tag/qgis%20browser/>`_ in the :menuselection:`Geospatial --> Databases` menu

* Try publishing your QGIS map to the web using :doc:`QGIS Map Server <../overview/qgis_mapserver_overview>` in the :menuselection:`Geospatial --> Web Services` menu.


参照情報
================================================================================

より進んだ QGIS のチュートリアルを `OSGeo-Live QGIS tutorials`_ に集めてあります。

QGIS について詳細の開始ページは QGIS ホームページの `Documentation page`_ になります。


`A Gentle Introduction to GIS`_ `[1]`_ eBook と `QGIS User Guide`_ `[2]`_ は
OSGeo-Live のディスクに含まれています。

.. _`OSGeo-Live QGIS tutorials`: ../../qgis/tutorials/en/
.. _`Documentation page`: http://docs.qgis.org/
.. _`A Gentle Introduction to GIS`: http://www.qgis.org/en/docs/gentle_gis_introduction/index.html
.. _`QGIS User Guide`: http://www.qgis.org/en/docs/user_manual/index.html
.. _`[1]`: ../../qgis/qgis-1.0.0_a-gentle-gis-introduction_en.pdf
.. _`[2]`: ../../qgis/QGIS-2.0-UserGuide-en.pdf

