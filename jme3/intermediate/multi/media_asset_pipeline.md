---
title: Multi-Media Asset Pipeline
---
<h1 class="sectionedit1" id="multi-media_asset_pipeline">Multi-Media Asset Pipeline</h1>
<div class="level1">

<p>
Assets are files that are not code. Your multi-media assets includes, for example, your textures (image files), models (mesh files), and sounds (audio files).
</p>
<ul>
<li class="level1"><div class="li"> You create textures in a graphic editor, for example <a href="http://gimp.org" class="urlextern" title="http://gimp.org" rel="nofollow">Gimp</a>, and export them as PNG or JPG.</div>
</li>
<li class="level1"><div class="li"> You <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">create models</a> in a 3D mesh editor, for example <a href="http://blender.org" class="urlextern" title="http://blender.org" rel="nofollow">Blender</a>, and export them in Ogre Mesh XML or Wavefront OBJ format. </div>
</li>
<li class="level1"><div class="li"> You create sounds in an audio editor, for example <a href="http://audacity.sourceforge.net" class="urlextern" title="http://audacity.sourceforge.net" rel="nofollow">Audacity</a>, and export them as WAVE or OGG.</div>
</li>
</ul>
<div class="table sectionedit2"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">DO</th><th class="col1">DON'T</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Import original models plus textures into <code>assets/Textures</code>. </td><td class="col1"> Don't leave textures or models in a folder outside your JME project: The game cannot load or reference them from there. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Save sounds into <code>assets/Sounds</code>. </td><td class="col1"> Don't leave audio files in a folder outside your JME project: The game cannot load or reference them from there. </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Create low-polygon models. </td><td class="col1"> Don't create high-polygon models, they render too slow to be useful in games. </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Only use Diffuse Map, Normal Map, Glow Map, Specular Map in your models' materials. </td><td class="col1"> Don't use unsupported material properties that are not listed in the <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a>.</td>
	</tr>
	<tr class="row5">
		<td class="col0"> Use UV texture / texture atlases / baking for each texture map. </td><td class="col1"> Don't create models based on multiple separate textures, it will break the model into separate meshes.</td>
	</tr>
	<tr class="row6">
		<td class="col0"> Convert original models to JME3's .j3o format. Move .j3o files into <code>assets/Models</code>. </td><td class="col1">Don't reference original Blender/Ogre/OBJ files in your load() code, because these unoptimized files are not automatically packaged into the final JAR.</td>
	</tr>
	<tr class="row7">
		<td class="col0">Agree on naming schemes and folder schemes with your artists early on to avoid confusion. E.g. keep naming schemes for bones and certain model parts. Try to keep your assets folder clean, its like your codes class structure.</td><td class="col1">Don't mindlessly import downloaded models and other assets into your project without keeping a structure and knowing the files work. You can reimport, delete junk.</td>
	</tr>
</table></div>
<!-- EDIT2 TABLE [623-2091] -->
<p>
Read on for details.
</p>

</div>
<!-- EDIT1 SECTION "Multi-Media Asset Pipeline" [1-2114] -->
<h2 class="sectionedit3" id="use_the_assets_folder">Use The Assets Folder</h2>
<div class="level2">

<p>
Store your assets in subfolders of your project's <code>assets</code> directory. The <code>assets</code> directory is the default path where a JME game's <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a> looks for files to load. 
</p>
<pre class="code">jMonkeyProjects/MyGame/assets/Interface/ # .font, .jpg, .png, .xml
jMonkeyProjects/MyGame/assets/MatDefs/   # .j3md
jMonkeyProjects/MyGame/assets/Materials/ # .j3m
jMonkeyProjects/MyGame/assets/Models/    # .blend, .j3o
jMonkeyProjects/MyGame/assets/Scenes/    # .j3o
jMonkeyProjects/MyGame/assets/Shaders/   # .j3f, .vert, .frag
jMonkeyProjects/MyGame/assets/Sounds/    # .ogg, .wav
jMonkeyProjects/MyGame/assets/Textures/  # .jpg, .png; also .mesh.xml+.material, .mtl+.obj, </pre>

<p>
Prepare the <code>asset</code> folder structure for your individual project:
</p>
<ol>
<li class="level1"><div class="li"> Agree on a directory structure with the graphic designers. </div>
</li>
<li class="level1"><div class="li"> Create subfolders of <code>assets</code> in any way that suits your project (see example above). Stick with one system.</div>
<ul>
<li class="level2"><div class="li"> If different assets belong together, create a parallel subdirectory structure for them. <br />
Example: For car models, create <code>Textures/vehicles/car1/</code>, <code>Materials/vehicles/car1/</code>, <code>Models/vehicles/car1/</code>, , <code>Sounds/vehicles/car1/</code> (etc) directories now.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Agree on a file naming and numbering scheme with the graphic designers. </div>
<ul>
<li class="level2"><div class="li"> Are some assets used interchangeably? Systematic naming and numbering lets developers easily swap out assets by swapping out parts of the path String. </div>
</li>
<li class="level2"><div class="li"> Decide on naming standards for naming interactive parts (arms/legs) of animated models.</div>
</li>
</ul>
</li>
</ol>

<p>
<a href="http://www.youtube.com/watch?v=HFR4socSv_E" class="urlextern" title="http://www.youtube.com/watch?v=HFR4socSv_E" rel="nofollow">Video: Horrible things happen if you mess up labeling your assets. Seriously. ;-)</a>
</p>

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> More details on <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>, including tips how to work with assets when using other IDEs.</div>
</li>
<li class="level1"><div class="li"> Use <a href="/sdk/asset_packs.html" class="wikilink1" title="sdk:asset_packs">Asset Packs</a> to bundle, share, and manage assets!</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Use The Assets Folder" [2115-4007] -->
<h2 class="sectionedit4" id="create_textures_and_materials">Create Textures and Materials</h2>
<div class="level2">

<p>
Install a graphic editor such as Gimp or Photoshop. <strong>Consult the graphic editor's documentation for specific details how to do the following tasks.</strong>
</p>
<ol>
<li class="level1"><div class="li"> Create textures in a graphic editor.</div>
<ul>
<li class="level2"><div class="li"> Save all textures to your prepared subfolders in the <code>assets/Textures</code> directory. </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> (Optional) If you plan to use JME materials that you set programmatically from the code, create .j3m materials in the SDK.</div>
<ul>
<li class="level2"><div class="li"> Save these .j3m files into the <code>assets/Materials</code> directory.</div>
</li>
</ul>
</li>
</ol>

<p>
Storing the textures inside your project directory is necessary for the paths in JME's binary model files (.j3o) to work. Treat the paths of your assets like class names of java classes, they define a specific asset. When you later generate .j3o files, and compile class files, and distribute the application, all paths and files need to be available in their final, absolute form. 
</p>

<p>
</p><p></p><div class="noteimportant">It is imperative to keep the same directory structure from beginning to end. If you ever change the assets directory structure, you have to do manual refactoring (just as for Java package name changes): Re-export all affected models, regenerate all affected .j3o files, and manually update all affected path Strings in your code.
</div>


</div>
<!-- EDIT4 SECTION "Create Textures and Materials" [4008-5269] -->
<h2 class="sectionedit5" id="create_3d_models">Create 3D Models</h2>
<div class="level2">

<p>
Install a mesh editor such as <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">Blender</a> or 3D Studio MAX. Reuse textures and materials as much as possible. <strong>Consult the mesh editor's documentation for specific details how to do the following tasks.</strong>
</p>

<p>
</p><p></p><div class="notetip">Note that UV coords are part of the mesh and not part of the material, so if you import your mesh successfully, you can later apply the texture again and it will map correctly.
</div>

<ol>
<li class="level1"><div class="li"> Create 3D models in a mesh editor. </div>
<ol>
<li class="level2"><div class="li"> Create efficient <strong>low-polygon models</strong>. High-polygon models may look pretty in static 3D art contests, but they slow down dynamic games!</div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/advanced/j3m_material_files.html" class="wikilink1" title="jme3:advanced:j3m_material_files">Create materials</a> for your models either in the 3D editor, or in the jME3 SDK. Only use the following material features: <strong>Diffuse Map or Diffuse Color (minimum); plus optionally Normal Map, Glow Map, Specular Map.</strong> <br />
Every material feature not listed in the <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a> is unsupported and ignored by JME3's renderer.</div>
</li>
<li class="level2"><div class="li"> Unwrap the model in the 3D editor and generate a <strong>UV texture</strong> (i.e. one texture file that contains all the pieces of one model from different angles). <br />
Don't use multiple separate texture files with one model, it will break the model into several meshes.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Export the model mesh in one of the following formats: <strong>.blend, Wavefront .OBJ/.MTL, Ogre .mesh/.material/.scene</strong>.</div>
<ol>
<li class="level2"><div class="li"> <strong>Bake</strong> each texture into one file when exporting. Create a Texture Atlas.</div>
</li>
<li class="level2"><div class="li"> <strong>Save exported models to subfolders of the <code>assets/Textures</code> (sic) directory, so they are together with their textures</strong>!</div>
</li>
</ol>
</li>
</ol>

<p>
See also: <a href="http://www.gamasutra.com/view/feature/2530/practical_texture_atlases.php" class="urlextern" title="http://www.gamasutra.com/view/feature/2530/practical_texture_atlases.php" rel="nofollow">Texture Atlases on gamasutra</a>
</p>

<p>
</p><p></p><div class="noteimportant"><strong>When I load the model in JME3, why does it look different than in the 3D editor?</strong> <br />
3D models will never look identical in a game engine and in a mesh editor. Mesh editors are optimized for high-quality offline rendering, and many of the material and texture options simply do not work in a live rendering context such as games. Also, the shaders that render the materials in JME3 are different implementations than in your mesh editor's renderer. Remind your graphic designers to <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">focus on features that game engines support</a>.
</div>


</div>
<!-- EDIT5 SECTION "Create 3D Models" [5270-7598] -->
<h2 class="sectionedit6" id="convert_3d_models_to_j3o_format">Convert 3D Models to .j3o Format</h2>
<div class="level2">

<p>
Convert all models and scenes to jME3's binary .j3o format to load() them. You use the jMonkeyEngine SDK to do the conversion. 
</p>
<ol>
<li class="level1"><div class="li"> Confirm that you exported the model into the <code>assets/Textures</code> directory (or subdirectories) together with all its textures.</div>
</li>
<li class="level1"><div class="li"> In the SDK, right-click the model and choose “Convert to j3o Binary”. <br />
The paths in the j3o now reference files with an absolute <code>assets/Textures/…</code> path.</div>
</li>
<li class="level1"><div class="li"> Now, move the .j3o into the corresponding <code>assets/Models/</code> or <code>assets/Scenes/</code> directory. </div>
</li>
<li class="level1"><div class="li"> Use the AssetManager to load() the .j3o files.</div>
</li>
</ol>

<p>
This process ensures that the texture paths are correct, and it also keeps your <code>assets/Models</code> folder free from textures. You can reuse your set of textures for many models.
</p>

</div>
<!-- EDIT6 SECTION "Convert 3D Models to .j3o Format" [7599-8398] -->
<h3 class="sectionedit7" id="must_i_convert_to_j3o_yes">Must I convert to .j3o? Yes!</h3>
<div class="level3">

<p>
The .j3o file format is an optimized format to store parts of a jME3 scene graph for 3-D games.
</p>
<ul>
<li class="level1"><div class="li"> A .j3o file can contain one shape, one model, or a whole scene.</div>
</li>
<li class="level1"><div class="li"> Only .j3o files can store all of jme3's material options and other features. Other formats can only be considered meshes with UV mapping data and always need extra work.</div>
</li>
<li class="level1"><div class="li"> .j3o files work seamlessly across platforms and can also be automatically adapted for certain platforms on distribution.</div>
</li>
<li class="level1"><div class="li"> (Optional) You can store the model's physical properties, materials, lights, particle emitters, and audio nodes, in the .j3o file. <br />
Use Java commands, or use the <a href="/sdk/scene_composer.html" class="wikilink1" title="sdk:scene_composer">jMonkeyEngine SDK SceneComposer</a> as a user-friendly interface to add these properties.</div>
</li>
<li class="level1"><div class="li"> The default Ant build script copies .j3o files, .j3m files, sounds, and textures, into the distributable JAR automatically.</div>
</li>
</ul>

<p>
</p><p></p><div class="noteimportant">Important: Unoptimized external model files (.mesh.xml, .material, .obj, .mat, .blend, etc) are not bundled by the default build script into the final game builds in the <code>dist</code> directory! If you or your customers try to run games containing code that loads non-.j3o models, you get a AssetNotFoundException <strong>Runtime Error</strong> (resource not found). Your final application code should only reference .j3o files. – Note that your developers will not get this runtime error when running development builds straight from the SDK.
</div>


</div>
<!-- EDIT7 SECTION "Must I convert to .j3o? Yes!" [8399-9861] -->
<h2 class="sectionedit8" id="see_also">See Also</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/save_and_load.html" class="wikilink1" title="jme3:advanced:save_and_load">Save and Load</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer">Model Loader and Viewer</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>
</span></div>

</div>
<!-- EDIT8 SECTION "See Also" [9862-] -->
