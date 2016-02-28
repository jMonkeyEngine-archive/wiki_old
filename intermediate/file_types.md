---
title: jMonkeyEngine3 Supported File Types
---
<h1 class="sectionedit1" id="jmonkeyengine3_supported_file_types">jMonkeyEngine3 Supported File Types</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "jMonkeyEngine3 Supported File Types" [1-51] -->
<h2 class="sectionedit2" id="jmonkeyengine3_file_formats">jMonkeyEngine3 File Formats</h2>
<div class="level2">
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Suffix</th><th class="col1">Usage</th><th class="col2">Learn more</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">.j3o</td><td class="col1">Binary 3D model or scene. At the latest from the Beta release of your game on, you should convert all models to .j3o format. <br />
During alpha and earlier development phases (when models still change a lot) you can alternatively load OgreXML/OBJ models directly.</td><td class="col2"><a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer">Model Loader and Viewer</a> </td>
	</tr>
	<tr class="row2">
		<td class="col0">.j3m</td><td class="col1">A custom Material. You can create a .j3m file to store a Material configuration for a Geometry (e.g. 3D model).</td><td class="col2"><a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a> <br />
<a href="/sdk/material_editing.html" class="wikilink1" title="sdk:material_editing">Material Editing</a> </td>
	</tr>
	<tr class="row3">
		<td class="col0">.j3md</td><td class="col1">A Material definition. These are pre-defined templates for shader-based Materials. <br />
Each custom .j3m Material is based on a material definition. Advanced users can create their own material definitions. </td><td class="col2"> <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a> </td>
	</tr>
	<tr class="row4">
		<td class="col0">.j3f</td><td class="col1">A custom post-processor filter configuration. You can create a .j3f file to store a FilterPostProcessor with a set of preconfigured filters. </td><td class="col2"> <a href="/sdk/filters.html" class="wikilink1" title="sdk:filters">Filters</a> <br />
<a href="/jme3/advanced/effects_overview.html" class="wikilink1" title="jme3:advanced:effects_overview">Effects Overview</a> </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [93-1068] -->
</div>
<!-- EDIT2 SECTION "jMonkeyEngine3 File Formats" [52-1069] -->
<h2 class="sectionedit4" id="supported_external_file_types">Supported External File Types</h2>
<div class="level2">
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">File Suffix</th><th class="col1">Type</th><th class="col2">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">.mesh.xml, .meshxml</td><td class="col1">3D model</td><td class="col2">Ogre Mesh XML </td>
	</tr>
	<tr class="row2">
		<td class="col0">.scene</td><td class="col1">3D scene</td><td class="col2">Ogre DotScene </td>
	</tr>
	<tr class="row3">
		<td class="col0">.OBJ, .MTL</td><td class="col1">3D model</td><td class="col2">Wavefront</td>
	</tr>
	<tr class="row4">
		<td class="col0">.blend</td><td class="col1">3D model</td><td class="col2">Blender version 2.49 onwards (tested up to 2.65)</td>
	</tr>
	<tr class="row5">
		<td class="col0">COLLADA</td><td class="col1"> 3D model</td><td class="col2">Imported via Blender bundled with the SDK</td>
	</tr>
	<tr class="row6">
		<td class="col0">3DS</td><td class="col1">3D model</td><td class="col2">Imported via Blender bundled with the SDK</td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [1113-1440] --><div class="table sectionedit6"><table class="inline">
	<tr class="row0">
		<td class="col0">.JPG, .PNG, .GIF</td><td class="col1">image</td><td class="col2">Textures, icons</td>
	</tr>
	<tr class="row1">
		<td class="col0">.DDS</td><td class="col1">image</td><td class="col2">Direct Draw Surface texture</td>
	</tr>
	<tr class="row2">
		<td class="col0">.HDR</td><td class="col1">image</td><td class="col2">High Dynamic Range texture</td>
	</tr>
	<tr class="row3">
		<td class="col0">.TGA</td><td class="col1">image</td><td class="col2">Targa Image File texture</td>
	</tr>
	<tr class="row4">
		<td class="col0">.PFM</td><td class="col1">image</td><td class="col2">Portable Float Map texture</td>
	</tr>
	<tr class="row5">
		<td class="col0">.fnt</td><td class="col1">bitmap font</td><td class="col2">AngelCode font for <abbr title="Graphical User Interface">GUI</abbr> and HUD</td>
	</tr>
	<tr class="row6">
		<td class="col0">.WAV</td><td class="col1">audio</td><td class="col2">Wave music and sounds</td>
	</tr>
	<tr class="row7">
		<td class="col0">.OGG</td><td class="col1">audio</td><td class="col2">OGG Vorbis music and sounds</td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [1442-1768] -->
</div>
<!-- EDIT4 SECTION "Supported External File Types" [1070-] -->
