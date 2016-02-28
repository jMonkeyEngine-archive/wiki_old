---
title: AssetManager
---
<h1 class="sectionedit1" id="assetmanager">AssetManager</h1>
<div class="level1">

<p>
By assets we mean multi-media files, such as 3D models, materials, textures, scenes, custom shaders, music and sound files, and custom fonts. JME3 has an integrated asset manager that helps you keep your project assets organized. Think of the asset manager as the filesystem of your game, independent of the actual deployment platform. By default, store your assets in the <code>MyGame/assets/ </code> directory of your project.
</p>

<p>
Advantages of the AssetManager:
</p>
<ul>
<li class="level1"><div class="li"> The paths stay the same, no matter whether the game runs on Windows, Mac, Linux, etc!</div>
</li>
<li class="level1"><div class="li"> The AssetManager automatically caches and optimizes the handling of OpenGL objects. <br />
For example, the same textures are not uploaded to the graphics card multiple times when multiple models use them.</div>
</li>
<li class="level1"><div class="li"> The <a href="/sdk/default_build_script.html" class="wikilink1" title="sdk:default_build_script">default build script</a> automatically bundles the contents of the <code>assets</code> directory into the executable. </div>
</li>
</ul>

<p>
Advanced users can write a custom build and packaging script, and can register custom paths to the AssetManager, but this is up to you then. 
</p>

</div>

<h4 id="context">Context</h4>
<div class="level4">
<pre class="code">jMonkeyProjects/MyGame/assets/    # You store assets in subfolders here! &lt;------
jMonkeyProjects/MyGame/build/     # SDK generates built classes here (*)
jMonkeyProjects/MyGame/build.xml  # You customize Ant build script here
jMonkeyProjects/MyGame/nbproject/ # SDK stores default build.xml and meta data (*)
jMonkeyProjects/MyGame/dist/      # SDK generates executable distribution here (*)
jMonkeyProjects/MyGame/src/       # You store Java sources here
jMonkeyProjects/MyGame/test/      # You store test classes here (optional)
(*) Managed by jMonkeyEngine SDK -- don't edit!</pre>

<p>
See also <a href="/jme3/intermediate/best_practices.html" class="wikilink1" title="jme3:intermediate:best_practices">Best Practices</a>.
</p>

</div>
<!-- EDIT1 SECTION "AssetManager" [1-1702] -->
<h2 class="sectionedit2" id="usage">Usage</h2>
<div class="level2">

<p>
The <code>assetManager</code> object is an com.jme3.asset.AssetManager instance that every com.jme3.app.Application can access. It maintains a root that also includes your project's classpath by default, so you can load any asset that's on the classpath, that is, the top level of your project directory. 
</p>

<p>
You can use the inherited <code>assetManager</code> object directly, or use the accessor <code>app.getAssetManager()</code>.
</p>

<p>
Here is an example how you load assets using the AssetManager. This lines loads a default Material from the built-in <code>Common/</code> directory:
</p>
<pre class="code java">Material mat <span class="sy0">=</span> <span class="br0">(</span>Material<span class="br0">)</span> assetManager.<span class="me1">loadAsset</span><span class="br0">(</span>
    <span class="kw1">new</span> AssetKey<span class="br0">(</span><span class="st0">"Common/Materials/RedColor.j3m"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This Material is “somewhere” in the jME3 JAR; the default Asset Manager is configured to handle a <code>Common/…</code> path correctly, so you don't have to specify the whole path when referring to built-in assets (such as default Materials).
</p>

<p>
Additionally, you can configure the Asset Manager and add any path to its root. This means, you can load assets from any project directory you specify. The next example shows how you load assets from your project's assets directory.
</p>

</div>
<!-- EDIT2 SECTION "Usage" [1703-2860] -->
<h2 class="sectionedit3" id="asset_directory">Asset Directory</h2>
<div class="level2">

<p>
By default, jME3 searches for models in a directory named <code>assets</code>. 
</p>

<p>
</p><p></p><div class="noteimportant">In Java projects created with the jMonkeyEngine SDK, an <code>assets</code> folder is created by default in your project directory. If you are using any other IDE, or the command line, you simply create an <code>assets</code> directory manually (see the Codeless Project tip below).
</div>


<p>
This is our recommended directory structure for storing assets:
</p>
<pre class="code">jMonkeyProjects/MyGame/src/...           # Packages, .java source code.
jMonkeyProjects/MyGame/assets/...        # The assets directory:
jMonkeyProjects/MyGame/assets/Interface/   # .font, .jpg, .png, .xml
jMonkeyProjects/MyGame/assets/MatDefs/     # .j3md
jMonkeyProjects/MyGame/assets/Materials/   # .j3m
jMonkeyProjects/MyGame/assets/Models/      # .j3o
jMonkeyProjects/MyGame/assets/Scenes/      # .j3o
jMonkeyProjects/MyGame/assets/Shaders/     # .j3f, .vert, .frag
jMonkeyProjects/MyGame/assets/Sounds/      # .ogg, .wav
jMonkeyProjects/MyGame/assets/Textures/    # .jpg, .png; also .mesh.xml+.material, .mtl+.obj, .blend (!) </pre>

<p>
These subdirectories are just the most common examples. 
</p>

<p>
</p><p></p><div class="noteimportant">You can rename/delete/add (sub)directories inside the <code>assets</code> directory in any way you like. Note however that there is no automatic refactoring for asset paths in the SDK, so if you modify them late in the development process, you have to refactor all paths manually.
</div>


<p>
<strong>Examples:</strong> You can rename <code>assets/Sounds</code> to <code>assets/Audio</code>, you can delete <code>assets/MatDefs</code> if you don't use it, you can create <code>assets/AIscripts</code>, etc. You can rename/move the <code>assets/Textures</code> directory or its subdirectories, but then you have to re-export all models, and re-convert them all to .j3o, so plan ahead!
</p>

<p>
</p><p></p><div class="noteimportant">Store textures in <code>assets/Textures/</code> before you work with them in a mesh editor! Export and save 3D model files (.mesh.xml+.material, .mtl+.obj, .blend) into the <code>assets/Textures/</code> (!) before you convert the model to binary format (.j3o)! This ensures that texture paths correctly point to the <code>assets/Textures</code> directory. <br />
After the conversion, you move the .j3o file into the <code>assets/Models/</code> or <code>assets/Scenes/</code> directories. This way, you can reuse textures, your binaries consistently link the correct textures, and the <code>assets/Models</code> and <code>assets/Scenes</code> directories don't become cluttered.
</div>


</div>
<!-- EDIT3 SECTION "Asset Directory" [2861-5290] -->
<h2 class="sectionedit4" id="example_codeloading_assets">Example Code: Loading Assets</h2>
<div class="level2">

<p>
Creating a material instance with the definition “Unshaded.j3md”:
</p>
<pre class="code java">Material mat_brick <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span> 
    assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Applying a texture to the material:
</p>
<pre class="code java">mat_brick.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, 
    assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/BrickWall/BrickWall.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Loading a font:
</p>
<pre class="code java">guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Loading a model:
</p>
<pre class="code java">Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Loading a scene from an Ogre3D dotScene file stored inside a zip:
</p>
<pre class="code java">assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Alternatively to ZipLocator, there is also a HttpZipLocator that can stream models from a zip file online:
</p>
<pre class="code java">assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"http://jmonkeyengine.googlecode.com/files/wildhouse.zip"</span>, 
                             HttpZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
jME3 also offers a ClasspathLocator, ZipLocator, FileLocator, HttpZipLocator, and UrlLocator (see <code>com.jme3.asset.plugins</code>). 
</p>

<p>
</p><p></p><div class="noteimportant">The custom build script does not automatically include all ZIP files in the executable build. See “Cannot Locate Resource” solution below.
</div>


</div>
<!-- EDIT4 SECTION "Example Code: Loading Assets" [5291-6763] -->
<h2 class="sectionedit5" id="common_assetmanager_tasks">Common AssetManager Tasks</h2>
<div class="level2">
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Task? </th><th class="col1"> Solution! </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Load a model with materials </td><td class="col1"> Use the asset manager's <code>loadModel()</code> method and attach the Spatial to the rootNode. <pre class="code java">Spatial elephant <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Elephant/Elephant.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>elephant<span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial elephant <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Elephant/Elephant.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>elephant<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row2">
		<td class="col0"> Load a model without materials </td><td class="col1"> If you have a model without materials, you have to add a default material to make it visible. <pre class="code java">Spatial teapot <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Teapot/Teapot.obj"</span><span class="br0">)</span><span class="sy0">;</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
teapot.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>teapot<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row3">
		<td class="col0"> Load a scene </td><td class="col1"> You load scenes just like you load models: <pre class="code java">Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/house/main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [6803-7731] -->
</div>
<!-- EDIT5 SECTION "Common AssetManager Tasks" [6764-7732] -->
<h2 class="sectionedit7" id="nullpointerexceptioncannot_locate_resource">NullPointerException: Cannot locate resource?</h2>
<div class="level2">

<p>
<strong>Problem:</strong>
</p>

<p>
My game runs fine when I run it right from the jMonkeyEngine SDK. But when I run the stand-alone executables (.jar, .jnlp .exe, .app), a DesktopAssetManager error message occurs in the console, and it quits?
</p>
<pre class="code">com.jme3.asset.DesktopAssetManager loadAsset
WARNING: Cannot locate resource: Scenes/town/main.scene
com.jme3.app.Application handleError
SEVERE: Uncaught exception thrown in Thread[LWJGL Renderer Thread,5,main]
java.lang.NullPointerException</pre>

<p>
<strong>Reason:</strong>
</p>

<p>
If you use the default build script, <strong>original models and scenes (.mesh.xml, .obj, .blend, .zip), are excluded</strong> from the distribution automatically. A stand-alone executable includes converted <strong>.j3o files</strong> (models and scenes) only. The default build script makes sure to bundle existing .j3o files in the distribution, but you need to remember to convert the models (from mesh.xml–&gt;.j3o, or .obj–&gt;.j3o, etc) yourself. 
</p>

<p>
<strong>Solution</strong>
</p>

<p>
Before building the executable, you must use the jMonkeyEngine SDK's context menu action to <a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer">convert 3D models to .j3o binary format</a>.
</p>
<ol>
<li class="level1"><div class="li"> Save your original models (.mesh.xml, .scene, .blend, or .obj files, plus textures) into <code>assets/Textures/</code>. (!)</div>
</li>
<li class="level1"><div class="li"> Open the jME3 project in the jMonkeyEngine SDK.</div>
</li>
<li class="level1"><div class="li"> Browse to the <code>assets</code> directory in the Projects window. </div>
</li>
<li class="level1"><div class="li"> Right-click an original model in <code>assets/Textures/</code>, and choose “Convert to JME3 binary”.</div>
</li>
<li class="level1"><div class="li"> The converted file appears in the same directory as the original file. It has the same name and a <code>.j3o</code> suffix. </div>
</li>
<li class="level1"><div class="li"> Move the .j3o file into the <code>assets/Models/</code> or <code>assets/Scenes/</code> directory.</div>
</li>
<li class="level1"><div class="li"> Use the assetManager's <code>load()</code> method to load the <code>.j3o</code> file.</div>
</li>
</ol>

<p>
This ensures that the model's Texture paths keep working between your 3D mesh editor and JME3.
</p>

<p>
</p><p></p><div class="noteimportant">If you must load custom assets from a non-.j3o ZIP file, you must manually ammend the <a href="/sdk/default_build_script.html" class="wikilink1" title="sdk:default_build_script">default build script</a> to copy ZIP files into your distribution. ZIPs are skipped by default.
</div>


</div>
<!-- EDIT7 SECTION "NullPointerException: Cannot locate resource?" [7733-9809] -->
<h2 class="sectionedit8" id="asset_handling_for_other_idescodeless_projects">Asset Handling For Other IDEs: Codeless Projects</h2>
<div class="level2">

<p>
<strong>Problem:</strong>
</p>

<p>
I use another IDE than jMonkeyEngine SDK for coding (Eclipse, IntelliJ, text editor). Where is my <code>asset</code> folder and .j3o converter?
</p>

<p>
<strong>Solution:</strong>
</p>

<p>
You can code in any IDE, but you must create a so-called codeless project in the jMonkeyEngine SDK to maintain assets. <strong>A code-less jMonkeyEngine project does not meddle with your sources or custom build scripts.</strong> You merely use it to convert models to .j3o binaries. 
</p>
<ol>
<li class="level1"><div class="li"> Create your (Eclipse or whatever) project as you like.</div>
</li>
<li class="level1"><div class="li"> Create a directory in your project folder and name it, for example, <code>assets</code>. <br />
Store your assets there as described above.</div>
</li>
<li class="level1"><div class="li"> Download and install the jMonkeyEngine SDK.</div>
</li>
<li class="level1"><div class="li"> In the SDK, go to File → Import Projects → External Project Assets.</div>
</li>
<li class="level1"><div class="li"> Select your (Eclipse or whatever) project and your assets folder in the Import Wizard.</div>
</li>
<li class="level1"><div class="li"> You can now open this (Eclipse or whatever) project in the jMonkeyEngine SDK. <br />
Convert assets as described above.</div>
</li>
</ol>

<p>
</p><p></p><div class="noteimportant">If you don't use the SDK for some reason, you can still convert models to j3o format: Load any model in Ogre3D or Wavefront format with the AssetManager.loadModel() as a spatial. Then save the spatial as j3o file using <a href="/jme3/advanced/save_and_load.html" class="wikilink1" title="jme3:advanced:save_and_load">BinaryExporter</a>.
</div>


<p>
</p><p></p><div class="notetip">Use file version control and let team members check out the project. Your developers open the project in Eclipse (etc) as they are used to. Additionally to their graphic tools, ask your graphic designers to install the jMonkeyEngine SDK, and to check out the codeless project that you just prepared. This makes it easy for non-coding team member to browse and preview game assets, to arrange scenes, and to convert files. At the same time, non-coders don't accidentally mess with code, and developers don't accidentally mess with assets. :)
</div>


</div>
<!-- EDIT8 SECTION "Asset Handling For Other IDEs: Codeless Projects" [9810-] -->
