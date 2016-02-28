---
title: jMonkeyEngine SDK: Terrain Editor
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkterrain_editor">jMonkeyEngine SDK: Terrain Editor</h1>
<div class="level1">

<p>
The terrain editor lets you create, modify, and paint terrain.
<a href="/resources/wp-uploads-2011-07-terrain-blogpost-july.png" class="media wikilink2" title="wp-uploads:2011:07:terrain-blogpost-july.png"><img src="/resources/wp-uploads-2011-07-terrain-blogpost-july.png" class="mediacenter" alt="" width="416" height="375" /></a>
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Terrain Editor" [1-171] -->
<h2 class="sectionedit2" id="controls">Controls</h2>
<div class="level2">

<p>
Terrain controls are the same as the Scene Composer, you rotate the camera with the left mouse button and pan the camera with the right mouse button. Until you select one of the terrain tools in the toolbar, then the controls change for that tool. Then left mouse button will use that tool: painting, raising/lowering terrain, etc. The right mouse button might do something, depending on the tool.
</p>

</div>
<!-- EDIT2 SECTION "Controls" [172-591] -->
<h2 class="sectionedit3" id="creating_terrain">Creating Terrain</h2>
<div class="level2">

<p>
To create terrain, first select a node (probably your root node) in your scene.<br />

<a href="/resources/sdk-sdk-terrain-tut-selectnode.png" class="media" title="sdk:sdk-terrain-tut-selectnode.png"><img src="/resources/sdk-sdk-terrain-tut-selectnode.png" class="media" alt="" /></a><br />

Then click the add terrain button.<br />

<a href="/resources/sdk-sdk-terrain-tut-addterrain.png" class="media" title="sdk:sdk-terrain-tut-addterrain.png"><img src="/resources/sdk-sdk-terrain-tut-addterrain.png" class="media" alt="" /></a><br />

This will pop up the Create Terrain wizard that will walk you through the steps for creating terrain. Make sure you decide now how large you want your terrain to be and how detailed you want the textures to be as you cannot change it later on!
</p>

<p>
In order to see the terrain, you will need to add light to your scene. To do this, right-click the root node in the SceneExplorer window and select “Add Light→Directional Light”
</p>

</div>
<!-- EDIT3 SECTION "Creating Terrain" [592-1248] -->
<h3 class="sectionedit4" id="step_1terrain_size">Step 1: Terrain Size</h3>
<div class="level3">

<p>
Here you determine the size of your terrain, the total size and the patch size. You should probably leave the patch size alone. But the total size should be defined; this is how big your terrain is.
</p>

</div>
<!-- EDIT4 SECTION "Step 1: Terrain Size" [1249-1479] -->
<h3 class="sectionedit5" id="step_2heightmap">Step 2: Heightmap</h3>
<div class="level3">

<p>
Here you can select a heightmap generation technique to give you a default/random look of the terrain. You can also select a heightmap image to pre-define how your terrain looks.
By default, it will give you a flat terrain.
</p>

</div>
<!-- EDIT5 SECTION "Step 2: Heightmap" [1480-1732] -->
<h3 class="sectionedit6" id="step_3alpha_image_detail">Step 3: Alpha Image Detail</h3>
<div class="level3">

<p>
This step determines how large the alpha blend images are for your terrain.  The smaller the alpha image, the less detailed you can paint the terrain. Play around with this to see how big you need it to be. Remember that terrain does not have to be that detailed, and is often covered by vegetation, rocks, and other items. So having a really detailed texture is not always necessary.
</p>

</div>
<!-- EDIT6 SECTION "Step 3: Alpha Image Detail" [1733-2155] -->
<h2 class="sectionedit7" id="modifying_terrain">Modifying Terrain</h2>
<div class="level2">

<p>
Right now there are two terrain modification tools: raise and lower terrain.<br />

<a href="/resources/sdk-sdk-terrain-raise-lower.png" class="media" title="sdk:sdk-terrain-raise-lower.png"><img src="/resources/sdk-sdk-terrain-raise-lower.png" class="media" alt="" /></a><br />

There are two sliders that affect how these tools operate:
</p>
<ul>
<li class="level1"><div class="li"> Radius: how big the brush is</div>
</li>
<li class="level1"><div class="li"> Weight/Height: how much impact the brush has</div>
</li>
</ul>

<p>
Once a tool is selected, you will see the tool marker (now an ugly wire sphere) on the map where your mouse is. Click and drag on the terrain to see the tool change the height of the terrain.
</p>

</div>
<!-- EDIT7 SECTION "Modifying Terrain" [2156-2637] -->
<h2 class="sectionedit8" id="painting_terrain">Painting Terrain</h2>
<div class="level2">

<p>
Your terrain comes with one diffuse default texture, and you can have up to 12 total diffuse textures. It also allows you to add normal maps to each texture layer. There can be a maximum of 13 textures, including Diffuse and Normal (3 textures are taken up by alpha maps).
</p>

<p>
All of the textures can be controlled in the Texture Layer table by clicking on the textures.
There are two sliders that affect how the paint tool operates:
</p>
<ul>
<li class="level1"><div class="li"> Radius: how big the brush is</div>
</li>
<li class="level1"><div class="li"> Weight/Height: how much impact the brush has.</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Painting Terrain" [2638-3182] -->
<h3 class="sectionedit9" id="adding_a_new_texture_layer">Adding a new texture layer</h3>
<div class="level3">

<p>
Adds a new texture layer to the terrain. The will be drawn over top of the other texture layers listed above it in the list.
</p>

<p>
<a href="/resources/sdk-sdk-terrain-addtexture.png" class="media" title="sdk:sdk-terrain-addtexture.png"><img src="/resources/sdk-sdk-terrain-addtexture.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT9 SECTION "Adding a new texture layer" [3183-3383] -->
<h3 class="sectionedit10" id="changing_the_diffuse_texture">Changing the diffuse texture</h3>
<div class="level3">

<p>
Click on the diffuse texture image in the texture table. This will pop up a window with the available textures in your assets directory.
</p>

<p>
<a href="/resources/sdk-sdk-terrain-editdiffuse.png" class="media" title="sdk:sdk-terrain-editdiffuse.png"><img src="/resources/sdk-sdk-terrain-editdiffuse.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT10 SECTION "Changing the diffuse texture" [3384-3599] -->
<h3 class="sectionedit11" id="adding_a_normal_map_to_the_texture_layer">Adding a normal map to the texture layer</h3>
<div class="level3">

<p>
When you add a texture layer, by default it does not add a normal map for you. To add one, click on the button next to the diffuse texture for that texture layer. This will pop up the texture browser. Select a texture and hit Ok, and you are done.<br />

<a href="/resources/sdk-sdk-terrain-addnormaltexture.png" class="media" title="sdk:sdk-terrain-addnormaltexture.png"><img src="/resources/sdk-sdk-terrain-addnormaltexture.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT11 SECTION "Adding a normal map to the texture layer" [3600-3943] -->
<h3 class="sectionedit12" id="removing_a_normal_map_from_the_texture_layer">Removing a normal map from the texture layer</h3>
<div class="level3">

<p>
To remove a normal map from the texture layer, hit the normal map button for that texture layer again, and deselect the texture. Then hit Ok and the texture should be removed.
</p>

</div>
<!-- EDIT12 SECTION "Removing a normal map from the texture layer" [3944-4175] -->
<h3 class="sectionedit13" id="changing_the_texture_scale">Changing the texture scale</h3>
<div class="level3">

<p>
The field in the table to the right of the diffuse and normal textures for your texture layer is the scale. Changing that value changes the scale of the texture.<br />

<a href="/resources/sdk-sdk-terrain-texturescale.png" class="media" title="sdk:sdk-terrain-texturescale.png"><img src="/resources/sdk-sdk-terrain-texturescale.png" class="media" alt="" /></a><br />

You will notice that the scale changes when you switch between Tri-Planar and normal texture mapping. Tri-planar mapping does not use the texture coordinates of the geometry, but real world coordinates. And because of this, in order for the texture to look the same when you switch between the two texture mapping methods, the terrain editor will automatically convert the scales for you.
Essentially if your scale in normal texture coordinates is 16, then for tri-planar gets converted like this: 1/terrainSize/16
</p>

</div>
<!-- EDIT13 SECTION "Changing the texture scale" [4176-4932] -->
<h3 class="sectionedit14" id="tri-planar_texture_mapping">Tri-planar texture mapping</h3>
<div class="level3">

<p>
Tri-planar texture mapping is recommended if you have lots of near-vertical terrain. With normal texture mapping the textures can look stretched because it is rendered on the one plane: X-Z. Tri-planar mapping renders the textures on three planes: X-Z, X-Y, Z-Y; and blends them together based on what plane the normal of the triangle is facing most on.
This makes the terrain look much better, but it does have a performance hit!
Here is an article on tri-planar mapping: <a href="http://http.developer.nvidia.com/GPUGems3/gpugems3_ch01.html" class="urlextern" title="http://http.developer.nvidia.com/GPUGems3/gpugems3_ch01.html" rel="nofollow">http://http.developer.nvidia.com/GPUGems3/gpugems3_ch01.html</a>
</p>

</div>
<!-- EDIT14 SECTION "Tri-planar texture mapping" [4933-5509] -->
<h3 class="sectionedit15" id="total_texture_count">Total texture count</h3>
<div class="level3">

<p>
Terrain will support a maximum of 12 diffuse texture. And a combined total of 13 diffuse and normal maps.
Most video cards are limited to 16 texture units (textures), and 3 are used behind the scenes of the terrain material for alpha blending of the textures, so you are left with a maximum of 13 textures.
</p>

</div>
<!-- EDIT15 SECTION "Total texture count" [5510-5847] -->
<h2 class="sectionedit16" id="generating_terrain_entropies_for_lod">Generating Terrain Entropies for LOD</h2>
<div class="level2">

<p>
If you are using the recommended PerspectiveLodCalculator for calculating LOD levels of the terrain, then you will want to pre-generate the entropy levels for the terrain. This is a slow process. If they are not pre-generated, the LOD control will generate them for you, but this will lag the user when they load the scene, and the terrain will flicker.
Use the 'Generate Entropies' button to pre-generate the entropies for the terrain, they will be saved with it.
Note that whenever you modify the height of the terrain, you should re-generate the entropies. Of course, don't do this every time, but maybe just before you are ready to send the map out for testing.
</p>

</div>
<!-- EDIT16 SECTION "Generating Terrain Entropies for LOD" [5848-6563] -->
<h2 class="sectionedit17" id="loading_terrain_into_your_game">Loading Terrain Into Your Game</h2>
<div class="level2">

<p>
There are a few things your code needs to do to load the terrain.
</p>
<ul>
<li class="level1"><div class="li"> You must first use the asset manager to load the scene, see the <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">hello asset tutorial</a>.</div>
</li>
<li class="level1"><div class="li"> The terrain (as you can see on the left in the editor) is a sub-node of the scene, so you have to write code to investigate the child nodes of the scene until you find the node that is the terrain, see <a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph">this tutorial for scene graph concepts</a>.</div>
</li>
<li class="level1"><div class="li"> You also have to set the camera on the LOD control in order for it to work correctly:</div>
</li>
</ul>
<pre class="code java">TerrainLodControl lodControl <span class="sy0">=</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span>terrain<span class="br0">)</span>.<span class="me1">getControl</span><span class="br0">(</span>TerrainLodControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">if</span> <span class="br0">(</span>lodControl <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span>
                lodControl.<span class="me1">setCamera</span><span class="br0">(</span>getCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>,
	<a href="/tag/terrain.html" class="wikilink1" title="tag:terrain" rel="tag">terrain</a>,
	<a href="/tag/asset.html" class="wikilink1" title="tag:asset" rel="tag">asset</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>
</span></div>

</div>
<!-- EDIT17 SECTION "Loading Terrain Into Your Game" [6564-] -->
