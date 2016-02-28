---
title: Quaternion
---
<h2 class="sectionedit1" id="quaternion">Quaternion</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Quaternion.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Quaternion.html" rel="nofollow">Javadoc</a>
</p>

</div>
<!-- EDIT1 SECTION "Quaternion" [1-102] -->
<h3 class="sectionedit2" id="definition">Definition</h3>
<div class="level3">

<p>
Quaternions define a subset of a hypercomplex number system. Quaternions are defined by (i<sup>2</sup> = j<sup>2</sup> = k<sup>2</sup> = ijk = -1). jME makes use of Quaternions because they allow for compact representations of rotations, or correspondingly, orientations, in 3D space. With only four float values, we can represent an object's orientation, where a rotation matrix would require nine. They also require fewer arithmetic operations for concatenation. 
</p>

<p>
Additional benefits of the Quaternion is reducing the chance of <a href="http://en.wikipedia.org/wiki/Gimbal_lock" class="urlextern" title="http://en.wikipedia.org/wiki/Gimbal_lock" rel="nofollow">Gimbal Lock</a> and allowing for easily interpolation between two rotations (spherical linear interpolation or slerp).
</p>

<p>
While Quaternions are quite difficult to fully understand, there are an exceeding number of convenience methods to allow you to use them without having to understand the math behind it. Basically, these methods involve nothing more than setting the Quaternion's x,y,z,w values using other means of representing rotations. The Quaternion is then contained in <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a> as its local rotation component.
</p>

<p>
Quaternion <strong>q</strong> has the form
</p>

<p>
<strong>q</strong> = &lt;<em>w,x,y,z</em>&gt; = <em>w + xi + yj + zk</em>
</p>

<p>
or alternatively, it can be written as:
</p>

<p>
<strong>q</strong> = <strong>s</strong> + <strong>v</strong>, where <strong>s</strong> represents the scalar part corresponding to the w-component of <strong>q</strong>, and <strong>v</strong> represents the vector part of the (x, y, z) components of <strong>q</strong>.
</p>

<p>
Multiplication of Quaternions uses the distributive law and adheres to the following rules with multiplying the imaginary components (i, j, k):
</p>

<p>
<code>i<sup>2</sup> = j<sup>2</sup> = k<sup>2</sup> = -1</code><br />

<code>ij = -ji = k</code><br />

<code>jk = -kj = i</code><br />

<code>ki = -ik = j</code>
</p>

<p>
However, Quaternion multiplication is <em>not</em> commutative, so we have to pay attention to order.
</p>

<p>
<strong>q<sub>1</sub>q<sub>2</sub></strong> = s<sub>1</sub>s<sub>2</sub> - <strong>v<sub>1</sub></strong> dot <strong>v<sub>2</sub></strong> + s<sub>1</sub><strong>v<sub>2</sub></strong> + s<sub>2</sub><strong>v<sub>1</sub></strong> + <strong>v<sub>1</sub></strong> X <strong>v<sub>2</sub></strong>
</p>

<p>
Quaternions also have conjugates where the conjugate of <strong>q</strong> is (s - <strong>v</strong>)
</p>

<p>
These basic operations allow us to convert various rotation representations to Quaternions.
</p>

</div>
<!-- EDIT2 SECTION "Definition" [103-2268] -->
<h3 class="sectionedit3" id="angle_axis">Angle Axis</h3>
<div class="level3">

<p>
You might wish to represent your rotations as Angle Axis pairs. That is, you define a axis of rotation and the angle with which to rotate about this axis. Quaternion defines a method <code>fromAngleAxis</code> (and <code>fromAngleNormalAxis</code>) to create a Quaternion from this pair. This is acutally used quite a bit in jME demos to continually rotate objects. You can also obtain a Angle Axis rotation from an existing Quaternion using <code>toAngleAxis</code>.
</p>

</div>

<h4 id="example_-_rotate_a_spatial_using_fromangleaxis">Example - Rotate a Spatial Using fromAngleAxis</h4>
<div class="level4">
<pre class="code java"><span class="co1">//rotate about the Y-Axis by approximately 1 pi</span>
Vector3f axis <span class="sy0">=</span> Vector3f.<span class="me1">UNIT_Y</span><span class="sy0">;</span> <span class="co1">// this equals (0, 1, 0) and does not require to create a new object</span>
<span class="kw4">float</span> angle <span class="sy0">=</span> 3.14f<span class="sy0">;</span>
s.<span class="me1">getLocalRotation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span>angle, axis<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT3 SECTION "Angle Axis" [2269-3024] -->
<h3 class="sectionedit4" id="three_angles">Three Angles</h3>
<div class="level3">

<p>
You can also represent a rotation by defining three angles. The angles represent the rotation about the individual axes. Passing in a three-element array of floats defines the angles where the first element is X, second Y and third is Z. The method provided by Quaternion is <code>fromAngles</code> and can also fill an array using <code>toAngles</code>
</p>

</div>

<h4 id="example_-_rotate_a_spatial_using_fromangles">Example - Rotate a Spatial Using fromAngles</h4>
<div class="level4">
<pre class="code java"><span class="co1">//rotate 1 radian on the x, 3 on the y and 0 on z</span>
<span class="kw4">float</span><span class="br0">[</span><span class="br0">]</span> angles <span class="sy0">=</span> <span class="br0">{</span><span class="nu0">1</span>, <span class="nu0">3</span>, <span class="nu0">0</span><span class="br0">}</span><span class="sy0">;</span>
s.<span class="me1">getLocalRotation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngles</span><span class="br0">(</span>angles<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Three Angles" [3025-3573] -->
<h3 class="sectionedit5" id="three_axes">Three Axes</h3>
<div class="level3">

<p>
If you have three axes that define your rotation, where the axes define the left axis, up axis and directional axis respectively) you can make use of <code>fromAxes</code> to generate the Quaternion. It should be noted that this will generate a new <a href="/jme3/matrix.html" class="wikilink1" title="jme3:matrix">Matrix</a> object that is then garbage collected, thus, this method should not be used if it will be called many times. Again, <code>toAxes</code> will populate a <a href="/doku.php/jme3:vector" class="wikilink2" title="jme3:vector" rel="nofollow">Vector3f</a> array.
</p>

</div>

<h4 id="example_-_rotate_a_spatial_using_fromaxes">Example - Rotate a Spatial Using fromAxes</h4>
<div class="level4">
<pre class="code java"><span class="co1">//rotate a spatial to face up ~45 degrees</span>
Vector3f<span class="br0">[</span><span class="br0">]</span> axes <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">[</span><span class="nu0">3</span><span class="br0">]</span><span class="sy0">;</span>
axes<span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//left</span>
axes<span class="br0">[</span><span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, 0.5f, 0.5f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//up</span>
axes<span class="br0">[</span><span class="nu0">2</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, 0.5f, 0.5f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//dir</span>
 
s.<span class="me1">getLocalRotation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAxes</span><span class="br0">(</span>axes<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT5 SECTION "Three Axes" [3574-4330] -->
<h3 class="sectionedit6" id="rotation_matrix">Rotation Matrix</h3>
<div class="level3">

<p>
Commonly you might find yourself with a <a href="/jme3/matrix.html" class="wikilink1" title="jme3:matrix">Matrix</a> defining a rotation. In fact, it's very common to contain a rotation in a <a href="/jme3/matrix.html" class="wikilink1" title="jme3:matrix">Matrix</a> create a Quaternion, rotate the Quaternion, and then get the <a href="/jme3/matrix.html" class="wikilink1" title="jme3:matrix">Matrix</a> back. Quaternion contains a <code>fromRotationMatrix</code> method that will create the appropriate Quaternion based on the give <a href="/jme3/matrix.html" class="wikilink1" title="jme3:matrix">Matrix</a>. The <code>toRotationMatrix</code> will populate a given <a href="/jme3/matrix.html" class="wikilink1" title="jme3:matrix">Matrix</a>.
</p>

</div>

<h4 id="example_-_rotate_a_spatial_using_a_rotation_matrix">Example - Rotate a Spatial Using a Rotation Matrix</h4>
<div class="level4">
<pre class="code java">Matrix3f mat <span class="sy0">=</span> <span class="kw1">new</span> Matrix3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColumn</span><span class="br0">(</span><span class="nu0">0</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColumn</span><span class="br0">(</span><span class="nu0">1</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="sy0">-</span><span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColumn</span><span class="br0">(</span><span class="nu0">2</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
s.<span class="me1">getLocalRotation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromRotationMatrix</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
As you can see there are many ways to build a Quaternion. This allows you to work with rotations in a way that is conceptually easier to picture, but still build Quaternions for internal representation.
</p>

</div>
<!-- EDIT6 SECTION "Rotation Matrix" [4331-5234] -->
<h3 class="sectionedit7" id="slerp">Slerp</h3>
<div class="level3">

<p>
One of the biggest advantages to using Quaternions is allowing interpolation between two rotations. That is, if you have an initial Quaternion representing the original orientation of an object, and you have a final Quaternion representing the orientation you want the object to face, you can do this very smoothly with slerp. Simply supply the time, where time is [0, 1] and 0 is the initial rotation and 1 is the final rotation.
</p>

</div>

<h4 id="example_-_use_slerp_to_rotate_between_two_quaternions">Example - Use Slerp to Rotate Between two Quaternions</h4>
<div class="level4">
<pre class="code java">Quaternion q1<span class="sy0">;</span>
Quaternion q2<span class="sy0">;</span>
 
<span class="co1">//the rotation half-way between these two</span>
Quaternion q3 <span class="sy0">=</span> q1.<span class="me1">slerp</span><span class="br0">(</span>q2, 0.5f<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT7 SECTION "Slerp" [5235-] -->
