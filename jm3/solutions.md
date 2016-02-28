---
title: Some proposed solutions
---
<h1 class="sectionedit1" id="some_proposed_solutions">Some proposed solutions</h1>
<div class="level1">

<p>
This is a user-proposed group of solutions for some or all of the exercises presented throughout the beginner tutorials (<a href="http://jmonkeyengine.org/wiki/doku.php/jme3#tutorials_for_beginners" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3#tutorials_for_beginners" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3#tutorials_for_beginners</a>). 
There are several ways to do them, so take what you see with a grain of salt, and actually try to do them yourself instead of jumping to the solution, for it is the best way to learn!
</p>

</div>
<!-- EDIT1 SECTION "Some proposed solutions" [1-416] -->
<h2 class="sectionedit2" id="hello_update_loop">Hello Update Loop</h2>
<div class="level2">

</div>
<!-- EDIT2 SECTION "Hello Update Loop" [417-447] -->
<h3 class="sectionedit3" id="exercise_1">Exercise 1</h3>
<div class="level3">

<p>
It will spin the other way around.
</p>

</div>
<!-- EDIT3 SECTION "Exercise 1" [448-505] -->
<h3 class="sectionedit4" id="exercise_2">Exercise 2</h3>
<div class="level3">

<p>
First, one must declare another Geometry, for example, a red cube:
</p>
<pre class="code java"><span class="kw1">protected</span> Geometry redCube<span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ...
 
    <span class="co1">// Creates the new cube</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    redCube <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"red cube"</span>, b2<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// For the new cube to become red colored</span>
    Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
    redCube.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// To position the red cube next the other cube</span>
    redCube.<span class="me1">move</span><span class="br0">(</span><span class="nu0">2</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// Makes the red cube appear on screen</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>redCube<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
To have the red cube spin twice as fast as the other cube, simply make it rotate on the same axis but with double the value:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// make the player rotate</span>
    player.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">2</span><span class="sy0">*</span>tpf, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// make the red cube rotate twice as fast the player</span>
    redCube.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">4</span><span class="sy0">*</span>tpf, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "Exercise 2" [506-1529] -->
<h3 class="sectionedit5" id="exercise_3">Exercise 3</h3>
<div class="level3">

<p>
One possible solution is to shrink or grow depending on current size. The cube may start by either growing or shrinking. If the cube is growing, it will start shrinking instead only when it reaches a size large enough. If the cube is shrinking, it will start growing again, only when the size is small enough. In short, the cube should switch between growing and shrinking when it reaches a specified maximum and minimum sizes. The following code is an example of this solution:
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw4">boolean</span> grow <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
...
<span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>grow<span class="br0">)</span> <span class="br0">{</span>
                player.<span class="me1">scale</span><span class="br0">(</span><span class="nu0">1</span> <span class="sy0">+</span> <span class="br0">(</span>3f <span class="sy0">*</span> tpf<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
                player.<span class="me1">scale</span><span class="br0">(</span><span class="nu0">1</span> <span class="sy0">-</span> <span class="br0">(</span>3f <span class="sy0">*</span> tpf<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
 
        Vector3f s <span class="sy0">=</span> player.<span class="me1">getLocalScale</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>s.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> 1.2f<span class="br0">)</span> <span class="br0">{</span>
                grow <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>s.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&lt;</span> 0.8f<span class="br0">)</span> <span class="br0">{</span>
                grow <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
        <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
The cube starts by growing, and when it reaches a size larger than 120% its original size, it starts shrinking instead. The cube will then keep shrinking, until it reaches a size smaller than 80% its original size, which will make it start growing again, and so on.
</p>

<p>
Another approach is to switch between shrinking and growing every chosen unit of time. The tpf variable stores the time per frame rendered, so if you sum every tpf at the simpleUpdate method, you get the time passed since the game started. Using time like a stopwatch, one may grow the cube for some time, and then shrink the cube for the same amount of time, and start over again. The following code shows an example of this solution:
</p>
<pre class="code java"><span class="co1">// Time passed</span>
<span class="kw1">private</span> <span class="kw4">float</span> timeVar <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
...
<span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    timeVar <span class="sy0">+=</span> tpf<span class="sy0">;</span>
    <span class="kw1">if</span> <span class="br0">(</span>timeVar <span class="sy0">&lt;</span> <span class="nu0">2</span><span class="br0">)</span> <span class="br0">{</span>
        player.<span class="me1">scale</span><span class="br0">(</span><span class="nu0">1</span> <span class="sy0">+</span> tpf <span class="sy0">*</span> 0.4f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>timeVar <span class="sy0">&lt;</span> <span class="nu0">4</span><span class="br0">)</span> <span class="br0">{</span>
        player.<span class="me1">scale</span><span class="br0">(</span><span class="nu0">1</span> <span class="sy0">-</span> tpf <span class="sy0">*</span> 0.4f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        timeVar <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
The cube grows for 2 two seconds, then shrinks for another 2 seconds, and repeats indefinitely.
</p>

<p>
Another approach is to set the cube scale as the result of a sine wave. This results in a smooth repetitive oscillating scale. Note however that this approach is computational expensive due to the use of the sine function. One may create a sine wave by calculating sine as a function of time. As such, for each iteration of the simpleUpdate method, the scale is set as the result of sine as function of time plus the original cube scale. The following code shows an example of this approach:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw4">float</span> timeInSec <span class="sy0">=</span> timer.<span class="me1">getTimeInSeconds</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw4">float</span> initScale <span class="sy0">=</span> <span class="nu0">1</span><span class="sy0">;</span>
    <span class="kw4">float</span> amplitude <span class="sy0">=</span> 0.5f<span class="sy0">;</span>
    <span class="kw4">float</span> angularFrequency <span class="sy0">=</span> <span class="nu0">1</span><span class="sy0">;</span>
    <span class="kw4">float</span> scale <span class="sy0">=</span> initScale <span class="sy0">+</span> amplitude <span class="sy0">*</span> FastMath.<span class="me1">sin</span><span class="br0">(</span>timeInSec <span class="sy0">*</span> angularFrequency<span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setLocalScale</span><span class="br0">(</span>scale<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
The cube should repeatedly and smoothly grow and shrink and have maximum and minimum scale of 0.5 and 1.5 its original size. The following variables can change the scale behavior:
</p>
<ul>
<li class="level1"><div class="li"> initScale - Sets the initial scale of cube</div>
</li>
<li class="level1"><div class="li"> amplitude - Increases minimum and maximum scale</div>
</li>
<li class="level1"><div class="li"> angularFrequency - Increases scale speed</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Exercise 3" [1530-4688] -->
<h3 class="sectionedit6" id="exercise_4">Exercise 4</h3>
<div class="level3">

<p>
Same logic! Use a timeVar, and make the Material declaration + initialization line we had @ simpleInitApp() into only the initialization, with the Material mat; going as a global variable, so we can access it on the simpleUpdate()! Like so:
</p>
<pre class="code java"><span class="kw1">protected</span> Material mat<span class="sy0">;</span></pre>

<p>
As global var, then the initialization cuts off the Material bit:
</p>
<pre class="code java">mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
And then the simpleUpdate()
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    timeVar <span class="sy0">+=</span> tpf<span class="sy0">;</span>
    <span class="kw1">if</span> <span class="br0">(</span>timeVar <span class="sy0">&gt;</span> <span class="nu0">1</span><span class="br0">)</span> <span class="br0">{</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">randomColor</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        timeVar<span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "Exercise 4" [4689-5375] -->
<h3 class="sectionedit7" id="exercise_5">Exercise 5</h3>
<div class="level3">

<p>
A possible solution is to change the rotation axis of player from y to x, and make it move along the z axis:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// make the player rotate</span>
    player.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">2</span><span class="sy0">*</span>tpf, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">move</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">2</span><span class="sy0">*</span>tpf<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
The above code should make the player roll towards the camera.
</p>

</div>
<!-- EDIT7 SECTION "Exercise 5" [5376-5723] -->
<h2 class="sectionedit8" id="hello_input">Hello Input</h2>
<div class="level2">

</div>
<!-- EDIT8 SECTION "Hello Input" [5724-5748] -->
<h3 class="sectionedit9" id="exercise_11">Exercise 1</h3>
<div class="level3">

<p>
First, add the mappings for the Up and Down actions to the initKeys() method:
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ...
    <span class="me1">inputManager</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Up"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_H</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Down"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_L</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    ...
    <span class="me1">inputManager</span>.<span class="me1">addListener</span><span class="br0">(</span>combinedListener, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="st0">"Left"</span>, <span class="st0">"Right"</span>, <span class="st0">"Up"</span>, <span class="st0">"Down"</span>, <span class="st0">"Rotate"</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Then implement the actions in the onAnalog() method:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>isRunning<span class="br0">)</span> <span class="br0">{</span>
        ...
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Up"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            Vector3f v <span class="sy0">=</span> player.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            player.<span class="me1">setLocalTranslation</span><span class="br0">(</span>v.<span class="me1">x</span>, v.<span class="me1">y</span> <span class="sy0">+</span> value <span class="sy0">*</span> speed, v.<span class="me1">z</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Down"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            Vector3f v <span class="sy0">=</span> player.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            player.<span class="me1">setLocalTranslation</span><span class="br0">(</span>v.<span class="me1">x</span>, v.<span class="me1">y</span> <span class="sy0">-</span> value <span class="sy0">*</span> speed, v.<span class="me1">z</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        ...
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
This should enable cube to move upwards, if the H key is pressed, and downwards, if the L key is pressed.
</p>

</div>
<!-- EDIT9 SECTION "Exercise 1" [5749-6805] -->
<h3 class="sectionedit10" id="exercise_21">Exercise 2</h3>
<div class="level3">

<p>
Following the proposed solution 1, add new mappings for the mouse wheel in the initKeys() method:
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ...
    <span class="me1">inputManager</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Up"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_H</span><span class="br0">)</span>,
                                  <span class="kw1">new</span> MouseAxisTrigger<span class="br0">(</span>MouseInput.<span class="me1">AXIS_WHEEL</span>, <span class="kw2">true</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Down"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_L</span><span class="br0">)</span>,
                                    <span class="kw1">new</span> MouseAxisTrigger<span class="br0">(</span>MouseInput.<span class="me1">AXIS_WHEEL</span>, <span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    ...
<span class="br0">}</span></pre>

<p>
Now you should be able to scroll the cube up or down with the mouse wheel.
</p>

</div>
<!-- EDIT10 SECTION "Exercise 2" [6806-7376] -->
<h3 class="sectionedit11" id="exercise_31">Exercise 3</h3>
<div class="level3">

<p>
When the controls are user-chosen.
</p>

</div>
<!-- EDIT11 SECTION "Exercise 3" [7377-7434] -->
<h2 class="sectionedit12" id="hello_picking">Hello Picking</h2>
<div class="level2">

</div>
<!-- EDIT12 SECTION "Hello Picking" [7435-7461] -->
<h3 class="sectionedit13" id="exercise_12">Exercise 1</h3>
<div class="level3">

<p>
You can jump right off and obtain the hit object's material, by acessing the “closest” object we previously acquired, obtain it's geometry through .getGeometry(), and then get the Geometry's material through .getMaterial(), like so: 
</p>
<pre class="code java">Material g <span class="sy0">=</span> closest.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
It's the same as going through the two steps hinted in the tips: <code>Geometry g = closest.getGeometry(); Material material = g.getMaterial();</code>
Finally, you need only add this line: <code>material.setColor(“Color”, ColorRGBA.randomColor())</code> , which will change the material from the hit object to a random color!
</p>

<p>
The lines can be added anywhere within the <code>if (results.size() &gt; 0)</code> block, after declaring the closest object. End result is as so:
</p>
<pre class="code java">Material material <span class="sy0">=</span> closest.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
material.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">randomColor</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT13 SECTION "Exercise 1" [7462-8365] -->
<h3 class="sectionedit14" id="exercise_22">Exercise 2</h3>
<div class="level3">

<p>
First of all, we need some light shed to make the model visible! Add a simple DirectionalLight like previously showed.
Then, declare a <code>Spatial golem</code> variable outside of methods. Then initialize golem to load his model: 
</p>
<pre class="code java">golem <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Oto/Oto.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now we need him to show up! So we need to attach him: but the rootNode won't do, because we're checking collision with it's child, the shootables node! So we attach it to shootables!
</p>
<pre class="code java">shootables.<span class="me1">attachChild</span><span class="br0">(</span>golem<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT14 SECTION "Exercise 2" [8366-8928] -->
<h3 class="sectionedit15" id="exercise_32">Exercise 3</h3>
<div class="level3">

<p>
Here is my code, it works and it is well commented.
</p>
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
<span class="kw1">import</span> <span class="co2">com.jme3.material.MatParam</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Ray</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Sphere</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.system.SystemListener</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> HelloPicking <span class="kw1">extends</span> SimpleApplication
<span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span>
    <span class="br0">{</span>
	HelloPicking app <span class="sy0">=</span> <span class="kw1">new</span> HelloPicking<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">private</span> Node shootables<span class="sy0">;</span>
    <span class="kw1">private</span> Node inventory<span class="sy0">;</span>
    <span class="kw1">private</span> Vector3f oldPosition<span class="sy0">;</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	initCrossHairs<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	initKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	shootables <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Shootables"</span><span class="br0">)</span><span class="sy0">;</span>
	inventory <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Inventory"</span><span class="br0">)</span><span class="sy0">;</span>
	guiNode.<span class="me1">attachChild</span><span class="br0">(</span>inventory<span class="br0">)</span><span class="sy0">;</span>
	<span class="co1">// add a light to the HUD so we can see the robot</span>
	DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="sy0">-</span>1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	guiNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
	rootNode.<span class="me1">attachChild</span><span class="br0">(</span>shootables<span class="br0">)</span><span class="sy0">;</span>
	shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"a Dragon"</span>, <span class="sy0">-</span>2f, 0f, 1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"a tin can"</span>, 1f, <span class="sy0">-</span>2f, 0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"the Sheriff"</span>, 0f, 1f, <span class="sy0">-</span>2f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCube<span class="br0">(</span><span class="st0">"the Deputy"</span>, 1f, 0f, <span class="sy0">-</span>4f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeFloor<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	shootables.<span class="me1">attachChild</span><span class="br0">(</span>makeCharacter<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	<span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span>
	<span class="br0">{</span>
	    <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Shoot"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span>
	    <span class="br0">{</span>
		<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>inventory.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">isEmpty</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>
		<span class="br0">{</span>
		    Spatial s1 <span class="sy0">=</span> inventory.<span class="me1">getChild</span><span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
		    <span class="co1">// scale back</span>
		    s1.<span class="me1">scale</span><span class="br0">(</span>.02f<span class="br0">)</span><span class="sy0">;</span>
		    s1.<span class="me1">setLocalTranslation</span><span class="br0">(</span>oldPosition<span class="br0">)</span><span class="sy0">;</span>
		    inventory.<span class="me1">detachAllChildren</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		    shootables.<span class="me1">attachChild</span><span class="br0">(</span>s1<span class="br0">)</span><span class="sy0">;</span>
		<span class="br0">}</span>
		<span class="kw1">else</span>
		<span class="br0">{</span>
		    CollisionResults results <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		    Ray ray <span class="sy0">=</span> <span class="kw1">new</span> Ray<span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span>, cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		    shootables.<span class="me1">collideWith</span><span class="br0">(</span>ray, results<span class="br0">)</span><span class="sy0">;</span>
 
		    <span class="kw1">if</span> <span class="br0">(</span>results.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span>
		    <span class="br0">{</span>
			CollisionResult closest <span class="sy0">=</span> results.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
			Spatial s <span class="sy0">=</span> closest.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
			<span class="co1">// we cheat Model differently with simple Geometry</span>
			<span class="co1">// s.parent is Oto-ogremesh when s is Oto_geom-1 and that is what we need</span>
			<span class="kw1">if</span> <span class="br0">(</span>s.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Oto-geom-1"</span><span class="br0">)</span><span class="br0">)</span>
			<span class="br0">{</span>
			    s <span class="sy0">=</span> s.<span class="me1">getParent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
			<span class="br0">}</span>
			<span class="co1">// It's important to get a clone or otherwise it will behave weird</span>
			oldPosition <span class="sy0">=</span> s.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
			shootables.<span class="me1">detachChild</span><span class="br0">(</span>s<span class="br0">)</span><span class="sy0">;</span>
			inventory.<span class="me1">attachChild</span><span class="br0">(</span>s<span class="br0">)</span><span class="sy0">;</span>
			<span class="co1">// make it bigger to see on the HUD</span>
			s.<span class="me1">scale</span><span class="br0">(</span>50f<span class="br0">)</span><span class="sy0">;</span>
			<span class="co1">// make it on the HUD center</span>
			s.<span class="me1">setLocalTranslation</span><span class="br0">(</span>settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span>, settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
		    <span class="br0">}</span>
		<span class="br0">}</span>
	    <span class="br0">}</span>
	<span class="br0">}</span>
    <span class="br0">}</span><span class="sy0">;</span>
 
    <span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Shoot"</span>,
				<span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span>,
				<span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Shoot"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">protected</span> Geometry makeCube<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> x, <span class="kw4">float</span> y, <span class="kw4">float</span> z<span class="br0">)</span>
    <span class="br0">{</span>
	<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
	Geometry cube <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>name, box<span class="br0">)</span><span class="sy0">;</span>
	cube.<span class="me1">setLocalTranslation</span><span class="br0">(</span>x, y, z<span class="br0">)</span><span class="sy0">;</span>
	Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
	mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">randomColor</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	cube.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
	<span class="kw1">return</span> cube<span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">protected</span> Geometry makeFloor<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">15</span>, .2f, <span class="nu0">15</span><span class="br0">)</span><span class="sy0">;</span>
	Geometry floor <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"the Floor"</span>, box<span class="br0">)</span><span class="sy0">;</span>
	floor.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">4</span>, <span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span><span class="sy0">;</span>
	Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
	mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Gray</span><span class="br0">)</span><span class="sy0">;</span>
	floor.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
	<span class="kw1">return</span> floor<span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">protected</span> <span class="kw4">void</span> initCrossHairs<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	setDisplayStatView<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
	guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
	BitmapText ch <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
	ch.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">*</span> <span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
	ch.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"+"</span><span class="br0">)</span><span class="sy0">;</span>
	ch.<span class="me1">setLocalTranslation</span><span class="br0">(</span>
		settings.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span> <span class="sy0">-</span> ch.<span class="me1">getLineWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span>, settings.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span> <span class="sy0">+</span> ch.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">2</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
	guiNode.<span class="me1">attachChild</span><span class="br0">(</span>ch<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">protected</span> Spatial makeCharacter<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
	Spatial golem <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Oto/Oto.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
	golem.<span class="me1">scale</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span>
	golem.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="sy0">-</span>1.0f, <span class="sy0">-</span>1.5f, <span class="sy0">-</span>0.6f<span class="br0">)</span><span class="sy0">;</span>
	<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"golem.locaoTranslation:"</span> <span class="sy0">+</span> golem.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="sy0">-</span>1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	golem.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
	<span class="kw1">return</span> golem<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT15 SECTION "Exercise 3" [8929-] -->
