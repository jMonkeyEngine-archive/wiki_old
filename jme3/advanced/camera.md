---
title: The jME3 Camera
---
<h1 class="sectionedit1" id="the_jme3_camera">The jME3 Camera</h1>
<div class="level1">

<p>
Note that by default, the mouse pointer is invisible, and the mouse is set up to control the camera rotation.
</p>

</div>
<!-- EDIT1 SECTION "The jME3 Camera" [1-142] -->
<h2 class="sectionedit2" id="default_camera">Default Camera</h2>
<div class="level2">

<p>
The default com.jme3.renderer.Camera object is <code>cam</code> in com.jme3.app.Application.
</p>

<p>
The camera object is created with the following defaults:
</p>
<ul>
<li class="level1"><div class="li"> Width and height are set to the current Application's settings.getWidth() and settings.getHeight() values. </div>
</li>
<li class="level1"><div class="li"> Frustum Perspective:</div>
<ul>
<li class="level2"><div class="li"> Frame of view angle of 45° along the Y axis</div>
</li>
<li class="level2"><div class="li"> Aspect ratio of width divided by height</div>
</li>
<li class="level2"><div class="li"> Near view plane of 1 wu</div>
</li>
<li class="level2"><div class="li"> Far view plane of 1000 wu</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Start location at (0f, 0f, 10f).</div>
</li>
<li class="level1"><div class="li"> Start direction is looking at the origin.</div>
</li>
</ul>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">cam.getLocation(), setLocation()</td><td class="col1">The camera position</td>
	</tr>
	<tr class="row2">
		<td class="col0">cam.getRotation(), setRotation()</td><td class="col1">The camera rotation</td>
	</tr>
	<tr class="row3">
		<td class="col0">cam.getLeft(), setLeft()</td><td class="col1">The left axis of the camera</td>
	</tr>
	<tr class="row4">
		<td class="col0">cam.getUp(), setUp()</td><td class="col1">The up axis of the camera, usually Vector3f(0,1,0)</td>
	</tr>
	<tr class="row5">
		<td class="col0">cam.getDirection()</td><td class="col1">The vector the camera is facing</td>
	</tr>
	<tr class="row6">
		<td class="col0">cam.getAxes(), setAxes(left,up,dir)</td><td class="col1">One accessor for the three properties left/up/direction.</td>
	</tr>
	<tr class="row7">
		<td class="col0">cam.getFrame(), setFrame(loc,left,up,dir)</td><td class="col1">One accessor for the four properties location/left/up/direction.</td>
	</tr>
	<tr class="row8">
		<td class="col0">cam.resize(width, height, fixAspect)</td><td class="col1">Resize an existing camera object while keeping all other settings. Set fixAspect to true to adjust the aspect ratio (?)</td>
	</tr>
	<tr class="row9">
		<td class="col0">cam.setFrustum( near, far, left, right, top, bottom )</td><td class="col1">The frustum is defined by the near/far plane, left/right plane, top/bottom plane (all distances as float values)</td>
	</tr>
	<tr class="row10">
		<td class="col0">cam.setFrustumPerspective( fovY, aspect ratio, near, far)</td><td class="col1">The frustum is defined by view angle along the Y axis (in degrees), aspect ratio, and the near/far plane.</td>
	</tr>
	<tr class="row11">
		<td class="col0">cam.lookAt(target,up)</td><td class="col1">Turn the camera to look at Coordinate target, and rotate it around the up axis.</td>
	</tr>
	<tr class="row12">
		<td class="col0">cam.setParallelProjection(false)</td><td class="col1">Normal perspective</td>
	</tr>
	<tr class="row13">
		<td class="col0">cam.setParallelProjection(true)</td><td class="col1">Parallel projection perspective</td>
	</tr>
	<tr class="row14">
		<td class="col0">cam.getScreenCoordinates()</td><td class="col1">?</td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [694-1953] -->
<p>
<strong>Tip:</strong> After you change view port, frustum, or frame, call <code>cam.update();</code>
</p>

</div>
<!-- EDIT2 SECTION "Default Camera" [143-2035] -->
<h2 class="sectionedit4" id="flyby_camera">FlyBy Camera</h2>
<div class="level2">

<p>
The <code>flyCam</code> class field gives you access to an AppState that extends the default camera in <code>com.jme3.app.SimpleApplication</code> with more features. The input manager of the <code>com.jme3.input.FlyByCamera</code> AppState is preconfigured to respond to the WASD keys for walking forwards and backwards, and strafing to the sides; move the mouse to rotate the camera (“Mouse Look”), scroll the mouse wheel for zooming in or out. The QZ keys raise or lower the camera vertically.
</p>
<pre class="code">Q  W             up   forw
A  S  D    --&gt;  left  back  right 
Z               down  </pre>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">flyCam.setEnabled(true);</td><td class="col1">Activate the flyby cam</td>
	</tr>
	<tr class="row2">
		<td class="col0">flyCam.setMoveSpeed(10);</td><td class="col1">Control the move speed</td>
	</tr>
	<tr class="row3">
		<td class="col0">flyCam.setRotationSpeed(10);</td><td class="col1">Control the rotation speed</td>
	</tr>
	<tr class="row4">
		<td class="col0">flyCam.setDragToRotate(true)</td><td class="col1">Forces the player to keep mouse button pressed to rotate camera, typically used for Applets. If false (default), all mouse movement will be captured and interpreted as rotations.</td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [2634-3016] -->
<p>
The FlyByCamera is active by default, but you can change all these defaults for your game.
</p>

</div>
<!-- EDIT4 SECTION "FlyBy Camera" [2036-3109] -->
<h2 class="sectionedit6" id="chase_camera">Chase Camera</h2>
<div class="level2">

<p>
jME3 also supports an optional Chase Cam that can follow a moving target Spatial (<code>com.jme3.input.ChaseCamera</code>). When you use the chase cam, the player clicks and hold the mouse button to rotate the camera around the camera target. You can use a chase cam if you need the mouse pointer visible in your game.
</p>
<pre class="code java">flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
ChaseCamera chaseCam <span class="sy0">=</span> <span class="kw1">new</span> ChaseCamera<span class="br0">(</span>cam, target, inputManager<span class="br0">)</span><span class="sy0">;</span></pre>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">chaseCam.setSmoothMotion(true);</td><td class="col1">Interpolates a smoother acceleration/deceleration when the camera moves.</td>
	</tr>
	<tr class="row2">
		<td class="col0">chaseCam.setChasingSensitivity(5f)</td><td class="col1">The lower the chasing sensitivity, the slower the camera will follow the target when it moves.</td>
	</tr>
	<tr class="row3">
		<td class="col0">chaseCam.setTrailingSensitivity(0.5f)</td><td class="col1">The lower the traling sensitivity, the slower the camera will begin to go after the target when it moves. Default is 0.5;</td>
	</tr>
	<tr class="row4">
		<td class="col0">chaseCam.setRotationSensitivity(5f)</td><td class="col1">The lower the sensitivity, the slower the camera will rotate around the target when the mosue is dragged. Default is 5.</td>
	</tr>
	<tr class="row5">
		<td class="col0">chaseCam.setTrailingRotationInertia(0.1f)</td><td class="col1">This prevents the camera to stop too abruptly when the target stops rotating before the camera has reached the target's trailing position. Default is 0.1f.</td>
	</tr>
	<tr class="row6">
		<td class="col0">chaseCam.setDefaultDistance(40);</td><td class="col1">The default distance to the target at the start of the application.</td>
	</tr>
	<tr class="row7">
		<td class="col0">chaseCam.setMaxDistance(40);</td><td class="col1">The maximum zoom distance. Default is 40f.</td>
	</tr>
	<tr class="row8">
		<td class="col0">chaseCam.setMinDistance(1);</td><td class="col1">The minimum zoom distance. Default is 1f.</td>
	</tr>
	<tr class="row9">
		<td class="col0">chaseCam.setMinVerticalRotation(-FastMath.PI/2);</td><td class="col1">The minimal vertical rotation angle of the camera around the target. Default is 0.</td>
	</tr>
	<tr class="row10">
		<td class="col0">chaseCam.setDefaultVerticalRotation(-FastMath.PI/2);</td><td class="col1">The default vertical rotation angle of the camera around the target at the start of the application.</td>
	</tr>
	<tr class="row11">
		<td class="col0">chaseCam.setDefaultHorizontalRotation(-FastMath.PI/2);</td><td class="col1">The default horizontal rotation angle of the camera around the target at the start of the application.</td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [3561-5033] --><div class="tags"><span>
	<a href="/tag/camera.html" class="wikilink1" title="tag:camera" rel="tag">camera</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT6 SECTION "Chase Camera" [3110-] -->
