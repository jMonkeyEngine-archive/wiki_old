---
title: jMonkeyEngine 3 Tutorial (4) - Hello Update Loop
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_4_-_hello_update_loop">jMonkeyEngine 3 Tutorial (4) - Hello Update Loop</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">Hello Assets</a>,
Next: <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">Hello Input System</a>
</p>

<p>
Now that you know how to load assets, such as 3D models, you want to implement some gameplay that uses these assets. In this tutorial we look at the update loop. The update loop of your game is where the action happens.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (4) - Hello Update Loop" [1-404] -->
<h2 class="sectionedit2" id="code_sample">Code Sample</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 4 - how to trigger repeating actions from the main event loop.
 * In this example, you use the loop to make the player character 
 * rotate continuously. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloLoop <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloLoop app <span class="sy0">=</span> <span class="kw1">new</span> HelloLoop<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> Geometry player<span class="sy0">;</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="co3">/** this blue box is our player character */</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        player <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"blue cube"</span>, b<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        player.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="coMULTI">/* Use the main event loop to trigger repeating actions. */</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// make the player rotate:</span>
        player.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">2</span><span class="sy0">*</span>tpf, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> 
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Build and run the file: You see a constantly rotating cube. 
</p>

</div>
<!-- EDIT2 SECTION "Code Sample" [405-1682] -->
<h2 class="sectionedit3" id="understanding_the_code">Understanding the Code</h2>
<div class="level2">

<p>
Compared to our previous code samples you note that the player Geometry is now a class field. This is because we want the update loop to be able to access and transform this Geometry. As usual, we initialize the player object in the <code>simpleInitApp()</code> method. 
</p>

<p>
Now have a closer look at the <code>simpleUpdate()</code> method – this is the update loop.
</p>
<ul>
<li class="level1"><div class="li"> The <code>player.rotate(0, 2*tpf, 0);</code> line changes the rotation of the player object. </div>
</li>
<li class="level1"><div class="li"> We use the <code>tpf</code> variable (“time per frame”) to time this action depending on the current frames per second rate. This simply means that the cube rotates with the same speed on fast and slow machines, and the game remains playable.</div>
</li>
<li class="level1"><div class="li"> When the game runs, the rotate() code is executed again and again. </div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Understanding the Code" [1683-2466] -->
<h2 class="sectionedit4" id="using_the_update_loop">Using the Update Loop</h2>
<div class="level2">

<p>
A rotating object is just a simple example. In the update loop, you typically have many tests and trigger various game actions. This is where you update score and health points, check for collisions, make enemies calculate their next move, roll the dice whether a trap has been set off, play random ambient sounds, and much more.  
</p>
<ul>
<li class="level1"><div class="li"> The <code>simpleUpdate()</code> method starts running after the <code>simpleInitApp()</code> method has initialized the scene graph and state variables.</div>
</li>
<li class="level1"><div class="li"> JME3 executes everything in the <code>simpleUpdate()</code> method repeatedly, as fast as possible.</div>
<ol>
<li class="level2"><div class="li"> Use the loop to poll the game state and then initiate actions. </div>
</li>
<li class="level2"><div class="li"> Use the loop to trigger reactions and update the game state.</div>
</li>
<li class="level2"><div class="li"> Use the loop wisely, because having too many calls in the loop also slows down the game.</div>
</li>
</ol>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Using the Update Loop" [2467-3301] -->
<h2 class="sectionedit5" id="init_-_update_-_render">Init - Update - Render</h2>
<div class="level2">

<p>
Note the the three phases of every game:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Init:</strong> The <code>simpleInitApp()</code> method is executed only <em>once</em>, right at the beginning; </div>
</li>
<li class="level1"><div class="li"> <strong>Update:</strong> The <code>simpleUpdate()</code> method runs <em>repeatedly</em>, during the game. </div>
</li>
<li class="level1"><div class="li"> <strong>Render:</strong> After every update, the jMonkeyEngine <em>automatically</em> redraws (<code>renders</code>) the screen for you.</div>
</li>
</ul>

<p>
Since rendering is automatic, initialization and updating are the two most important concepts in a SimpleApplication-based game for you:
</p>
<ul>
<li class="level1"><div class="li"> The <code>simpleInitApp()</code> method is the application's “first breath”. <br />
Here you load and create game data (once).</div>
</li>
<li class="level1"><div class="li"> The <code>simpleUpdate()</code> method is the application's “heartbeat” (the time unit is called <code>ticks</code>). <br />
Here you change their properties to update the game state (repeatedly).</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">Everything in a game happens either during initialization, or during the update loop. This means that these two methods grow very long over time. Follwo these two strategies to spread out init and update code over several modular Java classes:

<ul>
<li class="level1"><div class="li"> Move code blocks from the simpleInitApp() method to <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a>.</div>
</li>
<li class="level1"><div class="li"> Move code blocks from the simpleUpdate() method to <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a>.</div>
</li>
</ul>

<p>
Keep this in mind for later when your application grows.

</p></div>


</div>
<!-- EDIT5 SECTION "Init - Update - Render" [3302-4629] -->
<h2 class="sectionedit6" id="exercises">Exercises</h2>
<div class="level2">

<p>
Here are some fun things to try:
</p>
<ol>
<li class="level1"><div class="li"> What happens if you give the rotate() method negative numbers?</div>
</li>
<li class="level1"><div class="li"> Can you create two Geometries next to each other, and make one rotate twice as fast as the other? (use the <code>tpf</code> variable)</div>
</li>
<li class="level1"><div class="li"> Can you make a cube that pulsates? (grows and shrinks)</div>
</li>
<li class="level1"><div class="li"> Can you make a cube that changes color? (change and set the Material)</div>
</li>
<li class="level1"><div class="li"> Can you make a rolling cube? (rotate around the x axis, and translate along the z axis)</div>
</li>
</ol>

<p>
Look back at the <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a> tutorial if you do not remember the transformation methods for scaling, translating, and rotating.
</p>

<p>
</p><p></p><div class="noteimportant">Link to user-proposed solutions: <a href="http://jmonkeyengine.org/wiki/doku.php/jm3:solutions" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jm3:solutions" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jm3:solutions</a>
<em class="u">Be sure to try to solve them for yourself first!</em>
</div>


</div>
<!-- EDIT6 SECTION "Exercises" [4630-5401] -->
<h2 class="sectionedit7" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
Now you are listening to the update loop, “the heart beat” of the game, and you can add all kinds of action to it. 
</p>

<p>
The next thing the game needs is some <em>inter</em>action! Continue learning how to <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">respond to user input</a>.
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> Advanced jME3 developers use <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a> and <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a> to implement game mechanics in their update loops. You will come across these topics again later when you proceed to more advanced documentation.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/state.html" class="wikilink1" title="tag:state" rel="tag">state</a>,
	<a href="/tag/states.html" class="wikilink1" title="tag:states" rel="tag">states</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/control.html" class="wikilink1" title="tag:control" rel="tag">control</a>,
	<a href="/tag/loop.html" class="wikilink1" title="tag:loop" rel="tag">loop</a>
</span></div>

</div>
<!-- EDIT7 SECTION "Conclusion" [5402-] -->
