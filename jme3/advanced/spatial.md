---
title: Spatial
---
<h1 class="sectionedit1" id="spatial">Spatial</h1>
<div class="level1">

<p>
This is an introduction to the concept of Spatials, the elements of the 3D scene graph. The scene graph is a data structure that manages all objects in your 3D world. For example, the scene graph keeps track of the 3D models that you load and position. When you extend a Java class from com.jme3.app.SimpleApplication, you automatically inherit the scene graph and its rootNode. 
</p>

<p>
The rootNode is the central element of the scene graph. Even if the scene graph is empty, it always contains at least the rootNode. We <em>attach</em> Spatials to the rootNode. Attached Spatials are always in a <em>parent-child relationship</em>. Every time you attach a Spatial to something, it is implicitly detached from its previous parent. A Spatial can have only one parent. A Spatial can have several children.
</p>

<p>
If you think you need to understand the scene graph concept better, please read <a href="/jme3/scenegraph_for_dummies.html" class="wikilink1" title="jme3:scenegraph_for_dummies">Scenegraph for dummies</a> first.
</p>

</div>
<!-- EDIT1 SECTION "Spatial" [1-934] -->
<h2 class="sectionedit2" id="node_versus_geometry">Node versus Geometry</h2>
<div class="level2">

<p>
In your Java code, a Spatial is either an instance of <code>com.jme3.scene.Node</code> or a <code>com.jme3.scene.Geometry</code> instance. You use the two types of Spatials for different purposes:
</p>

<p>
<a href="/resources/jme3-intermediate-scene-graph.png" class="media" title="jme3:intermediate:scene-graph.png"><img src="/resources/jme3-intermediate-scene-graph.png" class="mediacenter" alt="" /></a>
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0"> </td><th class="col1" colspan="2">com.jme3.scene.Spatial </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> Purpose: </th><td class="col1" colspan="2"> A Spatial is an abstract data structure that stores user data and transformations (= translation, rotation, scale) of elements of the 3D scene graph. Spatials can be saved and loaded using the <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>. </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign">  </td><th class="col1"> com.jme3.scene.Geometry </th><th class="col2"> com.jme3.scene.Node </th>
	</tr>
	<tr class="row3">
		<th class="col0"> Visibility: </th><td class="col1"> A Geometry represents a <strong>visible</strong> 3D object in the scene graph. </td><td class="col2"> A Node is an <strong>invisible “handle”</strong> for a group of Spatials in the scene graph. </td>
	</tr>
	<tr class="row4">
		<th class="col0 leftalign"> Purpose:    </th><td class="col1"> Use Geometries to represent an object's <strong>look</strong>: Every Geometry contains a polygon mesh and a material, specifying its shape, color, texture, and opacity/transparency. <br />
You attach Geometries to Nodes. </td><td class="col2"> Use Nodes to <strong>structure and group</strong> Geometries and other Nodes. Every Node is attached to one parent node, and each node can have zero or more children (Nodes or Geometries) attached to itself. <br />
<strong>When you transform (move, rotate, etc) a parent node, all its children are transformed (moved, rotated, etc).</strong> </td>
	</tr>
	<tr class="row5">
		<th class="col0 leftalign"> Content:    </th><td class="col1 leftalign"> Transformations; custom user data; <br />
mesh and material;  </td><td class="col2"> Transformations; custom user data; <br />
no mesh, no material.</td>
	</tr>
	<tr class="row6">
		<th class="col0 leftalign"> Examples:   </th><td class="col1"> Box, sphere, player, building, terrain, vehicle, missiles, NPCs, etc… </td><td class="col2"> rootNode, guiNode, audioNode, a custom grouping node such as vehicleNode or shipNode with passengers attached, etc. </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [1191-2548] -->
<p>
</p><p></p><div class="noteimportant">You never create a Spatial with <code><del>Spatial s = new Spatial();</del></code>! A Spatial is an abstract concept, like a mammal (there is no actual creature called “mammal” walking around here). You create either a com.jme3.scene.Node or com.jme3.scene.Geometry instance. Some methods, however, require a <code>Spatial</code> type as argument: This is because they are able to accept both Nodes and Geometries as arguments. In this case, you simply <em>cast</em> a Node or Geometry to Spatial.
</div>


</div>
<!-- EDIT2 SECTION "Node versus Geometry" [935-3048] -->
<h3 class="sectionedit4" id="mesh">Mesh</h3>
<div class="level3">

<p>
The polygon <a href="/jme3/advanced/mesh.html" class="wikilink1" title="jme3:advanced:mesh">Mesh</a> inside a Geometry can be one of three things:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Shapes:</strong> The simplest type of Meshes are jME's default <a href="/jme3/advanced/shape.html" class="wikilink1" title="jme3:advanced:shape">Shape</a>s such as cubes and spheres. You can use several Shapes to build complex Geometries. Shapes are built-in and can be created without using the AssetManager.</div>
</li>
<li class="level1"><div class="li"> <strong>3D Models:</strong> <a href="/jme3/advanced/3d_models.html" class="wikilink1" title="jme3:advanced:3d_models">3D models and scenes</a> are also made up of meshes, but are more complex than Shapes. You create Models and Scenes in external 3D Mesh Editors and export them as Ogre XML or Wavefront OBJ. Use the <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a> to load models into a your jME3 game.</div>
</li>
<li class="level1"><div class="li"> <strong>Custom Meshes:</strong> Advanced users can create <a href="/jme3/advanced/custom_meshes.html" class="wikilink1" title="jme3:advanced:custom_meshes">Custom Meshes</a> programmatically.</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Mesh" [3049-3728] -->
<h2 class="sectionedit5" id="what_is_a_clone">What is a Clone?</h2>
<div class="level2">

<p>
Cloned spatials share the same mesh, while each cloned spatial can have its own local transformation (translation, rotation, and scale) in the scene. This means you only use <code>clone()</code> on spatials whose meshes never change. The most common use case for cloning is when you use several Spatials that are based on the same <a href="/jme3/advanced/shape.html" class="wikilink1" title="jme3:advanced:shape">Shape</a>s (e.g. trees, crates). 
</p>

<p>
The second use case is: When you load a model using <code>loadModel()</code> from the AssetManager, you may automatically get a <code>clone()</code>ed object. In particular:
</p>
<ul>
<li class="level1"><div class="li"> If the model is not animated (it has no <code><a href="/jme3/advanced/animation.html" class="wikilink1" title="jme3:advanced:animation">AnimControl</a></code>), jME loads a clone. All clones share one mesh object in order to use less memory.</div>
</li>
<li class="level1"><div class="li"> If the model is animated (it has a <code><a href="/jme3/advanced/animation.html" class="wikilink1" title="jme3:advanced:animation">AnimControl</a></code>), then <code>loadModel()</code> duplicates the mesh for each loaded instance. (Uses more memory, but can animate.)</div>
</li>
</ul>

<p>
Usually there is no need to manually use any of the <code>clone()</code> methods on models. Using the <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>'s <code>loadModel()</code> method will automatically do the right thing for your models.
</p>

<p>
</p><p></p><div class="noteclassic">“Box worlds” are not made up of statically cloned <code>Box()</code> shapes, this would still be too slow for large worlds. To learn how to make real fast box worlds, search the web for <em>voxelization</em> techniques.
</div>


</div>
<!-- EDIT5 SECTION "What is a Clone?" [3729-5049] -->
<h2 class="sectionedit6" id="how_to_add_fields_and_methods_to_a_spatial">How to Add Fields and Methods to a Spatial</h2>
<div class="level2">

<p>
You can include custom user data –that is, custom Java objects and methods– in Nodes and Geometries. This is very useful for maintaining information about a game element, such as health, budget, ammunition, inventory, equipment, etc for players, or landmark locations for terrains, and much more. 
</p>

<p>
</p><p></p><div class="noteimportant">You want to add custom accessor methods to a spatial? Do not extend <code>Node</code> or <code>Geometry</code>, use <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a> instead. You want to add custom fields to a spatial? Do not extend <code>Node</code> or <code>Geometry</code>, use the built-in <code>setUserData()</code> method instead. Where ever the Spatial is accessible, you can easily access the object's class fields (user data) and accessors (control methods) this way. 
</div>


<p>
This first example adds an integer field named <code>health</code> to the Spatial <code>playerNode</code>, and initializes it to 100.
</p>
<pre class="code java">playerNode.<span class="me1">setUserData</span><span class="br0">(</span><span class="st0">"health"</span>, <span class="nu0">100</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The second example adds a set of custom accessor methods to the player object. You create a <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">custom PlayerControl() class</a> and you add this control to the Spatial:
</p>
<pre class="code java">playerNode.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> PlayerControl<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
In your PlayerControl() class, you define custom methods that set and get your user data in the <code>spatial</code> object. For example, the control could add accessors that set and get the player's health:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">int</span> getHealth<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">return</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+integer"><span class="kw3">Integer</span></a><span class="br0">)</span>spatial.<span class="me1">getUserData</span><span class="br0">(</span><span class="st0">"health"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
<span class="kw1">public</span> <span class="kw4">void</span> setHealth<span class="br0">(</span><span class="kw4">int</span> h<span class="br0">)</span> <span class="br0">{</span>
  spatial.<span class="me1">setUserData</span><span class="br0">(</span><span class="st0">"health"</span>,h<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Elsewhere in your code, you can access this data wherever you have access to the Spatial <code>playerNode</code>. 
</p>
<pre class="code java">health <span class="sy0">=</span> playerNode.<span class="me1">getControl</span><span class="br0">(</span>PlayerControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">getHealth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">playerNode</span>.<span class="me1">getControl</span><span class="br0">(</span>PlayerControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setHealth</span><span class="br0">(</span><span class="nu0">99</span><span class="br0">)</span><span class="sy0">;</span></pre>
<ul>
<li class="level1"><div class="li"> You can add as many data objects (of String, Boolean, Integer, Float, Array types) to a Spatial as you want. Just make sure to label them with unique case-sensitive strings (<code>health</code>, <code>Inventory</code>, <code>equipment</code>, etc). </div>
</li>
<li class="level1"><div class="li"> The saved data can even be a custom Java object if you make the custom Java class <a href="/jme3/advanced/save_and_load.html" class="wikilink1" title="jme3:advanced:save_and_load">implement the Savable interface</a>! </div>
</li>
<li class="level1"><div class="li"> When you save a Spatial as a .j3o file, the custom data is saved, too, and all Savables are restored the next time you load the .j3o! </div>
</li>
</ul>

<p>
This is how you list all data keys that are already defined for one Spatial:
</p>
<pre class="code java"><span class="kw1">for</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> key <span class="sy0">:</span> spatial.<span class="me1">getUserDataKeys</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>spatial.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">+</span><span class="st0">"'s keys: "</span><span class="sy0">+</span>key<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "How to Add Fields and Methods to a Spatial" [5050-7620] -->
<h2 class="sectionedit7" id="how_to_access_a_named_sub-mesh">How to Access a Named Sub-Mesh</h2>
<div class="level2">

<p>
Often after you load a scene or model, you need to access a part of it as an individual Geometry in the scene graph. Maybe you want to swap a character's weapon, or you want to play a door-opening animation. First you need to know the unique name of the sub-mesh.
</p>
<ol>
<li class="level1"><div class="li"> Open the model in a 3D mesh editor, or in the jMonkeyEngine SDK's Scene Composer. </div>
</li>
<li class="level1"><div class="li"> Find out the existing names of sub-meshes in the model.</div>
</li>
<li class="level1"><div class="li"> Assign unique names to sub-meshes in the model if neccessary.</div>
</li>
</ol>

<p>
In the following example, the Node <code>house</code> is the loaded model. The sub-meshes in the Node are called its children. The String, here <code>door 12</code>, is the name of the mesh that you are searching. 
</p>
<pre class="code java">Geometry submesh <span class="sy0">=</span> <span class="br0">(</span>Geometry<span class="br0">)</span> houseScene.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"door 12"</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT7 SECTION "How to Access a Named Sub-Mesh" [7621-8423] -->
<h2 class="sectionedit8" id="what_is_culling">What is Culling?</h2>
<div class="level2">

<p>
There are two types of culling: Face culling, and view frustrum culling.
</p>

<p>
<strong>Face culling</strong> means not drawing certain polygons of a mesh. Face culling behaviour is a property of the material.
</p>

<p>
Usage: The “inside” of a mesh (the so called backface) is typically never visible to the player, and as an optimization, the <code>Back</code> mode skips calculating all backfaces by default. Activating the <code>Off</code> or <code>Front</code> modes can be useful when you are debugging <a href="/jme3/advanced/custom_meshes.html" class="wikilink1" title="jme3:advanced:custom_meshes">custom meshes</a> and try to identify accidental inside-out faces. 
</p>

<p>
You can switch the com.jme3.material.RenderState.FaceCullMode to either:
</p>
<ul>
<li class="level1"><div class="li"> <code>FaceCullMode.Back</code> (default) – Only the frontsides of a mesh are drawn. Backface culling is the default behaviour. </div>
</li>
<li class="level1"><div class="li"> <code>FaceCullMode.Front</code> – Only the backsides of a mesh are drawn. A mesh with frontface culling will most likely be invisible. Used for debugging “inside-out” custom meshes.</div>
</li>
<li class="level1"><div class="li"> <code>FaceCullMode.FrontAndBack</code> – Use this to make a mesh temporarily invisible. </div>
</li>
<li class="level1"><div class="li"> <code>FaceCullMode.Off</code> – Every side of the mesh is drawn. Looks normal, but slows down large scenes.</div>
</li>
</ul>

<p>
Example: 
</p>
<pre class="code java">material.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setFaceCullMode</span><span class="br0">(</span>FaceCullMode.<span class="me1">FrontAndBack</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>View frustum culling</strong> refers to not drawing (and not even calculating) certain whole models in the scene. At any given moment, half of the scene is behind the player and out of sight anyway. View frustum culling is an optimization to not calculate scene elements that are not visible – elements that are “outside the view frustrum”.
</p>

<p>
The decision what is visible and what not, is done automatically by the engine (<code>CullHint.Dynamic</code>). Optionally, you can manually control whether the engine culls individual spatials (and children) from the scene graph:
</p>
<ul>
<li class="level1"><div class="li"> <code>CullHint.Dynamic</code> – Default, faster because it doesn't waste time with objects that are out of view.</div>
</li>
<li class="level1"><div class="li"> <code>CullHint.Never</code> – Calculate and draw everything always (even if it does not end up on the user's screen because it's out of sight). Slower, but can be used while debugging custom meshes.</div>
</li>
<li class="level1"><div class="li"> <code>CullHint.Always</code> – The whole spatial is culled and is not visible. A fast way to hide a Spatial temporarily. Culling a Spatial is faster then detaching it, but it uses more memory.</div>
</li>
<li class="level1"><div class="li"> <code>CullHint.Inherit</code> – Inherit culling behaviour from parent node. </div>
</li>
</ul>

<p>
Example:
</p>
<pre class="code java">spatial.<span class="me1">setCullHint</span><span class="br0">(</span>CullHint.<span class="me1">Never</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// always drawn</span></pre>

</div>
<!-- EDIT8 SECTION "What is Culling?" [8424-10857] -->
<h2 class="sectionedit9" id="see_also">See also</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/optimization.html" class="wikilink1" title="jme3:intermediate:optimization">Optimization</a> – The GeometryBatchFactory class batches several Geometries into meshes with each their own texture.</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/traverse_scenegraph.html" class="wikilink1" title="jme3:advanced:traverse_scenegraph">Traverse SceneGraph</a> – Find any Node or Geometry in the scenegraph.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>
</span></div>

</div>
<!-- EDIT9 SECTION "See also" [10858-] -->
