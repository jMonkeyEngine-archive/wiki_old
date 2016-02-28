---
title: Matrix
---
<h2 class="sectionedit1" id="matrix">Matrix</h2>
<div class="level2">

<p>
See <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Matrix3f.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Matrix3f.html" rel="nofollow">Javadoc of Matrix3f</a><br />

and <a href="http://www.jmonkeyengine.com/doc/com/jme/math/Matrix4f.html" class="urlextern" title="http://www.jmonkeyengine.com/doc/com/jme/math/Matrix4f.html" rel="nofollow">Javadoc of Matrix4f</a>
</p>

</div>
<!-- EDIT1 SECTION "Matrix" [1-197] -->
<h3 class="sectionedit2" id="definition">Definition</h3>
<div class="level3">

<p>
A Matrix is typically used as a <em>linear transformation</em> to map vectors to vectors. That is: Y = MX where X is a Vector and M is a Matrix applying any or all transformations (scale, rotate, translate). 
</p>

<p>
There are a few special matrices: 
</p>

<p>
<em>zero matrix</em> is the Matrix with all zero entries.
</p>
<div class="table sectionedit3"><table class="inline">
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
<!-- EDIT3 TABLE [512-536] -->
<p>
The <em>Identity Matrix</em> is the matrix with 1 on the diagonal entries and 0 for all other entries.
</p>
<div class="table sectionedit4"><table class="inline">
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
<!-- EDIT4 TABLE [636-660] -->
<p>
A Matrix is <em>invertible</em> if there is a matrix <em>M<sup>-1</sup></em> where <em>MM<sup>-1</sup> = M<sup>-1</sup> = I</em>. 
</p>

<p>
The <em>transpose</em> of a matrix <em>M = [m<sub>ij</sub>]</em> is <em>M<sup>T</sup> = [m<sub>ji</sub>]</em>. This causes the rows of <em>M</em> to become the columns of <em>M<sup>T</sup></em>.
</p>
<div class="table sectionedit5"><table class="inline">
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
<!-- EDIT5 TABLE [950-1016] -->
<p>
A Matrix is symmetric if <em>M</em> = <em>M<sup>T</sup></em>.
</p>
<div class="table sectionedit6"><table class="inline">
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
<!-- EDIT6 TABLE [1070-1096] -->
<p>
Where X, A, B, and C equal numbers 
</p>

<p>
jME includes two types of Matrix classes: Matrix3f and Matrix4f. Matrix3f is a 3×3 matrix and is the most commonly used (able to handle scaling and rotating), while Matrix4f is a 4×4 matrix that can also handle translation.
</p>

</div>
<!-- EDIT2 SECTION "Definition" [198-1358] -->
<h3 class="sectionedit7" id="transformations">Transformations</h3>
<div class="level3">

<p>
Multiplying a <a href="/doku.php/jme3:vector" class="wikilink2" title="jme3:vector" rel="nofollow">Vector</a> with a Matrix allows the <a href="/doku.php/jme3:vector" class="wikilink2" title="jme3:vector" rel="nofollow">Vector</a> to be transformed. Either rotating, scaling or translating that <a href="/doku.php/jme3:vector" class="wikilink2" title="jme3:vector" rel="nofollow">Vector</a>.
</p>

</div>

<h4 id="scaling">Scaling</h4>
<div class="level4">

<p>
If a <em>diagonal Matrix</em>, defined by D = [d<sub>ij</sub>] and d<sub>ij</sub> = 0 for i != j, has all positive entries it is a <em>scaling matrix</em>. If d<sub>i</sub> is greater than 1 then the resulting <a href="/doku.php/jme3:vector" class="wikilink2" title="jme3:vector" rel="nofollow">Vector</a> will grow, while if d<sub>i</sub> is less than 1 it will shrink.
</p>

</div>

<h4 id="rotation">Rotation</h4>
<div class="level4">

<p>
A <em>rotation matrix</em> requires that the transpose and inverse are the same matrix (R<sup>-1</sup> = R<sup>T</sup>). The <em>rotation matrix</em> R can then be calculated as: R = I + (sin(angle)) S + (1 - cos(angle)S<sup>2</sup> where S is:
</p>
<div class="table sectionedit8"><table class="inline">
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
<!-- EDIT8 TABLE [2066-2164] -->
</div>

<h4 id="translation">Translation</h4>
<div class="level4">

<p>
Translation requires a 4×4 matrix, where the <a href="/doku.php/jme3:vector" class="wikilink2" title="jme3:vector" rel="nofollow">Vector</a> (x,y,z) is mapped to (x,y,z,1) for multiplication. The <em>Translation Matrix</em> is then defined as:
</p>
<div class="table sectionedit9"><table class="inline">
	<tr class="row0">
		<td class="col0">M</td><td class="col1">T</td>
	</tr>
	<tr class="row1">
		<td class="col0">S<sup>T</sup></td><td class="col1">1</td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [2340-2363] -->
<p>
where M is the 3×3 matrix (containing any rotation/scale information), T is the translation <a href="/doku.php/jme3:vector" class="wikilink2" title="jme3:vector" rel="nofollow">Vector</a> and S<sup>T</sup> is the transpose Vector of T. 1 is just a constant.
</p>

</div>
<!-- EDIT7 SECTION "Transformations" [1359-2539] -->
<h3 class="sectionedit10" id="jme_class">jME Class</h3>
<div class="level3">

<p>
Both Matrix3f and Matrix4f store their values as floats and are publicly available as (m00, m01, m02, …, mNN) where N is either 2 or 3. 
</p>

<p>
Most methods are straight forward, and I will leave documentation to the Javadoc. 
</p>

</div>
<!-- EDIT10 SECTION "jME Class" [2540-] -->
