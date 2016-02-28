---
title: Walking Character
---
<h1 class="sectionedit1" id="walking_character">Walking Character</h1>
<div class="level1">

<p>
In the <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a> tutorial and the <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestQ3.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestQ3.java" rel="nofollow">TestQ3.java</a> code sample you have seen how to create collidable landscapes and walk around in a first-person perspective. The first-person camera is enclosed by a collision shape and is steered by the BetterCharacterControl. 
</p>

<p>
Other games however require a third-person perspective of the character: In these cases you use a CharacterControl on a Spatial. This example also shows how to set up custom navigation controls, so you can press WASD to make the third-person character walk; and how to implement dragging the mouse to rotate.
</p>

<p>
</p><p></p><div class="notewarning">Some details on this page still need to be updated from old CharacterControl <abbr title="Application Programming Interface">API</abbr> to BetterCharacterControl <abbr title="Application Programming Interface">API</abbr>.
</div>


</div>
<!-- EDIT1 SECTION "Walking Character" [1-869] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
Several related code samples can be found here:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestPhysicsCharacter.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestPhysicsCharacter.java" rel="nofollow">TestPhysicsCharacter.java</a> (third-person view)</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestWalkingChar.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestWalkingChar.java" rel="nofollow">TestWalkingChar.java</a> (third-person view)</div>
<ul>
<li class="level2"><div class="li"> Uses also <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/BombControl.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/BombControl.java" rel="nofollow">BombControl.java</a> </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestQ3.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/bullet/TestQ3.java" rel="nofollow">TestQ3.java</a> (first-person view)</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/helloworld/HelloCollision.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/helloworld/HelloCollision.java" rel="nofollow">HelloCollision.java</a> (first-person view)</div>
</li>
</ul>

<p>
The code in this tutorial is a combination of these samples.
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [870-1788] -->
<h2 class="sectionedit3" id="bettercharactercontrol">BetterCharacterControl</h2>
<div class="level2">

<p>
Motivation: When you load a character model, give it a RigidBodyControl, and use forces to push it around, you do not get the desired behaviour: RigidBodyControl'ed objects (such as cubes and spheres) roll or tip over when pushed by physical forces. This is not the behaviour that you expect of a walking character. JME3's BulletPhysics integration offers a BetterCharacterControl with a <code>setWalkDirection()</code> method. You use it to create simple characters that treat floors and walls as solid, and always stays locked upright while moving.
</p>

<p>
This code sample creates a simple upright Character:
</p>
<pre class="code java"><span class="co1">// Load any model</span>
Node myCharacter <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/myCharacterModel.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>myCharacter<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Create a appropriate physical shape for it</span>
CapsuleCollisionShape capsuleShape <span class="sy0">=</span> <span class="kw1">new</span> CapsuleCollisionShape<span class="br0">(</span>1.5f, 6f, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
CharacterControl myCharacter_phys <span class="sy0">=</span> <span class="kw1">new</span> CharacterControl<span class="br0">(</span>capsuleShape, 0.01f<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Attach physical properties to model and PhysicsSpace</span>
myCharacter.<span class="me1">addControl</span><span class="br0">(</span>myCharacter_phys<span class="br0">)</span><span class="sy0">;</span>
bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>myCharacter_phys<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To use the BetterCharacterControl, you may load your character like this:
</p>
<pre class="code java"><span class="co1">// Load any model</span>
Spatial playerSpatial <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Oto/Oto.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
player <span class="sy0">=</span>  <span class="br0">(</span>Node<span class="br0">)</span>playerSpatial<span class="sy0">;</span> <span class="co1">// You can set the model directly to the player. (We just wanted to explicitly show that it's a spatial.)</span>
Node playerNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// You can create a new node to wrap your player to adjust the location. (This allows you to solve issues with character sinking into floor, etc.)</span>
playerNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// add it to the wrapper</span>
player.<span class="me1">move</span><span class="br0">(</span><span class="nu0">0</span>,3.5f,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// adjust position to ensure collisions occur correctly.</span>
player.<span class="me1">setLocalScale</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// optionally adjust scale of model</span>
<span class="co1">// setup animation:</span>
        control <span class="sy0">=</span> player.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        control.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
        channel <span class="sy0">=</span> control.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"stand"</span><span class="br0">)</span><span class="sy0">;</span>
playerControl <span class="sy0">=</span> <span class="kw1">new</span> BetterCharacterControl<span class="br0">(</span>1.5f, 6f, 1f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// construct character. (If your character bounces, try increasing height and weight.)</span>
playerNode.<span class="me1">addControl</span><span class="br0">(</span>playerControl<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// attach to wrapper</span>
<span class="co1">// set basic physical properties:</span>
        playerControl.<span class="me1">setJumpForce</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,5f,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> 
        playerControl.<span class="me1">setGravity</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,1f,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
playerControl.<span class="me1">warp</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">10</span>,<span class="nu0">10</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// warp character into landscape at particular location</span>
<span class="co1">// add to physics state</span>
        bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>playerControl<span class="br0">)</span><span class="sy0">;</span> 
        bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addAll</span><span class="br0">(</span>playerNode<span class="br0">)</span><span class="sy0">;</span> 
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>playerNode<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// add wrapper to root</span></pre>

<p>
</p><p></p><div class="noteimportant">The BulletPhysics CharacterControl only collides with “real” PhysicsControls (RigidBody). It does not detect collisions with other CharacterControls! If you need additional collision checks, add GhostControls to your characters and create a custom <a href="/jme3/advanced/physics_listeners.html" class="wikilink1" title="jme3:advanced:physics_listeners">collision listener</a> to respond. (The JME3 team may implement a better CharacterControl one day.)
</div>


<p>
A CharacterControl is a special kinematic object with restricted movement. CharacterControls have a fixed “upward” axis, this means they do not topple over when walking over an obstacle (as opposed to RigidBodyControls), which simulates a being's ability to balance upright. A CharacterControl can jump and fall along its upward axis, and it can scale steps of a certain height/steepness.
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> CharacterControl Method </th><th class="col1"> Property </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> setUpAxis(1)</td><td class="col1"> Fixed upward axis. Values: 0 = X axis , 1 = Y axis , 2 = Z axis. <br />
Default: 1, because for characters and vehicles, up is typically along the Y axis.</td>
	</tr>
	<tr class="row2">
		<td class="col0"> setJumpSpeed(10f) </td><td class="col1"> Jump speed (movement along upward-axis) </td>
	</tr>
	<tr class="row3">
		<td class="col0"> setFallSpeed(20f) </td><td class="col1"> Fall speed (movement opposite to upward-axis) </td>
	</tr>
	<tr class="row4">
		<td class="col0"> setMaxSlope(1.5f) </td><td class="col1"> How steep the slopes and steps are that the character can climb without considering them an obstacle. Higher obstacles need to be jumped. Vertical height in world units. </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> setGravity(1f)   </td><td class="col1"> The intensity of gravity for this CharacterControl'ed entity. Tip: To change the direction of gravity for a character, modify the up axis.</td>
	</tr>
	<tr class="row6">
		<td class="col0"> setWalkDirection(new Vector3f(0f,0f,0.1f))</td><td class="col1"> (CharacterControl only) Make a physical character walk continuously while checking for floors and walls as solid obstacles. This should probably be called “setPositionIncrementPerSimulatorStep”. This argument is neither a direction nor a velocity, but the amount to increment the position each physics tick: vector length = accuracy*speed in m/s. <br />
Use <code>setWalkDirection(Vector3f.ZERO)</code> to stop a directional motion. </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [5266-6429] -->
<p>
For best practices on how to use <code>setWalkDirection()</code>, see the Navigation Inputs example below.
</p>

</div>
<!-- EDIT3 SECTION "BetterCharacterControl" [1789-6528] -->
<h2 class="sectionedit5" id="walking_character_demo">Walking Character Demo</h2>
<div class="level2">

</div>
<!-- EDIT5 SECTION "Walking Character Demo" [6529-6564] -->
<h3 class="sectionedit6" id="code_skeleton">Code Skeleton</h3>
<div class="level3">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> WalkingCharacterDemo <span class="kw1">extends</span> SimpleApplication
        <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a>, AnimEventListener <span class="br0">{</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    WalkingCharacterDemo app <span class="sy0">=</span> <span class="kw1">new</span> WalkingCharacterDemo<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span> <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> isPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span> <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> onAnimCycleDone<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span> <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> onAnimChange<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span> <span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "Code Skeleton" [6565-7182] -->
<h3 class="sectionedit7" id="overview">Overview</h3>
<div class="level3">

<p>
To create a walking character:
</p>
<ol>
<li class="level1"><div class="li"> (Unless you already have it) Activate physics in the scene by adding a <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">BulletAppState</a>.</div>
</li>
<li class="level1"><div class="li"> Init the scene by loading the game level model (terrain or floor/buildings), and giving the scene a MeshCollisionShape.</div>
</li>
<li class="level1"><div class="li"> Create the animated character:</div>
<ol>
<li class="level2"><div class="li"> Load an animated character model.</div>
</li>
<li class="level2"><div class="li"> Add a CharacterControl to the model.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Set up animation channel and controllers.</div>
</li>
<li class="level1"><div class="li"> Add a ChaseCam or CameraNode.</div>
</li>
<li class="level1"><div class="li"> Handle navigational inputs.</div>
</li>
</ol>

</div>
<!-- EDIT7 SECTION "Overview" [7183-7706] -->
<h3 class="sectionedit8" id="activate_physics">Activate Physics</h3>
<div class="level3">
<pre class="code java"><span class="kw1">private</span> BulletAppState bulletAppState<span class="sy0">;</span>
...
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//bulletAppState.setThreadingType(BulletAppState.ThreadingType.PARALLEL);</span>
    stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span>
    ...
<span class="br0">}</span></pre>

</div>
<!-- EDIT8 SECTION "Activate Physics" [7707-8000] -->
<h3 class="sectionedit9" id="initialize_the_scene">Initialize the Scene</h3>
<div class="level3">

<p>
In the simpleInitApp() method you initialize the scene and give it a MeshCollisionShape. The sample in the jme3 sources uses a custom helper class that simply creates a flat floor and drops some cubes and spheres on it:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="me1">PhysicsTestHelper</span>.<span class="me1">createPhysicsTestWorld</span><span class="br0">(</span>rootNode,
      assetManager, bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  ...</pre>

<p>
In a real game, you would load a scene model here instead of a test world. You can load a model from a local or remote zip file, and scale and position it:
</p>
<pre class="code java"><span class="kw1">private</span> Node gameLevel<span class="sy0">;</span>
..
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="co1">//assetManager.registerLocator("quake3level.zip", ZipLocator.class);</span>
  assetManager.<span class="me1">registerLocator</span><span class="br0">(</span>
  <span class="st0">"http://jmonkeyengine.googlecode.com/files/quake3level.zip"</span>,
    HttpZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
  MaterialList matList <span class="sy0">=</span> <span class="br0">(</span>MaterialList<span class="br0">)</span> assetManager.<span class="me1">loadAsset</span><span class="br0">(</span><span class="st0">"Scene.material"</span><span class="br0">)</span><span class="sy0">;</span>
  OgreMeshKey key <span class="sy0">=</span> <span class="kw1">new</span> OgreMeshKey<span class="br0">(</span><span class="st0">"main.meshxml"</span>, matList<span class="br0">)</span><span class="sy0">;</span>
  gameLevel <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadAsset</span><span class="br0">(</span>key<span class="br0">)</span><span class="sy0">;</span>
  gameLevel.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="sy0">-</span><span class="nu0">20</span>, <span class="sy0">-</span><span class="nu0">16</span>, <span class="nu0">20</span><span class="br0">)</span><span class="sy0">;</span>
  gameLevel.<span class="me1">setLocalScale</span><span class="br0">(</span>0.10f<span class="br0">)</span><span class="sy0">;</span>
  gameLevel.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> RigidBodyControl<span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  rootNode.<span class="me1">attachChild</span><span class="br0">(</span>gameLevel<span class="br0">)</span><span class="sy0">;</span>
  bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addAll</span><span class="br0">(</span>gameLevel<span class="br0">)</span><span class="sy0">;</span>
  ...</pre>

<p>
Also, add a light source to be able to see the scene.
</p>
<pre class="code java">  AmbientLight light <span class="sy0">=</span> <span class="kw1">new</span> AmbientLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  light.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span>.<span class="me1">mult</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  rootNode.<span class="me1">addLight</span><span class="br0">(</span>light<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT9 SECTION "Initialize the Scene" [8001-9467] -->
<h3 class="sectionedit10" id="create_the_animated_character">Create the Animated Character</h3>
<div class="level3">

<p>
You create an animated model, such as Oto.mesh.xml.
</p>
<ol>
<li class="level1"><div class="li"> Place the “Oto” model into the <code>assets/Models/Oto/</code> directory of your project.</div>
</li>
<li class="level1"><div class="li"> Create the CollisionShape and adjust the capsule radius and height to fit your character model.</div>
</li>
<li class="level1"><div class="li"> Create the CharacterControl and adjust the stepheight (here 0.05f) to the height that the character can climb up without jumping.</div>
</li>
<li class="level1"><div class="li"> Load the visible model. Make sure its start position does not overlap with scene objects.</div>
</li>
<li class="level1"><div class="li"> Add the CharacterControl to the model and register it to the physicsSpace.</div>
</li>
<li class="level1"><div class="li"> Attach the visible model to the rootNode.</div>
</li>
</ol>
<pre class="code java"><span class="kw1">private</span> CharacterControl character<span class="sy0">;</span>
<span class="kw1">private</span> Node model<span class="sy0">;</span>
...
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="me1">CapsuleCollisionShape</span> capsule <span class="sy0">=</span> <span class="kw1">new</span> CapsuleCollisionShape<span class="br0">(</span>3f, 4f<span class="br0">)</span><span class="sy0">;</span>
  character <span class="sy0">=</span> <span class="kw1">new</span> CharacterControl<span class="br0">(</span>capsule, 0.05f<span class="br0">)</span><span class="sy0">;</span>
  character.<span class="me1">setJumpSpeed</span><span class="br0">(</span>20f<span class="br0">)</span><span class="sy0">;</span>
  model <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Oto/Oto.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
  model.<span class="me1">addControl</span><span class="br0">(</span>character<span class="br0">)</span><span class="sy0">;</span>
  bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>character<span class="br0">)</span><span class="sy0">;</span>
  rootNode.<span class="me1">attachChild</span><span class="br0">(</span>model<span class="br0">)</span><span class="sy0">;</span>
  ...</pre>

<p>
</p><p></p><div class="notetip"><strong>Did you know?</strong> A CapsuleCollisionShape is a cylinder with rounded top and bottom. A capsule rotated upright is a good collision shape for a humanoid character since its roundedness reduces the risk of getting stuck on obstacles.
</div>


</div>
<!-- EDIT10 SECTION "Create the Animated Character" [9468-10805] -->
<h3 class="sectionedit11" id="set_up_animcontrol_and_animchannels">Set Up AnimControl and AnimChannels</h3>
<div class="level3">

<p>
Create several AnimChannels, one for each animation that can happen simultaneously. In this example, you create one channel for walking and one for attacking. (Because the character can attack with its arms and walk with the rest of the body at the same time.)
</p>
<pre class="code java"><span class="kw1">private</span> AnimChannel animationChannel<span class="sy0">;</span>
<span class="kw1">private</span> AnimChannel attackChannel<span class="sy0">;</span>
<span class="kw1">private</span> AnimControl animationControl<span class="sy0">;</span>
...
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="me1">animationControl</span> <span class="sy0">=</span> model.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
  animationControl.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
  animationChannel <span class="sy0">=</span> animationControl.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  attackChannel <span class="sy0">=</span> animationControl.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  attackChannel.<span class="me1">addBone</span><span class="br0">(</span>animationControl.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getBone</span><span class="br0">(</span><span class="st0">"uparm.right"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  attackChannel.<span class="me1">addBone</span><span class="br0">(</span>animationControl.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getBone</span><span class="br0">(</span><span class="st0">"arm.right"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  attackChannel.<span class="me1">addBone</span><span class="br0">(</span>animationControl.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getBone</span><span class="br0">(</span><span class="st0">"hand.right"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  ...</pre>

<p>
The attackChannel only controls one arm, while the walking channels controls the whole character.
</p>

</div>
<!-- EDIT11 SECTION "Set Up AnimControl and AnimChannels" [10806-11831] -->
<h3 class="sectionedit12" id="add_chasecam_cameranode">Add ChaseCam / CameraNode</h3>
<div class="level3">
<pre class="code java"><span class="kw1">private</span> ChaseCamera chaseCam<span class="sy0">;</span>
 
...
 
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="me1">flyCam</span>.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
  chaseCam <span class="sy0">=</span> <span class="kw1">new</span> ChaseCamera<span class="br0">(</span>cam, model, inputManager<span class="br0">)</span><span class="sy0">;</span>
  ...</pre>

</div>
<!-- EDIT12 SECTION "Add ChaseCam / CameraNode" [11832-12051] -->
<h3 class="sectionedit13" id="handle_navigation">Handle Navigation</h3>
<div class="level3">

<p>
Configure custom key bindings for WASD keys that you will use to make the character walk. Then calculate the vector where the user wants the character to move. Note the use of the special <code>setWalkDirection()</code> method below.
</p>
<pre class="code java"><span class="co1">// track directional input, so we can walk left-forward etc</span>
<span class="kw1">private</span> <span class="kw4">boolean</span> left <span class="sy0">=</span> <span class="kw2">false</span>, right <span class="sy0">=</span> <span class="kw2">false</span>, up <span class="sy0">=</span> <span class="kw2">false</span>, down <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
...
 
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="co1">// configure mappings, e.g. the WASD keys</span>
  inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"CharLeft"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_A</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"CharRight"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_D</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"CharForward"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_W</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"CharBackward"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_S</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"CharJump"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_RETURN</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"CharAttack"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"CharLeft"</span>, <span class="st0">"CharRight"</span><span class="br0">)</span><span class="sy0">;</span>
  inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"CharForward"</span>, <span class="st0">"CharBackward"</span><span class="br0">)</span><span class="sy0">;</span>
  inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"CharJump"</span>, <span class="st0">"CharAttack"</span><span class="br0">)</span><span class="sy0">;</span>
  ...
<span class="br0">}</span></pre>

<p>
Respond to the key bindings by setting variables that track in which direction you will go. This allows us to steer the character forwards and to the left at the same time. <strong>Note that no actual walking happens here yet!</strong> We just track the input.
</p>
<pre class="code java">@Override
<span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> binding, <span class="kw4">boolean</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"CharLeft"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> left <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
      <span class="kw1">else</span> left <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"CharRight"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> right <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
      <span class="kw1">else</span> right <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"CharForward"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> up <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
      <span class="kw1">else</span> up <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"CharBackward"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> down <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
      <span class="kw1">else</span> down <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"CharJump"</span><span class="br0">)</span><span class="br0">)</span>
      character.<span class="me1">jump</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"CharAttack"</span><span class="br0">)</span><span class="br0">)</span>
    attack<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
The player can attack and walk at the same time. <code>Attack()</code> is a custom method that triggers an attack animation in the arms. Here you should also add custom code to play an effect and sound, and to determine whether the hit was successful.
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw4">void</span> attack<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    attackChannel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Dodge"</span>, 0.1f<span class="br0">)</span><span class="sy0">;</span>
    attackChannel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">DontLoop</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Finally, the update loop looks at the directional variables and moves the character accordingly. Since this is a special kinematic CharacterControl, we use the <code>setWalkDirection()</code> method. 
</p>

<p>
The variable <code>airTime</code> tracks how long the character is off the ground (e.g. when jumping or falling) and adjusts the walk and stand animations acccordingly.
</p>
<pre class="code java"><span class="kw1">private</span> Vector3f walkDirection <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// stop</span>
 
<span class="kw1">private</span> <span class="kw4">float</span> airTime <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
  Vector3f camDir <span class="sy0">=</span> cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  Vector3f camLeft <span class="sy0">=</span> cam.<span class="me1">getLeft</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  camDir.<span class="me1">y</span> <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
  camLeft.<span class="me1">y</span> <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
  camDir.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  camLeft.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  walkDirection.<span class="me1">set</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
 
  <span class="kw1">if</span> <span class="br0">(</span>left<span class="br0">)</span>  walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft<span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">if</span> <span class="br0">(</span>right<span class="br0">)</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">if</span> <span class="br0">(</span>up<span class="br0">)</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir<span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">if</span> <span class="br0">(</span>down<span class="br0">)</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
  <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>character.<span class="me1">onGround</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span> <span class="co1">// use !character.isOnGround() if the character is a BetterCharacterControl type.</span>
      airTime <span class="sy0">+=</span> tpf<span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
      airTime <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">if</span> <span class="br0">(</span>walkDirection.<span class="me1">lengthSquared</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">==</span> <span class="nu0">0</span><span class="br0">)</span> <span class="br0">{</span> <span class="co1">//Use lengthSquared() (No need for an extra sqrt())</span>
      <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span><span class="st0">"stand"</span>.<span class="me1">equals</span><span class="br0">(</span>animationChannel.<span class="me1">getAnimationName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        animationChannel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"stand"</span>, 1f<span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
      character.<span class="me1">setViewDirection</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">if</span> <span class="br0">(</span>airTime <span class="sy0">&gt;</span> .3f<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span><span class="st0">"stand"</span>.<span class="me1">equals</span><span class="br0">(</span>animationChannel.<span class="me1">getAnimationName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          animationChannel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"stand"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span><span class="st0">"Walk"</span>.<span class="me1">equals</span><span class="br0">(</span>animationChannel.<span class="me1">getAnimationName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        animationChannel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Walk"</span>, 0.7f<span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
 
  walkDirection.<span class="me1">multLocal</span><span class="br0">(</span>25f<span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>tpf<span class="br0">)</span><span class="sy0">;</span><span class="co1">// The use of the first multLocal here is to control the rate of movement multiplier for character walk speed. The second one is to make sure the character walks the same speed no matter what the frame rate is.</span>
  character.<span class="me1">setWalkDirection</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// THIS IS WHERE THE WALKING HAPPENS</span>
<span class="br0">}</span></pre>

<p>
This method resets the walk animation.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onAnimCycleDone<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>channel <span class="sy0">==</span> attackChannel<span class="br0">)</span> channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"stand"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> onAnimChange<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span> <span class="br0">}</span></pre>

</div>
<!-- EDIT13 SECTION "Handle Navigation" [12052-16709] -->
<h2 class="sectionedit14" id="see_also">See also</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/forum/topic/bettercharactercontrol-in-the-works/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/bettercharactercontrol-in-the-works/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/bettercharactercontrol-in-the-works/</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/animation.html" class="wikilink1" title="tag:animation" rel="tag">animation</a>,
	<a href="/tag/character.html" class="wikilink1" title="tag:character" rel="tag">character</a>,
	<a href="/tag/npc.html" class="wikilink1" title="tag:npc" rel="tag">NPC</a>,
	<a href="/tag/collision.html" class="wikilink1" title="tag:collision" rel="tag">collision</a>
</span></div>

</div>
<!-- EDIT14 SECTION "See also" [16710-] -->
