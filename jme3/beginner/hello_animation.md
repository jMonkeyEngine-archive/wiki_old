---
title: jMonkeyEngine 3 Tutorial (7) - Hello Animation
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_7_-_hello_animation">jMonkeyEngine 3 Tutorial (7) - Hello Animation</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a>,
Next: <a href="/jme3/beginner/hello_picking.html" class="wikilink1" title="jme3:beginner:hello_picking">Hello Picking</a>
</p>

<p>
This tutorial shows how to add an animation controller and channels, and how to respond to user input by triggering an animation in a loaded model.
</p>

<p>
<a href="/resources/jme3-beginner-beginner-animation.png" class="media" title="jme3:beginner:beginner-animation.png"><img src="/resources/jme3-beginner-beginner-animation.png" class="mediacenter" alt="" /></a>
</p>

<p>
</p><p></p><div class="notetip">To use the example assets in a new jMonkeyEngine SDK project, right-click your project, select “Properties”, go to “Libraries”, press “Add Library” and add the “jme3-test-data” library.
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (7) - Hello Animation" [1-514] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimChannel</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimEventListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.animation.LoopMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 7 - how to load an OgreXML model and play an animation,
 * using channels, a controller, and an AnimEventListener. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloAnimation <span class="kw1">extends</span> SimpleApplication
  <span class="kw1">implements</span> AnimEventListener <span class="br0">{</span>
  <span class="kw1">private</span> AnimChannel channel<span class="sy0">;</span>
  <span class="kw1">private</span> AnimControl control<span class="sy0">;</span>
  Node player<span class="sy0">;</span>
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloAnimation app <span class="sy0">=</span> <span class="kw1">new</span> HelloAnimation<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">LightGray</span><span class="br0">)</span><span class="sy0">;</span>
    initKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    DirectionalLight dl <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    dl.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f, <span class="sy0">-</span>1f, <span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span>dl<span class="br0">)</span><span class="sy0">;</span>
    player <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Oto/Oto.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setLocalScale</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
    control <span class="sy0">=</span> player.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    control.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
    channel <span class="sy0">=</span> control.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"stand"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> onAnimCycleDone<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>animName.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"stand"</span>, 0.50f<span class="br0">)</span><span class="sy0">;</span>
      channel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">DontLoop</span><span class="br0">)</span><span class="sy0">;</span>
      channel.<span class="me1">setSpeed</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> onAnimChange<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// unused</span>
  <span class="br0">}</span>
 
  <span class="co3">/** Custom Keybinding: Map named actions to inputs. */</span>
  <span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Walk"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Walk"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>channel.<span class="me1">getAnimationName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Walk"</span>, 0.50f<span class="br0">)</span><span class="sy0">;</span>
          channel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">Loop</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "Sample Code" [515-2941] -->
<h2 class="sectionedit3" id="creating_and_loading_animated_models">Creating and Loading Animated Models</h2>
<div class="level2">

<p>
You create animated models with a tool such as Blender. Take some time and learn how to create your own models in these <a href="http://www.blender.org/education-help/tutorials/animation/" class="urlextern" title="http://www.blender.org/education-help/tutorials/animation/" rel="nofollow">Blender Animation Tutorials</a>. For now, download and use a free model, such as the one included here as an example (<a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Models/Oto/" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Models/Oto/" rel="nofollow">Oto Golem</a>, and <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Models/Ninja/" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Models/Ninja/" rel="nofollow">Ninja</a>).
</p>

<p>
Loading an animated model is pretty straight-forward, just as you have learned in the previous chapters. Animated Ogre models come as a set of files: The model is in <code>Oto.mesh.xml</code>, and the animation details are in <code>Oto.skeleton.xml</code>, plus the usual files for materials and textures. Check that all files of the model are together in the same <code>Model</code> subdirectory.
</p>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="coMULTI">/* Displaying the model requires a light source */</span>
    DirectionalLight dl <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    dl.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f, <span class="sy0">-</span>1f, <span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span>dl<span class="br0">)</span><span class="sy0">;</span>
    <span class="coMULTI">/* load and attach the model as usual */</span>
    player <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Oto/Oto.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setLocalScale</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// resize</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
    ...
    <span class="br0">}</span></pre>

<p>
Don't forget to add a light source to make the material visible.
</p>

</div>
<!-- EDIT3 SECTION "Creating and Loading Animated Models" [2942-4362] -->
<h2 class="sectionedit4" id="animation_controller_and_channel">Animation Controller and Channel</h2>
<div class="level2">

<p>
After you load the animated model, you register it to the Animation Controller.
</p>
<ul>
<li class="level1"><div class="li"> The controller object gives you access to the available animation sequences.</div>
</li>
<li class="level1"><div class="li"> The controller can have several channels, each channel can run one animation sequence at a time.</div>
</li>
<li class="level1"><div class="li"> To run several sequences, you create several channels, and set them each to their animation.</div>
</li>
</ul>
<pre class="code java">  <span class="kw1">private</span> AnimChannel channel<span class="sy0">;</span>
  <span class="kw1">private</span> AnimControl control<span class="sy0">;</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ...
    <span class="coMULTI">/* Load the animation controls, listen to animation events,
     * create an animation channel, and bring the model in its default position.  */</span>
    control <span class="sy0">=</span> player.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span> 
    control.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
    channel <span class="sy0">=</span> control.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"stand"</span><span class="br0">)</span><span class="sy0">;</span>
    ...</pre>

<p>
</p><p></p><div class="noteclassic">In response to a question about animations on different channels interefering with each other, <strong>Nehon on the jME forum <a href="http://jmonkeyengine.org/groups/general-2/forum/topic/helloanimation-animations-seem-to-be-clashing/#post-180994" class="urlextern" title="http://jmonkeyengine.org/groups/general-2/forum/topic/helloanimation-animations-seem-to-be-clashing/#post-180994" rel="nofollow">wrote</a>,</strong>


<p>
“You have to consider channels as part of the skeleton that are animated. The default behavior is to use the whole skeleton for a channel.
In your example the first channel plays the walk anim, then the second channel plays the dodge animation.
Arms and feet are probably not affected by the doge animation so you can see the walk anim for them, but the rest of the body plays the dodge animation.
</p>

<p>
Usually multiple channels are used to animate different part of the body. For example you create one channel for the lower part of the body and one for the upper part. This allow you to play a walk animation with the lower part and for example a shoot animation with the upper part. This way your character can walk while shooting.
</p>

<p>
In your case, where you want animations to chain for the whole skeleton, you just have to use one channel.”
</p></div>


<p>
</p><p></p><div class="noteclassic">

<pre class="code">control = player.getControl(AnimControl.class);</pre>

<p>
This line of code will return NULL if the AnimeControl is not in the main node of your model. To check this, right click your model and click “Edit in SceneComposer” You can then see the tree for the model. You can then move everything to the main node. You can also access a subnode with the following code.
</p>
<pre class="code">player.getChild("Subnode").getControl(AnimControl.class);</pre>

<p>

</p></div>


</div>
<!-- EDIT4 SECTION "Animation Controller and Channel" [4363-6763] -->
<h2 class="sectionedit5" id="responding_to_animation_events">Responding to Animation Events</h2>
<div class="level2">

<p>
Add <code>implements AnimEventListener</code> to the class declaration. This interface gives you access to events that notify you when a sequence is done, or when you change from one sequence to another, so you can respond to it. In this example, you reset the character to a standing position after a <code>Walk</code> cycle is done.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HelloAnimation <span class="kw1">extends</span> SimpleApplication
                         <span class="kw1">implements</span> AnimEventListener <span class="br0">{</span>
  ...
 
  <span class="kw1">public</span> <span class="kw4">void</span> onAnimCycleDone<span class="br0">(</span>AnimControl control, 
                              AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>animName.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"stand"</span>, 0.50f<span class="br0">)</span><span class="sy0">;</span>
      channel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">DontLoop</span><span class="br0">)</span><span class="sy0">;</span>
      channel.<span class="me1">setSpeed</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
  <span class="kw1">public</span> <span class="kw4">void</span> onAnimChange<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// unused</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "Responding to Animation Events" [6764-7651] -->
<h2 class="sectionedit6" id="trigger_animations_after_user_input">Trigger Animations After User Input</h2>
<div class="level2">

<p>
There are ambient animations like animals or trees that you may want to trigger in the main event loop. In other cases, animations are triggered by user interaction, such as key input. You want to play the Walk animation when the player presses a certain key (here the spacebar), at the same time as the avatar performs the walk action and changes its location.
</p>
<ol>
<li class="level1"><div class="li"> Initialize a new input controller (in <code>simpleInitApp()</code>).</div>
<ul>
<li class="level2"><div class="li"> Write the <code>initKey()</code> convenience method and call it from <code>simpleInitApp()</code>.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Add a key mapping with the name as the action you want to trigger.</div>
<ul>
<li class="level2"><div class="li"> Here for example, you map <code>Walk</code> to the Spacebar key.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Add an input listener for the <code>Walk</code> action.</div>
</li>
</ol>
<pre class="code java">  <span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Walk"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Walk"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

<p>
To use the input controller, you need to implement the actionListener by testing for each action by name, then set the channel to the corresponding animation to run.
</p>
<ul>
<li class="level1"><div class="li"> The second parameter of setAnim() is the blendTime (how long the current animation should overlap with the last one).</div>
</li>
<li class="level1"><div class="li"> LoopMode can be Loop (repeat), Cycle (forward then backward), and DontLoop (only once).</div>
</li>
<li class="level1"><div class="li"> If needed, use channel.setSpeed() to set the speed of this animation.</div>
</li>
<li class="level1"><div class="li"> Optionally, use channel.setTime() to Fast-forward or rewind to a certain moment in time of this animation.</div>
</li>
</ul>
<pre class="code java">  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>channel.<span class="me1">getAnimationName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
                channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Walk"</span>, 0.50f<span class="br0">)</span><span class="sy0">;</span>
                channel.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">Cycle</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT6 SECTION "Trigger Animations After User Input" [7652-9548] -->
<h2 class="sectionedit7" id="exercises">Exercises</h2>
<div class="level2">

</div>

<h4 id="exercise_1two_animations">Exercise 1: Two Animations</h4>
<div class="level4">

<p>
Make a mouse click trigger another animation sequence!
</p>
<ol>
<li class="level1"><div class="li"> Create a second channel in the controller</div>
</li>
<li class="level2"><div class="li"> Create a new key trigger mapping and action (see: <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">Hello Input</a>)</div>
</li>
<li class="level2"><div class="li"> Tip: Do you want to find out what animation sequences are available in the model? Use: <pre class="code java"><span class="kw1">for</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> anim <span class="sy0">:</span> control.<span class="me1">getAnimationNames</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>anim<span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span></pre>
</div>
</li>
</ol>

</div>

<h4 id="exercise_2revealing_the_skeleton_1">Exercise 2: Revealing the Skeleton (1)</h4>
<div class="level4">

<p>
Open the <code>skeleton.xml</code> file in a text editor of your choice. You don't have to be able to read or write these xml files (Blender does that for you) – but it is good to know how skeletons work. “There's no magic to it!”
</p>
<ul>
<li class="level1"><div class="li"> Note how the bones are numbered and named. All names of animated models follow a naming scheme.</div>
</li>
<li class="level1"><div class="li"> Note the bone hierarchy that specifies how the bones are connected.</div>
</li>
<li class="level1"><div class="li"> Note the list of animations: Each animation has a name, and several tracks. Each track tells individual bones how and when to transform. These animation steps are called keyframes.</div>
</li>
</ul>

</div>

<h4 id="exercise_3revealing_the_skeleton_2">Exercise 3: Revealing the Skeleton (2)</h4>
<div class="level4">

<p>
Add the following import statements for the SkeletonDebugger and Material classes:
</p>
<pre class="code java">     <span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.SkeletonDebugger</span><span class="sy0">;</span>
     <span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span></pre>

<p>
Add the following code snippet to <code>simpleInitApp()</code> to make the bones (that you just read about) visible!
</p>
<pre class="code java">     SkeletonDebugger skeletonDebug <span class="sy0">=</span> 
         <span class="kw1">new</span> SkeletonDebugger<span class="br0">(</span><span class="st0">"skeleton"</span>, control.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
     Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
     mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
     mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setDepthTest</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
     skeletonDebug.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
     player.<span class="me1">attachChild</span><span class="br0">(</span>skeletonDebug<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Can you identify individual bones in the skeleton?
</p>

</div>
<!-- EDIT7 SECTION "Exercises" [9549-11416] -->
<h2 class="sectionedit8" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
Now you can load animated models, identify stored animations, and trigger animations by using onAnimCycleDone() and onAnimChange(). You also learned that you can play several animations simultaneously, by starting each in a channel of its own. This could be useful if you ever want to animate the lower and upper part of the characters body independently, for example the legs run, while the arms use a weapon.
</p>

<p>
Now that your character can walk, wouldn't it be cool if it could also pick up things, or aim a weapon at things, or open doors? Time to reveal the secrets of <a href="/jme3/beginner/hello_picking.html" class="wikilink1" title="jme3:beginner:hello_picking">mouse picking</a>!
</p>
<hr />

<p>
See also: <a href="https://docs.google.com/leaf?id=0B9hhZie2D-fEYmRkMTYwN2YtMzQ0My00NTM4LThhOTYtZTk1MTRlYTNjYTc3&amp;hl=en" class="urlextern" title="https://docs.google.com/leaf?id=0B9hhZie2D-fEYmRkMTYwN2YtMzQ0My00NTM4LThhOTYtZTk1MTRlYTNjYTc3&amp;hl=en" rel="nofollow">Creating Animated OgreXML Models in Blender</a>
</p>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/animation.html" class="wikilink1" title="tag:animation" rel="tag">animation</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/keyinput.html" class="wikilink1" title="tag:keyinput" rel="tag">keyinput</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/model.html" class="wikilink1" title="tag:model" rel="tag">model</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Conclusion" [11417-] -->
