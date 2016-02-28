---
title: Remote-Controlling the Camera
---
<h1 class="sectionedit1" id="remote-controlling_the_camera">Remote-Controlling the Camera</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Remote-Controlling the Camera" [1-45] -->
<h2 class="sectionedit2" id="positioning_the_camera">Positioning the Camera</h2>
<div class="level2">

<p>
You can steer the camera using <a href="/jme3/advanced/cinematics.html" class="wikilink1" title="jme3:advanced:cinematics">Cinematics</a>:
</p>
<ol>
<li class="level1"><div class="li"> Create a Cinematic.</div>
</li>
<li class="level1"><div class="li"> Create a CameraNode and bind the camera object to the Cinematic. Note that we also give the camera node a name in this step. <pre class="code java">CameraNode camNode <span class="sy0">=</span> cinematic.<span class="me1">bindCamera</span><span class="br0">(</span><span class="st0">"topView"</span>, cam<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Position the camera node in its start location.</div>
</li>
<li class="level1"><div class="li"> Use activateCamera() to give the control of the camera to this node. You now see the scene from this camera's point of view. For example to see through the camera node named “topView”, 6 seconds after the start of the cinematic, you'd write <pre class="code java">cinematic.<span class="me1">activateCamera</span><span class="br0">(</span><span class="nu0">6</span>, <span class="st0">"topView"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Positioning the Camera" [46-714] -->
<h3 class="sectionedit3" id="code_sample">Code Sample</h3>
<div class="level3">
<pre class="code java">flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
Cinematic cinematic <span class="sy0">=</span> <span class="kw1">new</span> Cinematic<span class="br0">(</span>rootNode, <span class="nu0">20</span><span class="br0">)</span><span class="sy0">;</span>
 
CameraNode camNodeTop <span class="sy0">=</span> cinematic.<span class="me1">bindCamera</span><span class="br0">(</span><span class="st0">"topView"</span>, cam<span class="br0">)</span><span class="sy0">;</span>
camNodeTop.<span class="me1">setControlDir</span><span class="br0">(</span>ControlDirection.<span class="me1">SpatialToCamera</span><span class="br0">)</span><span class="sy0">;</span>
camNodeTop.<span class="me1">getControl</span><span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span>.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
 
CameraNode camNodeSide <span class="sy0">=</span> cinematic.<span class="me1">bindCamera</span><span class="br0">(</span><span class="st0">"sideView"</span>, cam<span class="br0">)</span><span class="sy0">;</span>
camNodeSide.<span class="me1">setControlDir</span><span class="br0">(</span>ControlDirection.<span class="me1">CameraToSpatial</span><span class="br0">)</span><span class="sy0">;</span>
camNodeSide.<span class="me1">getControl</span><span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span>.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT3 SECTION "Code Sample" [715-1171] -->
<h2 class="sectionedit4" id="moving_the_camera">Moving the Camera</h2>
<div class="level2">

<p>
If desired, attach the camNode to a MotionTrack to let it travel along waypoints. This is demonstrated in the <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/animation/TestCinematic.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/animation/TestCinematic.java" rel="nofollow">TestCameraMotionPath.java example</a>.
</p>
<div class="tags"><span>
	<a href="/tag/camera.html" class="wikilink1" title="tag:camera" rel="tag">camera</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/cinematics.html" class="wikilink1" title="tag:cinematics" rel="tag">cinematics</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Moving the Camera" [1172-] -->
