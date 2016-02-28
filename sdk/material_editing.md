---
title: jMonkeyEngine SDK: Material Editor
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkmaterial_editor">jMonkeyEngine SDK: Material Editor</h1>
<div class="level1">

<p>
If you are looking for background information, read about <a href="/jme3/advanced/material_definitions.html" class="wikilink1" title="jme3:advanced:material_definitions">Material Definitions</a> and <a href="/jme3/advanced/j3m_material_files.html" class="wikilink1" title="jme3:advanced:j3m_material_files">j3M Material Files</a>. 
You can <a href="/jme3/advanced/j3m_material_files.html" class="wikilink1" title="jme3:advanced:j3m_material_files">write .j3m files in a text editor</a>, or <span class="curid"><a href="/sdk/material_editing.html" class="wikilink1" title="sdk:material_editing">use the jMonkeyEngine SDK to generate</a></span> them for you as described in this article.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Material Editor" [1-384] -->
<h2 class="sectionedit2" id="materials">Materials</h2>
<div class="level2">

<p>
The jMonkeyEngine uses a special Material format, which comes in .j3m files. You use .j3m files to store sets of material properties that you use repeatedly. This enables you write one short line of code that simply loads the presets from a custom .j3m file. Without a .j3m file you need to write several lines of material property setters every time when you want to use a non-default material. 
</p>

</div>
<!-- EDIT2 SECTION "Materials" [385-805] -->
<h2 class="sectionedit3" id="creating_j3m_materials">Creating .j3m Materials</h2>
<div class="level2">

<p>
<a href="/resources/sdk-material-editor.png" class="media" title="sdk:material-editor.png"><img src="/resources/sdk-material-editor.png" class="mediaright" alt="" width="275" height="245" /></a>
</p>

<p>
To create new .j3m files in the jMonkeyEngine SDK,
</p>
<ol>
<li class="level1"><div class="li"> Right-click the <code>assets/Materials</code> directory and choose New… &gt; Other.</div>
</li>
<li class="level1"><div class="li"> In the New File Wizard, choose Material &gt; Empty Material File, and click Next.</div>
</li>
<li class="level1"><div class="li"> Give the file a name, for example <code>mat_wall</code> for a wall material.</div>
</li>
<li class="level1"><div class="li"> A new file <code>mat_wall.j3m</code> is created in the Materials directory and opens in the Material Editor.</div>
</li>
</ol>

<p>
You can edit the source of the material, or use the user-friendly visual editor to set the properties of the material. Set the properties to the same values as you would otherwise specify with setters on a Material object in Java code: 
</p>
<pre class="code java">Material mat_wall <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>
    assetManager, <span class="st0">"Common/MatDefs/Light/Lighting.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
mat_wall.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"DiffuseMap"</span>, 
    assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/wall_diffuse.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mat_wall.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"NormalMap"</span>, 
    assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/wall_normals.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mat_wall.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Shininess"</span>, 5f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This Java code corresponds to the following .j3m file:
</p>
<pre class="code xml">Material my brick wall : Common/MatDefs/Light/Lighting.j3md {
  MaterialParameters {
    DiffuseMap: Repeat Textures/wall_diffuse.png
    NormalMap:  Repeat Textures/wall_normals.png
    Shininess: 5.0
  }
}</pre>

<p>
You can modify the source code of the j3m file in the “source” tab of the Material Editor.
</p>

</div>
<!-- EDIT3 SECTION "Creating .j3m Materials" [806-2214] -->
<h2 class="sectionedit4" id="using_j3m_materials">Using .j3m Materials</h2>
<div class="level2">

<p>
<a href="/resources/sdk-applymaterial.jpg" class="media" title="sdk:applymaterial.jpg"><img src="/resources/sdk-applymaterial.jpg" class="mediaright" title="applymaterial.jpg" alt="applymaterial.jpg" width="180" height="300" /></a>
</p>

<p>
When the material is ready and saved into your projects assets directory, you can assign the .j3m to a Geometry.
</p>

<p>
In the jMonkeyEngine SDK
</p>
<ol>
<li class="level1"><div class="li"> Right-click the j3o file and select “Edit in SceneComposer”</div>
</li>
<li class="level1"><div class="li"> Open the SceneExplorer window</div>
</li>
<li class="level1"><div class="li"> In the SceneExplorer, click the geometry to which you want to assign the material.</div>
</li>
<li class="level1"><div class="li"> Open the Properties window</div>
</li>
<li class="level1"><div class="li"> Assign the .j3m material to the .j3o in the Properties&gt;Geometry&gt;Material section</div>
</li>
<li class="level1"><div class="li"> Save the j3o and load it into you game.</div>
</li>
</ol>

<p>
Or in your Java code
</p>
<ul>
<li class="level1"><div class="li"> Use a loader and a setter to assign the material to a Geometry</div>
</li>
</ul>
<pre class="code java">mywall.<span class="me1">setMaterial</span><span class="br0">(</span>assetManager.<span class="me1">loadMaterial</span><span class="br0">(</span> <span class="st0">"Materials/mat_wall.j3m"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
<hr />

<p>
<strong>See also:</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/material_specification.html" class="wikilink1" title="jme3:advanced:material_specification">Developer specification of the jME3 material system (.j3md,.j3m)</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/material_definitions.html" class="wikilink1" title="jme3:advanced:material_definitions">Material Definitions</a> </div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/j3m_material_files.html" class="wikilink1" title="jme3:advanced:j3m_material_files">j3M Material Files</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/neotexture.html" class="wikilink1" title="sdk:neotexture">Neotexture</a> (Procedural textures)</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/material.html" class="wikilink1" title="tag:material" rel="tag">material</a>,
	<a href="/tag/file.html" class="wikilink1" title="tag:file" rel="tag">file</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Using .j3m Materials" [2215-] -->
