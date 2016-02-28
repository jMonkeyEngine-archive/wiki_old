---
title: Basic Example
---
<h1 class="sectionedit1" id="basic_example">Basic Example</h1>
<div class="level1">
<pre class="code java"><span class="kw1">package</span> <span class="co2">com.cubes.test</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">java.util.logging.Level</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.logging.Logger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.system.AppSettings</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.cubes.*</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> TestTutorial <span class="kw1">extends</span> SimpleApplication<span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        Logger.<span class="me1">getLogger</span><span class="br0">(</span><span class="st0">""</span><span class="br0">)</span>.<span class="me1">setLevel</span><span class="br0">(</span>Level.<span class="me1">SEVERE</span><span class="br0">)</span><span class="sy0">;</span>
        TestTutorial app <span class="sy0">=</span> <span class="kw1">new</span> TestTutorial<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> TestTutorial<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        settings <span class="sy0">=</span> <span class="kw1">new</span> AppSettings<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        settings.<span class="me1">setWidth</span><span class="br0">(</span><span class="nu0">1280</span><span class="br0">)</span><span class="sy0">;</span>
        settings.<span class="me1">setHeight</span><span class="br0">(</span><span class="nu0">720</span><span class="br0">)</span><span class="sy0">;</span>
        settings.<span class="me1">setTitle</span><span class="br0">(</span><span class="st0">"Cubes Demo - Tutorial"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        CubesTestAssets.<span class="me1">registerBlocks</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//This is your terrain, it contains the whole</span>
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
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrainNode<span class="br0">)</span><span class="sy0">;</span>
 
        cam.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">10</span>, <span class="nu0">10</span>, <span class="nu0">16</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        cam.<span class="me1">lookAtDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>, <span class="sy0">-</span>0.56f, <span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
        flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span><span class="nu0">50</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
</p><p></p><div class="noteclassic">This code uses the test settings offered by the framework - You can replace the call <code>CubesTestAssets.getSettings(this);</code> as described <a href="/jme3/contributions/cubes/settings.html" class="wikilink1" title="jme3:contributions:cubes:settings">here</a>.
</div>


<p>
</p><p></p><div class="noteclassic">This code uses the test blocks offered by the framework - You can replace the call <code>CubesTestAssets.registerBlocks();</code> as described <a href="/jme3/contributions/cubes/register_your_blocks.html" class="wikilink1" title="jme3:contributions:cubes:register_your_blocks">here</a>.
</div>


</div>
