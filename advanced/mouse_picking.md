---
title: Mouse Picking
---
<h1 class="sectionedit1" id="mouse_picking">Mouse Picking</h1>
<div class="level1">

<p>
Mouse picking means that the user clicks an object in the scene to select it, or to interact with it otherwise. Games use picking to implement aiming and shooting, casting spells, picking up objects, selecting targets, dragging and moving objects, etc. Mouse picking can be done using fixed crosshairs, or using the mouse pointer.
</p>

<p>
<a href="/resources/jme3-advanced-mouse-picking.png" class="media" title="jme3:advanced:mouse-picking.png"><img src="/resources/jme3-advanced-mouse-picking.png" class="media" alt="" /></a>
</p>

<p>
See <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">Input Handling</a> for details on how to define the necessary input triggers, input mappings, and input listeners.
</p>

</div>
<!-- EDIT1 SECTION "Mouse Picking" [1-533] -->
<h2 class="sectionedit2" id="pick_a_target_using_fixed_crosshairs">Pick a Target Using Fixed Crosshairs</h2>
<div class="level2">

<p>
The following <code>pick target</code> input mapping implements an action that determines what a user clicked. It assumes that the mouse pointer is invisible and there are crosshairs painted in the center of the screen. It assumes that the user aims the crosshairs at an object in the scene and clicks. You use Ray Casting to identify the geometry that was picked by the user. Use this method together with a first-person flyCam. 
</p>
<ol>
<li class="level1"><div class="li"> Activate the first-person camera: <code>flyCam.setEnabled(true);</code></div>
</li>
<li class="level1"><div class="li"> Keep mouse pointer invisible using <code>inputManager.setCursorVisible(false)</code>.</div>
</li>
<li class="level1"><div class="li"> Map the <code>pick target</code> action to a MouseButtonTrigger. </div>
</li>
<li class="level1"><div class="li"> Implement the action in the Listener.</div>
</li>
</ol>

<p>
The following example rotates Spatials named “Red Box” or “Blue Box” when they are clicked. Modify this code to do whatever your game needs to do with the identified target (shoot it, take it, move it, etc).
</p>
<pre class="code java">  <span class="kw1">private</span> AnalogListener analogListener <span class="sy0">=</span> <span class="kw1">new</span> AnalogListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> intensity, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"pick target"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
         <span class="co1">// Reset results list.</span>
         CollisionResults results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
         <span class="co1">// Aim the ray from camera location in camera direction</span>
         <span class="co1">// (assuming crosshairs in center of screen).</span>
         Ray ray <span class="sy0">=</span> <span class="kw1">new</span> Ray<span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span>, cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
         <span class="co1">// Collect intersections between ray and all nodes in results list.</span>
         rootNode.<span class="me1">collideWith</span><span class="br0">(</span>ray, results<span class="br0">)</span><span class="sy0">;</span>
         <span class="co1">// Print the results so we see what is going on</span>
         <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
           <span class="co1">// For each “hit”, we know distance, impact point, geometry.</span>
           <span class="kw4">float</span> dist <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getDistance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
           Vector3f pt <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
           <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> target <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
           <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Selection #"</span> <span class="sy0">+</span> i <span class="sy0">+</span> <span class="st0">": "</span> <span class="sy0">+</span> target <span class="sy0">+</span> <span class="st0">" at "</span> <span class="sy0">+</span> pt <span class="sy0">+</span> <span class="st0">", "</span> <span class="sy0">+</span> dist <span class="sy0">+</span> <span class="st0">" WU away."</span><span class="br0">)</span><span class="sy0">;</span>
         <span class="br0">}</span>
         <span class="co1">// 5. Use the results -- we rotate the selected geometry.</span>
         <span class="kw1">if</span> <span class="br0">(</span>results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span> <span class="br0">{</span>
           <span class="co1">// The closest result is the target that the player picked:</span>
           Geometry target <span class="sy0">=</span> results.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
           <span class="co1">// Here comes the action:</span>
           <span class="kw1">if</span><span class="br0">(</span>target.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Red Box"</span><span class="br0">)</span><span class="br0">)</span>
             target.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span> intensity, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
           <span class="kw1">else</span> <span class="kw1">if</span><span class="br0">(</span>target.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Blue Box"</span><span class="br0">)</span><span class="br0">)</span>
             target.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, intensity, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
         <span class="br0">}</span>
        <span class="br0">}</span> <span class="co1">// else if ...</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT2 SECTION "Pick a Target Using Fixed Crosshairs" [534-3105] -->
<h2 class="sectionedit3" id="pick_a_target_using_the_mouse_pointer">Pick a Target Using the Mouse Pointer</h2>
<div class="level2">

<p>
The following <code>pick target</code> input mapping implements an action that determines what a user clicked. It assumes that the mouse pointer is visible, and the user aims the cursor at an object in the scene. You use ray casting to determine the geometry that was picked by the user. 
</p>

<p>
<strong>Note:</strong> Picking with a visible mouse pointer implies that your application can no longer use the default flyCam where the MouseAxisTrigger rotates the camera. You have to deactivate the flyCam mappings and provide custom mappings. Either different inputs rotate the camera, or the camera is fixed.
</p>
<ol>
<li class="level1"><div class="li"> Map the <code>pick target</code> action to a MouseButtonTrigger. </div>
</li>
<li class="level1"><div class="li"> Make the mouse pointer visible using <code>inputManager.setCursorVisible(true)</code>.</div>
</li>
<li class="level1"><div class="li"> Remap the inputs for camera rotation, or deactivate camera rotation. </div>
</li>
<li class="level1"><div class="li"> Implement the action in the Listener.</div>
</li>
</ol>

<p>
The following example rotates Spatials named “Red Box” or “Blue Box” when they are clicked. Modify this code to do whatever your game needs to do with the identified target (shoot it, take it, move it, etc).
</p>
<pre class="code java"><span class="kw1">private</span> AnalogListener analogListener <span class="sy0">=</span> <span class="kw1">new</span> AnalogListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> intensity, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"pick target"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// Reset results list.</span>
        CollisionResults results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// Convert screen click to 3d position</span>
        Vector2f click2d <span class="sy0">=</span> inputManager.<span class="me1">getCursorPosition</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        Vector3f click3d <span class="sy0">=</span> cam.<span class="me1">getWorldCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span>click2d.<span class="me1">x</span>, click2d.<span class="me1">y</span><span class="br0">)</span>, 0f<span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        Vector3f dir <span class="sy0">=</span> cam.<span class="me1">getWorldCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span>click2d.<span class="me1">x</span>, click2d.<span class="me1">y</span><span class="br0">)</span>, 1f<span class="br0">)</span>.<span class="me1">subtractLocal</span><span class="br0">(</span>click3d<span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// Aim the ray from the clicked spot forwards.</span>
        Ray ray <span class="sy0">=</span> <span class="kw1">new</span> Ray<span class="br0">(</span>click3d, dir<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// Collect intersections between ray and all nodes in results list.</span>
        rootNode.<span class="me1">collideWith</span><span class="br0">(</span>ray, results<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// (Print the results so we see what is going on:)</span>
        <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
          <span class="co1">// (For each “hit”, we know distance, impact point, geometry.)</span>
          <span class="kw4">float</span> dist <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getDistance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          Vector3f pt <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> target <span class="sy0">=</span> results.<span class="me1">getCollision</span><span class="br0">(</span>i<span class="br0">)</span>.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Selection #"</span> <span class="sy0">+</span> i <span class="sy0">+</span> <span class="st0">": "</span> <span class="sy0">+</span> target <span class="sy0">+</span> <span class="st0">" at "</span> <span class="sy0">+</span> pt <span class="sy0">+</span> <span class="st0">", "</span> <span class="sy0">+</span> dist <span class="sy0">+</span> <span class="st0">" WU away."</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="co1">// Use the results -- we rotate the selected geometry.</span>
        <span class="kw1">if</span> <span class="br0">(</span>results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span> <span class="br0">{</span>
          <span class="co1">// The closest result is the target that the player picked:</span>
          Geometry target <span class="sy0">=</span> results.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          <span class="co1">// Here comes the action:</span>
          <span class="kw1">if</span> <span class="br0">(</span>target.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Red Box"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            target.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>intensity, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
          <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>target.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Blue Box"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            target.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, intensity, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
          <span class="br0">}</span>
        <span class="br0">}</span>
      <span class="br0">}</span> <span class="co1">// else if ...</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/ray.html" class="wikilink1" title="tag:ray" rel="tag">ray</a>,
	<a href="/tag/click.html" class="wikilink1" title="tag:click" rel="tag">click</a>,
	<a href="/tag/collision.html" class="wikilink1" title="tag:collision" rel="tag">collision</a>,
	<a href="/tag/keyinput.html" class="wikilink1" title="tag:keyinput" rel="tag">keyinput</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>
</span></div>

</div>
<!-- EDIT3 SECTION "Pick a Target Using the Mouse Pointer" [3106-] -->
