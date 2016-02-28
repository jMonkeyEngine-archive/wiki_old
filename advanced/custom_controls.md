---
title: Custom Controls
---
<h1 class="sectionedit1" id="custom_controls">Custom Controls</h1>
<div class="level1">

<p>
A <code>com.jme3.scene.control.Control</code> is a customizable jME3 interface that allows you to cleanly steer the behaviour of game entities (Spatials), such as artificially intelligent behaviour in NPCs, traps, automatic alarms and doors, animals and pets, self-steering vehicles or platforms – anything that moves and interacts. Several instances of custom Controls together implement the behaviours of a type of Spatial. 
</p>

<p>
To control global game behaviour see <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a> – you often use AppStates and Control together.
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=MNDiZ9YHIpM" class="urlextern" title="http://www.youtube.com/watch?v=MNDiZ9YHIpM" rel="nofollow">Quick video introduction to Custom Controls</a></div>
</li>
</ul>

<p>
To control the behaviour of spatials:
</p>
<ol>
<li class="level1"><div class="li"> Create one control for each <em>type of behavior</em>. When you add several controls to one spatial, they will be executed in the order they were added. <br />
For example, one NPC can be controlled by a PhysicsControl instance and an AIControl instance.</div>
</li>
<li class="level1"><div class="li"> Define the custom control and implement its behaviour in the Control's update method:</div>
<ul>
<li class="level2"><div class="li"> You can pass arguments into your custom control.</div>
</li>
<li class="level2"><div class="li"> In the control class, the object <code>spatial</code> gives you access to the spatial and subspatials that the control is attached to.</div>
</li>
<li class="level2"><div class="li"> Here you modify the <code>spatial</code>'s transformation (move, scale, rotate), play animations, check its environement, define how it acts and reacts. </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Add an instance of the Control to a spatial to give it this behavior. The spatial's game state is updated automatically from now on. <pre class="code java">spatial.<span class="me1">addControl</span><span class="br0">(</span>myControl<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
To implement game logic for a type of spatial, you will either extend AbstractControl (most common case), or implement the Control interface, as explained in this article.
</p>

</div>
<!-- EDIT1 SECTION "Custom Controls" [1-1746] -->
<h2 class="sectionedit2" id="usage">Usage</h2>
<div class="level2">

<p>
Use <span class="curid"><a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Controls</a></span> to implement the <em>behaviour of types of game entities</em>.
</p>
<ul>
<li class="level1"><div class="li"> Use Controls to add a type of behaviour (that is, methods and fields) to individual Spatials. </div>
</li>
<li class="level1"><div class="li"> Each Control has its own <code>update()</code> loop that hooks into <code>simpleUpdate()</code>. Use Controls to move blocks of code out of the <code>simpleUpdate()</code> loop.</div>
</li>
<li class="level1"><div class="li"> One Spatial can be influenced by several Controls. (Very powerful and modular!) </div>
</li>
<li class="level1"><div class="li"> Each Spatial needs its own instance of the Control. </div>
</li>
<li class="level1"><div class="li"> A Control only has access to and control over the Spatial it is attached to.</div>
</li>
<li class="level1"><div class="li"> Controls can be saved as .j3o file together with a Spatial. </div>
</li>
</ul>

<p>
Examples: You can write
</p>
<ul>
<li class="level1"><div class="li"> A WalkerNavControl, SwimmerNavControl, FlyerNavControl… that defines how a type of NPC finds their way around. All NPCs can walk, some can fly, others can swim, and some can all three, etc.</div>
</li>
<li class="level1"><div class="li"> A PlayerNavControl that is steered by user-configurable keyboard and mouse input.</div>
</li>
<li class="level1"><div class="li"> A generic animation control that acts as a common interface that triggers animations (walk, stand, attack, defend) for various entities.</div>
</li>
<li class="level1"><div class="li"> A DefensiveBehaviourControl that remote-controls NPC behaviour in fight situations. </div>
</li>
<li class="level1"><div class="li"> An IdleBehaviourControl that remote-controls NPC behaviour in neutral situations. </div>
</li>
<li class="level1"><div class="li"> A DestructionControl that automatically replaces a structure with an appropriate piece of debris after collision with a projectile… </div>
</li>
</ul>

<p>
The possibilities are endless. <img src="/lib/images/smileys/icon_smile.gif" class="icon" alt=":-)" />
</p>

</div>
<!-- EDIT2 SECTION "Usage" [1747-3214] -->
<h2 class="sectionedit3" id="example_code">Example Code</h2>
<div class="level2">

<p>
Other examples include the built-in RigidBodyControl in JME's physics integration, the built-in TerrainLODControl that updates the terrain's level of detail depending on the viewer's perspective, etc.
</p>

<p>
Existing examples in the code base include:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/animation/AnimControl.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/animation/AnimControl.java" rel="nofollow">AnimControl.java</a> allows manipulation of skeletal animation, including blending and multiple channels.</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/scene/control/CameraControl.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/scene/control/CameraControl.java" rel="nofollow">CameraControl.java</a> allows you to sync the camera position with the position of a given spatial.</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/scene/control/BillboardControl.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/scene/control/BillboardControl.java" rel="nofollow">BillboardControl.java</a> displays a flat picture orthogonally, e.g. a speech bubble or informational dialog.</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/#src%2Fjbullet%2Fcom%2Fjme3%2Fbullet%2Fcontrol" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/#src%2Fjbullet%2Fcom%2Fjme3%2Fbullet%2Fcontrol" rel="nofollow">PhysicsControl</a> subclasses (such as CharacterControl, RigidBodyControl, VehicleControl) allow you to add physical properties to any spatial. PhysicsControls tie into capabilities provided by the BulletAppState.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Example Code" [3215-4499] -->
<h2 class="sectionedit4" id="abstractcontrol_class">AbstractControl Class</h2>
<div class="level2">

<p>
</p><p></p><div class="notetip">The most common way to create a Control is to create a class that extends AbstractControl.
</div>


<p>
The AbstractControl can be found under <code>com.jme3.scene.control.AbstractControl</code>. This is a default abstract class that implements the Control interface.
</p>
<ul>
<li class="level1"><div class="li"> You have access to a boolean <code>isEnabled()</code>.</div>
</li>
<li class="level1"><div class="li"> You have access to the Spatial object <code>spatial</code>. </div>
</li>
<li class="level1"><div class="li"> You override the <code>controlUpdate()</code> method to implement the Spatial's behaviour. </div>
</li>
<li class="level1"><div class="li"> You have access to a <code>setEnabled(boolean)</code> method. This activates or deactivates this Control's behaviour in this spatial temporarily. While the AbstractControl is toggled to be disabled, the <code>controlUpdate()</code> loop is no longer executed. <br />
For example, you disable your IdleBehaviourControl when you enable your DefensiveBehaviourControl in a spatial.</div>
</li>
</ul>

<p>
Usage: Your custom subclass implements the three methods <code>controlUpdate()</code>, <code>controlRender()</code>, <code>setSpatial()</code>, and <code>cloneForSpatial()</code> as shown here:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyControl <span class="kw1">extends</span> AbstractControl <span class="kw1">implements</span> Savable, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+cloneable"><span class="kw3">Cloneable</span></a> <span class="br0">{</span>
  <span class="kw1">private</span> <span class="kw4">int</span> index<span class="sy0">;</span> <span class="co1">// can have custom fields -- example </span>
 
  <span class="kw1">public</span> MyControl<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span><span class="br0">}</span> <span class="co1">// empty serialization constructor</span>
 
  <span class="co3">/** Optional custom constructor with arguments that can init custom fields.
    * Note: you cannot modify the spatial here yet! */</span>
  <span class="kw1">public</span> MyControl<span class="br0">(</span><span class="kw4">int</span> i<span class="br0">)</span><span class="br0">{</span> 
    <span class="co1">// index=i; // example </span>
  <span class="br0">}</span> 
 
  <span class="co3">/** This method is called when the control is added to the spatial,
    * and when the control is removed from the spatial (setting a null value).
    * It can be used for both initialization and cleanup. */</span>    
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> setSpatial<span class="br0">(</span>Spatial spatial<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">super</span>.<span class="me1">setSpatial</span><span class="br0">(</span>spatial<span class="br0">)</span><span class="sy0">;</span>
    <span class="coMULTI">/* Example:
    if (spatial != null){
        // initialize
    }else{
        // cleanup
    }
    */</span>
  <span class="br0">}</span>
 
 
  <span class="co3">/** Implement your spatial's behaviour here.
    * From here you can modify the scene graph and the spatial
    * (transform them, get and set userdata, etc).
    * This loop controls the spatial while the Control is enabled. */</span>
  @Override
  <span class="kw1">protected</span> <span class="kw4">void</span> controlUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
    <span class="kw1">if</span><span class="br0">(</span>spatial <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// spatial.rotate(tpf,tpf,tpf); // example behaviour</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+control"><span class="kw3">Control</span></a> cloneForSpatial<span class="br0">(</span>Spatial spatial<span class="br0">)</span><span class="br0">{</span>
    <span class="kw1">final</span> MyControl control <span class="sy0">=</span> <span class="kw1">new</span> MyControl<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="coMULTI">/* Optional: use setters to copy userdata into the cloned control */</span>
    <span class="co1">// control.setIndex(i); // example</span>
    control.<span class="me1">setSpatial</span><span class="br0">(</span>spatial<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span> control<span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">protected</span> <span class="kw4">void</span> controlRender<span class="br0">(</span>RenderManager rm, ViewPort vp<span class="br0">)</span><span class="br0">{</span>
     <span class="coMULTI">/* Optional: rendering manipulation (for advanced users) */</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> read<span class="br0">(</span>JmeImporter im<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
      <span class="kw1">super</span>.<span class="me1">read</span><span class="br0">(</span>im<span class="br0">)</span><span class="sy0">;</span>
      <span class="co1">// im.getCapsule(this).read(...);</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> write<span class="br0">(</span>JmeExporter ex<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
      <span class="kw1">super</span>.<span class="me1">write</span><span class="br0">(</span>ex<span class="br0">)</span><span class="sy0">;</span>
      <span class="co1">// ex.getCapsule(this).write(...);</span>
  <span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> To learn more about <code>write()</code> and <code>read()</code>, see <a href="/jme3/advanced/save_and_load.html" class="wikilink1" title="jme3:advanced:save_and_load">Save and Load</a></div>
</li>
<li class="level1"><div class="li"> To learn more about <code>setUserData()</code>, see <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a>.</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "AbstractControl Class" [4500-7583] -->
<h2 class="sectionedit5" id="the_control_interface">The Control Interface</h2>
<div class="level2">

<p>
</p><p></p><div class="notetip">In the less common case that you want to create a Control that also extends another class, create a custom interface that  extends jME3's Control interface. Your class can become a Control by implementing the Control interface, and at the same time extending another class.
</div>


<p>
The Control interface can be found under <code>com.jme3.scene.control.Control</code>. It has the following method signatures:
</p>
<ul>
<li class="level1"><div class="li"> <code>cloneForSpatial(Spatial)</code>: Clones the Control and attaches it to a clone of the given Spatial. <br />
Implement this method to be able to <a href="/jme3/advanced/save_and_load.html" class="wikilink1" title="jme3:advanced:save_and_load">save() and load()</a> Spatials carrying this Control. <br />
The AssetManager also uses this method if the same spatial is loaded twice. You can specify which fields you want your object to reuse (e.g. collisionshapes) in this case. </div>
</li>
<li class="level1"><div class="li"> <code>setEnabled(boolean)</code>: Toggles a boolean that enables or disables the Control. Goes with accessor <code>isEnabled();</code>. You test for it in the <code>update(float tpf)</code> loop before you execute anything.</div>
</li>
<li class="level1"><div class="li"> There are also some internal methods that you do not call from user code: <code>setSpatial(Spatial s)</code>, <code>update(float tpf);</code>, <code>render(RenderManager rm, ViewPort vp)</code>.</div>
</li>
</ul>

<p>
Usage example:
1. Create a custom control interface
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">interface</span> MyControlInterface <span class="kw1">extends</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+control"><span class="kw3">Control</span></a> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> setSomething<span class="br0">(</span><span class="kw4">int</span> x<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// optionally, add custom methods</span>
<span class="br0">}</span></pre>

<p>
2. Create custom Controls implementing your Control interface.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyControl <span class="kw1">extends</span> MyCustomClass <span class="kw1">implements</span> MyControlInterface <span class="br0">{</span>
 
    <span class="kw1">protected</span> Spatial spatial<span class="sy0">;</span>
 
    <span class="kw1">protected</span> <span class="kw4">boolean</span> enabled <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
 
    <span class="kw1">public</span> MyControl<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> <span class="br0">}</span> <span class="co1">// empty serialization constructor</span>
 
    <span class="kw1">public</span> MyControl<span class="br0">(</span><span class="kw4">int</span> x<span class="br0">)</span> <span class="br0">{</span> <span class="co1">// custom constructor</span>
        <span class="kw1">super</span><span class="br0">(</span>x<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>enabled <span class="sy0">&amp;&amp;</span> spatial <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="co1">// Write custom code to control the spatial here!</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> render<span class="br0">(</span>RenderManager rm, ViewPort vp<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// optional for advanced users, e.g. to display a debug shape</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+control"><span class="kw3">Control</span></a> cloneForSpatial<span class="br0">(</span>Spatial spatial<span class="br0">)</span> <span class="br0">{</span>
        MyControl control <span class="sy0">=</span> <span class="kw1">new</span> MyControl<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// set custom properties</span>
        control.<span class="me1">setSpatial</span><span class="br0">(</span>spatial<span class="br0">)</span><span class="sy0">;</span>
        control.<span class="me1">setEnabled</span><span class="br0">(</span>isEnabled<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> 
        <span class="co1">// set some more properties here...</span>
        <span class="kw1">return</span> control<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> setEnabled<span class="br0">(</span><span class="kw4">boolean</span> enabled<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">enabled</span> <span class="sy0">=</span> enabled<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">boolean</span> isEnabled<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> enabled<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> setSomething<span class="br0">(</span><span class="kw4">int</span> z<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// You can add custom methods ...</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> write<span class="br0">(</span>JmeExporter ex<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">write</span><span class="br0">(</span>ex<span class="br0">)</span><span class="sy0">;</span>
        OutputCapsule oc <span class="sy0">=</span> ex.<span class="me1">getCapsule</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
        oc.<span class="me1">write</span><span class="br0">(</span>enabled, <span class="st0">"enabled"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        oc.<span class="me1">write</span><span class="br0">(</span>spatial, <span class="st0">"spatial"</span>, <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// write custom variables ....</span>
    <span class="br0">}</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> read<span class="br0">(</span>JmeImporter im<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">read</span><span class="br0">(</span>im<span class="br0">)</span><span class="sy0">;</span>
        InputCapsule ic <span class="sy0">=</span> im.<span class="me1">getCapsule</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
        enabled <span class="sy0">=</span> ic.<span class="me1">readBoolean</span><span class="br0">(</span><span class="st0">"enabled"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        spatial <span class="sy0">=</span> <span class="br0">(</span>Spatial<span class="br0">)</span> ic.<span class="me1">readSavable</span><span class="br0">(</span><span class="st0">"spatial"</span>, <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// read custom variables ....</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "The Control Interface" [7584-10841] -->
<h2 class="sectionedit6" id="best_practices">Best Practices</h2>
<div class="level2">

<p>
<strong>Tip:</strong> Use the getControl() accessor to get Control objects from Spatials. No need to pass around lots of object references.
Here an example from the <a href="http://code.google.com/p/monkeyzone/" class="urlextern" title="http://code.google.com/p/monkeyzone/" rel="nofollow">MonkeyZone</a> code:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> CharacterAnimControl <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+control"><span class="kw3">Control</span></a> <span class="br0">{</span>
  ...
  <span class="kw1">public</span> <span class="kw4">void</span> setSpatial<span class="br0">(</span>Spatial spatial<span class="br0">)</span> <span class="br0">{</span>
    ...
    <span class="me1">animControl</span>      <span class="sy0">=</span> spatial.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    characterControl <span class="sy0">=</span> spatial.<span class="me1">getControl</span><span class="br0">(</span>CharacterControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    ...
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
<strong>Tip:</strong> You can create custom Control interfaces so a set of different Controls provide the same methods and can be accessed with the interface class type.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">interface</span> ManualControl <span class="kw1">extends</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+control"><span class="kw3">Control</span></a> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> steerX<span class="br0">(</span><span class="kw4">float</span> value<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw4">void</span> steerY<span class="br0">(</span><span class="kw4">float</span> value<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw4">void</span> moveX<span class="br0">(</span><span class="kw4">float</span> value<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw4">void</span> moveY<span class="br0">(</span><span class="kw4">float</span> value<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">public</span> <span class="kw4">void</span> moveZ<span class="br0">(</span><span class="kw4">float</span> value<span class="br0">)</span><span class="sy0">;</span>
   ...
<span class="br0">}</span></pre>

<p>
Then you create custom sub-Controls and implement the methods accordingly to the context:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> ManualVehicleControl   <span class="kw1">extends</span> ManualControl <span class="br0">{</span>...<span class="br0">}</span></pre>

<p>
 and
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> ManualCharacterControl <span class="kw1">extends</span> ManualControl <span class="br0">{</span>...<span class="br0">}</span></pre>

<p>
Then add the appropriate controls to spatials:
</p>
<pre class="code java">characterSpatial.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> ManualCharacterControl<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">vehicleSpatial</span>.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">new</span> ManualVehicleControl<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
...</pre>

<p>
<strong>Tip:</strong> Use the getControl() method on a Spatial to get a specific Control object, and activate its behaviour!
</p>
<pre class="code java">ManualControl c <span class="sy0">=</span> mySpatial.<span class="me1">getControl</span><span class="br0">(</span>ManualControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
c.<span class="me1">steerX</span><span class="br0">(</span>steerX<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT6 SECTION "Best Practices" [10842-] -->
