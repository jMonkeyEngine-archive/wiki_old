---
title: jMonkeyEngine3 Material Specification
---
<h1 class="sectionedit1" id="jmonkeyengine3_material_specification">jMonkeyEngine3 Material Specification</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "jMonkeyEngine3 Material Specification" [1-53] -->
<h2 class="sectionedit2" id="general_syntax">General Syntax</h2>
<div class="level2">

<p>
Material definitions and material instance files are formatted similarly to curly-bracket languages, in other words, you have “blocks” and other “blocks” nested in them, surrounded by curly-brackets. There are statements inside the blocks, the next statement begins after a new line, or a semi-colon to allow two statements on the same line. Comments are made by prefixing with two slashes, the <code>/* */</code> style comments are not allowed.
</p>

<p>
<strong>Example:</strong>
</p>
<pre class="code">RootBlock {
  // Comment
  SubBlock NameForTheBlock {
    Statement1 // Another comment
  }
  SubBlock2 {
    SubSubBlock {
      Statement2
      Statement3
      // two statements on the same line
      Statement4; Statement5
    }
  }
  SubBlock3
    { // bracket can be on next line as well
    }
}</pre>

<p>
The syntax for J3MD and J3M files follows from this base format.
</p>

</div>
<!-- EDIT2 SECTION "General Syntax" [54-916] -->
<h2 class="sectionedit3" id="material_definition_files_j3md">Material Definition files (J3MD)</h2>
<div class="level2">

<p>
Material definitions provide the “logic” for the material. Usually a shader that will handle drawing the object, and corresponding parameters that allow configuration of the shader. The J3MD file abstracts the shader and its configuration away from the user, allowing a simple interface where one can simply set a few parameters on the material to change its appearance and the way it's handled.
</p>

<p>
Material definitions support multiple techniques, each technique describes a different way to draw the object. For example, currently in jME3, an additional technique is used to render shadow maps for example.
</p>

</div>
<!-- EDIT3 SECTION "Material Definition files (J3MD)" [917-1570] -->
<h3 class="sectionedit4" id="shaders">Shaders</h3>
<div class="level3">

<p>
Shader support inside J3MD files is rather sophisticated. First, shaders may reference shader libraries, in a similar way to Java's “import” statement, or C++'s “include” pre-processor directive. Shader libraries in turn, can also reference other shader libraries this way. In the end, it is possible for a shader to use many functions together from many libraries and combine them in ways to create a more advanced effect. For example, any shader that wishes to take advantage of hardware skinning, can just import the skinning shader library and use the function, without having to write the specific logic needed for hardware skinning.
</p>

<p>
Shaders can also take advantage of “defines” that are specified inside material definitions.
The defines “bind” into material parameters, so that a change in a material parameter can apply or remove a define from the corresponding shader. This allows the shader to completely change in behavior during run-time.
</p>

<p>
Although it is possible to use shader uniforms for the very same purpose, those may introduce slowdowns in older GPUs, that do not support branching. In that case, using defines can allow changing the way the shader works without using shader uniforms. In order to introduce a define into a shader, however, its source code must be changed, and therefore, it must be re-compiled. It is therefore not recommended to change define bound parameters often.
</p>

</div>
<!-- EDIT4 SECTION "Shaders" [1571-2996] -->
<h3 class="sectionedit5" id="syntax_of_a_j3md_file">Syntax of a J3MD file</h3>
<div class="level3">

<p>
All J3MD files begin with <code>MaterialDef</code> as the root block, following that, is the name of the material def (in this example <code>Test Material 123</code>). The name is not used for anything important currently, except for debugging. The name is typed as is without quotes, and can have spaces.
</p>

<p>
<strong>Example of a first line of a J3MD file:</strong>
</p>
<pre class="code">MaterialDef Test Material 123 {</pre>

<p>
Inside a MaterialDef block, there can be at most one MaterialParameters block, and one or more <code>Technique</code> blocks.
</p>

<p>
Techniques may have an optional name, which specifies the name of the technique. If no name is specified for a technique, then its name is “Default”, and it is used by default if the user does not specify another technique to use for the material.
</p>

<p>
<strong>Example of J3MD:</strong>
</p>
<pre class="code">MaterialDef Test Material 123 { 
  MaterialParameters { }
  Technique { }
  Technique NamedTech { } 
}</pre>

<p>
Inside the MaterialParameters block, the parameters are specified. Every parameter has a type and a name. Material parameters are similar to Java variables in that aspect.
</p>

<p>
<strong>Example of a MaterialParameters block:</strong>
</p>
<pre class="code">MaterialParameters {
    Texture2D TexParam
    Color     ColorParam
    Vector3   VectorParam
    Boolean   BoolParam
// ...
}</pre>

<p>
Whereas in the J3MD file, the parameter names and types are specified, in a J3M (Material instance) file, the values for these parameters are assigned, as will be shown later. This is how the materials are configured.
</p>

<p>
At the time of writing, the following types of parameters are allowed inside J3MD files: Int, Boolean, Float, Vector2, Vector3, Vector4, Texture2D, TextureCubeMap.
</p>

<p>
You can specify a default value for material parameters, inside material definitions, in the case that no value is specified in the material instance. 
</p>
<pre class="code">MaterialParameters {
     Float MyParam : 1
// ...
}</pre>

<p>
1 will be used as the default value and sent to the shader if it has not been set by a meterial.setFloat() call.
</p>

</div>
<!-- EDIT5 SECTION "Syntax of a J3MD file" [2997-4989] -->
<h3 class="sectionedit6" id="techniques">Techniques</h3>
<div class="level3">

<p>
Techniques are more advanced blocks than the MaterialParameters block. Techniques may have nested blocks, any many types of statements.
</p>

<p>
In this section, the statements and nested blocks that are allowed inside the Technique block will be described.
</p>

<p>
The two most important statements, are the <code>FragmentShader</code> and <code>VertexShader</code> statements. These statements specify the shader to use for the technique, and are required inside the “Default” technique. Both operate in the same way, after the statement, the language of the shader is specified, usually with a version number as well, for example <code>GLSL100</code> for OpenGL Shading Language version 1.00. Followed by a colon and an absolute path for an asset describing the actual shader source code. For GLSL, it is permitted to specify .glsl, .frag, and .vert files.
</p>

<p>
When the material is applied to an object, the shader has its uniforms set based on the material parameter values specified in the material instance. but the parameter is prefixed with an“m_”.
</p>

<p>
For example, assuming the parameter <code>Shininess</code> is defined in the MaterialParameters block like so:
</p>
<pre class="code">MaterialParameters {
  Float Shininess
}</pre>

<p>
The value of that parameter will map into an uniform with same name with the “m_” prefix in the GLSL shader:
</p>
<pre class="code">uniform float m_Shininess;</pre>

<p>
The letter <code>m</code> in the prefix stands for material.
</p>

</div>
<!-- EDIT6 SECTION "Techniques" [4990-6385] -->
<h3 class="sectionedit7" id="world_global_parameters">World/Global parameters</h3>
<div class="level3">

<p>
An important structure, that also relates to shaders, is the WorldParameters structure. It is similar in purpose to the MaterialParameters structure; it exposes various parameters to the shader, but it works differently. Whereas the user specified material parameters, world parameters are specified by the engine. In addition, the WorldParameters structure is nested in the Technique, because it is specific to the shader being used. For example, the Time world parameter specifies the time in seconds since the engine started running, the material can expose this parameter to the shader by specifying it in the WorldParameters structure like so:
</p>
<pre class="code">WorldParameters {
  Time
// ...
}</pre>

<p>
The shader will be able to access this parameter through a uniform, also named <code>Time</code> but prefixed with <code>g_</code>:
</p>
<pre class="code">uniform float g_Time;</pre>

<p>
The <code>g</code> letter stands for “global”, which is considered a synonym with “world” in the context of parameter scope.
</p>

<p>
There are many world parameters available for shaders, a comprehensive list will be specified elsewhere.
</p>

</div>
<!-- EDIT7 SECTION "World/Global parameters" [6386-7486] -->
<h3 class="sectionedit8" id="renderstate">RenderState</h3>
<div class="level3">

<p>
The RenderState block specifies values for various render states in the rendering context. The RenderState block is nested inside the Technique block. There are many types of render states, and a comprehensive list will not be included in this document.
</p>

<p>
The most commonly used render state is alpha blending, to specify it for a particular technique, including a RenderState block with the statement <code>Blend Alpha</code>.
</p>

<p>
<strong>Example:</strong>
</p>
<pre class="code">RenderState {
 Blend Alpha
}</pre>

<p>
<strong>Full Example of a J3MD</strong>
</p>

<p>
Included is a full example of a J3MD file using all the features learned:
</p>
<pre class="code">MaterialDef Test Material 123 { 
  MaterialParameters {
    Float m_Shininess
    Texture2D m_MyTex
  }
  Technique {
    VertexShader GLSL100 : Common/MatDefs/Misc/MyShader.vert
    FragmentShader GLSL100 : Common/MatDefs/Misc/MyShader.frag
    WorldParameters {
      Time
    }
    RenderState {
      Blend Alpha
    }
  } 
}</pre>

</div>
<!-- EDIT8 SECTION "RenderState" [7487-8430] -->
<h2 class="sectionedit9" id="material_instance_files_j3m">Material Instance files (J3M)</h2>
<div class="level2">

<p>
In comparison to J3MD files, material instance (J3M) files are significantly simpler. In most cases, the user will not have to modify or create his/her own J3MD files.
</p>

<p>
All J3M files begin with the word <code>Material</code> followed by the name of the material (once again, used for debugging only). Following the name, is a colon and the absolute asset path to the material definition (J3MD) file extended or implemented, followed by a curly-bracket.
</p>

<p>
<strong>Example:</strong>
</p>
<pre class="code">Material MyGrass : Common/MatDefs/Misc/TestMaterial.j3md {</pre>

<p>
The material definition is a required component, depending on the material definition being used, the appearance and functionality of the material changes completely. Whereas the material definition provided the “logic” for the material, the material instance provides the configuration for how this logic operates.
</p>

<p>
The J3M file includes only a single structure; MaterialParameters, analogous to the same-named structure in the J3MD file. Whereas the J3MD file specified the parameter names and types, the J3M file specifies the values for these parameters. By changing the parameters, the configuration of the parent J3MD changes, allowing a different effect to be achieved.
</p>

<p>
To specify a value for a parameter, one must specify first the parameter name, followed by a colon, and then followed by the parameter value. For texture parameters, the value is an absolute asset path pointing to the image file. Optionally, the path can be prefixed with the word “Flip” in order to flip the image along the Y-axis, this may be needed for some models.
</p>

<p>
<strong>Example of a MaterialParameters block in J3M:</strong>
</p>
<pre class="code">MaterialParameters {
  m_Shininess : 20.0 
}</pre>
<div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Param type</th><th class="col1">Value example</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Int</td><td class="col1">123</td>
	</tr>
	<tr class="row2">
		<td class="col0">Boolean</td><td class="col1">true</td>
	</tr>
	<tr class="row3">
		<td class="col0">Float</td><td class="col1">0.1</td>
	</tr>
	<tr class="row4">
		<td class="col0">Vector2</td><td class="col1">0.1 5.6</td>
	</tr>
	<tr class="row5">
		<td class="col0">Vector3</td><td class="col1">0.1 5.6 2.99</td>
	</tr>
	<tr class="row6">
		<td class="col0">Vector4=Color</td><td class="col1">0.1 5.6 2.99 3</td>
	</tr>
	<tr class="row7">
		<td class="col0">Texture2D=TextureCubeMap</td><td class="col1">Textures/MyTex.jpg</td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [10162-10343] -->
<p>
}
</p>

<p>
The formatting of the value, depends on the type of the value that was specified in the J3MD file being extended. Examples are provided for every parameter type:
</p>

<p>
<strong>Full example of a J3M</strong>
</p>
<pre class="code">Material MyGrass : Common/MatDefs/Misc/TestMaterial.j3md { 
  MaterialParameters {
    m_MyTex : Flip Textures/GrassTex.jpg
    m_Shininess : 20.0
  }
}</pre>

</div>
<!-- EDIT9 SECTION "Material Instance files (J3M)" [8431-10703] -->
<h3 class="sectionedit11" id="java_interface_for_j3m">Java interface for J3M</h3>
<div class="level3">

<p>
It is possible to generate an identical J3M file using Java code, by using the classes in the com.jme3.material package. Specifics of the <a href="http://jmonkeyengine.org/javadoc/com/jme3/material/Material.html" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/material/Material.html" rel="nofollow">Material API</a> will not be provided in this document. The J3M file above is represented by this Java code:
</p>
<pre class="code java"><span class="co1">// Create a material instance</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/
    TestMaterial.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Load the texture. Specify "true" for the flip flag in the TextureKey</span>
Texture tex <span class="sy0">=</span>
assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="kw1">new</span> TextureKey<span class="br0">(</span><span class="st0">"Textures/GrassTex.jpg"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Set the parameters</span>
mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"MyTex"</span>, tex<span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Shininess"</span>, 20.0f<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT11 SECTION "Java interface for J3M" [10704-11433] -->
<h2 class="sectionedit12" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
Congratulations on being able to read this entire document! To reward your efforts, jMonkeyEngine.com will offer a free prize, please contact Momoko_Fan aka “Kirill Vainer” with the password “bananapie” to claim.
</p>

</div>
<!-- EDIT12 SECTION "Conclusion" [11434-] -->
