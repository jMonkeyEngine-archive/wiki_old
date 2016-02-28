---
title: Saving and Loading Materials with .j3m Files
---
<h1 class="sectionedit1" id="saving_and_loading_materials_with_j3m_files">Saving and Loading Materials with .j3m Files</h1>
<div class="level1">

<p>
In the <a href="/jme3/advanced/material_definitions.html" class="wikilink1" title="jme3:advanced:material_definitions">Material Definitions</a> article you learned how to configure <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials</a>  programmatically in Java code. If you have certain commonly used Materials that never change, you can clean up the amount of Java code that clutters your init method, by moving material settings into .j3m files. Then later in your code, you only need to call one setter instead of several to apply the material.
</p>

<p>
If you want to colorize simple shapes (one texture all around), then .j3m are the most easily customizable solution. J3m files can contain texture mapped materials, but as usual you have to create the textures in an external editor, especially if you use UV-mapped textures. 
</p>

</div>
<!-- EDIT1 SECTION "Saving and Loading Materials with .j3m Files" [1-753] -->
<h2 class="sectionedit2" id="writing_the_j3m_file">Writing the .j3m File</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> For every Material, create a file and give it a name that describes it: e.g. <code>SimpleBump.j3m</code></div>
</li>
<li class="level1"><div class="li"> Place the file in your project's <code>assets/Materials/</code> directory, e.g. <code>MyGame/src/assets/Materials/SimpleBump.j3m</code></div>
</li>
<li class="level1"><div class="li"> Edit the file and add content using the following Syntax, e.g.:<pre class="code">Material shiny bumpy rock : Common/MatDefs/Light/Lighting.j3md {
     MaterialParameters {
         Shininess: 8.0
         NormalMap: Textures/bump_rock_normal.png
         UseMaterialColors : true
         Ambient  : 0.0 0.0 0.0 1.0
         Diffuse  : 1.0 1.0 1.0 1.0
         Specular : 0.0 0.0 0.0 1.0
     }
}</pre>
</div>
</li>
</ol>

<p>
How to this file is structured:
</p>
<ol>
<li class="level1"><div class="li"> Header</div>
<ol>
<li class="level2"><div class="li"> <code>Material</code> is a fixed keyword, keep it.</div>
</li>
<li class="level2"><div class="li"> <code>shiny bumpy rock</code> is a descriptive string that you can make up. Choose a name to help you remember for what you intend to use this material.</div>
</li>
<li class="level2"><div class="li"> After the colon, specify on which <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Material</a> definition you base this Material.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Now look up the choosen Material Definition's parameters and their parameter types from the <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Material</a> table. Add one line for each parameter.</div>
<ul>
<li class="level2"><div class="li"> For example: The series of four numbers in the example above represent RGBA color values.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Check the detailed syntax reference below if you are unsure.</div>
</li>
</ol>

<p>
</p><p></p><div class="notetip">In the jMonkeyEngine SDK, use File→New File→Material→Empty Material File to create .j3m files. You can edit .j3m files directly in the SDK. On the other hand, they are plain text files, so you can also create them in any plain text editor.
</div>


</div>
<!-- EDIT2 SECTION "Writing the .j3m File" [754-2349] -->
<h2 class="sectionedit3" id="how_to_use_j3m_materials">How to Use .j3m Materials</h2>
<div class="level2">

<p>
This is how you use the prepared .j3m Material on a Spatial. Since you have saved the .j3m file to your project's Assets directory, the .j3m path is relative to <code>MyGame/src/assets/…</code>.
</p>
<pre class="code java">myGeometry.<span class="me1">setMaterial</span><span class="br0">(</span>assetManager.<span class="me1">loadMaterial</span><span class="br0">(</span><span class="st0">"Materials/SimpleBump.j3m"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Tip:</strong> In the jMonkeyEngine SDK, open Windows&gt;Palette and drag the <code>JME Material: Set J3M</code> snippet into your code.
</p>

</div>
<!-- EDIT3 SECTION "How to Use .j3m Materials" [2350-2795] -->
<h2 class="sectionedit4" id="syntax_reference_for_j3m_files">Syntax Reference for .j3m Files</h2>
<div class="level2">

</div>
<!-- EDIT4 SECTION "Syntax Reference for .j3m Files" [2796-2840] -->
<h3 class="sectionedit5" id="paths">Paths</h3>
<div class="level3">

<p>
Make sure to get the paths to the textures (.png, .jpg) and material definitions (.j3md) right. 
</p>
<ul>
<li class="level1"><div class="li"> The paths to the built-in .j3md files are relative to jME3's Core Data directory. Just copy the path stated in the <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Material</a> table. <br />
<code>Common/MatDefs/Misc/Unshaded.j3md</code> is resolved to <code>jme3/src/src/core-data/Common/MatDefs/Misc/Unshaded.j3md</code>.</div>
</li>
<li class="level1"><div class="li"> The paths to your textures are relative to your project's assets directory. <br />
<code>Textures/bump_rock_normal.png</code> is resolved to <code>MyGame/src/assets/Textures/bump_rock_normal.png</code></div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Paths" [2841-3417] -->
<h3 class="sectionedit6" id="data_types">Data Types</h3>
<div class="level3">

<p>
All data types (except Color) are specified in com.jme3.shader.VarType.
“Color” is specified as Vector4 in J3MLoader.java.
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Name</th><th class="col1">jME Java class</th><th class="col2">.j3m file syntax</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Float</td><td class="col1"> (basic Java type) </td><td class="col2"> a float (e.g. 0.72) , no comma or parentheses </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Vector2</td><td class="col1"> <code>com.jme3.math.Vector2f</code></td><td class="col2"> Two floats, no comma or parentheses </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Vector3 </td><td class="col1"> <code>com.jme3.math.Vector3f</code> </td><td class="col2"> Three floats, no comma or parentheses </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Vector4</td><td class="col1"> <code>com.jme3.math.Vector4f</code> </td><td class="col2"> Four floats, no comma or parentheses </td>
	</tr>
	<tr class="row5">
		<td class="col0"> Texture2D </td><td class="col1"> <code>com.jme3.texture.Texture2D</code> </td><td class="col2"> Path to texture in <code>assets</code> directory, no quotation marks </td>
	</tr>
	<tr class="row6">
		<td class="col0"> Texture3D</td><td class="col1"> <code>com.jme3.texture.Texture3D</code> </td><td class="col2"> Same as texture 2D except it is interpreted as a 3D texture </td>
	</tr>
	<tr class="row7">
		<td class="col0"> TextureCubeMap</td><td class="col1"> <code>com.jme3.texture.TextureCubeMap</code> </td><td class="col2"> Same as texture 2D except it is interpreted as a cubemap texture </td>
	</tr>
	<tr class="row8">
		<td class="col0"> Boolean</td><td class="col1"> (basic Java type) </td><td class="col2"> <code>true</code> or <code>false</code> </td>
	</tr>
	<tr class="row9">
		<td class="col0"> Int</td><td class="col1"> (basic Java type) </td><td class="col2"> Integer number, no comma or parentheses </td>
	</tr>
	<tr class="row10">
		<td class="col0"> Color </td><td class="col1"> <code>com.jme3.math.ColorRGBA</code> </td><td class="col2"> Four floats, no comma or parentheses </td>
	</tr>
	<tr class="row11">
		<td class="col0"> FloatArray</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row12">
		<td class="col0"> Vector2Array</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row13">
		<td class="col0"> Vector3Array</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row14">
		<td class="col0"> Vector4Array</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row15">
		<td class="col0"> Matrix3</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row16">
		<td class="col0"> Matrix4</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row17">
		<td class="col0"> Matrix3Array</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row18">
		<td class="col0"> Matrix4Array</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row19">
		<td class="col0"> TextureBuffer</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
	<tr class="row20">
		<td class="col0"> TextureArray</td><td class="col1"> </td><td class="col2"> (Currently not supported in J3M) </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [3565-4979] -->
</div>
<!-- EDIT6 SECTION "Data Types" [3418-4981] -->
<h3 class="sectionedit8" id="flip_and_repeat_syntax">Flip and Repeat Syntax</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> A texture can be flipped using the following syntax <code>NormalMap: Flip Textures/bump_rock_normal.png</code></div>
</li>
<li class="level1"><div class="li"> A texture can be set to repeat using the following syntax <code>NormalMap: Repeat Textures/bump_rock_normal.png</code></div>
</li>
<li class="level1"><div class="li"> If a texture is set to both being flipped and repeated, Flip must come before Repeat</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Flip and Repeat Syntax" [4982-5325] -->
<h3 class="sectionedit9" id="syntax_for_additional_render_states">Syntax for Additional Render States</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> A Boolean can be “On” or “Off”</div>
</li>
<li class="level1"><div class="li"> Float is “123.0” etc</div>
</li>
<li class="level1"><div class="li"> Enum - values depend on the enum</div>
</li>
</ul>

<p>
See the <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html" rel="nofollow">RenderState</a> javadoc for a detailed explanation of render states.
</p>
<div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Name</th><th class="col1">Type</th><th class="col2">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setWireframe(boolean)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setWireframe(boolean)" rel="nofollow">Wireframe</a> </td><td class="col1">(Boolean)</td><td class="col2"> Enable wireframe rendering mode </td>
	</tr>
	<tr class="row2">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setFaceCullMode(com.jme3.material.RenderState.FaceCullMode)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setFaceCullMode(com.jme3.material.RenderState.FaceCullMode)" rel="nofollow">FaceCull</a> </td><td class="col1">(Enum: FaceCullMode)</td><td class="col2"> Set face culling mode (Off, Front, Back, FrontAndBack) </td>
	</tr>
	<tr class="row3">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setDepthWrite(boolean)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setDepthWrite(boolean)" rel="nofollow">DepthWrite</a> </td><td class="col1">(Boolean)</td><td class="col2"> Enable writing depth to the depth buffer </td>
	</tr>
	<tr class="row4">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setDepthTest(boolean)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setDepthTest(boolean)" rel="nofollow">DepthTest</a> </td><td class="col1">(Boolean)</td><td class="col2"> Enable depth testing </td>
	</tr>
	<tr class="row5">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setBlendMode(com.jme3.material.RenderState.BlendMode)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setBlendMode(com.jme3.material.RenderState.BlendMode)" rel="nofollow">Blend</a> </td><td class="col1">(Enum: BlendMode)</td><td class="col2"> Set the blending mode </td>
	</tr>
	<tr class="row6">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setAlphaFallOff(float)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setAlphaFallOff(float)" rel="nofollow">AlphaTestFalloff</a> </td><td class="col1">(Float)</td><td class="col2"> Set the alpha testing alpha falloff value (if set, it will enable alpha testing) </td>
	</tr>
	<tr class="row7">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setPolyOffset(float, float)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setPolyOffset(float, float)" rel="nofollow">PolyOffset</a> </td><td class="col1">(Float, Float)</td><td class="col2"> Set the polygon offset factor and units </td>
	</tr>
	<tr class="row8">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setColorWrite(boolean)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setColorWrite(boolean)" rel="nofollow">ColorWrite</a> </td><td class="col1">(Boolean)</td><td class="col2"> Enable color writing</td>
	</tr>
	<tr class="row9">
		<td class="col0"> <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setPointSprite(boolean)" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/RenderState.html#setPointSprite(boolean)" rel="nofollow">PointSprite</a> </td><td class="col1">(Boolean)</td><td class="col2"> Enable point sprite rendering for point meshes </td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [5617-7185] -->
</div>
<!-- EDIT9 SECTION "Syntax for Additional Render States" [5326-7187] -->
<h2 class="sectionedit11" id="examples">Examples</h2>
<div class="level2">

</div>
<!-- EDIT11 SECTION "Examples" [7188-7209] -->
<h3 class="sectionedit12" id="example_1shiny">Example 1: Shiny</h3>
<div class="level3">
<pre class="code java">Spatial signpost <span class="sy0">=</span> <span class="br0">(</span>Spatial<span class="br0">)</span> assetManager.<span class="me1">loadAsset</span><span class="br0">(</span>
    <span class="kw1">new</span> OgreMeshKey<span class="br0">(</span><span class="st0">"Models/Sign Post/Sign Post.mesh.xml"</span>, <span class="kw2">null</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
signpost.<span class="me1">setMaterial</span><span class="br0">(</span> assetManager.<span class="me1">loadMaterial</span><span class="br0">(</span>
    <span class="kw1">new</span> AssetKey<span class="br0">(</span><span class="st0">"Models/Sign Post/Sign Post.j3m"</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
TangentBinormalGenerator.<span class="me1">generate</span><span class="br0">(</span>signpost<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>signpost<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The file <code>assets/Models/Sign Post/Sign Post.j3m</code> contains:
</p>
<pre class="code">Material Signpost : Common/MatDefs/Light/Lighting.j3md {
    MaterialParameters {
         Shininess: 4.0
         DiffuseMap:  Models/Sign Post/Sign Post.jpg
         NormalMap:   Models/Sign Post/Sign Post_normal.jpg
         SpecularMap: Models/Sign Post/Sign Post_specular.jpg
         UseMaterialColors : true
         Ambient  : 0.5 0.5 0.5 1.0
         Diffuse  : 1.0 1.0 1.0 1.0
         Specular : 1.0 1.0 1.0 1.0
    }
}</pre>

<p>
The JPG files are in the same directory, <code>assets/Models/Sign Post/…</code>.
</p>

</div>
<!-- EDIT12 SECTION "Example 1: Shiny" [7210-8142] -->
<h3 class="sectionedit13" id="example_2repeating_texture">Example 2: Repeating Texture</h3>
<div class="level3">
<pre class="code java">Material mat <span class="sy0">=</span> assetManager.<span class="me1">loadMaterial</span><span class="br0">(</span>
    <span class="st0">"Textures/Terrain/Pond/Pond.j3m"</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Ambient"</span>, ColorRGBA.<span class="me1">DarkGray</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Diffuse"</span>, ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"UseMaterialColors"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The file <code>assets/Textures/Terrain/Pond/Pond.j3m</code> contains:
</p>
<pre class="code">Material Pong Rock : Common/MatDefs/Light/Lighting.j3md {
     MaterialParameters {
         Shininess: 8.0
         DiffuseMap: Repeat Textures/Terrain/Pond/Pond.png
         NormalMap:  Repeat Textures/Terrain/Pond/Pond_normal.png
     }
}</pre>

<p>
The PNG files are in the same directory, <code>assets/Textures/Terrain/Pond/</code>
</p>

</div>
<!-- EDIT13 SECTION "Example 2: Repeating Texture" [8143-8810] -->
<h3 class="sectionedit14" id="example_3transparent">Example 3: Transparent</h3>
<div class="level3">

<p>
The file <code>assets/Models/Tree/Leaves.j3m</code> contains:
</p>
<pre class="code">Material Leaves : Common/MatDefs/Light/Lighting.j3md {

    Transparent On

    MaterialParameters {
        DiffuseMap : Models/Tree/Leaves.png
        UseAlpha : true
        AlphaDiscardThreshold : 0.5
        UseMaterialColors : true
        Ambient : .5 .5 .5 .5
        Diffuse : 0.7 0.7 0.7 1
        Specular : 0 0 0 1
        Shininess : 16
    }
    AdditionalRenderState {
        Blend Alpha
        AlphaTestFalloff 0.50
        FaceCull Off
    }
}</pre>

<p>
The PNG file is in the same directory, <code>assets/Models/Tree/…</code>
</p>

</div>
<!-- EDIT14 SECTION "Example 3: Transparent" [8811-9444] -->
<h2 class="sectionedit15" id="related_links">Related Links</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/material_specification.html" class="wikilink1" title="jme3:advanced:material_specification">Developer specification of the jME3 material system (.j3md,.j3m)</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/material.html" class="wikilink1" title="tag:material" rel="tag">material</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>,
	<a href="/tag/file.html" class="wikilink1" title="tag:file" rel="tag">file</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/wireframe.html" class="wikilink1" title="tag:wireframe" rel="tag">wireframe</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT15 SECTION "Related Links" [9445-] -->
