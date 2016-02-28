---
title: Animation in jME3
---
<h1 class="sectionedit1" id="animation_in_jme3">Animation in jME3</h1>
<div class="level1">

<p>
In 3D games, you do not only load static 3D models, you also want to be able to trigger animations in the model from the Java code. 
</p>

</div>
<!-- EDIT1 SECTION "Animation in jME3" [1-167] -->
<h2 class="sectionedit2" id="requirements">Requirements</h2>
<div class="level2">

<p>
JME3 only loads and plays animated models, it does not create them. 
</p>

<p>
What is required for an animated model? (<a href="/jme3/terminology.html" class="wikilink1" title="jme3:terminology">See also: Animation terminology</a>)
</p>
<ol>
<li class="level1"><div class="li"> For each model, you have to segment the model into a skeleton (<strong>bone rigging</strong>). </div>
</li>
<li class="level1"><div class="li"> For each motion, you have to specify how the animation distorts parts of the model (<strong>skinning</strong>).  </div>
</li>
<li class="level1"><div class="li"> For each animation, you have to specify a series of snapshots of how the bones are positioned (<strong>keyframes</strong>).</div>
</li>
<li class="level1"><div class="li"> One model can contain several animations. You give every animation a name when you save it in the mesh editor.</div>
</li>
</ol>

<p>
Unless you download free models, or buy them from a 3D artist, you must create your animated models in an <strong>external mesh editor</strong> (for example, Blender) yourself.
</p>
<ul>
<li class="level1"><div class="li"> <a href="/sdk/blender.html" class="wikilink1" title="sdk:blender">Converting Blender Models to JME3 (.J3o files)</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/user/aramakara" class="urlextern" title="http://www.youtube.com/user/aramakara" rel="nofollow">Video Series: Creating models in Blender, OgreMax, 3dsMax</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=NdjC9sCRV0s" class="urlextern" title="http://www.youtube.com/watch?v=NdjC9sCRV0s" rel="nofollow">Video: Creating and Exporting OgreXML Animations from Blender 2.61 to JME3 </a></div>
</li>
<li class="level1"><div class="li"> <a href="https://docs.google.com/fileview?id=0B9hhZie2D-fENDBlZDU5MzgtNzlkYi00YmQzLTliNTQtNzZhYTJhYjEzNWNk&amp;hl=en" class="urlextern" title="https://docs.google.com/fileview?id=0B9hhZie2D-fENDBlZDU5MzgtNzlkYi00YmQzLTliNTQtNzZhYTJhYjEzNWNk&amp;hl=en" rel="nofollow">Scene Workflow: Exporting OgreXML scenes from Blender to JME3</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://docs.google.com/leaf?id=0B9hhZie2D-fEYmRkMTYwN2YtMzQ0My00NTM4LThhOTYtZTk1MTRlYTNjYTc3&amp;hl=en" class="urlextern" title="https://docs.google.com/leaf?id=0B9hhZie2D-fEYmRkMTYwN2YtMzQ0My00NTM4LThhOTYtZTk1MTRlYTNjYTc3&amp;hl=en" rel="nofollow">Animation Workflow: Create Animated UV-Mapped OgreXML Models in Blender, and use them in JME3</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=IDHMWsu_PqA" class="urlextern" title="http://www.youtube.com/watch?v=IDHMWsu_PqA" rel="nofollow">Video: Creating Worlds with Instances in Blender</a></div>
</li>
</ul>

<p>
What is required in your JME3-based Java class?
</p>
<ul>
<li class="level1"><div class="li"> One Animation Control per animated model</div>
</li>
<li class="level1"><div class="li"> As many Animation Channels per Control as you need to play your animations. In simple cases one channel is enough, sometimes you need two or more Channels per model to play gestures and motions in parallel.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Requirements" [168-2038] -->
<h2 class="sectionedit3" id="code_samples">Code Samples</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestSpatialAnim.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestSpatialAnim.java" rel="nofollow">TestSpatialAnim.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestBlenderAnim.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestBlenderAnim.java" rel="nofollow">TestBlenderAnim.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestBlenderObjectAnim.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestBlenderObjectAnim.java" rel="nofollow">TestBlenderObjectAnim.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestOgreAnim.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestOgreAnim.java" rel="nofollow">TestOgreAnim.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestOgreComplexAnim.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestOgreComplexAnim.java" rel="nofollow">TestOgreComplexAnim.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestCustomAnim.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/anim/TestCustomAnim.java" rel="nofollow">TestCustomAnim.java</a></div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Code Samples" [2039-2947] -->
<h2 class="sectionedit4" id="controlling_animations">Controlling Animations</h2>
<div class="level2">

</div>
<!-- EDIT4 SECTION "Controlling Animations" [2948-2983] -->
<h3 class="sectionedit5" id="the_animation_control">The Animation Control</h3>
<div class="level3">

<p>
Create one <code>com.jme3.animation.AnimControl</code> object in your JME3 application for each animated model that you want to control. You have to register each animated model to one of these Animation Controls. The control object gives you access to the available animation sequences in the model.  
</p>
<pre class="code java">  AnimControl playerControl<span class="sy0">;</span> <span class="co1">// you need one Control per model</span>
  Node player <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Oto/Oto.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// load a model</span>
  playerControl <span class="sy0">=</span> player.<span class="me1">getControl</span><span class="br0">(</span>AnimControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// get control over this model</span>
  playerControl.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// add listener</span></pre>

</div>
<!-- EDIT5 SECTION "The Animation Control" [2984-3623] -->
<h3 class="sectionedit6" id="animation_channels">Animation Channels</h3>
<div class="level3">

<p>
An Animation Control has several Animation Channels (<code>com.jme3.animation.AnimChannel</code>). Each channel can play one animation sequence at a time. 
</p>

<p>
There often are situations where you want to run several animation sequences at the same time, e.g. “shooting while walking” or “boxing while jumping”. In this case, you create several channels, assign an animation to each, and play them in parallel. 
</p>
<pre class="code java">  AnimChannel channel_walk <span class="sy0">=</span> playerControl.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  AnimChannel channel_jump <span class="sy0">=</span> playerControl.<span class="me1">createChannel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  ...</pre>

<p>
To reset a Control, call <code>control.clearChannels();</code>
</p>

</div>
<!-- EDIT6 SECTION "Animation Channels" [3624-4257] -->
<h2 class="sectionedit7" id="animation_control_properties">Animation Control Properties</h2>
<div class="level2">

<p>
The following information is available for an AnimControl.
</p>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AnimControl Property</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">createChannel()</td><td class="col1">Returns a new channel, controlling all bones by default.</td>
	</tr>
	<tr class="row2">
		<td class="col0">getNumChannels()</td><td class="col1">The number of channels registered to this Control.</td>
	</tr>
	<tr class="row3">
		<td class="col0">getChannel(0)</td><td class="col1">Gets individual channels by index number. At most <code>getNumChannels()</code>.</td>
	</tr>
	<tr class="row4">
		<td class="col0">clearChannels()</td><td class="col1">Clear all channels in this control.</td>
	</tr>
	<tr class="row5">
		<td class="col0">addListener(animEventListener) <br />
removeListener(animEventListener) <br />
clearListeners() </td><td class="col1">Adds or removes listeners to receive animation related events.</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [4360-4829] --><div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AnimControl Property</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setAnimations(aniHashMap)</td><td class="col1">Sets the animations that this AnimControl is capable of playing. The animations must be compatible with the skeleton given in the constructor.</td>
	</tr>
	<tr class="row2">
		<td class="col0">addAnim(boneAnim) <br />
removeAnim(boneAnim)</td><td class="col1">Adds or removes an animation from this Control.</td>
	</tr>
	<tr class="row3">
		<td class="col0">getAnimationNames()</td><td class="col1">A String Collection of names of all animations that this Control can play for this model.</td>
	</tr>
	<tr class="row4">
		<td class="col0">getAnim(“anim”)</td><td class="col1">Retrieve an animation from the list of animations.</td>
	</tr>
	<tr class="row5">
		<td class="col0">getAnimationLength(“anim”)</td><td class="col1">Returns the length of the given named animation in seconds</td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [4831-5391] --><div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AnimControl Property</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getSkeleton()</td><td class="col1">The Skeleton object controlled by this Control.</td>
	</tr>
	<tr class="row2">
		<td class="col0">getTargets()</td><td class="col1">The Skin objects controlled by this Control, as Mesh array.</td>
	</tr>
	<tr class="row3">
		<td class="col0">getAttachmentsNode(“bone”)</td><td class="col1">Returns the attachment node of a bone. Attach models and effects to this node to make them follow this bone's motions.</td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [5393-5708] -->
</div>
<!-- EDIT7 SECTION "Animation Control Properties" [4258-5710] -->
<h2 class="sectionedit11" id="animation_channel_properties">Animation Channel Properties</h2>
<div class="level2">

<p>
The following properties are set per AnimChannel.
</p>
<div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AnimChannel Property</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setLoopMode(LoopMode.Loop); </td><td class="col1"> From now on, the animation on this channel will repeat from the beginning when it ends. </td>
	</tr>
	<tr class="row2">
		<td class="col0">setLoopMode(LoopMode.DontLoop); </td><td class="col1"> From now on, the animation on this channel will play once, and the freeze at the last keyframe. </td>
	</tr>
	<tr class="row3">
		<td class="col0">setLoopMode(LoopMode.Cycle); </td><td class="col1"> From now on, the animation on this channel will play forward, then backward, then again forward, and so on. </td>
	</tr>
	<tr class="row4">
		<td class="col0">setSpeed(1f); </td><td class="col1"> From now on, play this animation slower (&lt;1f) or faster (&gt;1f), or with default speed (1f). </td>
	</tr>
	<tr class="row5">
		<td class="col0">setTime(1.3f); </td><td class="col1"> Fast-forward or rewind to a certain moment in time of this animation. </td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [5804-6428] -->
<p>
The following information is available for a channel.
</p>
<div class="table sectionedit13"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AnimChannel Property</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getAnimationName()</td><td class="col1">The name of the animation playing on this channel. Returns <code>null</code> when no animation is playing.</td>
	</tr>
	<tr class="row2">
		<td class="col0">getLoopMode()</td><td class="col1">The current loop mode on this channel. The returned com.jme3.animation enum can be LoopMode.Loop, LoopMode.DontLoop, or LoopMode.Cycle.</td>
	</tr>
	<tr class="row3">
		<td class="col0">getAnimMaxTime()</td><td class="col1">The total length of the animation on this channel. Or <code>0f</code> if nothing is playing.</td>
	</tr>
	<tr class="row4">
		<td class="col0">getTime()</td><td class="col1">How long the animation on this channel has been playing. It returns <code>0f</code> if the channel has not started playing yet, or a value up to getAnimMaxTime().</td>
	</tr>
	<tr class="row5">
		<td class="col0">getControl()</td><td class="col1">The AnimControl that belongs to this AnimChannel.</td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [6485-7118] -->
<p>
Use the following methods to add or remove individual bones to an AnimChannel. This is useful when you play two animations in parallel on two channels, and each controls a subset of the bones (e.g. one the arms, and the other the legs).
</p>
<div class="table sectionedit14"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AnimChannel Methods</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">addAllBones()</td><td class="col1">Add all the bones of the model's skeleton to be influenced by this animation channel. (default)</td>
	</tr>
	<tr class="row2">
		<td class="col0">addBone(“bone1”) <br />
addBone(bone1)</td><td class="col1">Add a single bone to be influenced by this animation channel.</td>
	</tr>
	<tr class="row3">
		<td class="col0">addToRootBone(“bone1”) <br />
addToRootBone(bone1) </td><td class="col1">Add a series of bones to be influenced by this animation channel: Add all bones, starting from the given bone, to the root bone.</td>
	</tr>
	<tr class="row4">
		<td class="col0">addFromRootBone(“bone1”) <br />
addFromRootBone(bone1) </td><td class="col1">Add a series of bones to be influenced by this animation channel: Add all bones, starting from the given root bone, going towards the children bones.</td>
	</tr>
</table></div>
<!-- EDIT14 TABLE [7358-7979] -->
</div>
<!-- EDIT11 SECTION "Animation Channel Properties" [5711-7981] -->
<h2 class="sectionedit15" id="playing_animations">Playing Animations</h2>
<div class="level2">

<p>
Animations are played by channel. <strong>Note:</strong> Whether the animation channel plays continuously or only once, depends on the Loop properties you have set.
</p>
<div class="table sectionedit16"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Channel Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">channel_walk.setAnim(“Walk”,0.50f); </td><td class="col1"> Start the animation named “Walk” on channel channel_walk. <br />
The float value specifies the time how long the animation should overlap with the previous one on this channel. If set to 0f, then no blending will occur and the new animation will be applied instantly.</td>
	</tr>
</table></div>
<!-- EDIT16 TABLE [8167-8493] -->
<p>
<strong>Tip:</strong> Use the AnimEventLister below to react at the end or start of an animation cycle.
</p>

</div>
<!-- EDIT15 SECTION "Playing Animations" [7982-8586] -->
<h3 class="sectionedit17" id="usage_example">Usage Example</h3>
<div class="level3">

<p>
In this short example, we define the space key to trigger playing the “Walk” animation on channel2.
</p>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ...
    <span class="me1">inputManager</span>.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Walk"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Walk"</span><span class="br0">)</span><span class="sy0">;</span>
    ...
  <span class="br0">}</span>
 
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>channel2.<span class="me1">getAnimationName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          channel2.<span class="me1">setLoopMode</span><span class="br0">(</span>LoopMode.<span class="me1">Loop</span><span class="br0">)</span><span class="sy0">;</span>
          channel2.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Walk"</span>, 0.50f<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT17 SECTION "Usage Example" [8587-9276] -->
<h2 class="sectionedit18" id="animation_event_listener">Animation Event Listener</h2>
<div class="level2">

<p>
A jME3 application that contains animations can implement the <code>com.jme3.animation.AnimEventListener</code> interface.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HelloAnimation <span class="kw1">extends</span> SimpleApplication
                     <span class="kw1">implements</span> AnimEventListener <span class="br0">{</span> ... <span class="br0">}</span></pre>

<p>
This optional Listener enables you to respond to animation start and end events, onAnimChange() and onAnimCycleDone().
</p>

</div>
<!-- EDIT18 SECTION "Animation Event Listener" [9277-9680] -->
<h3 class="sectionedit19" id="responding_to_animation_end">Responding to Animation End</h3>
<div class="level3">

<p>
The onAnimCycleDone() event is invoked when an animation cycle has ended. For non-looping animations, this event is invoked when the animation is finished playing. For looping animations, this event is invoked each time the animation loop is restarted.
</p>

<p>
You have access to the following objects:
</p>
<ul>
<li class="level1"><div class="li"> The Control to which the listener is assigned.</div>
</li>
<li class="level1"><div class="li"> The animation channel being played.</div>
</li>
<li class="level1"><div class="li"> The name of the animation that has just finished playing.</div>
</li>
</ul>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> onAnimCycleDone<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// test for a condition you are interested in, e.g. ...</span>
    <span class="kw1">if</span> <span class="br0">(</span>animName.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// respond to the event here, e.g. ...</span>
      channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Stand"</span>, 0.50f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT19 SECTION "Responding to Animation End" [9681-10471] -->
<h3 class="sectionedit20" id="responding_to_animation_start">Responding to Animation Start</h3>
<div class="level3">

<p>
The onAnimChange() event is invoked every time before an animation is set by the user to be played on a given channel (<code>channel.setAnim()</code>).
</p>

<p>
You have access to the following objects
</p>
<ul>
<li class="level1"><div class="li"> The Control to which the listener is assigned.</div>
</li>
<li class="level1"><div class="li"> The animation channel being played.</div>
</li>
<li class="level1"><div class="li"> The name of the animation that will start playing.</div>
</li>
</ul>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> onAnimChange<span class="br0">(</span>AnimControl control, AnimChannel channel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> animName<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// test for a condition you are interested in, e.g. ...</span>
    <span class="kw1">if</span> <span class="br0">(</span>animName.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Walk"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// respond to the event here, e.g. ...</span>
      channel.<span class="me1">setAnim</span><span class="br0">(</span><span class="st0">"Reset"</span>, 0.50f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT20 SECTION "Responding to Animation Start" [10472-] -->
