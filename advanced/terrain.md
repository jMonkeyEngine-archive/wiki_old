---
title: TerraMonkey - The jMonkeyEngine Terrain System
---
<h1 class="sectionedit1" id="terramonkey_-_the_jmonkeyengine_terrain_system">TerraMonkey - The jMonkeyEngine Terrain System</h1>
<div class="level1">

<p>
The goal of TerraMonkey is to provide a base implementation that will be usable for 80% of people's goals, while providing tools and a good foundation for the other 20% to build off of. Check out the videos in the following announcements:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/2011/06/17/infinite-terrains-with-terraingrid-new-features-in-terramonkey/" class="urlextern" title="http://hub.jmonkeyengine.org/2011/06/17/infinite-terrains-with-terraingrid-new-features-in-terramonkey/" rel="nofollow">New features</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/2011/07/03/terramonkey-more-textures-tools-and-undo/" class="urlextern" title="http://hub.jmonkeyengine.org/2011/07/03/terramonkey-more-textures-tools-and-undo/" rel="nofollow">More textures and Tools</a></div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "TerraMonkey - The jMonkeyEngine Terrain System" [1-541] -->
<h2 class="sectionedit2" id="overview">Overview</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.org/wp-content/uploads/2011/07/terrain-blogpost-july.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="400" height="300" /></a>
</p>

<p>
TerraMonkey is a GeoMipMapping quad tree of terrain tiles that supports real time editing and texture splatting. That's a mouth full! Lets look at each part:
</p>
<ul>
<li class="level1"><div class="li"> <strong>GeoMipMapping:</strong> a method of changing the level of detail (LOD) of geometry tiles based on how far away they are from the camera. Between the edges of two tiles, it will seam those edges together so you don't get gaps or holes. For an in-depth read on how it works, here is a pdf <a href="http://www.flipcode.com/archives/article_geomipmaps.pdf" class="urlextern" title="http://www.flipcode.com/archives/article_geomipmaps.pdf" rel="nofollow">http://www.flipcode.com/archives/article_geomipmaps.pdf</a>.</div>
</li>
<li class="level1"><div class="li"> <strong>Quad Tree:</strong> The entire terrain structure is made up of TerrainPatches (these hold the actual meshes) as leaves in a quad tree (TerrainQuad). TerrainQuads are subdivided by 4 until they reach minimum size, then a TerrainPatch is created, and that is where the actual geometry mesh lives. This allows for fast culling of the terrain that you can't see.</div>
</li>
<li class="level1"><div class="li"> <strong>Splatting:</strong> The ability to paint multiple textures onto your terrain. What differs here from JME2 is that this is all done in a shader, no more render passes. So it performs much faster.</div>
</li>
<li class="level1"><div class="li"> <strong>Real-time editing:</strong> <a href="/sdk/terrain_editor.html" class="wikilink1" title="sdk:terrain_editor">TerraMonkey terrains are editable in jMonkeyEngine SDK</a>, and you are able to modify them in real time, for example by raising and lowering the terrain.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Overview" [542-1914] -->
<h3 class="sectionedit3" id="current_features">Current Features:</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Support for 16 splat textures. You use a custom combination of Diffuse, Normal, Specular, and Glow Maps.</div>
</li>
<li class="level1"><div class="li"> GeoMipMapping: LodControl optimizes the level of detail</div>
</li>
<li class="level1"><div class="li"> Terrain can be randomized or generated from a heightmap</div>
</li>
<li class="level1"><div class="li"> jMonkeyEngine SDK terrain editor</div>
</li>
<li class="level1"><div class="li"> Streaming <a href="/jme3/advanced/endless_terraingrid.html" class="wikilink1" title="jme3:advanced:endless_terraingrid">terrain grid</a> (ie. “infinite” terrain)</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Current Features:" [1915-2301] -->
<h3 class="sectionedit4" id="planned_features">Planned Features:</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Hydraulic erosion and procedural texture generation</div>
</li>
<li class="level1"><div class="li"> Holes: caves, cliffs</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Planned Features:" [2302-2411] -->
<h2 class="sectionedit5" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTest.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTest.java" rel="nofollow">TerrainTest.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTestAdvanced.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTestAdvanced.java" rel="nofollow">TerrainTestAdvanced.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTestCollision.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTestCollision.java" rel="nofollow">TerrainTestCollision.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTestModifyHeight.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTestModifyHeight.java" rel="nofollow">TerrainTestModifyHeight.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTestReadWrite.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/terrain/TerrainTestReadWrite.java" rel="nofollow">TerrainTestReadWrite.java</a></div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Sample Code" [2412-3183] -->
<h2 class="sectionedit6" id="geo_mip_mapping">Geo Mip Mapping</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-terrain-lod-high-medium-low.png" class="media" title="jme3:advanced:terrain-lod-high-medium-low.png"><img src="/resources/jme3-advanced-terrain-lod-high-medium-low.png" class="mediaright" title="The wiremesh of a terrain with visible differences in levels of detail (LOD)" alt="The wiremesh of a terrain with visible differences in levels of detail (LOD)" /></a>
</p>

<p>
You have seen GeoMipMapping implemented in games before. This is where the farther away terrain has fewer polygons, and as you move closer, more polygons fill in. The whole terrain is divided into a grid of patches, and each one has its own level of detail (LOD). The GeoMipMapping algorithm looks at each patch, and its neighbours, to determine how to render the geometry. It will seam the edges between two patches with different LOD.
</p>

<p>
GeoMipMapping often leads to “popping” where you see the terrain switch from one LOD to another. TerraMonkey has been designed so you can swap out different LOD calculation algorithms based on what will look best for your game. You can do this with the LodCalculator interface.
</p>

<p>
GeoMipMapping in TerraMonkey has been split into several parts: the terrain quad tree, and the LODGeomap. The geomap deals with the actual LOD and seaming algorithm. So if you want a different data structure for your terrain system, you can re-use this piece of code. The quad tree (TerrainQuad and TerrainPatch) provide a means to organize the LODGeomaps, notify them of their neighbour's LOD change, and to update the geometry when the LOD does change. To change the LOD it does this by changing the index buffer of the triangle strip, so the whole geometry doesn't have to be re-loaded onto the video card. If you are eager, you can read up more detail how GeoMipMapping works here: <a href="http://www.flipcode.com/archives/article_geomipmaps.pdf" class="urlextern" title="http://www.flipcode.com/archives/article_geomipmaps.pdf" rel="nofollow">www.flipcode.com/archives/article_geomipmaps.pdf</a>
</p>

</div>
<!-- EDIT6 SECTION "Geo Mip Mapping" [3184-4795] -->
<h2 class="sectionedit7" id="terrain_quad_tree">Terrain Quad Tree</h2>
<div class="level2">

<p>
TerraMonkey is a quad tree. Each node is a TerrainQuad, and each leaf is a TerrainPatch. A TerrainQuad has either 4 child TerrainQuads, or 4 child TerrainPatches. The TerrainPatch holds the actual mesh geometry. This structure is almost exactly the same as JME2's TerrainPage system. Except now each leaf has a reference to its neighbours, so it doesn't ever have to traverse the tree to get them.
</p>

</div>
<!-- EDIT7 SECTION "Terrain Quad Tree" [4796-5225] -->
<h2 class="sectionedit8" id="texture_splatting">Texture Splatting</h2>
<div class="level2">

<p>
When you “slap” a texture on a mesh, the whole mesh looks the same. For big meshes (such as terrains) that is undesirable because it looks very boring (your whole landscape would be all rock, or all grass, or all sand). Texture Splatting is a technique that lets you “paint” several textures into one combined texure. Each of the splat textures has an opacity value so you can define where it is visible in the final overall texture.
</p>

<p>
The default material for TerraMonkey is TerrainLighting.j3md. This material combines several texture maps to produce the final custom texture. Remember, Diffuse Maps are the main textures that define the look; optionally, each Diffuse Map can be enhanced with a Normal Map; Alpha Maps describe the opacity of each Diffuse Map used (one color –red, green, blue, or alpha– stands for one Diffuse Map's opacity); Glow and Specular Maps define optional effects. 
</p>

<p>
</p><p></p><div class="noteimportant">We recommend to <a href="http://jmonkeyengine.org/wiki/doku.php/sdk:terrain_editor" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/sdk:terrain_editor" rel="nofollow">create and edit Splat Textures for terrains visually in the jMonkeyEngine SDK</a>, and not do it manually. If you are simply curious about how the SDK's terrain texture plugin works, or if you indeed want to generate materials manually, then read on for the implementation details.
</div>


<p>
Here are the names of TerrainLighting.j3md's material properties:
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/mountains512.png"><img src="/resources/fetch.php" class="mediaright" title="A heightmap encodes the topological highs and lows of the terrain" alt="A heightmap encodes the topological highs and lows of the terrain" width="128" height="128" /></a>
</p>
<ul>
<li class="level1"><div class="li"> 1-3 Alpha Maps</div>
<ul>
<li class="level3"><div class="li"> <code>AlphaMap</code></div>
</li>
<li class="level3"><div class="li"> <code>AlphaMap_1</code></div>
</li>
<li class="level3"><div class="li"> <code>AlphaMap_2</code></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> 12 Diffuse and/or Normal Maps (either in 6 pairs, or 12 stand-alone Diffuse Maps)</div>
<ul>
<li class="level3"><div class="li"> <code>DiffuseMap</code>, <code>DiffuseMap_0_scale</code>, <code>NormalMap</code> </div>
</li>
<li class="level3"><div class="li"> <code>DiffuseMap_1</code>, <code>DiffuseMap_1_scale</code>, <code>NormalMap_1</code></div>
</li>
<li class="level3"><div class="li"> <code>DiffuseMap_2</code>, <code>DiffuseMap_2_scale</code>, <code>NormalMap_2</code></div>
</li>
<li class="level3"><div class="li"> <code>DiffuseMap_3</code>, <code>DiffuseMap_3_scale</code>, <code>NormalMap_3</code> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/alphamap.png"><img src="/resources/fetch.php" class="mediaright" title="An alpha map can describe where 4 textures are painted onto the terrain." alt="An alpha map can describe where 4 textures are painted onto the terrain." width="128" height="128" /></a></div>
</li>
<li class="level3"><div class="li"> <code>DiffuseMap_4</code>, <code>DiffuseMap_4_scale</code>, <code>NormalMap_4</code></div>
</li>
<li class="level3"><div class="li"> … </div>
</li>
<li class="level3"><div class="li"> <code>DiffuseMap_11</code>, <code>DiffuseMap_11_scale</code>, <code>NormalMap_11</code></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> “Light” maps</div>
<ul>
<li class="level3"><div class="li"> <code>GlowMap</code></div>
</li>
<li class="level3"><div class="li"> <code>SpecularMap</code></div>
</li>
</ul>
</li>
</ul>

<p>
<strong>Note:</strong> <code>DiffuseMap_0_scale</code> is a float value (e.g. 1.0f); you must specify one scale per Diffuse Map.
</p>

<p>
OpenGL supports a maximum of 16 <em>samplers</em> in any given shader. This means you can only use a subset of material properties at the same time if you use the terrain's default lighting shader (TerrainLighting.j3md)!
</p>

<p>
Adhere to the following constraints:
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/road.jpg"><img src="/resources/fetch.php" class="mediaright" title="The Diffuse Map of one of the terrain textures depicts the colors of a paved surface" alt="The Diffuse Map of one of the terrain textures depicts the colors of a paved surface" /></a>
</p>
<ul>
<li class="level1"><div class="li"> 1-12 Diffuse Maps. One Diffuse Map is the minimum!</div>
</li>
<li class="level1"><div class="li"> 1-3 Alpha Maps. For each 4 Diffuse Maps, you need 1 more Alpha Map!</div>
</li>
<li class="level1"><div class="li"> 0-6 Normal Maps. Diffuse Maps &amp; Normal Maps always come in pairs!</div>
</li>
<li class="level1"><div class="li"> 0 or 1 Glow Map</div>
</li>
<li class="level1"><div class="li"> 0 or 1 Specular Map.</div>
</li>
<li class="level1"><div class="li"> <strong>The sum of all textures used must be 16, or less.</strong></div>
</li>
</ul>

<p>
Here are some common examples what this means:
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/splat/road_normal.png"><img src="/resources/fetch.php" class="mediaright" title="The Normal Map of one of the terrain textures depicts the bumpiness of a paved surface" alt="The Normal Map of one of the terrain textures depicts the bumpiness of a paved surface" /></a>
</p>
<ul>
<li class="level1"><div class="li"> 3 Alpha + 11 Diffuse + 1 Normal. </div>
</li>
<li class="level1"><div class="li"> 3 Alpha + 11 Diffuse + 1 Glow. </div>
</li>
<li class="level1"><div class="li"> 3 Alpha + 11 Diffuse + 1 Specular. </div>
</li>
<li class="level1"><div class="li"> 3 Alpha + 10 Diffuse + 3 Normal. </div>
</li>
<li class="level1"><div class="li"> 3 Alpha + 10 Diffuse + 1 Normal + 1 Glow + 1 Specular. </div>
</li>
<li class="level1"><div class="li"> 2 Alpha + 8 Diffuse + 6 Normal. </div>
</li>
<li class="level1"><div class="li"> 2 Alpha + 6 Diffuse + 6 Normal + 1 Glow + 1 Specular. </div>
</li>
<li class="level1"><div class="li"> 1 Alpha + 3 Diffuse + 3 Normal + 1 Glow + 1 Specular (rest unused)</div>
</li>
</ul>

<p>
You can hand-paint Alpha, Diffuse, Glow, and Specular maps in a drawing program, like Photoshop. Define each splat texture in the Alpha Map in either Red, Green, Blue, or Alpha (=RGBA). The JmeTests project bundled in the <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> includes some image files that show you how this works. The example images show a terrain heightmap next to its Alpha Map (which has been prepare for 3 Diffuse Maps), and one examplary Diffuse/Normal Map pair.
</p>

</div>
<!-- EDIT8 SECTION "Texture Splatting" [5226-9523] -->
<h2 class="sectionedit9" id="code_sampleterrainj3md">Code Sample: Terrain.j3md</h2>
<div class="level2">

<p>
This example shows the simpler material definition <code>Terrain.j3md</code>, which only supports 1 Alpha Map, 3 Diffuse Maps, 3 Normal Maps, and does not support Phong illumination. It makes the exmaple shorter – TerrainLighting.j3md works accordingly (The list of material properties see above. Links to extended sample code see above.)
</p>

<p>
First, we load our textures and the heightmap texture for the terrain
</p>
<pre class="code java"><span class="co1">// Create material from Terrain Material Definition</span>
matRock <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Terrain/Terrain.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Load alpha map (for splat textures)</span>
matRock.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Alpha"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/alphamap.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// load heightmap image (for the terrain heightmap)</span>
Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/mountains512.png"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// load grass texture</span>
Texture grass <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/grass.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
grass.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
matRock.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex1"</span>, grass<span class="br0">)</span><span class="sy0">;</span>
matRock.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex1Scale"</span>, 64f<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// load dirt texture</span>
Texture dirt <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/dirt.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
dirt.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
matRock.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex2"</span>, dirt<span class="br0">)</span><span class="sy0">;</span>
matRock.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex2Scale"</span>, 32f<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// load rock texture</span>
Texture rock <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/road.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
rock.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
matRock.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex3"</span>, rock<span class="br0">)</span><span class="sy0">;</span>
matRock.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex3Scale"</span>, 128f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
We create the heightmap from the <code>heightMapImage</code>.
</p>
<pre class="code java">AbstractHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span>, 1f<span class="br0">)</span><span class="sy0">;</span>
heightmap.<span class="me1">load</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Next we create the actual terrain.
</p>
<ul>
<li class="level1"><div class="li"> The terrain tiles are 65×65.</div>
</li>
<li class="level1"><div class="li"> The total size of the terrain is 513×513, but it can easily be up to 1025×1025.</div>
</li>
<li class="level1"><div class="li"> It uses the heightmap to generate the height values.</div>
</li>
</ul>
<pre class="code java">terrain <span class="sy0">=</span> <span class="kw1">new</span> TerrainQuad<span class="br0">(</span><span class="st0">"terrain"</span>, <span class="nu0">65</span>, <span class="nu0">513</span>, heightmap.<span class="me1">getHeightMap</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
terrain.<span class="me1">setMaterial</span><span class="br0">(</span>matRock<span class="br0">)</span><span class="sy0">;</span>
terrain.<span class="me1">setLocalScale</span><span class="br0">(</span>2f, 1f, 2f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// scale to make it less steep</span>
List<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span> cameras <span class="sy0">=</span> <span class="kw1">new</span> ArrayList<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
cameras.<span class="me1">add</span><span class="br0">(</span>getCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
TerrainLodControl control <span class="sy0">=</span> <span class="kw1">new</span> TerrainLodControl<span class="br0">(</span>terrain, cameras<span class="br0">)</span><span class="sy0">;</span>
terrain.<span class="me1">addControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
PS: As an alternative to an image-based height map, you can also generate a Hill hightmap:
</p>
<pre class="code java">heightmap <span class="sy0">=</span> <span class="kw1">new</span> HillHeightMap<span class="br0">(</span><span class="nu0">1025</span>, <span class="nu0">1000</span>, <span class="nu0">50</span>, <span class="nu0">100</span>, <span class="br0">(</span><span class="kw4">byte</span><span class="br0">)</span> <span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT9 SECTION "Code Sample: Terrain.j3md" [9524-] -->
