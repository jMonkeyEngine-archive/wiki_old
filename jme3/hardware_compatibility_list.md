---
title: General System Requirements for Applications Built with jMonkeyEngine
---
<p>
<br />

</p>

<p>
<img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" /> <strong>Please expand this list!</strong>
I've copied this page from the original jME2 hardware compatibility list and will work on getting this up to date for jME3 -Skye
</p>

<p>
<br />

This page lists the compatibility of various different graphic cards and the latest version of jME3
</p>

<p>
To fill in a new entry add the name of your graphics card in the first column (Card Name), which driver version the card is running on in the second column (Driver Version).  Then put a 'Y' for yes and a 'N' for no in the next three columns as to whether your card supports the given feature.
</p>
<ul>
<li class="level1"><div class="li"> Basic Features should be considered things like rendering primitive shapes and models fully textured and lit. </div>
</li>
<li class="level1"><div class="li"> Advanced Features should be considered things like Render to Texture and Cloth effects.</div>
</li>
<li class="level1"><div class="li"> Shader Features should be anything that uses shaders such as Bloom and Motion Blur.</div>
</li>
</ul>

<h2 class="sectionedit1" id="general_system_requirements_for_applications_built_with_jmonkeyengine">General System Requirements for Applications Built with jMonkeyEngine</h2>
<div class="level2">

<p>
Please see <a href="/jme3/requirements.html" class="wikilink1" title="jme3:requirements">requirements</a>
<br />

For a detailed list of Graphic Card/Driver combinations and which OpenGL features they support see <del><a href="http://www.delphi3d.net/hardware/index.php" class="urlextern" title="http://www.delphi3d.net/hardware/index.php" rel="nofollow">http://www.delphi3d.net/hardware/index.php</a></del> <a href="http://www.opengl.org/wiki/Hardware_specifics" class="urlextern" title="http://www.opengl.org/wiki/Hardware_specifics" rel="nofollow">http://www.opengl.org/wiki/Hardware_specifics</a>
</p>

</div>
<!-- EDIT1 SECTION "General System Requirements for Applications Built with jMonkeyEngine" [864-1174] -->
<h3 class="sectionedit2" id="ati_amd">ATI/AMD</h3>
<div class="level3">
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Card Name </th><th class="col1"> Driver Version </th><th class="col2"> Basic Features? </th><th class="col3"> Advanced Features (No Shader)? </th><th class="col4"> Shader Features? </th><th class="col5"> Notes </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Radeon HD 4850 512MB </td><td class="col1"> 11.8 running on Linux Mint 12 x64<br />
11.12 running on Windows 7 Professional x64</td><td class="col2">Y</td><td class="col3">Y</td><td class="col4">Y</td><td class="col5">All tests works fine.</td>
	</tr>
	<tr class="row2">
		<td class="col0"> Radeon HD 5850 1GB </td><td class="col1"> 11.12 running on Windows 7 Professional x64 </td><td class="col2">Y</td><td class="col3">Y</td><td class="col4">Y</td><td class="col5">All tests works fine.</td>
	</tr>
	<tr class="row3">
		<td class="col0"> Radeon HD 6900 2GB </td><td class="col1"> 11.5 running on Windows 7 x64 </td><td class="col2">Y</td><td class="col3">Y</td><td class="col4">Y</td><td class="col5">All tests works fine.</td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [1191-1613] -->
</div>
<!-- EDIT2 SECTION "ATI/AMD" [1175-1614] -->
<h3 class="sectionedit4" id="intel">Intel</h3>
<div class="level3">
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Card Name </th><th class="col1"> Driver Version </th><th class="col2"> Basic Features? </th><th class="col3"> Advanced Features (No Shader)? </th><th class="col4"> Shader Features? </th><th class="col5"> Notes </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Intel GMA 950 </td><td class="col1"> Mac <abbr title="Operating System">OS</abbr> X 10.5 </td><td class="col2">Y</td><td class="col3">Y</td><td class="col4">N</td><td class="col5">Works in OpenGL1 compatibility mode.</td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [1629-1813] -->
</div>
<!-- EDIT4 SECTION "Intel" [1615-1814] -->
<h3 class="sectionedit6" id="nvidia">NVidia</h3>
<div class="level3">
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Card Name </th><th class="col1"> Driver Version </th><th class="col2"> Basic Features? </th><th class="col3"> Advanced Features (No Shader)? </th><th class="col4"> Shader Features? </th><th class="col5"> Notes </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">NVidia GeForce GT330M 512M </td><td class="col1"> Mac <abbr title="Operating System">OS</abbr> X 10.7.2 </td><td class="col2">Y</td><td class="col3">Y</td><td class="col4">Y</td><td class="col5">All tests works fine.</td>
	</tr>
	<tr class="row2">
		<td class="col0">NVidia GeForce GT540M 1024M </td><td class="col1"> Windows 7 280.26 </td><td class="col2">Y</td><td class="col3">Y</td><td class="col4">Y</td><td class="col5">All tests works fine.</td>
	</tr>
	<tr class="row3">
		<td class="col0">NVidia GeForce GTX480 1536M </td><td class="col1"> Windows 7 285.62 </td><td class="col2">Y</td><td class="col3">Y</td><td class="col4">Y</td><td class="col5">All tests works fine.</td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [1830-2170] -->
</div>
<!-- EDIT6 SECTION "NVidia" [1815-2171] -->
<h3 class="sectionedit8" id="sis">SiS</h3>
<div class="level3">
<div class="table sectionedit9"><table class="inline">
	<tr class="row0">
		<th class="col0"> Card Name </th><th class="col1"> Driver Version </th><th class="col2"> Basic Features? </th><th class="col3"> Advanced Features (No Shader)? </th><th class="col4"> Shader Features? </th><th class="col5"> Notes </th>
	</tr>
</table></div>
<!-- EDIT9 TABLE [2184-2292] -->
</div>
<!-- EDIT8 SECTION "SiS" [2172-] -->
