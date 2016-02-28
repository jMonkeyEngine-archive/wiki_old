---
title: The Tree System
---
<h1 class="sectionedit1" id="the_tree_system">The Tree System</h1>
<div class="level1">

<p>
Here you will learn how to use the tree system.
</p>

</div>
<!-- EDIT1 SECTION "The Tree System" [1-80] -->
<h2 class="sectionedit2" id="simpletreetestjava">SimpleTreeTest.java</h2>
<div class="level2">

<p>
There's a file in the demo-project named SimpleTreeTest. There's a method in it named <strong>setupForester()</strong> where you can see how a tree system is set up. If you haven't already done so, you might also want
to check out the SimpleGrassTest.java file, because it contains a lot more information on certain other, important topics regarding the forester lib in general.
</p>

<p>
The basic procedure is this:
</p>

<p>
1) Create a Forester object, and initialize it.
</p>

<p>
2) Use it to create a tree-loader.
</p>

<p>
3) Use the treeloader to create a map-provider.
</p>

<p>
4) Use the treeloader to create one tree-layer for each type of tree.
</p>

<p>
5) Tweak everything until it fits your app.
</p>

<p>
6) Make sure you call forester.update() each frame.
</p>

</div>
<!-- EDIT2 SECTION "SimpleTreeTest.java" [81-813] -->
<h2 class="sectionedit3" id="physicstestjava">PhysicsTest.java</h2>
<div class="level2">

<p>
There's another file in the demo project called PhysicsTest.java. In that file you can see how collision-shapes are added to the trees. 
</p>

<p>
When you create a tree-layer through <strong>treeLoader.createTreeLayer(Spatial spat, boolean usePhysics)</strong>, you supply the model and a boolean whether or not to use physics. If you want to enable collision physics, look in that file how it's done.
</p>

<p>
There are some general principles:
</p>

<p>
1) In order to enable collision physics _at all_, you first need to set up a physics space. There's a great tutorial available in the tutorials section of the jME wiki: <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_physics" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_physics" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_physics</a>.
</p>

<p>
2) If you want to enable physics with the forester, you need to provide the physics space to the Forester object. This is shown in the PhysicsTest.java file.
</p>

<p>
3) Once that is done, you need to provide a collision shape with your model, obviously. This can be done in several ways. You can do it through the jMP scene composer, or programatically.
</p>

<p>
When a model is supplied to a tree-layer, and physics is enabled, the model will be checked for collision shapes. The shape is then removed from the model, and added to the tree-layer instead.
</p>

<p>
The reason for this is that the trees are lumped together in a process called geometry-batching. It is commonly used to reduce the number of drawing-calls for groups of objects that are very similar.
</p>

<p>
What this means in practice is that your model is not just duplicated and spread out across the scene, they are in fact baked together into one single mesh (per “block”). This process is also used for collision shapes. They are all compounded into one large collision shape, then added to this newly created clump of vertices. Basically.
</p>

<p>
<strong>In short</strong> - there are a couple of instances when the collision physics system may fail:
</p>

<p>
- If you do not supply a physics space to the forester, no physics will be enabled.
</p>

<p>
- If you do not check “true” for enable physics when creating the tree-layer.
</p>

<p>
- If you do not supply a collision mesh to the model.
</p>

</div>
<!-- EDIT3 SECTION "PhysicsTest.java" [814-2897] -->
<h2 class="sectionedit4" id="the_tree_data_system_basic">The tree data system (Basic)</h2>
<div class="level2">

<p>
<strong>Basics</strong>
</p>

<p>
At the core of tree placement is the class <strong>TreeData</strong>. It contains five floats representing a tree - x,y,z-coords, rotation, scale. This means a tree-layer just needs to keep one copy of the model, rather then many instances that differ only in transformation.
</p>

<p>
Tree data is stored in TreeDataLists, which are basically arraylists.
</p>

<p>
<strong>Using tree data</strong>
</p>

<p>
In the SimpleTreeTest.java is an example of how to set up a treeloader to use density maps to generate tree-data through the <strong>MapGrid</strong> data-provider. You do not have to worry about this stuff if you use density maps. 
</p>

<p>
There will be info here on how to use the alternative <strong>DataGrid</strong> data-provider later.
</p>

</div>
<!-- EDIT4 SECTION "The tree data system (Basic)" [2898-] -->
