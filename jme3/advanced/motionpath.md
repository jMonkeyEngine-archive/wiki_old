---
title: MotionPath
---
<h1 class="sectionedit1" id="motionpath">MotionPath</h1>
<div class="level1">

<p>
A MotionPath describes the motion of a spatial between waypoints. The path can be linear or rounded. You use MotionPaths to remote-control a spatial, or the camera.
</p>

<p>
<strong>Tip:</strong> If you want to remote-control a whole cutscene with several spatials moving at various times, then we recommened you use MotionPaths together with <a href="/jme3/advanced/cinematics.html" class="wikilink1" title="jme3:advanced:cinematics">Cinematics</a>.
</p>

</div>
<!-- EDIT1 SECTION "MotionPath" [1-365] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestMotionPath.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestMotionPath.java" rel="nofollow">TestMotionPath.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestCameraMotionPath.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/animation/TestCameraMotionPath.java" rel="nofollow">TestCameraMotionPath.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [366-713] -->
<h2 class="sectionedit3" id="what_are_way_points">What Are Way Points?</h2>
<div class="level2">

<p>
When shooting a movie scene, the director tells actors where to walk, for example, by drawing a series of small crosses on the floor. Cameramen often mount the camera on rails (so called dolly track) so they can follow along complex scenes more easily. 
</p>

<p>
In JME3, you use MotionPaths to specify a series of positions for a character or the camera. The MotionPath automatically updates the transformation of the spatial in each frame to make it move from one point to the next.
</p>
<ul>
<li class="level1"><div class="li"> <strong>A way point</strong> is one positions on a path. </div>
</li>
<li class="level1"><div class="li"> <strong>A MotionPath</strong> contains a list of all way points of one path. </div>
</li>
</ul>

<p>
The final shape of the path is computed using a linear interpolation or a <a href="http://www.mvps.org/directx/articles/catmull/" class="urlextern" title="http://www.mvps.org/directx/articles/catmull/" rel="nofollow">Catmull-Rom</a> spline interpolation on the way points. 
</p>

</div>
<!-- EDIT3 SECTION "What Are Way Points?" [714-1522] -->
<h2 class="sectionedit4" id="create_a_motionpath">Create a MotionPath</h2>
<div class="level2">

<p>
Create a Motionpath object and add way points to it.
</p>
<pre class="code java">MotionPath path <span class="sy0">=</span> <span class="kw1">new</span> MotionPath<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
path.<span class="me1">addWayPoint</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">10</span>, <span class="nu0">3</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
path.<span class="me1">addWayPoint</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">8</span>, <span class="sy0">-</span><span class="nu0">2</span>, <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
...</pre>

<p>
You can configure the path as follows.
</p>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> MotionPath Method </th><th class="col1"> Usage </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">path.setCycle(true)</td><td class="col1">Sets whether the motion along this path should be closed (true) or open-ended (false). </td>
	</tr>
	<tr class="row2">
		<td class="col0">path.addWayPoint(vector)</td><td class="col1">Adds individual waypoints to this path. The order is relevant.</td>
	</tr>
	<tr class="row3">
		<td class="col0">path.removeWayPoint(vector) <br />
removeWayPoint(index)</td><td class="col1">Removes a way point from this path. You can specify the point that you want to remove as vector or as integer index.</td>
	</tr>
	<tr class="row4">
		<td class="col0">path.setCurveTension(0.83f)</td><td class="col1">Sets the tension of the curve (Catmull-Rom Spline). A value of 0.0f results in a straight linear line, 1.0 a very round curve.</td>
	</tr>
	<tr class="row5">
		<td class="col0">path.getNbWayPoints()</td><td class="col1">Returns the number of waypoints in this path.</td>
	</tr>
	<tr class="row6">
		<td class="col0">path.enableDebugShape(assetManager,rootNode)</td><td class="col1">Shows a line that visualizes the path. Use this during development and for debugging so you see what you are doing.</td>
	</tr>
	<tr class="row7">
		<td class="col0">path.disableDebugShape()</td><td class="col1">Hides the line that visualizes the path. Use this for the release build.</td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [1793-2684] -->
</div>
<!-- EDIT4 SECTION "Create a MotionPath" [1523-2685] -->
<h2 class="sectionedit6" id="motionpathlistener">MotionPathListener</h2>
<div class="level2">

<p>
You can hook interactions into a playing MotionPath. Register a MotionPathListener to the MotionPath to track whether way points have been reached, and then trigger a custom action. The onWayPointReach() method of the interface gives you access to the MotionTrack object <code>control</code>, and an integer value representing the current wayPointIndex.
</p>

<p>
In this example, you just print the status at every way point. In a game you could trigger actions here: Transformations, animations, sounds, game actions (attack, open door, etc).
</p>
<pre class="code java">path.<span class="me1">addListener</span><span class="br0">(</span> <span class="kw1">new</span> MotionPathListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw4">void</span> onWayPointReach<span class="br0">(</span>MotionTrack control, <span class="kw4">int</span> wayPointIndex<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>path.<span class="me1">getNbWayPoints</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">==</span> wayPointIndex <span class="sy0">+</span> <span class="nu0">1</span><span class="br0">)</span> <span class="br0">{</span>
      println<span class="br0">(</span>control.<span class="me1">getSpatial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">" has finished moving. "</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
      println<span class="br0">(</span>control.<span class="me1">getSpatial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">" has reached way point "</span> <span class="sy0">+</span> wayPointIndex<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
<span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT6 SECTION "MotionPathListener" [2686-] -->
