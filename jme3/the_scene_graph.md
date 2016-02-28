---
title: The Scene Graph and Other jME3 Terminology
---
<h1 class="sectionedit1" id="the_scene_graph_and_other_jme3_terminology">The Scene Graph and Other jME3 Terminology</h1>
<div class="level1">

<p>
Before you start making games, make sure you understand general <a href="/jme3/terminology.html" class="wikilink1" title="jme3:terminology">3D Gaming terminology</a>.
</p>

<p>
Second, if you are a beginner, we recommend our <a href="/jme3/scenegraph_for_dummies.html" class="wikilink1" title="jme3:scenegraph_for_dummies">Scene Graph for Dummies</a> presentation for a visual introduction to the concept of a scene graph. 
</p>

<p>
Then continue learning about jME3 concepts here.
</p>

</div>
<!-- EDIT1 SECTION "The Scene Graph and Other jME3 Terminology" [1-396] -->
<h2 class="sectionedit2" id="coordinate_system">Coordinate System</h2>
<div class="level2">

<p>
<a href="/resources/jme3-intermediate-coordinate-system.png" class="media" title="jme3:intermediate:coordinate-system.png"><img src="/resources/jme3-intermediate-coordinate-system.png" class="mediaright" alt="" width="235" height="210" /></a>
</p>

<p>
The jMonkeyEngine uses a right-handed coordinate system, just as OpenGL does.
</p>

<p>
The coordinate system consists of:
</p>
<ul>
<li class="level1"><div class="li"> The <em>origin</em>, a single central point in space.</div>
<ul>
<li class="level2"><div class="li"> The origin point is always at coordinate zero, in Java: <code>new Vector3f(0,0,0)</code>.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Three <em>coordinate axes</em> that are mutually perpendicular, and meet in the origin. </div>
<ul>
<li class="level2"><div class="li"> The X axis starts left and goes right.</div>
</li>
<li class="level2"><div class="li"> The Y axis starts below and goes up.</div>
</li>
<li class="level2"><div class="li"> The Z axis starts away from you, and goes towards you.</div>
</li>
</ul>
</li>
</ul>

<p>
Every point in 3D space is uniquely defined by its X,Y,Z coordinates. The three numeric coordinates express how many “steps” from each of the three axes a point is. The data type for all vectors in jME3 is <code>com.jme3.math.Vector3f</code>. All vectors are relative to the described coordinate system.  <br />
Example: The point <code>new Vector3f(3,-5,1)</code> is 3 steps to the right, 5 steps down, and 1 towards you.
</p>

<p>
</p><p></p><div class="noteclassic">The unit of meassurement (“one step”) in jME3 is the <strong>world unit</strong>, short: wu. Typically, 1 wu is considered to be one meter. As long as you are consistant throughout your game, 1 wu can be any distance you like.
</div>


<p>
For your orientation:
</p>
<ul>
<li class="level1"><div class="li"> The default camera's location is <code>Vector3f(0.0f, 0.0f, 10.0f)</code>.</div>
</li>
<li class="level1"><div class="li"> The default camera is looking in the direction described by the (so called) negative Z unit vector <code>Vector3f(0.0f, 0.0f, -1.0f)</code>. </div>
</li>
</ul>

<p>
This means the player's point of view is on the positive side of the Z axis, looking back, towards the origin, down the Z axis.
</p>

</div>
<!-- EDIT2 SECTION "Coordinate System" [397-1966] -->
<h2 class="sectionedit3" id="how_to_move_yourself_through_the_3d_scene">How to move yourself through the 3D scene</h2>
<div class="level2">

<p>
When you play a 3D game, you typically want to navigate the 3D scene. Note that by default, the mouse pointer is invisible, and the mouse is set up to control the camera rotation!
</p>

<p>
By default, jME3 uses the following common navigation inputs
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Game Inputs </th><th class="col1"> Camera Motion </th><th class="col2"> Player POV </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Press the W and S keys</td><td class="col1">move the camera forward, and backward</td><td class="col2">you walk back and forth</td>
	</tr>
	<tr class="row2">
		<td class="col0">Press the A and D keys</td><td class="col1">move the camera left and right</td><td class="col2">you step left or right</td>
	</tr>
	<tr class="row3">
		<td class="col0">Press the Q and Y keys</td><td class="col1">move the camera up and down</td><td class="col2">you fly up and down</td>
	</tr>
	<tr class="row4">
		<td class="col0">Move the mouse left-right</td><td class="col1">rotate the camera left/right</td><td class="col2">you look left or right</td>
	</tr>
	<tr class="row5">
		<td class="col0">Move the mouse forwards-backwards</td><td class="col1">rotate up/down</td><td class="col2">you look at the sky or your feet</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2265-2712] -->
<p>
These default settings are called “WASD keys” and “Mouse Look”. You can customize <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">input handling</a> for your game. Sorry, but these settings work best on a QWERTY/QWERTZ keyboard.
</p>

</div>
<!-- EDIT3 SECTION "How to move yourself through the 3D scene" [1967-2910] -->
<h2 class="sectionedit5" id="scene_graph_and_rootnode">Scene Graph and RootNode</h2>
<div class="level2">

<p>
The <em>scene graph</em> represents your 3D world. Objects in the jME3 scene graph are called <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a>s. Everything attached to the parent <em>rootNode</em> is part of your scene. Your game inherits the <code>rootNode</code> object from the <code>SimpleApplication</code> class. 
</p>

<p>
<a href="/resources/jme3-intermediate-scene-graph.png" class="media" title="jme3:intermediate:scene-graph.png"><img src="/resources/jme3-intermediate-scene-graph.png" class="mediacenter" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> <em>Attaching</em> a Spatial to the rootNode (or its child nodes) adds it to the scene; </div>
</li>
<li class="level1"><div class="li"> <em>Detaching</em> a Spatial from the rootNode (or its child nodes) removes it from the scene.</div>
</li>
</ul>

<p>
All objects in the scene graph are in a parent-child relationship. When you transform (move, rotate, scale) one parent, all its children follow.
</p>

<p>
</p><p></p><div class="noteclassic">The scene graph only manages the parent-child relationship of spatials. The actual location, rotation, or scale of an object is stored inside each Spatial. 
</div>


</div>
<!-- EDIT5 SECTION "Scene Graph and RootNode" [2911-3763] -->
<h2 class="sectionedit6" id="spatialsnode_vs_geometry">Spatials: Node vs Geometry</h2>
<div class="level2">

<p>
A Spatial can be transformed (in other words, it has a location, a rotation, and a scale). A Spatial can be loaded and saved as a .3jo file. There are two types of Spatials, <em>Nodes</em> and <em>Geometries</em>:
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0 leftalign">  </td><th class="col1" colspan="2"> Spatial </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> Purpose: </th><td class="col1" colspan="2"> A Spatial is an abstract data structure that stores transformations (translation, rotation, scale). </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign">  </td><th class="col1"> Geometry </th><th class="col2"> Node </th>
	</tr>
	<tr class="row3">
		<th class="col0"> Visibility: </th><td class="col1"> A visible 3-D object. </td><td class="col2"> An invisible “handle” for a group of objects. </td>
	</tr>
	<tr class="row4">
		<th class="col0"> Purpose: </th><td class="col1"> A Geometry represents the “look” of an object: Shape, color, texture, opacity/transparency. </td><td class="col2"> A Node groups Geometries and other Nodes together: You transform a Node to affect all attached Nodes (parent-child relationship). </td>
	</tr>
	<tr class="row5">
		<th class="col0"> Content: </th><td class="col1"> Transformations, mesh, material. </td><td class="col2"> Transformations. No mesh, no material. </td>
	</tr>
	<tr class="row6">
		<th class="col0"> Examples: </th><td class="col1"> A box, a sphere, player, a building, a piece of terrain, a vehicle, missiles, NPCs, etc… </td><td class="col2"> The rootNode, the guiNode, an audioNode, a custom grouping node for a vehicle plus its passengers, etc. </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [4009-4793] -->
</div>
<!-- EDIT6 SECTION "Spatials: Node vs Geometry" [3764-4794] -->
<h2 class="sectionedit8" id="how_to_use_this_knowledge">How to Use This Knowledge?</h2>
<div class="level2">

<p>
Before you start creating your game, you should plan your scene graph: Which Nodes and Geometries will you need? Complete the <a href="/jme3/beginner.html" class="wikilink1" title="jme3:beginner">Beginner tutorials</a> to learn how to load and create Spatials, how to lay out a scene by attaching, detaching, and transforming Spatials, and how to add interaction and effects to a game.
</p>

<p>
The <a href="/jme3.html" class="wikilink1" title="jme3">intermediate and advanced documentation</a> gives you more details on how to put all the parts together to create an awesome 3D game in Java!
</p>

</div>
<!-- EDIT8 SECTION "How to Use This Knowledge?" [4795-5318] -->
<h2 class="sectionedit9" id="see_also">See also</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a> – More details about working with Nodes and Geometries</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/traverse_scenegraph.html" class="wikilink1" title="jme3:advanced:traverse_scenegraph">Traverse SceneGraph</a> – Find any Node or Geometry in the scenegraph.</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/camera.html" class="wikilink1" title="jme3:advanced:camera">Camera</a> – Learn more about the Camera in the scene.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>,
	<a href="/tag/rootnode.html" class="wikilink1" title="tag:rootnode" rel="tag">rootnode</a>
</span></div>

</div>
<!-- EDIT9 SECTION "See also" [5319-] -->
