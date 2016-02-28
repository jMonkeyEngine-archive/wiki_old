---
title: JME3 Cinematics
---
<h1 class="sectionedit1" id="jme3_cinematics">JME3 Cinematics</h1>
<div class="level1">

<p>
JME3 cinematics (com.jme.cinematic) allow you to remote control nodes and cameras in a 3D game: You can script and and play cinematic scenes. You can use cinematics to create <a href="http://en.wikipedia.org/wiki/Cutscene" class="urlextern" title="http://en.wikipedia.org/wiki/Cutscene" rel="nofollow">cutscenes</a> and movies/trailers for your game. Another good use case is efficient “destruction physics”: Playing back prerecorded flying pieces of debris for demolitions is much faster than calculating them with live physics.
</p>

<p>
Internally, Cinematics are implemented as <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a>. 
</p>

<p>
Short overview of the cinematic process:
</p>
<ol>
<li class="level1"><div class="li"> Plan the script of your movie. <br />
Write down a timeline (e.g. on paper) of which character should be at which spot at which time.</div>
</li>
<li class="level1"><div class="li"> Attach the scene objects that you want to remote-control to one Node. <br />
This Node can be the rootNode, or a Node that is attached to the rootNode. </div>
</li>
<li class="level1"><div class="li"> Create a Cinematic object for this movie scene. The Cinematic will contain and manage the movie script.</div>
</li>
<li class="level1"><div class="li"> For each line in your script (for each keyframe in your timeline), add a CinematicEvent to the Cinematic. </div>
</li>
</ol>

</div>
<!-- EDIT1 SECTION "JME3 Cinematics" [1-1103] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestCinematic.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestCinematic.java" rel="nofollow">TestCinematic.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [1104-1282] -->
<h2 class="sectionedit3" id="how_to_use_a_cinematic">How to Use a Cinematic</h2>
<div class="level2">

<p>
A Cinematic is like a movie script for a node. 
</p>
<pre class="code java">Cinematic cinematic <span class="sy0">=</span> <span class="kw1">new</span> Cinematic<span class="br0">(</span>sceneNode, duration<span class="br0">)</span><span class="sy0">;</span>
cinematic.<span class="me1">addCinematicEvent</span><span class="br0">(</span>starttime1, event1<span class="br0">)</span><span class="sy0">;</span>
cinematic.<span class="me1">addCinematicEvent</span><span class="br0">(</span>starttime2, event2<span class="br0">)</span><span class="sy0">;</span>
cinematic.<span class="me1">addCinematicEvent</span><span class="br0">(</span>starttime2, event3<span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">stateManager</span>.<span class="me1">attach</span><span class="br0">(</span>cinematic<span class="br0">)</span><span class="sy0">;</span></pre>
<ol>
<li class="level1"><div class="li"> Create one Cinematic per scripted scene.</div>
<ul>
<li class="level2"><div class="li"> <code>sceneNode</code> is the node containing the scene (can be the rootNode).</div>
</li>
<li class="level2"><div class="li"> <code>duration</code> is the duration of the whole scene in seconds.</div>
</li>
<li class="level2"><div class="li"> Each Cinematic is a set of CinematicEvents, that are triggered at a given moment on the timeline.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Create one CinematicEvent for each line of your movie script.  </div>
<ul>
<li class="level2"><div class="li"> <code>event</code> is one motion of a moving object. You can add several events. More details below.</div>
</li>
<li class="level2"><div class="li"> <code>starttime</code> is the time when this particular cinematic event starts on the timeline. Specify the start time in seconds since the beginning of the cinematic.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Attach the Cinematic to the SimpleApplication's stateManager. </div>
</li>
<li class="level1"><div class="li"> Play, stop and pause the Cinematic from your code.</div>
</li>
</ol>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">cinematic.play()</td><td class="col1">Starts playing the cinematic from the start, or from where it was paused.</td>
	</tr>
	<tr class="row2">
		<td class="col0">cinematic.stop()</td><td class="col1">Stops playing the cinematic and rewinds it.</td>
	</tr>
	<tr class="row3">
		<td class="col0">cinematic.pause()</td><td class="col1">Pauses the cinematic.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2374-2586] -->
</div>
<!-- EDIT3 SECTION "How to Use a Cinematic" [1283-2586] -->
<h2 class="sectionedit5" id="events_cinematicevents">Events(CinematicEvents)</h2>
<div class="level2">

<p>
Just like a movie script consists of lines with instructions to the actors, each Cinematic consists of a series of events.
</p>

<p>
Here is the list of available CinematicEvents that you use as events. Each track remote-controls scene objects in a different way:
</p>
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Events(CinematicEvents)</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">MotionEvent</td><td class="col1">Use a MotionEvent to move a Spatial non-linearly over time. A MotionEvent is based on a list of waypoints in a MotionPath. The curve goes through each waypoint, and you can adjust the tension of the curve to modify the roundedness of the path. This is the motion interpolation you are going to use in most cases. </td>
	</tr>
	<tr class="row2">
		<td class="col0">SoundEvent</td><td class="col1">Use a SoundEvent to play a <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">sound</a> at a given time for the given duration.</td>
	</tr>
	<tr class="row3">
		<td class="col0">GuiEvent</td><td class="col1">Displays a <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI</a> at a given time for the given duration. Use it to display subtitles or HUD elements. Bind the Nifty <abbr title="Graphical User Interface">GUI</abbr> XML to the cinematic using <code>cinematic.bindUi(“path/to/nifty/file.xml”);</code></td>
	</tr>
	<tr class="row4">
		<td class="col0">AnimationEvent</td><td class="col1">Use this to start playing a model <a href="/jme3/advanced/animation.html" class="wikilink1" title="jme3:advanced:animation">animation</a> at a given time (a character walking animation for example)</td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [2880-3681] -->
<p>
You can add custom events by extending AbstractCinematicEvent.
</p>

</div>
<!-- EDIT5 SECTION "Events(CinematicEvents)" [2587-3745] -->
<h3 class="sectionedit7" id="motionevent">MotionEvent</h3>
<div class="level3">

<p>
A MotionEvent moves a Spatial along a complex path.
</p>
<pre class="code java">MotionEvent events<span class="sy0">=</span> <span class="kw1">new</span> MotionEvent <span class="br0">(</span>thingNode, path<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Details of the constructor:
</p>
<ul>
<li class="level1"><div class="li"> <code>thingNode</code> is the Spatial to be moved.</div>
</li>
<li class="level1"><div class="li"> <code>path</code> is a complex <a href="/jme3/advanced/motionpath.html" class="wikilink1" title="jme3:advanced:motionpath">MotionPath</a>.</div>
</li>
</ul>

<p>
To create a MotionEvent, do the following:
</p>
<ol>
<li class="level1"><div class="li"> <a href="/doku.php/jme3:advanced:motiontrack" class="wikilink2" title="jme3:advanced:motiontrack" rel="nofollow">Create a MotionEvent</a></div>
</li>
<li class="level1"><div class="li"> Create a MotionEvent based on the MotionPath.</div>
</li>
<li class="level1"><div class="li"> Configure your MotionEvent (see below).</div>
</li>
<li class="level1"><div class="li"> Add the MotionEvent to a Cinematic.</div>
</li>
</ol>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">MotionEvent configuration method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">event.setLoopMode(LoopMode.Loop)</td><td class="col1">Sets whether the animation along this path should loop (LoopMode.Loop) or play only once (LoopMode.DontLoop).</td>
	</tr>
	<tr class="row2">
		<td class="col0">event.setDirectionType(MotionEvent.Direction.None)</td><td class="col1">Sets the direction behavior type of the controlled node. Direction.None deactivates this feature. You can choose from the following options: LookAt, Path, PathAndRotation, Rotation.</td>
	</tr>
	<tr class="row3">
		<td class="col0">event.setDirectionType(MotionEvent.Direction.LookAt)</td><td class="col1">The spatial turns (rotates) to keep facing a certain point while moving. Specify the point with the <code>setLookAt()</code> method.</td>
	</tr>
	<tr class="row4">
		<td class="col0">event.setDirectionType(MotionEvent.Direction.Path)</td><td class="col1">The spatial always faces in the direction of the path while moving.</td>
	</tr>
	<tr class="row5">
		<td class="col0">event.setDirectionType(MotionEvent.Direction.PathAndRotation)</td><td class="col1">The spatial faces the direction of the path, plus an added rotation. Use together with the <code>setRotation()</code> method.</td>
	</tr>
	<tr class="row6">
		<td class="col0">event.setDirectionType(MotionEvent.Direction.Rotation)</td><td class="col1">The spatial spins (rotates) while moving. You describe the spin by a custom quaternion. Use together with the <code>setRotation()</code> method.</td>
	</tr>
	<tr class="row7">
		<td class="col0">event.setLookAt(teapot.getWorldTranslation(), Vector3f.UNIT_Y)</td><td class="col1">The spatial always faces towards this location. Use together with <code>MotionEvent.Direction.LookAt</code>.</td>
	</tr>
	<tr class="row8">
		<td class="col0">event.setRotation(quaternion)</td><td class="col1">Sets the rotation. Use together with <code>MotionEvent.Direction.Rotation</code> or <code>MotionEvent.Direction.PathAndRotation</code>.</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [4231-5640] -->
<p>
<strong>Tip:</strong> Most likely you remote-control more than one object in your scene. Give the events and paths useful names such as <code>dragonEvent</code>, <code>dragonPath</code>, <code>heroEvent</code>, <code>heroPath</code>, etc.
</p>

</div>
<!-- EDIT7 SECTION "MotionEvent" [3746-5835] -->
<h3 class="sectionedit9" id="soundevent">SoundEvent</h3>
<div class="level3">

<p>
A SoundEventplays a sound as part of the cinematic. 
</p>
<pre class="code java">SoundEvent<span class="br0">(</span> audioPath, isStream, duration, loopMode <span class="br0">)</span></pre>

<p>
Details of the constructor:
</p>
<ul>
<li class="level1"><div class="li"> <code>audioPath</code> is the path to an audio file as String, e.g. “Sounds/mySound.wav”.</div>
</li>
<li class="level1"><div class="li"> <code>isStream</code> toggles between streaming and buffering. Set to true to stream long audio file, set to false to play short buffered sounds.</div>
</li>
<li class="level1"><div class="li"> <code>duration</code> is the time that it should take to play.</div>
</li>
<li class="level1"><div class="li"> <code>loopMode</code> can be LoopMode.Loop, LoopMode.DontLoop, LoopMode.Cycle.</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "SoundEvent" [5836-6366] -->
<h3 class="sectionedit10" id="guievent">GuiEvent</h3>
<div class="level3">

<p>
A GuiEventshows or hide a NiftyGUI as part of a cinematic.
</p>
<pre class="code java">GuiEvent<span class="br0">(</span> screen, duration, loopMode <span class="br0">)</span></pre>

<p>
You must use this together with bindUI() to specify the Nifty <abbr title="Graphical User Interface">GUI</abbr> XML file that you want to load:
</p>
<pre class="code java">cinematic.<span class="me1">bindUi</span><span class="br0">(</span><span class="st0">"Interface/subtitle.xml"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Details of the constructor:
</p>
<ul>
<li class="level1"><div class="li"> <code>screen</code> is the name of the Nifty <abbr title="Graphical User Interface">GUI</abbr> screen to load, as String. </div>
</li>
<li class="level1"><div class="li"> <code>duration</code> is the time that it should take to play.</div>
</li>
<li class="level1"><div class="li"> <code>loopMode</code> can be LoopMode.Loop, LoopMode.DontLoop, LoopMode.Cycle.</div>
</li>
</ul>

</div>
<!-- EDIT10 SECTION "GuiEvent" [6367-6894] -->
<h3 class="sectionedit11" id="animationevent">AnimationEvent</h3>
<div class="level3">

<p>
An AnimationEvent triggers an animation as part of a cinematic.
</p>
<pre class="code java">AnimationEvent<span class="br0">(</span> thingNode, animationName, duration, loopMode <span class="br0">)</span></pre>

<p>
Details of the constructor:
</p>
<ul>
<li class="level1"><div class="li"> <code>thingNode</code> is the Spatial whose animation you want to play.</div>
</li>
<li class="level1"><div class="li"> <code>animationName</code> the name of the animation stored in the animated model that you want to trigger, as a String.</div>
</li>
<li class="level1"><div class="li"> <code>duration</code> is the time that it should take to play.</div>
</li>
<li class="level1"><div class="li"> <code>loopMode</code> can be LoopMode.Loop, LoopMode.DontLoop, LoopMode.Cycle.</div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "AnimationEvent" [6895-7407] -->
<h3 class="sectionedit12" id="camera_management">Camera Management</h3>
<div class="level3">

<p>
There is a built in system for camera switching in Cinematics. It based on CameraNode, and the cinematic just enable the given CameraNode control at a given time.
</p>

<p>
First you have to bind a camera to the cinematic with a unique name. You'll be provided with a CameraNode
</p>
<pre class="code java"> CameraNode camNode <span class="sy0">=</span> cinematic.<span class="me1">bindCamera</span><span class="br0">(</span><span class="st0">"topView"</span>, cam<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
then you can do whatever you want with this camera node : place it so that you have a the camera angle you'd like, attach it to a motion event to have some camera scrolling, attach control of your own that give it whatever behavior you'd like.
In the above example, I want it to be a top view of the scene looking at the world origin.
</p>
<pre class="code java"> <span class="co1">//set its position</span>
 camNode.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">50</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 <span class="co1">// set it to look at the world origin</span>
 camNode.<span class="me1">lookAt</span><span class="br0">(</span>Vector3F.<span class="me1">ZERO</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Then i just have to schedule its activation in the cinematic. I want it to get activated 3 seconds after the start of the cinematic so I just have to do 
</p>
<pre class="code java"> cinematic.<span class="me1">activateCamera</span><span class="br0">(</span><span class="nu0">3</span>,”topView”<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT12 SECTION "Camera Management" [7408-8520] -->
<h3 class="sectionedit13" id="customizations">Customizations</h3>
<div class="level3">

<p>
You can extend individual CinematicEvents. The <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/SubtitleTrack.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/SubtitleTrack.java" rel="nofollow">SubtitleTrack.java example</a> shows how to extend a GuiTrack to script subtitles. See how the subtitles are used in the <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestCinematic.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestCinematic.java" rel="nofollow">TestCinematic.java example</a>.
</p>

<p>
You can also create new CinematicEvent by extending <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/cinematic/events/AbstractCinematicEvent.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/cinematic/events/AbstractCinematicEvent.java" rel="nofollow">AbstractCinematicEvent</a>. An AbstractCinematicEvent implements the CinematicEvent interface and provides duration, time, speed, etc… management. Look at the <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestCinematic.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestCinematic.java" rel="nofollow">TestCinematic.java example</a> is to use this for a custom fadeIn/fadeOut effect in combination with a com.jme3.post.filters.FadeFilter.
</p>

</div>
<!-- EDIT13 SECTION "Customizations" [8521-9610] -->
<h2 class="sectionedit14" id="interacting_with_cinematics">Interacting with Cinematics</h2>
<div class="level2">

</div>
<!-- EDIT14 SECTION "Interacting with Cinematics" [9611-9651] -->
<h3 class="sectionedit15" id="cinematiceventlistener">CinematicEventListener</h3>
<div class="level3">
<pre class="code java">CinematicEventListener cel <span class="sy0">=</span> <span class="kw1">new</span> CinematicEventListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw4">void</span> onPlay<span class="br0">(</span>CinematicEvent cinematic<span class="br0">)</span> <span class="br0">{</span>
    chaseCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"play"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> onPause<span class="br0">(</span>CinematicEvent cinematic<span class="br0">)</span> <span class="br0">{</span>
    chaseCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"pause"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> onStop<span class="br0">(</span>CinematicEvent cinematic<span class="br0">)</span> <span class="br0">{</span>
    chaseCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"stop"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span>
cinematic.<span class="me1">addListener</span><span class="br0">(</span>cel<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT15 SECTION "CinematicEventListener" [9652-10147] -->
<h3 class="sectionedit16" id="physics_interaction">Physics Interaction</h3>
<div class="level3">

<p>
Upcoming.
</p>

</div>
<!-- EDIT16 SECTION "Physics Interaction" [10148-] -->
