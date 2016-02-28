---
title: Physics: Gravity, Collisions, Forces
---
<h1 class="sectionedit1" id="physicsgravity_collisions_forces">Physics: Gravity, Collisions, Forces</h1>
<div class="level1">

<p>
A physics simulation is used in games and applications where objects are exposed to physical forces: Think of games like pool billiard and car racing simulators. Massive objects are pulled by gravity, forces cause objects to gain momentum, friction slows them down, solid objects collide and bounce off one another, etc. Action and Adventure games also make use of physics to implement solid obstacles, falling, and jumping.
</p>

<p>
The jMonkeyEngine3 has built-in support for <a href="http://jbullet.advel.cz" class="urlextern" title="http://jbullet.advel.cz" rel="nofollow">jBullet Physics</a> (based on <a href="http://bulletphysics.org" class="urlextern" title="http://bulletphysics.org" rel="nofollow">Bullet Physics</a>) via the <code>com.jme3.bullet</code> package. This article focuses mostly on the RigidBodyControl, but also introduces you to others. 
</p>

<p>
If you are looking for info on how to respond to physics events such as collisions, read about <a href="/jme3/advanced/physics_listeners.html" class="wikilink1" title="jme3:advanced:physics_listeners">Physics Listeners</a>.
</p>

</div>
<!-- EDIT1 SECTION "Physics: Gravity, Collisions, Forces" [1-867] -->
<h2 class="sectionedit2" id="technical_overview">Technical Overview</h2>
<div class="level2">

<p>
jME3 has a complete, slightly adapted but fully wrapped Bullet <abbr title="Application Programming Interface">API</abbr> that uses normal jME math objects (Vector3f, Quaternion etc) as input/output data. All normal bullet objects like RigidBodies, Constraints (called “Joints” in jME3) and the various collision shapes are available, all mesh formats can be converted from jME to bullet.
</p>

<p>
The PhysicsSpace object is the central object in bullet and all objects have to be added to it so they are physics-enabled. You can create multiple physics spaces as well to have multiple independent physics simulations or to run simulations in the background that you step at a different pace. You can also create a Bullet PhysicsSpace in jME3 with a <code>com.jme3.bullet.BulletAppState</code> which runs a PhysicsSpace along the update loop, which is the easiest way to instantiate a physics space. It can be run in a mode where it runs in parallel to rendering, yet syncs to the update loop so you can apply physics changes safely during the update() calls of Controls and SimpleApplication.
</p>

<p>
The base bullet objects are also available as simple to use controls that can be attached to spatials to directly control these by physics forces and influences. The RigidBodyControl for example includes a simple constructor that automatically creates a hull collision shape or a mesh collision shape based on the given input mass and the mesh of the spatial it is attached to. This makes enabling physics on a Geometry as simple as “spatial.addControl(new RigidBodyControl(1));”
</p>

<p>
Due to some differences in how bullet and jME handle the scene and other objects relations there is some things to remember about the controls implementation:
</p>
<ul>
<li class="level1"><div class="li"> The collision shape is not automatically updated when the spatial mesh changes</div>
<ul>
<li class="level2"><div class="li"> You can update it by reattaching the control or by using the CollisionShapeFactory yourself.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In bullet the scale parameter is on the collision shape (which equals the mesh in jME3) and not on the RigidBody so you cannot scale a collision shape without scaling any other RigidBody with reference of it</div>
<ul>
<li class="level2"><div class="li"> Note that you should share collision shapes in general and that j3o files loaded from file do that as well when instantiated twice so this is something to consider.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <strong>Physics objects remain in the physics space when their spatials are detached from the scene graph!</strong></div>
<ul>
<li class="level2"><div class="li"> Use PhysicsSpace.remove(physicsObject) or simply physicsControl.setEnabled(false); to remove them from the PhysicsSpace</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> If you apply forces to the physics object in an update() call they might not get applied because internally bullet still runs at 60fps while your app might run at 120.</div>
<ul>
<li class="level2"><div class="li"> You can use the PhysicsTickListener interface and register with the physics space and use the preTick() method to be sure that you actually apply the force in the right moment.</div>
</li>
<li class="level2"><div class="li"> Reading values from the physics objects in the update loop should always yield correct values but they might not change over several fames due to the same reason.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Reading or writing from the physics objects during the render phase is not recommended as this is when the physics space is stepped and would cause data corruption. This is why the debug display does not work properly in a threaded BulletAppState</div>
</li>
<li class="level1"><div class="li"> Bullet always uses world coordinates, there is no such concept as nodes so the object will be moved into a world location with no regard to its parent spatial.</div>
<ul>
<li class="level2"><div class="li"> You can configure this behavior using the setApplyPhysicsLocal() method on physics controls but remember the physics space still runs in world coordinates so you can visually detach things that will actually still collide in the physics space.</div>
</li>
<li class="level2"><div class="li"> To use the local applying to simulate e.g. the internal physics system of a train passing by, simply create another BulletAppState and add all models with physics controls in local mode to a node. When you move the node the physics will happen all the same but the objects will move along with the node.</div>
</li>
</ul>
</li>
</ul>

<p>
When you use this physics simulation, values correspond to the following units:
</p>
<ul>
<li class="level1"><div class="li"> 1 length unit (1.0f) equals 1 meter, </div>
</li>
<li class="level1"><div class="li"> 1 weight unit (1.0f) equals 1 kilogram,</div>
</li>
<li class="level1"><div class="li"> most torque and rotation values are expressed in radians.</div>
</li>
</ul>

<p>
Bullet physics runs internally at 60fps by default. This rate is not dependent on the actual framerate and it does not lock the framerate at 60fps. Instead, when the actual fps is higher than the physics framerate the system will display interpolated positions for the physics objects. When the framerate is lower than the physics framerate, the physics space will be stepped multiple times per frame to make up for the missing calculations. 
</p>

<p>
Internally, the updating and syncing of the actual physics objects in the BulletAppState happens in the following way:
</p>
<ol>
<li class="level1"><div class="li"> collision callbacks (<code>BulletAppState.update()</code>)</div>
</li>
<li class="level1"><div class="li"> user update (<code>simpleUpdate</code> in main loop, <code>update()</code> in Controls and AppStates)</div>
</li>
<li class="level1"><div class="li"> physics to scenegraph syncing and applying (<code>updateLogicalState()</code>)</div>
</li>
<li class="level1"><div class="li"> stepping physics (before or in parallel to <code>Application.render()</code>)</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Technical Overview" [868-5940] -->
<h2 class="sectionedit3" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
Full code samples are here:
</p>
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestBrickWall.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestBrickWall.java" rel="nofollow">TestBrickWall.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestQ3.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestQ3.java" rel="nofollow">TestQ3.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestSimplePhysics.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestSimplePhysics.java" rel="nofollow">TestSimplePhysics.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestWalkingChar.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestWalkingChar.java" rel="nofollow">TestWalkingChar.java</a></div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Sample Code" [5941-6588] -->
<h2 class="sectionedit4" id="physics_application">Physics Application</h2>
<div class="level2">

<p>
A short overview of how to write a jME application with Physics capabilities:
</p>

<p>
Do the following once per application to gain access to the <code>physicsSpace</code> object:
</p>
<ol>
<li class="level1"><div class="li"> Make your application extend <code>com.jme3.app.SimpleApplication</code>.</div>
</li>
<li class="level1"><div class="li"> Create a BulletAppState field: <pre class="code java"><span class="kw1">private</span> BulletAppState bulletAppState<span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Initialize your bulletAppState and attach it to the state manager: <pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
</p><p></p><div class="notetip">In your application, you can always access the <code>BulletAppState</code> via the ApplicationStateManager: 

<pre class="code java">BulletAppState bas <span class="sy0">=</span> app.<span class="me1">getStateManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getState</span><span class="br0">(</span>BulletAppState.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>

</p></div>


<p>
For each Spatial that you want to be physical:
</p>
<ol>
<li class="level1"><div class="li"> Create a CollisionShape.</div>
</li>
<li class="level1"><div class="li"> Create the PhysicsControl from the CollisionShape and a mass value.</div>
</li>
<li class="level1"><div class="li"> Add the PhysicsControl to its Spatial.</div>
</li>
<li class="level1"><div class="li"> Add the PhysicsControl to the PhysicsSpace.</div>
</li>
<li class="level1"><div class="li"> Attach the Spatial to the rootNode (as usual).</div>
</li>
<li class="level1"><div class="li"> (Optional) Implement the <code>PhysicsCollisionListener</code> interface to respond to <code>PhysicsCollisionEvent</code>s.</div>
</li>
</ol>

<p>
Let's look at the details: 
</p>

</div>
<!-- EDIT4 SECTION "Physics Application" [6589-7790] -->
<h2 class="sectionedit5" id="create_a_collisionshape">Create a CollisionShape</h2>
<div class="level2">

<p>
A CollisionShape is a simplified shape for which physics are easier to calculate than for the true shape of the model. This simplication approach speeds up the simulation greatly.
</p>

<p>
Before you can create a Physics Control, you must create a CollisionShape from the <code>com.jme3.bullet.collision.shapes</code> package. (Read the tip under “PhysicsControls Code Samples” how to use default CollisionShapes for Boxes and Spheres.)
</p>
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Non-Mesh CollisionShape     </th><th class="col1 leftalign"> Usage                                </th><th class="col2"> Examples </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> BoxCollisionShape()         </td><td class="col1"> Box-shaped behaviour, does not roll. </td><td class="col2 leftalign"> Oblong or cubic objects like bricks, crates, furniture.  </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> SphereCollisionShape()      </td><td class="col1 leftalign"> Spherical behaviour, can roll.       </td><td class="col2"> Compact objects like apples, soccer balls, cannon balls, compact spaceships. </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> CylinderCollisionShape()    </td><td class="col1"> Tube-shaped and disc-shaped behaviour, can roll on one side. </td><td class="col2"> Oblong objects like pillars. <br />
Disc-shaped objects like wheels, plates. </td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> CompoundCollisionShape()    </td><td class="col1"> A CompoundCollisionShape allows custom combinations of shapes. Use the <code>addChildShape()</code> method on the compound object to add other shapes to it and position them relative to one another. </td><td class="col2"> A car with wheels (1 box + 4 cylinders), etc. </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> CapsuleCollisionShape()     </td><td class="col1 leftalign"> A built-in compound shape of a vertical cylinder with one sphere at the top and one sphere at the bottom. Typically used with <a href="/jme3/advanced/walking_character.html" class="wikilink1" title="jme3:advanced:walking_character">CharacterControls</a>: A cylinder-shaped body does not get stuck at corners and vertical obstacles; the rounded top and bottom do not get stuck on stair steps and ground obstacles.  </td><td class="col2"> Persons, animals. </td>
	</tr>
	<tr class="row6">
		<td class="col0 leftalign"> SimplexCollisionShape()     </td><td class="col1"> A physical point, line, triangle, or rectangle Shape, defined by one to four points.</td><td class="col2">Guardrails</td>
	</tr>
	<tr class="row7">
		<td class="col0 leftalign"> PlaneCollisionShape()       </td><td class="col1"> A 2D plane. Very fast. </td><td class="col2"> Flat solid floor or wall. </td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [8249-9646] -->
<p>
All non-mesh CollisionShapes can be used for dynamic, kinematic, as well as static Spatials. (Code samples see below)
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Mesh CollisionShapes   </th><th class="col1 leftalign"> Usage                                </th><th class="col2"> Examples </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> MeshCollisionShape        </td><td class="col1"> A mesh-accurate shape for static or kinematic Spatials. Can have complex shapes with openings and appendages. <br />
<strong>Limitations:</strong> Collisions between two mesh-accurate shapes cannot be detected, only non-mesh shapes can collide with this shape. This Shape does not work with dynamic Spatials. </td><td class="col2"> A whole static game level model. </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> HullCollisionShape        </td><td class="col1"> A less accurate shape for dynamic Spatials that cannot easily be represented by a CompoundShape. <br />
<strong>Limitations:</strong> The shape is convex (behaves as if you gift-wrapped the object), i.e. openings, appendages, etc, are not individually represented. </td><td class="col2"> A dynamic 3D model. </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> GImpactCollisionShape     </td><td class="col1"> A mesh-accurate shape for dynamic Spatials. It uses <a href="http://gimpact.sourceforge.net/" class="urlextern" title="http://gimpact.sourceforge.net/" rel="nofollow">http://gimpact.sourceforge.net/</a>. <br />
<strong>Limitations:</strong> CPU intensive, use sparingly! We recommend using HullCollisionShape (or CompoundShape) instead to improve performance. Collisions between two mesh-accurate shapes cannot be detected, only non-mesh shapes can collide with this shape. </td><td class="col2"> Complex dynamic objects (like spiders) in Virtual Reality or scientific simulations. </td>
	</tr>
	<tr class="row4">
		<td class="col0"> HeightfieldCollisionShape </td><td class="col1"> A mesh-accurate shape optimized for static terrains. This shape is much faster than other mesh-accurate shapes. <br />
<strong>Limitations:</strong> Requires heightmap data. Collisions between two mesh-accurate shapes cannot be detected, only non-mesh shapes can collide with this shape.</td><td class="col2">Static terrains.</td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [9767-11284] -->
<p>
On a CollisionShape, you can apply a few properties
</p>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> CollisionShape Method </th><th class="col1"> Property </th><th class="col2"> Examples </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> setScale(new Vector3f(2f,2f,2f)) </td><td class="col1"> You can change the scale of collisionshapes (whether it be, Simple or Mesh). You cannot change the scale of a CompoundCollisionShape however. A sphere collision shape, will change its radius based on the X component of the vector passed in. You must scale a collision shape before attaching it to the physicsSpace, or you must readd it to the physicsSpace each time the scale changes. </td><td class="col2"> Scale a player in the Y axis by 2: <br />
<code>new Vector3f(1f,2f,1f)</code></td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [11338-11875] -->
<p>
The mesh-accurate shapes can use a CollisionShapeFactory as constructor (code samples see below).
</p>

<p>
</p><p></p><div class="noteimportant">Pick the simplest and most applicable shape for the mesh for what you want to do: If you give a box a sphere collision shape, it will roll; if you give a ball a box collision shape, it will sit on a slope. If the shape is too big, the object will seem to float; if the shape is too small it will seem to sink into the ground. During development and debugging, you can make collision shapes visible by adding the following line after the bulletAppState initialization: 

<pre class="code java">bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">enableDebug</span><span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span></pre>

<p>

</p></div>


</div>
<!-- EDIT5 SECTION "Create a CollisionShape" [7791-12545] -->
<h3 class="sectionedit9" id="collisionshape_code_samples">CollisionShape Code Samples</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> One way of using a constructor and a Geometry's mesh for static Spatials:<pre class="code java">MeshCollisionShape level_shape <span class="sy0">=</span> 
    <span class="kw1">new</span> MeshCollisionShape<span class="br0">(</span>level_geo.<span class="me1">getMesh</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> One way of using a constructor and a Geometry's mesh for dynamic Spatials:<pre class="code java">HullCollisionShape shape <span class="sy0">=</span> 
    <span class="kw1">new</span> HullCollisionShape<span class="br0">(</span>katamari_geo.<span class="me1">getMesh</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Creating a dynamic compound shape for a whole Node and subnodes:<pre class="code java">CompoundCollisionShape myComplexShape <span class="sy0">=</span>
    CollisionShapeFactory.<span class="me1">createMeshShape</span><span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> myComplexGeometry <span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Creating a dynamic HullCollisionShape shape (or CompoundCollisionShape with HullCollisionShapes as children) for a Geometry:<pre class="code java">CollisionShape shape <span class="sy0">=</span> 
    CollisionShapeFactory.<span class="me1">createDynamicMeshShape</span><span class="br0">(</span>spaceCraft<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> An angular, non-mesh-accurate compound shape:<pre class="code java">CompoundCollisionShape boxShape <span class="sy0">=</span>
    CollisionShapeFactory.<span class="me1">createBoxShape</span><span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> crate_geo<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> A round, non-mesh-accurate compound shape: <pre class="code java">SphereCollisionShape sphereShape <span class="sy0">=</span>
    <span class="kw1">new</span> SphereCollisionShape<span class="br0">(</span>1.0f<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "CollisionShape Code Samples" [12546-13664] -->
<h2 class="sectionedit10" id="create_physicscontrol">Create PhysicsControl</h2>
<div class="level2">

<p>
BulletPhysics are available in jME3 through PhysicsControls classes from the com.jme3.bullet.control package. jME3's PhysicsControl classes directly extend BulletPhysics objects and are the recommended way to use physics in a jME3 application. PhysicsControls are flexible and can be added to any Spatial to make it act according to physical properties. 
</p>
<div class="table sectionedit11"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Standard PhysicsControls</th><th class="col1"> Usage</th><th class="col2"> Examples </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">RigidBodyControl</td><td class="col1">The most commonly used PhysicsControl. You can use it for dynamic objects (solid objects that freely affected by collisions, forces, or gravity), for static objects (solid but not affected by any forces), or kinematic objects (remote-controlled solid objects). </td><td class="col2">Impacting projectiles, moving obstacles like crates, rolling and bouncing balls, elevators, flying aircaft or space ships. <br />
Solid immobile floors, walls, static obstacles.</td>
	</tr>
	<tr class="row2">
		<td class="col0">GhostControl</td><td class="col1">Use for collision and intersection detection between physical objects. A GhostControl itself is <em>non-solid</em> and invisible. GhostControl moves with the Spatial it is attached to. Use GhostControls to <a href="/jme3/advanced/physics_listeners.html" class="wikilink1" title="jme3:advanced:physics_listeners">implement custom game interactions</a> by adding it to a visible Geometry. </td><td class="col2">A monster's “aggro radius”, CharacterControl collisions, motion detectors, photo-electric alarm sensors, poisonous or radioactive perimeters, life-draining ghosts, etc. </td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [14056-15035] --><div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Special PhysicsControls</th><th class="col1"> Usage</th><th class="col2"> Examples </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">VehicleControl <br />
PhysicsVehicleWheel</td><td class="col1"> Special Control used for <a href="/jme3/advanced/vehicles.html" class="wikilink1" title="jme3:advanced:vehicles">"terrestrial"  vehicles with suspension and wheels</a>. </td><td class="col2">Cars, tanks, hover crafts, ships, motorcycles…</td>
	</tr>
	<tr class="row2">
		<td class="col0">CharacterControl</td><td class="col1">Special Control used for <a href="/jme3/advanced/walking_character.html" class="wikilink1" title="jme3:advanced:walking_character">Walking Character</a>s.</td><td class="col2">Upright walking persons, animals, robots… </td>
	</tr>
	<tr class="row3">
		<td class="col0">RagDollControl</td><td class="col1">Special Control used for <a href="/jme3/advanced/ragdoll.html" class="wikilink1" title="jme3:advanced:ragdoll">collapsing, flailing, or falling characters</a> </td><td class="col2">Falling persons, animals, robots, “Rag dolls”</td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [15037-15549] -->
<p>
Click the links for details on the special PhysicsControls. This article is about RigidBodyControl.
</p>

</div>
<!-- EDIT10 SECTION "Create PhysicsControl" [13665-15651] -->
<h3 class="sectionedit13" id="physics_control_code_samples">Physics Control Code Samples</h3>
<div class="level3">

<p>
The most commonly used physics control is RigidBodyControl.  The RigidBodyControl constructor takes up to two parameters:  a collision shape and a mass (a float in kilograms).  The mass parameter also determines whether the object is dynamic (movable) or static (fixed). For a static object such as a floor or wall, specify zero mass. 
</p>
<pre class="code java">RigidBodyControl myThing_phys <span class="sy0">=</span> 
    <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span> myThing_shape , 123.0f <span class="br0">)</span><span class="sy0">;</span> <span class="co1">// dynamic</span></pre>
<pre class="code java">RigidBodyControl myDungeon_phys <span class="sy0">=</span> 
    <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span> myDungeon_shape , 0.0f <span class="br0">)</span><span class="sy0">;</span> <span class="co1">// static </span></pre>

<p>
</p><p></p><div class="noteimportant">If you give your floor a non-zero mass, it will fall out of the scene!
</div>


<p>
The following creates a box Geometry with the correct default BoxCollisionShape:
</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
Geometry box_geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>
box_geo.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> RigidBodyControl<span class="br0">(</span> 1.0f <span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// explicit non-zero mass, implicit BoxCollisionShape</span></pre>

<p>
The following creates a MeshCollisionShape for a whole loaded (static) scene:
</p>
<pre class="code java">...
<span class="me1">gameLevel</span>.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>0.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// explicit zero mass, implicit MeshCollisionShape</span></pre>

<p>
</p><p></p><div class="notetip">Spheres and Boxes automatically fall back on the correct default CollisionShape if you do not specify a CollisionShape in the RigidBodyControl constructor. Complex static objects can fall back on MeshCollisionShapes, unless it is a Node, in which case it will become a CompoundCollisionShape containing a MeshCollisionShape
</div>


</div>
<!-- EDIT13 SECTION "Physics Control Code Samples" [15652-17169] -->
<h2 class="sectionedit14" id="add_physicscontrol_to_spatial">Add PhysicsControl to Spatial</h2>
<div class="level2">

<p>
For each physical Spatial in the scene:
</p>
<ol>
<li class="level1"><div class="li"> Add a PhysicsControl to a Spatial. <pre class="code java">myThing_geo.<span class="me1">addControl</span><span class="br0">(</span>myThing_phys<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Remember to also attach the Spatial to the rootNode, as always!</div>
</li>
</ol>

</div>
<!-- EDIT14 SECTION "Add PhysicsControl to Spatial" [17170-17417] -->
<h2 class="sectionedit15" id="add_physicscontrol_to_physicsspace">Add PhysicsControl to PhysicsSpace</h2>
<div class="level2">

<p>
The PhysicsSpace is an object in BulletAppState that is like a rootNode for Physics Controls. 
</p>
<ul>
<li class="level1"><div class="li"> Just like you add the Geometry to the rootNode, you add its PhysicsControl to the PhysicsSpace. <pre class="code java">bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>myThing_phys<span class="br0">)</span><span class="sy0">;</span> 
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>myThing_geo<span class="br0">)</span><span class="sy0">;</span> </pre>
</div>
</li>
<li class="level1"><div class="li"> When you remove a Geometry from the scene and detach it from the rootNode, also remove the PhysicsControl from the PhysicsSpace: <pre class="code java">bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">remove</span><span class="br0">(</span>myThing_phys<span class="br0">)</span><span class="sy0">;</span>
myThing_geo.<span class="me1">removeFromParent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">You can either add the <em>PhysicsControl</em> to the PhysicsSpace, or add the PhysicsControl to the Geometry and then add the <em>Geometry</em> to the PhysicsSpace. jME3 understands both and the outcome is the same.
</div>


</div>
<!-- EDIT15 SECTION "Add PhysicsControl to PhysicsSpace" [17418-18233] -->
<h2 class="sectionedit16" id="changing_the_scale_of_a_physicscontrol">Changing the Scale of a PhysicsControl</h2>
<div class="level2">

<p>
To change the scale of a PhysicsControl you must change the scale of the collisionshape which belongs to it.
</p>

<p>
MeshCollisionShapes can have a scale correctly set, but it only works when being constructed on a geometry (not a node). CompoundCollisionShapes cannot be scaled at this time(the type obtained when creating a CollisionShape from a Node i.e using imported models).
</p>

<p>
When you import a model from blender, it often comes as a Node (even if it only contains 1 mesh), which is by de-facto automatically converted to a CompoundCollisionShape. So when you try to scale this it won't work! Below illustrates an example, of how to scale an imported model:
</p>
<pre class="code java"><span class="co1">// Doesn't scale</span>
<span class="co1">// This modified version contains Node -&gt; Geometry (name = "MonkeyHeadGeom")</span>
Spatial model <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/MonkeyHead.j3o"</span><span class="br0">)</span><span class="sy0">;</span> model.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> RigidBodyControl<span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Won't work as this is now a CompoundCollisionShape containing a MeshCollisionShape</span>
model.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">getCollisionShape</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setScale</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">2</span>, <span class="nu0">2</span>, <span class="nu0">2</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> 
bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>model<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Works fine</span>
Spatial model <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/MonkeyHead.j3o"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Same Model</span>
 <span class="co1">// IMPORTANT : You must navigate to the Geometry for this to work</span>
Geometry geom <span class="sy0">=</span> <span class="br0">(</span><span class="br0">(</span>Geometry<span class="br0">)</span> <span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> model<span class="br0">)</span>.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"MonkeyHeadGeom"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
geom.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> RigidBodyControl<span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Works great (scaling of a MeshCollisionShape)	</span>
geom.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">getCollisionShape</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setScale</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">2</span>, <span class="nu0">2</span>, <span class="nu0">2</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
With the corresponding output below:
<a href="http://i.imgur.com/fAXlF.png" class="urlextern" title="http://i.imgur.com/fAXlF.png" rel="nofollow">External Link</a>
<a href="http://i.imgur.com/Josua.png" class="urlextern" title="http://i.imgur.com/Josua.png" rel="nofollow">External Link</a>
</p>

</div>
<!-- EDIT16 SECTION "Changing the Scale of a PhysicsControl" [18234-19984] -->
<h3 class="sectionedit17" id="physicsspace_code_samples">PhysicsSpace Code Samples</h3>
<div class="level3">

<p>
The PhysicsSpace also manages global physics settings. Typically, you can leave the defaults, and you don't need to change the following settings, but it's good to know what they are for:
</p>
<div class="table sectionedit18"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">bulletAppState.getPhysicsSpace() Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setGravity(new Vector3f(0, -9.81f, 0));</td><td class="col1">Specifies the global gravity.</td>
	</tr>
	<tr class="row2">
		<td class="col0">setAccuracy(1f/60f);</td><td class="col1">Specifies physics accuracy. The higher the accuracy, the slower the game. Decrease value if objects are passing through one another, or bounce oddly. (e.g. Change value from 1f/60f to something like 1f/80f.) </td>
	</tr>
	<tr class="row3">
		<td class="col0">setMaxSubSteps(4);</td><td class="col1">Compensates low FPS: Specifies the maximum amount of extra steps that will be used to step the physics when the game fps is below the physics fps. This maintains determinism in physics in slow (low-fps) games. For example a maximum number of 2 can compensate for framerates as low as 30 fps (physics has a default accuracy of 60 fps). Note that setting this value too high can make the physics drive down its own fps in case its overloaded.</td>
	</tr>
	<tr class="row4">
		<td class="col0">setWorldMax(new Vector3f(10000f, 10000f, 10000f)); <br />
setWorldMin(new Vector3f(-10000f, -10000f, -10000f));</td><td class="col1">Specifies the size of the physics space as two opposite corners (only applies to AXIS_SWEEP broadphase).</td>
	</tr>
</table></div>
<!-- EDIT18 TABLE [20211-21239] -->
</div>
<!-- EDIT17 SECTION "PhysicsSpace Code Samples" [19985-21240] -->
<h2 class="sectionedit19" id="specify_physical_properties">Specify Physical Properties</h2>
<div class="level2">

<p>
After you have registered, attached, and added everything, you can adjust physical properties or apply forces.
</p>

<p>
On a RigidBodyControl, you can set the following physical properties.
</p>
<div class="table sectionedit20"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> RigidBodyControl Method </th><th class="col1"> Property </th><th class="col2"> Examples </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> setGravity(new Vector3f(0f,-9.81f,0f)) </td><td class="col1"> You can change the gravity of individual physics objects after they were added to the PhysicsSpace. Gravity is a vector pointing from this Spatial towards the source of gravity. The longer the vector, the stronger is gravity. <br />
If gravity is the same absolute direction for all objects (e.g. on a planet surface), set this vector globally on the PhysicsSpace object and not individually. <br />
If the center of gravity is relative (e.g. towards a black hole) then setGravity() on each Spatial to constantly adjust the gravity vectors at each tick of their update() loops.</td><td class="col2">For planet earth: <br />
<code>new Vector3f(0f,-9.81f,0f)</code></td>
	</tr>
	<tr class="row2">
		<td class="col0"> setMass(1f) </td><td class="col1"> Sets the mass in kilogram. Dynamic objects have masses &gt; 0.0f. Heavy dynamic objects need more force to be moved and light ones move with small amounts of force. <br />
Static immobile objects (walls, floors, including buildings and terrains) must have a mass of zero! </td><td class="col2"> Person: 60f, ball: 1.0f <br />
Floor: 0.0f (!)</td>
	</tr>
	<tr class="row3">
		<td class="col0"> setFriction(1f) </td><td class="col1"> Friction. <br />
Slippery objects have low friction. The ground has high friction. </td><td class="col2"> Ice, slides: 0.0f <br />
Soil, concrete, rock: 1.0f </td>
	</tr>
	<tr class="row4">
		<td class="col0"> setRestitution(0.0f) </td><td class="col1"> Bounciness. By default objects are not bouncy (0.0f). For a bouncy rubber object set this &gt; 0.0f. <br />
Both the object and the surface must have non-zero restitution for bouncing to occur. <br />
This setting has an impact on performance, so use it sparingly. </td><td class="col2"> Brick: 0.0f <br />
Rubber ball: 1.0f </td>
	</tr>
	<tr class="row5">
		<td class="col0">setCcdMotionThreshold()</td><td class="col1">The amount of motion in 1 physics tick to trigger the continuous motion detection in moving objects that push one another. Rarely used, but necessary if your moving objects get stuck or roll through one another.</td><td class="col2">around 0.5 to 1 * object diameter</td>
	</tr>
</table></div>
<!-- EDIT20 TABLE [21465-23247] -->
<p>
On a RigidBodyControl, you can apply the following physical forces:
</p>
<div class="table sectionedit21"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> RigidBodyControl Method </th><th class="col1"> Motion </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> setPhysicsLocation()</td><td class="col1">Positions the objects. Do not use setLocalTranslation() for physical objects. Important: Make certain not to make CollisionShapes overlap when positioning them. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> setPhysicsRotation()</td><td class="col1">Rotates the object. Do not use setLocalRotate() for physical objects.</td>
	</tr>
	<tr class="row3">
		<td class="col0"> setKinematic(true) </td><td class="col1"> By default, RigidBodyControls are dynamic (kinematic=false) and are affected by forces. If you set kinematic=true, the object is no longer affected by forces, but it still affects others. A kinematic is solid, and must have a mass. <br />
(See detailed explanation below.) </td>
	</tr>
</table></div>
<!-- EDIT21 TABLE [23318-23928] -->
</div>
<!-- EDIT19 SECTION "Specify Physical Properties" [21241-23928] -->
<h3 class="sectionedit22" id="kinematic_vs_dynamic_vs_static">Kinematic vs Dynamic vs Static</h3>
<div class="level3">

<p>
All physical objects…
</p>
<ul>
<li class="level1"><div class="li"> must not overlap. </div>
</li>
<li class="level1"><div class="li"> can detect collisions and report several values about the impact.</div>
</li>
<li class="level1"><div class="li"> can respond to collisions dynamically, or statically, or kinematically.</div>
</li>
</ul>
<div class="table sectionedit23"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0"> Property </td><th class="col1"> Static </th><th class="col2"> Kinematic </th><th class="col3"> Dynamic </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> Examples</th><td class="col1">Immobile obstacles: Floors, walls, buildings, …</td><td class="col2">Remote-controlled solid objects: Airships, meteorites, elevators, doors; networked or remote-controlled NPCs; invisible “airhooks” for hinges and joints.</td><td class="col3">Interactive objects: Rolling balls, movable crates, falling pillars, zero-g space ship…</td>
	</tr>
	<tr class="row2">
		<th class="col0"> Does it have a mass?</th><td class="col1">no, 0.0f</td><td class="col2">yes<sup><a href="#fn__1" id="fnt__1" class="fn_top">1)</a></sup>, &gt;0.0f </td><td class="col3">yes, &gt;0.0f</td>
	</tr>
	<tr class="row3">
		<th class="col0"> How does it move?</th><td class="col1">never</td><td class="col2">setLocalTranslation();</td><td class="col3">setLinearVelocity(); applyForce(); <br />
setWalkDirection(); for CharacterControl</td>
	</tr>
	<tr class="row4">
		<th class="col0"> How to place in scene?</th><td class="col1">setPhysicsLocation(); <br />
setPhysicsRotation()</td><td class="col2">setLocalTranslation(); <br />
setLocalRotation();</td><td class="col3">setPhysicsLocation(); <br />
 setPhysicsRotation()</td>
	</tr>
	<tr class="row5">
		<th class="col0"> Can it move and push others?</th><td class="col1">no</td><td class="col2">yes</td><td class="col3">yes</td>
	</tr>
	<tr class="row6">
		<th class="col0"> Is is affected by forces? <br />
(Falls when it mid-air? Can be pushed by others?)</th><td class="col1">no</td><td class="col2">no</td><td class="col3">yes</td>
	</tr>
	<tr class="row7">
		<th class="col0"> How to activate this behaviour? </th><td class="col1">setMass(0f); <br />
setKinematic(false); </td><td class="col2">setMass(1f); <br />
setKinematic(true);</td><td class="col3">setMass(1f); <br />
setKinematic(false);</td>
	</tr>
</table></div>
<!-- EDIT23 TABLE [24165-25224] -->
</div>

<h4 id="when_do_i_use_kinematic_objects">When Do I Use Kinematic Objects?</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> Kinematics are solid and characters can “stand” on them.</div>
</li>
<li class="level1"><div class="li"> When they collide, Kinematics push dynamic objects, but a dynamic object never pushes a Kinematic. </div>
</li>
<li class="level1"><div class="li"> You can hang kinematics up “in mid-air” and attach other PhysicsControls to them using <a href="/jme3/advanced/hinges_and_joints.html" class="wikilink1" title="jme3:advanced:hinges_and_joints">hinges and joints</a>. Picture them as “air hooks” for flying aircraft carriers, floating islands in the clouds, suspension bridges, swings, chains… </div>
</li>
<li class="level1"><div class="li"> You can use Kinematics to create mobile remote-controlled physical objects, such as moving elevator platforms, flying blimps/airships. You have full control how Kinematics move, they never “fall” or “topple over”.</div>
</li>
</ul>

<p>
</p><p></p><div class="noteimportant">The position of a kinematic RigidBodyControl is updated automatically depending on its spatial's translation. You move Spatials with a kinematic RigidBodyControl programmatically, that means you write translation and rotation code in the update loop. You describe the motion of kinematic objects either by using methods such as <code>setLocalTranslation()</code> or <code>move()</code>, or by using a <a href="/jme3/advanced/motionpath.html" class="wikilink1" title="jme3:advanced:motionpath">MotionPath</a>. 
</div>


</div>
<!-- EDIT22 SECTION "Kinematic vs Dynamic vs Static" [23929-26330] -->
<h2 class="sectionedit24" id="forcesmoving_dynamic_objects">Forces: Moving Dynamic Objects</h2>
<div class="level2">

<p>
Use the following methods to move dynamic physical objects.
</p>
<div class="table sectionedit25"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> PhysicsControl Method </th><th class="col1"> Motion </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> setLinearVelocity(new Vector3f(0f,0f,1f)) </td><td class="col1"> Set the linear speed of this object. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> setAngularVelocity(new Vector3f(0f,0f,1f)) </td><td class="col1"> Set the rotational speed of the object; the x, y and z component are the speed of rotation around that axis. </td>
	</tr>
	<tr class="row3">
		<td class="col0"> applyCentralForce(…) </td><td class="col1 leftalign"> Move (push) the object once with a certain moment, expressed as a Vector3f.  </td>
	</tr>
	<tr class="row4">
		<td class="col0"> applyForce(…) </td><td class="col1"> Move (push) the object once with a certain moment, expressed as a Vector3f. Optionally, you can specify where on the object the pushing force hits. </td>
	</tr>
	<tr class="row5">
		<td class="col0"> applyTorque(…) </td><td class="col1"> Rotate (twist) the object once around its axes, expressed as a Vector3f. </td>
	</tr>
	<tr class="row6">
		<td class="col0"> applyImpulse(…) </td><td class="col1"> An idealised change of momentum. This is the kind of push that you would use on a pool billiard ball. </td>
	</tr>
	<tr class="row7">
		<td class="col0"> applyTorqueImpulse(…) </td><td class="col1"> An idealised change of momentum. This is the kind of push that you would use on a pool billiard ball. </td>
	</tr>
	<tr class="row8">
		<td class="col0"> clearForces()</td><td class="col1">Cancels out all forces (force, torque) etc and stops the motion.</td>
	</tr>
</table></div>
<!-- EDIT25 TABLE [26436-27425] -->
<p>
</p><p></p><div class="noteimportant">It is technically possible to position PhysicsControls using setLocalTranslation(), e.g. to place them in their start position in the scene. However you must be very careful not to cause an “impossible state” where one physical object overlaps with another! Within the game, you typically use the setters shown here exclusively.
</div>


<p>
PhysicsControls also support the following advanced features:
</p>
<div class="table sectionedit26"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> PhysicsControl Method </th><th class="col1"> Property </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> setCollisionShape(collisionShape)</td><td class="col1">Changes the collision shape after creation.</td>
	</tr>
	<tr class="row2">
		<td class="col0"> setCollideWithGroups() <br />
setCollisionGroup() <br />
addCollideWithGroup(COLLISION_GROUP_01) <br />
removeCollideWithGroup(COLLISION_GROUP_01)</td><td class="col1">Collision Groups are integer bit masks – enums are available in the CollisionObject. All physics objects are by default in COLLISION_GROUP_01. Two objects collide when the collideWithGroups set of one contains the Collision Group of the other. Use this to improve performance by grouping objects that will never collide in different groups (the the engine saves times because it does not need to check on them).</td>
	</tr>
	<tr class="row3">
		<td class="col0"> setDamping(float, float)</td><td class="col1">The first value is the linear threshold and the second the angular. This simulates dampening of forces, for example for underwater scenes.</td>
	</tr>
	<tr class="row4">
		<td class="col0"> setAngularFactor(1f)</td><td class="col1">Set the amount of rotation that will be applied. A value of zero will cancel all rotational force outcome. (?)</td>
	</tr>
	<tr class="row5">
		<td class="col0"> setSleepingThreshold(float,float)</td><td class="col1">Sets the sleeping thresholds which define when the object gets deactivated to save resources. The first value is the linear threshold and the second the angular. Low values keep the object active when it barely moves (slow precise performance), high values put the object to sleep immediately (imprecise fast performance). (?) </td>
	</tr>
	<tr class="row6">
		<td class="col0"> setCcdMotionThreshold(0f) </td><td class="col1">Sets the amount of motion that has to happen in one physics tick to trigger the continuous motion detection in moving objects that push one another. This avoids the problem of fast objects moving through other objects. Set to zero to disable (default).</td>
	</tr>
	<tr class="row7">
		<td class="col0"> setCcdSweptSphereRadius(.5f)</td><td class="col1">Bullet does not use the full collision shape for continuous collision detection, instead it uses a “swept sphere” shape to approximate a motion, which can be imprecise and cause strange behaviors such as objects passing through one another or getting stuck. Only relevant for fast moving dynamic bodies. </td>
	</tr>
</table></div>
<!-- EDIT26 TABLE [27843-29798] -->
<p>
</p><p></p><div class="notetip"> You can <code>setApplyPhysicsLocal(true)</code> for an object to make it move relatively to its local physics space. You would do that if you need a physics space that moves with a node (e.g. a spaceship with artificial gravity surrounded by zero-g space). By default, it's set to false, and all movement is relative to the world.
</div>


</div>
<!-- EDIT24 SECTION "Forces: Moving Dynamic Objects" [26331-30140] -->
<h2 class="sectionedit27" id="best_practices">Best Practices</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <strong>Multiple Objects Too Slow?</strong> Do not overuse PhysicsControls. Although PhysicsControls are put to “sleep” when they are not moving, creating a world solely out of dynamic physics objects will quickly bring you to the limits of your computer's capabilities. <br />
<strong>Solution:</strong> Improve performance by replacing some physical Spatials with non-physical Spatials. Use the non-physical ones for non-solid things for which you do not need to detect collisions – foliage, plants, effects, ghosts, all remote or unreachable objects.</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> <strong>Complex Shape Too Slow?</strong> Breaking the level into manageable pieces helps the engine improve performance: The less CPU-intensive <a href="http://en.wikipedia.org/wiki/Sweep_and_prune" class="urlextern" title="http://en.wikipedia.org/wiki/Sweep_and_prune" rel="nofollow">broadphase</a> filters out parts of the scene that are out of reach. It only calculates the collisions for objects that are actually close to the action. <br />
<strong>Solution:</strong> A huge static city or terrain model should never be loaded as one huge mesh. Divide the scene into multiple physics objects, with each its own CollisionShape. Choose the most simple CollisionShape possible; use mesh-accurate shapes only for the few cases where precision is more important than speed. For example, you can use the very fast <code>PlaneCollisionShape</code> for flat streets, floors and the outside edge of the scene, if you keep these pieces separate.</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> <strong>Eject?</strong> If you have physical nodes jittering wildy and being ejected “for no apparent reason”, it means you have created an impossible state – solid objects overlapping. This can happen when you position solid spatials too close to other solid spatials, e.g. when moving them with setLocalTranslation(). <br />
<strong>Solution:</strong> Use the debug mode to make CollisionShapes visible and verify that CollisionShapes do not overlap. <pre class="code java">bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">enableDebug</span><span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> <strong>Buggy?</strong> If you get weird behaviour, such as physical nodes passing through one another, or getting stuck for no reason. <br />
<strong>Solution:</strong> Look at the physics space accessors and change the acuracy and other parameters.</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> <strong>Need more interactivity?</strong> You can actively <em>control</em> a physical game by triggering forces. You may also want to be able <em>respond</em> to collisions, e.g. by substracting health, awarding points, or by playing a sound. <br />
<strong>Solution:</strong> To specify how the game responds to collisions, you use <a href="/jme3/advanced/physics_listeners.html" class="wikilink1" title="jme3:advanced:physics_listeners">Physics Listeners</a>.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/control.html" class="wikilink1" title="tag:control" rel="tag">control</a>
</span></div>

</div>
<!-- EDIT27 SECTION "Best Practices" [30141-] --><div class="footnotes">
<div class="fn"><sup><a href="#fnt__1" id="fn__1" class="fn_bot">1)</a></sup> 
Inertia is calculated for kinematic objects, and you need mass to do that.</div>
</div>
