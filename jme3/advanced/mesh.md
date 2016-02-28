---
title: Polygon Meshes
---
<h1 class="sectionedit1" id="polygon_meshes">Polygon Meshes</h1>
<div class="level1">

<p>
<a href="/resources/jme3-dolphin-mesh.png" class="media" title="jme3:dolphin-mesh.png"><img src="/resources/jme3-dolphin-mesh.png" class="mediaright" alt="" /></a>
</p>

<p>
All visible game elements in a scene, whether it is a Model or a Shape, are made up of polygon meshes. JME3 has a com.jme3.scene.Mesh class that represents all meshes.
</p>
<ul>
<li class="level1"><div class="li"> Meshes are made up of triangles: <code>getTriangleCount(…)</code> and <code>getTriangle(…)</code></div>
</li>
<li class="level1"><div class="li"> Each mesh has a unique ID: <code>getId()</code></div>
</li>
<li class="level1"><div class="li"> Meshes have transformations: Location (local translation), rotation, scale.</div>
</li>
<li class="level1"><div class="li"> Meshes have a bounding volume. jME3 can detect intersections (that is, non-physical collisions) between meshes, or between meshes and 2D elements such as rays: <code>collideWith()</code>.</div>
</li>
<li class="level1"><div class="li"> Meshes are locked with <code>setStatic()</code> and unlocked with <code>setDynamic()</code>. </div>
<ul>
<li class="level2"><div class="li"> Static Meshes cannot be modified, but are more optimized and faster (they can be precalculated). </div>
</li>
<li class="level2"><div class="li"> Dynamic Meshes can be modified live, but are not optimized and slower. </div>
</li>
</ul>
</li>
</ul>

<p>
You have several options when <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">creating Geometries from meshes</a>:
</p>
<ul>
<li class="level1"><div class="li"> Use built-in <a href="/jme3/advanced/shape.html" class="wikilink1" title="jme3:advanced:shape">Shape</a>s as meshes; </div>
</li>
<li class="level1"><div class="li"> Load <a href="/jme3/advanced/3d_models.html" class="wikilink1" title="jme3:advanced:3d_models">3D models</a> (that is, meshes created in external applications); or </div>
</li>
<li class="level1"><div class="li"> Create free-form <a href="/jme3/advanced/custom_meshes.html" class="wikilink1" title="jme3:advanced:custom_meshes">custom meshes</a> programmatically. </div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "Polygon Meshes" [1-1154] -->
<h2 class="sectionedit2" id="vertex_buffer">Vertex Buffer</h2>
<div class="level2">

<p>
The VertexBuffer contains a particular type of geometry data used by Meshes. Every VertexBuffer set on a Mesh is sent as an attribute to the vertex shader to be processed.
</p>

</div>
<!-- EDIT2 SECTION "Vertex Buffer" [1155-1354] -->
<h3 class="sectionedit3" id="mesh_vertex_buffers">Mesh Vertex Buffers</h3>
<div class="level3">
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Vertex Buffer Type</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Type.Position </td><td class="col1">Position of the vertex (3 floats)</td>
	</tr>
	<tr class="row2">
		<td class="col0">Type.Index </td><td class="col1"> Specifies the index buffer, must contain integer data.</td>
	</tr>
	<tr class="row3">
		<td class="col0">Type.TexCoord </td><td class="col1"> Texture coordinate</td>
	</tr>
	<tr class="row4">
		<td class="col0">Type.TexCoord2 </td><td class="col1"> Texture coordinate #2</td>
	</tr>
	<tr class="row5">
		<td class="col0">Type.Normal </td><td class="col1"> Normal vector, normalized.</td>
	</tr>
	<tr class="row6">
		<td class="col0">Type.Tangent </td><td class="col1"> Tangent vector, normalized.</td>
	</tr>
	<tr class="row7">
		<td class="col0">Type.Binormal </td><td class="col1"> Binormal vector, normalized.</td>
	</tr>
	<tr class="row8">
		<td class="col0">Type.Color </td><td class="col1"> Color and Alpha (4 floats)</td>
	</tr>
	<tr class="row9">
		<td class="col0">Type.Size </td><td class="col1">The size of the point when using point buffers.</td>
	</tr>
	<tr class="row10">
		<td class="col0">Type.InterleavedData </td><td class="col1"> Specifies the source data for various vertex buffers when interleaving is used.</td>
	</tr>
	<tr class="row11">
		<td class="col0">Type.BindPosePosition </td><td class="col1"> Inital vertex position, used with animation.</td>
	</tr>
	<tr class="row12">
		<td class="col0">Type.BindPoseNormal </td><td class="col1"> Inital vertex normals, used with animation</td>
	</tr>
	<tr class="row13">
		<td class="col0">Type.BoneWeight </td><td class="col1"> Bone weights, used with animation</td>
	</tr>
	<tr class="row14">
		<td class="col0">Type.BoneIndex </td><td class="col1"> Bone indices, used with animation</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [1386-2205] -->
</div>
<!-- EDIT3 SECTION "Mesh Vertex Buffers" [1355-2206] -->
<h3 class="sectionedit5" id="mesh_properties">Mesh Properties</h3>
<div class="level3">
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Mesh method</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setLineWidth(1)</td><td class="col1">the thickness of the line if using Mode.Lines</td>
	</tr>
	<tr class="row2">
		<td class="col0">setPointSize(4.0f)</td><td class="col1">the thickness of the point when using Mode.Points</td>
	</tr>
	<tr class="row3">
		<td class="col0">setBound(boundingVolume)</td><td class="col1">if you need to specifiy a custom optimized bounding volume</td>
	</tr>
	<tr class="row4">
		<td class="col0">setStatic()</td><td class="col1">Locks the mesh so you cannot modify it anymore, thus optimizing its data (faster).</td>
	</tr>
	<tr class="row5">
		<td class="col0">setDynamic()</td><td class="col1">Unlocks the mesh so you can modified it, but this will un-optimize the data (slower).</td>
	</tr>
	<tr class="row6">
		<td class="col0">setMode(Mesh.Mode.Points)</td><td class="col1">Used to set mesh rendering modes, see below.</td>
	</tr>
	<tr class="row7">
		<td class="col0">getId()</td><td class="col1">returns the Mesh ID</td>
	</tr>
	<tr class="row8">
		<td class="col0">getTriangle(int,tri)</td><td class="col1">returns data of triangle number <code>int</code> into variable <code>tri</code></td>
	</tr>
	<tr class="row9">
		<td class="col0">scaleTextureCoordinates(Vector2f)</td><td class="col1">How the texture will be stretched over the whole mesh.</td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [2234-2957] -->
</div>
<!-- EDIT5 SECTION "Mesh Properties" [2207-2958] -->
<h3 class="sectionedit7" id="mesh_rendering_modes">Mesh Rendering Modes</h3>
<div class="level3">
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Mesh Mode</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Mesh.Mode.Points</td><td class="col1">Show only corner points (vertices) of mesh</td>
	</tr>
	<tr class="row2">
		<td class="col0">Mesh.Mode.Lines</td><td class="col1">Show lines (edges) of mesh</td>
	</tr>
	<tr class="row3">
		<td class="col0">Mesh.Mode.LineLoop</td><td class="col1">?</td>
	</tr>
	<tr class="row4">
		<td class="col0">Mesh.Mode.LineStrip</td><td class="col1">?</td>
	</tr>
	<tr class="row5">
		<td class="col0">Mesh.Mode.Triangles</td><td class="col1">?</td>
	</tr>
	<tr class="row6">
		<td class="col0">Mesh.Mode.TriangleStrip</td><td class="col1">?</td>
	</tr>
	<tr class="row7">
		<td class="col0">Mesh.Mode.TriangleFan</td><td class="col1">?</td>
	</tr>
	<tr class="row8">
		<td class="col0">Mesh.Mode.Hybrid</td><td class="col1">?</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [2991-3267] -->
</div>
<!-- EDIT7 SECTION "Mesh Rendering Modes" [2959-3268] -->
<h3 class="sectionedit9" id="level_of_detail">Level of Detail</h3>
<div class="level3">

<p>
Optionally, custom meshes can have a LOD (level of detail optimization) that renders more or less detail, depending on the distance of the mesh from the camera. You have to specify several vertex buffers, one for each level of detail you want (very far away with few details, close up with all details, and something in the middle). Use <code>setLodLevels(VertexBuffer[] lodLevels)</code>. 
</p>
<div class="tags"><span>
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>
</span></div>

</div>
<!-- EDIT9 SECTION "Level of Detail" [3269-] -->
