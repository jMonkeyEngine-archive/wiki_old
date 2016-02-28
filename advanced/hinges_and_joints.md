---
title: Physical Hinges and Joints
---
<h1 class="sectionedit1" id="physical_hinges_and_joints">Physical Hinges and Joints</h1>
<div class="level1">

<p>
The jMonkeyEngine3 has built-in support for <a href="http://jbullet.advel.cz" class="urlextern" title="http://jbullet.advel.cz" rel="nofollow">jBullet physics</a> via the <code>com.jme3.bullet</code> package.
</p>

<p>
Game Physics are not only employed to calculate collisions, but they can also simulate hinges and joints. Think of pulley chains, shaky rope bridges, swinging pendulums, or (trap)door and chest hinges. Physics are a great addition to e.g. an action or puzzle game.
</p>

<p>
In this example, we will create a pendulum. The joint is the (invisible) connection between the pendulum body and the hook. You will see that you can use what you learn from the simple pendulum and apply it to other joint/hinge objects (rope bridges, etc).
</p>

</div>
<!-- EDIT1 SECTION "Physical Hinges and Joints" [1-692] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsHingeJoint.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsHingeJoint.java" rel="nofollow">TestPhysicsHingeJoint.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [693-883] -->
<h2 class="sectionedit3" id="overview_of_this_physics_application">Overview of this Physics Application</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Create a SimpleApplication with a <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">BulletAppState</a> </div>
<ul>
<li class="level2"><div class="li"> This gives us a PhysicsSpace for PhysicsControls</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> For the pendulum, we use a Spatial with a PhysicsControl, and we apply physical forces to them.</div>
<ul>
<li class="level2"><div class="li"> The parts of the “pendulum” are Physics Control'ed Spatials with Collision Shapes. </div>
</li>
<li class="level2"><div class="li"> We create a fixed <code>hookNode</code> and a dynamic <code>pendulumNode</code>. </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> We can “crank the handle” and rotate the joint like a hinge, or we can let loose and expose the joints freely to gravity. </div>
<ul>
<li class="level2"><div class="li"> For physical forces we will use the method <code>joint.enableMotor();</code></div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Overview of this Physics Application" [884-1531] -->
<h2 class="sectionedit4" id="creating_a_fixed_node">Creating a Fixed Node</h2>
<div class="level2">

<p>
The hookNode is the fixed point from which the pendulum hangs. It has no mass. 
</p>
<pre class="code java">Node hookNode<span class="sy0">=</span>PhysicsTestHelper.<span class="me1">createPhysicsTestNode</span><span class="br0">(</span>
    assetManager, <span class="kw1">new</span> BoxCollisionShape<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span> .1f, .1f, .1f<span class="br0">)</span><span class="br0">)</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
hookNode.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setPhysicsLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>0f,<span class="nu0">0</span>,0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>hookNode<span class="br0">)</span><span class="sy0">;</span>
getPhysicsSpace<span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>hookNode<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For a rope bridge, there would be two fixed nodes where the bridge is attached to the mountainside.
</p>

</div>
<!-- EDIT4 SECTION "Creating a Fixed Node" [1532-2051] -->
<h2 class="sectionedit5" id="creating_a_dynamic_node">Creating a Dynamic Node</h2>
<div class="level2">

<p>
The pendulumNode is the dynamic part of the construction. It has a mass. 
</p>
<pre class="code java">Node pendulumNode<span class="sy0">=</span>PhysicsTestHelper.<span class="me1">createPhysicsTestNode</span><span class="br0">(</span>
    assetManager, <span class="kw1">new</span> BoxCollisionShape<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span> .3f, .3f, .3f<span class="br0">)</span><span class="br0">)</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
pendulumNode.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setPhysicsLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>0f,<span class="sy0">-</span><span class="nu0">1</span>,0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pendulumNode<span class="br0">)</span><span class="sy0">;</span>
getPhysicsSpace<span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>pendulumNode<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For a rope bridge, each set of planks would be one dynamic node. 
</p>

</div>
<!-- EDIT5 SECTION "Creating a Dynamic Node" [2052-2549] -->
<h2 class="sectionedit6" id="understanding_dof_joints_and_hinges">Understanding DOF, Joints, and Hinges</h2>
<div class="level2">

<p>
A PhysicsHingeJoint is an invisible connection between two nodes – here between the pendulum body and the hook. Why are hinges and joints represented by the same class? Hinges and joints have something in common: They constrain the <em>mechanical degree of freedom</em> (DOF) of another object. 
</p>

<p>
Consider a free falling, “unchained” object in physical 3D space: It has 6 DOFs:
</p>
<ul>
<li class="level1"><div class="li"> It translates along 3 axes</div>
</li>
<li class="level1"><div class="li"> It rotates around 3 axes</div>
</li>
</ul>

<p>
Now consider some examples of objects with joints:
</p>
<ul>
<li class="level1"><div class="li"> An individual chain link is free to spin and move around, but joined into a chain, the link's movement is restricted to stay with the surrounding links.</div>
</li>
<li class="level1"><div class="li"> A person's arm can rotate around some axes, but not around others. The shoulder joint allows one and restricts the other.</div>
</li>
<li class="level1"><div class="li"> A door hinge is one of the most restricted types of joint: It can only rotate around one axis. </div>
</li>
</ul>

<p>
You'll understand that, when creating any type of joint, it is important to correctly specify the DOFs that the joint restricts, and the DOFs that the joint allows. For the typical DOF of a <a href="/jme3/advanced/ragdoll.html" class="wikilink1" title="jme3:advanced:ragdoll">ragDoll</a> character's limbs, jME even offers a special joint, <code>ConeJoint</code>.
</p>

</div>
<!-- EDIT6 SECTION "Understanding DOF, Joints, and Hinges" [2550-3740] -->
<h2 class="sectionedit7" id="creating_the_joint">Creating the Joint</h2>
<div class="level2">

<p>
You create the HingeJoint after you have created the nodes that are to be chained together. In the code snippet you see that the HingeJoint constructor requires the two node objects. You also have to specify axes and pivots – they are the degrees of freedom that you just heard about.
</p>
<pre class="code java"><span class="kw1">private</span> HingeJoint joint<span class="sy0">;</span>
...
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ...
    <span class="co1">// hookNode and pendulumNode are created here...</span>
    ...
 
    <span class="me1">joint</span><span class="sy0">=</span><span class="kw1">new</span> HingeJoint<span class="br0">(</span>hookNode.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>, <span class="co1">// A</span>
                     pendulumNode.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>, <span class="co1">// B</span>
                     <span class="kw1">new</span> Vector3f<span class="br0">(</span>0f, 0f, 0f<span class="br0">)</span>,  <span class="co1">// pivot point local to A</span>
                     <span class="kw1">new</span> Vector3f<span class="br0">(</span>0f, 1f, 0f<span class="br0">)</span>,  <span class="co1">// pivot point local to B </span>
                     Vector3f.<span class="me1">UNIT_Z</span>,           <span class="co1">// DoF Axis of A (Z axis)</span>
                     Vector3f.<span class="me1">UNIT_Z</span>  <span class="br0">)</span><span class="sy0">;</span>        <span class="co1">// DoF Axis of B (Z axis)</span></pre>

<p>
The pivot point's position will be at <code>(0,0,0)</code> in the global 3D space. In A's local space that is at <code>(0,0,0)</code> and in B's local space (remember B's position was set to <code>(0,-1,0)</code>) that is at <code>(0,1,0)</code>.
</p>

<p>
Specify the following parameters for each joint:
</p>
<ul>
<li class="level1"><div class="li"> PhysicsControl A and B – the two nodes that are to be joined</div>
</li>
<li class="level1"><div class="li"> Vector3f pivot A and pivot B – coordinates of the attachment point relative to A and B</div>
<ul>
<li class="level2"><div class="li"> The points typically lie on the surface of the PhysicsControl's Spatials, rarely in the middle.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Vector3f axisA and axisB – around which axes each node is allowed to spin.</div>
<ul>
<li class="level2"><div class="li"> In our example, we constrain the pendulum to swing only along the Z axis.</div>
</li>
</ul>
</li>
</ul>

<p>
Remember to add all joint objects to the physicsSpace, just like you would do with any physical objects.
</p>
<pre class="code java">bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>joint<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Tip:</strong> If you want the joint to be visible, attach a geometry to the dynamic node, and translate it to its start position.
</p>

</div>
<!-- EDIT7 SECTION "Creating the Joint" [3741-5640] -->
<h2 class="sectionedit8" id="apply_physical_forces">Apply Physical Forces</h2>
<div class="level2">

<p>
You can apply forces to dynamic nodes (the ones that have a mass), and see how other joined (“chained”) objects are dragged along. 
</p>

<p>
Alternatively, you can also apply forces to the joint itself. In a game, you may want to spin an automatic revolving door, or slam a door closed in a spooky way, or dramatically open the lid of a treasure chest.
</p>

<p>
The method to call on the joint is <code>enableMotor()</code>.
</p>
<pre class="code java">joint.<span class="me1">enableMotor</span><span class="br0">(</span><span class="kw2">true</span>, <span class="nu0">1</span>, .1f<span class="br0">)</span><span class="sy0">;</span>
joint.<span class="me1">enableMotor</span><span class="br0">(</span><span class="kw2">true</span>, <span class="sy0">-</span><span class="nu0">1</span>, .1f<span class="br0">)</span><span class="sy0">;</span></pre>
<ol>
<li class="level1"><div class="li"> Switch the motor on by supplying <code>true</code></div>
</li>
<li class="level1"><div class="li"> Specify the velocity with which the joint should rotate around the specified axis. </div>
<ul>
<li class="level2"><div class="li"> Use positive and negative numbers to change direction.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Specify the impulse for this motor. Heavier masses need a bigger impulse to be moved.</div>
</li>
</ol>

<p>
When you disable the motor, the chained nodes are exposed to gravity again:
</p>
<pre class="code java">joint.<span class="me1">enableMotor</span><span class="br0">(</span><span class="kw2">false</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>,
	<a href="/tag/joint.html" class="wikilink1" title="tag:joint" rel="tag">joint</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Apply Physical Forces" [5641-] -->
