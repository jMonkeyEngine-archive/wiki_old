---
title: Blender importer for jMonkeyEngine 3
---
<h1 class="sectionedit1" id="blender_importer_for_jmonkeyengine_3">Blender importer for jMonkeyEngine 3</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Blender importer for jMonkeyEngine 3" [1-52] -->
<h2 class="sectionedit2" id="introduction">Introduction</h2>
<div class="level2">

<p>
Importing models to any game engine is as important as using them. The quality of the models depends on the abilities of the people who create it and on the tools they use.
Blender is one of the best free tools for creating 3D enviroments. Its high amount of features attract many model designers.
So far jMonkeyEngine used Ogre mesh files to import 3D data. These files were created by the python script that exported data from blender.
It was important to have always the lates version of the script that is compatible with the version of blender and to use it before importing data to jme.
Now we have an opportunity to simplify the import process by loading data directly from blender binary files: *.blend.
</p>

<p>
</p><p></p><div class="noteimportant">Before you try to import models, make sure you <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">created them properly</a>.
</div>


</div>
<!-- EDIT2 SECTION "Introduction" [53-911] -->
<h2 class="sectionedit3" id="usage">Usage</h2>
<div class="level2">

<p>
To use it in your game or the SDK you should follow the standard asset loading instructions.
By default a BlenderModelLoader is registered with your assetManager to load blend files. This means you can load and convert .blend model files to .j3o format, just like any other supported model format.
</p>

</div>
<!-- EDIT3 SECTION "Usage" [912-1228] -->
<h2 class="sectionedit4" id="currently_supported_features">Currently supported features</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Loading scene (only the current scene is loaded and imported as a node)</div>
</li>
<li class="level1"><div class="li"> Loading mesh objects.</div>
<ul>
<li class="level2"><div class="li"> Meshes are split into several geometries when they have several materials applied.</div>
</li>
<li class="level2"><div class="li"> All faces are stored as triangles (even if blender uses quads).</div>
</li>
<li class="level2"><div class="li"> The mesh is 'Smooth' aware.</div>
</li>
<li class="level2"><div class="li"> User defined UV coordinates are read.</div>
</li>
<li class="level2"><div class="li"> Loading BMesh is supported.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Loading textures.</div>
<ul>
<li class="level2"><div class="li"> Both image and generated textures are imported.</div>
</li>
<li class="level2"><div class="li"> Textures influence is supported ('Influence' tab in blender 2.5+ and 'Map to' in 2.49).</div>
</li>
<li class="level2"><div class="li"> Map input is not yet fully supported (currently working on it ;) ) so please use UV-mapping for all kinds of textures.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Image textures.</div>
<ul>
<li class="level2"><div class="li"> Textures can be loaded from: png, jpg, bmp, dds and tga.</div>
</li>
<li class="level2"><div class="li"> Both textures stored in the blender file and the outside are loaded (the outside textures need a valid path).</div>
</li>
<li class="level2"><div class="li"> Image textures are stored as Texture2D.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Generated textures.</div>
<ul>
<li class="level2"><div class="li"> All generated textures can be loaded except: VoxelData, EnviromentMap and PointDensity.</div>
</li>
<li class="level2"><div class="li"> Feel free to use colorbands.</div>
</li>
<li class="level2"><div class="li"> Generated textures are 'baked' into 2D textures and merged to create one flat texture. They can be freely merged with image textures.</div>
</li>
<li class="level2"><div class="li"> Generated textures can be used as normal maps (but this looks poor when large amount of small triangles is used; incleasing generated texture ppu in blender key might help a little)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Loading materials.</div>
<ul>
<li class="level2"><div class="li"> Materials are loaded and attached to geometries.</div>
</li>
<li class="level2"><div class="li"> Because jMonkeyEngine supports only one material for each Mesh, if you apply several materials to one object – it will be split into several meshes (but still in one node).</div>
</li>
<li class="level2"><div class="li"> Several kinds of input mapping is supported: UV maps, Orco and Nor; all projection types for 2D textures, XYZ coordinates mapping.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Loading animations.</div>
<ul>
<li class="level2"><div class="li"> Bone animations and object animations are supported.</div>
</li>
<li class="level2"><div class="li"> Armatures are imported as Skeleton. Constraint loading is not fully supported so use it carefully.</div>
</li>
<li class="level2"><div class="li"> Only assigning vertices to bones is at the moment supported so do not use bones' envelopes.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Loading modifiers.</div>
<ol>
<li class="level2"><div class="li"> Array modifier</div>
</li>
<li class="level2"><div class="li"> Mirror modifier</div>
</li>
<li class="level2"><div class="li"> Armature modifier (see loading animations)</div>
</li>
<li class="level2"><div class="li"> Particles modifier (see loading particles)</div>
</li>
</ol>
<ul>
<li class="level2"><div class="li"> More will come with time.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Constraints loading</div>
<ul>
<li class="level2"><div class="li"> Constraints are basicly supported but they do not work the way I'd like it. So feel free to experiment with it. I will create another post when I get it to work properly.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Particles loading.</div>
<ul>
<li class="level2"><div class="li"> Some features of particles loading is supported. You can use only particle emitters at the moment.</div>
</li>
<li class="level2"><div class="li"> You can choose to emit particles from vertices, faces or the geometry's convex hull (instead of volume).</div>
</li>
<li class="level2"><div class="li"> Currently Newtonian Physics is only supported.</div>
</li>
<li class="level2"><div class="li"> It was mostly tested for blender 2.49 (so I'm not 100% sure about its use in blender 2.5+).</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Using sculpting.</div>
<ul>
<li class="level2"><div class="li"> This should work quite well for now :).</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Importing curves.</div>
<ul>
<li class="level2"><div class="li"> Both bezier and NURBS curves are supproted.</div>
</li>
<li class="level2"><div class="li"> Feel free to use bevel and taper objects as well ;)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Importing surfaces</div>
<ul>
<li class="level2"><div class="li"> NURBS surface and sphere can be imported.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Importing sky</div>
<ul>
<li class="level2"><div class="li"> loading world's horizon color as a background color if no sky type is used</div>
</li>
<li class="level2"><div class="li"> loading sky without the texture</div>
</li>
<li class="level2"><div class="li"> loading textured sky (including both generated and normal textures)</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "Currently supported features" [1229-4610] -->
<h2 class="sectionedit5" id="planned_features">Planned features.</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Full support for scale and offset in texture input mapping.</div>
</li>
<li class="level1"><div class="li"> Full support for bone and object constraints.</div>
</li>
<li class="level1"><div class="li"> More modifiers loaded.</div>
</li>
<li class="level1"><div class="li"> Loading texts.</div>
</li>
<li class="level1"><div class="li"> Loading meta objects (if jme will support it ;) ).</div>
</li>
</ol>

</div>
<!-- EDIT5 SECTION "Planned features." [4611-4854] -->
<h2 class="sectionedit6" id="known_bugs_problems">Known bugs/problems.</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> RGB10 and RGB9E5 texture types are not supported in texture merging operations (which means that you can use this as a single texture on the model, but you should not combine it with other images or generated textures).</div>
</li>
<li class="level1"><div class="li"> If an armature is attached to a mesh that has more than one material the vertices of the mesh might be strongly displaced. Hope to fix that soon.</div>
</li>
</ol>

</div>
<!-- EDIT6 SECTION "Known bugs/problems." [4855-5261] -->
<h2 class="sectionedit7" id="using_blenderloader_instead_of_blendermodelloader">Using BlenderLoader instead of BlenderModelLoader</h2>
<div class="level2">

<p>
You have two loaders available.
</p>
<ul>
<li class="level1"><div class="li"> BlenderLoader that loads the whole scene. It returns an instance of  LoadingResults that contains all the data loaded from the scene.</div>
</li>
</ul>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">static</span> <span class="kw1">class</span> LoadingResults <span class="kw1">extends</span> Spatial <span class="br0">{</span>
        <span class="co3">/** Bitwise mask of features that are to be loaded. */</span>
        <span class="kw1">private</span> <span class="kw1">final</span> <span class="kw4">int</span> featuresToLoad<span class="sy0">;</span>
        <span class="co3">/** The scenes from the file. */</span>
        <span class="kw1">private</span> List<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span> scenes<span class="sy0">;</span>
        <span class="co3">/** Objects from all scenes. */</span>
        <span class="kw1">private</span> List<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span> objects<span class="sy0">;</span>
        <span class="co3">/** Materials from all objects. */</span>
        <span class="kw1">private</span> List<span class="sy0">&lt;</span>Material<span class="sy0">&gt;</span> materials<span class="sy0">;</span>
        <span class="co3">/** Textures from all objects. */</span>
        <span class="kw1">private</span> List<span class="sy0">&lt;</span>Texture<span class="sy0">&gt;</span> textures<span class="sy0">;</span>
        <span class="co3">/** Animations of all objects. */</span>
        <span class="kw1">private</span> List<span class="sy0">&lt;</span>AnimData<span class="sy0">&gt;</span> animations<span class="sy0">;</span>
        <span class="co3">/** All cameras from the file. */</span>
        <span class="kw1">private</span> List<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span> cameras<span class="sy0">;</span>
        <span class="co3">/** All lights from the file. */</span>
        <span class="kw1">private</span> List<span class="sy0">&lt;</span>Light<span class="sy0">&gt;</span> lights<span class="sy0">;</span>
	<span class="co3">/** Access Methods goes here. */</span>
<span class="br0">}</span></pre>
<ul>
<li class="level1"><div class="li"> BlenderModelLoader loads only the model node and should be used if you have a single model in a file.</div>
</li>
</ul>

<p>
To register the model do the following:
</p>
<pre class="code java">assetManager.<span class="me1">registerLoader</span><span class="br0">(</span>BlenderLoader.<span class="kw1">class</span>, <span class="st0">"blend"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
or
</p>
<pre class="code java">assetManager.<span class="me1">registerLoader</span><span class="br0">(</span>BlenderModelLoader.<span class="kw1">class</span>, <span class="st0">"blend"</span><span class="br0">)</span><span class="sy0">;</span></pre>
<ul>
<li class="level1"><div class="li"> The last thing to do is to create a proper key.</div>
</li>
</ul>

<p>
You can use com.jme3.asset.BlenderKey for that.
The simplest use is to create the key with the asset's name.
It has many differens settings descibing the blender file more precisely, but all of them have default values so you do not need to worry about it at the beggining.
You can use ModelKey as well. This will give the same result as using default BlenderKey.
</p>

</div>
<!-- EDIT7 SECTION "Using BlenderLoader instead of BlenderModelLoader" [5262-6998] -->
<h2 class="sectionedit8" id="how_does_it_work">How does it work?</h2>
<div class="level2">

<p>
BlenderLoader (as well as BlenderModelLoader) is looking for all kinds of known assets to load.
It's primary use is of course to load the models withon the files.
Each blender object is imported as scene Node. The node should have applied textures and materials as well.
If you define animations in your BlenderKey the animations will as well be imported and attached to the model.
</p>

<p>
Here is the list of how blender features are mapped into jme.
</p>
<div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Blender</th><th class="col1">jMonkeyEngine3</th><th class="col2">Note</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign">Scene		</td><td class="col1">Node</td><td class="col2"> </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign">Object		</td><td class="col1">Node</td><td class="col2"> </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign">Mesh		</td><td class="col1">List&lt;Geometry&gt; </td><td class="col2">One mesh can have several materials so that is why a list is needed here.</td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign">Lamp		</td><td class="col1">Light</td><td class="col2"> </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign">Camera		</td><td class="col1">Camera</td><td class="col2"> </td>
	</tr>
	<tr class="row6">
		<td class="col0 leftalign">Material	</td><td class="col1">Material</td><td class="col2"> </td>
	</tr>
	<tr class="row7">
		<td class="col0 leftalign">Texture	</td><td class="col1">Texture</td><td class="col2"> </td>
	</tr>
	<tr class="row8">
		<td class="col0 leftalign">Curve		</td><td class="col1">Node </td><td class="col2">Node with Curve as its mesh</td>
	</tr>
	<tr class="row9">
		<td class="col0 leftalign">Surface	</td><td class="col1">Node </td><td class="col2">The surface is transformed to the proper mesh</td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [7472-7823] -->
<p>
Using BlenderLoader can allow you to use blend file as your local assets repository.
You can store your textures, materials or meshes there and simply import it when needed.
Currently blender 2.49 and 2.5+ are supported (only the stable versions).
Probably versions before 2.49 will work pretty well too, but I never checked that :)
</p>

</div>
<!-- EDIT8 SECTION "How does it work?" [6999-8158] -->
<h2 class="sectionedit10" id="notes">Notes</h2>
<div class="level2">

<p>
I know that the current version of loader is not yet fully functional, but belive me – Blender is a very large issue ;)
Hope I will meet your expectations.
</p>

<p>
Be mindful of the result model vertices amount. The best results are achieved when the model is smooth and has no texture. Then the vertex amount is equal to the vertex amount in blender. If the model is not smooth or has a generated texture applied then the amount of vertices is 3 times larger than mesh's triangles amount. If a 2d texture is applied with UV mapping then the vertex count will vary depending on how much the UV map is fragmented.
</p>

<p>
When using polygon meshes in blender 2.5 and newer, better add and apply the triangulation modifier (if available in your version) or save the file with convertion from polygons to triangles.
Even though the importer supports loading of polygons as the mesh faces, if your face isn't convex, the results might contain errors.
</p>

<p>
Not all modifiers are supported. If your model has modifiers and looks not the way you want in the jme scene - try to apply them and load again.
</p>

<p>
Cheers,
Marcin Roguski (Kaelthas)
</p>

<p>
P.S.
This text might be edited in a meantime if I forgot about something ;)
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/sdk/3ds_to_blender_to_jmp.html" class="wikilink1" title="sdk:3ds_to_blender_to_jmp">3DS to Blender to j3o</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>,
	<a href="/tag/asset.html" class="wikilink1" title="tag:asset" rel="tag">asset</a>
</span></div>

</div>
<!-- EDIT10 SECTION "Notes" [8159-] -->
