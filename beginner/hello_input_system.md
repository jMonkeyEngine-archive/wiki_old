---
title: jMonkeyEngine 3 Tutorial (5) - Hello Input System
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_5_-_hello_input_system">jMonkeyEngine 3 Tutorial (5) - Hello Input System</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_main_event_loop.html" class="wikilink1" title="jme3:beginner:hello_main_event_loop">Hello Update Loop</a>,
Next: <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a>
</p>

<p>
By default, SimpleApplication sets up a camera control that allows you to steer the camera with the WASD keys, the arrow keys, and the mouse. You can use it as a flying first-person camera right away. But what if you need a third-person camera, or you want keys to trigger special game actions? 
</p>

<p>
Every game has its custom keybindings, and this tutorial explains how you define them. We first define the key presses and mouse events, and then we define the actions they should trigger.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (5) - Hello Input System" [1-633] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.MouseInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.AnalogListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.MouseButtonTrigger</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 5 - how to map keys and mousebuttons to actions */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloInput <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloInput app <span class="sy0">=</span> <span class="kw1">new</span> HelloInput<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
  <span class="kw1">protected</span> Geometry player<span class="sy0">;</span>
  <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+boolean"><span class="kw3">Boolean</span></a> isRunning<span class="sy0">=</span><span class="kw2">true</span><span class="sy0">;</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    player <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Player"</span>, b<span class="br0">)</span><span class="sy0">;</span>
    Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
    initKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// load my custom keybinding</span>
  <span class="br0">}</span>
 
  <span class="co3">/** Custom Keybinding: Map named actions to inputs. */</span>
  <span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// You can map one or several inputs to one named action</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Pause"</span>,  <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_P</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Left"</span>,   <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_J</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Right"</span>,  <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_K</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Rotate"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span>,
                                      <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">// Add the names to the action listener.</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener,<span class="st0">"Pause"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>analogListener,<span class="st0">"Left"</span>, <span class="st0">"Right"</span>, <span class="st0">"Rotate"</span><span class="br0">)</span><span class="sy0">;</span>
 
  <span class="br0">}</span>
 
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Pause"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        isRunning <span class="sy0">=</span> <span class="sy0">!</span>isRunning<span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span>
 
  <span class="kw1">private</span> AnalogListener analogListener <span class="sy0">=</span> <span class="kw1">new</span> AnalogListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>isRunning<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Rotate"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          player.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, value<span class="sy0">*</span>speed, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Right"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          Vector3f v <span class="sy0">=</span> player.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          player.<span class="me1">setLocalTranslation</span><span class="br0">(</span>v.<span class="me1">x</span> <span class="sy0">+</span> value<span class="sy0">*</span>speed, v.<span class="me1">y</span>, v.<span class="me1">z</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Left"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          Vector3f v <span class="sy0">=</span> player.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          player.<span class="me1">setLocalTranslation</span><span class="br0">(</span>v.<span class="me1">x</span> <span class="sy0">-</span> value<span class="sy0">*</span>speed, v.<span class="me1">y</span>, v.<span class="me1">z</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Press P to unpause."</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Build and run the example.
</p>
<ul>
<li class="level1"><div class="li"> Press the Spacebar or click to rotate the cube. </div>
</li>
<li class="level1"><div class="li"> Press the J and K keys to move the cube.</div>
</li>
<li class="level1"><div class="li"> Press P to pause and unpause the game. While paused, the game should not respond to any input, other than <code>P</code>.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [634-3636] -->
<h2 class="sectionedit3" id="defining_mappings_and_triggers">Defining Mappings and Triggers</h2>
<div class="level2">

<p>
First you register each mapping name with its trigger(s). Remember the following:
</p>
<ul>
<li class="level1"><div class="li"> An input trigger can be a key press or mouse action. <br />
For example a mouse movement, a mouse click, or pressing the letter “P”.</div>
</li>
<li class="level1"><div class="li"> The mapping name is a string that you can choose. <br />
The name should describe the action (e.g. “Rotate”), and not the trigger. Because the trigger can change.</div>
</li>
<li class="level1"><div class="li"> One named mapping can have several triggers. <br />
For example, the “Rotate” action can be triggered by a click and by pressing the spacebar.</div>
</li>
</ul>

<p>
Have a look at the code:
</p>
<ol>
<li class="level1"><div class="li"> You register the mapping named “Rotate” to the Spacebar key trigger. <br />
<code>new KeyTrigger(KeyInput.KEY_SPACE)</code>). </div>
</li>
<li class="level1"><div class="li"> In the same line, you also register “Rotate” to an alternative mouse click trigger. <br />
<code>new MouseButtonTrigger(MouseInput.BUTTON_LEFT)</code></div>
</li>
<li class="level1"><div class="li"> You map the <code>Pause</code>, <code>Left</code>, <code>Right</code> mappings to the P, J, K keys, respectively. </div>
</li>
</ol>
<pre class="code java">    <span class="co1">// You can map one or several inputs to one named action</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Pause"</span>,  <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_P</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Left"</span>,   <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_J</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Right"</span>,  <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_K</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Rotate"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span>,
                                      <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now you need to register your trigger mappings.
</p>
<ol>
<li class="level1"><div class="li"> You register the pause action to the ActionListener, because it is an “on/off” action.</div>
</li>
<li class="level1"><div class="li"> You register the movement actions to the AnalogListener, because they are gradual actions.</div>
</li>
</ol>
<pre class="code java">    <span class="co1">// Add the names to the action listener.</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener,<span class="st0">"Pause"</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>analogListener,<span class="st0">"Left"</span>, <span class="st0">"Right"</span>, <span class="st0">"Rotate"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This code goes into the <code>simpleInitApp()</code> method. But since we will likely add many keybindings, we extract these lines and wrap them in an auxiliary method, <code>initKeys()</code>. The <code>initKeys()</code> method is not part of the Input Controls interface – you can name it whatever you like. Just don't forget to call your method from the <code>initSimpleApp()</code> method.
</p>

</div>
<!-- EDIT3 SECTION "Defining Mappings and Triggers" [3637-5820] -->
<h2 class="sectionedit4" id="implementing_the_actions">Implementing the Actions</h2>
<div class="level2">

<p>
You have mapped action names to input triggers. Now you specify the actions themselves.
</p>

<p>
The two important methods here are the <code>ActionListener</code> with its <code>onAction()</code> method, and the <code>AnalogListener</code> with its <code>onAnalog()</code> method. In these two methods, you test for each named mapping, and call the game action you want to trigger. 
</p>

<p>
In this example, we trigger the following actions: 
</p>
<ol>
<li class="level1"><div class="li"> The <em>Rotate</em> mapping triggers the action <code>player.rotate(0, value, 0)</code>. </div>
</li>
<li class="level1"><div class="li"> The <em>Left</em> and <em>Right</em> mappings increase and decrease the player's x coordinate. </div>
</li>
<li class="level1"><div class="li"> The <em>Pause</em> mapping flips a boolean <code>isRunning</code>. </div>
</li>
<li class="level1"><div class="li"> We also want to check the boolean <code>isRunning</code> before any action (other than unpausing) is executed.</div>
</li>
</ol>
<pre class="code java">  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Pause"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        isRunning <span class="sy0">=</span> <span class="sy0">!</span>isRunning<span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span>
 
  <span class="kw1">private</span> AnalogListener analogListener <span class="sy0">=</span> <span class="kw1">new</span> AnalogListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>isRunning<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Rotate"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          player.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, value<span class="sy0">*</span>speed, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Right"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          Vector3f v <span class="sy0">=</span> player.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          player.<span class="me1">setLocalTranslation</span><span class="br0">(</span>v.<span class="me1">x</span> <span class="sy0">+</span> value<span class="sy0">*</span>speed, v.<span class="me1">y</span>, v.<span class="me1">z</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Left"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          Vector3f v <span class="sy0">=</span> player.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          player.<span class="me1">setLocalTranslation</span><span class="br0">(</span>v.<span class="me1">x</span> <span class="sy0">-</span> value<span class="sy0">*</span>speed, v.<span class="me1">y</span>, v.<span class="me1">z</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Press P to unpause."</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

<p>
You can also combine both listeners into one, the engine will send the appropriate events to each method (onAction or onAnalog). For example:
</p>
<pre class="code java">  <span class="kw1">private</span> MyCombinedListener combinedListener <span class="sy0">=</span> <span class="kw1">new</span> MyCombinedListener<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
  <span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">class</span> MyCombinedListener <span class="kw1">implements</span> AnalogListener, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Pause"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        isRunning <span class="sy0">=</span> <span class="sy0">!</span>isRunning<span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>isRunning<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Rotate"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          player.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, value<span class="sy0">*</span>speed, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Right"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          Vector3f v <span class="sy0">=</span> player.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          player.<span class="me1">setLocalTranslation</span><span class="br0">(</span>v.<span class="me1">x</span> <span class="sy0">+</span> value<span class="sy0">*</span>speed, v.<span class="me1">y</span>, v.<span class="me1">z</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Left"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          Vector3f v <span class="sy0">=</span> player.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
          player.<span class="me1">setLocalTranslation</span><span class="br0">(</span>v.<span class="me1">x</span> <span class="sy0">-</span> value<span class="sy0">*</span>speed, v.<span class="me1">y</span>, v.<span class="me1">z</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Press P to unpause."</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
<span class="co1">// ...</span>
inputManager.<span class="me1">addListener</span><span class="br0">(</span>combinedListener, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="st0">"Pause"</span>, <span class="st0">"Left"</span>, <span class="st0">"Right"</span>, <span class="st0">"Rotate"</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 </pre>

<p>
It's okay to use only one of the two Listeners, and not implement the other one, if you are not using this type of interaction. In the following, we have a closer look how to decide which of the two listeners is best suited for which situation.
</p>

</div>
<!-- EDIT4 SECTION "Implementing the Actions" [5821-8939] -->
<h2 class="sectionedit5" id="analog_pressed_or_released">Analog, Pressed, or Released?</h2>
<div class="level2">

<p>
Technically, every input can be either an “analog” or a “digital” action. Here is how you find out which listener is the right one for which type of input.
</p>

<p>
Mappings registered to the <strong>AnalogListener</strong> are triggered repeatedly and gradually.
</p>
<ul>
<li class="level1"><div class="li"> Parameters: </div>
<ol>
<li class="level2"><div class="li"> JME gives you access to the name of the triggered action.</div>
</li>
<li class="level2"><div class="li"> JME gives you access to a gradual value showing the strength of that input. In the case of a keypress that will be the tpf value for which it was pressed since the last frame. For other inputs such as a joystick which give analogue control though then the value will also indicate the strength of the input premultiplied by tpf. For an example on this go to <a href="/jme3/beginner/hello_input_system/timekeypressed.html" class="wikilink1" title="jme3:beginner:hello_input_system:timekeypressed">jMonkeyEngine 3 Tutorial (5) - Hello Input System - Variation over time key is pressed</a></div>
</li>
</ol>
</li>
</ul>

<p>
In order to see the total time that a key has been pressed for then the incoming value can be accumulated. The analogue listener may also need to be combined with an action listener so that you are notified when the key is released.
</p>
<ul>
<li class="level1"><div class="li"> Example: Navigational events (e.g. Left, Right, Rotate, Run, Strafe), situations where you interact continuously. </div>
</li>
</ul>

<p>
Mappings registered to the <strong>ActionListener</strong> are digital either-or actions – “Pressed or released? On or off?”
</p>
<ul>
<li class="level1"><div class="li"> Parameters: </div>
<ol>
<li class="level2"><div class="li"> JME gives you access to the name of the triggered action.</div>
</li>
<li class="level2"><div class="li"> JME gives you access to a boolean whether the key is pressed or not.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Example: Pause button, shooting, selecting, jumping, one-time click interactions.</div>
</li>
</ul>

<p>
<strong>Tip:</strong> It's very common that you want an action to be only triggered once, in the moment when the key is <em>released</em>. For instance when opening a door, flipping a boolean state, or picking up an item. To achieve that, you use an <code>ActionListener</code> and test for <code>… &amp;&amp; !keyPressed</code>. For an example, look at the Pause button code:
</p>
<pre class="code java">      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Pause"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        isRunning <span class="sy0">=</span> <span class="sy0">!</span>isRunning<span class="sy0">;</span>
      <span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "Analog, Pressed, or Released?" [8940-10964] -->
<h2 class="sectionedit6" id="table_of_triggers">Table of Triggers</h2>
<div class="level2">

<p>
You can find the list of input constants in the files <code>src/core/com/jme3/input/KeyInput.java</code>, <code>JoyInput.java</code>, and <code>MouseInput.java</code>. Here is an overview of the most common triggers constants:
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Trigger </th><th class="col1"> Code </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Mouse button: Left Click </td><td class="col1"> MouseButtonTrigger(MouseInput.BUTTON_LEFT) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Mouse button: Right Click </td><td class="col1"> MouseButtonTrigger(MouseInput.BUTTON_RIGHT) </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Keyboard: Characters and Numbers </td><td class="col1"> KeyTrigger(KeyInput.KEY_X) </td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> Keyboard: Spacebar  </td><td class="col1"> KeyTrigger(KeyInput.KEY_SPACE) </td>
	</tr>
	<tr class="row5">
		<td class="col0"> Keyboard: Return, Enter </td><td class="col1 leftalign"> KeyTrigger(KeyInput.KEY_RETURN), KeyTrigger(KeyInput.KEY_NUMPADENTER)  </td>
	</tr>
	<tr class="row6">
		<td class="col0"> Keyboard: Escape </td><td class="col1"> KeyTrigger(KeyInput.KEY_ESCAPE) </td>
	</tr>
	<tr class="row7">
		<td class="col0"> Keyboard: Arrows </td><td class="col1"> KeyTrigger(KeyInput.KEY_UP), KeyTrigger(KeyInput.KEY_DOWN) <br />
KeyTrigger(KeyInput.KEY_LEFT), KeyTrigger(KeyInput.KEY_RIGHT) </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [11197-11793] -->
<p>
<strong>Tip:</strong> If you don't recall an input constant during development, you benefit from an IDE's code completion functionality: Place the caret after e.g. <code>KeyInput.|</code> and trigger code completion to select possible input identifiers.
</p>

</div>
<!-- EDIT6 SECTION "Table of Triggers" [10965-12027] -->
<h2 class="sectionedit8" id="exercises">Exercises</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Add mappings for moving the player (box) up and down with the H and L keys!</div>
</li>
<li class="level1"><div class="li"> Switch off the flyCam and override the WASD keys.</div>
<ul>
<li class="level2"><div class="li"> Tip: Use <a href="/jme3/faq.html" class="wikilink1" title="jme3:faq">flyCam.setEnabled(false);</a> </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Modify the mappings so that you can also trigger the up an down motion with the mouse scroll wheel!</div>
<ul>
<li class="level2"><div class="li"> Tip: Use <code>new MouseAxisTrigger(MouseInput.AXIS_WHEEL, true)</code></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In which situation would it be better to use variables instead of literals for the MouseInput/KeyInput definitions? <pre class="code java"><span class="kw4">int</span> usersPauseKey <span class="sy0">=</span> KeyInput.<span class="me1">KEY_P</span><span class="sy0">;</span> 
...
<span class="me1">inputManager</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Pause"</span>,  <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>usersPauseKey<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
</p><p></p><div class="noteimportant">Link to user-proposed solutions: <a href="http://jmonkeyengine.org/wiki/doku.php/jm3:solutions" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jm3:solutions" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jm3:solutions</a>
<em class="u">Be sure to try to solve them for yourself first!</em>
</div>


</div>
<!-- EDIT8 SECTION "Exercises" [12028-12891] -->
<h2 class="sectionedit9" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You are now able to add custom interactions to your game: You know that you first have to define the key mappings, and then the actions for each mapping. You have learned to respond to mouse events and to the keyboard. You understand the difference between “analog” (gradually repeated) and “digital” (on/off) inputs.
</p>

<p>
Now you can already write a little interactive game! But wouldn't it be cooler if these old boxes were a bit more fancy? Let's continue with learning about <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">materials</a>.
</p>
<div class="tags"><span>
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/keyinput.html" class="wikilink1" title="tag:keyinput" rel="tag">keyinput</a>,
	<a href="/tag/click.html" class="wikilink1" title="tag:click" rel="tag">click</a>
</span></div>

</div>
<!-- EDIT9 SECTION "Conclusion" [12892-] -->
