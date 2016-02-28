---
title: Build Your Block World
---
<h1 class="sectionedit1" id="build_your_block_world">Build Your Block World</h1>
<div class="level1">

<p>
Now you've set up your different block types and we're ready to build some cool stuff in our world. :)
</p>

</div>
<!-- EDIT1 SECTION "Build Your Block World" [1-142] -->
<h2 class="sectionedit2" id="usage_example">Usage example</h2>
<div class="level2">

<p>
Instead of explaining every different method of the framework, here's a descriptive example, that should explain the usage:
</p>
<pre class="code java"><span class="co1">//This is your terrain, it contains the whole</span>
<span class="co1">//block world and offers methods to modify it</span>
BlockTerrainControl blockTerrain <span class="sy0">=</span> <span class="kw1">new</span> BlockTerrainControl<span class="br0">(</span>CubesTestAssets.<span class="me1">getSettings</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//To set a block, just specify the location and the block object</span>
<span class="co1">//(Existing blocks will be replaced)</span>
blockTerrain.<span class="me1">setBlock</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>, CubesTestAssets.<span class="me1">BLOCK_WOOD</span><span class="br0">)</span><span class="sy0">;</span>
blockTerrain.<span class="me1">setBlock</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">1</span><span class="br0">)</span>, CubesTestAssets.<span class="me1">BLOCK_WOOD</span><span class="br0">)</span><span class="sy0">;</span>
blockTerrain.<span class="me1">setBlock</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>, CubesTestAssets.<span class="me1">BLOCK_WOOD</span><span class="br0">)</span><span class="sy0">;</span>
blockTerrain.<span class="me1">setBlock</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">1</span><span class="br0">)</span>, CubesTestAssets.<span class="me1">BLOCK_STONE</span><span class="br0">)</span><span class="sy0">;</span>
blockTerrain.<span class="me1">setBlock</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span>, CubesTestAssets.<span class="me1">BLOCK_GRASS</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//For the lazy users :P</span>
 
<span class="co1">//You can place whole areas of blocks too: setBlockArea(location, size, block)</span>
<span class="co1">//(The specified block will be cloned each time)</span>
<span class="co1">//The following line will set 3 blocks on top of each other</span>
<span class="co1">//({1,1,1}, {1,2,3} and {1,3,1})</span>
blockTerrain.<span class="me1">setBlockArea</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">3</span>, <span class="nu0">1</span><span class="br0">)</span>, CubesTestAssets.<span class="me1">BLOCK_STONE</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Removing a block works in a similar way</span>
blockTerrain.<span class="me1">removeBlock</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">2</span>, <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
blockTerrain.<span class="me1">removeBlock</span><span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">3</span>, <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//The terrain is a jME-Control, you can add it</span>
<span class="co1">//to a node of the scenegraph to display it</span>
Node terrainNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
terrainNode.<span class="me1">addControl</span><span class="br0">(</span>blockTerrain<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrainNode<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
After running those few lines, you should see this:
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/test_tutorial.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

<p>
As you see, creating and managing your own block world will just take a few lines of code and doesn't require any special knowledge. :)
</p>

</div>
<!-- EDIT2 SECTION "Usage example" [143-1972] -->
<h2 class="sectionedit3" id="me_wantz_spezzial_phyziczzz_and_shadowzzz">Me wantz spezzial phyziczzz and shadowzzz</h2>
<div class="level2">

<p>
The BlockTerrainControl attaches the world to the assigned jME-Node - This way you can specify behaviors like shadows or even physics just like you do with each other object:
</p>
<pre class="code java">terrainNode.<span class="me1">setShadowMode</span><span class="br0">(</span>ShadowMode.<span class="me1">CastAndReceive</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">terrainNode.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> RigidBodyControl<span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
physicsSpace.<span class="me1">addAll</span><span class="br0">(</span>terrainNode<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT3 SECTION "Me wantz spezzial phyziczzz and shadowzzz" [1973-] -->
