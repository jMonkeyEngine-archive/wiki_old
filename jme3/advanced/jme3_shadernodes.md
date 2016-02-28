---
title: Shader Nodes
---
<h1 class="sectionedit1" id="shader_nodes">Shader Nodes</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Shader Nodes" [1-27] -->
<h3 class="sectionedit2" id="motivations">Motivations</h3>
<div class="level3">

<p>
jME3 material system is entirely based on shaders. While it's pretty powerful, this system has some issues and limitations : 
</p>
<ul>
<li class="level1"><div class="li"> Monolithic shaders have a serious lack of flexibility, and it can be daunting to get into the code for inexperienced users.</div>
</li>
<li class="level1"><div class="li"> Maintenance ease of such shaders is poor. (for example the whole lighting shaders represent around 500 lines of code, and it could be a lot worse with more features)</div>
</li>
<li class="level1"><div class="li"> Adding new features to those shaders decrease the ease of maintenance a lot. This point made us reluctant to do so and some feature were never added (Fog to name it, but many more).</div>
</li>
<li class="level1"><div class="li"> Users can't add their own feature to the shader unless they fork it, and fall back to the same issues explained in previous points.</div>
</li>
</ul>

<p>
Shader Nodes were designed with this in mind and are the fruit of many long discussions in the core chat balancing the pros and cons of this or that pattern.<br />

At first this system was referred to as “Shader injection”. The basic idea was to allow users to inject code into shaders with a tag replacement system.<br />

We finally came with a different concept called Shader Nodes, that is inspired from blender nodes system for textures and post process.<br />

<strong>The final shader is generated at run time by the system by assembling shader nodes together.</strong>
</p>

</div>
<!-- EDIT2 SECTION "Motivations" [28-1348] -->
<h3 class="sectionedit3" id="what_is_a_shader_node">What is a Shader Node?</h3>
<div class="level3">

<p>
Conceptually, it's just a self sufficient piece of glsl code that accepts inputs and produce some outputs.<br />

Inputs are glsl variables that may be fed by previous nodes output values.<br />

Outputs are glsl variables fed with values computed in the shader node code.<br />

</p>

<p>
In practice it's a bit more than that.A shader node is declined in several parts :
</p>
<ul>
<li class="level1"><div class="li"> A shader node definition, defining : </div>
<ul>
<li class="level2"><div class="li"> The type of shader node (Vertex or Fragment for now)</div>
</li>
<li class="level2"><div class="li"> The minimal glsl version needed for the shader node</div>
</li>
<li class="level2"><div class="li"> The path to the shader file (containing the shader code heh)</div>
</li>
<li class="level2"><div class="li"> <strong>A mandatory documentation block</strong> for this Shader node. As I hope many users will do their own nodes and contribute them back this point is crucial.</div>
</li>
<li class="level2"><div class="li"> A list of inputs accepted by this shader (typed glsl variable optional or needed for the code to run properly)</div>
</li>
<li class="level2"><div class="li"> A list of outputs produced by this shader (typed glsl variable computed and fed by the node's code)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> The actual shader code file (.vert or .frag depending on the node's type like any shader file)</div>
</li>
<li class="level1"><div class="li"> A shader node declaration having :</div>
<ul>
<li class="level2"><div class="li"> A unique name(in the shader scope)</div>
</li>
<li class="level2"><div class="li"> The shader node definition it's based on</div>
</li>
<li class="level2"><div class="li"> An optional activation condition (based on the actual define system)</div>
</li>
<li class="level2"><div class="li"> A list of input mapping (what will be actually fed to those inputs)</div>
</li>
<li class="level2"><div class="li"> A list of output mapping (what will be output to the global output of the shader)</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "What is a Shader Node?" [1349-2801] -->
<h3 class="sectionedit4" id="shader_node_definition">Shader Node definition</h3>
<div class="level3">

<p>
First ShaderNodes have to be defined either in a separate file (j3sn for jme3 shader node) or directly embed in the Technique block of the j3md file.<br />

Please refer to this documentation for global structure of a j3md file 
<a href="/jme3/advanced/material_specification.html" class="wikilink1" title="jme3:advanced:material_specification">jMonkeyEngine3 Material Specification</a>
</p>

<p>
All is included in a <strong>ShaderNodeDefinitions</strong> bloc. This block can have several nodes defined (it's recommended to define nodes that have strong dependencies with each other in the same j3sn file).<br />

A ShaderNode is declared in a <strong>ShaderNodeDefinition</strong> block.<br />

global structure should look like this :<br />

</p>
<pre class="code java">ShaderNodeDefinitions<span class="br0">{</span>
      ShaderNodeDefinition <span class="sy0">&lt;</span>NodeDefName<span class="sy0">&gt;</span><span class="br0">{</span>
            Type <span class="sy0">:</span> <span class="sy0">&lt;</span>ShaderType<span class="sy0">&gt;</span> 
            Shader <span class="sy0">&lt;</span>ShaderLangAndVersion<span class="sy0">&gt;</span> <span class="sy0">:</span> <span class="sy0">&lt;</span>ShaderPath<span class="sy0">&gt;</span>
            <span class="br0">[</span>Shader <span class="sy0">&lt;</span>ShaderLangAndVersion<span class="sy0">&gt;</span> <span class="sy0">:</span> <span class="sy0">&lt;</span>ShaderPath<span class="sy0">&gt;</span><span class="br0">]</span>
            <span class="br0">[</span>...<span class="br0">]</span>
            Documentation <span class="br0">{</span>
                <span class="sy0">&lt;</span>DocContent<span class="sy0">&gt;</span>
            <span class="br0">}</span> 
            Input <span class="br0">{</span>
                <span class="sy0">&lt;</span>GlslVarType<span class="sy0">&gt;</span> <span class="sy0">&lt;</span>VarName<span class="sy0">&gt;</span>
                <span class="br0">[</span><span class="sy0">&lt;</span>GlslVarType<span class="sy0">&gt;</span> <span class="sy0">&lt;</span>VarName<span class="sy0">&gt;</span><span class="br0">]</span>
                <span class="br0">[</span>...<span class="br0">]</span>
            <span class="br0">}</span>
            Output <span class="br0">{</span>
                <span class="sy0">&lt;</span>GlslVarType<span class="sy0">&gt;</span> <span class="sy0">&lt;</span>VarName<span class="sy0">&gt;</span>
                <span class="br0">[</span><span class="sy0">&lt;</span>GlslVarType<span class="sy0">&gt;</span> <span class="sy0">&lt;</span>VarName<span class="sy0">&gt;</span><span class="br0">]</span>
                <span class="br0">[</span>...<span class="br0">]</span>
            <span class="br0">}</span>
      <span class="br0">}</span>
      <span class="br0">[</span>ShaderNodeDefinition <span class="sy0">&lt;</span>NodeDef2Name<span class="sy0">&gt;</span> <span class="br0">{</span>
         <span class="br0">[</span>...<span class="br0">]</span>
      <span class="br0">}</span><span class="br0">]</span>
      <span class="br0">[</span>...<span class="br0">]</span>
<span class="br0">}</span></pre>

<p>
All that is not between [] is mandatory.<br />

</p>
<ul>
<li class="level1"><div class="li"> <em class="u">ShaderNodeDefinition</em> : the definition block. You can have several definition in the same ShaderNodeDefinitions block.</div>
<ul>
<li class="level2"><div class="li"> <strong>NodeDefName</strong> : The name of this ShaderNodeDefinition</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <em class="u">Type</em> : define the type of this shader node</div>
<ul>
<li class="level2"><div class="li"> <strong>ShaderType</strong> : The type of shader for this definition. For now only “Vertex” and “Fragment” are supported.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <em class="u">Shader</em> : the version and path of the shader code to use. note that you can have several shader with different GLSL version. The generator will pick the relevant one according to GPU capabilities.</div>
<ul>
<li class="level2"><div class="li"> <strong>ShaderLangAndVersion</strong> : follows the same syntax than the shader declaration in the j3md file : GLSL&lt;version&gt;, version being 100 for glsl 1.0 , 130 for glsl 1.3, 150 for glsl 1.5 and so on. Note that this is the <strong>minimum</strong> glsl version this shader supports</div>
</li>
<li class="level2"><div class="li"> <strong>ShaderPath</strong> the path to the shader code file (relative to the asset folder)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <em class="u">Documentation</em> : the documentation block. This is mandatory and I really recommend filling this if you want to contribute your shader nodes. This documentation will be read buy the SDK and presented to users willing to add this node to their material definitions. This should contain a brief description of the node and a description for each input and ouput.</div>
<ul>
<li class="level2"><div class="li"> <strong>@input</strong> can be use to prefix an input name so the sdk recognize it and format it accordingly. the syntax id @input &lt;inputName&gt; &lt;description&gt;.</div>
</li>
<li class="level2"><div class="li"> <strong>@output</strong> can be use to prefix an output name so the sdk recognize it and format it accordingly. the syntax id @output &lt;inputName&gt; &lt;description&gt;</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <em class="u">Input</em> : The input block containing all the inputs of this node. A node can have 1 or several inputs.</div>
<ul>
<li class="level2"><div class="li"> <strong>GlslVarType</strong> : a valid glsl variable type that will be used in the shader for this input. see <a href="http://www.opengl.org/wiki/GLSL_Type" class="urlextern" title="http://www.opengl.org/wiki/GLSL_Type" rel="nofollow">http://www.opengl.org/wiki/GLSL_Type</a> and the “Declare an array” chapter</div>
</li>
<li class="level2"><div class="li"> <strong>VarName</strong> : the name of the variable. Note that you can't have several inputs with the same name.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <em class="u">Output</em> : The output block containing all the outputs of this node. A node can have 1 or several outputs.</div>
<ul>
<li class="level2"><div class="li"> <strong>GlslVarType</strong> : a valid glsl variable type that will be used in the shader for this input. see <a href="http://www.opengl.org/wiki/GLSL_Type" class="urlextern" title="http://www.opengl.org/wiki/GLSL_Type" rel="nofollow">http://www.opengl.org/wiki/GLSL_Type</a> and the “Declare an array” chapter</div>
</li>
<li class="level2"><div class="li"> <strong>VarName</strong> : the name of the variable. Note that you can't have several outputs with the same name.</div>
</li>
</ul>
</li>
</ul>

<p>
<strong> Note that if you use the same name for an input and an ouput, the generator will consider them as the SAME variable so they should be of the same glsl type.</strong>
</p>

</div>

<h4 id="example">Example</h4>
<div class="level4">

<p>
Here is a typical shader node definition
</p>
<pre class="code java">ShaderNodeDefinitions<span class="br0">{</span>
     ShaderNodeDefinition LightMapping<span class="br0">{</span>
        Type<span class="sy0">:</span> Fragment
        Shader GLSL100<span class="sy0">:</span> Common<span class="sy0">/</span>MatDefs<span class="sy0">/</span>ShaderNodes<span class="sy0">/</span>LightMapping<span class="sy0">/</span>lightMap.<span class="me1">frag</span>
        Documentation <span class="br0">{</span>
            <span class="kw1">This</span> Node is responsible <span class="kw1">for</span> multiplying a light mapping contribution to a given color.   
            @input texCoord the texture coordinates to use <span class="kw1">for</span> light mapping
            @input lightMap the texture to use <span class="kw1">for</span> light mapping   
            @input color the color the lightmap color will be multiplied to
            @output color the resulting color             
        <span class="br0">}</span>
        Input<span class="br0">{</span>            
            vec2 texCoord
            sampler2D lightMap    
            vec4 color               
        <span class="br0">}</span>
        Output<span class="br0">{</span>
            vec4 color
        <span class="br0">}</span>
    <span class="br0">}</span>   
<span class="br0">}</span>    </pre>

</div>

<h4 id="declare_an_array">Declare an array</h4>
<div class="level4">

<p>
To declare an array you have to specify its size between square brackets.<br />

<strong>Constant size</strong><br />

The size can be an int constant<br />

<em>Example</em>
</p>
<pre class="code">      float myArray[10]</pre>

<p>
this will declare a float array with 10 elements.
Any material parameter mapped with this array should be of FloatArray type and it's size will be assumed as 10 when the shader is generated.<br />

</p>

<p>
<strong>Material parameter driven size</strong><br />

The size can be dynamic and driven by a material parameter. GLSL does not support non constant values for array declaration so this material parameter will be mapped to a define.<br />

<em>Example</em>
</p>
<pre class="code">     float myArray[NumberOfElements]</pre>

<p>
This declares a float array with the size depending on the value of the NumberOfElement material parameter.<br />

NumberOfElement <strong>HAS</strong> to be declared in the material definition as a material parameter. It will be mapped to a define and used in the shader.
Not that if this value change the shader will have to be recompiled, due to the fact that it's mapped to a define.
</p>

</div>
<!-- EDIT4 SECTION "Shader Node definition" [2802-8620] -->
<h3 class="sectionedit5" id="shader_node_code">Shader Node code</h3>
<div class="level3">

<p>
The shader code associated with a Shader node is similar to any shader code.<br />

the code for a Vertex shader node should be in a .vert file and the code for a Fragment shader node should be in a .frag file.
It has a declarative part containing variable declaration, function declaration and so on… And a main part that is embed in a “void main(){}” block.<br />

Input and output variables declared in the shader node definition can be used <strong>without</strong> being declared in the shader code. ( they shouldn't even or you'll have issues).<br />

Here is a the code of the LightMap.frag shader.<br />

</p>
<pre class="code java"><span class="kw4">void</span> main<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    color <span class="sy0">*=</span> texture2D<span class="br0">(</span>lightMap, texCoord<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Very simple, it's just a texture fetch, but of course anything can be done.<br />

<strong>Do not declare uniforms, attributes or varyings in a shader node code</strong>, the Generator will handle this, just use the inputs and outputs and optional local variables you may need.
</p>

</div>
<!-- EDIT5 SECTION "Shader Node code" [8621-9569] -->
<h3 class="sectionedit6" id="shader_node_declaration">Shader Node declaration</h3>
<div class="level3">

<p>
To create a shader we need to plug shader nodes to each other, but also interact with built in glsl inputs and outputs.
Shader nodes are declared inside the Technique block. The vertex nodes are declared in the VertexShaderNodes block and the fragment nodes are declared in the FragmentShaderNodes block.<br />

Note that if the j3md has ember shader nodes definition (in a ShaderNodesDefinitions block) it <strong>must</strong> be declared before the VertexShaderNodes and FragmentShaderNodes blocks.
Of course there can be several ShaderNode declaration in those block.<br />

Here is how a ShaderNode declaration should look :
</p>
<pre class="code java">ShaderNode <span class="sy0">&lt;</span>ShaderNodeName<span class="sy0">&gt;</span><span class="br0">{</span>
     Definition <span class="sy0">:</span> <span class="sy0">&lt;</span>DefinitionName<span class="sy0">&gt;</span> <span class="br0">[</span><span class="sy0">:</span> <span class="sy0">&lt;</span>DefinitionPath<span class="sy0">&gt;</span><span class="br0">]</span>
     <span class="br0">[</span>Condition <span class="sy0">:</span> <span class="sy0">&lt;</span>ActivationCondition<span class="sy0">&gt;</span><span class="br0">]</span>
     InputMapping<span class="br0">{</span>
          <span class="sy0">&lt;</span>InputVariableName<span class="sy0">&gt;</span><span class="br0">[</span>.<span class="sy0">&lt;</span>Swizzle<span class="sy0">&gt;</span><span class="br0">]</span> <span class="sy0">=</span> <span class="sy0">&lt;</span>NameSpace<span class="sy0">&gt;</span>.<span class="sy0">&lt;</span>VarName<span class="sy0">&gt;</span><span class="br0">[</span>.<span class="sy0">&lt;</span>Swizzle<span class="sy0">&gt;</span><span class="br0">]</span> <span class="br0">[</span><span class="sy0">:</span> <span class="sy0">&lt;</span>MappingCondition<span class="sy0">&gt;</span><span class="br0">]</span>
          <span class="br0">[</span>...<span class="br0">]</span>
     <span class="br0">}</span>
     <span class="br0">[</span>OutputMapping<span class="br0">{</span>
          <span class="sy0">&lt;</span>NameSpace<span class="sy0">&gt;</span>.<span class="sy0">&lt;</span>VarName<span class="sy0">&gt;</span><span class="br0">[</span>.<span class="sy0">&lt;</span>Swizzle<span class="sy0">&gt;</span><span class="br0">]</span> <span class="sy0">=</span> <span class="sy0">&lt;</span>OutputVariableName<span class="sy0">&gt;</span><span class="br0">[</span>.<span class="sy0">&lt;</span>Swizzle<span class="sy0">&gt;</span><span class="br0">]</span> <span class="br0">[</span><span class="sy0">:</span> <span class="sy0">&lt;</span>MappingCondition<span class="sy0">&gt;</span><span class="br0">]</span>
          <span class="br0">[</span>...<span class="br0">]</span>
     <span class="br0">}</span><span class="br0">]</span>
<span class="br0">}</span></pre>
<ul>
<li class="level1"><div class="li"> <em class="u">ShaderNode</em> the shader node block</div>
<ul>
<li class="level2"><div class="li"> <strong>ShaderNodeName</strong> the name of this shader node, can be anything, but has to be <strong>unique</strong> in the shader scope</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <em class="u">Definition</em> : a reference to the shader node definition</div>
<ul>
<li class="level2"><div class="li"> <strong>DefinitionName</strong> : the name of the definition this Node use. this definition can be declared in the same j3md or in its own j3sn file.</div>
</li>
<li class="level2"><div class="li"> <strong>DefinitionPath</strong> : in case the definition is declared in it's own j3sn file, you have to set the path to this file here.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <em class="u">Condition</em> a condition that dictates if the node is active or not.</div>
<ul>
<li class="level2"><div class="li"> <strong>Activationcondition</strong> : The condition for this node to be used. Today we use Defines to use different blocks of code used depending on the state of a Material Parameter. The condition here use the exact same paradigm. A valid condition must be the name of a material parameter or any combinations using logical operators “||”,“&amp;&amp;”,“!” or grouping characters “(” and “)”. The generator will create the corresponding define and the shader node code will be embed into and #ifdef statement.<br />
</div>
</li>
</ul>
</li>
</ul>

<p>
    For example, let's say we have a Color and ColorMap material parameter, this condition “Color || ColorMap” will generate this statement :
</p>
<pre class="code java">        #if defined<span class="br0">(</span>COLOR<span class="br0">)</span> <span class="sy0">||</span> defined<span class="br0">(</span>COLORMAP<span class="br0">)</span>
            ...
        #endif</pre>
<ul>
<li class="level1"><div class="li"> <em class="u">InputMapping</em> the wiring of the inputs of this node, coming from previous node's outputs or from built in glsl inputs.</div>
<ul>
<li class="level2"><div class="li"> <strong>InputVariableName</strong> : the name of the variable to map as declared in the definition.</div>
</li>
<li class="level2"><div class="li"> <strong>Swizzle</strong> : Swizling for the preceding variable. More information on glsl swizzling on this page <a href="http://www.opengl.org/wiki/GLSL_Type" class="urlextern" title="http://www.opengl.org/wiki/GLSL_Type" rel="nofollow">http://www.opengl.org/wiki/GLSL_Type</a></div>
</li>
<li class="level2"><div class="li"> <strong>NameSpace</strong> : The generator will use variable name space to avoid collision between variable names. Name space can be one of these values : </div>
<ul>
<li class="level3"><div class="li"> <strong>MatParam</strong> : the following variable is a Material Parameter declared in the MaterialParameters block of the materialDefinition</div>
</li>
<li class="level3"><div class="li"> <strong>WorldParam</strong> : the following variable is a World Parameter declared in the WorldParameters block of the current technique block. World parameters can be one of those declared in this file : <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/shader/UniformBinding.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/shader/UniformBinding.java" rel="nofollow">https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/shader/UniformBinding.java</a></div>
</li>
<li class="level3"><div class="li"> <strong>Attr</strong> : the following variable is a shader attribute. It can be one those declared in the Type enum of the VertexBuffer class <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/VertexBuffer.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/VertexBuffer.java" rel="nofollow">https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/VertexBuffer.java</a></div>
</li>
<li class="level3"><div class="li"> <strong>Global</strong> : the variable is a global variable to the shader. Global variables will be assign at the end of the shader to glsl built in outputs : gl_Position for the vertex shader, or to one of the possible outputs of the fragment shader (for example  gl_FragColor). The global variable can have what ever name pleases you, it will assigned in the order they've been found in the declaration to the shader output. <strong>Global variables can be inputs of a shader node. Global variables are forced to be vec4 and are defaulted to the value of the attribute inPosition in the vertex shader and vec4(1.0)(opaque white color) in the fragment shader</strong>.</div>
</li>
<li class="level3"><div class="li"> <strong>The name of a previous shader node</strong> : this must be followed by and output variable of a the named shader node. This is what allows one to plug outputs from a node to inputs of another.</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> <strong>VarName</strong> : the name of the variable to assign to the input. This variable must be known in name space declared before.</div>
</li>
<li class="level2"><div class="li"> <strong>MappingCondition</strong> : Follows the same rules as the activation condition for the shaderNode, this mapping will be embed in a #ifdef statement n the resulting shader.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <em class="u">OutputMapping</em> : This block is optional, as mapping of output will be done in input mapping block of following shaderNodes, ecept if you want to output a value to the Global output of the shader.</div>
<ul>
<li class="level2"><div class="li"> <strong>NameSpace</strong> : the name space of the output to assign, this can only be “Global” here.</div>
</li>
<li class="level2"><div class="li"> <strong>VarName</strong> : the name of a global output (can be anything, just be aware that 2 different names result in 2 different outputs)</div>
</li>
<li class="level2"><div class="li"> <strong>OutputVariable</strong> : Must be an output of the current node's definition.</div>
</li>
<li class="level2"><div class="li"> <strong>MappingCondition</strong> : Same as before.</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Shader Node declaration" [9570-14879] -->
<h3 class="sectionedit7" id="complete_material_definition_and_shader_nodes_example">Complete material definition and Shader Nodes example</h3>
<div class="level3">

<p>
Here is an example of a very simple Material definition that just displays a solid color (controlled by a material parameter) on a mesh.
</p><p></p><div class="noteimportant">Shader Nodes only work if there is no shader declared in the technique. If you want to bypass the Shader Nodes, you can put a VertexShader and a FragmentShader statement in the technique and the shader nodes will be ignored. 
</div>

<pre class="code java">MaterialDef Simple <span class="br0">{</span>
    MaterialParameters <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>
    <span class="br0">}</span>
    Technique <span class="br0">{</span>
        WorldParameters <span class="br0">{</span>
            WorldViewProjectionMatrix
        <span class="br0">}</span>
        VertexShaderNodes <span class="br0">{</span>
            ShaderNode CommonVert <span class="br0">{</span>
                Definition <span class="sy0">:</span> CommonVert <span class="sy0">:</span> Common<span class="sy0">/</span>MatDefs<span class="sy0">/</span>ShaderNodes<span class="sy0">/</span>Common<span class="sy0">/</span>CommonVert.<span class="me1">j3sn</span>
                InputMappings <span class="br0">{</span>
                    worldViewProjectionMatrix <span class="sy0">=</span> WorldParam.<span class="me1">WorldViewProjectionMatrix</span>
                    modelPosition <span class="sy0">=</span> Global.<span class="me1">position</span>.<span class="me1">xyz</span>
                <span class="br0">}</span>
                OutputMappings <span class="br0">{</span>
                    Global.<span class="me1">position</span> <span class="sy0">=</span> projPosition
                <span class="br0">}</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
        FragmentShaderNodes <span class="br0">{</span>
            ShaderNode ColorMult <span class="br0">{</span>
                Definition <span class="sy0">:</span> ColorMult <span class="sy0">:</span> Common<span class="sy0">/</span>MatDefs<span class="sy0">/</span>ShaderNodes<span class="sy0">/</span>Basic<span class="sy0">/</span>ColorMult.<span class="me1">j3sn</span>
                InputMappings <span class="br0">{</span>
                    color1 <span class="sy0">=</span> MatParam.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>
                    color2 <span class="sy0">=</span> Global.<span class="me1">color</span>
                <span class="br0">}</span>
                OutputMappings <span class="br0">{</span>
                    Global.<span class="me1">color</span> <span class="sy0">=</span> outColor
                <span class="br0">}</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
This Material definition has one Default technique with 2 node declarations.<br />

<em class="u"><strong>CommonVert Definition</strong></em><br />

CommonVert is a vertex shader node that has commonly used input and outputs of a vertex shader. It also computes the position of the vertex in projection space
here is the definition content (Common/MatDefs/ShaderNodes/Common/CommonVert.j3sn) : 
</p>
<pre class="code java">ShaderNodesDefinitions <span class="br0">{</span>
    ShaderNodeDefinition CommonVert <span class="br0">{</span>
        Type<span class="sy0">:</span> Vertex
        Shader GLSL100<span class="sy0">:</span> Common<span class="sy0">/</span>MatDefs<span class="sy0">/</span>ShaderNodes<span class="sy0">/</span>Common<span class="sy0">/</span>commonVert.<span class="me1">vert</span>
        Documentation <span class="br0">{</span>
            <span class="kw1">This</span> Node is responsible <span class="kw1">for</span> computing vertex position in projection space.
            <span class="me1">It</span> also can pass texture coordinates <span class="nu0">1</span> <span class="sy0">&amp;</span> <span class="nu0">2</span>, and vertexColor to the frgment shader as varying <span class="br0">(</span>or inputs <span class="kw1">for</span> glsl <span class="sy0">&gt;=</span><span class="nu0">1.3</span><span class="br0">)</span>                   
            @input modelPosition the vertex position in model space <span class="br0">(</span>usually assigned with Attr.<span class="me1">inPosition</span> or Global.<span class="me1">position</span><span class="br0">)</span>
            @input worldViewProjectionMatrix the World <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+view"><span class="kw3">View</span></a> Projection Matrix transforms model space to projection space.
            @input texCoord1 The first texture coordinates of the vertex <span class="br0">(</span>usually assigned with Attr.<span class="me1">inTexCoord</span><span class="br0">)</span>
            @input texCoord2 The second texture coordinates of the vertex <span class="br0">(</span>usually assigned with Attr.<span class="me1">inTexCoord2</span><span class="br0">)</span>
            @input vertColor The color of the vertex <span class="br0">(</span>usually assigned with Attr.<span class="me1">inColor</span><span class="br0">)</span>                    
            @output projPosition <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> of the vertex in projection space.<span class="br0">(</span>usually assigned to Global.<span class="me1">position</span><span class="br0">)</span>
            @output vec2 texCoord1 The first texture coordinates of the vertex <span class="br0">(</span>output as a varying<span class="br0">)</span>
            @output vec2 texCoord2 The second texture coordinates of the vertex <span class="br0">(</span>output as a varying<span class="br0">)</span>
            @output vec4 vertColor The color of the vertex <span class="br0">(</span>output as a varying<span class="br0">)</span>
        <span class="br0">}</span>                
        Input<span class="br0">{</span>
            vec3 modelPosition                    
            mat4 worldViewProjectionMatrix                    
            vec2 texCoord1
            vec2 texCoord2
            vec4 vertColor
        <span class="br0">}</span>
        Output<span class="br0">{</span>
            vec4 projPosition
            vec2 texCoord1
            vec2 texCoord2
            vec4 vertColor
        <span class="br0">}</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
</p><p></p><div class="notetip">Note that texCoord1/2 and vertColor are declared both as input and output. the generator will use the same variables for them
</div>
here is the shader Node code ( Common/MatDefs/ShaderNodes/Common/commonVert.vert)

<pre class="code java"><span class="kw4">void</span> main<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    projPosition <span class="sy0">=</span> worldViewProjectionMatrix <span class="sy0">*</span> vec4<span class="br0">(</span>modelPosition, <span class="nu0">1.0</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
As you can see all the inputs and outputs are not used. that's because most of them are attributes meant to be passed to the fragment shader as varyings. all the wiring will be handled by the generator only if those variables are used in an input or output mapping.<br />

</p>

<p>
<em class="u"><strong>CommonVert input mapping</strong></em><br />

here we have the most basic yet mandatory thing in a vertex shader, computing vertex position in projection space. for this we have 2 mapping :
</p>
<ul>
<li class="level1"><div class="li"> <strong>worldViewProjectionMatrix = WorldParam.WorldViewProjectionMatrix</strong> : the input parameter worldViewProjectionMatrix is assigned with the WorldViewProjectionMatrix World parameter declared in the WorlParameters block of the technique.</div>
</li>
<li class="level1"><div class="li"> <strong>modelPosition = Global.position.xyz</strong> : the modelPosition (understand the vertex position in the model coordinate space) is assigned with the Global position variable.</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">As mentioned before Global position is initialized with the attribute inPosition, so this is equivalent to : modelPosition = Attr.inPosition.xyz
</div>
<p></p><div class="notetip">also note the swizzle of the Global.position variable. modelPosition is a vec3 and GlobalPosition is a vec4 so we just take the first 3 components.
</div>
<em class="u"><strong>CommonVert output mapping</strong></em><br />


<ul>
<li class="level1"><div class="li"> <strong>Global.position = projPosition</strong> : The result of the multiplication of the worldViewProjectionMatrix  and the modelPosition is assigned to the Globale position</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">The Global.position variable will be assigned to the gl_Position glsl built in output at the end of the shader.
</div>
<em class="u"><strong>ColorMult Definition</strong></em><br />

ColorMult is a very basic Shader Node that takes two colors as input and multiply them.
here is the definition content (Common/MatDefs/ShaderNodes/Basic/ColorMult.j3sn) : 

<pre class="code java">ShaderNodeDefinitions<span class="br0">{</span>
    ShaderNodeDefinition ColorMult <span class="br0">{</span>      
        Type<span class="sy0">:</span> Fragment
        Shader GLSL100<span class="sy0">:</span> Common<span class="sy0">/</span>MatDefs<span class="sy0">/</span>ShaderNodes<span class="sy0">/</span>Basic<span class="sy0">/</span>colorMult.<span class="me1">frag</span>
        Documentation<span class="br0">{</span>
            Multiplies two colors
            @input color1 the first color
            @input color2 the second color            
            @output outColor the resulting color
        <span class="br0">}</span>
        Input <span class="br0">{</span>
            vec4 color1
            vec4 color2            
        <span class="br0">}</span>
        Output <span class="br0">{</span>
            vec4 outColor
        <span class="br0">}</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
here is the shader Node code (Common/MatDefs/ShaderNodes/Basic/colorMult.frag)
</p>
<pre class="code java"><span class="kw4">void</span> main<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    outColor <span class="sy0">=</span> color1 <span class="sy0">*</span> color2<span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
<em class="u"><strong>ColorMult input mapping</strong></em><br />

All inputs are mapped here :
</p>
<ul>
<li class="level1"><div class="li"> <strong>color1 = MatParam.Color</strong> : The first color is assigned to the Color Material parameter declared in the MaterialParameter block of the material definition  </div>
</li>
<li class="level1"><div class="li"> <strong>color2 = Global.color</strong> : The second color is assigned with the Global color variable. this is defaulted to vec4(1.0) (opaque white). Note that in a much complex material def this variable could already have been assigned with a previous Shader Node output</div>
</li>
</ul>

<p>
<em class="u"><strong>ColorMult output mapping</strong></em><br />

</p>
<ul>
<li class="level1"><div class="li"> <strong>Global.color = outColor</strong> : the resulting color is assigned to the Global color variable.</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">Note that the Global.color variable will be assigned to gl_FragColor (glsl &lt; 1.5) or declared as a Global ouput of the shader (glsl &gt;= 1.5).
</div>
<p></p><div class="notetip">Also note that in case several Global variables are declared, the generator will assign them gl_FragData[i](glsl &lt; 1.5) i being the order the variable has been found in the material def. For glsl &gt;= 1.5 the veriable will just all be declared as shader output in the order they've been found in the declaration
</div>


<p>
<em class="u"><strong>Generated shader code</strong></em><br />

</p><p></p><div class="noteimportant">Don't take this code as carved in stone, the generated code can change as optimization of the shader generator goes on
</div>
Vertex Shader (glsl 1.0)

<pre class="code java">uniform mat4 g_WorldViewProjectionMatrix<span class="sy0">;</span>
 
attribute vec4 inPosition<span class="sy0">;</span>
 
<span class="kw4">void</span> main<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        vec4 Global_position <span class="sy0">=</span> inPosition<span class="sy0">;</span>
 
        <span class="co1">//CommonVert : Begin</span>
        vec3 CommonVert_modelPosition <span class="sy0">=</span> Global_position.<span class="me1">xyz</span><span class="sy0">;</span>
        vec4 CommonVert_projPosition<span class="sy0">;</span>
        vec2 CommonVert_texCoord1<span class="sy0">;</span>
        vec2 CommonVert_texCoord2<span class="sy0">;</span>
        vec4 CommonVert_vertColor<span class="sy0">;</span>
 
        CommonVert_projPosition <span class="sy0">=</span> g_WorldViewProjectionMatrix <span class="sy0">*</span> vec4<span class="br0">(</span>CommonVert_modelPosition, <span class="nu0">1.0</span><span class="br0">)</span><span class="sy0">;</span>
        Global_position <span class="sy0">=</span> CommonVert_projPosition<span class="sy0">;</span>
        <span class="co1">//CommonVert : End</span>
 
        gl_Position <span class="sy0">=</span> Global_position<span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
All materials parameter, world parameters, attributes varying are declared first. then for each shader node, the declarative part is appended.<br />

For the main function, for each shader node, the input mappings are declared and assigned, the output are declared.<br />

Then the variable names are replaced in the sahder node code with there complete name (NameSpace_varName), material parameters are replaced in the shader code as is.<br />

Then, the output are mapped.<br />

</p>

<p>
As you can see texCoord1/2 and vertColor are declared but never used. That's because the generator is not aware of that. By default it will declare all inputs in case they are used in the shaderNode code.
Note that most glsl compiler will optimize this when compiling the shader on the GPU.
</p>

<p>
Fragment Shader (glsl 1.0)
</p>
<pre class="code java">uniform vec4 m_Color<span class="sy0">;</span>
 
<span class="kw4">void</span> main<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        vec4 Global_color <span class="sy0">=</span> vec4<span class="br0">(</span><span class="nu0">1.0</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//ColorMult : Begin</span>
        vec4 ColorMult_color2 <span class="sy0">=</span> Global_color<span class="sy0">;</span>
        vec4 ColorMult_outColor<span class="sy0">;</span>
 
        ColorMult_outColor <span class="sy0">=</span> m_Color <span class="sy0">*</span> ColorMult_color2<span class="sy0">;</span>
        Global_color <span class="sy0">=</span> ColorMult_outColor<span class="sy0">;</span>
        <span class="co1">//ColorMult : End</span>
 
        gl_FragColor <span class="sy0">=</span> Global_color<span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Same as for the Vertex shader. note that the color1 is not declared, because it's directly replaced by the material parameter.
</p>

<p>
</p><p></p><div class="noteimportant">As a rule of thumb you should not assign a value to an input. input are likely to be material paramters or  outputs from other shaders and modifying them may cause unexpected behavior, even failure in your resulting shader.
</div>


<p>
For more explanations and design decisions please refer to the <abbr title="specification">spec</abbr> here 
<a href="https://docs.google.com/document/d/1S6xO3d1TBz0xcKe_MPTqY9V-QI59AKdg1OGy3U-HeVY/edit?usp=sharing" class="urlextern" title="https://docs.google.com/document/d/1S6xO3d1TBz0xcKe_MPTqY9V-QI59AKdg1OGy3U-HeVY/edit?usp=sharing" rel="nofollow">https://docs.google.com/document/d/1S6xO3d1TBz0xcKe_MPTqY9V-QI59AKdg1OGy3U-HeVY/edit?usp=sharing</a>
</p>

<p>
Thank you for the brave ones that came through all this reading. i'm not gonna offer you a prize in exchange of a password, because we ran out of JME thongs…
</p>

</div>
<!-- EDIT7 SECTION "Complete material definition and Shader Nodes example" [14880-] -->
