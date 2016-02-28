---
title: Ragdoll Physics
---
<h1 class="sectionedit1" id="ragdoll_physics">Ragdoll Physics</h1>
<div class="level1">

<p>
The jMonkeyEngine3 has built-in support for <a href="http://jbullet.advel.cz" class="urlextern" title="http://jbullet.advel.cz" rel="nofollow">jBullet physics</a> via the <code>com.jme3.bullet</code> package. Physics are not only responsible for handing collisions, but they also make <a href="/jme3/advanced/hinges_and_joints.html" class="wikilink1" title="jme3:advanced:hinges_and_joints">hinges and joints</a> possible. One special example of physical joints are ragdoll physics, shown here.
</p>

<p>
<a href="/resources/jme3-advanced-ragdoll.png" class="media" title="jme3:advanced:ragdoll.png"><img src="/resources/jme3-advanced-ragdoll.png" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT1 SECTION "Ragdoll Physics" [1-385] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestRagDoll.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestRagDoll.java" rel="nofollow">TestRagDoll.java</a> (Tip: Click to pull the ragdoll up)</div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestBoneRagdoll.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestBoneRagdoll.java" rel="nofollow">TestBoneRagdoll.java</a> – This ragdoll replaces a rigged model of a character in the moment it is “shot” to simulate a collapsing person. (Also note DoF of the limbs.)</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [386-891] -->
<h2 class="sectionedit3" id="preparing_the_physics_game">Preparing the Physics Game</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Create a SimpleApplication with a <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">BulletAppState</a></div>
<ul>
<li class="level2"><div class="li"> This gives us a PhysicsSpace for PhysicControls</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Add a physical floor (A box collision shape with mass zero)</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Preparing the Physics Game" [892-1130] -->
<h2 class="sectionedit4" id="creating_the_ragdoll">Creating the Ragdoll</h2>
<div class="level2">

<p>
A ragdoll is a simple “person” (dummy) that you build out of cylinder collision shapes. The ragdoll has 11 limbs: 1 for shoulders, 1 for the body, 1 for hips; plus 2 arms and 2 legs that are made up of two limbs each. In your game, you will likely replace the cylinders with your own (better looking) limb models. In this example here we just use simple cylinders.
</p>

</div>
<!-- EDIT4 SECTION "Creating the Ragdoll" [1131-1530] -->
<h3 class="sectionedit5" id="limbs">Limbs</h3>
<div class="level3">

<p>
Since you're just creating the ragdoll for this example, all the limbs have the same shape, and you can write a simple helper method to create them. The function returns a PhysicsControl with CollisionShape with the width, height, location, and rotation (vertical or horizontal) that you specify. You choose a CapsuleCollisionShape (a cylinder with rounded top and bottom) so the limbs collide smoothly against one another.
</p>
<pre class="code java"><span class="kw1">private</span> Node createLimb<span class="br0">(</span><span class="kw4">float</span> width, <span class="kw4">float</span> height, Vector3f location, <span class="kw4">boolean</span> rotate<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw4">int</span> axis <span class="sy0">=</span> rotate <span class="sy0">?</span> PhysicsSpace.<span class="me1">AXIS_X</span> <span class="sy0">:</span> PhysicsSpace.<span class="me1">AXIS_Y</span><span class="sy0">;</span>
        CapsuleCollisionShape shape <span class="sy0">=</span> <span class="kw1">new</span> CapsuleCollisionShape<span class="br0">(</span>width, height, axis<span class="br0">)</span><span class="sy0">;</span>
        Node node <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Limb"</span><span class="br0">)</span><span class="sy0">;</span>
        RigidBodyControl rigidBodyControl <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>shape, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        node.<span class="me1">setLocalTranslation</span><span class="br0">(</span>location<span class="br0">)</span><span class="sy0">;</span>
        node.<span class="me1">addControl</span><span class="br0">(</span>rigidBodyControl<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> node<span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
You write a custom helper method to initialize the limbs. Look at the screenshot above for orientation.
</p>
<ul>
<li class="level1"><div class="li"> All cylinders have the same diameter, 0.2f.</div>
</li>
<li class="level1"><div class="li"> You make the body and shoulders longer than the other limbs, 1.0f instead of 0.5f.</div>
</li>
<li class="level1"><div class="li"> You determine the coordinates for positioning the limbs to form a person.</div>
</li>
<li class="level1"><div class="li"> The shoulders and hips are <em>vertical</em> cylinders, this is why we set the rotation to true.</div>
</li>
</ul>
<pre class="code java">Node shoulders <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 1.0f, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.00f, 1.5f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
Node     uArmL <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.75f, 0.8f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Node     uArmR <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.75f, 0.8f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Node     lArmL <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.75f,<span class="sy0">-</span>0.2f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Node     lArmR <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.75f,<span class="sy0">-</span>0.2f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Node      body <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 1.0f, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.00f, 0.5f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Node      hips <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.00f,<span class="sy0">-</span>0.5f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
Node     uLegL <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.25f,<span class="sy0">-</span>1.2f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Node     uLegR <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.25f,<span class="sy0">-</span>1.2f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Node     lLegL <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.25f,<span class="sy0">-</span>2.2f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Node     lLegR <span class="sy0">=</span> createLimb<span class="br0">(</span>0.2f, 0.5f, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.25f,<span class="sy0">-</span>2.2f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You now have the outline of a person. But if you ran the application now, the individual limbs would fall down independently of one another – the ragdoll is still lacking joints.
</p>

</div>
<!-- EDIT5 SECTION "Limbs" [1531-3945] -->
<h3 class="sectionedit6" id="joints">Joints</h3>
<div class="level3">

<p>
As before, you write a small helper method. This time its purpose is to quickly join two limbs A and B at the connection point that we specify.
</p>
<ul>
<li class="level1"><div class="li"> Convert A's and B's connectionPoint vector from world coordinate space to local coordinate space.</div>
</li>
<li class="level1"><div class="li"> Use a ConeJoint, a special joint that approximates the degree of freedom that limbs typically have. The ConeJoint constructor requires the two nodes, and the two local pivot coordinates that we just determined.</div>
</li>
<li class="level1"><div class="li"> Set the joints limits to allow swinging, but not twisting.<pre class="code java"><span class="kw1">private</span> PhysicsJoint join<span class="br0">(</span>Node A, Node B, Vector3f connectionPoint<span class="br0">)</span> <span class="br0">{</span>
        Vector3f pivotA <span class="sy0">=</span> A.<span class="me1">worldToLocal</span><span class="br0">(</span>connectionPoint, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        Vector3f pivotB <span class="sy0">=</span> B.<span class="me1">worldToLocal</span><span class="br0">(</span>connectionPoint, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        ConeJoint joint <span class="sy0">=</span> <span class="kw1">new</span> ConeJoint<span class="br0">(</span>A.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>,
                                        B.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>,
                                        pivotA, pivotB<span class="br0">)</span><span class="sy0">;</span>
        joint.<span class="me1">setLimit</span><span class="br0">(</span>1f, 1f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> joint<span class="sy0">;</span>
<span class="br0">}</span></pre>
</div>
</li>
</ul>

<p>
Use the helper method to connect all limbs with joints where they belong, at one end of the limb.
</p>
<pre class="code java">join<span class="br0">(</span>body,  shoulders, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.00f,  1.4f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>body,       hips, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.00f, <span class="sy0">-</span>0.5f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>uArmL, shoulders, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.75f,  1.4f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>uArmR, shoulders, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.75f,  1.4f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>uArmL,     lArmL, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.75f,  0.4f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>uArmR,     lArmR, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.75f,  0.4f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>uLegL,      hips, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.25f, <span class="sy0">-</span>0.5f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>uLegR,      hips, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.25f, <span class="sy0">-</span>0.5f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>uLegL,     lLegL, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.25f, <span class="sy0">-</span>1.7f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
join<span class="br0">(</span>uLegR,     lLegR, <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.25f, <span class="sy0">-</span>1.7f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now the ragdoll is connected. If you ran the app now, the doll would collapse, but the limbs would stay together.
</p>

</div>
<!-- EDIT6 SECTION "Joints" [3946-5791] -->
<h3 class="sectionedit7" id="attaching_everything_to_the_scene">Attaching Everything to the Scene</h3>
<div class="level3">

<p>
We create one (non-physical) Node named ragDoll, and attach all other nodes to it.
</p>
<pre class="code java">ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>shoulders<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>body<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>hips<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>uArmL<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>uArmR<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>lArmL<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>lArmR<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>uLegL<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>uLegR<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>lLegL<span class="br0">)</span><span class="sy0">;</span>
ragDoll.<span class="me1">attachChild</span><span class="br0">(</span>lLegR<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To use the ragdoll in a scene, we attach its main node to the rootNode, and to the PhysicsSpace.
</p>
<pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>ragDoll<span class="br0">)</span><span class="sy0">;</span>
bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addAll</span><span class="br0">(</span>ragDoll<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT7 SECTION "Attaching Everything to the Scene" [5792-6450] -->
<h2 class="sectionedit8" id="applying_forces">Applying Forces</h2>
<div class="level2">

<p>
To pull the doll up, you could add an input handler that triggers the following action:
</p>
<pre class="code java">Vector3f upforce <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">200</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
shoulders.<span class="me1">applyContinuousForce</span><span class="br0">(</span><span class="kw2">true</span>, upforce<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
We can use the action to pick the doll up and put it back on its feet, or what ever. Read more about <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">Forces</a> here.
</p>

</div>
<!-- EDIT8 SECTION "Applying Forces" [6451-6852] -->
<h2 class="sectionedit9" id="detecting_collisions">Detecting Collisions</h2>
<div class="level2">

<p>
Read the <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">Responding to a PhysicsCollisionEvent</a> chapter in the general physics documentation on how to detect collisions. You can detect collisions between limbs or between limbs and the floor, and trigger game events.
</p>

</div>
<!-- EDIT9 SECTION "Detecting Collisions" [6853-7170] -->
<h2 class="sectionedit10" id="best_practices">Best Practices</h2>
<div class="level2">

<p>
If you experience weird behaviour in a ragdoll – such as exploding into pieces and then reassembling – check your collision shapes. Verify you did not position the limbs too close to one another when assmebling the ragdoll. You typically see physical nodes being ejected when their collision shapes intersect, which puts physics in an impossible state.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>,
	<a href="/tag/character.html" class="wikilink1" title="tag:character" rel="tag">character</a>,
	<a href="/tag/npc.html" class="wikilink1" title="tag:npc" rel="tag">NPC</a>,
	<a href="/tag/forces.html" class="wikilink1" title="tag:forces" rel="tag">forces</a>,
	<a href="/tag/collisions.html" class="wikilink1" title="tag:collisions" rel="tag">collisions</a>
</span></div>

</div>
<!-- EDIT10 SECTION "Best Practices" [7171-] -->
