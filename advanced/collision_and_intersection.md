---
title: Collision and Intersection
---
<h1 class="sectionedit1" id="collision_and_intersection">Collision and Intersection</h1>
<div class="level1">

<p>
The term collision can be used to refer to <a href="/jme3/advanced/physics_listeners.html" class="wikilink1" title="jme3:advanced:physics_listeners">physical interactions</a> (where <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">physical objects</a> collide, push and bump off one another), and also to non-physical <em>intersections</em> in 3D space. This article is about the non-physical (mathematical) collisions.
</p>

<p>
Non-physical collision detection is interesting because it uses less computing resources than physical collision detection. The non-physical calculations are faster because they do not have any side effects such as pushing other objects or bumping off of them. Tasks such as <a href="/jme3/advanced/mouse_picking.html" class="wikilink1" title="jme3:advanced:mouse_picking">mouse picking</a> are easily implemented using mathematical techniques such as ray casting and intersections.  Experienced developers optimize their games by finding ways to simulate certain (otherwise expensive physical) interactions in a non-physical way. 
</p>

<p>
<strong>Example:</strong> One example for an optimization is a physical vehicle's wheels. You could make the wheels fully physical disks, and have jME calculate every tiny force – sounds very accurate? It's total overkill and too slow for a racing game. A more performant solution is to cast four invisible rays down from the vehicle and calculate the intersections with the floor. These non-physical wheels require (in the simplest case) only four calculations per tick to achieve an effect that players can hardly distinguish from the real thing.
</p>

</div>
<!-- EDIT1 SECTION "Collision and Intersection" [1-1432] -->
<h2 class="sectionedit2" id="collidable">Collidable</h2>
<div class="level2">

<p>
The interface com.jme3.collision.Collidable declares one method that returns how many collisions were found between two Collidables: <code>collideWith(Collidable other, CollisionResults results)</code>.
</p>
<ul>
<li class="level1"><div class="li"> A <code>com.jme3.collision.CollisionResults</code> object is an ArrayList of comparable <code>com.jme3.collision.CollisionResult</code> objects.</div>
</li>
<li class="level1"><div class="li"> You can iterate over the CollisionResults to identify the other parties involved in the collision. <br />
Note that jME counts <em>all</em> collisions, this means a ray intersecting a box will be counted as two hits, one on the front where the ray enters, and one on the back where the ray exits.</div>
</li>
</ul>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">CollisionResults Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign">size()                </td><td class="col1">Returns the number of CollisionResult objects.</td>
	</tr>
	<tr class="row2">
		<td class="col0">getClosestCollision() </td><td class="col1">Returns the CollisionResult with the lowest distance.</td>
	</tr>
	<tr class="row3">
		<td class="col0">getFarthestCollision()</td><td class="col1">Returns the CollisionResult with the farthest distance.</td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign">getCollision(i)       </td><td class="col1">Returns the CollisionResult at index i.</td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [2075-2403] -->
<p>
A CollisionResult object contains information about the second party of the collision event.
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">CollisionResult Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getContactPoint()</td><td class="col1">Returns the contact point coordinate on the second party, as Vector3f.</td>
	</tr>
	<tr class="row2">
		<td class="col0">getContactNormal()</td><td class="col1">Returns the Normal vector at the contact point, as Vector3f.</td>
	</tr>
	<tr class="row3">
		<td class="col0">getDistance()</td><td class="col1">Returns the distance between the Collidable and the second party, as float.</td>
	</tr>
	<tr class="row4">
		<td class="col0">getGeometry()</td><td class="col1">Returns the Geometry of the second party.</td>
	</tr>
	<tr class="row5">
		<td class="col0">getTriangle(t)</td><td class="col1">Binds t to the triangle t on the second party's mesh that was hit.</td>
	</tr>
	<tr class="row6">
		<td class="col0">getTriangleIndex()</td><td class="col1">Returns the index of the triangle on the second party's mesh that was hit.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2497-3030] -->
</div>
<!-- EDIT2 SECTION "Collidable" [1433-3031] -->
<h3 class="sectionedit5" id="code_sample">Code Sample</h3>
<div class="level3">

<p>
Assume you have two collidables a and b and want to detect collisions between them. The collision parties can be Geometries, Nodes with Geometries attached (including the rootNode), Planes, Quads, Lines, or Rays. An important restriction is that you can only collide geometry vs bounding volumes or rays. (This means for example that a must be of Type Node or Geometry and b respectively of Type BoundingBox, BoundingSphere or Ray.)
</p>

<p>
The following code snippet can be triggered by listeners (e.g. after an input action such as a click), or timed in the update loop.
</p>
<pre class="code java">  <span class="co1">// Calculate detection results</span>
  CollisionResults results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  a.<span class="me1">collideWith</span><span class="br0">(</span>b, results<span class="br0">)</span><span class="sy0">;</span>
  <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Number of Collisions between"</span> <span class="sy0">+</span> 
      a.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">+</span> <span class="st0">" and "</span> <span class="sy0">+</span> b.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">": "</span> <span class="sy0">+</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="co1">// Use the results</span>
  <span class="kw1">if</span> <span class="br0">(</span>results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// how to react when a collision was detected</span>
    CollisionResult closest  <span class="sy0">=</span> results.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"What was hit? "</span> <span class="sy0">+</span> closest.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Where was it hit? "</span> <span class="sy0">+</span> closest.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Distance? "</span> <span class="sy0">+</span> closest.<span class="me1">getDistance</span><span class="br0">(</span><span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
    <span class="co1">// how to react when no collision occured</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
You can also loop over all results and trigger different reactions depending on what was hit and where it was hit. In this example, we simply print info about them.
</p>
<pre class="code java">  <span class="co1">// Calculate Results</span>
  CollisionResults results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  a.<span class="me1">collideWith</span><span class="br0">(</span>b, results<span class="br0">)</span><span class="sy0">;</span>
  <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Number of Collisions between"</span> <span class="sy0">+</span> a.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">+</span> <span class="st0">" and "</span>
   <span class="sy0">+</span> b.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="st0">" : "</span> <span class="sy0">+</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="co1">// Use the results</span>
  <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// For each hit, we know distance, impact point, name of geometry.</span>
    <span class="kw4">float</span>     dist <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getDistance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    Vector3f    pt <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a>   party <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw4">int</span>        tri <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getTriangleIndex</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    Vector3f  norm <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getTriangle</span><span class="br0">(</span><span class="kw1">new</span> Triangle<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">getNormal</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Details of Collision #"</span> <span class="sy0">+</span> i <span class="sy0">+</span> <span class="st0">":"</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"  Party "</span> <span class="sy0">+</span> party <span class="sy0">+</span> <span class="st0">" was hit at "</span> <span class="sy0">+</span> pt <span class="sy0">+</span> <span class="st0">", "</span> <span class="sy0">+</span> dist <span class="sy0">+</span> <span class="st0">" wu away."</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"  The hit triangle #"</span> <span class="sy0">+</span> tri <span class="sy0">+</span> <span class="st0">" has a normal vector of "</span> <span class="sy0">+</span> norm<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

<p>
Knowing the distance of the collisions is useful for example when you intersect Lines and Rays with other objects.
</p>

</div>
<!-- EDIT5 SECTION "Code Sample" [3032-5570] -->
<h2 class="sectionedit6" id="bounding_volumes">Bounding Volumes</h2>
<div class="level2">

<p>
A <code>com.jme3.bounding.BoundingVolume</code> is an interface for dealing with containment of a collection of points. All BoundingVolumes are <code>Collidable</code> and are used as optimization to calculate non-physical collisions more quickly: It's always faster to calculate an intersection between simple shapes like spheres and boxes than between complex shapes like models. 
</p>

<p>
jME3 computes bounding volumes for all objects. These bounding volumes are later used for frustum culling, which is making sure only objects visible on-screen are actually sent for rendering. 
</p>

<p>
All fast-paced action and shooter games use BoundingVolumes as an optimization. Wrap all complex models into simpler shapes – in the end, you get equally useful collision detection results, but faster. <a href="http://en.wikipedia.org/wiki/Bounding_volume" class="urlextern" title="http://en.wikipedia.org/wiki/Bounding_volume" rel="nofollow">More about bounding volumes...</a>
</p>

<p>
Supported types:
<a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/jme/wiki-data/userref/capsule.png"><img src="/resources/fetch.php" class="mediaright" title="Capsule" alt="Capsule" width="150" height="110" /></a>
</p>
<ul>
<li class="level1"><div class="li"> Type.AABB = Axis-aligned bounding box, that means it doesn't rotate, which makes it less precise. A <code>com.jme3.bounding.BoundingBox</code> is an axis-aligned cuboid used as a container for a group of vertices of a piece of geometry. A BoundingBox has a center and extents from that center along the x, y and z axis. This is the default bounding volume, since it is fairly fast to generate and gives better accuracy than the bounding sphere.</div>
</li>
<li class="level1"><div class="li"> Type.Sphere: <code>com.jme3.bounding.BoundingSphere</code> is a sphere used as a container for a group of vertices of a piece of geometry. A BoundingSphere has a center and a radius.</div>
</li>
<li class="level1"><div class="li"> Type.OBB = Oriented bounding box. This bounding box is more precise because it can rotate with its content, but is computationally more expensive. (Currently not supported.)</div>
</li>
<li class="level1"><div class="li"> Type.Capsule = Cylinder with rounded ends, also called “swept sphere”. Typically used for mobile characters. (Currently not supported.)</div>
</li>
</ul>

<p>
</p><p></p><div class="noteclassic">Note: If you are looking for bounding volumes for physical objects, use <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">CollisionShapes</a>.
</div>


</div>
<!-- EDIT6 SECTION "Bounding Volumes" [5571-7614] -->
<h3 class="sectionedit7" id="usage">Usage</h3>
<div class="level3">

<p>
For example you can use Bounding Volumes on custom meshes, or complex non-physical shapes.
</p>
<pre class="code java">mesh.<span class="me1">setBound</span><span class="br0">(</span><span class="kw1">new</span> BoundingSphere<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mesh.<span class="me1">updateBound</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT7 SECTION "Usage" [7615-7796] -->
<h2 class="sectionedit8" id="mesh_and_scene_graph_collision">Mesh and Scene Graph Collision</h2>
<div class="level2">

<p>
One of the supported <code>Collidable</code>s are meshes and scene graph objects. To execute a collision detection query against a scene graph, use <code>Spatial.collideWith()</code>. This will traverse the scene graph and return any mesh collisions that were detected. Note that the first collision against a particular scene graph may take a long time, this is because a special data structure called <a href="http://en.wikipedia.org/wiki/Bounding_interval_hierarchy" class="urlextern" title="http://en.wikipedia.org/wiki/Bounding_interval_hierarchy" rel="nofollow">|Bounding Interval Hierarchy (BIH)</a> needs to be generated for the meshes. At a later point, the mesh could change and the BIH tree would become out of date, in that case, call <a href="http://jmonkeyengine.org/javadoc/com/jme3/scene/Mesh.html#createCollisionData()" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/scene/Mesh.html#createCollisionData()" rel="nofollow">Mesh.createCollisionData()</a> on the changed mesh to update the BIH tree.
</p>

</div>
<!-- EDIT8 SECTION "Mesh and Scene Graph Collision" [7797-8617] -->
<h2 class="sectionedit9" id="intersection">Intersection</h2>
<div class="level2">

<p>
A <code>com.jme3.math.Ray</code> is an infinite line with a beginning, a direction, and no end; whereas a <code>com.jme3.math.Line</code> is an infinite line with only a direction (no beginning, no end).
</p>

<p>
Rays are used to perform line-of-sight calculations. This means you can detect what users were “aiming at” when they clicked or pressed a key. You can also use this to detect whether game characters can see something (or someone) or not.
</p>
<ul>
<li class="level1"><div class="li"> <strong>Click to select:</strong> You can determine what a user has clicked by casting a ray from the camera forward in the direction of the camera. Now identify the closest collision of the ray with the rootNode, and you have the clicked object.</div>
</li>
<li class="level1"><div class="li"> <strong>Line of sight:</strong> Cast a ray from a player in the direction of another player. Then you detect all collisions of this ray with other entities (walls versus foliage versus window panes) and use this to calculate how likely it is that one can see the other.</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">These simple but powerful ray-surface intersection tests are called Ray Casting. As opposed to the more advanced Ray Tracing technique, Ray Casting does not follow the ray's reflection after the first hit – the ray just goes straight on.
</div>


<p>
Learn the details of how to implement <a href="/jme3/advanced/mouse_picking.html" class="wikilink1" title="jme3:advanced:mouse_picking">Mouse Picking</a> here.
</p>
<hr />

<p>
TODO:
</p>
<ul>
<li class="level1"><div class="li"> Bounding Interval Hierarchy (<code>com.jme3.collision.bih.BIHNode</code>)</div>
</li>
<li class="level1"><div class="li"> com.jme3.scene.CollisionData</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Intersection" [8618-] -->
