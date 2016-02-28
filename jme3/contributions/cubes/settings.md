---
title: Settings
---
<h1 class="sectionedit1" id="settings">Settings</h1>
<div class="level1">

<p>
This framework is intended to run every kind of block world the user wants - This includes different chunk sizes, block sizes, materials and a lot more.
</p>

<p>
Those attributes are handled by an instance of the class <strong>CubesSettings</strong>. You will have to specify such an object when creating your block world:
</p>
<pre class="code java"><span class="co1">//You have to specify a valid application, the framework will use e.g. its assetManager</span>
CubesSettings settings <span class="sy0">=</span> <span class="kw1">new</span> CubesSettings<span class="br0">(</span>application<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now, you can set all needed options via <code>get</code>/<code>set</code>-methods:
</p>
<div class="table sectionedit2"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Setting </th><th class="col1"> Default Value </th><th class="col2 leftalign"> Usage  </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> <code>Block Size</code> </td><td class="col1"> 3 </td><td class="col2"> The side length of a block in world units. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> <code>Chunk Size X/Y/Z</code> </td><td class="col1"> 16/256/15 </td><td class="col2"> The amount of blocks, that are contained in one chunk in the given direction. </td>
	</tr>
	<tr class="row3">
		<td class="col0"> <code>Block Material</code> </td><td class="col1"> null </td><td class="col2"> The material that will be used by the chunks' geometries. You can load also load a default blockworld-fitting material by calling <code>setDefaultBlockMaterial(String textureFilePath)</code>. </td>
	</tr>
	<tr class="row4">
		<td class="col0"> <code>Textures Count X/Y</code> </td><td class="col1"> 16 </td><td class="col2"> The amount of textures in your image file, on the given axis. </td>
	</tr>
</table></div>
<!-- EDIT2 TABLE [557-1089] -->
<p>
</p><p></p><div class="notetip">You can generate valid test settings by calling <code>CubesTestAssets.getSettings(application)</code>.
</div>


<p>
</p><p></p><div class="notewarning">At the moment, changes to the settings won't affect the block world at “runtime”, i.e. <strong>after</strong> it's created.
</div>


</div>
