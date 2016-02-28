---
title: Noise
---
<h1 class="sectionedit1" id="noise">Noise</h1>
<div class="level1">

<p>
Noises are arrays of random numbers, that “fit” together in some way - They're often used to generate content, for example block worlds. After specifying a noise, the framework will generate the random numbers and place according blocks (the larger the number, the heigher the terrain at this point).
</p>

<p>
</p><p></p><div class="noteimportant">Remember that large noises will take some time to calculate.
</div>


</div>
<!-- EDIT1 SECTION "Noise" [1-409] -->
<h2 class="sectionedit2" id="generate_a_noise">Generate a noise</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/noise_example.jpg"><img src="/resources/fetch.php" class="mediaright" title="destroflyer.mania-community.de_other_imagehost_cubes_noise_example.jpg" alt="destroflyer.mania-community.de_other_imagehost_cubes_noise_example.jpg" /></a>
At the moment, the framework supports only one noise type (based on the <a href="http://en.wikipedia.org/wiki/Diamond-square_algorithm" class="urlextern" title="http://en.wikipedia.org/wiki/Diamond-square_algorithm" rel="nofollow">Diamond-square Algorithm</a>) - You can see a visualization of such a noise at the right.
</p>

<p>
This is how you can use it:
</p>
<pre class="code java"><span class="co1">//Create the block terrain (4x1x4 chunks)</span>
BlockTerrainControl blockTerrain <span class="sy0">=</span> <span class="kw1">new</span> BlockTerrainControl<span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">4</span>, <span class="nu0">1</span>, <span class="nu0">4</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Specify location, size, roughness and the block class</span>
<span class="co1">//(The smaller the roughness, the flatter the generated terrain)</span>
blockTerrain.<span class="me1">setBlocksFromNoise</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">64</span>, <span class="nu0">50</span>, <span class="nu0">64</span><span class="br0">)</span>, 0.3f, CubesTestAssets.<span class="me1">BLOCK_GRASS</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Add the block terrain to a node</span>
Node terrainNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
terrainNode.<span class="me1">addControl</span><span class="br0">(</span>blockTerrain<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrainNode<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Some random results of the according noise:
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/test_noise.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

</div>
<!-- EDIT2 SECTION "Generate a noise" [410-1433] -->
<h2 class="sectionedit3" id="further_improvements">Further improvements</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> There will be mutltiple noises available and even an interface to define your own noises</div>
</li>
<li class="level1"><div class="li"> It will be possible to specify a loader, that selects a “suitable” block type dependant on the location</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Further improvements" [1434-] -->
