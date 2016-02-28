---
title: jMonkeyEngine 3 Tutorial (9) - Hello Collision
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_9_-_hello_collision">jMonkeyEngine 3 Tutorial (9) - Hello Collision</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_picking.html" class="wikilink1" title="jme3:beginner:hello_picking">Hello Picking</a>,
Next: <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">Hello Terrain</a>
</p>

<p>
This tutorial demonstrates how you load a scene model and give it solid walls and floors for a character to walk around.
You use a <code>RigidBodyControl</code> for the static collidable scene, and a <code>CharacterControl</code> for the mobile first-person character. You also learn how to set up the default first-person camera to work with physics-controlled navigation.
You can use the solution shown here for first-person shooters, mazes, and similar games.
</p>

<p>
<a href="/resources/jme3-beginner-beginner-scene.png" class="media" title="jme3:beginner:beginner-scene.png"><img src="/resources/jme3-beginner-beginner-scene.png" class="mediacenter" alt="" width="360" height="281" /></a>
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (9) - Hello Collision" [1-595] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
If you don't have it yet, <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" rel="nofollow">download the town.zip</a> sample scene.
</p>
<pre class="code">jMonkeyProjects$ ls -1 BasicGame
assets/
build.xml
town.zip
src/</pre>

<p>
Place town.zip in the root directory of your JME3 project. Here is the code:
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.plugins.ZipLocator</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.BulletAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.collision.shapes.CapsuleCollisionShape</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.collision.shapes.CollisionShape</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.CharacterControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.RigidBodyControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.util.CollisionShapeFactory</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.AmbientLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
 
<span class="co3">/**
 * Example 9 - How to make walls and floors solid.
 * This collision code uses Physics and a custom Action Listener.
 * @author normen, with edits by Zathras
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloCollision <span class="kw1">extends</span> SimpleApplication
        <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> <span class="br0">{</span>
 
  <span class="kw1">private</span> Spatial sceneModel<span class="sy0">;</span>
  <span class="kw1">private</span> BulletAppState bulletAppState<span class="sy0">;</span>
  <span class="kw1">private</span> RigidBodyControl landscape<span class="sy0">;</span>
  <span class="kw1">private</span> CharacterControl player<span class="sy0">;</span>
  <span class="kw1">private</span> Vector3f walkDirection <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw4">boolean</span> left <span class="sy0">=</span> <span class="kw2">false</span>, right <span class="sy0">=</span> <span class="kw2">false</span>, up <span class="sy0">=</span> <span class="kw2">false</span>, down <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
 
  <span class="co1">//Temporary vectors used on each frame.</span>
  <span class="co1">//They here to avoid instanciating new vectors on each frame</span>
  <span class="kw1">private</span> Vector3f camDir <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> Vector3f camLeft <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloCollision app <span class="sy0">=</span> <span class="kw1">new</span> HelloCollision<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** Set up Physics */</span>
    bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//bulletAppState.getPhysicsSpace().enableDebug(assetManager);</span>
 
    <span class="co1">// We re-use the flyby camera for rotation, while positioning is handled by physics</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span>0.7f, 0.8f, 1f, 1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span><span class="nu0">100</span><span class="br0">)</span><span class="sy0">;</span>
    setUpKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    setUpLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// We load the scene from the zip file and adjust its size.</span>
    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    sceneModel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    sceneModel.<span class="me1">setLocalScale</span><span class="br0">(</span>2f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// We set up collision detection for the scene by creating a</span>
    <span class="co1">// compound collision shape and a static RigidBodyControl with mass zero.</span>
    CollisionShape sceneShape <span class="sy0">=</span>
            CollisionShapeFactory.<span class="me1">createMeshShape</span><span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> sceneModel<span class="br0">)</span><span class="sy0">;</span>
    landscape <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>sceneShape, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    sceneModel.<span class="me1">addControl</span><span class="br0">(</span>landscape<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// We set up collision detection for the player by creating</span>
    <span class="co1">// a capsule collision shape and a CharacterControl.</span>
    <span class="co1">// The CharacterControl offers extra settings for</span>
    <span class="co1">// size, stepheight, jumping, falling, and gravity.</span>
    <span class="co1">// We also put the player in its starting position.</span>
    CapsuleCollisionShape capsuleShape <span class="sy0">=</span> <span class="kw1">new</span> CapsuleCollisionShape<span class="br0">(</span>1.5f, 6f, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    player <span class="sy0">=</span> <span class="kw1">new</span> CharacterControl<span class="br0">(</span>capsuleShape, 0.05f<span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setJumpSpeed</span><span class="br0">(</span><span class="nu0">20</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setFallSpeed</span><span class="br0">(</span><span class="nu0">30</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setGravity</span><span class="br0">(</span><span class="nu0">30</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setPhysicsLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">10</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// We attach the scene and the player to the rootnode and the physics space,</span>
    <span class="co1">// to make them appear in the game world.</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>sceneModel<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>landscape<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">private</span> <span class="kw4">void</span> setUpLight<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// We add light so we see the scene</span>
    AmbientLight al <span class="sy0">=</span> <span class="kw1">new</span> AmbientLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    al.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span>.<span class="me1">mult</span><span class="br0">(</span>1.3f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span>al<span class="br0">)</span><span class="sy0">;</span>
 
    DirectionalLight dl <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    dl.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
    dl.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>2.8f, <span class="sy0">-</span>2.8f, <span class="sy0">-</span>2.8f<span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span>dl<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** We over-write some navigational key mappings here, so we can
   * add physics-controlled walking and jumping: */</span>
  <span class="kw1">private</span> <span class="kw4">void</span> setUpKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Left"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_A</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Right"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_D</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Up"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_W</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Down"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_S</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Jump"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Left"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Right"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Up"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Down"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Jump"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** These are our custom actions triggered by key presses.
   * We do not walk yet, we just keep track of the direction the user pressed. */</span>
  <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> binding, <span class="kw4">boolean</span> isPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Left"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      left <span class="sy0">=</span> isPressed<span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Right"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      right<span class="sy0">=</span> isPressed<span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Up"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      up <span class="sy0">=</span> isPressed<span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Down"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      down <span class="sy0">=</span> isPressed<span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Jump"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>isPressed<span class="br0">)</span> <span class="br0">{</span> player.<span class="me1">jump</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
 
  <span class="co3">/**
   * This is the main event loop--walking happens here.
   * We check in which direction the player is walking by interpreting
   * the camera direction forward (camDir) and to the side (camLeft).
   * The setWalkDirection() command is what lets a physics-controlled player walk.
   * We also make sure here that the camera moves with player.
   */</span>
  @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        camDir.<span class="me1">set</span><span class="br0">(</span>cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>0.6f<span class="br0">)</span><span class="sy0">;</span>
        camLeft.<span class="me1">set</span><span class="br0">(</span>cam.<span class="me1">getLeft</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>0.4f<span class="br0">)</span><span class="sy0">;</span>
        walkDirection.<span class="me1">set</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>left<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>right<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>up<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>down<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        player.<span class="me1">setWalkDirection</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span>
        cam.<span class="me1">setLocation</span><span class="br0">(</span>player.<span class="me1">getPhysicsLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Run the sample. You should see a town square with houses and a monument. Use the WASD keys and the mouse to navigate around with a first-person perspective. Run forward and jump by pressing W and Space. Note how you step over the sidewalk, and up the steps to the monument. You can walk in the alleys between the houses, but the walls are solid. Don't walk over the edge of the world! <img src="/lib/images/smileys/icon_smile.gif" class="icon" alt=":-)" />
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [596-7341] -->
<h2 class="sectionedit3" id="understanding_the_code">Understanding the Code</h2>
<div class="level2">

<p>
Let's start with the class declaration:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HelloCollision <span class="kw1">extends</span> SimpleApplication
        <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> <span class="br0">{</span> ... <span class="br0">}</span></pre>

<p>
You already know that SimpleApplication is the base class for all jME3 games. You make this class implement the <code>ActionListener</code> interface because you want to customize the navigational inputs later.
</p>
<pre class="code java">  <span class="kw1">private</span> Spatial sceneModel<span class="sy0">;</span>
  <span class="kw1">private</span> BulletAppState bulletAppState<span class="sy0">;</span>
  <span class="kw1">private</span> RigidBodyControl landscape<span class="sy0">;</span>
  <span class="kw1">private</span> CharacterControl player<span class="sy0">;</span>
  <span class="kw1">private</span> Vector3f walkDirection <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw4">boolean</span> left <span class="sy0">=</span> <span class="kw2">false</span>, right <span class="sy0">=</span> <span class="kw2">false</span>, up <span class="sy0">=</span> <span class="kw2">false</span>, down <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
 
  <span class="co1">//Temporary vectors used on each frame.</span>
  <span class="co1">//They here to avoid instanciating new vectors on each frame</span>
  <span class="kw1">private</span> Vector3f camDir <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> Vector3f camLeft <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You initialize a few private fields:
</p>
<ul>
<li class="level1"><div class="li"> The BulletAppState gives this SimpleApplication access to physics features (such as collision detection) supplied by jME3's jBullet integration</div>
</li>
<li class="level1"><div class="li"> The Spatial sceneModel is for loading an OgreXML model of a town.</div>
</li>
<li class="level1"><div class="li"> You need a RigidBodyControl to make the town model solid.</div>
</li>
<li class="level1"><div class="li"> The (invisible) first-person player is represented by a CharacterControl object.</div>
</li>
<li class="level1"><div class="li"> The fields <code>walkDirection</code> and the four Booleans are used for physics-controlled navigation.</div>
</li>
<li class="level1"><div class="li"> camDir and camLeft are temporary vectors used later when computing the walkingDirection from the cam position and rotation</div>
</li>
</ul>

<p>
Let's have a look at all the details:
</p>

</div>
<!-- EDIT3 SECTION "Understanding the Code" [7342-8887] -->
<h2 class="sectionedit4" id="initializing_the_game">Initializing the Game</h2>
<div class="level2">

<p>
As usual, you initialize the game in the <code>simpleInitApp()</code> method.
</p>
<pre class="code java">    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span>0.7f,0.8f,1f,1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span><span class="nu0">100</span><span class="br0">)</span><span class="sy0">;</span>
    setUpKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    setUpLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>
<ol>
<li class="level1"><div class="li"> You set the background color to light blue, since this is a scene with a sky.</div>
</li>
<li class="level1"><div class="li"> You repurpose the default camera control “flyCam” as first-person camera and set its speed.</div>
</li>
<li class="level1"><div class="li"> The auxiliary method <code>setUpLights()</code> adds your light sources.</div>
</li>
<li class="level1"><div class="li"> The auxiliary method <code>setUpKeys()</code> configures input mappings–we will look at it later.</div>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "Initializing the Game" [8888-9484] -->
<h3 class="sectionedit5" id="the_physics-controlled_scene">The Physics-Controlled Scene</h3>
<div class="level3">

<p>
The first thing you do in every physics game is create a BulletAppState object. It gives you access to jME3's jBullet integration which handles physical forces and collisions.
</p>
<pre class="code java">    bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For the scene, you load the <code>sceneModel</code> from a zip file, and adjust the size.
</p>
<pre class="code java">    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    sceneModel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    sceneModel.<span class="me1">setLocalScale</span><span class="br0">(</span>2f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The file <code>town.zip</code> is included as a sample model in the JME3 sources – you can <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" rel="nofollow">download it here</a>. (Optionally, use any OgreXML scene of your own.) For this sample, place the zip file in the application's top level directory (that is, next to src/, assets/, build.xml).
</p>
<pre class="code java">    CollisionShape sceneShape <span class="sy0">=</span>
      CollisionShapeFactory.<span class="me1">createMeshShape</span><span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span> sceneModel<span class="br0">)</span><span class="sy0">;</span>
    landscape <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>sceneShape, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    sceneModel.<span class="me1">addControl</span><span class="br0">(</span>landscape<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>sceneModel<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To use collision detection, you add a RigidBodyControl to the <code>sceneModel</code> Spatial. The RigidBodyControl for a complex model takes two arguments: A Collision Shape, and the object's mass.
</p>
<ul>
<li class="level1"><div class="li"> JME3 offers a <code>CollisionShapeFactory</code> that precalculates a mesh-accurate collision shape for a Spatial. You choose to generate a <code>CompoundCollisionShape</code> (which has MeshCollisionShapes as its children) because this type of collision shape is optimal for immobile objects, such as terrain, houses, and whole shooter levels.</div>
</li>
<li class="level1"><div class="li"> You set the mass to zero since a scene is static and its mass is irrevelant.</div>
</li>
<li class="level1"><div class="li"> Add the control to the Spatial to give it physical properties. </div>
</li>
<li class="level1"><div class="li"> As always, attach the sceneModel to the rootNode to make it visible.</div>
</li>
</ul>

<p>
<strong>Tip:</strong> Remember to add a light source so you can see the scene.
</p>

</div>
<!-- EDIT5 SECTION "The Physics-Controlled Scene" [9485-11458] -->
<h3 class="sectionedit6" id="the_physics-controlled_player">The Physics-Controlled Player</h3>
<div class="level3">

<p>
A first-person player is typically invisible. When you use the default flyCam as first-person cam, it does not even test for collisons and runs through walls. This is because the flyCam control does not have any physical shape assigned. In this code sample, you represent the first-person player as an (invisible) physical shape. You use the WASD keys to steer this physical shape around, while the physics engine manages for you how it walks along solid walls and on solid floors and jumps over solid obstacles. Then you simply make the camera follow the walking shape's location – and you get the illusion of being a physical body in a solid environment seeing through the camera.
</p>

<p>
So let's set up collision detection for the first-person player.
</p>
<pre class="code java">    CapsuleCollisionShape capsuleShape <span class="sy0">=</span> <span class="kw1">new</span> CapsuleCollisionShape<span class="br0">(</span>1.5f, 6f, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Again, you create a CollisionShape: This time you choose a CapsuleCollisionShape, a cylinder with a rounded top and bottom. This shape is optimal for a person: It's tall and the roundness helps to get stuck less often on obstacles.
</p>
<ul>
<li class="level1"><div class="li"> Supply the CapsuleCollisionShape constructor with the desired radius and height of the bounding capsule to fit the shape of your character. In this example the character is 2*1.5f units wide, and 6f units tall.</div>
</li>
<li class="level1"><div class="li"> The final integer argument specifies the orientation of the cylinder: 1 is the Y-axis, which fits an upright person. For animals which are longer than high you would use 0 or 2 (depending on how it is rotated).</div>
</li>
</ul>
<pre class="code java">    player <span class="sy0">=</span> <span class="kw1">new</span> CharacterControl<span class="br0">(</span>capsuleShape, 0.05f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="notetip">“Does that CollisionShape make me look fat?” If you ever get confusing physics behaviour, remember to have a look at the collision shapes. Add the following line after the bulletAppState initialization to make the shapes visible: 

<pre class="code java">bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">enableDebug</span><span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span></pre>

<p>

</p></div>


<p>
Now you use the CollisionShape to create a <code>CharacterControl</code> that represents the first-person player. The last argument of the CharacterControl constructor (here <code>.05f</code>) is the size of a step that the character should be able to surmount.
</p>
<pre class="code java">    player.<span class="me1">setJumpSpeed</span><span class="br0">(</span><span class="nu0">20</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setFallSpeed</span><span class="br0">(</span><span class="nu0">30</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setGravity</span><span class="br0">(</span><span class="nu0">30</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Apart from step height and character size, the <code>CharacterControl</code> lets you configure jumping, falling, and gravity speeds. Adjust the values to fit your game situation.
</p>
<pre class="code java">    player.<span class="me1">setPhysicsLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">10</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Finally we put the player in its starting position and update its state – remember to use <code>setPhysicsLocation()</code> instead of <code>setLocalTranslation()</code> now, since you are dealing with a physical object. 
</p>

</div>
<!-- EDIT6 SECTION "The Physics-Controlled Player" [11459-14223] -->
<h3 class="sectionedit7" id="physicsspace">PhysicsSpace</h3>
<div class="level3">

<p>
Remember, in physical games, you must register all solid objects (usually the characters and the scene) to the PhysicsSpace!
</p>
<pre class="code java">    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>landscape<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The invisible body of the character just sits there on the physical floor. It cannot walk yet – you will deal with that next.
</p>

</div>
<!-- EDIT7 SECTION "PhysicsSpace" [14224-14625] -->
<h2 class="sectionedit8" id="navigation">Navigation</h2>
<div class="level2">

<p>
The default camera controller <code>cam</code> is a third-person camera. JME3 also offers a first-person controller, <code>flyCam</code>, which we use here to handle camera rotation. The <code>flyCam</code> control moves the camera using <code>setLocation()</code>.
</p>

<p>
However, you must redefine how walking (camera movement) is handled for physics-controlled objects: When you navigate a non-physical node (e.g. the default flyCam), you simply specify the <em>target location</em>. There are no tests that prevent the flyCam from getting stuck in a wall! When you move a PhysicsControl, you want to specify a <em>walk direction</em> instead. Then the PhysicsSpace can calculate for you how far the character can actually move in the desired direction – or whether an obstacle prevents it from going any further.
</p>

<p>
In short, you must re-define the flyCam's navigational key mappings to use <code>setWalkDirection()</code> instead of <code>setLocalTranslation()</code>. Here are the steps:
</p>

</div>
<!-- EDIT8 SECTION "Navigation" [14626-15573] -->
<h3 class="sectionedit9" id="inputmanager">1. inputManager</h3>
<div class="level3">

<p>
In the <code>simpleInitApp()</code> method, you re-configure the familiar WASD inputs for walking, and Space for jumping.
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw4">void</span> setUpKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Left"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_A</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Right"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_D</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Up"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_W</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Down"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_S</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Jump"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Left"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Right"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Up"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Down"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Jump"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
You can move this block of code into an auxiliary method <code>setupKeys()</code> and call this method from <code>simpleInitApp()</code>– to keep the code more readable.
</p>

</div>
<!-- EDIT9 SECTION "1. inputManager" [15574-16484] -->
<h3 class="sectionedit10" id="onaction">2. onAction()</h3>
<div class="level3">

<p>
Remember that this class implements the <code>ActionListener</code> interface, so you can customize the flyCam inputs. The <code>ActionListener</code> interface requires you to implement the <code>onAction()</code> method: You re-define the actions triggered by navigation key presses to work with physics.
</p>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> binding, <span class="kw4">boolean</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Left"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span> left <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span> <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span> left <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span> <span class="br0">}</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Right"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span> right <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span> <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span> right <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span> <span class="br0">}</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Up"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span> up <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span> <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span> up <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span> <span class="br0">}</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Down"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span> down <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span> <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span> down <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span> <span class="br0">}</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Jump"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      player.<span class="me1">jump</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span></pre>

<p>
The only movement that you do not have to implement yourself is the jumping action. The call <code>player.jump()</code> is a special method that handles a correct jumping motion for your <code>PhysicsCharacterNode</code>.
</p>

<p>
For all other directions: Every time the user presses one of the WASD keys, you <em>keep track</em> of the direction the user wants to go, by storing this info in four directional Booleans. No actual walking happens here yet. The update loop is what acts out the directional info stored in the booleans, and makes the player move, as shown in the next code snippet:
</p>

</div>
<!-- EDIT10 SECTION "2. onAction()" [16485-17898] -->
<h3 class="sectionedit11" id="setwalkdirection">3. setWalkDirection()</h3>
<div class="level3">

<p>
Previously in the <code>onAction()</code> method, you have collected the info in which direction the user wants to go in terms of “forward” or “left”. In the update loop, you repeatedly poll the current rotation of the camera. You calculate the actual vectors to which “forward” or “left” corresponds in the coordinate system.
</p>

<p>
This last and most important code snippet goes into the <code>simpleUpdate()</code> method.
</p>
<pre class="code java"> <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        camDir.<span class="me1">set</span><span class="br0">(</span>cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>0.6f<span class="br0">)</span><span class="sy0">;</span>
        camLeft.<span class="me1">set</span><span class="br0">(</span>cam.<span class="me1">getLeft</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>0.4f<span class="br0">)</span><span class="sy0">;</span>
        walkDirection.<span class="me1">set</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>left<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>right<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>up<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>down<span class="br0">)</span> <span class="br0">{</span>
            walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        player.<span class="me1">setWalkDirection</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span>
        cam.<span class="me1">setLocation</span><span class="br0">(</span>player.<span class="me1">getPhysicsLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span></pre>

<p>
This is how the walking is triggered:
</p>
<ol>
<li class="level1"><div class="li"> Initialize the vector <code>walkDirection</code> to zero. This is where you want to store the calculated walk direction.</div>
</li>
<li class="level2"><div class="li"> Add to <code>walkDirection</code> the recent motion vectors that you polled from the camera. This way it is posible for a character to move forward and to the left simultaneously, for example! </div>
</li>
<li class="level2"><div class="li"> This one last line does the “walking magic”: <pre class="code java">player.<span class="me1">setWalkDirection</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Always use <code>setWalkDirection()</code> to make a physics-controlled object move continuously, and the physics engine handles collision detection for you.
</p>
</div>
</li>
<li class="level2"><div class="li"> Make the first-person camera object follow along with the physics-controlled player:<pre class="code java">cam.<span class="me1">setLocation</span><span class="br0">(</span>player.<span class="me1">getPhysicsLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
<strong>Important:</strong> Again, do not use <code>setLocalTranslation()</code> to walk the player around. You will get it stuck by overlapping with another physical object. You can put the player in a start position with <code>setPhysicalLocation()</code> if you make sure to place it a bit above the floor and away from obstacles.
</p>

</div>
<!-- EDIT11 SECTION "3. setWalkDirection()" [17899-20017] -->
<h2 class="sectionedit12" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned how to load a “solid” physical scene model and walk around in it with a first-person perspective.
You learned to speed up the physics calculations by using the CollisionShapeFactory to create efficient CollisionShapes for complex Geometries. You know how to add PhysicsControls to your collidable geometries and you register them to the PhysicsSpace. You also learned to use <code>player.setWalkDirection(walkDirection)</code> to move collision-aware characters around, and not <code>setLocalTranslation()</code>.
</p>

<p>
Terrains are another type of scene in which you will want to walk around. Let's proceed with learning <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">how to generate terrains</a> now. 
</p>
<hr />

<p>
Related info:
</p>
<ul>
<li class="level1"><div class="li"> How to load models and scenes: <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">Hello Asset</a>, <a href="/sdk/scene_explorer.html" class="wikilink1" title="sdk:scene_explorer">Scene Explorer</a>, <a href="/sdk/scene_composer.html" class="wikilink1" title="sdk:scene_composer">Scene Composer</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/terrain_collision.html" class="wikilink1" title="jme3:advanced:terrain_collision">Terrain Collision</a></div>
</li>
<li class="level1"><div class="li"> To learn more about complex physics scenes, where several mobile physical objects bump into each other, read <a href="/jme3/beginner/hello_physics.html" class="wikilink1" title="jme3:beginner:hello_physics">Hello Physics</a>.</div>
</li>
<li class="level1"><div class="li"> FYI, there are simpler collision detection solutions without physics, too. Have a look at <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/collision/TestTriangleCollision.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/collision/TestTriangleCollision.java" rel="nofollow">jme3test.collision.TestTriangleCollision.java</a>.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/collision.html" class="wikilink1" title="tag:collision" rel="tag">collision</a>,
	<a href="/tag/control.html" class="wikilink1" title="tag:control" rel="tag">control</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/model.html" class="wikilink1" title="tag:model" rel="tag">model</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>
</span></div>

</div>
<!-- EDIT12 SECTION "Conclusion" [20018-] -->
