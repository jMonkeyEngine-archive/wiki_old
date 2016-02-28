---
title: Endless Terrain
---
<h1 class="sectionedit1" id="endless_terrain">Endless Terrain</h1>
<div class="level1">

<p>
</p><p></p><div class="noteclassic">Deprecated. Look at <a href="http://hub.jmonkeyengine.org/forum/topic/design-question-terrain/#post-262072" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/design-question-terrain/#post-262072" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/design-question-terrain/#post-262072</a> instead
</div>


<p>
TerrainGrid is DEPRECATED.
</p>

<p>
TerrainGrid is an extension built on top of the TerraMonkey tools like TerrainQuad and HeightMap, that provides “infinite” Terrain paging routines.  <br />

Thanks to Gábor (@anthyon) and Brent (@sploreg) for this contribution!
</p>

</div>
<!-- EDIT1 SECTION "Endless Terrain" [1-484] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
The classes with source code can be found in the org.jme3.terrain.geomipmapping and org.jme3.terrain.heightmap packages. Also there are 3 tests prepared in the jme3test.terrain package:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainGridTest.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainGridTest.java" rel="nofollow">TerrainGridTest.java</a>: uses an ImageBasedHeightMapGrid instance to load the tiles</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainFractalGridTest.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainFractalGridTest.java" rel="nofollow">TerrainFractalGridTest.java</a>: makes use of the FractalHeightMapGrid class, and generates a terrain from noise</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainGridAlphaMapTest.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainGridAlphaMapTest.java" rel="nofollow">TerrainGridAlphaMapTest.java</a>: shows how to use TerrainGridListener to change the material of the tiles</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [485-1364] -->
<h2 class="sectionedit3" id="specification">Specification</h2>
<div class="level2">

<p>
TerrainGrid is made up of the TerrainGrid class, and the HeightMapGrid and TerrainGridListener interfaces.
</p>
<ul>
<li class="level1"><div class="li"> TerrainGrid is the central class of the system. It takes care for handling camera movement in LODUpdate, loading and unloading terrain tiles on demand, and notifying any registered listeners of changes.</div>
</li>
<li class="level1"><div class="li"> TerrainGridListener defines two events to listen to:</div>
<ul>
<li class="level2"><div class="li"> gridMoved(Vector3f):  gets the new center as parameter after terrain update, so any objects can be added or removed as needed.</div>
</li>
<li class="level2"><div class="li"> Material tileLoaded(Material material, Vector3f cell): notifies the system about a tile being loaded. Parameters are a cloned value of the material added to the TerrainGrid, and the cell of the new tile. The system can change the material according to this information (eg. load required alphamaps, etc).</div>
</li>
</ul>
</li>
</ul>

<p>
<br />

Multiple listeners can be added to the TerrainGrid, they will be called in the order of addition, so it’s possible to have multiple changes to the material before completing the load of the tile.
<br />

HeightMapGrid adds the possibility of loading terrain tiles on demand instead of having a simple height array. There’s no predefined way of how to store these tiles, it only takes care of loading one HeightMap object at given location at a time.
</p>

</div>
<!-- EDIT3 SECTION "Specification" [1365-2655] -->
<h2 class="sectionedit4" id="motivation">Motivation</h2>
<div class="level2">

<p>
<a href="/resources/wp-uploads-2011-06-grid-tiles.jpg" class="media wikilink2" title="wp-uploads:2011:06:grid-tiles.jpg"><img src="/resources/wp-uploads-2011-06-grid-tiles.jpg" class="mediaright" alt="" width="130" height="130" /></a>
After playing around with the terrain in jME3, soon comes the requirement of having larger explorable lands. Increasing the size of one TerrainQuad leads to more memory usage, while it will still be easy to reach the worlds boundaries. That’s why TerrainGrid was designed. It extends the TerraindQuad class and uses 4 HeightMaps (dark blue) as the four sub-quad. This means that a terrain of size 513 will use tiles of 257. Also an LRUCache is built into the terrain package, so surrounding tiles (green) can be pre-cached on a different thread, lowering the loading time. The quads are updated as the camera approaches the boundary of the light blue section.
</p>

</div>
<!-- EDIT4 SECTION "Motivation" [2656-3387] -->
<h2 class="sectionedit5" id="rationale">Rationale</h2>
<div class="level2">

<p>
The design of the TerrainGrid system was chosen carefully, so that minimal effort needs to be taken to switch from previous TerrainQuad uses. It has the same constructors with the small exception that instead of an array of heightmap it takes a HeightMapGrid instance. All other parameters are forwarded down to the underlying TerrainQuad system.
There exist also two basic HeightMapGrid implementations:
</p>
<ul>
<li class="level1"><div class="li"> ImageBasedHeightMapGrid: uses a sequentially numbered, 16 bit grayscale heightmaps. The physical filename of these files can be generated through the Namer interface. When a tile cannot be found by the assetManager, an empty (all-zero) heightmap is created, and a warning is added to the log.</div>
</li>
<li class="level1"><div class="li"> FractalHeightMapGrid: uses a noise library to create a landscape on the fly. The shape of the terrain can be controlled by the various parameters and postfilters of the fractals. With the help of this grid implementation there’s no limitation – above of floating point precision limits – how far the camera can get. The tiles generated this way can be cached to the filesystem, for later modification. The FractalHeightMapGrid will always load from cache if a tile exists there!</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Rationale" [3388-4598] -->
<h2 class="sectionedit6" id="usage">Usage</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li">  instantiate a TerrainGrid object</div>
</li>
<li class="level1"><div class="li">  set material, listeners, translation, scale, etc.</div>
</li>
<li class="level1"><div class="li">  add a LODControl instance to the object</div>
</li>
<li class="level1"><div class="li">  call initialize with the camera location</div>
</li>
<li class="level1"><div class="li">  (optional) add it to the physicsSpace as you would a TerrainQuad</div>
</li>
</ol>

<p>
Further information about terrain and TerrainQuad can be found in the wiki at:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_terrain" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_terrain" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_terrain</a> and</div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:advanced:terrain" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:advanced:terrain" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3:advanced:terrain</a></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Usage" [4599-] -->
