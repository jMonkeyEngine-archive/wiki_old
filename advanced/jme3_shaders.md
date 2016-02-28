---
title: JME3 and Shaders
---
<h1 class="sectionedit1" id="jme3_and_shaders">JME3 and Shaders</h1>
<div class="level1">

<p>
<br />

</p>

</div>
<!-- EDIT1 SECTION "JME3 and Shaders" [1-36] -->
<h1 class="sectionedit2" id="shaders_basics">Shaders Basics</h1>
<div class="level1">

<p>
Shaders are sets of instructions that are executed on the GPU. They are used to take advantage of hardware acceleration available on the GPU for rendering purposes.<br />

This paper only covers Vertex and Fragment shaders because they are the only ones supported by JME3 for the moment. But be aware that there are some other types of shaders (geometry, tessellation,…).<br />

There are multiple frequently used languages that you may encounter to code shaders but as JME3 is based on OpenGL, shaders in JME use GLSL and any example in this paper will be written in GLSL.<br />

<br />

</p>

</div>
<!-- EDIT2 SECTION "Shaders Basics" [37-634] -->
<h3 class="sectionedit3" id="how_does_it_work">How Does it work?</h3>
<div class="level3">

<p>
To keep it Simple: The Vertex shader is executed once for each vertex in the view, then the Fragment shader (also called the Pixel shader) is executed once for each pixel on the screen.<br />

The main purpose of the Vertex shader is to compute the screen coordinate of a vertex (where this vertex will be displayed on screen) while the main purpose of the Fragment shader is to compute the color of a pixel.<br />

This is a very simplified graphic to describe the call stack: <br />

<a href="/resources/jme3-advanced-jme3andshaders.png" class="media" title="jme3:advanced:jme3andshaders.png"><img src="/resources/jme3-advanced-jme3andshaders.png" class="media" alt="" /></a><br />

The main program sends mesh data to the vertex shader (vertex position in object space, normals, tangents, etc..). The vertex shader computes the screen position of the vertex and sends it to the Fragment shader. The fragment shader computes the color, and the result is displayed on screen or in a texture.
<br />

</p>

</div>
<!-- EDIT3 SECTION "How Does it work?" [635-1483] -->
<h3 class="sectionedit4" id="variables_scope">Variables scope</h3>
<div class="level3">

<p>
There are different types of scope for variables in a shader :
</p>
<ul>
<li class="level1"><div class="li"> uniform : User defined variables that are passed by the main program to the vertex and fragment shader, these variables are global for a given execution of a shader.</div>
</li>
<li class="level1"><div class="li"> attribute : Per-vertex variables passed by the engine to the shader, like position, normal, etc (Mesh data in the graphic)</div>
</li>
<li class="level1"><div class="li"> varying : Variables passed from the vertex shader to the fragment shader.</div>
</li>
</ul>

<p>
There is a large panel of variable types to be used, for more information about it I recommend reading the GLSL specification <a href="http://www.opengl.org/registry/doc/GLSLangSpec.Full.1.20.8.pdf" class="urlextern" title="http://www.opengl.org/registry/doc/GLSLangSpec.Full.1.20.8.pdf" rel="nofollow">here</a>.<br />

<br />

</p>

</div>
<!-- EDIT4 SECTION "Variables scope" [1484-2149] -->
<h3 class="sectionedit5" id="spaces_and_matrices">Spaces and Matrices</h3>
<div class="level3">

<p>
To understand the coming example you must know about the different spaces in 3D computer graphics, and the matrices used to translate coordinate from one space to another.<br />

<a href="/resources/jme3-advanced-jme3andshaders-1.png" class="media" title="jme3:advanced:jme3andshaders-1.png"><img src="/resources/jme3-advanced-jme3andshaders-1.png" class="media" alt="" /></a><br />

The engine passes the object space coordinates to the vertex shader. We need to compute its position in projection space. To do that we transform the object space position by the WorldViewProjectionMatrix which is a combination of the World, View, Projection matrices (who would have guessed?).<br />

<br />

</p>

</div>
<!-- EDIT5 SECTION "Spaces and Matrices" [2150-2694] -->
<h3 class="sectionedit6" id="simple_examplerendering_a_solid_color_on_an_object">Simple example : rendering a solid color on an object</h3>
<div class="level3">

<p>
Here is the simplest application to shaders, rendering a solid color.<br />

Vertex Shader : <br />

</p>
<pre class="code java"><span class="co1">//the global uniform World view projection matrix</span>
<span class="co1">//(more on global uniforms below)</span>
uniform mat4 g_WorldViewProjectionMatrix<span class="sy0">;</span>
<span class="co1">//The attribute inPosition is the Object space position of the vertex</span>
attribute vec3 inPosition<span class="sy0">;</span>
<span class="kw4">void</span> main<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    <span class="co1">//Transformation of the object space coordinate to projection space</span>
    <span class="co1">//coordinates.</span>
    <span class="co1">//- gl_Position is the standard GLSL variable holding projection space</span>
    <span class="co1">//position. It must be filled in the vertex shader</span>
    <span class="co1">//- To convert position we multiply the worldViewProjectionMatrix by</span>
    <span class="co1">//by the position vector.</span>
    <span class="co1">//The multiplication must be done in this order.</span>
    gl_Position <span class="sy0">=</span> g_WorldViewProjectionMatrix <span class="sy0">*</span> vec4<span class="br0">(</span>inPosition, <span class="nu0">1.0</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Fragment Shader : <br />

</p>
<pre class="code java"><span class="kw4">void</span> main<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    <span class="co1">//returning the color of the pixel (here solid blue)</span>
    <span class="co1">//- gl_FragColor is the standard GLSL variable that holds the pixel</span>
    <span class="co1">//color. It must be filled in the Fragment Shader.</span>
    gl_FragColor <span class="sy0">=</span> vec4<span class="br0">(</span><span class="nu0">0.0</span>, <span class="nu0">0.0</span>, <span class="nu0">1.0</span>, <span class="nu0">1.0</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
For example applying this shader to a sphere would render a solid blue sphere on screen.<br />

<br />

</p>

</div>
<!-- EDIT6 SECTION "Simple example : rendering a solid color on an object" [2695-3932] -->
<h1 class="sectionedit7" id="how_to_use_shaders_in_jme3">How to use shaders in JME3</h1>
<div class="level1">

<p>
You probably heard that JME3 is “shader oriented”, but what does that mean?<br />

Usually to use shaders you must create what is called a program. This program specify the vertex shader and the fragment shader to use.<br />

JME3 encloses this in the material system. Every material in JME3 uses shaders.<br />

For example let’s have a look at the SolidColor.j3md file : <br />

</p>
<pre class="code java">MaterialDef Solid <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a> <span class="br0">{</span>
    <span class="co1">//This is the complete list of user defined uniforms to be used in the</span>
    <span class="co1">//shaders</span>
    MaterialParameters <span class="br0">{</span>
        Vector4 <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>
    <span class="br0">}</span>
    Technique <span class="br0">{</span>
        <span class="co1">//This is where the vertex and fragment shader files are</span>
        <span class="co1">//specified</span>
        VertexShader GLSL100<span class="sy0">:</span>   Common<span class="sy0">/</span>MatDefs<span class="sy0">/</span>Misc<span class="sy0">/</span>SolidColor.<span class="me1">vert</span>
        FragmentShader GLSL100<span class="sy0">:</span> Common<span class="sy0">/</span>MatDefs<span class="sy0">/</span>Misc<span class="sy0">/</span>SolidColor.<span class="me1">frag</span>
        <span class="co1">//This is where you specify which global uniform you need for your</span>
        <span class="co1">//shaders</span>
        WorldParameters <span class="br0">{</span>
            WorldViewProjectionMatrix
        <span class="br0">}</span>
    <span class="br0">}</span>
    Technique FixedFunc <span class="br0">{</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
For more information on JME3 material system, i suggest you read this <a href="http://jmonkeyengine.org/groups/development-discussion-jme3/forum/topic/jmonkeyengine3-material-system-full-explanation" class="urlextern" title="http://jmonkeyengine.org/groups/development-discussion-jme3/forum/topic/jmonkeyengine3-material-system-full-explanation" rel="nofollow">topic</a>.<br />

<br />

</p>

</div>
<!-- EDIT7 SECTION "How to use shaders in JME3" [3933-5176] -->
<h3 class="sectionedit8" id="jme3_global_uniforms">JME3 Global uniforms</h3>
<div class="level3">

<p>
JME3 can expose pre-computed global uniforms to your shaders. You must specify the one that are required for your shader in the WorldParameters section of the material definition file (.j3md).<br />

Note that in the shader the uniform names will be prefixed by a “g_”.<br />

In the example above, WorldViewProjectionMatrix is declared as uniform mat4 g_WorldViewProjectionMatrix in the shader.<br />

The complete list of global uniforms that can be used in JME3 can be found <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/shader/UniformBinding.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/shader/UniformBinding.java" rel="nofollow">here</a>.<br />

<br />

</p>

</div>
<!-- EDIT8 SECTION "JME3 Global uniforms" [5177-5798] -->
<h3 class="sectionedit9" id="jme3_lighting_global_uniforms">JME3 Lighting Global uniforms</h3>
<div class="level3">

<p>
JME3 uses some global uniforms for lighting :
</p>
<ul>
<li class="level1"><div class="li"> g_LightDirection (vec4) : the direction of the light</div>
<ul>
<li class="level2"><div class="li"> use for SpotLight : x,y,z contain the world direction vector of the light, the w component contains the spotlight angle cosine </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> g_LightColor (vec4) : the color of the light</div>
</li>
<li class="level1"><div class="li"> g_LightPosition : the position of the light</div>
<ul>
<li class="level2"><div class="li"> use for SpotLight : x,y,z contain the world position of the light, the w component contains 1/lightRange</div>
</li>
<li class="level2"><div class="li"> use for PointLight : x,y,z contain the world position of the light, the w component contains 1/lightRadius</div>
</li>
<li class="level2"><div class="li"> use for DirectionalLight : strangely enough it's used for the direction of the light…this might change though. The fourth component contains -1 and it's used in the lighting shader to know if it's a directionalLight or not.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> g_AmbientLightColor the color of the ambient light.</div>
</li>
</ul>

<p>
These uniforms are passed to the shader without having to declare them in the j3md file, but you have to specify in the technique definition “ LightMode MultiPass” see lighting.j3md for more information.
<br />

</p>

</div>
<!-- EDIT9 SECTION "JME3 Lighting Global uniforms" [5799-6889] -->
<h3 class="sectionedit10" id="jme3_attributes">JME3 attributes</h3>
<div class="level3">

<p>
Those are different attributes that are always passed to your shader.<br />

You can find a complete list of those attribute in the Type enum of the VertexBuffer <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/scene/VertexBuffer.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/scene/VertexBuffer.java" rel="nofollow">here</a>.<br />

Note that in the shader the attributes names will be prefixed by an “in”.<br />

<br />

When the enumeration lists some usual types for each attribute (for example texCoord specifies two floats) then that is the format expected by all standard JME3 shaders that use that attribute. When writing your own shaders though you can use alternative formats such as placing three floats in texCoord simply by declaring the attribute as vec3 in the shader and passing 3 as the component count into the mesh setBuffer call.
</p>

</div>
<!-- EDIT10 SECTION "JME3 attributes" [6890-7701] -->
<h3 class="sectionedit11" id="user_s_uniforms">User's uniforms</h3>
<div class="level3">

<p>
At some point when making your own shader you'll need to pass your own uniforms<br />

Any uniform has to be declared in the material definition file (.j3md) in the “MaterialParameters” section.<br />

</p>
<pre class="code java">    MaterialParameters <span class="br0">{</span>
        Vector4 <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>
        Texture2D ColorMap
    <span class="br0">}</span></pre>

<p>
You can also pass some define to your vertex/fragment programs to know if an uniform as been declared. <br />

You simply add it in the Defines section of your Technique in the definition file. <br />

</p>
<pre class="code java">    Defines <span class="br0">{</span>
        COLORMAP <span class="sy0">:</span> ColorMap
    <span class="br0">}</span></pre>

<p>
For integer and floating point parameters, the define will contain the value that was set.<br />

For all other types of parameters, the value 1 is defined.<br />

If no value is set for that parameter, the define is not declared in the shader.<br />

</p>

<p>
Those material parameters will be sent from the engine to the shader as follows, 
there are setXXXX methods for any type of uniform you want to pass.<br />

</p>
<pre class="code java">   material.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1.0f, 0.0f, 0.0f, 1.0f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// red color</span>
   material.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, myTexture<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// bind myTexture for that sampler uniform</span></pre>

<p>
To use this uniform in the shader, you need to declare it in the .frag or .vert files (depending on where you need it).
You can make use of the defines here and later in the code:
<strong>Note that the “m_” prefix specifies that the uniform is a material parameter.</strong><br />

</p>
<pre class="code java">   uniform vec4 m_Color<span class="sy0">;</span>
   #ifdef COLORMAP
     uniform sampler2D m_ColorMap<span class="sy0">;</span>
   #endif</pre>

<p>
The uniforms will be populated at runtime with the value you sent.
</p>

</div>
<!-- EDIT11 SECTION "User's uniforms" [7702-9304] -->
<h3 class="sectionedit12" id="exampleadding_color_keying_to_the_lightingj3md_material_definition">Example: Adding Color Keying to the Lighting.j3md Material Definition</h3>
<div class="level3">

<p>
Color Keying is useful in games involving many players. It consists of adding some <br />

player-specific color on models textures. <br />

The easiest way of doing this is to use a keyMap which will contain the amount of <br />

color to add in its alpha channel. <br />

Here I will use this color map: <a href="http://wstaw.org/m/2011/10/24/plasma-desktopxB2787.jpg" class="urlextern" title="http://wstaw.org/m/2011/10/24/plasma-desktopxB2787.jpg" rel="nofollow">http://wstaw.org/m/2011/10/24/plasma-desktopxB2787.jpg</a> <br />

to blend color on this texture: <a href="http://wstaw.org/m/2011/10/24/plasma-desktopbq2787.jpg" class="urlextern" title="http://wstaw.org/m/2011/10/24/plasma-desktopbq2787.jpg" rel="nofollow">http://wstaw.org/m/2011/10/24/plasma-desktopbq2787.jpg</a> <br />

<br />

We need to pass 2 new parameters to the Lighting.j3md definition, MaterialParameters section :
</p>
<pre class="code java"><span class="co1">// Keying Map</span>
Texture2D KeyMap
 
<span class="co1">// Key Color </span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a> KeyColor</pre>

<p>
Below, add a new Define in the main Technique section:
</p>
<pre class="code java">KEYMAP <span class="sy0">:</span> KeyMap</pre>

<p>
In the Lighting.frag file, define the new uniforms:
</p>
<pre class="code java">#ifdef KEYMAP
  uniform sampler2D m_KeyMap<span class="sy0">;</span>
  uniform vec4 m_KeyColor<span class="sy0">;</span>
#endif</pre>

<p>
Further, when obtaining the diffuseColor from the DiffuseMap texture, check
if we need to blend it:
</p>
<pre class="code java">    #ifdef KEYMAP
      vec4 keyColor <span class="sy0">=</span> texture2D<span class="br0">(</span>m_KeyMap, newTexCoord<span class="br0">)</span><span class="sy0">;</span>
      diffuseColor.<span class="me1">rgb</span> <span class="sy0">=</span> <span class="br0">(</span><span class="nu0">1.0</span><span class="sy0">-</span>keyColor.<span class="me1">a</span><span class="br0">)</span> <span class="sy0">*</span> diffuseColor.<span class="me1">rgb</span> <span class="sy0">+</span> keyColor.<span class="me1">a</span> <span class="sy0">*</span> m_KeyColor.<span class="me1">rgb</span><span class="sy0">;</span>
    #endif</pre>

<p>
This way, a transparent pixel in the KeyMap texture doesn't modify the color. <br />

A black pixel replaces it for the m_KeyColor and values in between are blended.<br />

<br />

A result preview can be seen here: <a href="http://wstaw.org/m/2011/10/24/plasma-desktopuV2787.jpg" class="urlextern" title="http://wstaw.org/m/2011/10/24/plasma-desktopuV2787.jpg" rel="nofollow">http://wstaw.org/m/2011/10/24/plasma-desktopuV2787.jpg</a>
</p>

</div>
<!-- EDIT12 SECTION "Example: Adding Color Keying to the Lighting.j3md Material Definition" [9305-10795] -->
<h3 class="sectionedit13" id="step_by_step">Step by step</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Create a vertex shader (.vert) file</div>
</li>
<li class="level1"><div class="li"> Create a fragment shader (.frag) file</div>
</li>
<li class="level1"><div class="li"> Create a material definition (j3md) file specifying the user defined uniforms, path to the shaders and the global uniforms to use</div>
</li>
<li class="level1"><div class="li"> In your initSimpleApplication, create a material using this definition, apply it to a geometry</div>
</li>
<li class="level1"><div class="li"> That’s it!!</div>
</li>
</ul>
<pre class="code java">    <span class="co1">// A cube</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box<span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, 1f,1f,1f<span class="br0">)</span><span class="sy0">;</span>
    Geometry cube <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"box"</span>, box<span class="br0">)</span><span class="sy0">;</span>
    Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,<span class="st0">"Path/To/My/materialDef.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    cube.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>cube<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<br />

</p>

</div>
<!-- EDIT13 SECTION "Step by step" [10796-11415] -->
<h3 class="sectionedit14" id="jme3_and_opengl_3_4_compatibility">JME3 and OpenGL 3 &amp; 4 compatibility</h3>
<div class="level3">

<p>
GLSL 1.0 to 1.2 comes with built in attributes and uniforms (ie, gl_Vertex, gl_ModelViewMatrix, etc…).<br />
Those attributes are deprecated since GLSL 1.3 (opengl 3), hence JME3 global uniforms and attributes. Here is a list of deprecated attributes and their equivalent in JME3<br />

</p>
<div class="table sectionedit15"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">GLSL 1.2 attributes</th><th class="col1">JME3 equivalent</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign">gl_Vertex	</td><td class="col1">inPosition</td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign">gl_Normal	</td><td class="col1">inNormal</td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign">gl_Color	</td><td class="col1">inColor</td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign">gl_MultiTexCoord0	</td><td class="col1">inTexCoord</td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign">gl_ModelViewMatrix	</td><td class="col1">g_WorldViewMatrix</td>
	</tr>
	<tr class="row6">
		<td class="col0 leftalign">gl_ProjectionMatrix	</td><td class="col1">g_ProjectionMatrix</td>
	</tr>
	<tr class="row7">
		<td class="col0 leftalign">gl_ModelViewProjectionMatrix	</td><td class="col1">g_WorldViewProjectionMatrix</td>
	</tr>
	<tr class="row8">
		<td class="col0 leftalign">gl_NormalMatrix	</td><td class="col1">g_NormalMatrix</td>
	</tr>
</table></div>
<!-- EDIT15 TABLE [11741-12052] -->
</div>
<!-- EDIT14 SECTION "JME3 and OpenGL 3 & 4 compatibility" [11416-12052] -->
<h3 class="sectionedit16" id="useful_links">Useful links</h3>
<div class="level3">

<p>
<a href="http://www.eng.utah.edu/~cs5610/lectures/GLSL-ATI-Intro.pdf" class="urlextern" title="http://www.eng.utah.edu/~cs5610/lectures/GLSL-ATI-Intro.pdf" rel="nofollow">http://www.eng.utah.edu/~cs5610/lectures/GLSL-ATI-Intro.pdf</a>
</p>

</div>
<!-- EDIT16 SECTION "Useful links" [12053-] -->
