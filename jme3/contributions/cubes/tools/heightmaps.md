---
title: Heightmaps
---
<h1 class="sectionedit1" id="heightmaps">Heightmaps</h1>
<div class="level1">

<p>
Most of you will know the term “heightmap” - Those are images (normally gray-scaled), which describe a terrain. Each pixel is a point on the surface: The brighter the pixel, the higher the terrain at this location. Easy, huh?
</p>

<p>
“Cubes” offers a way to load those heightmaps to generate your blockworld - You specify the image, the frameworks loads it and adds blocks that look like it.
</p>

</div>
<!-- EDIT1 SECTION "Heightmaps" [1-413] -->
<h2 class="sectionedit2" id="loading_heightmaps">Loading heightmaps</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/heightmap_australia.jpg"><img src="/resources/fetch.php" class="mediaright" title="destroflyer.mania-community.de_other_imagehost_cubes_heightmap_australia.jpg" alt="destroflyer.mania-community.de_other_imagehost_cubes_heightmap_australia.jpg" /></a>
When specifying the heightmap, you can tell the framework where to set the blocks and how to scale them - As an example, let's rebuild australia in our blockworld:
</p>
<pre class="code java"><span class="co1">//Create the block terrain (7x1x7 chunks)</span>
BlockTerrainControl blockTerrain <span class="sy0">=</span> <span class="kw1">new</span> BlockTerrainControl<span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">7</span>, <span class="nu0">1</span>, <span class="nu0">7</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Specify location, heightmap filepath, maximum height and the block class</span>
<span class="co1">//(See the heightmap at the right)</span>
blockTerrain.<span class="me1">setBlocksFromHeightmap</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="st0">"Textures/cubes/heightmap_australia.jpg"</span>, <span class="nu0">10</span>, CubesTestAssets.<span class="me1">BLOCK_GRASS</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Add the block terrain to a node</span>
Node terrainNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
terrainNode.<span class="me1">addControl</span><span class="br0">(</span>blockTerrain<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrainNode<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
After running this code (and adding nice water and shadow effects :P), you should see this:
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/test_australia.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

</div>
<!-- EDIT2 SECTION "Loading heightmaps" [414-1421] -->
<h2 class="sectionedit3" id="important_notes">Important notes</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> The size of your heightmap defines how large (X, Z) the terrain will be (1px = 1 block)</div>
</li>
<li class="level1"><div class="li"> The heighest block will be at a height of <code>(StartY + MaximumHeight)</code></div>
</li>
<li class="level1"><div class="li"> Black pixels (R|G|B = 0|0|0) means that no block will be set</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Important notes" [1422-1683] -->
<h2 class="sectionedit4" id="further_improvements">Further improvements</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> You will be able to scale the loaded blocks by the X and Z axis, too</div>
</li>
<li class="level1"><div class="li"> It will be possible to specify a loader, that selects a “suitable” block type dependant on the location</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Further improvements" [1684-] -->
