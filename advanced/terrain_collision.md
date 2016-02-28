---
title: Terrain Collision
---
<h2 class="sectionedit1" id="terrain_collision">Terrain Collision</h2>
<div class="level2">

<p>
This tutorial expands the HelloTerrain tutorial and makes the terrain solid. You combine what you learned in <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">Hello Terrain</a> and <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a> and add a CollisionShape to the terrain. The terrain's CollisionShape lets the first-person player (who is also a CollisionShape) collide with the terrain, i.e. walk on it and stand on it. 
</p>

</div>
<!-- EDIT1 SECTION "Terrain Collision" [1-401] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.BulletAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.collision.shapes.CapsuleCollisionShape</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.collision.shapes.CollisionShape</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.CharacterControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.control.RigidBodyControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.bullet.util.CollisionShapeFactory</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainLodControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.AbstractHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainQuad</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.ImageBasedHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture.WrapMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.ArrayList</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.List</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">jme3tools.converters.ImageToAwt</span><span class="sy0">;</span>
 
<span class="co3">/**
 * This demo shows a terrain with collision detection, 
 * that you can walk around in with a first-person perspective.
 * This code combines HelloCollision and HelloTerrain.
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloTerrainCollision <span class="kw1">extends</span> SimpleApplication
        <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> <span class="br0">{</span>
 
  <span class="kw1">private</span> BulletAppState bulletAppState<span class="sy0">;</span>
  <span class="kw1">private</span> RigidBodyControl landscape<span class="sy0">;</span>
  <span class="kw1">private</span> CharacterControl player<span class="sy0">;</span>
  <span class="kw1">private</span> Vector3f walkDirection <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw4">boolean</span> left <span class="sy0">=</span> <span class="kw2">false</span>, right <span class="sy0">=</span> <span class="kw2">false</span>, up <span class="sy0">=</span> <span class="kw2">false</span>, down <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
  <span class="kw1">private</span> TerrainQuad terrain<span class="sy0">;</span>
  <span class="kw1">private</span> Material mat_terrain<span class="sy0">;</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloTerrainCollision app <span class="sy0">=</span> <span class="kw1">new</span> HelloTerrainCollision<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** Set up Physics */</span>
    bulletAppState <span class="sy0">=</span> <span class="kw1">new</span> BulletAppState<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    stateManager.<span class="me1">attach</span><span class="br0">(</span>bulletAppState<span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//bulletAppState.getPhysicsSpace().enableDebug(assetManager);</span>
 
    flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span><span class="nu0">100</span><span class="br0">)</span><span class="sy0">;</span>
    setUpKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1. Create terrain material and load four textures into it. */</span>
    mat_terrain <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
            <span class="st0">"Common/MatDefs/Terrain/Terrain.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.1) Add ALPHA map (for red-blue-green coded splat textures) */</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Alpha"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/alphamap.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.2) Add GRASS texture into the red layer (Tex1). */</span>
    Texture grass <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/grass.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    grass.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex1"</span>, grass<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex1Scale"</span>, 64f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.3) Add DIRT texture into the green layer (Tex2) */</span>
    Texture dirt <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/dirt.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    dirt.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex2"</span>, dirt<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex2Scale"</span>, 32f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 1.4) Add ROAD texture into the blue layer (Tex3) */</span>
    Texture rock <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/road.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    rock.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex3"</span>, rock<span class="br0">)</span><span class="sy0">;</span>
    mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex3Scale"</span>, 128f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 2. Create the height map */</span>
    AbstractHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
    Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Textures/Terrain/splat/mountains512.png"</span><span class="br0">)</span><span class="sy0">;</span>
    heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    heightmap.<span class="me1">load</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 3. We have prepared material and heightmap. 
     * Now we create the actual terrain:
     * 3.1) Create a TerrainQuad and name it "my terrain".
     * 3.2) A good value for terrain tiles is 64x64 -- so we supply 64+1=65.
     * 3.3) We prepared a heightmap of size 512x512 -- so we supply 512+1=513.
     * 3.4) As LOD step scale we supply Vector3f(1,1,1).
     * 3.5) We supply the prepared heightmap itself.
     */</span>
    terrain <span class="sy0">=</span> <span class="kw1">new</span> TerrainQuad<span class="br0">(</span><span class="st0">"my terrain"</span>, <span class="nu0">65</span>, <span class="nu0">513</span>, heightmap.<span class="me1">getHeightMap</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 4. We give the terrain its material, position &amp; scale it, and attach it. */</span>
    terrain.<span class="me1">setMaterial</span><span class="br0">(</span>mat_terrain<span class="br0">)</span><span class="sy0">;</span>
    terrain.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">100</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    terrain.<span class="me1">setLocalScale</span><span class="br0">(</span>2f, 1f, 2f<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 5. The LOD (level of detail) depends on were the camera is: */</span>
    List<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span> cameras <span class="sy0">=</span> <span class="kw1">new</span> ArrayList<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    cameras.<span class="me1">add</span><span class="br0">(</span>getCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    TerrainLodControl control <span class="sy0">=</span> <span class="kw1">new</span> TerrainLodControl<span class="br0">(</span>terrain, cameras<span class="br0">)</span><span class="sy0">;</span>
    terrain.<span class="me1">addControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** 6. Add physics: */</span> 
    <span class="co1">// We set up collision detection for the scene by creating a static </span>
    RigidBodyControl with mass zero.<span class="sy0">*/</span>
    terrain.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> RigidBodyControl<span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
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
    player.<span class="me1">setPhysicsLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">10</span>, <span class="nu0">10</span>, <span class="nu0">10</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// We attach the scene and the player to the rootnode and the physics space,</span>
    <span class="co1">// to make them appear in the game world.</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
 
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
  <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> binding, <span class="kw4">boolean</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
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
    Vector3f camDir <span class="sy0">=</span> cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>0.6f<span class="br0">)</span><span class="sy0">;</span>
    Vector3f camLeft <span class="sy0">=</span> cam.<span class="me1">getLeft</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">multLocal</span><span class="br0">(</span>0.4f<span class="br0">)</span><span class="sy0">;</span>
    walkDirection.<span class="me1">set</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">if</span> <span class="br0">(</span>left<span class="br0">)</span>  <span class="br0">{</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft<span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
    <span class="kw1">if</span> <span class="br0">(</span>right<span class="br0">)</span> <span class="br0">{</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camLeft.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
    <span class="kw1">if</span> <span class="br0">(</span>up<span class="br0">)</span>    <span class="br0">{</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir<span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
    <span class="kw1">if</span> <span class="br0">(</span>down<span class="br0">)</span>  <span class="br0">{</span> walkDirection.<span class="me1">addLocal</span><span class="br0">(</span>camDir.<span class="me1">negate</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
    player.<span class="me1">setWalkDirection</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span>
    cam.<span class="me1">setLocation</span><span class="br0">(</span>player.<span class="me1">getPhysicsLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
To try this code, create a New Project → JME3 → BasicGame using the default settings. Paste the sample code over the pregenerated Main.java class. Chnage the package to “mygame” if necessary. Open the Project Properties, Libraries, and add the <code>jme3-test-data</code> library to make certain you have all the files. 
</p>

<p>
Compile and run the code. You should see a terrain. You can use the WASD keys and the mouse to run up and down the hills.
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [402-8616] -->
<h2 class="sectionedit3" id="understanding_the_code">Understanding the Code</h2>
<div class="level2">

</div>
<!-- EDIT3 SECTION "Understanding the Code" [8617-8649] -->
<h3 class="sectionedit4" id="the_terrain_code">The Terrain Code</h3>
<div class="level3">

<p>
Read <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">Hello Terrain</a> for details of the following parts that we reuse:
</p>
<ol>
<li class="level1"><div class="li"> The <code>AbstractHeightMap</code> is an efficient way to describe the shape of the terrain.</div>
</li>
<li class="level1"><div class="li"> The <code>Terrain.j3md</code>-based Material and its texture layers let you colorize rocky mountain, grassy valleys, and a paved path criss-crossing over the landscape. </div>
</li>
<li class="level1"><div class="li"> The TerrainQuad is the finished <code>terrain</code> Spatial that you attach to the rootNode.</div>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "The Terrain Code" [8650-9106] -->
<h3 class="sectionedit5" id="the_collision_detection_code">The Collision Detection Code</h3>
<div class="level3">

<p>
Read <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a> for details of the following parts that we reuse:
</p>
<ol>
<li class="level1"><div class="li"> The <code>BulletAppState</code> lines activate physics.</div>
</li>
<li class="level1"><div class="li"> The <code>ActionListener</code> (<code>onAction()</code>) lets you reconfigure the input handling for the first-person player, so it takes collision detection into account.</div>
</li>
<li class="level1"><div class="li"> The custom <code>setUpKeys()</code> method loads your reconfigured input handlers. They now don't just walk blindly, but calculate the <code>walkDirection</code> vector that we need for collision detection.</div>
</li>
<li class="level1"><div class="li"> <code>simpleUpdate()</code> uses the <code>walkDirection</code> vector and makes the character walk, while taking obstacles and solid walls/floor into account. <pre class="code java">player.<span class="me1">setWalkDirection</span><span class="br0">(</span>walkDirection<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> The RigidBodyControl <code>landscape</code> is the CollisionShape of the terrain.</div>
</li>
<li class="level1"><div class="li"> The physical first-person player is a CapsuleCollisionShape with a CharacterControl.</div>
</li>
</ol>

</div>
<!-- EDIT5 SECTION "The Collision Detection Code" [9107-10007] -->
<h3 class="sectionedit6" id="combining_the_two">Combining the Two</h3>
<div class="level3">

<p>
Here are the changed parts to combine the two:
</p>
<ol>
<li class="level1"><div class="li"> You create a static (zero-mass) RigidBodyControl. </div>
</li>
<li class="level1"><div class="li"> Add the control to the <code>terrain</code> to make it physical.</div>
</li>
</ol>
<pre class="code java"><span class="co3">/** 6. Add physics: */</span> 
    terrain.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> RigidBodyControl<span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>  </pre>

<p>
You attach the <code>terrain</code> and the first-person <code>player</code> to the rootNode, and to the physics space, to make them appear in the game world.
</p>
<pre class="code java">    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span>
    bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT6 SECTION "Combining the Two" [10008-10557] -->
<h2 class="sectionedit7" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You see that you can combine snippets of sample code (such as HelloTerrain and HelloCollision), and create a new application from it that combines two features into soemthing new.
</p>

<p>
You should spawn high up in the area and fall down to the map, giving you a few seconds to survey the area.  Then walk around and see how you like the lay of the land.
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">Hello Terrain</a>,</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/terrain.html" class="wikilink1" title="jme3:advanced:terrain">Terrain</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/terrain.html" class="wikilink1" title="tag:terrain" rel="tag">terrain</a>,
	<a href="/tag/collision.html" class="wikilink1" title="tag:collision" rel="tag">collision</a>
</span></div>

</div>
<!-- EDIT7 SECTION "Conclusion" [10558-] -->
