---
title: 3-D Rotation
---
<h1 class="sectionedit1" id="d_rotation">3-D Rotation</h1>
<div class="level1">

<p>
<em>Bad news: 3D rotation is done using matrix calculus. <br />
Good news: If you do not understand calculus, there are two simple rules how you get it right.</em>
</p>

<p>
<br />

</p>

<p>
<strong>3D rotation</strong> is a crazy mathematical operation where you need to multiply all vertices in your object by four floating point numbers; the multiplication is referred to as concatenation, the array of four numbers {x,y,z,w} is referred to as quaternion. Don't worry, the 3D engine does the tough work for you. All you need to know is: 
</p>

<p>
<strong>The Quaternion</strong> is an object capable of deep-freezing and storing a rotation that you can apply to a 3D object.
</p>

</div>
<!-- EDIT1 SECTION "3-D Rotation" [1-643] -->
<h2 class="sectionedit2" id="using_quaternions_for_rotation">Using Quaternions for Rotation</h2>
<div class="level2">

<p>
To store a rotation in a Quaternion, you must specify two things: The angle and the axis of the rotation.
</p>
<ul>
<li class="level1"><div class="li"> The rotation angle is defined as a multiple of the number PI. </div>
</li>
<li class="level1"><div class="li"> The rotation axis is defined by a vector: Think of them in terms of “pitch”, “yaw”, and “roll”. </div>
</li>
</ul>

<p>
<br />

</p>

<p>
Example:
</p>
<pre class="code java"><span class="coMULTI">/* This quaternion stores a 180 degree rolling rotation */</span> 
Quaternion roll180 <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> 
roll180.<span class="me1">fromAngleAxis</span><span class="br0">(</span> FastMath.<span class="me1">PI</span> , <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">1</span><span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span> 
<span class="coMULTI">/* The rotation is applied: The object rolls by 180 degrees. */</span> 
thingamajig.<span class="me1">setLocalRotation</span><span class="br0">(</span> roll180 <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
So how to choose the right numbers for the Quaternion parameters? I'll give you my cheat-sheet: 
</p>

<p>
<br />

</p>
<div class="table sectionedit3"><table class="inline">
	<tr class="row0">
		<td class="col0"> <strong>Rotation around Axis?</strong> </td><td class="col1"> <strong>Use this Axis Vector!</strong> </td><td class="col2"> <strong>Examples for this kind of rotation</strong> </td>
	</tr>
	<tr class="row1">
		<td class="col0">X axis </td><td class="col1"> (1,0,0) </td><td class="col2"> A plane pitches. Nodding your head. </td>
	</tr>
	<tr class="row2">
		<td class="col0">Y axis </td><td class="col1"> (0,1,0) </td><td class="col2"> A plane yaws. A vehicle turns. Shaking your head. </td>
	</tr>
	<tr class="row3">
		<td class="col0">Z axis </td><td class="col1"> (0,0,1) </td><td class="col2"> A plane rolls or banks. Cocking your head. </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [1368-1661] -->
<p>
<br />

Note: These are the three most common examples – technically you can rotate around any axis expressed by a vector.
</p>

<p>
<br />

</p>
<div class="table sectionedit4"><table class="inline">
	<tr class="row0">
		<td class="col0"> <strong>Angle?</strong> </td><td class="col1"> <strong>Use Radians!</strong> </td><td class="col2"> <strong>Examples</strong> </td>
	</tr>
	<tr class="row1">
		<td class="col0 leftalign">45 degrees  </td><td class="col1"> FastMath.PI / 4 </td><td class="col2"> eighth of a circle </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign">90 degrees  </td><td class="col1"> FastMath.PI / 2 </td><td class="col2"> quarter circle, 3 o'clock </td>
	</tr>
	<tr class="row3">
		<td class="col0">180 degrees </td><td class="col1"> FastMath.PI </td><td class="col2"> half circle, 6 o'clock </td>
	</tr>
	<tr class="row4">
		<td class="col0">270 degrees </td><td class="col1"> FastMath.PI * 3 / 2 </td><td class="col2"> three quarter circle, 9 o'clock </td>
	</tr>
	<tr class="row5">
		<td class="col0">360 degrees </td><td class="col1"> FastMath.PI * 2 </td><td class="col2"> full circle, 12  o'clock <img src="/lib/images/smileys/icon_wink.gif" class="icon" alt=";-)" /> </td>
	</tr>
	<tr class="row6">
		<td class="col0"><code>g</code> degrees </td><td class="col1"> FastMath.PI * g / 180 </td><td class="col2"> any angle <code>g</code> </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [1787-2198] -->
<p>
<br />

<strong>Important:</strong> You must specify angles in <a href="http://en.wikipedia.org/wiki/Radian" class="urlextern" title="http://en.wikipedia.org/wiki/Radian" rel="nofollow">Radian</a>s (multiples or fractions of PI). If you use degrees, you will just get useless results.
</p>

<p>
<br />

How to use these tables to speficy a certain rotation:
</p>
<ol>
<li class="level1"><div class="li"> Pick the appropriate vector from the axis table.</div>
</li>
<li class="level1"><div class="li"> Pick the appropriate radians value from the angle table.</div>
</li>
<li class="level1"><div class="li"> Create a Quaternion to store this rotation. <code>… fromAngleAxis( radians , vector )</code></div>
</li>
<li class="level1"><div class="li"> Apply the Quaternion to a node to rotate it. <code>… setLocalRotation(…)</code></div>
</li>
</ol>

<p>
Quaternion objects can be used as often as you want, so give them meaningfull names, like <code>roll90, pitch45, yaw180</code>. 
</p>

<p>
<a href="http://gpwiki.org/index.php/OpenGL:Tutorials:Using_Quaternions_to_represent_rotation" class="urlextern" title="http://gpwiki.org/index.php/OpenGL:Tutorials:Using_Quaternions_to_represent_rotation" rel="nofollow">More about Quaternions</a>…
</p>

</div>
<!-- EDIT2 SECTION "Using Quaternions for Rotation" [644-2959] -->
<h2 class="sectionedit5" id="code_sample">Code Sample</h2>
<div class="level2">
<pre class="code java"><span class="coMULTI">/* We start out with a horizontal object */</span> 
Cylinder cylinder <span class="sy0">=</span> <span class="kw1">new</span> Cylinder<span class="br0">(</span><span class="st0">"post"</span>, <span class="nu0">10</span>, <span class="nu0">10</span>, <span class="nu0">1</span>, <span class="nu0">10</span><span class="br0">)</span><span class="sy0">;</span>
cylinder.<span class="me1">setModelBound</span><span class="br0">(</span><span class="kw1">new</span> BoundingBox<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="coMULTI">/* Create a 90-degree-pitch Quaternion. */</span>
Quaternion pitch90 <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
pitch90.<span class="me1">fromAngleAxis</span><span class="br0">(</span>FastMath.<span class="me1">PI</span><span class="sy0">/</span><span class="nu0">2</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="coMULTI">/* Apply the rotation to the object */</span>
cylinder.<span class="me1">setLocalRotation</span><span class="br0">(</span>pitch90<span class="br0">)</span><span class="sy0">;</span>
<span class="coMULTI">/* Update the model. Now it's vertical. */</span>
cylinder.<span class="me1">updateModelBound</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
cylinder.<span class="me1">updateGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT5 SECTION "Code Sample" [2960-3465] -->
<h2 class="sectionedit6" id="interpolating_rotations">Interpolating Rotations</h2>
<div class="level2">

<p>
You can specify two rotations, and then have jme calculate (interpolate) the steps between two rotations:
</p>
<ul>
<li class="level1"><div class="li"> com.jme3.math.Quaternion, slerp() – store an interpolated step between two rotations</div>
<ul>
<li class="level2"><div class="li"> <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Quaternion.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Quaternion.html" rel="nofollow">com.jme.math.Quaternion</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://www.jmonkeyengine.com/doc/com/jme/math/TransformQuaternion.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/TransformQuaternion.html" rel="nofollow">com.jme.math.TransformQuaternion</a></div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Interpolating Rotations" [3466-3910] -->
<h2 class="sectionedit7" id="adding_rotations">"Adding" Rotations</h2>
<div class="level2">

<p>
You can concatenate (add) rotations: This means you turn the object first around one axis, then around the other, in one step.
</p>

<p>
<code>Quaternion myRotation =  pitch90.mult(roll45); /* pitch and roll */</code>
</p>

</div>
<!-- EDIT7 SECTION "Adding Rotations" [3911-4144] -->
<h2 class="sectionedit8" id="troubleshooting_rotations">Troubleshooting Rotations</h2>
<div class="level2">

<p>
Does the object end up in an unexpected location, or at an unexpected angle? If you are getting weird results, check the following:
</p>
<ol>
<li class="level1"><div class="li"> 3-D transformations are non-commutative! This means it often makes a huge difference whether you first move a node and then rotate it around an axis, or first rotate the node around an axis and then move it. Make sure you code does what you mean to do.</div>
</li>
<li class="level1"><div class="li"> Are you intending to rotate around the object's origin along an axis, or around another pivot point outside the object? If you are trying to <em>rotate an object around a pivot point</em>, you have to create an (invisible) pivot node first, and attach the object to it. Then apply the rotation to the <em>parental pivot node</em>, not to the child object itself!</div>
</li>
<li class="level1"><div class="li"> Did you enter the angle in degrees (0 - 360°) or radians (0 - 2*PI)? A 3D engine expects radians, so make sure to convert your values! Formula: <code>g° = FastMath.PI * g / 180</code></div>
</li>
</ol>

</div>
<!-- EDIT8 SECTION "Troubleshooting Rotations" [4145-5113] -->
<h2 class="sectionedit9" id="tiptransformation_matrix">Tip: Transformation Matrix</h2>
<div class="level2">

<p>
This here is just about rotation, but there are three types of 3-D transformation: <span class="curid"><a href="/jme3/rotate.html" class="wikilink1" title="jme3:rotate">rotate</a></span>, <a href="/doku.php/jme3:scale" class="wikilink2" title="jme3:scale" rel="nofollow">scale</a>, and <a href="/doku.php/jme3:translate" class="wikilink2" title="jme3:translate" rel="nofollow">translate</a>.
</p>

<p>
You can do all transformations in individual steps (and then update the objects geometry and bounds), or you can combine them and transform the object in one step. If you have a lot of repetitive movement going on in your game it's worth learning more about Transformation Matrices for optimization. JME can also help you interpolate the steps between two fixed transformations.
</p>

<p>
<br />

</p>
<ul>
<li class="level1"><div class="li"> com.jme3.math.Transform, interpolateTransforms() – interpolate a step between two transformations</div>
<ul>
<li class="level2"><div class="li"> <a href="http://www.jmonkeyengine.com/doc/com/jme/math/TransformMatrix.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/TransformMatrix.html" rel="nofollow">com.jme.math.TransformMatrix</a></div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Tip: Transformation Matrix" [5114-] -->
