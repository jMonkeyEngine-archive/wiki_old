---
title: Math Cheat Sheet
---
<h1 class="sectionedit1" id="math_cheat_sheet">Math Cheat Sheet</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Math Cheat Sheet" [1-31] -->
<h2 class="sectionedit2" id="formulas">Formulas</h2>
<div class="level2">

<p>
Note: Typically you have to string these formulas together. Look in the table for what you want, and what you have. If the two are not the same line, than you need conversion steps inbetween. E.g. if you have an angle in degrees, but the formula expects radians: 1) convert degrees to radians, 2) use the radians formula on the result.
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">I have…</th><th class="col1">I want…</th><th class="col2">Formula</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">normalized direction and length <br />
n1,d1</td><td class="col1">a vector that goes that far in that direction <br />
new direction vector v0</td><td class="col2">v0 = n1.mult(d1)</td>
	</tr>
	<tr class="row2">
		<td class="col0">point and direction vector <br />
p1,v1</td><td class="col1">to move the point <br />
new point p0</td><td class="col2">p0 = p1.add(v1)</td>
	</tr>
	<tr class="row3">
		<td class="col0"> direction, position and distance <br />
v1,p1,dist</td><td class="col1">Position at distance <br />
p2 </td><td class="col2">v1.normalzeLocal() <br />
scaledDir = v1.mult(dist) <br />
p2 = p1.add(scaledDir)</td>
	</tr>
	<tr class="row4">
		<td class="col0">two direction vectors or normals <br />
v1,v2</td><td class="col1">to combine both directions <br />
new direction vector v0</td><td class="col2">v0 = v1.add(v2)</td>
	</tr>
	<tr class="row5">
		<td class="col0">two points <br />
p1, p2</td><td class="col1">distance between two points <br />
new scalar d0</td><td class="col2">d0 = p1.subtract(p2).length() <br />
d0 = p1.distance(p2)</td>
	</tr>
	<tr class="row6">
		<td class="col0">two points <br />
p1, p2</td><td class="col1">the direction from p2 to p1 <br />
new direction vector v0</td><td class="col2">v0 = p1.substract(p2)</td>
	</tr>
	<tr class="row7">
		<td class="col0">two points, a fraction <br />
p1, p2, h=0.5f</td><td class="col1">the point “halfway” (h=0.5f) between the two points <br />
new interpolated point p0</td><td class="col2">p0 = FastMath.interpolateLinear(h,p1,p2)</td>
	</tr>
	<tr class="row8">
		<td class="col0">a direction vector, an up vector <br />
v, up</td><td class="col1">A rotation around this up axis towards this direction <br />
new Quaternion q</td><td class="col2">Quaternion q = new Quaternion(); <br />
q.lookAt(v,up)</td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [387-1459] --><div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">I have…</th><th class="col1">I want…</th><th class="col2">Formula</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">angle in degrees <br />
a </td><td class="col1"> to convert angle a from degrees to radians <br />
new float angle phi</td><td class="col2">phi = a / 180 * FastMath.PI; <br />
OR <br />
phi=a.mult(FastMath.DEG_TO_RAD); </td>
	</tr>
	<tr class="row2">
		<td class="col0">angle in radians <br />
phi </td><td class="col1"> to convert angle phi from radians to degrees <br />
new float angle a</td><td class="col2">a = phi * 180 / FastMath.PI </td>
	</tr>
	<tr class="row3">
		<td class="col0">radian angle and x axis <br />
phi, x </td><td class="col1">to rotate around x axis <br />
new quaternion q0</td><td class="col2">q0.fromAngleAxis( phi, Vector3f.UNIT_X )</td>
	</tr>
	<tr class="row4">
		<td class="col0">radian angle and y axis <br />
phi, y </td><td class="col1">to rotate around y axis <br />
new quaternion q0</td><td class="col2">q0.fromAngleAxis( phi, Vector3f.UNIT_Y )</td>
	</tr>
	<tr class="row5">
		<td class="col0">radian angle and z axis <br />
phi, z </td><td class="col1">to rotate around z axis <br />
new quaternion q0</td><td class="col2">q0.fromAngleAxis( phi, Vector3f.UNIT_Z )</td>
	</tr>
	<tr class="row6">
		<td class="col0">several quaternions <br />
q1, q2, q3</td><td class="col1">to combine rotations, in that order <br />
new quaternion q0</td><td class="col2">q0 = q1.mult(q2).mult(q3)</td>
	</tr>
	<tr class="row7">
		<td class="col0">point and quaternion <br />
p1, q1</td><td class="col1">to rotate the point around origin <br />
new point p0</td><td class="col2">p0 = q1.mult(p1)</td>
	</tr>
	<tr class="row8">
		<td class="col0">angle in radians and radius <br />
phi,r</td><td class="col1">to arrange or move objects horizontally in a circle (with y=0) <br />
x and z coordinates</td><td class="col2">float x = FastMath.cos(phi)*r; <br />
float z = FastMath.sin(phi)*r;</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [1461-2555] -->
</div>
<!-- EDIT2 SECTION "Formulas" [32-2556] -->
<h2 class="sectionedit5" id="local_vs_non-local_methods">Local vs Non-local methods?</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Non-local method creates new object as return value, v remains unchanged. <br />
<code>v2 = v.mult(); v2 = v.add(); v2 = v.subtract();</code> etc</div>
</li>
<li class="level1"><div class="li"> Local method changes v directly! <br />
<code>v.multLocal(); v.addLocal(); v.subtractLocal();</code> etc</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Local vs Non-local methods?" [2557-] -->
