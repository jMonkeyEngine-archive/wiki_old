---
title: Working Blender and OgreXML Versions
---
<h1 class="sectionedit1" id="working_blender_and_ogrexml_versions">Working Blender and OgreXML Versions</h1>
<div class="level1">

<p>
Here you can find working combinations of Blender and the OgreXML exporter, with any tips or bugs associated with each.
</p>
<div class="table sectionedit2"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Blender Version </th><th class="col1"> OgreXML Exporter Version </th><th class="col2"> Notes </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> 2.6.3 </td><td class="col1"> <a href="http://code.google.com/p/blender2ogre/downloads/list" class="urlextern" title="http://code.google.com/p/blender2ogre/downloads/list" rel="nofollow">0.5.8</a> </td><td class="col2"> Root bone, no transforms on object, no envelopes </td>
	</tr>
	<tr class="row2">
		<td class="col0"> 2.6.2 </td><td class="col1"> <a href="http://code.google.com/p/blender2ogre/downloads/list" class="urlextern" title="http://code.google.com/p/blender2ogre/downloads/list" rel="nofollow">0.5.5</a> </td><td class="col2"> Root bone, no transforms on object, no envelopes </td>
	</tr>
	<tr class="row3">
		<td class="col0"> 2.6.1 </td><td class="col1"> ? </td><td class="col2 leftalign">  </td>
	</tr>
	<tr class="row4">
		<td class="col0"> 2.6.0 </td><td class="col1"> ? </td><td class="col2 leftalign">  </td>
	</tr>
</table></div>
<!-- EDIT2 TABLE [173-518] -->
</div>
<!-- EDIT1 SECTION "Working Blender and OgreXML Versions" [1-519] -->
<h1 class="sectionedit3" id="tips">Tips</h1>
<div class="level1">

<p>
Tips for exporting animations through OgreXML correctly:
</p>
<ul>
<li class="level1"><div class="li"> apply all transformations</div>
</li>
<li class="level1"><div class="li"> armature should have 0,0,0 transformation (loc,rot,scale)</div>
</li>
<li class="level1"><div class="li"> model object should have 0,0,0 transformation (loc,rot,scale)</div>
</li>
<li class="level1"><div class="li"> root bone should have 0,0,0 transformation (loc,rot,scale)</div>
</li>
<li class="level1"><div class="li"> no envelopes</div>
</li>
</ul>

<p>
Test Character - <a href="http://dl.dropbox.com/u/26887202/123/jme_blender/characterOgre26.zip" class="urlextern" title="http://dl.dropbox.com/u/26887202/123/jme_blender/characterOgre26.zip" rel="nofollow">http://dl.dropbox.com/u/26887202/123/jme_blender/characterOgre26.zip</a>
</p>

<p>
<a href="/resources/jme3-advanced-ogre_solved.jpg" class="media" title="jme3:advanced:ogre_solved.jpg"><img src="/resources/jme3-advanced-ogre_solved.jpg" class="media" alt="" /></a>
<a href="/resources/jme3-advanced-ogre_solved2.png" class="media" title="jme3:advanced:ogre_solved2.png"><img src="/resources/jme3-advanced-ogre_solved2.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT3 SECTION "Tips" [520-996] -->
<h1 class="sectionedit4" id="troubleshooting">Troubleshooting</h1>
<div class="level1">

<p>
<strong>Q:</strong> <em>My animation is stretched.</em>
</p>

<p>
<strong>A:</strong> Use the exporting tips provided above
</p>

</div>
<!-- EDIT4 SECTION "Troubleshooting" [997-] -->
