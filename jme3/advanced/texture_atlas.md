---
title: Optimization: Texture Atlas
---
<h1 class="sectionedit1" id="optimizationtexture_atlas">Optimization: Texture Atlas</h1>
<div class="level1">

<p>
The <code>jme3tools.optimize.TextureAtlas</code> allows combining multiple textures into one texture atlas.  Loading one geometry with one material is much more efficient than handling several geometries and materials. Optimally, you already export your textures as texture atlas from e.g. Blender.
</p>

<p>
<code>jme3tools.optimize.GeometryBatchFactory</code>, in contrast, only works if the geometries have only one material with textures.
</p>
<ol>
<li class="level1"><div class="li"> Create a TextureAtlas. </div>
</li>
<li class="level1"><div class="li"> Add textures to texture atlas, each texture goes onto one map (e.g. <code>DiffuseMap</code>). <br />
The image data is stored in a byte array for each named texture map. </div>
</li>
<li class="level1"><div class="li"> Later, you retrieve each map by name as a Texture, and use it in materials.</div>
</li>
</ol>

</div>
<!-- EDIT1 SECTION "Optimization: Texture Atlas" [1-732] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/tools/TestTextureAtlas.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/tools/TestTextureAtlas.java" rel="nofollow">TestTextureAtlas.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [733-910] -->
<h2 class="sectionedit3" id="api">API</h2>
<div class="level2">
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">TextureAtlas method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">addGeometry(g)</td><td class="col1">Add this geometry's DiffuseMap (or ColorMap), NormalMap, and SpecularMap to the atlas (if they exist). The DiffuseMap will automatically be the master map.</td>
	</tr>
	<tr class="row2">
		<td class="col0">addTexture(t, mapname)</td><td class="col1">Add a texture to the named master map.</td>
	</tr>
	<tr class="row3">
		<td class="col0">addTexture(t1,mapName,t2)</td><td class="col1">Add a texture t1 to the named secondary map, and make the location of texture t1 correspond to texture t2 on the master map. t2 can be Texture object or the String name of the texture.</td>
	</tr>
	<tr class="row4">
		<td class="col0">applyCoords(g)</td><td class="col1">Applies the texture coordinates to the geometries mesh. Short for the default, <code>applyCoords(geom, 0, geom.getMesh()</code>.</td>
	</tr>
	<tr class="row5">
		<td class="col0">applyCoords(g,offset,mesh)</td><td class="col1">Applies the texture coordinates at the given texture coord buffer offset to the mesh, if the DiffuseMap or ColorMap of the input geometry g exist in the atlas. The mesh can be <code>g.getMesh()</code>. Target buffer offset is between 0 and buffer.size().</td>
	</tr>
	<tr class="row6">
		<td class="col0">getAtlasTile(texture)</td><td class="col1">Get the <code>TextureAtlasTile</code> for the given Texture. The TextureAtlasTile objects contains info about this texture. such as size and location in the atlas.</td>
	</tr>
	<tr class="row7">
		<td class="col0">getAtlasTexture(mapName)</td><td class="col1">Creates a new atlas texture from the added textures for the given map name.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [928-2099] --><div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">TextureAtlasTile method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getHeight(), getWidth()</td><td class="col1">Gets the size of the texture.</td>
	</tr>
	<tr class="row2">
		<td class="col0">getX(), getY()</td><td class="col1">Gets the x and y coordinate inside the texture atlas where this texture can be found</td>
	</tr>
	<tr class="row3">
		<td class="col0">transformTextureCoords(inBuf,offset,outBuf)</td><td class="col1">Transforms the texture coordinates in a buffer from their original 0-1 values to the new values fitting to the location of the tile on the atlas texture.</td>
	</tr>
	<tr class="row4">
		<td class="col0">getLocation(l)</td><td class="col1">Get the transformed texture coordinate for a given input location.</td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [2101-2574] -->
</div>
<!-- EDIT3 SECTION "API" [911-2575] -->
<h2 class="sectionedit6" id="primary_and_secondary_maps">Primary and Secondary Maps</h2>
<div class="level2">

<p>
The helper methods that work with Geometry objects automatically consider the <code>DiffuseMap</code> (for Lighting.j3md-based Materials) or ColorMap (for Unshaded.j3md-based Materials) the <strong>master map</strong>, and additionally treat the <code>NormalMap</code> and <code>SpecularMap</code> as secondary maps, if they exist in the Geometry.
</p>
<ul>
<li class="level1"><div class="li"> The first map name that you supply becomes the <strong>master map</strong>. The master map defines locations on the atlas. Typically, you name the master map <code>DiffuseMap</code> (for Lighting.j3md) or <code>ColorMap</code> (for Unshaded.j3md). <br />
In general, if you want to use the texture with a certain shader, you should supply the map names that are specified in this shader's .j3md for clarity.</div>
</li>
<li class="level1"><div class="li"> Secondary textures (other map names, for example <code>SpecularMap</code> and <code>NormalMap</code> for Lighting.j3md) have to reference a existing texture on the master map, so the Atlas knows where to position the added texture on the secondary map. This is necessary because the maps share texture coordinates and thus need to be placed at the same location on both maps. If you do not share texture coordinates in your maps, use separate TextureAtlas classes.</div>
</li>
</ul>

<p>
You reference textures by their <strong>asset key name</strong>, this is what their “id” is. For each texture, the atlas stores its location. A texture with an existing key name is never added more than once to the atlas. You can access the information for each texture or geometry texture via helper methods.
</p>
<ul>
<li class="level1"><div class="li"> Textures are not scaled automatically, and your atlas needs to be created large enough to hold all textures. All methods that allow adding textures return false if the texture could not be added due to the atlas being full. </div>
</li>
<li class="level1"><div class="li"> Secondary textures (normal maps, specular maps etc.) have to be the same size as the main (e.g. DiffuseMap) texture.</div>
</li>
<li class="level1"><div class="li"> The TextureAtlas lets you change the texture coordinates of a mesh or geometry to point at the new locations of its texture inside the atlas (if the texture exists inside the atlas). ??</div>
</li>
</ul>

<p>
</p><p></p><div class="noteimportant">Note that models that use texture coordinates outside the 0-1 range (that is, they use repeating/wrapping textures) do not work correctly as their new coordinates leak into other parts of the atlas and thus display other textures instead of repeating the texture!
</div>


</div>
<!-- EDIT6 SECTION "Primary and Secondary Maps" [2576-4880] -->
<h2 class="sectionedit7" id="usage_examplescombine_geometries">Usage examples: Combine Geometries</h2>
<div class="level2">

<p>
Use <code>makeAtlasBatch</code> to turn several geometries that are loaded from a j3o file into one geometry:
</p>
<pre class="code java"> <span class="co1">// scene contains many geometries ared attached to one node:</span>
 Node scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/MyScene.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
 <span class="co1">// geom is one geometry containing all of these geometries together</span>
 Geometry geom <span class="sy0">=</span> TextureAtlas.<span class="me1">makeAtlasBatch</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span>
 rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Create a texture atlas and change the texture coordinates of one geometry:
</p>
<pre class="code java"> Node scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/MyScene.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
 
 <span class="co1">// Either auto-create texture Atlas from an existing node that has geometries...</span>
 TextureAtlas atlas <span class="sy0">=</span> TextureAtlas.<span class="me1">createAtlas</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span>
 
 <span class="co1">//... or create Atlas manually by adding textures (e.g. myDiffuseTexture) to the atlas, </span>
 TextureAtlas atlas <span class="sy0">=</span> <span class="kw1">new</span> TextureAtlas<span class="br0">(</span><span class="nu0">1024</span>,<span class="nu0">1024</span><span class="br0">)</span><span class="sy0">;</span>
 atlas.<span class="me1">addTexture</span><span class="br0">(</span>myDiffuseTexture, <span class="st0">"DiffuseMap"</span><span class="br0">)</span><span class="sy0">;</span> 
 
 <span class="co1">// ... or create Atlas manually by adding textured geometries (e.g. myGeometry) to the atlas:</span>
 TextureAtlas atlas <span class="sy0">=</span> <span class="kw1">new</span> TextureAtlas<span class="br0">(</span><span class="nu0">1024</span>,<span class="nu0">1024</span><span class="br0">)</span><span class="sy0">;</span>
 atlas.<span class="me1">addGeometry</span><span class="br0">(</span>MyGeometry<span class="br0">)</span><span class="sy0">;</span>
 
 <span class="co1">// Create material, load texture from Atlas, apply texture to material map.</span>
 Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>mgr, <span class="st0">"Common/MatDefs/Light/Lighting.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
 mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"DiffuseMap"</span>, atlas.<span class="me1">getAtlasTexture</span><span class="br0">(</span><span class="st0">"DiffuseMap"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
 <span class="co1">// Get one sub-geometry on which you want to use the Atlas, apply texture coordinates </span>
 <span class="co1">// of this geometry to the atlas, and replace the material.</span>
 Geometry geom <span class="sy0">=</span> scene.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"MyGeometry"</span><span class="br0">)</span><span class="sy0">;</span>
 atlas.<span class="me1">applyCoords</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
 geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT7 SECTION "Usage examples: Combine Geometries" [4881-] -->
