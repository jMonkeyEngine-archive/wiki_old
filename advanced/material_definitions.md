---
title: How to Use Material Definitions (.j3md)
---
<h1 class="sectionedit1" id="how_to_use_material_definitions_j3md">How to Use Material Definitions (.j3md)</h1>
<div class="level1">

<p>
All Geometries need a Material to be visible. Every Material is based on a Material Definition. Material definitions provide the “logic” for the material, and a shader draws the material according to the parameters specified in the definition. The J3MD file abstracts the shader and its configuration away from the user, allowing a simple interface where the user can simply set a few parameters on the material to change its appearance and the way its handled by the shaders. 
</p>

<p>
The most common Material Definitions are included in the engine, advanced users can create custom ones. In this case you will also be interested in the <a href="/jme3/advanced/material_specification.html" class="wikilink1" title="jme3:advanced:material_specification">in-depth developer specification of the jME3 material system</a>.
</p>

<p>
<strong>Example:</strong>
</p>
<pre class="code java">Spatial myGeometry <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Teapot/Teapot.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,  <span class="co1">// Create new material and...</span>
    <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// ... specify a Material Definition file, here "Unshaded.j3md"!</span>
mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>     <span class="co1">// Set one or more material parameters.</span>
myGeometry.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>               <span class="co1">// Use material on this Geometry.</span></pre>

<p>
</p><p></p><div class="notetip">If you use one custom material with certain settings very often, learn about storing material settings in <a href="/jme3/advanced/j3m_material_files.html" class="wikilink1" title="jme3:advanced:j3m_material_files">j3m Material Files</a>. You either <a href="/sdk/material_editing.html" class="wikilink1" title="sdk:material_editing">use the jMonkeyEngine SDK to create .j3m files</a> (user-friendly), or you <a href="/jme3/advanced/j3m_material_files.html" class="wikilink1" title="jme3:advanced:j3m_material_files">write .j3m files in a text editor</a> (IDE-independent).
</div>


</div>
<!-- EDIT1 SECTION "How to Use Material Definitions (.j3md)" [1-1585] -->
<h2 class="sectionedit2" id="preparing_a_material">Preparing a Material</h2>
<div class="level2">

<p>
In the <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a> list:
</p>
<ol>
<li class="level1"><div class="li"> Choose a Material Definition that has the features that you need. </div>
<ul>
<li class="level2"><div class="li"> Tip: If you don't know, start with <code>Unshaded.j3md</code> or <code>Lighting.j3md</code>.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Look at the applicable parameters of the Material Definition and determine which parameters you need to achieve the desired effect (e.g. “glow” or “color”). Most parameters are optional! </div>
</li>
<li class="level1"><div class="li"> Create and save the necessary Texture files to your <code>assets/Textures</code> directory.</div>
<ul>
<li class="level2"><div class="li"> E.g. mytex_diffuse.png as ColorMap / DiffuseMap, mytex_normal.png as NormalMap, mytex_alpha.png as AlphaMap, etc…</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Determine the required values to achieve the effect that you want.</div>
<ul>
<li class="level2"><div class="li"> E.g. set colors, floats, booleans, etc… </div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Preparing a Material" [1586-2329] -->
<h2 class="sectionedit3" id="using_a_material">Using a Material</h2>
<div class="level2">

<p>
In your Java code,
</p>
<ol>
<li class="level1"><div class="li"> Create a Material object based on the chosen Material Definition (.j3md file): <pre class="code java">Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Configure your Material by setting the appropriate values listed in the <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a> table. <pre class="code java">mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Yellow</span> <span class="br0">)</span><span class="sy0">;</span> <span class="co1">// and more</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Apply your prepared Material to a Geometry: <pre class="code java">myGeometry.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> (Optional) Adjust the texture scale of the mesh: <pre class="code java">myGeometryMesh.<span class="me1">scaleTextureCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span>2f, 2f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
For details see also: <a href="/jme3/intermediate/how_to_use_materials.html" class="wikilink1" title="jme3:intermediate:how_to_use_materials">How to Use Materials</a>
</p>

</div>
<!-- EDIT3 SECTION "Using a Material" [2330-3036] -->
<h3 class="sectionedit4" id="examples">Examples</h3>
<div class="level3">

<p>
Here are examples of the methods that set the different data types:
</p>
<ul>
<li class="level1"><div class="li"> <code>mat.setColor(   “Color”,       ColorRGBA.White );</code> </div>
</li>
<li class="level1"><div class="li"> <code>mat.setTexture( “ColorMap”,    assetManager.loadTexture(“Interface/Logo/Monkey.png” ));</code></div>
</li>
<li class="level1"><div class="li"> <code>mat.setFloat(   “Shininess”,   5f);</code></div>
</li>
<li class="level1"><div class="li"> <code>mat.setBoolean( “SphereMap”,   true);</code></div>
</li>
<li class="level1"><div class="li"> <code>mat.setVector3( “NormalScale”, new Vector3f(1f,1f,1f));</code></div>
</li>
</ul>

<p>
A simpled textured material.
</p>
<pre class="code java">Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
    <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
    <span class="st0">"Interface/Logo/Monkey.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
A textured material with a color bleeding through transparent areas.
</p>
<pre class="code java">Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
    <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
    <span class="st0">"Textures/ColoredTex/Monkey.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can test these examples within the following code snippet. It creates a box and applies the material:
</p>
<pre class="code java"> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// ... insert Material definition...</span>
geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="notetip">You can find these and other common code snippets in the jMonkeyEngine SDK Code Palette. Drag and drop them into your source code.
</div>


</div>
<!-- EDIT4 SECTION "Examples" [3037-4410] -->
<h2 class="sectionedit5" id="creating_a_custom_material_definition">Creating a Custom Material Definition</h2>
<div class="level2">

<p>
First read the <a href="/jme3/advanced/material_specification.html" class="wikilink1" title="jme3:advanced:material_specification">developer specification of the jME3 material system (.j3md,.j3m)</a>. Also check out the <a href="/jme3/build_from_sources.html" class="wikilink1" title="jme3:build_from_sources">engine source code</a> and have a look at how some Material Definitions are implemented. 
</p>

<p>
You can create your own Material Definitions and place them in your project's <code>assets/MatDefs</code> directory.
</p>
<ol>
<li class="level1"><div class="li"> Find the existing MatDefs in <code>engine/src/core-data/Common/MatDefs/</code>. </div>
</li>
<li class="level1"><div class="li"> Open a Something.j3md file in a text editor. You see that this .j3md file defines Material Parameters and Techniques.</div>
<ul>
<li class="level2"><div class="li"> Material Parameters are the ones that you set in Materials, as shown in the examples above.</div>
</li>
<li class="level2"><div class="li"> The Techniques rely on VertexShaders and FragmentShaders: You find those in the files Something.vert and Something.frag in the same directory.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Learn about GLSL (OpenGL Shading Language) to understand the .vert and .frag syntax, then write your own.</div>
</li>
</ol>

</div>
<!-- EDIT5 SECTION "Creating a Custom Material Definition" [4411-5384] -->
<h2 class="sectionedit6" id="related_links">Related Links</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/material_specification.html" class="wikilink1" title="jme3:advanced:material_specification">Developer specification of the jME3 material system (.j3md,.j3m)</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/material.html" class="wikilink1" title="tag:material" rel="tag">Material</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">SDK</a>,
	<a href="/tag/matdef.html" class="wikilink1" title="tag:matdef" rel="tag">MatDef</a>,
	<a href="/tag/file.html" class="wikilink1" title="tag:file" rel="tag">file</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT6 SECTION "Related Links" [5385-] -->
