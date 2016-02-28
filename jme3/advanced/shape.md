---
title: Shapes
---
<h1 class="sectionedit1" id="shapes">Shapes</h1>
<div class="level1">

<p>
The simplest type of Meshes are the built-in JME Shapes. You can create Shapes without using the AssetManager.
</p>

</div>
<!-- EDIT1 SECTION "Shapes" [1-133] -->
<h2 class="sectionedit2" id="d_shapes">3D shapes</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/jme/wiki-data/userref/sphere.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="108" height="80" /></a><a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/jme/wiki-data/userref/cylinder.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="108" height="80" /></a><a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/jme/wiki-data/userref/box.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="108" height="80" /></a>
</p>
<ul>
<li class="level1"><div class="li"> com.jme3.scene.shape.Box – A cube or cuboid. Single-sided Quad faces (outside only). </div>
</li>
<li class="level1"><div class="li"> com.jme3.scene.shape.StripBox – A cube or cuboid. Solid filled faces (inside and outside).</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> com.jme3.scene.shape.Cylinder – A disk or pillar.</div>
</li>
<li class="level1"><div class="li"> com.jme3.scene.shape.Sphere – A ball or elipsoid. </div>
</li>
</ul>

<p>
<a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/jme/wiki-data/userref/pyramid.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="108" height="80" /></a><a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/jme/wiki-data/userref/cone.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="108" height="80" /></a><a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/jme/wiki-data/userref/dome.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="108" height="80" /></a>
</p>
<ul>
<li class="level1"><div class="li"> com.jme3.scene.shape.Dome – A semi-sphere, e.g. SkyDome.</div>
<ul>
<li class="level2"><div class="li"> For a cone, set the Dome's radialSamples&gt;4 and planes=2. </div>
</li>
<li class="level2"><div class="li"> For a pyramid, set the Dome's radialSamples=4 and planes=2. </div>
</li>
</ul>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> com.jme3.scene.shape.Torus – An single-holed torus or “donut”.</div>
</li>
<li class="level1"><div class="li"> com.jme3.scene.shape.PQTorus – A parameterized torus. A PQ-Torus looks like a <a href="http://en.wikipedia.org/wiki/Torus_knot" class="urlextern" title="http://en.wikipedia.org/wiki/Torus_knot" rel="nofollow">donut knotted into spirals</a>. <a href="/resources/jme3-advanced-nurbs_3-d_surface.png" class="media" title="jme3:advanced:nurbs_3-d_surface.png"><img src="/resources/jme3-advanced-nurbs_3-d_surface.png" class="mediaright" title="NURBS surface" alt="NURBS surface" width="108" height="80" /></a><a href="/resources/jme3-advanced-220px-trefoil_knot_arb.png" class="media" title="jme3:advanced:220px-trefoil_knot_arb.png"><img src="/resources/jme3-advanced-220px-trefoil_knot_arb.png" class="mediaright" title="PQ torus knoz" alt="PQ torus knoz" width="108" height="80" /></a><a href="/resources/fetch.php" class="media" title="http://i204.photobucket.com/albums/bb19/mike_ch_1/torus.png"><img src="/resources/fetch.php" class="mediaright" title="Torus" alt="Torus" width="108" height="80" /></a></div>
</li>
<li class="level1"><div class="li"> com.jme3.scene.shape.Surface – A curved surface (called <a href="http://en.wikipedia.org/wiki/File:NURBS_3-D_surface.gif" class="urlextern" title="http://en.wikipedia.org/wiki/File:NURBS_3-D_surface.gif" rel="nofollow">NURBS</a>) described by knots, weights and control points. Compare with shape.Curve.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "3D shapes" [134-1719] -->
<h2 class="sectionedit3" id="non-3d_shapes">Non-3D shapes</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> com.jme3.scene.shape.Quad – A flat 2D rectangle (single-sided, center is in bottom-left corner)</div>
</li>
<li class="level1"><div class="li"> com.jme3.scene.shape.Line – A straight 1D line defined by a start and end point.</div>
</li>
<li class="level1"><div class="li"> com.jme3.scene.shape.Curve – A curved 1D spline. Compare with shape.Surface.</div>
</li>
</ul>

</div>

<h4 id="comjme3math_versus_comjme3shape">com.jme3.math versus com.jme3.shape?</h4>
<div class="level4">

<p>
Do not mix up these visible com.jme3.shapes with similarly named classes from the com.jme3.math package. Choose the right package when letting your IDE fill in the import statements!
</p>
<ul>
<li class="level1"><div class="li"> com.jme3.math.Line – is invisible, has a direction, goes through a point, infinite length.</div>
</li>
<li class="level1"><div class="li"> com.jme3.math.Ray – is invisible, has a direction and start point, but no end.</div>
</li>
<li class="level1"><div class="li"> com.jme3.math.Spline – is an invisible curve.</div>
</li>
<li class="level1"><div class="li"> etc</div>
</li>
</ul>

<p>
These maths objects are invisible and are used for collision testing (ray casting) or to describe motion paths. They cannot be wrapped into a Geometry.
</p>

</div>
<!-- EDIT3 SECTION "Non-3D shapes" [1720-2635] -->
<h2 class="sectionedit4" id="usage">Usage</h2>
<div class="level2">

</div>

<h4 id="basic_usage">Basic Usage</h4>
<div class="level4">

<p>
To add a shape to the scene:
</p>
<ol>
<li class="level1"><div class="li"> Create the base mesh shape.</div>
</li>
<li class="level1"><div class="li"> Wrap the mesh into a Geometry.</div>
</li>
<li class="level1"><div class="li"> Assign a Material to the Geometry.</div>
</li>
<li class="level1"><div class="li"> Attach the Geometry to the rootNode to make it visible.</div>
</li>
</ol>

<p>
</p><p></p><div class="notetip">Create one static shape as mesh and use it in several geometries, or clone() the geometries.
</div>


</div>

<h4 id="complex_shapes">Complex Shapes</h4>
<div class="level4">

<p>
You can compose more complex custom Geometries out of simple Shapes. Think of the buildings in games like Angry Birds, or the building blocks in Second Life (“prims”) and in Tetris (“Tetrominos”).
</p>
<ol>
<li class="level1"><div class="li"> Create a Node. By default it is located at the origin (0/0/0) – leave the Node there for now.</div>
</li>
<li class="level1"><div class="li"> Create your shapes and wrap each into a Geometry, as just described.</div>
</li>
<li class="level1"><div class="li"> Attach each Geometry to the Node.</div>
</li>
<li class="level1"><div class="li"> Arrange the Geometries around the Node (using <code>setLocalTranslation()</code>) so that the Node is in the center of the new constellation. The central Node is the pivot point for transformations (move/scale/rotate).</div>
</li>
<li class="level1"><div class="li"> Move the pivot Node to its final location in the scene. Moving the pivot Node moves the attached constellation of Geometries with it.</div>
</li>
</ol>

<p>
The order is important: First arrange around origin, then transform. Otherwise, transformations are applied around the wrong center (pivot). Of course, you can attach your constellation to other pivot Nodes to create even more complex shapes (a chair, a furnished room, a house, a city, …), but again, arrange them around the origin first before you transform them. Obviously, such composed Geometries are simpler than hand-sculpted meshes from a mesh editor.
</p>

</div>
<!-- EDIT4 SECTION "Usage" [2636-4228] -->
<h2 class="sectionedit5" id="code_examples">Code Examples</h2>
<div class="level2">

<p>
Create the Mesh shape:
</p>
<pre class="code java">Sphere mesh <span class="sy0">=</span> <span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">32</span>, <span class="nu0">32</span>, <span class="nu0">10</span>, <span class="kw2">false</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Dome mesh <span class="sy0">=</span> <span class="kw1">new</span> Dome<span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">2</span>, <span class="nu0">4</span>, 1f,<span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Pyramid</span></pre>
<pre class="code java">Dome mesh <span class="sy0">=</span> <span class="kw1">new</span> Dome<span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">2</span>, <span class="nu0">32</span>, 1f,<span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Cone</span></pre>
<pre class="code java">Dome mesh <span class="sy0">=</span> <span class="kw1">new</span> Dome<span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">32</span>, <span class="nu0">32</span>, 1f,<span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Small hemisphere</span></pre>
<pre class="code java">Dome mesh <span class="sy0">=</span> <span class="kw1">new</span> Dome<span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">32</span>, <span class="nu0">32</span>, 1000f,<span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// SkyDome</span></pre>
<pre class="code java">PQTorus mesh <span class="sy0">=</span> <span class="kw1">new</span> PQTorus<span class="br0">(</span><span class="nu0">5</span>,<span class="nu0">3</span>, 2f, 1f, <span class="nu0">32</span>, <span class="nu0">32</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Spiral torus</span></pre>
<pre class="code java">PQTorus mesh <span class="sy0">=</span> <span class="kw1">new</span> PQTorus<span class="br0">(</span><span class="nu0">3</span>,<span class="nu0">8</span>, 2f, 1f, <span class="nu0">32</span>, <span class="nu0">32</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Flower torus</span></pre>

<p>
Use one of the above examples together with the following geometry in a scene:
</p>
<pre class="code java">Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"A shape"</span>, mesh<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// wrap shape into geometry</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,      
    <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// create material</span>
geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>                         <span class="co1">// assign material to geometry</span>
<span class="co1">// if you want, transform (move, rotate, scale) the geometry.</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>                    <span class="co1">// attach geometry to a node</span></pre>

</div>
<!-- EDIT5 SECTION "Code Examples" [4229-5359] -->
<h2 class="sectionedit6" id="see_also">See also</h2>
<div class="level2">

<p>
* <a href="/jme3/intermediate/optimization.html" class="wikilink1" title="jme3:intermediate:optimization">Optimization</a> – The GeometryBatchFactory class combines several of your shapes with the same texture into one mesh with one texture.
</p>
<div class="tags"><span>
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>
</span></div>

</div>
<!-- EDIT6 SECTION "See also" [5360-] -->
