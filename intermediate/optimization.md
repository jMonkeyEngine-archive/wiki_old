---
title: Optimization reference
---
<h1 class="sectionedit1" id="optimization_reference">Optimization reference</h1>
<div class="level1">

<p>
This page is intended as a reference collection of optimization tricks that can be used to speed up JME3 applications.
</p>

</div>
<!-- EDIT1 SECTION "Optimization reference" [1-156] -->
<h2 class="sectionedit2" id="maintain_low_geometry_count">Maintain low Geometry count</h2>
<div class="level2">

<p>
The more Geometry objects are added to the scene, the harder it gets to handle them in a speedy fashion.
The reason for this is that a render command must be done for every object, potentially creating a bottleneck between the CPU and the graphics card.
</p>

<p>
<strong>Possible optimization techniques</strong>
</p>
<ul>
<li class="level1"><div class="li"> Use GeometryBatchFactory.optimize(node) to merge the meshes of the geometries contained in the given node into fewer batches, each based on common Materials used. <br />
You can optimize nodes using the SceneComposer in the SDK as well: Right-click a node and select “Optimize Geometry”.</div>
</li>
</ul>

<p>
<strong>Side-effects</strong>
</p>
<ul>
<li class="level1"><div class="li"> Using GeometryBatchFactory merges individual Geometries into a single mesh. Thereby it becomes hard to apply specific Materials or to remove a single Geometry. Therefore it should be used for static Geometry only that does not require frequent changes or individual materials/texturing. </div>
</li>
<li class="level1"><div class="li"> Using a <a href="/jme3/advanced/texture_atlas.html" class="wikilink1" title="jme3:advanced:texture_atlas">Texture Atlas</a> provides limited individual texturing of batched geometries.</div>
</li>
<li class="level1"><div class="li"> Using the still experimental BatchNode allows batching Geometry while keeping the single Geometry objects movable separately (similar to animation, the buffer gets updated per Geometry position).</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Maintain low Geometry count" [157-1393] -->
<h2 class="sectionedit3" id="avoid_creating_new_objects">Avoid creating new objects</h2>
<div class="level2">

<p>
Different Java implementations use different garbage collection algorithms, so depending on the platforms you target, different advice applies.
</p>

<p>
The major variants are Oracle's JRE, old (pre-Gingerbread) Androids, and newer (Gingerbread or later) Androids.
</p>

<p>
Oracle's JRE is a copying collector. This means that it does not need to do any work for objects that have become unreachable, it just keeps copying live objects to new memory areas and recycles the now-unused area as a whole.
Older objects are copied less often, so the garbage collection overhead is roughly proportional to the rate at which your code creates new objects that survive for, say, more than a minute.
</p>

<p>
Gingerbread and newer Androids use a garbage collector that does some optimization tricks with local variables, but you should avoid creating and forgetting lots of objects in the scene graph.
</p>

<p>
Older Androids use a very naive garbage collector that needs to do real work for every object, both during creation and during collection. Creating local variables can build up a heap of work, particularly if the function is called often.
</p>

<p>
To avoid creating a temporary object, use <em>local methods</em> to overwrite the contents of an existing object instead of creating a new temporary object for the result.
</p>

<p>
E.g. when you use math operations like <code>vectorA.mult(vectorB);</code>, they create new objects for the result.
</p>

<p>
Check your math operations for opportunities to use the <em>local</em> version of the math operations, e.g. <code>vectorA.multLocal(vectorB)</code>. Local methods store the result in vectorA and do not create a new object.
</p>

</div>
<!-- EDIT3 SECTION "Avoid creating new objects" [1394-3028] -->
<h2 class="sectionedit4" id="avoid_large_objects_in_physics">Avoid large objects in physics</h2>
<div class="level2">

<p>
To offload much computation to the less CPU intense physics broadphase collision check, avoid having large meshes that cover e.g. the whole map of your level. Instead, separate the collision shapes into multiple smaller chunks. Obviously, don't exaggerate the chunking, because having excessive amounts of physics objects similarly cause performance problems.
</p>

</div>
<!-- EDIT4 SECTION "Avoid large objects in physics" [3029-3433] -->
<h2 class="sectionedit5" id="check_the_statistics">Check the Statistics</h2>
<div class="level2">

<p>
SimpleApplication displays a HUD with statistics. Use <code>app.setDisplayStatView(true);</code> to activate it, and false to deactivate it. 
The StatsView counts Objects,Uniforms,Triangles,Vertices are in the scene, and it counts how many FrameBuffers, Textures, or Shaders:
</p>
<ul>
<li class="level1"><div class="li"> … were switched in the last frame (S)</div>
</li>
<li class="level1"><div class="li"> … were used during the last frame (F)</div>
</li>
<li class="level1"><div class="li"> … exist in OpenGL memory (M)</div>
</li>
</ul>

<p>
For example, <code>Textures (M)</code> tells you how many textures are currently in OpenGL memory.
</p>

<p>
Generally jME3 is well optimized and optimizes these things correctly. Read <a href="/jme3/advanced/statsview.html" class="wikilink1" title="jme3:advanced:statsview">statsview</a> to learn the details about how to interpret the statistics, how to tell whether your values are off, or whether they point out a problem.
</p>
<div class="tags"><span>
	<a href="/tag/performance.html" class="wikilink1" title="tag:performance" rel="tag">performance</a>
</span></div>

</div>
<!-- EDIT5 SECTION "Check the Statistics" [3434-] -->
