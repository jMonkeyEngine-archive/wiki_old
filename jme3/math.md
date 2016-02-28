---
title: Introduction to Mathematical Functionality
---
<h1 class="sectionedit1" id="introduction_to_mathematical_functionality">Introduction to Mathematical Functionality</h1>
<div class="level1">

<p>
It's a fact of life, math is hard. Unfortunately, 3D graphics require a fair bit of knowledge about the subject. Fortunately, jME is able to hide the majority of the details away from the user. Vectors are the fundamental type in the 3D environment, and it is used extensively. Matrices are also a basic necessity of 3D for representing linear systems. <a href="/jme3/quaternion.html" class="wikilink1" title="jme3:quaternion">Quaternion</a>s are perhaps the most powerful and complicated of the basic types and are used for rotation in jME. 
</p>

<p>
I'll discuss how these are used in the system for the core functionality. Including Transforming, Visibility Determination, Collision Detection, and the Coordinate System. Note, that these are low level details. Further chapters will discuss how to use these various systems from a high level perspective.
</p>

<p>
To get a visual introduction to math in jME3 for the absolute beginner, check out our <a href="/jme3/math_for_dummies.html" class="wikilink1" title="jme3:math_for_dummies">Math for Dummies</a> introduction class.
</p>

</div>
<!-- EDIT1 SECTION "Introduction to Mathematical Functionality" [1-961] -->
<h2 class="sectionedit2" id="coordinate_system">Coordinate System</h2>
<div class="level2">

</div>
<!-- EDIT2 SECTION "Coordinate System" [962-992] -->
<h3 class="sectionedit3" id="definition">Definition</h3>
<div class="level3">

<p>
A <em>coordinate system</em> consists of an origin (single point in space) and three coordinate axes that are each unit length and mutually perpendicular. The axes can be written as the column of a Matrix, R = [U1|U2|U3]. In fact, this is exactly how CameraNode works. The coordinate system defined by Camera is stored in a Matrix.
</p>

<p>
jME uses a Right-Handed coordinate system (as OpenGL does).
</p>

<p>
The definition of a coordinate system is defined in jME by the properties sent to Camera. There are no error checks to insure that: 1) the coordinate system is right-handed and 2) The axes are mutually perpendicular. Therefore, if the user sets the axes incorrectly, they are going to experience very odd rendering artifacts (random culling, etc).
</p>

<p>
<a href="/resources/jme3-intermediate-coordinate-system.png" class="media" title="jme3:intermediate:coordinate-system.png"><img src="/resources/jme3-intermediate-coordinate-system.png" class="mediacenter" alt="" width="235" height="210" /></a>
</p>

</div>
<!-- EDIT3 SECTION "Definition" [993-1806] -->
<h3 class="sectionedit4" id="homogenous_coordinates">Homogenous coordinates</h3>
<div class="level3">

<p>
Homogenous coordinates have an additional <em>W</em> value tacked on to the end. The XYZ values are to be divided by W to give the true coordinates.
</p>

<p>
This has several advantages, one technical, some relevant to application programmers:
</p>

<p>
Technically, it simplifies some formulae used inside the vector math. For example, some operations need to apply the same factor to the XYZ coordinates. Chain multiple operations of that kind (and vector math tends to do that), and you can save a lot of multiplications by simply keeping the scaling factor around and doing the multiplication to XYZ at the end of the pipeline, in the 3D card (which does accept homogenous coordinates).
It also simplifies some formulae, in particular anything that is related to rotations.
</p>

<p>
For application programmers, this means you can express infinitely long vectors that still have a direction - these tend to be used in lighting. Just use a W value of 0.0.
</p>

</div>
<!-- EDIT4 SECTION "Homogenous coordinates" [1807-2767] -->
<h2 class="sectionedit5" id="transformations">Transformations</h2>
<div class="level2">

<p>
Transformations define an operation that converts points from one coordinate system to another. This includes translation, rotation and scaling. In jME, local transforms are used to represent the positioning of objects relative to a parent coordinate system. While, world transforms are used to represent the positioning of objects in a global coordinate system.
</p>

</div>
<!-- EDIT5 SECTION "Transformations" [2768-3160] -->
<h2 class="sectionedit6" id="visibility_determination">Visibility Determination</h2>
<div class="level2">

<p>
Visibility Determination concerns itself with minimizing the amount of data that is sent to the graphics card for rendering. Specifically, we do not want to send data that will not be seen. Data not sent to the graphics card is said to be culled. The primary focus of this section is Frustum Culling based on the Camera's view frustum. In essence, this frustum creates six standard view planes. The BoundingVolume of an object is tested against the frustum planes to determine if it is contained in the frustum. If at any point the object's bounding is outside of the plane, it is tossed out and no longer processed for rendering. This also includes any children that it managed, allowing fast culling of large sections of the scene.
</p>

</div>
<!-- EDIT6 SECTION "Visibility Determination" [3161-3933] -->
<h1 class="sectionedit7" id="fundamental_types">Fundamental Types</h1>
<div class="level1">

</div>
<!-- EDIT7 SECTION "Fundamental Types" [3934-3966] -->
<h2 class="sectionedit8" id="colorrgba">ColorRGBA</h2>
<div class="level2">

</div>
<!-- EDIT8 SECTION "ColorRGBA" [3967-3987] -->
<h3 class="sectionedit9" id="definition1">Definition</h3>
<div class="level3">

<p>
ColorRGBA defines a color value in the jME library. The color value is made of three components, red, green and blue. A fourth component defines the alpha value (transparent) of the color. Every value is set between [0, 1]. Anything less than 0 will be clamped to 0 and anything greater than 1 will be clamped to 1.
</p>

<p>
<strong>Note:</strong> If you would like to “convert” an ordinary RGB value (0-255) to the format used here (0-1), simply multiply it with: 1/255.
</p>

</div>
<!-- EDIT9 SECTION "Definition" [3988-4459] -->
<h3 class="sectionedit10" id="jme_class">jME Class</h3>
<div class="level3">

<p>
ColorRGBA defines a few static color values for ease of use. That is, rather than:
</p>
<pre class="code java">ColorRGBA red <span class="sy0">=</span> <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
object.<span class="me1">setSomeColor</span><span class="br0">(</span>red<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
you can simply say:
</p>
<pre class="code java">object.<span class="me1">setSomeColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">red</span><span class="br0">)</span></pre>

<p>
ColorRGBA will also handle interpolation between two colors. Given a second color and a value between 0 and 1, a the owning ColorRGBA object will have its color values altered to this new interpolated color.
</p>

</div>
<!-- EDIT10 SECTION "jME Class" [4460-4934] -->
<h2 class="sectionedit11" id="matrix">Matrix</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Matrix3f.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Matrix3f.html" rel="nofollow">Matrix3f Javadoc</a><br />

and <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Matrix4f.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Matrix4f.html" rel="nofollow">Matrix4f Javadoc</a>
</p>

</div>
<!-- EDIT11 SECTION "Matrix" [4935-5125] -->
<h3 class="sectionedit12" id="definition2">Definition</h3>
<div class="level3">

<p>
A Matrix is typically used as a <em>linear transformation</em> to map vectors to vectors. That is: Y = MX where X is a Vector and M is a Matrix applying any or all transformations (scale, <a href="/jme3/rotate.html" class="wikilink1" title="jme3:rotate">rotate</a>, translate). 
</p>

<p>
There are a few special matrices: 
</p>

<p>
<em>zero matrix</em> is the Matrix with all zero entries.
</p>
<div class="table sectionedit13"><table class="inline">
	<tr class="row0">
		<td class="col0">0</td><td class="col1">0</td><td class="col2">0</td>
	</tr>
	<tr class="row1">
		<td class="col0">0</td><td class="col1">0</td><td class="col2">0</td>
	</tr>
	<tr class="row2">
		<td class="col0">0</td><td class="col1">0</td><td class="col2">0</td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [5444-5468] -->
<p>
The <em>Identity Matrix</em> is the matrix with 1 on the diagonal entries and 0 for all other entries.
</p>
<div class="table sectionedit14"><table class="inline">
	<tr class="row0">
		<td class="col0">1</td><td class="col1">0</td><td class="col2">0</td>
	</tr>
	<tr class="row1">
		<td class="col0">0</td><td class="col1">1</td><td class="col2">0</td>
	</tr>
	<tr class="row2">
		<td class="col0">0</td><td class="col1">0</td><td class="col2">1</td>
	</tr>
</table></div>
<!-- EDIT14 TABLE [5568-5592] -->
<p>
A Matrix is <em>invertible</em> if there is a matrix <em>M<sup>-1</sup></em> where <em>MM<sup>-1</sup> = M<sup>-1</sup>M = I</em>. 
</p>

<p>
The <em>transpose</em> of a matrix <em>M = [m<sub>ij</sub>]</em> is <em>M<sup>T</sup> = [m<sub>ji</sub>]</em>. This causes the rows of <em>M</em> to become the columns of <em>M<sup>T</sup></em>.
</p>
<div class="table sectionedit15"><table class="inline">
	<tr class="row0">
		<td class="col0">1</td><td class="col1">1</td><td class="col2">1</td><td class="col3 leftalign">    </td><td class="col4">1</td><td class="col5">2</td><td class="col6">3</td>
	</tr>
	<tr class="row1">
		<td class="col0">2</td><td class="col1">2</td><td class="col2">2</td><td class="col3"> ⇒ </td><td class="col4">1</td><td class="col5">2</td><td class="col6">3</td>
	</tr>
	<tr class="row2">
		<td class="col0">3</td><td class="col1">3</td><td class="col2">3</td><td class="col3 leftalign">    </td><td class="col4">1</td><td class="col5">2</td><td class="col6">3</td>
	</tr>
</table></div>
<!-- EDIT15 TABLE [5883-5949] -->
<p>
A Matrix is symmetric if <em>M</em> = <em>M<sup>T</sup></em>.
</p>
<div class="table sectionedit16"><table class="inline">
	<tr class="row0">
		<td class="col0">X</td><td class="col1">A</td><td class="col2">B</td>
	</tr>
	<tr class="row1">
		<td class="col0">A</td><td class="col1">X</td><td class="col2">C</td>
	</tr>
	<tr class="row2">
		<td class="col0">B</td><td class="col1">C</td><td class="col2">X</td>
	</tr>
</table></div>
<!-- EDIT16 TABLE [6003-6029] -->
<p>
Where X, A, B, and C equal numbers 
</p>

<p>
jME includes two types of Matrix classes: Matrix3f and Matrix4f. Matrix3f is a 3×3 matrix and is the most commonly used (able to handle scaling and rotating), while Matrix4f is a 4×4 matrix that can also handle translation.
</p>

</div>
<!-- EDIT12 SECTION "Definition" [5126-6291] -->
<h3 class="sectionedit17" id="transformations1">Transformations</h3>
<div class="level3">

<p>
Multiplying a vector with a Matrix allows the vector to be transformed. Either rotating, scaling or translating that vector.
</p>

</div>

<h4 id="scaling">Scaling</h4>
<div class="level4">

<p>
If a <em>diagonal Matrix</em>, defined by D = [d<sub>ij</sub>] and d<sub>ij</sub> = 0 for i != j, has all positive entries it is a <em>scaling matrix</em>. If d<sub>i</sub> is greater than 1 then the resulting vector will grow, while if d<sub>i</sub> is less than 1 it will shrink.
</p>

</div>

<h4 id="rotation">Rotation</h4>
<div class="level4">

<p>
A <em>rotation matrix</em> requires that the transpose and inverse are the same matrix (R<sup>-1</sup> = R<sup>T</sup>). The <em>rotation matrix</em> R can then be calculated as: R = I + (sin(angle)) S + (1 - cos(angle)S<sup>2</sup> where S is:
</p>
<div class="table sectionedit18"><table class="inline">
	<tr class="row0">
		<td class="col0">0</td><td class="col1">u<sub>2</sub></td><td class="col2">-u<sub>1</sub></td>
	</tr>
	<tr class="row1">
		<td class="col0">-u<sub>2</sub></td><td class="col1">0</td><td class="col2">u<sub>0</sub></td>
	</tr>
	<tr class="row2">
		<td class="col0">u<sub>1</sub></td><td class="col1">-u<sub>0</sub></td><td class="col2">0</td>
	</tr>
</table></div>
<!-- EDIT18 TABLE [6983-7081] -->
</div>

<h4 id="translation">Translation</h4>
<div class="level4">

<p>
Translation requires a 4×4 matrix, where the vector (x,y,z) is mapped to (x,y,z,1) for multiplication. The <em>Translation Matrix</em> is then defined as:
</p>
<div class="table sectionedit19"><table class="inline">
	<tr class="row0">
		<td class="col0">M</td><td class="col1">T</td>
	</tr>
	<tr class="row1">
		<td class="col0">S<sup>T</sup></td><td class="col1">1</td>
	</tr>
</table></div>
<!-- EDIT19 TABLE [7253-7276] -->
<p>
where M is the 3×3 matrix (containing any rotation/scale information), T is the translation vector and S<sup>T</sup> is the transpose Vector of T. 1 is just a constant.
</p>

</div>
<!-- EDIT17 SECTION "Transformations" [6292-7448] -->
<h3 class="sectionedit20" id="jme_class1">jME Class</h3>
<div class="level3">

<p>
Both Matrix3f and Matrix4f store their values as floats and are publicly available as (m00, m01, m02, …, mNN) where N is either 2 or 3. 
</p>

<p>
Most methods are straight forward, and I will leave documentation to the Javadoc. 
</p>

</div>
<!-- EDIT20 SECTION "jME Class" [7449-7691] -->
<h2 class="sectionedit21" id="vector">Vector</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Vector3f.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Vector3f.html" rel="nofollow">Vector3f Javadoc</a><br />

and <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Vector2f.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Vector2f.html" rel="nofollow">Vector2f Javadoc</a>
</p>

</div>
<!-- EDIT21 SECTION "Vector" [7692-7882] -->
<h3 class="sectionedit22" id="definition3">Definition</h3>
<div class="level3">

<p>
Vectors are used to represent a multitude of things in jME, points in space, vertices in a triangle mesh, normals, etc. These classes (Vector3f in particular) are probably the most used class in jME.
</p>

<p>
A Vector is defined by an n-tuple of real numbers. <strong>V</strong> = &lt;V<sub>1</sub>, V<sub>2</sub>,…, V<sub>n</sub>&gt;.
</p>

<p>
We have two Vectors (2f and 3f) meaning we have tuples of 2 float values or 3 float values.
</p>

</div>
<!-- EDIT22 SECTION "Definition" [7883-8307] -->
<h3 class="sectionedit23" id="operations">Operations</h3>
<div class="level3">

</div>

<h4 id="multiplication_by_scalar">Multiplication by Scalar</h4>
<div class="level4">

<p>
A Vector can be multiplied by a scalar value to produce a second Vector with the same proportions as the first. a<strong>V</strong> = <strong>V</strong>a = &lt;aV<sub>1</sub>, aV<sub>2</sub>,…,aV<sub>n</sub>&gt;
</p>

</div>

<h4 id="addition_and_subtraction">Addition and Subtraction</h4>
<div class="level4">

<p>
Adding or subtracting two Vectors occurs component-wise. That is the first component is added (subtracted) with the first component of the second Vector and so on.
</p>

<p>
<strong>P</strong> + <strong>Q</strong> = &lt;P<sub>1</sub>+Q<sub>1</sub>, P<sub>2</sub>+Q<sub>2</sub>, …, P<sub>n</sub>+Q<sub>n</sub>&gt;
</p>

</div>

<h4 id="magnitude">Magnitude</h4>
<div class="level4">

<p>
The <em>magnitude</em> defines the length of a Vector. A Vector of magnitude 1 is <em>unit length</em>.
</p>

<p>
For example, if <strong>V</strong> = (x, y, z), the magnitude is the square root of (x<sup>2</sup> + y<sup>2</sup> + z<sup>2</sup>).
</p>

<p>
A Vector can be <em>normalized</em> or made <em>unit length</em> by multiplying the Vector by (1/magnitude).
</p>

</div>

<h4 id="dot_products">Dot Products</h4>
<div class="level4">

<p>
The dot product of two vectors is defined as: 
<strong>P</strong> dot <strong>Q</strong> = P<sub>x</sub>Q<sub>x</sub> + P<sub>y</sub>Q<sub>y</sub> + P<sub>z</sub>Q<sub>z</sub>
</p>

<p>
Using the dot product allows us to determine how closely two Vectors are pointing to the same point. If the dot product is negative they are facing in relatively opposite directions, while postive tells us they are pointing in the relative same direction.
</p>

<p>
If the dot product is 0 then the two Vectors are <em>orthogonal</em> or 90 degrees off.
</p>

</div>

<h4 id="cross_product">Cross Product</h4>
<div class="level4">

<p>
The Cross Product of two Vectors returns a third Vector that is prependicular to the two Vectors. This is very useful for calculating surface normals.
</p>

<p>
<strong>P</strong> X <strong>Q</strong> = &lt;P<sub>y</sub>Q<sub>z</sub> - P<sub>z</sub>Q<sub>y</sub>, P<sub>z</sub>Q<sub>x</sub> - P<sub>x</sub>Q<sub>z</sub>, P<sub>x</sub>Q<sub>y</sub> - P<sub>y</sub>Q<sub>x</sub>&gt;
</p>

</div>

<h4 id="jme_class2">jME Class</h4>
<div class="level4">

<p>
Vector3f and Vector2f store their values (x, y, z) and (x, y) respectively as floats. Most methods are straight forward, and I will leave documentation to the Javadoc.
</p>

</div>
<!-- EDIT23 SECTION "Operations" [8308-10243] -->
<h2 class="sectionedit24" id="quaternion">Quaternion</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Quaternion.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Quaternion.html" rel="nofollow">Quaternion Javadoc</a>
</p>

</div>
<!-- EDIT24 SECTION "Quaternion" [10244-10356] -->
<h3 class="sectionedit25" id="definition4">Definition</h3>
<div class="level3">

<p>
Quaternions define a subset of a hypercomplex number system. Quaternions are defined by (i<sup>2</sup> = j<sup>2</sup> = k<sup>2</sup> = ijk = -1). jME makes use of Quaternions because they allow for compact representations of rotations, or correspondingly, orientations, in 3D space. With only four float values, we can represent an object's orientation, where a rotation matrix would require nine. They also require fewer arithmetic operations for concatenation. 
</p>

<p>
Additional benefits of the Quaternion is reducing the chance of <a href="http://en.wikipedia.org/wiki/Gimbal_lock" class="urlextern" title="http://en.wikipedia.org/wiki/Gimbal_lock" rel="nofollow">Gimbal Lock</a> and allowing for easily interpolation between two rotations (spherical linear interpolation or slerp).
</p>

<p>
While Quaternions are quite difficult to fully understand, there are an exceeding number of convenience methods to allow you to use them without having to understand the math behind it. Basically, these methods involve nothing more than setting the Quaternion's x,y,z,w values using other means of representing rotations. The Quaternion is then contained in the <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a> as its local rotation component.
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
<!-- EDIT25 SECTION "Definition" [10357-12525] -->
<h3 class="sectionedit26" id="angle_axis">Angle Axis</h3>
<div class="level3">

<p>
You might wish to represent your rotations as Angle Axis pairs. That is, you define a axis of rotation and the angle with which to <a href="/jme3/rotate.html" class="wikilink1" title="jme3:rotate">rotate</a> about this axis. <a href="/jme3/quaternion.html" class="wikilink1" title="jme3:quaternion">Quaternion</a> defines a method <code>fromAngleAxis</code> (and <code>fromAngleNormalAxis</code>) to create a Quaternion from this pair. This is acutally used quite a bit in jME demos to continually rotate objects. You can also obtain a Angle Axis rotation from an existing Quaternion using <code>toAngleAxis</code>.
</p>

</div>

<h4 id="example_-_rotate_a_spatial_using_fromangleaxis">Example - Rotate a Spatial Using fromAngleAxis</h4>
<div class="level4">
<pre class="code java"><span class="co1">//rotate about the Y-Axis by approximately 1 pi</span>
Vector3f axis <span class="sy0">=</span> Vector3f.<span class="me1">UNIT_Y</span><span class="sy0">;</span> 
<span class="co1">// UNIT_Y equals (0,1,0) and does not require to create a new object</span>
<span class="kw4">float</span> angle <span class="sy0">=</span> 3.14f<span class="sy0">;</span>
s.<span class="me1">getLocalRotation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span>angle, axis<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT26 SECTION "Angle Axis" [12526-13291] -->
<h3 class="sectionedit27" id="three_angles">Three Angles</h3>
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
<!-- EDIT27 SECTION "Three Angles" [13292-13841] -->
<h3 class="sectionedit28" id="three_axes">Three Axes</h3>
<div class="level3">

<p>
If you have three axes that define your rotation, where the axes define the left axis, up axis and directional axis respectively) you can make use of <code>fromAxes</code> to generate the Quaternion. It should be noted that this will generate a new <a href="/jme3/matrix.html" class="wikilink1" title="jme3:matrix">Matrix</a> object that is then garbage collected, thus, this method should not be used if it will be called many times. Again, <code>toAxes</code> will populate a Vector3f array.
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
<!-- EDIT28 SECTION "Three Axes" [13842-14588] -->
<h3 class="sectionedit29" id="rotation_matrix">Rotation Matrix</h3>
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
<!-- EDIT29 SECTION "Rotation Matrix" [14589-15493] -->
<h3 class="sectionedit30" id="slerp">Slerp</h3>
<div class="level3">

<p>
One of the biggest advantages to using Quaternions is allowing interpolation between two rotations. That is, if you have an initial Quaternion representing the original orientation of an object, and you have a final Quaternion representing the orientation you want the object to face, you can do this very smoothly with slerp. Simply supply the time, where time is [0, 1] and 0 is the initial rotation and 1 is the final rotation.
</p>

</div>

<h4 id="example_-_use_slerp_to_rotate_between_two_quaternions">Example - Use Slerp to Rotate Between two Quaternions</h4>
<div class="level4">
<pre class="code java"><span class="coMULTI">/*
You can interpolate rotations between two quaternions using spherical linear
interpolation (slerp).
*/</span>
Quaternion Xroll45 <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Xroll45.<span class="me1">fromAngleAxis</span><span class="br0">(</span><span class="nu0">45</span> <span class="sy0">*</span> FastMath.<span class="me1">DEG_TO_RAD</span>, Vector3f.<span class="me1">UNIT_X</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//</span>
Quaternion Yroll45 <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Yroll45.<span class="me1">fromAngleAxis</span><span class="br0">(</span><span class="nu0">45</span> <span class="sy0">*</span> FastMath.<span class="me1">DEG_TO_RAD</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//the rotation half - way between these two</span>
 
Quaternion halfBetweenXroll45Yroll45 <span class="sy0">=</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
halfBetweenXroll45Yroll45.<span class="me1">slerp</span><span class="br0">(</span>Xroll45, Yroll45, 0.5f<span class="br0">)</span><span class="sy0">;</span>
geom2.<span class="me1">setLocalRotation</span><span class="br0">(</span>halfBetweenXroll45Yroll45<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT30 SECTION "Slerp" [15494-16552] -->
<h3 class="sectionedit31" id="multiplication">Multiplication</h3>
<div class="level3">

<p>
You can concatenate (add) rotations: This means you turn the object first around one axis, then around the other, in one step.
</p>
<pre class="code java">Quaternion myRotation <span class="sy0">=</span> pitch90.<span class="me1">mult</span><span class="br0">(</span>roll45<span class="br0">)</span><span class="sy0">;</span> <span class="coMULTI">/* pitch and roll */</span></pre>

<p>
To rotate a Vector3f around its origin by the Quaternion amount, use the multLocal method of the Quaternion:
</p>
<pre class="code java">Quaternion myRotation <span class="sy0">=</span> pitch90<span class="sy0">;</span>
Vector3f myVector <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
myRotation.<span class="me1">multLocal</span><span class="br0">(</span>myVector<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT31 SECTION "Multiplication" [16553-17027] -->
<h1 class="sectionedit32" id="utility_classes">Utility Classes</h1>
<div class="level1">

<p>
Along with the base Math classes, jME provides a number of Math classes to make development easier (and, hopefully, faster). Most of these classes find uses throughout the jME system internally. They can also prove beneficial to users as well.
</p>

</div>
<!-- EDIT32 SECTION "Utility Classes" [17028-17303] -->
<h2 class="sectionedit33" id="fast_math">Fast Math</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/FastMath.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/FastMath.html" rel="nofollow">FastMath Javadoc</a>
</p>

</div>
<!-- EDIT33 SECTION "Fast Math" [17304-17410] -->
<h3 class="sectionedit34" id="definition5">Definition</h3>
<div class="level3">

<p>
FastMath provides a number of convience methods, and where possible faster versions (although this can be at the sake of accuracy). 
</p>

</div>
<!-- EDIT34 SECTION "Definition" [17411-17564] -->
<h3 class="sectionedit35" id="usage">Usage</h3>
<div class="level3">

<p>
FastMath provides a number of constants that can help with general math equations. One important attribute is <code>USE_FAST_TRIG</code> if you set this to true, a look-up table will be used for trig functions rather than Java's standard Math library. This provides significant speed increases, but might suffer from accuracy so care should be taken.
</p>

<p>
There are five major categories of functions that FastMath provides.
</p>

</div>

<h4 id="trig_functions">Trig Functions</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li">cos and acos - provide <a href="http://en.wikipedia.org/wiki/cosine" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/cosine">cosine</a> and <a href="http://en.wikipedia.org/wiki/arc cosine" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/arc cosine">arc cosine</a> values (make use of the look-up table if <code>USE_FAST_TRIG</code> is true)</div>
</li>
<li class="level1"><div class="li">sin and asin - provide <a href="http://en.wikipedia.org/wiki/sine" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/sine">sine</a> and <a href="http://en.wikipedia.org/wiki/arc sine" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/arc sine">arc sine</a> values (make use of the look-up table if <code>USE_FAST_TRIG</code> is true)</div>
</li>
<li class="level1"><div class="li">tan and atan - provide <a href="http://en.wikipedia.org/wiki/tangent" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/tangent">tangent</a> and <a href="http://en.wikipedia.org/wiki/arc tangent" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/arc tangent">arc tangent</a> values</div>
</li>
</ul>

</div>

<h4 id="numerical_methods">Numerical Methods</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li">ceil - provides the ceiling (smallest value that is greater than or equal to a given value and an integer)of a value.</div>
</li>
<li class="level1"><div class="li">floor - provides the floor (largest value that is less than or equal to a given value and an integer) of a value.</div>
</li>
<li class="level1"><div class="li">exp - provides the <a href="http://en.wikipedia.org/wiki/euler number" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/euler number">euler number</a> (e) raised to the provided value.</div>
</li>
<li class="level1"><div class="li">sqr - provides the square of a value (i.e. value * value).</div>
</li>
<li class="level1"><div class="li">pow - provides the first given number raised to the second.</div>
</li>
<li class="level1"><div class="li">isPowerOfTwo - provides a boolean if a value is a power of two or not (e.g. 32, 64, 4).</div>
</li>
<li class="level1"><div class="li">abs - provides the <a href="http://en.wikipedia.org/wiki/absolute value" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/absolute value">absolute value</a> of a given number.</div>
</li>
<li class="level1"><div class="li">sign - provides the sign of a value (1 if positive, -1 if negative, 0 if 0). </div>
</li>
<li class="level1"><div class="li">log - provides the <a href="http://en.wikipedia.org/wiki/natural logarithm" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/natural logarithm">natural logarithm</a> of a value.</div>
</li>
<li class="level1"><div class="li">sqrt - provides the <a href="http://en.wikipedia.org/wiki/square root" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/square root">square root</a> of a value.</div>
</li>
<li class="level1"><div class="li">invSqrt - provides the inverse <a href="http://en.wikipedia.org/wiki/square root" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/square root">square root</a> of a value (1 / sqrt(value).</div>
</li>
</ul>

</div>

<h4 id="linear_algebra">Linear Algebra</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li">LERP - calculate the <a href="http://en.wikipedia.org/wiki/Linear interpolation" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/Linear interpolation">linear interpolation</a> of two points given a time between 0 and 1.</div>
</li>
<li class="level1"><div class="li">determinant - calculates the <a href="http://en.wikipedia.org/wiki/determinant" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/determinant">determinant</a> of a 4×4 matrix.</div>
</li>
</ul>

</div>

<h4 id="geometric_functions">Geometric Functions</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li">counterClockwise - given three points (defining a triangle), the winding is determined. 1 if counter-clockwise, -1 if clockwise and 0 if the points define a line.</div>
</li>
<li class="level1"><div class="li">pointInsideTriangle - calculates if a point is inside a triangle.</div>
</li>
<li class="level1"><div class="li">sphericalToCartesian - converts a point from <a href="http://en.wikipedia.org/wiki/spherical coordinates" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/spherical coordinates">spherical coordinates</a> to <a href="http://en.wikipedia.org/wiki/cartesian coordinates" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/cartesian coordinates">cartesian coordinates</a>.</div>
</li>
<li class="level1"><div class="li">cartesianToSpherical - converts a point from <a href="http://en.wikipedia.org/wiki/cartesian coordinates" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/cartesian coordinates">cartesian coordinates</a> to <a href="http://en.wikipedia.org/wiki/spherical coordinates" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/spherical coordinates">spherical coordinates</a>.</div>
</li>
</ul>

</div>

<h4 id="misc">Misc.</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li">newRandomFloat - obtains a random float.</div>
</li>
</ul>

</div>
<!-- EDIT35 SECTION "Usage" [17565-19986] -->
<h2 class="sectionedit36" id="line">Line</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Line.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Line.html" rel="nofollow">Line Javadoc</a>
</p>

</div>
<!-- EDIT36 SECTION "Line" [19987-20080] -->
<h3 class="sectionedit37" id="definition6">Definition</h3>
<div class="level3">

<p>
A line is a straight one-dimensional figure having no thickness and extending infinitely in both directions. A line is defined by two points <strong>A</strong> and <strong>B</strong> with the line passing through both.
</p>

</div>
<!-- EDIT37 SECTION "Definition" [20081-20294] -->
<h3 class="sectionedit38" id="usage1">Usage</h3>
<div class="level3">

<p>
jME defines a Line class that is defined by an origin and direction. In reality, this Line class is typically used as a <em>line segment</em>. Where the line is finite and contained between these two points.
</p>

<p>
<code>random</code> provides a means of generate a random point that falls on the line between the origin and direction points.
</p>

</div>
<!-- EDIT38 SECTION "Usage" [20295-20633] -->
<h3 class="sectionedit39" id="example_1_-_find_a_random_point_on_a_line">Example 1 - Find a Random Point on a Line</h3>
<div class="level3">
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+line"><span class="kw3">Line</span></a> l <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+line"><span class="kw3">Line</span></a><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">3</span>,<span class="nu0">2</span>,<span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f randomPoint <span class="sy0">=</span> l.<span class="me1">random</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT39 SECTION "Example 1 - Find a Random Point on a Line" [20634-20801] -->
<h2 class="sectionedit40" id="plane">Plane</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Plane.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Plane.html" rel="nofollow">Plane Javadoc</a>
</p>

</div>
<!-- EDIT40 SECTION "Plane" [20802-20898] -->
<h3 class="sectionedit41" id="definition7">Definition</h3>
<div class="level3">

<p>
A plane is defined by the equation <strong>N</strong> . (<strong>X</strong> - <strong>X<sub>0</sub></strong>) = 0 where <strong>N</strong> = (a, b, c) and passes through the point <strong>X<sub>0</sub></strong> = (x<sub>0</sub>, y<sub>0</sub>, z<sub>0</sub>). <strong>X</strong> defines another point on this plane (x, y, z).
</p>

<p>
<strong>N</strong> . (<strong>X</strong> - <strong>X<sub>0</sub></strong>) = 0 can be described as (<strong>N</strong> . <strong>X</strong>) + (<strong>N</strong> . -<strong>X<sub>0</sub></strong>) = 0 
</p>

<p>
or 
</p>

<p>
(ax + by + cz) + (-ax<sub>0</sub>-by<sub>0</sub>-cz<sub>0</sub>) = 0
</p>

<p>
where (-ax<sub>0</sub>-by<sub>0</sub>-cz<sub>0</sub>) = d 
</p>

<p>
Where d is the negative value of a point in the plane times the unit vector describing the orientation of the plane.
</p>

<p>
This gives us the general equation: (ax + by + cz + d = 0)
</p>

</div>
<!-- EDIT41 SECTION "Definition" [20899-21593] -->
<h3 class="sectionedit42" id="usage_in_jme">Usage in jME</h3>
<div class="level3">

<p>
jME defines the Plane as ax + by + cz = -d. Therefore, during creation of the plane, the normal of the plane (a,b,c) and the constant d is supplied.
</p>

<p>
The most common usage of Plane is <a href="/doku.php/jme3:introduction_to_the_camera" class="wikilink2" title="jme3:introduction_to_the_camera" rel="nofollow">Camera</a> frustum planes. Therefore, the primary purpose of Plane is to determine if a point is on the positive side, negative side, or intersecting a plane.
</p>

<p>
Plane defines the constants:
</p>
<ul>
<li class="level1"><div class="li"><code>NEGATIVE_SIDE</code> - represents a point on the opposite side to which the normal points.</div>
</li>
<li class="level1"><div class="li"><code>NO_SIDE</code> - represents a point that lays on the plane itself.</div>
</li>
<li class="level1"><div class="li"><code>POSITIVE_SIDE</code> - represents a point on the side to which the normal points.</div>
</li>
</ul>

<p>
These values are returned on a call to <code>whichSide</code>.
</p>

</div>
<!-- EDIT42 SECTION "Usage in jME" [21594-22312] -->
<h3 class="sectionedit43" id="example_1_-_determining_if_a_point_is_on_the_positive_side_of_a_plane">Example 1 - Determining if a Point is On the Positive Side of a Plane</h3>
<div class="level3">
<pre class="code java">Vector3f normal <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw4">float</span> constant <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span>.<span class="me1">dot</span><span class="br0">(</span>normal<span class="br0">)</span><span class="sy0">;</span>
Plane testPlane <span class="sy0">=</span> <span class="kw1">new</span> Plane<span class="br0">(</span>normal, constant<span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw4">int</span> side <span class="sy0">=</span> testPlane.<span class="me1">whichSide</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">2</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">if</span><span class="br0">(</span>side <span class="sy0">==</span> Plane.<span class="me1">NO_SIDE</span><span class="br0">)</span> <span class="br0">{</span>
   <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"This point lies on the plane"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT43 SECTION "Example 1 - Determining if a Point is On the Positive Side of a Plane" [22313-22687] -->
<h3 class="sectionedit44" id="example_2_-_for_the_layperson">Example 2 - For the Layperson</h3>
<div class="level3">

<p>
Using the standard constructor Plane(Vector3f normal, float constant), here is what you need to do to create a plane, and then use it to check which side of the plane a point is on.
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">test</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">java.util.logging.Logger</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme.math.*</span><span class="sy0">;</span>
 
<span class="co3">/**
 *@author Nick Wiggill
 */</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> TestPlanes
<span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw1">final</span> Logger logger <span class="sy0">=</span> Logger.<span class="me1">getLogger</span><span class="br0">(</span>LevelGraphBuilder.<span class="kw1">class</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a>
  <span class="br0">{</span>
    <span class="co1">//***Outline.</span>
    <span class="co1">//This example shows how to construct a plane representation using</span>
    <span class="co1">//com.jme.math.Plane.</span>
    <span class="co1">//We will create a very simple, easily-imagined 3D plane. It will</span>
    <span class="co1">//be perpendicular to the x axis (it's facing). It's "centre" (if</span>
    <span class="co1">//such a thing exists in an infinite plane) will be positioned 1</span>
    <span class="co1">//unit along the positive x axis.</span>
 
    <span class="co1">//***Step 1.</span>
    <span class="co1">//The vector that represents the normal to the plane, in 3D space.</span>
    <span class="co1">//Imagine a vector coming out of the origin in this direction.</span>
    <span class="co1">//There is no displacement yet (see Step 2, below).</span>
    Vector3f normal <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>5f,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">//***Step 2.</span>
    <span class="co1">//This is our displacement vector. The plane remains facing in the</span>
    <span class="co1">//direction we've specified using the normal above, but now we are</span>
    <span class="co1">//are actually giving it a position other than the origin.</span>
    <span class="co1">//We will use this displacement to define the variable "constant"</span>
    <span class="co1">//needed to construct the plane. (see step 3)</span>
    Vector3f displacement <span class="sy0">=</span> Vector3f.<span class="me1">UNIT_X</span><span class="sy0">;</span>
    <span class="co1">//or</span>
    <span class="co1">//Vector3f displacement = new Vector3f(1f, 0, 0);</span>
 
    <span class="co1">//***Step 3.</span>
    <span class="co1">//Here we generate the constant needed to define any plane. This</span>
    <span class="co1">//is semi-arcane, don't let it worry you. All you need to</span>
    <span class="co1">//do is use this same formula every time.</span>
    <span class="kw4">float</span> constant <span class="sy0">=</span> displacement.<span class="me1">dot</span><span class="br0">(</span>normal<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">//***Step 4.</span>
    <span class="co1">//Finally, construct the plane using the data you have assembled.</span>
    Plane plane <span class="sy0">=</span> <span class="kw1">new</span> Plane<span class="br0">(</span>normal, constant<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">//***Some tests.</span>
    logger.<span class="me1">info</span><span class="br0">(</span><span class="st0">"Plane info: "</span><span class="sy0">+</span>plane.<span class="me1">toString</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//trace our plane's information</span>
 
    Vector3f p1  <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>1.1f,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//beyond the plane (further from origin than plane)</span>
    Vector3f p2  <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>0.9f,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//before the plane (closer to origin than plane)</span>
    Vector3f p3  <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>1f,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//on the plane</span>
 
    logger.<span class="me1">info</span><span class="br0">(</span><span class="st0">"p1 position relative to plane is "</span><span class="sy0">+</span>plane.<span class="me1">whichSide</span><span class="br0">(</span>p1<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//outputs NEGATIVE</span>
    logger.<span class="me1">info</span><span class="br0">(</span><span class="st0">"p2 position relative to plane is "</span><span class="sy0">+</span>plane.<span class="me1">whichSide</span><span class="br0">(</span>p2<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//outputs POSITIVE</span>
    logger.<span class="me1">info</span><span class="br0">(</span><span class="st0">"p3 position relative to plane is "</span><span class="sy0">+</span>plane.<span class="me1">whichSide</span><span class="br0">(</span>p3<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//outputs NONE</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT44 SECTION "Example 2 - For the Layperson" [22688-25325] -->
<h2 class="sectionedit45" id="ray">Ray</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Ray.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Ray.html" rel="nofollow">Ray Javadoc</a>
</p>

</div>
<!-- EDIT45 SECTION "Ray" [25326-25416] -->
<h3 class="sectionedit46" id="definition8">Definition</h3>
<div class="level3">

<p>
Ray defines a line that starts at a point <strong>A</strong> and continues in a direction through <strong>B</strong> into infinity. 
</p>

<p>
This Ray is used extensively in jME for <a href="/doku.php/jme3:picking" class="wikilink2" title="jme3:picking" rel="nofollow">Picking</a>. A Ray is cast from a point in screen space into the scene. Intersections are found and returned. To create a ray supply the object with two points, where the first point is the origin.
</p>

</div>
<!-- EDIT46 SECTION "Definition" [25417-25783] -->
<h3 class="sectionedit47" id="example_1_-_create_a_ray_that_represents_where_the_camera_is_looking">Example 1 - Create a Ray That Represents Where the Camera is Looking</h3>
<div class="level3">
<pre class="code java">Ray ray <span class="sy0">=</span> <span class="kw1">new</span> Ray<span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span>, cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT47 SECTION "Example 1 - Create a Ray That Represents Where the Camera is Looking" [25784-25940] -->
<h2 class="sectionedit48" id="rectangle">Rectangle</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Rectangle.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Rectangle.html" rel="nofollow">Rectangle Javadoc</a>
</p>

</div>
<!-- EDIT48 SECTION "Rectangle" [25941-26049] -->
<h3 class="sectionedit49" id="definition9">Definition</h3>
<div class="level3">

<p>
Rectangle defines a finite plane within three dimensional space that is specified via three points (A, B, C). These three points define a triangle with the forth point defining the rectangle ( (B + C) - A ).
</p>

</div>
<!-- EDIT49 SECTION "Definition" [26050-26278] -->
<h3 class="sectionedit50" id="jme_usage">jME Usage</h3>
<div class="level3">

<p>
Rectangle is a straight forward data class that simply maintains values that defines a Rectangle in 3D space. One interesting use is the <code>random</code> method that will create a random point on the Rectangle. The <a href="/doku.php/jme3:particle_system" class="wikilink2" title="jme3:particle_system" rel="nofollow">Particle System</a> makes use of this to define an area that generates <a href="/doku.php/jme3:particles" class="wikilink2" title="jme3:particles" rel="nofollow">Particles</a>.
</p>

</div>
<!-- EDIT50 SECTION "jME Usage" [26279-26593] -->
<h3 class="sectionedit51" id="example_1define_a_rectangle_and_get_a_point_from_it">Example 1 : Define a Rectangle and Get a Point From It</h3>
<div class="level3">
<pre class="code java">Vector3f v1 <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f v2 <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f v3 <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+rectangle"><span class="kw3">Rectangle</span></a> r <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+rectangle"><span class="kw3">Rectangle</span></a><span class="br0">(</span>v1, v2, v3<span class="br0">)</span><span class="sy0">;</span>
Vector3f point <span class="sy0">=</span> r.<span class="me1">random</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT51 SECTION "Example 1 : Define a Rectangle and Get a Point From It" [26594-26853] -->
<h2 class="sectionedit52" id="triangle">Triangle</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Triangle.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Triangle.html" rel="nofollow">Triangle Javadoc</a>
</p>

</div>
<!-- EDIT52 SECTION "Triangle" [26854-26959] -->
<h3 class="sectionedit53" id="definition10">Definition</h3>
<div class="level3">

<p>
A triangle is a 3-sided polygon. Every triangle has three sides and three angles, some of which may be the same. If the triangle is a right triangle (one angle being 90 degrees), the side opposite the 90 degree angle is the hypotenuse, while the other two sides are the legs. All triangles are <a href="http://en.wikipedia.org/wiki/Convex_polygon" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/Convex_polygon">convex</a> and <a href="http://mathworld.wolfram.com/BicentricPolygon.html" class="urlextern" title="http://mathworld.wolfram.com/BicentricPolygon.html" rel="nofollow">bicentric</a>.
</p>

</div>
<!-- EDIT53 SECTION "Definition" [26960-27373] -->
<h3 class="sectionedit54" id="usage2">Usage</h3>
<div class="level3">

<p>
jME's Triangle class is a simple data class. It contains three <a href="/doku.php/jme3:vector" class="wikilink2" title="jme3:vector" rel="nofollow">Vector3f</a> objects that represent the three points of the triangle. These can be retrieved via the <code>get</code> method. The <code>get</code> method, obtains the point based on the index provided. Similarly, the values can be set via the <code>set</code> method.
</p>

</div>
<!-- EDIT54 SECTION "Usage" [27374-27700] -->
<h3 class="sectionedit55" id="example_1_-_creating_a_triangle">Example 1 - Creating a Triangle</h3>
<div class="level3">
<pre class="code java"><span class="co1">//the three points that make up the triangle</span>
Vector3f p1 <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f p2 <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f p3 <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
Triangle t <span class="sy0">=</span> <span class="kw1">new</span> Triangle<span class="br0">(</span>p1, p2, p3<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT55 SECTION "Example 1 - Creating a Triangle" [27701-27951] -->
<h1 class="sectionedit56" id="tips_and_tricks">Tips and Tricks</h1>
<div class="level1">

</div>
<!-- EDIT56 SECTION "Tips and Tricks" [27952-27982] -->
<h2 class="sectionedit57" id="how_do_i_get_height_width_of_a_spatial">How do I get height/width of a spatial?</h2>
<div class="level2">

<p>
Cast the spatial to com.jme3.bounding.BoundingBox to be able to use getExtent().
</p>
<pre class="code java">Vector3f extent <span class="sy0">=</span> <span class="br0">(</span><span class="br0">(</span>BoundingBox<span class="br0">)</span> spatial.<span class="me1">getWorldBound</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">getExtent</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw4">float</span> x <span class="sy0">=</span> <span class="br0">(</span> <span class="br0">(</span>BoundingBox<span class="br0">)</span>spatial.<span class="me1">getWorldBound</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">getXExtent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw4">float</span> y <span class="sy0">=</span> <span class="br0">(</span> <span class="br0">(</span>BoundingBox<span class="br0">)</span>spatial.<span class="me1">getWorldBound</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">getYExtent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw4">float</span> z <span class="sy0">=</span> <span class="br0">(</span> <span class="br0">(</span>BoundingBox<span class="br0">)</span>spatial.<span class="me1">getWorldBound</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">getZExtent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT57 SECTION "How do I get height/width of a spatial?" [27983-28413] -->
<h2 class="sectionedit58" id="how_do_i_position_the_center_of_a_geomtry">How do I position the center of a Geomtry?</h2>
<div class="level2">
<pre class="code java">geo.<span class="me1">center</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">move</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT58 SECTION "How do I position the center of a Geomtry?" [28414-28513] -->
<h3 class="sectionedit59" id="see_also">See Also</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/rotate.html" class="wikilink1" title="jme3:rotate">Rotate</a> </div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/quaternion.html" class="wikilink1" title="jme3:quaternion">Quaternion</a></div>
</li>
</ul>

</div>
<!-- EDIT59 SECTION "See Also" [28514-] -->
