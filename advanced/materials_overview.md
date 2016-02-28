---
title: Material Definition Properties
---
<h1 class="sectionedit1" id="material_definition_properties">Material Definition Properties</h1>
<div class="level1">

<p>
In jMonkeyEngine 3, colors and textures are represented as Material objects.
</p>
<ul>
<li class="level1"><div class="li"> All Geometries must have Materials. To improve performance, reuse Materials for similar models, don't create a new Material object for every Geometry. (E.g. use one bark Material for several tree models.) </div>
</li>
<li class="level1"><div class="li"> Each Material is based on one of jme3's default Material Definitions (.j3md files) that are included in the engine. Advanced users can create additional custom Material Definitions (see how it's done in the <a href="/jme3/build_from_sources.html" class="wikilink1" title="jme3:build_from_sources">jme3 sources</a>).</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">Find out quickly <a href="/jme3/intermediate/how_to_use_materials.html" class="wikilink1" title="jme3:intermediate:how_to_use_materials">How to Use Materials</a>, including the most commonly used code samples and RenderStates. <br />
Or find more background info on <a href="/jme3/advanced/material_definitions.html" class="wikilink1" title="jme3:advanced:material_definitions">How to use Material Definitions</a>.
</div>


</div>
<!-- EDIT1 SECTION "Material Definition Properties" [1-841] -->
<h2 class="sectionedit2" id="all_materials_definition_properties">All Materials Definition Properties</h2>
<div class="level2">

<p>
The following Materials table shows you the Material Definitions that jMonkeyEngine 3 supports. 
</p>

<p>
</p><p></p><div class="notetip">Looks confusing? <br />
1) Start learning about <code>Unshaded.j3md</code> and <code>Lighting.j3md</code>, they cover 90% of the cases. <br />
2) Use <a href="/sdk/material_editing.html" class="wikilink1" title="sdk:material_editing">the SDK's visual material editor</a> to try out and save material settings easily. <br />
3) The <a href="/sdk/code_editor.html" class="wikilink1" title="sdk:code_editor">SDK's Palette</a> contains drag&amp;drop code snippets for loading materials. 
</div>


<p>
Most Material parameters are optional. For example, it is okay to specify solely the <code>DiffuseMap</code> and <code>NormalMap</code> when using <code>Lighting.j3md</code>, and leave the other texture maps empty. In this case, you are only using a subset of the possible features, but that's fine if it already makes in the material look the way that you want. You can always add more texture maps later.
</p>

</div>
<!-- EDIT2 SECTION "All Materials Definition Properties" [842-1717] -->
<h3 class="sectionedit3" id="unshaded_coloring_and_textures">Unshaded Coloring and Textures</h3>
<div class="level3">

<p>
jMonkeyEngine supports illuminated and unshaded Material Definitions.
</p>
<ul>
<li class="level1"><div class="li"> Phong Illuminated materials look more naturalistic.</div>
</li>
<li class="level1"><div class="li"> Unshaded materials look more abstract. </div>
</li>
</ul>

<p>
“Unshaded” materials look somewhat abstract because they ignore lighting and shading. Unshaded Materials work even if the scene does not include a light source. These Materials can be single-colored or textured. For example, they are used for cards and tiles, for the sky, billboards and UI elements, for toon-style games, or for testing. 
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Standard Unshaded Material Definition </th><th class="col1"> Usage </th><th class="col2 leftalign"> Material Parameters  </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Common/MatDefs/Misc/Unshaded.j3md </td><td class="col1"> Standard, non-illuminated Materials. <br />
Use this for simple coloring and texturing, glow, and transparency. <br />
See also: <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a> </td><td class="col2"> <strong>Texture Maps</strong> <br />
setTexture(“ColorMap”, assetManager.loadTexture(“”)); <br />
 setBoolean(“SeparateTexCoord”,true);  <br />
setTexture(“LightMap”, assetManager.loadTexture(“”)); <br />
<strong>Colors</strong> <br />
setColor(“Color”, ColorRGBA.White); <br />
setBoolean(“VertexColor”,true); <br />
<strong>Glow</strong> <br />
setTexture(“GlowMap”, assetManager.loadTexture(“”)); <br />
setColor(“GlowColor”, ColorRGBA.White); </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2273-2913] -->
<p>
Other useful, but less commonly used material definitions:
</p>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Special Unshaded Material Definitions </th><th class="col1"> Usage </th><th class="col2 leftalign"> Material Parameters  </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> Common/MatDefs/Misc/Sky.j3md            </td><td class="col1"> A solid skyblue, or use with a custom SkyDome texture. <br />
See also: <a href="/jme3/advanced/sky.html" class="wikilink1" title="jme3:advanced:sky">Sky</a> </td><td class="col2"> setTexture(“TextureCubeMap”, assetManager.loadTexture(“”)); <br />
 setBoolean(“SphereMap”,true); <br />
setVector3(“NormalScale”, new Vector3f(0,0,0)); </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Common/MatDefs/Terrain/Terrain.j3md </td><td class="col1"> Splat textures for e.g. terrains. <br />
See also: <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">Hello Terrain</a> </td><td class="col2"> setTexture(“Tex1”, assetManager.loadTexture(“”)); (red) <br />
 setFloat(“Tex1Scale”,1f); <br />
 setTexture(“Tex2”, assetManager.loadTexture(“”)); (green) <br />
 setFloat(“Tex2Scale”,1f); <br />
setTexture(“Tex3”, assetManager.loadTexture(“”)); (blue)  <br />
 setFloat(“Tex3Scale”,1f); <br />
setTexture(“Alpha”, assetManager.loadTexture(“”)); </td>
	</tr>
	<tr class="row3">
		<td class="col0">Common/MatDefs/Terrain/HeightBasedTerrain.j3md</td><td class="col1">A multi-layered texture for terrains. <br />
Specify four textures and a Vector3f describing the region in which each texture should appear: <br />
X = start height, <br />
Y = end height, <br />
Z = texture scale. <br />
Texture regions can overlap. <br />
For example: Specify a seafloor texture for the lowest areas, <br />
a sandy texture for the beaches, <br />
a grassy texure for inland areas, <br />
and a rocky texture for mountain tops.</td><td class="col2"> setFloat(“terrainSize”,512f); <br />
setTexture(“region1ColorMap”, assetManager.loadTexture(“”)); <br />
setTexture(“region2ColorMap”, assetManager.loadTexture(“”)); <br />
setTexture(“region3ColorMap”, assetManager.loadTexture(“”)); <br />
setTexture(“region4ColorMap”, assetManager.loadTexture(“”)); <br />
setVector3(“region1”, new Vector3f(0,0,0)); <br />
 setVector3(“region2”, new Vector3f(0,0,0)); <br />
 setVector3(“region3”, new Vector3f(0,0,0)); <br />
 setVector3(“region4”, new Vector3f(0,0,0)); <br />
<strong>Settings for steep areas:</strong> <br />
setTexture(“slopeColorMap”, assetManager.loadTexture(“”)); <br />
 setFloat(“slopeTileFactor”,1f);</td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> Common/MatDefs/Misc/Particle.j3md       </td><td class="col1"> Used with texture masks for particle effects, or for point sprites. <br />
The Quadratic value scales the particle for perspective view (<a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/effect/ParticleEmitter.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/effect/ParticleEmitter.java" rel="nofollow">formula</a>). <br />
Does support an optional colored glow effect. <br />
See also: <a href="/jme3/beginner/hello_effects.html" class="wikilink1" title="jme3:beginner:hello_effects">Hello Effects</a> </td><td class="col2"> setTexture(“Texture”, assetManager.loadTexture(“”)); <br />
setTexture(“GlowMap”, assetManager.loadTexture(“”)); <br />
setColor(“GlowColor”, ColorRGBA.White); <br />
 setFloat(“Quadratic”,1f); <br />
 setBoolean(“PointSprite”,true); </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [2975-5467] -->
</div>
<!-- EDIT3 SECTION "Unshaded Coloring and Textures" [1718-5468] -->
<h3 class="sectionedit6" id="phong_illuminated">Phong Illuminated</h3>
<div class="level3">

<p>
jMonkeyEngine supports illuminated and unshaded Material Definitions.
</p>
<ul>
<li class="level1"><div class="li"> Phong Illuminated materials look more naturalistic.</div>
</li>
<li class="level1"><div class="li"> Unshaded materials look more abstract.</div>
</li>
</ul>

<p>
Illuminated materials require a <a href="/jme3/advanced/light_and_shadow.html" class="wikilink1" title="jme3:advanced:light_and_shadow">light source</a> added to at least one of their parent nodes! (e.g. rootNode.) Illuminated materials are darker on the sides facing away from light sources. They use Phong illumination model (default), or the Ward isotropic gaussian specular shader (WardIso) which looks more like plastic. They do not cast <a href="/jme3/advanced/light_and_shadow.html" class="wikilink1" title="jme3:advanced:light_and_shadow">drop shadows</a> unless you use a FilterPostProcessor. 
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Standard Illuminated Material Definition </th><th class="col1"> Usage </th><th class="col2"> Material Parameters </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> Common/MatDefs/Light/Lighting.j3md      </td><td class="col1"> Commonly used Material with Phong illumination. <br />
Use this material together with DiffuseMap, SpecularMap, BumpMap (NormalMaps, ParalaxMap) textures. <br />
Supports shininess, transparency, and plain material colors (Diffuse, Ambient, Specular colors). <br />
See also: <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a> </td><td class="col2 leftalign"> <strong>Texture Maps</strong> <br />
setTexture(“DiffuseMap”, assetManager.loadTexture(“”)); <br />
setBoolean(“UseAlpha”,true);<sup><a href="#fn__1" id="fnt__1" class="fn_top">1)</a></sup>  <br />
setTexture(“NormalMap”, assetManager.loadTexture(“”)); <br />
setBoolean(“LATC”,true); <sup><a href="#fn__2" id="fnt__2" class="fn_top">2)</a></sup>  <br />
setTexture(“SpecularMap”, assetManager.loadTexture(“”)); <br />
 setFloat(“Shininess”,64f); <br />
setTexture(“ParallaxMap”, assetManager.loadTexture(“”)); <br />
setTexture(“AlphaMap”, assetManager.loadTexture(“”)); <br />
 setFloat(“AlphaDiscardThreshold”,1f); <br />
setTexture(“ColorRamp”, assetManager.loadTexture(“”)); <br />
<strong>Glow</strong> <br />
setTexture(“GlowMap”, assetManager.loadTexture(“”)); <br />
setColor(“GlowColor”, ColorRGBA.White); <br />
<strong>Performance and quality</strong> <br />
setBoolean(“VertexLighting”,true); <br />
  setBoolean(“UseVertexColor”,true); <br />
 setBoolean(“LowQuality”,true); <br />
 setBoolean(“HighQuality”,true); <br />
<strong>Material Colors</strong> <br />
 setBoolean(“UseMaterialColors”,true); <br />
setColor(“Diffuse”, ColorRGBA.White); <br />
 setColor(“Ambient”, ColorRGBA.White); <br />
setColor(“Specular”, ColorRGBA.White); <br />
<strong>Tangent shading:</strong> <br />
 setBoolean(“VTangent”,true); <br />
 setBoolean(“Minnaert”,true);<sup><a href="#fn__3" id="fnt__3" class="fn_top">3)</a></sup> <br />
setBoolean(“WardIso”,true);<sup><a href="#fn__4" id="fnt__4" class="fn_top">4)</a></sup>  </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [6128-7846] --><div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Special Illuminated Material Definitions </th><th class="col1"> Usage </th><th class="col2"> Material Parameters </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Common/MatDefs/Terrain/TerrainLighting.j3md</td><td class="col1">Same kind of multi-layered splat texture as Terrain.j3md, but with illumination and shading. <br />
Typically used for terrains, but works on any mesh. <br />
For every 3 splat textures, you need one alpha map. <br />
You can use a total of 11 texture maps in the terrain's splat texture: <br />
Note that diffuse and normal maps all count against that. <br />
For example, you can use a maximum of 9 diffuse textures, two of which can have normal maps; <br />
or, five textures with both diffuse and normal maps.</td><td class="col2"><strong>Texture Splat Maps</strong> <br />
 setTexture(“DiffuseMap”, assetManager.loadTexture(“”)); <br />
 setFloat(“DiffuseMap_0_scale”,1f); <br />
setTexture(“NormalMap”, assetManager.loadTexture(“”)); <br />
setTexture(“DiffuseMap_1”, assetManager.loadTexture(“”)); <br />
 setFloat(“DiffuseMap_1_scale”,1f); <br />
setTexture(“NormalMap_1”, assetManager.loadTexture(“”)); <br />
setTexture(“DiffuseMap_2”, assetManager.loadTexture(“”)); <br />
 setFloat(“DiffuseMap_2_scale”,1f); <br />
setTexture(“NormalMap_2”, assetManager.loadTexture(“”)); <br />
setTexture(“DiffuseMap_3”, assetManager.loadTexture(“”)); <br />
 setFloat(“DiffuseMap_3_scale”,1f); <br />
setTexture(“NormalMap_3”, assetManager.loadTexture(“”)); <br />
etc, up to 11. <br />
<strong>Alpha Maps</strong> <br />
setTexture(“AlphaMap”, assetManager.loadTexture(“”)); <br />
setTexture(“AlphaMap_1”, assetManager.loadTexture(“”)); <br />
setTexture(“AlphaMap_2”, assetManager.loadTexture(“”)); <br />
<strong>Glowing</strong> <br />
setTexture(“GlowMap”, assetManager.loadTexture(“”)); <br />
setColor(“GlowColor”, ColorRGBA.White); <br />
<strong>Miscellaneous</strong> <br />
setColor(“Diffuse”, ColorRGBA.White); <br />
setColor(“Ambient”, ColorRGBA.White); <br />
setFloat(“Shininess”,64f); <br />
setColor(“Specular”, ColorRGBA.White); <br />
setTexture(“SpecularMap”, assetManager.loadTexture(“”)); <br />
setBoolean(“WardIso”,true); <br />
 setBoolean(“useTriPlanarMapping”,true); <br />
 setBoolean(“isTerrainGrid”,true); </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> Common/MatDefs/Light/Reflection.j3md    </td><td class="col1"> Reflective glass material with environment map (CubeMap/SphereMap). See also: <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/texture/TestCubeMap.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/texture/TestCubeMap.java" rel="nofollow">TestCubeMap.java</a> </td><td class="col2"> setTexture(“Texture”, assetManager.loadTexture(“”)); <br />
 setBoolean(“SphereMap”,true); </td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [7848-10134] -->
</div>
<!-- EDIT6 SECTION "Phong Illuminated" [5469-10135] -->
<h3 class="sectionedit9" id="othertest_and_debug">Other: Test and Debug</h3>
<div class="level3">
<div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Material Definition                     </th><th class="col1"> Usage </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> Common/MatDefs/Misc/ShowNormals.j3md    </td><td class="col1"> A color gradient calculated from the model's surface normals. You can use this built-in material to debug the generation of normals in meshes, to preview models that have no material and no lights, or as fall-back default material. This built-in material has no parameters. </td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [10169-10540] -->
</div>
<!-- EDIT9 SECTION "Other: Test and Debug" [10136-10541] -->
<h2 class="sectionedit11" id="renderstates">RenderStates</h2>
<div class="level2">

</div>
<!-- EDIT11 SECTION "RenderStates" [10542-10567] -->
<h3 class="sectionedit12" id="transparency">Transparency</h3>
<div class="level3">
<div class="table sectionedit13"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Material Option</th><th class="col1">Description</th><th class="col2">Example</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getAdditionalRenderState().setBlendMode(BlendMode.Off);</td><td class="col1">This is the default, no transparency.</td><td class="col2">Use for all opaque objects like walls, floors, people…</td>
	</tr>
	<tr class="row2">
		<td class="col0">getAdditionalRenderState().setBlendMode(BlendMode.Alpha);</td><td class="col1">Interpolates the background pixel with the current pixel by using the current pixel's alpha.</td><td class="col2">Use this for normal every-day translucency: Frosted window panes, ice, glass, alpha-blended vegetation textures… </td>
	</tr>
	<tr class="row3">
		<td class="col0">getAdditionalRenderState().setDepthWrite(false);</td><td class="col1">Disables writing of the pixel's depth value to the depth buffer.</td><td class="col2">Use this on Materials if you have several transparent/translucent objects obscuring one another, but you want to see through both.</td>
	</tr>
	<tr class="row4">
		<td class="col0">getAdditionalRenderState().setAlphaFallOff(0.5f); <br />
getAdditionalRenderState().setAlphaTest(true)</td><td class="col1">Enables Alpha Testing with a “AlphaDiscardThreshold” in the AlphaMap.</td><td class="col2">Activate Alpha Testing for (partially) <strong>transparent</strong> objects such as foliage, hair, etc. <br />
Deactivate Alpha Testing for gradually <strong>translucent</strong> objects, such as colored glass, smoked glass, ghosts.</td>
	</tr>
	<tr class="row5">
		<td class="col0">getAdditionalRenderState().setBlendMode(BlendMode.Additive);</td><td class="col1">Additive alpha blending adds colors in a commutative way, i.e. the result does not depend on the order of transparent layers, since it adds the scene's background pixel color to the current pixel color. This is useful if you have lots of transparent textures overlapping and don't care about the order. <br />
<strong>Note:</strong> Viewed in front of a white background, Additive textures become fully transparent! </td><td class="col2"> This is the default for Particle.j3md-based textures that have a black color background. </td>
	</tr>
	<tr class="row6">
		<td class="col0">getAdditionalRenderState().setBlendMode(BlendMode.AlphaAdditive);</td><td class="col1">Same as “Additive”, except first it multiplies the current pixel color by the pixel alpha.</td><td class="col2">This can be used for particle effects that have alpha as background. </td>
	</tr>
	<tr class="row7">
		<td class="col0">getAdditionalRenderState().setBlendMode(BlendMode.Color);</td><td class="col1">Blends by color.</td><td class="col2">Generally useless.</td>
	</tr>
	<tr class="row8">
		<td class="col0">getAdditionalRenderState().setBlendMode(BlendMode.Modulate);</td><td class="col1">Multiplies the background pixel by the current pixel.</td><td class="col2">?</td>
	</tr>
	<tr class="row9">
		<td class="col0">getAdditionalRenderState().setBlendMode(BlendMode.ModulateX2);</td><td class="col1">Same as “Modulate”, except the result is doubled.</td><td class="col2">?</td>
	</tr>
	<tr class="row10">
		<td class="col0">getAdditionalRenderState().setBlendMode(BlendMode.PremultAlpha);</td><td class="col1">Pre-multiplied alpha blending. E.g. if the color of the object has already been multiplied by its alpha, this is used instead of “Alpha” blend mode.</td><td class="col2">For use with Premult Alpha textures.</td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [10592-13042] -->
<p>
If the DiffuseMap has an alpha channel, use:
</p>
<pre class="code java">mat.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"UseAlpha"</span>,<span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Later, put the Geometry (not the Material!) in the appropriate render queue
</p>
<ul>
<li class="level1"><div class="li"> <pre class="code java">geo.<span class="me1">setQueueBucket</span><span class="br0">(</span>Bucket.<span class="me1">Translucent</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> <pre class="code java">geo.<span class="me1">setQueueBucket</span><span class="br0">(</span>Bucket.<span class="me1">Transparent</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>

</div>
<!-- EDIT12 SECTION "Transparency" [10568-13341] -->
<h3 class="sectionedit14" id="culling">Culling</h3>
<div class="level3">
<div class="table sectionedit15"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Material Option</th><th class="col1">Usage</th><th class="col2">Example</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getAdditionalRenderState().setFaceCullMode(FaceCullMode.Back); </td><td class="col1">Activates back-face culling. Mesh faces that are facing away from the camera are not rendered, which saves time. *Backface culling is activated by default as a major optimization.* </td><td class="col2">The invisible backsides and insides of models are not calculated. </td>
	</tr>
	<tr class="row2">
		<td class="col0">getAdditionalRenderState().setFaceCullMode(FaceCullMode.Off); </td><td class="col1">No meshes are culled. Both mesh faces are rendered, even if they face away from the camera. Slow.</td><td class="col2">Sometimes used to debug custom meshes if you messed up some of the polygon sides, or for special shadow effects.</td>
	</tr>
	<tr class="row3">
		<td class="col0">getAdditionalRenderState().setFaceCullMode(FaceCullMode.Front); </td><td class="col1">Activates front-face culling. Mesh faces facing the camera are not rendered.</td><td class="col2">No example – Typically not used because you wouldn't see anything meaningful.</td>
	</tr>
	<tr class="row4">
		<td class="col0">getAdditionalRenderState().setFaceCullMode(FaceCullMode.FrontAndBack)</td><td class="col1">Culls both backfaces and frontfaces.</td><td class="col2">Use this as an efficient way to make an object temporarily invisible, while keeping all its other in-game properties (such as node attachment, collision shapes, interactions, etc) active.</td>
	</tr>
</table></div>
<!-- EDIT15 TABLE [13361-14503] -->
</div>
<!-- EDIT14 SECTION "Culling" [13342-14504] -->
<h3 class="sectionedit16" id="miscellaneous">Miscellaneous</h3>
<div class="level3">
<div class="table sectionedit17"><table class="inline">
	<tr class="row0">
		<td class="col0">getAdditionalRenderState().setColorWrite(false);</td><td class="col1">Disable writing the color of pixels.</td><td class="col2">Use this together with setDepthWrite(true) to write pixels only to the depth buffer, for example. </td>
	</tr>
	<tr class="row1">
		<td class="col0">getAdditionalRenderState().setPointSprite(true);</td><td class="col1">Enables point-sprite mode, e.g. meshes with “Mode.Points” will be rendered as textured sprites. Note that gl_PointCoord must be set in the shader.</td><td class="col2">Point sprites are used internally for hardware accelerated particle effects.</td>
	</tr>
	<tr class="row2">
		<td class="col0">getAdditionalRenderState().setPolyOffset();</td><td class="col1">Enable polygon offset.</td><td class="col2">Use this when you have meshes that have triangles really close to each over (e.g. <a href="http://en.wikipedia.org/wiki/Coplanarity" class="urlextern" title="http://en.wikipedia.org/wiki/Coplanarity" rel="nofollow">Coplanar</a>), it will shift the depth values to prevent <a href="http://en.wikipedia.org/wiki/Z-fighting" class="urlextern" title="http://en.wikipedia.org/wiki/Z-fighting" rel="nofollow">Z-fighting</a>.</td>
	</tr>
</table></div>
<!-- EDIT17 TABLE [14530-15296] -->
<p>
<strong>Related Links</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/material_specification.html" class="wikilink1" title="jme3:advanced:material_specification">Developer specification of the jME3 material system (.j3md,.j3m)</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/material.html" class="wikilink1" title="tag:material" rel="tag">material</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>,
	<a href="/tag/matdefs.html" class="wikilink1" title="tag:matdefs" rel="tag">MatDefs</a>,
	<a href="/tag/light.html" class="wikilink1" title="tag:light" rel="tag">light</a>,
	<a href="/tag/culling.html" class="wikilink1" title="tag:culling" rel="tag">culling</a>,
	<a href="/tag/renderstates.html" class="wikilink1" title="tag:renderstates" rel="tag">RenderStates</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT16 SECTION "Miscellaneous" [14505-] --><div class="footnotes">
<div class="fn"><sup><a href="#fnt__1" id="fn__1" class="fn_bot">1)</a></sup> 
UseAlpha specifies whether DiffuseMap uses the alpha channel</div>
<div class="fn"><sup><a href="#fnt__2" id="fn__2" class="fn_bot">2)</a></sup> 
LATC Specifies whether NormalMap is BC5/ATI2n/LATC/3Dc-compressed</div>
<div class="fn"><sup><a href="#fnt__3" id="fn__3" class="fn_bot">3)</a></sup> 
Minnaert is a shader type.</div>
<div class="fn"><sup><a href="#fnt__4" id="fn__4" class="fn_bot">4)</a></sup> 
WardIso is a shader type.</div>
</div>
