---
title: jMonkeyEngine 3 Tutorial (13) - Hello Physics
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_13_-_hello_physics">jMonkeyEngine 3 Tutorial (13) - Hello Physics</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_effects.html" class="wikilink1" title="jme3:beginner:hello_effects">Hello Effects</a>,
Next: <a href="/jme3.html" class="wikilink1" title="jme3">JME 3 documentation</a>
</p>

<p>
Do you remember the <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a> tutorial where you made the model of a town solid and walked through it in a first-person perspective? Then you may remember that, for the simulation of physical forces, jME3 integrates the <a href="http://jbullet.advel.cz/" class="urlextern" title="http://jbullet.advel.cz/" rel="nofollow">jBullet</a> library. 
</p>

<p>
Apart from making models “solid”, the most common use cases for physics in 3D games are:
</p>
<ul>
<li class="level1"><div class="li"> Driving vehicles with suspensions, tyre friction, ramp jumping, drifting – Example: car racers</div>
</li>
<li class="level1"><div class="li"> Rolling and bouncing balls – Example: pong, pool billiard, bowling</div>
</li>
<li class="level1"><div class="li"> Sliding and falling boxes – Example: Breakout, Arkanoid</div>
</li>
<li class="level1"><div class="li"> Exposing objects to forces and gravity – Example: spaceships or zero-g flight</div>
</li>
<li class="level1"><div class="li"> Animating ragdolls – Example: “realistic” character simulations</div>
</li>
<li class="level1"><div class="li"> Swinging pendulums, rope bridges, flexible chains, and much more…</div>
</li>
</ul>

<p>
All these physical properties can be simulated in JME3. Let's have a look at a simulation of physical forces in this example where you shoot cannon balls at a brick wall.
</p>

<p>
<a href="/resources/jme3-beginner-beginner-physics.png" class="media" title="jme3:beginner:beginner-physics.png"><img src="/resources/jme3-beginner-beginner-physics.png" class="mediacenter" alt="" width="360" height="291" /></a>
</p>

<p>
</p><p></p><div class="notetip">To use the example assets in a new jMonkeyEngine SDK project, right-click your project, select “Properties”, go to “Libraries”, press “Add Library” and add the “jme3-test-data” library.
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (13) - Hello Physics" [1-1378] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
Thanks to double1984 for contributing this fun sample!
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.TextureKey</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.BulletAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.RigidBodyControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapText</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.MouseInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.MouseButtonTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector2f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Sphere</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Sphere.TextureMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture.WrapMode</span><span class="sy0">;</span>
 
<span class="co3">/**
 * Example 12 - how to give objects physical properties so they bounce and fall.
 * @author base code by double1984, updated by zathras
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloPhysics <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> args<span class="br0">[</span><span class="br0">]</span><span class="br0">)</span> <span class="br0">{</span>
    HelloPhysics app <span class="sy0">=</span> <span class="kw1">new</span> HelloPhysics<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** Prepare the Physics Application State (jBullet) */</span>
  <span class="kw1">private</span> BulletAppState bulletAppState<span class="sy0">;</span>
 
  <span class="co3">/** Prepare Materials */</span>
  Material wall_mat<span class="sy0">;</span>
  Material stone_mat<span class="sy0">;</span>
  Material floor_mat<span class="sy0">;</span>
 
  <span class="co3">/** Prepare geometries and physical nodes for bricks and cannon balls. */</span>
  <span class="kw1">private</span> RigidBodyControl    brick_phy<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a>    box<span class="sy0">;</span>
  <span class="kw1">private</span> RigidBodyControl    ball_phy<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> Sphere sphere<span class="sy0">;</span>
  <span class="kw1">private</span> RigidBodyControl    floor_phy<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a>    floor<span class="sy0">;</span>
 
  <span class="co3">/** dimensions used for bricks and wall */</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> brickLength <span class="sy0">=</span> 0.48f<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> brickWidth  <span class="sy0">=</span> 0.24f<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> brickHeight <span class="sy0">=</span> 0.12f<span class="sy0">;</span>
 
  <span class="kw1">static</span> <span class="br0">{</span>
    <span class="co3">/** Initialize the cannon ball geometry */</span>
    sphere <span class="sy0">=</span> <span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">32</span>, <span class="nu0">32</span>, 0.4f, <span class="kw2">true</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    sphere.<span class="me1">setTextureMode</span><span class="br0">(</span>TextureMode.<span class="me1">Projected</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Initialize the brick geometry */</span>
    box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>brickLength, brickHeight, brickWidth<span class="br0">)</span><span class="sy0">;</span>
    box.<span class="me1">scaleTextureCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span>1f, .5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Initialize the floor geometry */</span>
    floor <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>10f, 0.1f, 5f<span class="br0">)</span><span class="sy0">;</span>
    floor.<span class="me1">scaleTextureCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">6</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** Set up Physics Game */</span>
    bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//bulletAppState.getPhysicsSpace().enableDebug(assetManager);</span>
 
    <span class="co3">/** Configure cam to look at scene */</span>
    cam.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, 4f, 6f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    cam.<span class="me1">lookAt</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">2</span>, <span class="nu0">2</span>, <span class="nu0">0</span><span class="br0">)</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Add InputManager action: Left click triggers shooting. */</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"shoot"</span>, 
            <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"shoot"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Initialize the scene, materials, and physics space */</span>
    initMaterials<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    initWall<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    initFloor<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    initCrossHairs<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/**
   * Every time the shoot action is triggered, a new cannon ball is produced.
   * The ball is set up to fly from the camera position in the camera direction.
   */</span>
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"shoot"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        makeCannonBall<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span>
 
  <span class="co3">/** Initialize the materials used in this scene. */</span>
  <span class="kw1">public</span> <span class="kw4">void</span> initMaterials<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    wall_mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    TextureKey key <span class="sy0">=</span> <span class="kw1">new</span> TextureKey<span class="br0">(</span><span class="st0">"Textures/Terrain/BrickWall/BrickWall.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    key.<span class="me1">setGenerateMips</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    Texture tex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>key<span class="br0">)</span><span class="sy0">;</span>
    wall_mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, tex<span class="br0">)</span><span class="sy0">;</span>
 
    stone_mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    TextureKey key2 <span class="sy0">=</span> <span class="kw1">new</span> TextureKey<span class="br0">(</span><span class="st0">"Textures/Terrain/Rock/Rock.PNG"</span><span class="br0">)</span><span class="sy0">;</span>
    key2.<span class="me1">setGenerateMips</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    Texture tex2 <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>key2<span class="br0">)</span><span class="sy0">;</span>
    stone_mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, tex2<span class="br0">)</span><span class="sy0">;</span>
 
    floor_mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    TextureKey key3 <span class="sy0">=</span> <span class="kw1">new</span> TextureKey<span class="br0">(</span><span class="st0">"Textures/Terrain/Pond/Pond.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    key3.<span class="me1">setGenerateMips</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    Texture tex3 <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>key3<span class="br0">)</span><span class="sy0">;</span>
    tex3.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    floor_mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, tex3<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** Make a solid floor and add it to the scene. */</span>
  <span class="kw1">public</span> <span class="kw4">void</span> initFloor<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    Geometry floor_geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Floor"</span>, floor<span class="br0">)</span><span class="sy0">;</span>
    floor_geo.<span class="me1">setMaterial</span><span class="br0">(</span>floor_mat<span class="br0">)</span><span class="sy0">;</span>
    floor_geo.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>0.1f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">rootNode</span>.<span class="me1">attachChild</span><span class="br0">(</span>floor_geo<span class="br0">)</span><span class="sy0">;</span>
    <span class="coMULTI">/* Make the floor physical with mass 0.0f! */</span>
    floor_phy <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>0.0f<span class="br0">)</span><span class="sy0">;</span>
    floor_geo.<span class="me1">addControl</span><span class="br0">(</span>floor_phy<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>floor_phy<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** This loop builds a wall out of individual bricks. */</span>
  <span class="kw1">public</span> <span class="kw4">void</span> initWall<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw4">float</span> startpt <span class="sy0">=</span> brickLength <span class="sy0">/</span> <span class="nu0">4</span><span class="sy0">;</span>
    <span class="kw4">float</span> height <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
    <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> j <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> j <span class="sy0">&lt;</span> <span class="nu0">15</span><span class="sy0">;</span> j<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> <span class="nu0">6</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
        Vector3f vt <span class="sy0">=</span>
         <span class="kw1">new</span> Vector3f<span class="br0">(</span>i <span class="sy0">*</span> brickLength <span class="sy0">*</span> <span class="nu0">2</span> <span class="sy0">+</span> startpt, brickHeight <span class="sy0">+</span> height, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        makeBrick<span class="br0">(</span>vt<span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
      startpt <span class="sy0">=</span> <span class="sy0">-</span>startpt<span class="sy0">;</span>
      height <span class="sy0">+=</span> <span class="nu0">2</span> <span class="sy0">*</span> brickHeight<span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
 
  <span class="co3">/** This method creates one individual physical brick. */</span>
  <span class="kw1">public</span> <span class="kw4">void</span> makeBrick<span class="br0">(</span>Vector3f loc<span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** Create a brick geometry and attach to scene graph. */</span>
    Geometry brick_geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"brick"</span>, box<span class="br0">)</span><span class="sy0">;</span>
    brick_geo.<span class="me1">setMaterial</span><span class="br0">(</span>wall_mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>brick_geo<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Position the brick geometry  */</span>
    brick_geo.<span class="me1">setLocalTranslation</span><span class="br0">(</span>loc<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Make brick physical with a mass &gt; 0.0f. */</span>
    brick_phy <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>2f<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Add physical brick to physics space. */</span>
    brick_geo.<span class="me1">addControl</span><span class="br0">(</span>brick_phy<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>brick_phy<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** This method creates one individual physical cannon ball.
   * By defaul, the ball is accelerated and flies
   * from the camera position in the camera direction.*/</span>
   <span class="kw1">public</span> <span class="kw4">void</span> makeCannonBall<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** Create a cannon ball geometry and attach to scene graph. */</span>
    Geometry ball_geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"cannon ball"</span>, sphere<span class="br0">)</span><span class="sy0">;</span>
    ball_geo.<span class="me1">setMaterial</span><span class="br0">(</span>stone_mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>ball_geo<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Position the cannon ball  */</span>
    ball_geo.<span class="me1">setLocalTranslation</span><span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Make the ball physcial with a mass &gt; 0.0f */</span>
    ball_phy <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Add physical ball to physics space. */</span>
    ball_geo.<span class="me1">addControl</span><span class="br0">(</span>ball_phy<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>ball_phy<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Accelerate the physcial ball to shoot it. */</span>
    ball_phy.<span class="me1">setLinearVelocity</span><span class="br0">(</span>cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">mult</span><span class="br0">(</span><span class="nu0">25</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** A plus sign used as crosshairs to help the player with aiming.*/</span>
  <span class="kw1">protected</span> <span class="kw4">void</span> initCrossHairs<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    guiNode.<span class="me1">detachAllChildren</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
    BitmapText ch <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    ch.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">*</span> <span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    ch.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"+"</span><span class="br0">)</span><span class="sy0">;</span>        <span class="co1">// fake crosshairs :)</span>
    ch.<span class="me1">setLocalTranslation</span><span class="br0">(</span> <span class="co1">// center</span>
      settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span> <span class="sy0">-</span> guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">3</span> <span class="sy0">*</span> <span class="nu0">2</span>,
      settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span> <span class="sy0">+</span> ch.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">attachChild</span><span class="br0">(</span>ch<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
You should see a brick wall. Click to shoot cannon balls. Watch the bricks fall and bounce off one another!
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [1379-8734] -->
<h2 class="sectionedit3" id="a_basic_physics_application">A Basic Physics Application</h2>
<div class="level2">

<p>
In the previous tutorials, you used static Geometries (boxes, spheres, and models) that you placed in the scene. Depending on their translation, Geometries can “float in mid-air” and even overlap – they are not affected by “gravity” and have no physical mass. This tutorial shows how to add physical properties to Geometries.
</p>

<p>
As always, start with a standard com.jme3.app.SimpleApplication. To activate physics, create a com.jme3.bullet.BulletAppState, and and attach it to the SimpleApplication's AppState manager.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HelloPhysics <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
  <span class="kw1">private</span> BulletAppState bulletAppState<span class="sy0">;</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span>
    ...
  <span class="br0">}</span>
  ...
<span class="br0">}</span></pre>

<p>
The BulletAppState gives the game access to a PhysicsSpace. The PhysicsSpace lets you use com.jme3.bullet.control.PhysicsControls that add physical properties to Nodes.
</p>

</div>
<!-- EDIT3 SECTION "A Basic Physics Application" [8735-9718] -->
<h2 class="sectionedit4" id="creating_bricks_and_cannon_balls">Creating Bricks and Cannon Balls</h2>
<div class="level2">

</div>
<!-- EDIT4 SECTION "Creating Bricks and Cannon Balls" [9719-9764] -->
<h3 class="sectionedit5" id="geometries">Geometries</h3>
<div class="level3">

<p>
In this “shoot at the wall” example, you use Geometries such as cannon balls and bricks. Geometries contain meshes, such as Shapes. Let's create and initialize some Shapes: Boxes and Spheres.
</p>
<pre class="code java">  <span class="co3">/** Prepare geometries and physical nodes for bricks and cannon balls. */</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a>    box<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> Sphere sphere<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a>    floor<span class="sy0">;</span>
  <span class="co3">/** dimensions used for bricks and wall */</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> brickLength <span class="sy0">=</span> 0.48f<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> brickWidth  <span class="sy0">=</span> 0.24f<span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> <span class="kw4">float</span> brickHeight <span class="sy0">=</span> 0.12f<span class="sy0">;</span>
  <span class="kw1">static</span> <span class="br0">{</span>
    <span class="co3">/** Initialize the cannon ball geometry */</span>
    sphere <span class="sy0">=</span> <span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">32</span>, <span class="nu0">32</span>, 0.4f, <span class="kw2">true</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    sphere.<span class="me1">setTextureMode</span><span class="br0">(</span>TextureMode.<span class="me1">Projected</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Initialize the brick geometry */</span>
    box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>brickLength, brickHeight, brickWidth<span class="br0">)</span><span class="sy0">;</span>
    box.<span class="me1">scaleTextureCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span>1f, .5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Initialize the floor geometry */</span>
    floor <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>10f, 0.1f, 5f<span class="br0">)</span><span class="sy0">;</span>
    floor.<span class="me1">scaleTextureCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">6</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "Geometries" [9765-10830] -->
<h3 class="sectionedit6" id="rigidbodycontrolbrick">RigidBodyControl: Brick</h3>
<div class="level3">

<p>
We want to create brick Geometries from those boxes. For each Geometry with physical properties, you create a RigidBodyControl.
</p>
<pre class="code java">  <span class="kw1">private</span> RigidBodyControl brick_phy<span class="sy0">;</span></pre>

<p>
The custom <code>makeBrick(loc)</code> methods creates individual bricks at the location <code>loc</code>. A brick has the following properties:
</p>
<ul>
<li class="level1"><div class="li"> It has a visible Geometry <code>brick_geo</code> (Box Shape Geometry).</div>
</li>
<li class="level1"><div class="li"> It has physical properties <code>brick_phy</code> (RigidBodyControl)</div>
</li>
</ul>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> makeBrick<span class="br0">(</span>Vector3f loc<span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** Create a brick geometry and attach to scene graph. */</span>
    Geometry brick_geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"brick"</span>, box<span class="br0">)</span><span class="sy0">;</span>
    brick_geo.<span class="me1">setMaterial</span><span class="br0">(</span>wall_mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>brick_geo<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Position the brick geometry  */</span>
    brick_geo.<span class="me1">setLocalTranslation</span><span class="br0">(</span>loc<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Make brick physical with a mass &gt; 0.0f. */</span>
    brick_phy <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>2f<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Add physical brick to physics space. */</span>
    brick_geo.<span class="me1">addControl</span><span class="br0">(</span>brick_phy<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>brick_phy<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

<p>
This code sample does the following:
</p>
<ol>
<li class="level1"><div class="li"> You create a brick Geometry brick_geo. A Geometry describes the shape and look of an object.</div>
<ul>
<li class="level2"><div class="li"> brick_geo has a box shape</div>
</li>
<li class="level2"><div class="li"> brick_geo has a brick-colored material.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> You attach brick_geo to the rootNode </div>
</li>
<li class="level1"><div class="li"> You position brick_geo at <code>loc</code>. </div>
</li>
<li class="level1"><div class="li"> You create a RigidBodyControl brick_phy for brick_geo.</div>
<ul>
<li class="level2"><div class="li"> brick_phy has a mass of 2f.</div>
</li>
<li class="level2"><div class="li"> You add brick_phy to brick_geo.</div>
</li>
<li class="level2"><div class="li"> You register brick_phy to the PhysicsSpace.</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT6 SECTION "RigidBodyControl: Brick" [10831-12353] -->
<h3 class="sectionedit7" id="rigidbodycontrolcannonball">RigidBodyControl: Cannonball</h3>
<div class="level3">

<p>
You notice that the cannon ball is created in the same way, using the custom <code>makeCannonBall()</code> method. The cannon ball has the following properties:
</p>
<ul>
<li class="level1"><div class="li"> It has a visible Geometry <code>ball_geo</code> (Sphere Shape Geometry)</div>
</li>
<li class="level1"><div class="li"> It has physical properties <code>ball_phy</code> (RigidBodyControl)</div>
</li>
</ul>
<pre class="code java">    <span class="co3">/** Create a cannon ball geometry and attach to scene graph. */</span>
    Geometry ball_geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"cannon ball"</span>, sphere<span class="br0">)</span><span class="sy0">;</span>
    ball_geo.<span class="me1">setMaterial</span><span class="br0">(</span>stone_mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>ball_geo<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Position the cannon ball  */</span>
    ball_geo.<span class="me1">setLocalTranslation</span><span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Make the ball physcial with a mass &gt; 0.0f */</span>
    ball_phy <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Add physical ball to physics space. */</span>
    ball_geo.<span class="me1">addControl</span><span class="br0">(</span>ball_phy<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>ball_phy<span class="br0">)</span><span class="sy0">;</span>
    <span class="co3">/** Accelerate the physcial ball to shoot it. */</span>
    ball_phy.<span class="me1">setLinearVelocity</span><span class="br0">(</span>cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">mult</span><span class="br0">(</span><span class="nu0">25</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 </pre>

<p>
This code sample does the following:
</p>
<ol>
<li class="level1"><div class="li"> You create a ball Geometry ball_geo. A Geometry describes the shape and look of an object.</div>
<ul>
<li class="level2"><div class="li"> ball_geo has a sphere shape</div>
</li>
<li class="level2"><div class="li"> ball_geo has a stone-colored material.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> You attach ball_geo to the rootNode </div>
</li>
<li class="level1"><div class="li"> You position ball_geo at the camera location. </div>
</li>
<li class="level1"><div class="li"> You create a RigidBodyControl ball_phy for ball_geo.</div>
<ul>
<li class="level2"><div class="li"> ball_phy has a mass of 1f.</div>
</li>
<li class="level2"><div class="li"> You add ball_phy to ball_geo.</div>
</li>
<li class="level2"><div class="li"> You register ball_phy to the PhysicsSpace.</div>
</li>
</ul>
</li>
</ol>

<p>
Since you are shooting cannon balls, the last line accelerates the ball in the direction the camera is looking, with a speed of 25f.
</p>

</div>
<!-- EDIT7 SECTION "RigidBodyControl: Cannonball" [12354-13950] -->
<h3 class="sectionedit8" id="rigidbodycontrolfloor">RigidBodyControl: Floor</h3>
<div class="level3">

<p>
The (static) floor has one important difference compared to the (dynamic) bricks and cannonballs: <strong>Static objects have a mass of zero.</strong>
As before, you write a custom <code>initFloor()</code> method that creates a flat box with a rock texture that you use as floor. The floor has the following properties:
</p>
<ul>
<li class="level1"><div class="li"> It has a visible Geometry <code>floor_geo</code> (Box Shape Geometry)</div>
</li>
<li class="level1"><div class="li"> It has physical properties <code>floor_phy</code> (RigidBodyControl)</div>
</li>
</ul>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> initFloor<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    Geometry floor_geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Floor"</span>, floor<span class="br0">)</span><span class="sy0">;</span>
    floor_geo.<span class="me1">setMaterial</span><span class="br0">(</span>floor_mat<span class="br0">)</span><span class="sy0">;</span>
    floor_geo.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>0.1f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">rootNode</span>.<span class="me1">attachChild</span><span class="br0">(</span>floor_geo<span class="br0">)</span><span class="sy0">;</span>
    <span class="coMULTI">/* Make the floor physical with mass 0.0f! */</span>
    floor_phy <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span>0.0f<span class="br0">)</span><span class="sy0">;</span>
    floor_geo.<span class="me1">addControl</span><span class="br0">(</span>floor_phy<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>floor_phy<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

<p>
This code sample does the following:
</p>
<ol>
<li class="level1"><div class="li"> You create a floor Geometry floor_geo. A Geometry describes the shape and look of an object.</div>
<ul>
<li class="level2"><div class="li"> floor_geo has a box shape</div>
</li>
<li class="level2"><div class="li"> floor_geo has a pebble-colored material.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> You attach floor_geo to the rootNode </div>
</li>
<li class="level1"><div class="li"> You position floor_geo a bit below y=0 (to prevent overlap with other PhysicControl'ed Spatials). </div>
</li>
<li class="level1"><div class="li"> You create a RigidBodyControl floor_phy for floor_geo.</div>
<ul>
<li class="level2"><div class="li"> floor_phy has a mass of 0f <img src="/lib/images/smileys/icon_exclaim.gif" class="icon" alt=":!:" /></div>
</li>
<li class="level2"><div class="li"> You add floor_phy to floor_geo.</div>
</li>
<li class="level2"><div class="li"> You register floor_phy to the PhysicsSpace.</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT8 SECTION "RigidBodyControl: Floor" [13951-15375] -->
<h2 class="sectionedit9" id="creating_the_scene">Creating the Scene</h2>
<div class="level2">

<p>
Let's have a quick look at the custom helper methods:
</p>
<ul>
<li class="level1"><div class="li"> <code>initMaterial()</code> – This method initializes all the materials we use in this demo.</div>
</li>
<li class="level1"><div class="li"> <code>initWall()</code> – A double loop that generates a wall by positioning brick objects: 15 rows high with 6 bricks per row. It's important to space the physical bricks so they do not overlap.</div>
</li>
<li class="level1"><div class="li"> <code>initCrossHairs()</code> – This method simply displays a plus sign that you use as crosshairs for aiming. Note that screen elements such as crosshairs are attached to the <code>guiNode</code>, not the <code>rootNode</code>!</div>
</li>
<li class="level1"><div class="li"> <code>initInputs()</code> – This method sets up the click-to-shoot action.</div>
</li>
</ul>

<p>
These methods are each called once from the <code>simpleInitApp()</code> method at the start of the game. As you see, you can write any number of custom methods to set up your game's scene. 
</p>

</div>
<!-- EDIT9 SECTION "Creating the Scene" [15376-16204] -->
<h2 class="sectionedit10" id="the_cannon_ball_shooting_action">The Cannon Ball Shooting Action</h2>
<div class="level2">

<p>
In the <code>initInputs()</code> method, you add an input mapping that triggers a shoot action when the left mouse button is pressed.
</p>
<pre class="code java">  <span class="kw1">private</span> <span class="kw4">void</span> initInputs<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"shoot"</span>, 
            <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"shoot"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

<p>
You define the actual action of shooting a new cannon ball as follows:
</p>
<pre class="code java">    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"shoot"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
                makeCannonBall<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span><span class="sy0">;</span></pre>

<p>
In the moment the cannonball appears in the scene, it flies off with the velocity (and in the direction) that you specified using <code>setLinearVelocity()</code> inside <code>makeCannonBall()</code>. The newly created cannon ball flies off, hits the wall, and exerts a <em>physical force</em> that impacts individual bricks.
</p>

</div>
<!-- EDIT10 SECTION "The Cannon Ball Shooting Action" [16205-17245] -->
<h2 class="sectionedit11" id="moving_a_physical_spatial">Moving a Physical Spatial</h2>
<div class="level2">

<p>
The location of the dynamic Spatial is controlled by its RigidBodyControl. Move the RigidBodyControl to move the Spatial. If it's a dynamic PhysicsControl, you can use setLinearVelocity() and apply forces and torques to it. Other RigidBodyControl'led objects can push the dynamic Spatial around (like pool/billiard balls).
</p>

<p>
You can make Spatials that are not dynamic: Switch the RigidBodyControl to setKinematic(true) to have it move along with its Spatial.
</p>
<ul>
<li class="level1"><div class="li"> A kinematic is unaffected by forces or gravity, which means it can float in mid-air and cannot be pushed away by dynamic “cannon balls” etc.</div>
</li>
<li class="level1"><div class="li"> A kinematic RigidBody has a mass.</div>
</li>
<li class="level1"><div class="li"> A kinematic can be moved and can exert forces on dynamic RigidBodys. This means you can use a kinematic node as a billiard cue or a remote-controlled battering ram.</div>
</li>
</ul>

<p>
Learn more about static versus kinematic versus dynamic in the <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">advanced physics doc</a>.
</p>

</div>
<!-- EDIT11 SECTION "Moving a Physical Spatial" [17246-18209] -->
<h2 class="sectionedit12" id="excercises">Excercises</h2>
<div class="level2">

</div>
<!-- EDIT12 SECTION "Excercises" [18210-18233] -->
<h3 class="sectionedit13" id="exercise_1debug_shapes">Exercise 1: Debug Shapes</h3>
<div class="level3">

<p>
Add the following line after the bulletAppState initialization. 
</p>
<pre class="code java">bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">enableDebug</span><span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now you see the collisionShapes of the bricks and spheres, and the floor highlighted. 
</p>

</div>
<!-- EDIT13 SECTION "Exercise 1: Debug Shapes" [18234-18499] -->
<h3 class="sectionedit14" id="exercise_2no_mo_static">Exercise 2: No Mo' Static</h3>
<div class="level3">

<p>
What happens if you give a static node, such as the floor, a mass of more than 0.0f?
</p>

</div>
<!-- EDIT14 SECTION "Exercise 2: No Mo' Static" [18500-18620] -->
<h3 class="sectionedit15" id="exercise_3behind_the_curtain">Exercise 3: Behind the Curtain</h3>
<div class="level3">

<p>
Fill your scene with walls, bricks, and cannon balls. When do you begin to see a performance impact?
</p>

<p>
Popular AAA games use a clever mix of physics, animation and prerendered graphics to give you the illusion of a real, “physical” world. Think of your favorite video games and try to spot where and how the game designers trick you into believing that the whole scene is physical. For example, think of a building “breaking” into 4-8 parts after an explosion. The pieces most likely fly on predefined (so called kinematic) paths and are only replaced by dynamic Spatials after they touch the ground… Now that you start to implement game physics yourself, look behind the curtain!
</p>

<p>
Using physics everywhere in a game sounds like a cool idea, but it is easily overused. Although the physics nodes are put to “sleep” when they are not moving, creating a world solely out of dynamic physics nodes will quickly bring you to the limits of your computer's capabilities.
</p>

</div>
<!-- EDIT15 SECTION "Exercise 3: Behind the Curtain" [18621-19626] -->
<h2 class="sectionedit16" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned how to activate the jBullet PhysicsSpace in an application by adding a <code>BulletAppState</code>. You have created PhysicsControls for simple Shape-based Geometries (for more complex shapes, read up on <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">CollisionShapes</a>). You have learned that physical objects are not only attached to the rootNode, but also registered to the PhysicsSpace. You know that it makes a difference whether a physical object has a mass (dynamic) or not (static). You are aware that overusing physics has a huge performance impact.
</p>

<p>
</p><p></p><div class="notetip">Congratulations! – You have completed the last beginner tutorial. Now you are ready to start <a href="/jme3.html" class="wikilink1" title="jme3">combining what you have learned</a>, to create a cool 3D game of your own. Show us what you can do, and feel free to share your demos, game videos, and screenshots on the <a href="http://jmonkeyengine.org/groups/free-announcements/forum/" class="urlextern" title="http://jmonkeyengine.org/groups/free-announcements/forum/" rel="nofollow">Free Announcements Forum</a>!
</div>

<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/model.html" class="wikilink1" title="tag:model" rel="tag">model</a>,
	<a href="/tag/control.html" class="wikilink1" title="tag:control" rel="tag">control</a>
</span></div>

</div>
<!-- EDIT16 SECTION "Conclusion" [19627-] -->
