---
title: Bullet Physics Pitfalls
---
<h1 class="sectionedit1" id="bullet_physics_pitfalls">Bullet Physics Pitfalls</h1>
<div class="level1">

<p>
Bullet physics is not without its problems. Unfortunately, many of those are outside of the control of the jMonkeyEngine Core Team and thus cannot be fixed.
</p>

</div>
<!-- EDIT1 SECTION "Bullet Physics Pitfalls" [1-197] -->
<h3 class="sectionedit2" id="sweep_test_issues">Sweep Test Issues</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> When using <a href="http://jmonkeyengine.org/javadoc/com/jme3/bullet/PhysicsSpace.html#sweepTest(com.jme3.bullet.collision.shapes.CollisionShape, com.jme3.math.Transform, com.jme3.math.Transform)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/bullet/PhysicsSpace.html#sweepTest(com.jme3.bullet.collision.shapes.CollisionShape, com.jme3.math.Transform, com.jme3.math.Transform)" rel="nofollow">PhysicsSpace.sweepTest()</a>, ensure that the distance between the transforms is at least 0.4wu or greater.</div>
</li>
<li class="level1"><div class="li"> Note that the sweep will not detect collisions if it done inside of a collision shape. It must be on the edge of a collision shape to detect any collisions.</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Sweep Test Issues" [198-687] -->
<h3 class="sectionedit3" id="ghost_control_aabb_collision_only">Ghost Control AABB Collision only</h3>
<div class="level3">

<p>
As the javadoc for <a href="http://jmonkeyengine.org/javadoc/com/jme3/bullet/objects/PhysicsGhostObject.html" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/bullet/objects/PhysicsGhostObject.html" rel="nofollow">PhysicsObjectControl</a> says, the ghost object collision detection uses AABB (Axis-aligned bounding box) collision only, regardless of the collision shape it has been assigned.
</p>

<p>
<strong>Workaround:</strong><br />

Please use PhysicsSpace.sweepTest() instead, or kinematic physics objects with <a href="http://jmonkeyengine.org/javadoc/com/jme3/bullet/PhysicsSpace.html#addCollisionListener(com.jme3.bullet.collision.PhysicsCollisionListener)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/bullet/PhysicsSpace.html#addCollisionListener(com.jme3.bullet.collision.PhysicsCollisionListener)" rel="nofollow">collision listeners</a>.
</p>

</div>
<!-- EDIT3 SECTION "Ghost Control AABB Collision only" [688-1274] -->
<h3 class="sectionedit4" id="rigid_bodies_fall_through_ground">Rigid bodies fall through ground</h3>
<div class="level3">

<p>
This usually happens if the ground physics object has large triangles or consists of a large BoxCollisionShape. 
</p>

<p>
<strong>Workaround:</strong><br />

</p>
<ul>
<li class="level1"><div class="li"> For meshes with large triangles - Subdivide the mesh in a model editor such as Blender.</div>
</li>
<li class="level1"><div class="li"> For large boxes - seperate into smaller boxes or use a MeshCollisionShape for terrain instead of BoxCollisionShape.</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Rigid bodies fall through ground" [1275-] -->
