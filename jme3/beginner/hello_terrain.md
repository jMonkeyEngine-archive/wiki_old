---
title: jMonkeyEngine 3 Tutorial (10) - Hello Terrain
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_10_-_hello_terrain">jMonkeyEngine 3 Tutorial (10) - Hello Terrain</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a>,
Next: <a href="/jme3/beginner/hello_audio.html" class="wikilink1" title="jme3:beginner:hello_audio">Hello Audio</a>
</p>

<p>
One way to create a 3D landscape is to sculpt a huge terrain model. This gives you a lot of artistic freedom – but rendering such a huge model can be quite slow. This tutorial explains how to create fast-rendering terrains from heightmaps, and how to use texture splatting to make the terrain look good.
</p>

<p>
<a href="/resources/jme3-beginner-beginner-terrain.png" class="media" title="jme3:beginner:beginner-terrain.png"><img src="/resources/jme3-beginner-beginner-terrain.png" class="mediacenter" alt="" width="360" height="291" /></a>
</p>

<p>
Note: If you get an error when trying to create your ImageBasedHeightMap object, you may need to update the SDK, click on “Help” / “Check for updates”
</p>

<p>
</p><p></p><div class="notetip">To use the example assets in a new jMonkeyEngine SDK project, right-click your project, select “Properties”, go to “Libraries”, press “Add Library” and add the “jme3-test-data” library.
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (10) - Hello Terrain" [1-827] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainLodControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.AbstractHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainQuad</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.lodcalc.DistanceLodCalculator</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.HillHeightMap</span><span class="sy0">;</span> <span class="co1">// for exercise 2</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.ImageBasedHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture.WrapMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.ArrayList</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.List</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 10 - How to create fast-rendering terrains from heightmaps,
and how to use texture splatting to make the terrain look good.  */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloTerrain <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
  <span class="kw1">private</span> TerrainQuad terrain<span class="sy0">;</span>
  Material mat_terrain<span class="sy0">;</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloTerrain app <span class="sy0">=</span> <span class="kw1">new</span> HelloTerrain<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span><span class="nu0">50</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1. Create terrain material and load four textures into it. */</span>
    mat_terrain <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
            <span class="st0">"Common/MatDefs/Terrain/Terrain.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.1) Add ALPHA map (for red-blue-green coded splat textures) */</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Alpha"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/alphamap.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.2) Add GRASS texture into the red layer (Tex1). */</span>
    Texture grass <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/grass.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    grass.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex1"</span>, grass<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex1Scale"</span>, 64f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.3) Add DIRT texture into the green layer (Tex2) */</span>
    Texture dirt <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/dirt.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    dirt.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex2"</span>, dirt<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex2Scale"</span>, 32f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.4) Add ROAD texture into the blue layer (Tex3) */</span>
    Texture rock <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/road.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    rock.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex3"</span>, rock<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex3Scale"</span>, 128f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 2. Create the height map */</span>
    AbstractHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
    Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/mountains512.png"</span><span class="br0">)</span><span class="sy0">;</span>
    heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    heightmap.<span class="me1">load</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 3. We have prepared material and heightmap. 
     * Now we create the actual terrain:
     * 3.1) Create a TerrainQuad and name it "my terrain".
     * 3.2) A good value for terrain tiles is 64x64 -- so we supply 64+1=65.
     * 3.3) We prepared a heightmap of size 512x512 -- so we supply 512+1=513.
     * 3.4) As LOD step scale we supply Vector3f(1,1,1).
     * 3.5) We supply the prepared heightmap itself.
     */</span>
    <span class="kw4">int</span> patchSize <span class="sy0">=</span> <span class="nu0">65</span><span class="sy0">;</span>
    terrain <span class="sy0">=</span> <span class="kw1">new</span> TerrainQuad<span class="br0">(</span><span class="st0">"my terrain"</span>, patchSize, <span class="nu0">513</span>, heightmap.<span class="me1">getHeightMap</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 4. We give the terrain its material, position &amp; scale it, and attach it. */</span>
    terrain.<span class="me1">setMaterial</span><span class="br0">(</span>mat_terrain<span class="br0">)</span><span class="sy0">;</span>
    terrain.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">100</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    terrain.<span class="me1">setLocalScale</span><span class="br0">(</span>2f, 1f, 2f<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 5. The LOD (level of detail) depends on were the camera is: */</span>
    TerrainLodControl control <span class="sy0">=</span> <span class="kw1">new</span> TerrainLodControl<span class="br0">(</span>terrain, getCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    terrain.<span class="me1">addControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
When you run this sample you should see a landscape with dirt mountains, grass plains, plus some winding roads in between.
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [828-4465] -->
<h2 class="sectionedit3" id="what_is_a_heightmap">What is a Heightmap?</h2>
<div class="level2">

<p>
Heightmaps are an efficient way of representing the shape of a hilly landscape. Not every pixel of the landscape is stored, instead, a grid of sample values is used to outline the terrain height at certain points. The heights between the samples is interpolated. 
</p>

<p>
In Java, a heightmap is a float array containing height values between 0f and 255f. Here is a very simple example of a terrain generated from a heightmap with 5×5=25 height values.
</p>

<p>
<a href="/resources/jme2-terrain-from-float-array.png" class="media" title="jme2:terrain-from-float-array.png"><img src="/resources/jme2-terrain-from-float-array.png" class="media" alt="" /></a>
</p>

<p>
Important things to note:
</p>
<ul>
<li class="level1"><div class="li"> Low values (e.g. 0 or 50) are valeys.</div>
</li>
<li class="level1"><div class="li"> High values (e.g. 200, 255) are hills.</div>
</li>
<li class="level1"><div class="li"> The heightmap only specifies a few points, and the engine interpolates the rest. Interpolation is more efficient than creating a model with several millions vertices.</div>
</li>
</ul>

<p>
When looking at Java data types to hold an array of floats between 0 and 255, the Image class comes to mind. Storing a terrain's height values as a grayscale image has one big advantage: The outcome is a very userfriendly, like a topographical map:
</p>
<ul>
<li class="level1"><div class="li"> Low values (e.g. 0 or 50) are dark gray – these are valleys.</div>
</li>
<li class="level1"><div class="li"> High values (e.g. 200, 255) are light grays – these are hills.</div>
</li>
</ul>

<p>
Look at the next screenshot: In the top left you see a 128×128 grayscale image (heightmap) that was used as a base to generate the depicted terrain. To make the hilly shape better visible, the mountain tops are colored white, valleys brown, and the areas inbetween green:
</p>

<p>
<a href="/resources/jme2-terrain-from-heightmap.png" class="media" title="jme2:terrain-from-heightmap.png"><img src="/resources/jme2-terrain-from-heightmap.png" class="media" alt="" /></a>}
</p>

<p>
In a real game, you will want to use more complex and smoother terrains than the simple heightmaps shown here. Heightmaps typically have square sizes of 512×512 or 1024×1024, and contain hundred thousands to 1 million height values. No matter which size, the concept is the same as described here.
</p>

</div>
<!-- EDIT3 SECTION "What is a Heightmap?" [4466-6264] -->
<h3 class="sectionedit4" id="looking_at_the_heightmap_code">Looking at the Heightmap Code</h3>
<div class="level3">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/mountains512.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="128" height="128" /></a>
</p>

<p>
The first step of terrain creation is the heightmap. You can create one yourself in any standard graphic application. Make sure it has the following properties:
</p>
<ul>
<li class="level1"><div class="li"> The size must be square, and a power of two.</div>
<ul>
<li class="level2"><div class="li"> Examples: 128×128, 256×256, 512×512, 1024×1024</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Color mode must be 255 grayscales.</div>
<ul>
<li class="level2"><div class="li"> Don't supply a color image, it will be interpreted as grayscale, with possibly weird results.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Save the map as a .jpg or .png image file</div>
</li>
</ul>

<p>
The file <code>mountains512.png</code> that you see here is a typical example of an image heightmap.
</p>

<p>
Here is how you create the heightmap object in your jME code:
</p>
<ol>
<li class="level1"><div class="li"> Create a Texture object.</div>
</li>
<li class="level1"><div class="li"> Load your prepared heightmap image into the texture object.</div>
</li>
<li class="level1"><div class="li"> Create an AbstractHeightmap object from an ImageBasedHeightMap. <br />
It requires an image from a JME Texture.</div>
</li>
<li class="level1"><div class="li"> Load the heightmap.</div>
</li>
</ol>
<pre class="code java">    AbstractHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
    Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/mountains512.png"</span><span class="br0">)</span><span class="sy0">;</span>
    heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    heightmap.<span class="me1">load</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Looking at the Heightmap Code" [6265-7518] -->
<h2 class="sectionedit5" id="what_is_texture_splatting">What is Texture Splatting?</h2>
<div class="level2">

<p>
Previously you learned how to create a material for a simple shape such as a cube. All sides of the cube have the same color. You can apply the same material to a terrain, but then you have one big meadow, one big rock desert, etc. This is not always what you want.
</p>

<p>
Texture splatting allows you create a custom material, and “paint” textures on it like with a “paint brush”. This is very useful for terrains: As you see in the example here, you can paint a grass texture into the valleys, a dirt texture onto the mountains, and free-form roads inbetween.
</p>

<p>
</p><p></p><div class="notetip">The jMonkeyEngine SDK comes with a <a href="/sdk/terrain_editor.html" class="wikilink1" title="sdk:terrain_editor">TerrainEditor plugin</a>. Using the TerrainEditor plugin, you can sculpt the terrain with the mouse, and save the result as heightmap. You can paint textures on the terrain and the plugin saves the resulting splat textures as alphamap(s). The following paragraphs describe the manual process for you. You can choose to create the terrain by hand, or using the <a href="/sdk/terrain_editor.html" class="wikilink1" title="sdk:terrain_editor">TerrainEditor plugin</a>.
</div>


<p>
Splat textures are based on the <code>Terrain.j3md</code> material defintion. If you open the Terrain.j3md file, and look in the Material Parameters section, you see that you have several texture layers to paint on: <code>Tex1</code>, <code>Tex2</code>, <code>Tex3</code>, etc. 
</p>

<p>
Before you can start painting, you have to make a few decisions:
</p>
<ol>
<li class="level1"><div class="li"> Choose three textures. For example grass.jpg, dirt.jpg, and road.jpg. <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/road.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_splat_road.jpg" alt="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_splat_road.jpg" width="64" height="64" /></a>  <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/dirt.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_splat_dirt.jpg" alt="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_splat_dirt.jpg" width="64" height="64" /></a> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/grass.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_splat_grass.jpg" alt="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_splat_grass.jpg" width="64" height="64" /></a></div>
</li>
<li class="level1"><div class="li"> You “paint” three texture layers by using three colors: Red, blue and, green. You arbitrarily decide that…</div>
<ol>
<li class="level2"><div class="li"> Red   is grass – red   is layer <code>Tex1</code>, so put the grass texture into Tex1.</div>
</li>
<li class="level2"><div class="li"> Green is dirt  – green is layer <code>Tex2</code>, so put the dirt  texture into Tex2.</div>
</li>
<li class="level2"><div class="li"> Blue  is roads – blue  is layer <code>Tex3</code>, so put the roads texture into Tex3.</div>
</li>
</ol>
</li>
</ol>

<p>
Now you start painting the texture:
</p>
<ol>
<li class="level1"><div class="li"> Make a copy of your terrains heightmap, <code>mountains512.png</code>. You want it as a reference for the shape of the landscape.</div>
</li>
<li class="level1"><div class="li"> Name the copy <code>alphamap.png</code>.</div>
</li>
<li class="level1"><div class="li"> Open <code>alphamap.png</code> in a graphic editor and switch the image mode to color image.</div>
<ol>
<li class="level2"><div class="li"> Paint the black valleys red – this will be the grass.</div>
</li>
<li class="level2"><div class="li"> Paint the white hills green – this will be the dirt of the mountains.</div>
</li>
<li class="level2"><div class="li"> Paint blue lines where you want roads to criss-cross the landscape.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> The end result should look similar to this:</div>
</li>
</ol>

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/mountains512.png"><img src="/resources/fetch.php" class="media" alt="" width="64" height="64" /></a> ⇒ <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/alphamap.png"><img src="/resources/fetch.php" class="media" alt="" width="64" height="64" /></a>
</p>

</div>
<!-- EDIT5 SECTION "What is Texture Splatting?" [7519-10438] -->
<h3 class="sectionedit6" id="looking_at_the_texturing_code">Looking at the Texturing Code</h3>
<div class="level3">

<p>
As usual, you create a Material object. Base it on the Material Definition <code>Terrain.j3md</code> that is included in the jME3 framework.
</p>
<pre class="code java">Material mat_terrain <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Terrain/Terrain.j3md"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Load four textures into this material. The first one, <code>Alpha</code>, is the alphamap that you just created.
</p>
<pre class="code java">mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Alpha"</span>,
    assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/alphamap.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The three other textures are the layers that you have previously decided to paint: grass, dirt, and road. You create texture objects and load the three textures as usual. Note how you assign them to their respective texture layers (Tex1, Tex2, and Tex3) inside the Material!
</p>
<pre class="code java">    <span class="co3">/** 1.2) Add GRASS texture into the red layer (Tex1). */</span>
    Texture grass <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/grass.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    grass.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex1"</span>, grass<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex1Scale"</span>, 64f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.3) Add DIRT texture into the green layer (Tex2) */</span>
    Texture dirt <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/dirt.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    dirt.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex2"</span>, dirt<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex2Scale"</span>, 32f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.4) Add ROAD texture into the blue layer (Tex3) */</span>
    Texture rock <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/road.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    rock.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex3"</span>, rock<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex3Scale"</span>, 128f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The individual texture scales (e.g. <code>mat_terrain.setFloat(“Tex3Scale”, 128f);</code>) depend on the size of the textures you use.
</p>
<ul>
<li class="level1"><div class="li"> You can tell you picked too small a scale if, for example, your road tiles appear like tiny grains of sand. </div>
</li>
<li class="level1"><div class="li"> You can tell you picked too big a scale if, for example, the blades of grass look like twigs.</div>
</li>
</ul>

<p>
Use <code>setWrap(WrapMode.Repeat)</code> to make the small texture fill the wide area. If the repetition is too visible, try adjusting the respective <code>Tex*Scale</code> value.
</p>

</div>
<!-- EDIT6 SECTION "Looking at the Texturing Code" [10439-12577] -->
<h2 class="sectionedit7" id="what_is_a_terrain">What is a Terrain?</h2>
<div class="level2">

<p>
Internally, the generated terrain mesh is broken down into tiles and blocks. This is an optimization to make culling easier. You do not need to worry about “tiles and blocks” too much, just use recommended values for now – 64 is a good start.
</p>

<p>
Let's assume you want to generate a 512×512 terrain. You already have created the heightmap object. Here are the steps that you perform everytime you create a new terrain.
</p>

<p>
Create a TerrainQuad with the following arguments:
</p>
<ol>
<li class="level1"><div class="li"> Specify a name: E.g. <code>my terrain</code>.</div>
</li>
<li class="level1"><div class="li"> Specify tile size: You want to terrain tiles of size 64×64, so you supply 64+1 = 65.</div>
<ul>
<li class="level2"><div class="li"> In general, 64 is a good starting value for terrain tiles.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Specify block size: Since you prepared a heightmap of size 512×512, you supply 512+1 = 513.</div>
<ul>
<li class="level2"><div class="li"> If you supply a block size of 2x the heightmap size (1024+1=1025), you get a stretched out, wider, flatter terrain.</div>
</li>
<li class="level2"><div class="li"> If you supply a block size 1/2 the heightmap size (256+1=257), you get a smaller, more detailed terrain.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Supply the 512×512 heightmap object that you created.</div>
</li>
</ol>

</div>
<!-- EDIT7 SECTION "What is a Terrain?" [12578-13661] -->
<h3 class="sectionedit8" id="looking_at_the_terrain_code">Looking at the Terrain Code</h3>
<div class="level3">

<p>
Here's the code:
</p>
<pre class="code">terrain = new TerrainQuad(
  "my terrain",               // name
  65,                         // tile size
  513,                        // block size
  heightmap.getHeightMap());  // heightmap</pre>

<p>
You have created the terrain object.
</p>
<ol>
<li class="level1"><div class="li"> Remember to apply the created material: <pre class="code java">terrain.<span class="me1">setMaterial</span><span class="br0">(</span>mat_terrain<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Remember to attach the terrain to the rootNode.<pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> If needed, scale and translate the terrain object, just like any other Spatial.</div>
</li>
</ol>

<p>
<strong>Tip:</strong> Terrain.j3md is an unshaded material definition, so you do not need a light source. You can also use TerrainLighting.j3md plus a light, if you want a shaded terrain.
</p>

</div>
<!-- EDIT8 SECTION "Looking at the Terrain Code" [13662-14424] -->
<h2 class="sectionedit9" id="what_is_lod_level_of_detail">What is LOD (Level of Detail)?</h2>
<div class="level2">

<p>
JME3 includes an optimization that adjusts the level of detail (LOD) of the rendered terrain depending on how close or far the camera is.
</p>
<pre class="code java">    TerrainLodControl control <span class="sy0">=</span> <span class="kw1">new</span> TerrainLodControl<span class="br0">(</span>terrain, getCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    terrain.<span class="me1">addControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Close parts of the terrain are rendered in full detail. Terrain parts that are further away are not clearly visible anyway, and JME3 improves performance by rendering them less detailed. This way you can afford to load huge terrains with no penalty caused by invisible details.
</p>

</div>
<!-- EDIT9 SECTION "What is LOD (Level of Detail)?" [14425-15017] -->
<h2 class="sectionedit10" id="exercises">Exercises</h2>
<div class="level2">

</div>
<!-- EDIT10 SECTION "Exercises" [15018-15040] -->
<h3 class="sectionedit11" id="exercise_1texture_layers">Exercise 1: Texture Layers</h3>
<div class="level3">

<p>
What happens when you swap two layers, for example <code>Tex1</code> and <code>Tex2</code>?
</p>
<pre class="code java">...
<span class="me1">mat_terrain</span>.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex2"</span>, grass<span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">mat_terrain</span>.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex1"</span>, dirt<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You see it's easier to swap layers in the code, than to change the colors in the alphamap.
</p>

</div>
<!-- EDIT11 SECTION "Exercise 1: Texture Layers" [15041-15350] -->
<h3 class="sectionedit12" id="exercise_2randomized_terrains">Exercise 2: Randomized Terrains</h3>
<div class="level3">

<p>
The following three lines generate the heightmap object based on your user-defined image:
</p>
<pre class="code java">    AbstractHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
    Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
        <span class="st0">"Textures/Terrain/splat/mountains512.png"</span><span class="br0">)</span><span class="sy0">;</span>
    heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Instead, you can also let JME3 generate a random landscape for you:
</p>
<ol>
<li class="level1"><div class="li"> What result do you get when you replace the above three heightmap lines by the following lines and run the sample?<pre class="code java">HillHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
HillHeightMap.<span class="me1">NORMALIZE_RANGE</span> <span class="sy0">=</span> <span class="nu0">100</span><span class="sy0">;</span> <span class="co1">// optional</span>
<span class="kw1">try</span> <span class="br0">{</span>
    heightmap <span class="sy0">=</span> <span class="kw1">new</span> HillHeightMap<span class="br0">(</span><span class="nu0">513</span>, <span class="nu0">1000</span>, <span class="nu0">50</span>, <span class="nu0">100</span>, <span class="br0">(</span><span class="kw4">byte</span><span class="br0">)</span> <span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// byte 3 is a random seed</span>
<span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> ex<span class="br0">)</span> <span class="br0">{</span>
    ex.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Change one parameter at a time, and the run the sample again. Note the differences. Can you find out which of the values has which effect on the generated terrain (look at the javadoc also)?</div>
<ul>
<li class="level2"><div class="li"> Which value controls the size?</div>
<ul>
<li class="level3"><div class="li"> What happens if the size is not a square number +1 ?</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> Which value controls the number of hills generated?</div>
</li>
<li class="level2"><div class="li"> Which values control the size and steepness of the hills?</div>
<ul>
<li class="level3"><div class="li"> What happens if the min is bigger than or equal to max? </div>
</li>
<li class="level3"><div class="li"> What happens if both min and max are small values (e.g. 10/20)?</div>
</li>
<li class="level3"><div class="li"> What happens if both min and max are large values (e.g. 1000/1500)?</div>
</li>
<li class="level3"><div class="li"> What happens if min and max are very close(e.g. 1000/1001, 20/21)? Very far apart (e.g. 10/1000)?</div>
</li>
</ul>
</li>
</ul>
</li>
</ol>

<p>
You see the variety of hilly landscapes that can be generated using this method.
</p>

<p>
</p><p></p><div class="notetip">For this exercise, you can keep using the splat Material from the sample code above. Just don't be surprised that the Material does not match the shape of the newly randomized landscape. If you want to generate real matching splat textures for randomized heightmaps, you need to write a custom method that, for example, creates an alphamap from the heightmap by replacing certain grayscales with certain RGB values.
</div>


</div>
<!-- EDIT12 SECTION "Exercise 2: Randomized Terrains" [15351-17411] -->
<h3 class="sectionedit13" id="exercise_3solid_terrains">Exercise 3: Solid Terrains</h3>
<div class="level3">

<p>
Can you combine what you learned here and in <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a>, and <a href="/jme3/advanced/terrain_collision.html" class="wikilink1" title="jme3:advanced:terrain_collision">make the terrain solid</a>?
</p>

</div>
<!-- EDIT13 SECTION "Exercise 3: Solid Terrains" [17412-17581] -->
<h2 class="sectionedit14" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned how to create terrains that are more efficient than loading one giant model. You know how to generate random or create handmade heightmaps. You can add a LOD control to render large terrains faster. You are aware that you can combine what you learned about collision detection to make the terrain solid to a physical player. You are also able to texture a terrain “like a boss” using layered Materials and texture splatting. You are aware that the jMonkeyEngine SDK provides a TerrainEditor that helps with most of these manual tasks.
</p>

<p>
Do you want to hear your players say “ouch!” when they bump into a wall or fall off a hill? Continue with learning <a href="/jme3/beginner/hello_audio.html" class="wikilink1" title="jme3:beginner:hello_audio">how to add sound</a> to your game.
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/terrain_collision.html" class="wikilink1" title="jme3:advanced:terrain_collision">Terrain Collision</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/heightmap.html" class="wikilink1" title="tag:heightmap" rel="tag">heightmap</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/terrain.html" class="wikilink1" title="tag:terrain" rel="tag">terrain</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>
</span></div>

</div>
<!-- EDIT14 SECTION "Conclusion" [17582-] -->
