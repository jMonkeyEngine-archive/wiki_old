---
title: jMonkeyEngine 3 Tutorial (8) - Hello Picking
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_8_-_hello_picking">jMonkeyEngine 3 Tutorial (8) - Hello Picking</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_animation.html" class="wikilink1" title="jme3:beginner:hello_animation">Hello Animation</a>,
Next: <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a>
</p>

<p>
Typical interactions in games include shooting, picking up objects, and opening doors. From an implementation point of view, these apparently different interactions are surprisingly similar: The user first aims and selects a target in the 3D scene, and then triggers an action on it. We call this process picking.
</p>

<p>
You can pick something by either pressing a key on the keyboard, or by clicking with the mouse. In either case, you identify the target by aiming a ray –a straight line– into the scene. This method to implement picking is called <em>ray casting</em> (which is not the same as <em>ray tracing</em>).
</p>

<p>
This tutorial relies on what you have learned in the <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">Hello Input</a> tutorial. You find more related code samples under <a href="/jme3/advanced/mouse_picking.html" class="wikilink1" title="jme3:advanced:mouse_picking">Mouse Picking</a> and <a href="/jme3/advanced/collision_and_intersection.html" class="wikilink1" title="jme3:advanced:collision_and_intersection">Collision and Intersection</a>.
</p>

<p>
<a href="/resources/jme3-beginner-beginner-picking.png" class="media" title="jme3:beginner:beginner-picking.png"><img src="/resources/jme3-beginner-beginner-picking.png" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (8) - Hello Picking" [1-991] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.collision.CollisionResult</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.collision.CollisionResults</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapText</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.MouseInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.MouseButtonTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Ray</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Sphere</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 8 - how to let the user pick (select) objects in the scene 
 * using the mouse or key presses. Can be used for shooting, opening doors, etc. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloPicking <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloPicking app <span class="sy0">=</span> <span class="kw1">new</span> HelloPicking<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
  <span class="kw1">private</span> Node shootables<span class="sy0">;</span>
  <span class="kw1">private</span> Geometry mark<span class="sy0">;</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    initCrossHairs<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// a "+" in the middle of the screen to help aiming</span>
    initKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>       <span class="co1">// load custom key mappings</span>
    initMark<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>       <span class="co1">// a red sphere to mark the hit</span>
 
    <span class="co3">/** create four colored boxes and a floor to shoot at: */</span>
    shootables <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Shootables"</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>shootables<span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"a Dragon"</span>, <span class="sy0">-</span>2f, 0f, 1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"a tin can"</span>, 1f, <span class="sy0">-</span>2f, 0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"the Sheriff"</span>, 0f, 1f, <span class="sy0">-</span>2f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"the Deputy"</span>, 1f, 0f, <span class="sy0">-</span>4f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeFloor<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCharacter<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** Declaring the "Shoot" action and mapping to its triggers. */</span>
  <span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Shoot"</span>,
      <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span>, <span class="co1">// trigger 1: spacebar</span>
      <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// trigger 2: left-button click</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Shoot"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
  <span class="co3">/** Defining the "Shoot" action: Determine what was hit and how to respond. */</span>
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Shoot"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// 1. Reset results list.</span>
        CollisionResults results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// 2. Aim the ray from cam loc to cam direction.</span>
        Ray ray <span class="sy0">=</span> <span class="kw1">new</span> Ray<span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span>, cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// 3. Collect intersections between Ray and Shootables in results list.</span>
        shootables.<span class="me1">collideWith</span><span class="br0">(</span>ray, results<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// 4. Print the results</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"----- Collisions? "</span> <span class="sy0">+</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"-----"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
          <span class="co1">// For each hit, we know distance, impact point, name of geometry.</span>
          <span class="kw4">float</span> dist <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getDistance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          Vector3f pt <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> hit <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"* Collision #"</span> <span class="sy0">+</span> i<span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"  You shot "</span> <span class="sy0">+</span> hit <span class="sy0">+</span> <span class="st0">" at "</span> <span class="sy0">+</span> pt <span class="sy0">+</span> <span class="st0">", "</span> <span class="sy0">+</span> dist <span class="sy0">+</span> <span class="st0">" wu away."</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="co1">// 5. Use the results (we mark the hit object)</span>
        <span class="kw1">if</span> <span class="br0">(</span>results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span> <span class="br0">{</span>
          <span class="co1">// The closest collision point is what was truly hit:</span>
          CollisionResult closest <span class="sy0">=</span> results.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          <span class="co1">// Let's interact - we mark the hit with a red dot.</span>
          mark.<span class="me1">setLocalTranslation</span><span class="br0">(</span>closest.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
          rootNode.<span class="me1">attachChild</span><span class="br0">(</span>mark<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
          <span class="co1">// No hits? Then remove the red mark.</span>
          rootNode.<span class="me1">detachChild</span><span class="br0">(</span>mark<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span>
 
  <span class="co3">/** A cube object for target practice */</span>
  <span class="kw1">protected</span> Geometry makeCube<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> x, <span class="kw4">float</span> y, <span class="kw4">float</span> z<span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    Geometry cube <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>name, box<span class="br0">)</span><span class="sy0">;</span>
    cube.<span class="me1">setLocalTranslation</span><span class="br0">(</span>x, y, z<span class="br0">)</span><span class="sy0">;</span>
    Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">randomColor</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    cube.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span> cube<span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** A floor to show that the "shot" can go through several objects. */</span>
  <span class="kw1">protected</span> Geometry makeFloor<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">15</span>, .2f, <span class="nu0">15</span><span class="br0">)</span><span class="sy0">;</span>
    Geometry floor <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"the Floor"</span>, box<span class="br0">)</span><span class="sy0">;</span>
    floor.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">4</span>, <span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span><span class="sy0">;</span>
    Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Gray</span><span class="br0">)</span><span class="sy0">;</span>
    floor.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span> floor<span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** A red ball that marks the last spot that was "hit" by the "shot". */</span>
  <span class="kw1">protected</span> <span class="kw4">void</span> initMark<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    Sphere sphere <span class="sy0">=</span> <span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">30</span>, <span class="nu0">30</span>, 0.2f<span class="br0">)</span><span class="sy0">;</span>
    mark <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"BOOM!"</span>, sphere<span class="br0">)</span><span class="sy0">;</span>
    Material mark_mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mark_mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
    mark.<span class="me1">setMaterial</span><span class="br0">(</span>mark_mat<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** A centred plus sign to help the player aim. */</span>
  <span class="kw1">protected</span> <span class="kw4">void</span> initCrossHairs<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    setDisplayStatView<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
    BitmapText ch <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    ch.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">*</span> <span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    ch.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"+"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// crosshairs</span>
    ch.<span class="me1">setLocalTranslation</span><span class="br0">(</span> <span class="co1">// center</span>
      settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span> <span class="sy0">-</span> ch.<span class="me1">getLineWidth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">2</span>, settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span> <span class="sy0">+</span> ch.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">/</span><span class="nu0">2</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">attachChild</span><span class="br0">(</span>ch<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">protected</span> Spatial makeCharacter<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// load a character from jme3test-test-data</span>
    Spatial golem <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Oto/Oto.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
    golem.<span class="me1">scale</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span>
    golem.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="sy0">-</span>1.0f, <span class="sy0">-</span>1.5f, <span class="sy0">-</span>0.6f<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// We must add a light to make the model visible</span>
    DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f, <span class="sy0">-</span>0.7f, <span class="sy0">-</span>1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    golem.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span> golem<span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
You should see four colored cubes floating over a gray floor, and cross-hairs. Aim the cross-hairs and click, or press the spacebar to shoot. The hit spot is marked with a red dot.
</p>

<p>
Keep an eye on the application's output stream, it will give you more details: The name of the mesh that was hit, the coordinates of the hit, and the distance.
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [992-7402] -->
<h2 class="sectionedit3" id="understanding_the_helper_methods">Understanding the Helper Methods</h2>
<div class="level2">

<p>
The methods <code>makeCube()</code>,  <code>makeFloor()</code>, <code>initMark()</code>, and <code>initCrossHairs</code>, are custom helper methods. We call them from  <code>simpleInitApp()</code> to initialize the scenegraph with sample content.
</p>
<ol>
<li class="level1"><div class="li"> <code>makeCube()</code> creates simple colored boxes for “target practice”.</div>
</li>
<li class="level1"><div class="li"> <code>makeFloor()</code> creates a gray floor node for “target practice”.</div>
</li>
<li class="level1"><div class="li"> <code>initMark()</code> creates a red sphere (“mark”). We will use it later to mark the spot that was hit.</div>
<ul>
<li class="level2"><div class="li"> Note that the mark is not attached and therefor not visible at the start!</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <code>initCrossHairs()</code> creates simple cross-hairs by printing a “+” sign in the middle of the screen.</div>
<ul>
<li class="level2"><div class="li"> Note that the cross-hairs are attached to the <code>guiNode</code>, not to the <code>rootNode</code>.</div>
</li>
</ul>
</li>
</ol>

<p>
In this example, we attached all “shootable” objects to one custom node, <code>Shootables</code>. This is an optimization so the engine only has to calculate intersections with objects we are actually interested in.  The <code>Shootables</code> node is attached to the <code>rootNode</code> as usual.
</p>

</div>
<!-- EDIT3 SECTION "Understanding the Helper Methods" [7403-8443] -->
<h2 class="sectionedit4" id="understanding_ray_casting_for_hit_testing">Understanding Ray Casting for Hit Testing</h2>
<div class="level2">

<p>
Our goal is to determine which box the user “shot” (picked). In general, we want to determine which mesh the user has selected by aiming the cross-hairs at it. Mathematically, we draw a line from the camera and see whether it intersects with objects in the 3D scene. This line is called a ray.
</p>

<p>
Here is our simple ray casting algorithm for picking objects:
</p>
<ol>
<li class="level1"><div class="li"> Reset the results list.</div>
</li>
<li class="level1"><div class="li"> Cast a ray from cam location into the cam direction.</div>
</li>
<li class="level1"><div class="li"> Collect all intersections between the ray and <code>Shootable</code> nodes in the <code>results</code> list.</div>
</li>
<li class="level1"><div class="li"> Use the results list to determine what was hit:</div>
<ol>
<li class="level2"><div class="li"> For each hit, JME reports its distance from the camera, impact point, and the name of the mesh.</div>
</li>
<li class="level2"><div class="li"> Sort the results by distance.</div>
</li>
<li class="level2"><div class="li"> Take the closest result, it is the mesh that was hit.</div>
</li>
</ol>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "Understanding Ray Casting for Hit Testing" [8444-9286] -->
<h2 class="sectionedit5" id="implementing_hit_testing">Implementing Hit Testing</h2>
<div class="level2">

</div>
<!-- EDIT5 SECTION "Implementing Hit Testing" [9287-9324] -->
<h3 class="sectionedit6" id="loading_the_scene">Loading the scene</h3>
<div class="level3">

<p>
First initialize some shootable nodes and attach them to the scene. You will use the <code>mark</code> object later.
</p>
<pre class="code java">  Node shootables<span class="sy0">;</span>
  Geometry mark<span class="sy0">;</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    initCrossHairs<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    initKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    initMark<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
    shootables <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Shootables"</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>shootables<span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"a Dragon"</span>,    <span class="sy0">-</span>2f, 0f, 1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"a tin can"</span>,    1f,<span class="sy0">-</span>2f, 0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"the Sheriff"</span>,  0f, 1f,<span class="sy0">-</span>2f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"the Deputy"</span>,   1f, 0f, <span class="sy0">-</span><span class="nu0">4</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeFloor<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "Loading the scene" [9325-10011] -->
<h3 class="sectionedit7" id="setting_up_the_input_listener">Setting Up the Input Listener</h3>
<div class="level3">

<p>
Next you declare the shooting action. It can be triggered either by clicking, or by pressing the space bar. The <code>initKeys()</code> method is called from <code>simpleInitApp()</code> to set up these input mappings.
</p>
<pre class="code java">  <span class="co3">/** Declaring the "Shoot" action and its triggers. */</span>
  <span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Shoot"</span>,      <span class="co1">// Declare...</span>
      <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span>, <span class="co1">// trigger 1: spacebar, or</span>
      <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>         <span class="co1">// trigger 2: left-button click</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Shoot"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// ... and add.</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT7 SECTION "Setting Up the Input Listener" [10012-10652] -->
<h3 class="sectionedit8" id="picking_action_using_crosshairs">Picking Action Using Crosshairs</h3>
<div class="level3">

<p>
Next we implement the ActionListener that responds to the Shoot trigger with an action. The action follows the ray casting algorithm described above:
</p>
<ol>
<li class="level1"><div class="li"> For every click or press of the spacebar, the <code>Shoot</code> action is triggered.</div>
</li>
<li class="level1"><div class="li"> The action casts a ray forward and determines intersections with shootable objects (= ray casting).</div>
</li>
<li class="level1"><div class="li"> For any target that has been hit, it prints name, distance, and coordinates of the hit.</div>
</li>
<li class="level1"><div class="li"> Finally it attaches a red mark to the closest result, to highlight the spot that was actually hit.</div>
</li>
<li class="level1"><div class="li"> When nothing was hit, the results list is empty, and the red mark is removed.</div>
</li>
</ol>

<p>
Note how it prints a lot of output to show you which hits were registered.
</p>
<pre class="code java">  <span class="co3">/** Defining the "Shoot" action: Determine what was hit and how to respond. */</span>
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Shoot"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// 1. Reset results list.</span>
        CollisionResults results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// 2. Aim the ray from cam loc to cam direction.</span>
        Ray ray <span class="sy0">=</span> <span class="kw1">new</span> Ray<span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span>, cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// 3. Collect intersections between Ray and Shootables in results list.</span>
        shootables.<span class="me1">collideWith</span><span class="br0">(</span>ray, results<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// 4. Print results.</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"----- Collisions? "</span> <span class="sy0">+</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"-----"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
          <span class="co1">// For each hit, we know distance, impact point, name of geometry.</span>
          <span class="kw4">float</span> dist <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getDistance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          Vector3f pt <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> hit <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"* Collision #"</span> <span class="sy0">+</span> i<span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"  You shot "</span> <span class="sy0">+</span> hit <span class="sy0">+</span> <span class="st0">" at "</span> <span class="sy0">+</span> pt <span class="sy0">+</span> <span class="st0">", "</span> <span class="sy0">+</span> dist <span class="sy0">+</span> <span class="st0">" wu away."</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="co1">// 5. Use the results (we mark the hit object)</span>
        <span class="kw1">if</span> <span class="br0">(</span>results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span><span class="br0">{</span>
          <span class="co1">// The closest collision point is what was truly hit:</span>
          CollisionResult closest <span class="sy0">=</span> results.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          mark.<span class="me1">setLocalTranslation</span><span class="br0">(</span>closest.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
          <span class="co1">// Let's interact - we mark the hit with a red dot.</span>
          rootNode.<span class="me1">attachChild</span><span class="br0">(</span>mark<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        <span class="co1">// No hits? Then remove the red mark.</span>
          rootNode.<span class="me1">detachChild</span><span class="br0">(</span>mark<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

<p>
<strong>Tip:</strong> Notice how you use the provided method <code>results.getClosestCollision().getContactPoint()</code> to determine the <em>closest</em> hit's location. If your game includes a “weapon” or “spell” that can hit multiple targets, you could also loop over the list of results, and interact with each of them.
</p>

</div>
<!-- EDIT8 SECTION "Picking Action Using Crosshairs" [10653-13426] -->
<h3 class="sectionedit9" id="picking_action_using_mouse_pointer">Picking Action Using Mouse Pointer</h3>
<div class="level3">

<p>
The above example assumes that the player is aiming crosshairs (attached to the center of the screen) at the target. But you can change the picking code to allow you to freely click at objects in the scene with a visible mouse pointer. In order to do this you have to convert the 2d screen coordinates of the click to 3D world coordinates to get the start point of the picking ray.
</p>
<ol>
<li class="level1"><div class="li"> Reset result list.</div>
</li>
<li class="level1"><div class="li"> Get 2D click coordinates.</div>
</li>
<li class="level1"><div class="li"> Convert 2D screen coordinates to their 3D equivalent.</div>
</li>
<li class="level1"><div class="li"> Aim the ray from the clicked 3D location forwards into the scene.</div>
</li>
<li class="level1"><div class="li"> Collect intersections between ray and all nodes into a results list.</div>
</li>
</ol>
<pre class="code java">...
<span class="me1">CollisionResults</span> results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Vector2f click2d <span class="sy0">=</span> inputManager.<span class="me1">getCursorPosition</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f click3d <span class="sy0">=</span> cam.<span class="me1">getWorldCoordinates</span><span class="br0">(</span>
    <span class="kw1">new</span> Vector2f<span class="br0">(</span>click2d.<span class="me1">x</span>, click2d.<span class="me1">y</span><span class="br0">)</span>, 0f<span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f dir <span class="sy0">=</span> cam.<span class="me1">getWorldCoordinates</span><span class="br0">(</span>
    <span class="kw1">new</span> Vector2f<span class="br0">(</span>click2d.<span class="me1">x</span>, click2d.<span class="me1">y</span><span class="br0">)</span>, 1f<span class="br0">)</span>.<span class="me1">subtractLocal</span><span class="br0">(</span>click3d<span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Ray ray <span class="sy0">=</span> <span class="kw1">new</span> Ray<span class="br0">(</span>click3d, dir<span class="br0">)</span><span class="sy0">;</span>
shootables.<span class="me1">collideWith</span><span class="br0">(</span>ray, results<span class="br0">)</span><span class="sy0">;</span>
...</pre>

<p>
Use this together with <code>inputManager.setCursorVisible(true)</code> to make certain the cursor is visible. 
</p>

<p>
Note that since you now use the mouse for picking, you can no longer use it to rotate the camera. If you want to have a visible mouse pointer for picking in your game, you have to redefine the camera rotation mappings.
</p>

</div>
<!-- EDIT9 SECTION "Picking Action Using Mouse Pointer" [13427-14858] -->
<h2 class="sectionedit10" id="exercises">Exercises</h2>
<div class="level2">

<p>
After a hit was registered, the closest object is identified as target, and marked with a red dot.
Modify the code sample to solve these exercises:
</p>

</div>
<!-- EDIT10 SECTION "Exercises" [14859-15030] -->
<h3 class="sectionedit11" id="exercise_1magic_spell">Exercise 1: Magic Spell</h3>
<div class="level3">

<p>
Change the color of the closest clicked target! <br />
Here are some tips:
</p>
<ol>
<li class="level1"><div class="li"> Go to the line where the closest target is indentified, and add your changes after that.</div>
</li>
<li class="level1"><div class="li"> To change an object's color, you must first know its Geometry. Identify the node by identifying the target's name.</div>
<ul>
<li class="level2"><div class="li"> Use <code>Geometry g = closest.getGeometry();</code></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Create a new color material and set the node's Material to this color.</div>
<ul>
<li class="level2"><div class="li"> Look inside the <code>makeCube()</code> method for an example of how to set random colors.</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT11 SECTION "Exercise 1: Magic Spell" [15031-15563] -->
<h3 class="sectionedit12" id="exercise_2shoot_a_character">Exercise 2: Shoot a Character</h3>
<div class="level3">

<p>
Shooting boxes isn't very exciting – can you add code that loads and positions a model in the scene, and shoot at it?
</p>
<ul>
<li class="level1"><div class="li"> Tip: You can use <code>Spatial golem = assetManager.loadModel(“Models/Oto/Oto.mesh.xml”);</code> from the engine's jme3-test-data.jar.</div>
</li>
<li class="level1"><div class="li"> Tip: Models are shaded! You need some light!</div>
</li>
</ul>

</div>
<!-- EDIT12 SECTION "Exercise 2: Shoot a Character" [15564-15902] -->
<h3 class="sectionedit13" id="exercise_3pick_up_into_inventory">Exercise 3: Pick up into Inventory</h3>
<div class="level3">

<p>
Change the code as follows to simulate the player picking up objects into the inventory: When you click once, the closest target is identified and detached from the scene. When you click a second time, the target is reattached at the location that you have clicked. Here are some tips:
</p>
<ol>
<li class="level1"><div class="li"> Create an inventory node to store the detached nodes temporarily.</div>
</li>
<li class="level1"><div class="li"> The inventory node is not attached to the rootNode.</div>
</li>
<li class="level1"><div class="li"> You can make the inventory visible by attaching the inventory node to the guiNode (which attaches it to the HUD). Note the following caveats:</div>
<ul>
<li class="level2"><div class="li"> If your nodes use a lit Material (not “Unshaded.j3md”), also add a light to the guiNode.</div>
</li>
<li class="level2"><div class="li"> Size units are pixels in the HUD, therefor a 2-wu cube is displayed only 2 pixels wide in the HUD. – Scale it bigger!</div>
</li>
<li class="level2"><div class="li"> Position the nodes: The bottom left corner of the HUD is (0f,0f), and the top right corner is at (settings.getWidth(),settings.getHeight()).</div>
</li>
</ul>
</li>
</ol>

<p>
</p><p></p><div class="noteimportant">Link to user-proposed solutions: <a href="http://jmonkeyengine.org/wiki/doku.php/jm3:solutions" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jm3:solutions" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jm3:solutions</a>
<em class="u">Be sure to try to solve them for yourself first!</em>
</div>


</div>
<!-- EDIT13 SECTION "Exercise 3: Pick up into Inventory" [15903-17036] -->
<h2 class="sectionedit14" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned how to use ray casting to solve the task of determining what object a user selected on the screen. You learned that this can be used for a variety of interactions, such as shooting, opening, picking up and dropping items, pressing a button or lever, etc.
</p>

<p>
Use your imagination from here:
</p>
<ul>
<li class="level1"><div class="li"> In your game, the click can trigger any action on the identified Geometry: Detach it and put it into the inventory, attach something to it, trigger an animation or effect, open a door or crate, – etc.</div>
</li>
<li class="level1"><div class="li"> In your game, you could replace the red mark with a particle emitter, add an explosion effect, play a sound, calculate the new score after each hit depending on what was hit – etc.</div>
</li>
</ul>

<p>
Now, wouldn't it be nice if those targets and the floor were solid objects and you could walk around between them? Let's continue to learn about <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Collision Detection</a>.
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">Hello Input</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/mouse_picking.html" class="wikilink1" title="jme3:advanced:mouse_picking">Mouse Picking</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/collision_and_intersection.html" class="wikilink1" title="jme3:advanced:collision_and_intersection">Collision and Intersection</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/ray.html" class="wikilink1" title="tag:ray" rel="tag">ray</a>,
	<a href="/tag/click.html" class="wikilink1" title="tag:click" rel="tag">click</a>,
	<a href="/tag/collision.html" class="wikilink1" title="tag:collision" rel="tag">collision</a>,
	<a href="/tag/keyinput.html" class="wikilink1" title="tag:keyinput" rel="tag">keyinput</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>
</span></div>

</div>
<!-- EDIT14 SECTION "Conclusion" [17037-] -->
