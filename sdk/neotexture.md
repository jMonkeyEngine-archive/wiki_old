---
title: jMonkeyEngine SDK: Procedural Textures with NeoTexture
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkprocedural_textures_with_neotexture">jMonkeyEngine SDK: Procedural Textures with NeoTexture</h1>
<div class="level1">

<p>
The NeoTextureEditor allows creating tiled textures procedurally using a simple node interface for generating images, blending them, creating normal maps and much more. You can directly load the .tgr files as a material or export the generated images as .png files and use them in a jMonkeyEngine-based game. 
</p>

<p>
Textures usually make up most of the size of a game distribution. This is why NeoTexture is not only an editor, but also a library that generates textures from .tgr files. Use the library to load .tgr files directly in jME3 as a material, without having to export the textures before. This means high-quality textures for your models, but just tiny description files in your distribution. 
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Procedural Textures with NeoTexture" [1-772] -->
<h3 class="sectionedit2" id="creating_and_editing_a_neotexture_file">Creating and Editing a NeoTexture file</h3>
<div class="level3">

<p>
<a href="/resources/wp-uploads-2010-10-neotexture-300x189.jpg" class="media wikilink2" title="wp-uploads:2010:10:neotexture-300x189.jpg"><img src="/resources/wp-uploads-2010-10-neotexture-300x189.jpg" class="mediaright" title="neotexture-300x189.jpg" alt="neotexture-300x189.jpg" /></a>
</p>
<ol>
<li class="level1"><div class="li"> Right-click the <code>assets/Textures</code> directory and choose New… &gt; Other.</div>
</li>
<li class="level1"><div class="li"> In the New File Wizard, choose NeoTexture &gt; Empty NeoTextureFile and click Next.</div>
</li>
<li class="level1"><div class="li"> Give the file a name, for exmaple <code>neoMaterial</code>.</div>
</li>
<li class="level1"><div class="li"> A new file <code>neoMaterial.tgr</code> is created in the Textures directory and opens in the NeoTexture Editor.</div>
</li>
</ol>

<p>
Edit the .tgr file and create your procedural texture: (<a href="http://neotextureedit.sourceforge.net/" class="urlextern" title="http://neotextureedit.sourceforge.net/" rel="nofollow">Learn more about creating Procedural Textures here</a>)
</p>
<ol>
<li class="level1"><div class="li"> Drag any pattern from the left bar to the editor area. </div>
</li>
<li class="level1"><div class="li"> Right-click the editor area and paste a NormalMap filter node.</div>
</li>
<li class="level1"><div class="li"> Connect the green output mark of the pattern with the red input mark of the filter. <br />
This generates a Normal Map that can be used as bump map.</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Creating and Editing a NeoTexture file" [773-1626] -->
<h3 class="sectionedit3" id="adding_the_neotexture_libraries_to_your_project">Adding the NeoTexture libraries to your project</h3>
<div class="level3">

<p>
To use NeoTexture tgr files directly in your application, you have to add the NeoTexture libraries to your project:
</p>
<ol>
<li class="level1"><div class="li"> Right-click your project and select “Properties”</div>
</li>
<li class="level1"><div class="li"> Go to the “Libraries” section of the properties window</div>
</li>
<li class="level1"><div class="li"> Press “Add Library..”</div>
</li>
<li class="level1"><div class="li"> Select “NeoTexture-Libraries” and press “add”</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Adding the NeoTexture libraries to your project" [1627-1990] -->
<h3 class="sectionedit4" id="loading_tgr_files_as_material">Loading tgr files as material</h3>
<div class="level3">

<p>
<a href="/resources/wp-uploads-2010-10-neotexture-2-300x149.jpg" class="media wikilink2" title="wp-uploads:2010:10:neotexture-2-300x149.jpg"><img src="/resources/wp-uploads-2010-10-neotexture-2-300x149.jpg" class="mediaright" title="neotexture-2-300x149.jpg" alt="neotexture-2-300x149.jpg" /></a>
</p>

<p>
We want to use the procedural texture as a material based on <code>Lighting.j3md</code> (the default). We know that Lighting.j3md supports DiffuseMap, NormalMap, SpecularMap, and ParallaxMap.
</p>
<ol>
<li class="level1"><div class="li"> Click the Normal Map filter to select it. We want to use it as the Normal Map of the texture.</div>
<ol>
<li class="level2"><div class="li"> In the NeoTextures Properties window under <code>Export name</code>, enter the name of the texture layer as it would appear in a .j3m file, e.g. “NormalMap”.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Click the pattern to select it. We want to (re)use it as Diffuse Map of the texture.</div>
<ol>
<li class="level2"><div class="li"> In the NeoTextures Properties window under <code>Export name</code>, enter the name of the texture layer as it would appear in a .j3m file, e.g. “DiffuseMap”.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Click the Save button in the NeoTextures Editor. The .tgr file is saved with two layers. (We could add SpecularMap and ParallaxMap the same way, if we wanted.)</div>
</li>
</ol>

<p>
Let's assign the newly created texture to a mesh to see what it looks like.
</p>
<ol>
<li class="level1"><div class="li"> Open your Main.java file.</div>
</li>
<li class="level1"><div class="li"> Choose Window→Palette to open the Palette. You will find two NeoTexture code snippets, one for adding the NeoTexture loader to the assetManager, and one for loading a NeoTexture material. </div>
</li>
<li class="level1"><div class="li"> Drag&amp;Drop one of each into the simpleInitApp() method of your application.</div>
</li>
<li class="level1"><div class="li"> Adjust the .tgr file path names to match the file that we just created: “Materials/neoMaterial.tgr”.</div>
</li>
</ol>

<p>
Clean, build and run. You’re ready to load your procedural material!
</p>
<pre class="code java">assetManager.<span class="me1">registerLoader</span><span class="br0">(</span>com.<span class="me1">jme3</span>.<span class="me1">material</span>.<span class="me1">plugins</span>.<span class="me1">NeoTextureMaterialLoader</span>.<span class="kw1">class</span>,<span class="st0">"tgr"</span><span class="br0">)</span><span class="sy0">;</span>
NeoTextureMaterialKey key <span class="sy0">=</span> <span class="kw1">new</span> NeoTextureMaterialKey<span class="br0">(</span><span class="st0">"Materials/neoMaterial.tgr"</span><span class="br0">)</span><span class="sy0">;</span>
 
Material mat <span class="sy0">=</span> assetManager.<span class="me1">loadAsset</span><span class="br0">(</span>key<span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Shininess"</span>,<span class="nu0">12</span><span class="br0">)</span><span class="sy0">;</span> <span class="coMULTI">/* Lighting.j3md has non-map parameters too that we can set. */</span>
thing.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The default Material Definition for NeoTextures is <code>Lighting.j3md</code>, and it's probably the one you will use most often. In case that you want to use additional texture parameters, other than DiffuseMap, SpecularMap, ParallaxMap, and NormalMap, you can switch to another Material Definition using setMaterialDef(), for instance:
</p>
<pre class="code java">key.<span class="me1">setMaterialDef</span><span class="br0">(</span><span class="st0">"Commons/MatDefs/Misc/ColoredTextured.j3md"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Remember that the layer names in the .tgr file must match the ones declared in the .j3md file. In our example of <code>ColoredTextured.j3md</code>, the .tgr file must contain a <code>ColorMap</code> and you need to set a RGBAColor.
</p>

</div>
<!-- EDIT4 SECTION "Loading tgr files as material" [1991-4484] -->
<h3 class="sectionedit5" id="using_tgr_files_like_normal_textures_in_j3m_files">Using tgr files like normal textures in j3m files</h3>
<div class="level3">

<p>
You can use the .tgr files like normal textures in j3m files, with a syntax like this:
<code>Materials/neoMaterial?DiffuseMap.tgr</code>
The part between the <code>?</code> and the suffix is the name of the node you want to load as a texture. If you dont supply a name, <code>texture</code> is used.
</p>

<p>
To be able to load these textures, you have to register a Locator and a Loader in the AssetManager, note that you can only register one loader per extension so you cannot load .tgr files as materials and as textures with the same assetManager.
</p>
<pre class="code java">assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"/"</span>, com.<span class="me1">jme3</span>.<span class="me1">texture</span>.<span class="me1">plugins</span>.<span class="me1">NeoTextureLocator</span>.<span class="kw1">class</span> <span class="br0">)</span><span class="sy0">;</span>
assetManager.<span class="me1">registerLoader</span><span class="br0">(</span>com.<span class="me1">jme3</span>.<span class="me1">texture</span>.<span class="me1">plugins</span>.<span class="me1">NeoTextureLoader</span>.<span class="kw1">class</span>,<span class="st0">"tgr"</span><span class="br0">)</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>,
	<a href="/tag/material.html" class="wikilink1" title="tag:material" rel="tag">material</a>
</span></div>

</div>
<!-- EDIT5 SECTION "Using tgr files like normal textures in j3m files" [4485-] -->
