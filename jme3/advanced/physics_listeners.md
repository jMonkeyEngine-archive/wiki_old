---
title: Physics Listeners
---
<h1 class="sectionedit1" id="physics_listeners">Physics Listeners</h1>
<div class="level1">

<p>
You can control physical objects (push them around) by applying physical forces to them. Typically, you also want to respond to the resulting collisions, e.g. by substracting health points or by playing a sound. To specify how the game responds to such physics events, you use Physics Listeners.
</p>

</div>
<!-- EDIT1 SECTION "Physics Listeners" [1-329] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestCollisionListener.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestCollisionListener.java" rel="nofollow">TestCollisionListener.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestAttachGhostObject.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestAttachGhostObject.java" rel="nofollow">TestAttachGhostObject.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestGhostObject.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestGhostObject.java" rel="nofollow">TestGhostObject.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [330-809] -->
<h2 class="sectionedit3" id="physicsghostobjects">PhysicsGhostObjects</h2>
<div class="level2">

<p>
Attach a com.jme3.bullet.control.GhostControl to any Spatial to turn it into a PhysicsGhostObject. Ghost objects automatically follow their spatial and detect collisions. The attached ghost itself is invisible and non-solid (!) and doesn't interfere with your game otherwise, it only passively reports collisions. 
</p>

<p>
You can leave the GhostControl non-solid and invisible and attach it to an (invisible) Node in the scene to create something like a motion detector. But a GhostControl also works fine when added to spatials that are solid (with RigidBodyControl) and visible (with Geometry). One use case for GhostControls is to check for collisions among <a href="/jme3/advanced/walking_character.html" class="wikilink1" title="jme3:advanced:walking_character">CharacterControls</a> when the characters are walking.
</p>

<p>
The shape of the ghost depends on the CollisionShape that you gave the GhostControl. This means that the GhostControl's shape can be different from the RigidBodyControl's shape. For example, the non-solid ghost shape can be bigger than the solid shape of the Spatial (so you can “feel” ahead).
</p>
<pre class="code java">GhostControl ghost <span class="sy0">=</span> <span class="kw1">new</span> GhostControl<span class="br0">(</span>
  <span class="kw1">new</span> BoxCollisionShape<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// a box-shaped ghost</span>
Node node <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"a ghost-controlled thing"</span><span class="br0">)</span><span class="sy0">;</span>
node.<span class="me1">addControl</span><span class="br0">(</span>ghost<span class="br0">)</span><span class="sy0">;</span>                         <span class="co1">// the ghost follows this node</span>
<span class="co1">// Optional: Add a Geometry, or other controls, to the node if you need to</span>
...
<span class="co1">// attach everything to activate it</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>node<span class="br0">)</span><span class="sy0">;</span>
getPhysicsSpace<span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>ghost<span class="br0">)</span><span class="sy0">;</span></pre>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Ghost methods</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getOverlappingObjects()</td><td class="col1">Returns the List of objects that are currently colliding (overlapping) with the ghost.</td>
	</tr>
	<tr class="row2">
		<td class="col0">getOverlappingCount()</td><td class="col1">Returns the number of currently colliding objects.</td>
	</tr>
	<tr class="row3">
		<td class="col0">getOverlapping(i)</td><td class="col1">Get PhysicsCollisionObject number i.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2299-2565] -->
</div>
<!-- EDIT3 SECTION "PhysicsGhostObjects" [810-2566] -->
<h2 class="sectionedit5" id="physics_tick_listener">Physics Tick Listener</h2>
<div class="level2">

<p>
The jBullet Physics implementation is stepped at a constant 60 physics ticks per second frame rate.
Applying forces or checking for overlaps only has an effect right at a physics update cycle, which is not every frame. If you do physics interactions at arbitrary spots in the simpleUpdate() loop, calls will be dropped at irregular intervals, because they happen out of cycle.
</p>

</div>
<!-- EDIT5 SECTION "Physics Tick Listener" [2567-2979] -->
<h3 class="sectionedit6" id="when_not_to_use_tick_listener">When (Not) to Use Tick Listener?</h3>
<div class="level3">

<p>
When you write game mechanics that apply forces, you must implement a tick listener (com.jme3.bullet.PhysicsTickListener) for it. The tick listener makes certain the forces are not dropped, but applied in time for the next physics tick.
</p>

<p>
Also, when you check for overlaps of two physical objects using a GhostControl, you cannot just go <code>ghost.getOverLappingObjects()</code> somewhere outside the update loop. You have to make certain 1 physics tick has passed before the overlapping objects list is filled with data. Again, the PhysicsTickListener does the timing for you.
</p>

<p>
When your game mechanics however just poll the current state (e.g. getPhysicsLocation()) of physical objects, or if you only use the GhostControl like a sphere trigger inside an update loop, then you don't need an extra PhysicsTickListener.
</p>

</div>
<!-- EDIT6 SECTION "When (Not) to Use Tick Listener?" [2980-3836] -->
<h3 class="sectionedit7" id="how_to_listen_to_physics_ticks">How to Listen to Physics Ticks</h3>
<div class="level3">

<p>
Here's is the declaration of an examplary Physics Control that listens to ticks. (The example shows a RigidBodyControl, but it can also be GhostControl.)
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyCustomControl
    <span class="kw1">extends</span> RigidBodyControl <span class="kw1">implements</span> PhysicsTickListener <span class="br0">{</span> ... <span class="br0">}</span></pre>

<p>
When you implement the interface, you have to implement <code>physicsTick()</code> and <code>preTick()</code> methods.
</p>
<ul>
<li class="level1"><div class="li"> <code>prePhysicsTick(PhysicsSpace space, float tpf)</code> is called before each step, here you apply forces (change the state).</div>
</li>
<li class="level1"><div class="li"> <code>physicsTick(PhysicsSpace space, float tpf)</code> is called after each step, here you poll the results (get the current state).</div>
</li>
</ul>

<p>
The tpf value is time per frame in seconds. You can use it as a factor to time actions so they run equally on slow and fast machines.
</p>
<pre class="code java">@override
<span class="kw1">public</span> <span class="kw4">void</span> prePhysicsTick<span class="br0">(</span>PhysicsSpace space, <span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
  <span class="co1">// apply state changes ...</span>
<span class="br0">}</span>
@override
<span class="kw1">public</span> <span class="kw4">void</span> physicsTick<span class="br0">(</span>PhysicsSpace space, <span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
  <span class="co1">// poll game state ...</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT7 SECTION "How to Listen to Physics Ticks" [3837-4856] -->
<h2 class="sectionedit8" id="physics_collision_listener">Physics Collision Listener</h2>
<div class="level2">

</div>
<!-- EDIT8 SECTION "Physics Collision Listener" [4857-4896] -->
<h3 class="sectionedit9" id="when_not_to_use_collision_listener">When (Not) to Use Collision Listener</h3>
<div class="level3">

<p>
If you do not implement the Collision Listener interface (com.jme3.bullet.collision.PhysicsCollisionListener), a collisions will just mean that physical forces between solid objects are applied automatically. If you just want “Balls rolling, bricks falling” you do not need a listener.
</p>

<p>
If however you want to respond to a collision event (com.jme3.bullet.collision.PhysicsCollisionEvent) with a custom action, then you need to implement the PhysicsCollisionListener interface. Typical actions triggered by collisions include:
</p>
<ul>
<li class="level1"><div class="li"> Increasing a counter (e.g. score points)</div>
</li>
<li class="level1"><div class="li"> Decreasing a counter (e.g. health points)</div>
</li>
<li class="level1"><div class="li"> Triggering an effect (e.g. explosion)</div>
</li>
<li class="level1"><div class="li"> Playing a sound (e.g. explosion, ouch)</div>
</li>
<li class="level1"><div class="li"> … and countless more, depending on your game</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "When (Not) to Use Collision Listener" [4897-5699] -->
<h3 class="sectionedit10" id="how_to_listen_to_collisions">How to Listen to Collisions</h3>
<div class="level3">

<p>
You need to add the PhysicsCollisionListener to the physics space before collisions will be listened for. Here's an example of a Physics Control that uses a collision listener. (The example shows a RigidBodyControl, but it can also be GhostControl.)
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyCustomControl <span class="kw1">extends</span> RigidBodyControl
    <span class="kw1">implements</span> PhysicsCollisionListener <span class="br0">{</span>
    <span class="kw1">public</span> MyCustomControl<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addCollisionListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
        ...
    <span class="br0">}</span></pre>

<p>
To respond to the PhysicsCollisionEvent you now have to override the <code>collision()</code> method in MyCustomControl. This gives you access to the <code>event</code> object. Mostly you will be interested in the identity of any two nodes that collided: <code>event.getNodeA()</code> and <code>event.getNodeB()</code>.
</p>

<p>
After you identify the colliding nodes, specify the action to trigger when this pair collides. Note that you cannot know which one will be Node A or Node B, you have to deal with either variant.
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> collision<span class="br0">(</span>PhysicsCollisionEvent event<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span> event.<span class="me1">getNodeA</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"player"</span><span class="br0">)</span> <span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">final</span> Node node <span class="sy0">=</span> event.<span class="me1">getNodeA</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co3">/** ... do something with the node ... */</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span> event.<span class="me1">getNodeB</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"player"</span><span class="br0">)</span> <span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">final</span> Node node <span class="sy0">=</span> event.<span class="me1">getNodeB</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co3">/** ... do something with the node ... */</span>
        <span class="br0">}</span>
    <span class="br0">}</span></pre>

<p>
</p><p></p><div class="noteimportant">Note that after the collision() method ends, the PhysicsCollisionEvent is cleared. You must get all objects and values you need within the collision() method.
</div>


</div>
<!-- EDIT10 SECTION "How to Listen to Collisions" [5700-7311] -->
<h3 class="sectionedit11" id="reading_details_from_a_physicscollisionevent">Reading Details From a PhysicsCollisionEvent</h3>
<div class="level3">

<p>
The PhysicsCollisionEvent <code>event</code> gives you access to detailed information about the collision. You already know the event objects can identify which nodes collided, but it even knows how hard they collided:
</p>
<div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign">Method                        </th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> getObjectA() <br />
getObjectB()     </td><td class="col1"> The two participants in the collision. You cannot know in advance whether some node will be recorded as A or B, you always have to consider both cases. </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> getAppliedImpulse()          </td><td class="col1"> A float value representing the collision impulse </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> getAppliedImpulseLateral1()  </td><td class="col1"> A float value representing the lateral collision impulse </td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> getAppliedImpulseLateral2()  </td><td class="col1"> A float value representing the lateral collision impulse </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> getCombinedFriction()        </td><td class="col1"> A float value representing the collision friction </td>
	</tr>
	<tr class="row6">
		<td class="col0 leftalign"> getCombinedRestitution()     </td><td class="col1"> A float value representing the collision restitution (bounciness) </td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [7578-8263] -->
<p>
Note that after the collision method has been called the object is not valid anymore so you should copy any data you want to keep into local variables.
</p>

</div>
<!-- EDIT11 SECTION "Reading Details From a PhysicsCollisionEvent" [7312-8416] -->
<h3 class="sectionedit13" id="collision_groups">Collision Groups</h3>
<div class="level3">

<p>
You can improve performance by resricting the number of tests that collision detection has to perform. If you have a case where you are only interested in collisions between certain objects but not others, you can assign sets of physical obejcts to different collision groups.
</p>

<p>
For example, for a click-to-select, you only care if the selection ray collides with a few selectable objects such as dropped weapons or powerups (one group), but not with non-selectables such as floors or walls (different group). 
</p>
<pre class="code java">myNode.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setCollisionGroup</span><span class="br0">(</span>PhysicsCollisionObject.<span class="me1">COLLISION_GROUP_02</span><span class="br0">)</span><span class="sy0">;</span>
myNode.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setCollideWithGroups</span><span class="br0">(</span>PhysicsCollisionObject.<span class="me1">COLLISION_GROUP_02</span><span class="br0">)</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>,
	<a href="/tag/collision.html" class="wikilink1" title="tag:collision" rel="tag">collision</a>,
	<a href="/tag/forces.html" class="wikilink1" title="tag:forces" rel="tag">forces</a>,
	<a href="/tag/interaction.html" class="wikilink1" title="tag:interaction" rel="tag">interaction</a>
</span></div>

</div>
<!-- EDIT13 SECTION "Collision Groups" [8417-] -->
