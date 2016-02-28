---
title: Making the Camera Follow a 3rd-Person Character
---
<h1 class="sectionedit1" id="making_the_camera_follow_a_3rd-person_character">Making the Camera Follow a 3rd-Person Character</h1>
<div class="level1">

<p>
When players steer a game character with 1st-person view, they directly steer the camera (<code>flyCam.setEnabled(true);</code>), and they never see the walking character itself. In a game with 3rd-person view, however, the players see the character walk, and you (the game developer) want to make the camera follow the character around when it walks.
</p>

<p>
There are two ways how the camera can do that:
</p>
<ul>
<li class="level1"><div class="li"> Registering a chase camera to the player and the input manager.</div>
</li>
<li class="level1"><div class="li"> Attaching the camera to the character using a camera node.</div>
</li>
</ul>

<p>
<strong>Important:</strong> Using third-person view requires you to deactivate the default flyCam (first-person view). This means that you have to configure your own navigation (<a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">key inputs and analogListener</a>) that make your player character walk. For moving a physical player character, use <code>player.setWalkDirection()</code>, for a non-physical character you can use <code>player.move()</code>.
</p>

</div>
<!-- EDIT1 SECTION "Making the Camera Follow a 3rd-Person Character" [1-990] -->
<h2 class="sectionedit2" id="code_samples">Code Samples</h2>
<div class="level2">

<p>
Press the WASD or arrow keys to move. Drag with the left mouse button to rotate.
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestChaseCamera.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestChaseCamera.java" rel="nofollow">TestChaseCamera.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestCameraNode.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestCameraNode.java" rel="nofollow">TestCameraNode.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Code Samples" [991-1372] -->
<h2 class="sectionedit3" id="camera_node">Camera Node</h2>
<div class="level2">

<p>
To make the camera follow a target node, add this camera node code to your init method (e.g. <code>simpleInitApp()</code>). The <code>target</code> spatial is typically the player node.
</p>
<pre class="code java"><span class="co1">// Disable the default flyby cam</span>
flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//create the camera Node</span>
camNode <span class="sy0">=</span> <span class="kw1">new</span> CameraNode<span class="br0">(</span><span class="st0">"Camera Node"</span>, cam<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//This mode means that camera copies the movements of the target:</span>
camNode.<span class="me1">setControlDir</span><span class="br0">(</span>ControlDirection.<span class="me1">SpatialToCamera</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//Attach the camNode to the target:</span>
target.<span class="me1">attachChild</span><span class="br0">(</span>camNode<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//Move camNode, e.g. behind and above the target:</span>
camNode.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">5</span>, <span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//Rotate the camNode to look at the target:</span>
camNode.<span class="me1">lookAt</span><span class="br0">(</span>target.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Important:</strong> Where the example says <code>camNode.setLocalTranslation(new Vector3f(0, 5, -5));</code>, you have to supply your own start position for the camera. This depends on the size of your target (the player character) and its position in your particular scene. Optimally, you set this to a spot a bit behind and above the target.
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Methods</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setControlDir(ControlDirection.SpatialToCamera)</td><td class="col1">User input steers the target spatial, and the camera follows the spatial.<br />
The spatial's transformation is copied over the camera's transformation. <br />
Example: Use with <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">CharacterControl</a>led spatial.</td>
	</tr>
	<tr class="row2">
		<td class="col0">setControlDir(ControlDirection.CameraToSpatial)</td><td class="col1">User input steers the camera, and the target spatial follows the camera. <br />
The camera's transformation is copied over the spatial's transformation. Use with first-person flyCam.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2446-2957] -->
<p>
<strong>Code sample:</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestCameraNode.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestCameraNode.java" rel="nofollow">TestCameraNode.java</a> – Press the WASD or arrow keys to move. Drag with the left mouse button to rotate.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Camera Node" [1373-3198] -->
<h2 class="sectionedit5" id="chase_camera">Chase Camera</h2>
<div class="level2">

<p>
To activate the chase camera, add the following code to your init method (e.g. <code>simpleInitApp()</code>). The <code>target</code> spatial is typically the player node. You will be able to rotate the target by dragging (keeping the left mouse button pressed and moving the mouse).
</p>
<pre class="code java"><span class="co1">// Disable the default flyby cam</span>
flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Enable a chase cam for this target (typically the player).</span>
ChaseCamera chaseCam <span class="sy0">=</span> <span class="kw1">new</span> ChaseCamera<span class="br0">(</span>cam, target, inputManager<span class="br0">)</span><span class="sy0">;</span>
chaseCam.<span class="me1">setSmoothMotion</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Method</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setInvertVerticalAxis(true)</td><td class="col1">Invert the camera's vertical rotation Axis </td>
	</tr>
	<tr class="row2">
		<td class="col0">setInvertHorizontalAxis(true)</td><td class="col1">Invert the camera's horizontal rotation Axis</td>
	</tr>
	<tr class="row3">
		<td class="col0">setTrailingEnabled(true)</td><td class="col1">Camera follows the target and flies around and behind when the target moves towards the camera. Trailing only works with smooth motion enabled. (Default)</td>
	</tr>
	<tr class="row4">
		<td class="col0">setTrailingEnabled(false)</td><td class="col1">Camera follows the target, but does not rotate around the target when the target changes direction.</td>
	</tr>
	<tr class="row5">
		<td class="col0">setSmoothMotion(true)</td><td class="col1">Activate SmoothMotion when trailing. This means the camera seems to accelerate and fly after the character, when it has caught up, it slows down again.</td>
	</tr>
	<tr class="row6">
		<td class="col0">setSmoothMotion(false)</td><td class="col1">Disable smooth camera motion. Disabling SmoothMotion also disables trailing.</td>
	</tr>
	<tr class="row7">
		<td class="col0">setLookAtOffset(Vector3f.UNIT_Y.mult(3))</td><td class="col1">Camera looks at a point 3 world units above the target.</td>
	</tr>
	<tr class="row8">
		<td class="col0">setToggleRotationTrigger(new MouseButtonTrigger(MouseInput.BUTTON_MIDDLE))</td><td class="col1">Enable rotation by keeping the middle mouse button pressed (like in Blender). This disables the rotation on right and left mouse button click.</td>
	</tr>
	<tr class="row9">
		<td class="col0">setToggleRotationTrigger(new MouseButtonTrigger(<br />
MouseInput.BUTTON_MIDDLE),<br />
new KeyTrigger(KeyInput.KEY_SPACE))</td><td class="col1">Activate mutiple triggers for the rotation of the camera, e.g. spacebar and middle mouse button, etc.</td>
	</tr>
	<tr class="row10">
		<td class="col0">setRotationSensitivity(5f)</td><td class="col1">How fast the camera rotates. Use values around &lt;1.0f (all bigger values are ignored).</td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [3733-5145] -->
<p>
<strong>Code sample:</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestChaseCamera.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestChaseCamera.java" rel="nofollow">TestChaseCamera.java</a> – Press the WASD or arrow keys to move. Drag with the left mouse button to rotate.</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Chase Camera" [3199-5388] -->
<h2 class="sectionedit7" id="which_to_choose">Which to Choose?</h2>
<div class="level2">

<p>
What is the difference of the two code samples above?
</p>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">CameraNode</th><th class="col1">ChaseCam</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Camera follows immediately, flies at same speed as target.</td><td class="col1">Camera moves smoothly and accelerates and decelerates, flies more slowly than the target and catches up.</td>
	</tr>
	<tr class="row2">
		<td class="col0">Camera stays attached to the target at a constant distance.</td><td class="col1">Camera orbits the target and approaches slowly.</td>
	</tr>
	<tr class="row3">
		<td class="col0">Drag-to-Rotate rotates the target and the camera. You always see the target from behind.</td><td class="col1">Drag-to-Rotate rotates only the camera. You can see the target from various sides.</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [5474-5945] -->
</div>
<!-- EDIT7 SECTION "Which to Choose?" [5389-] -->
