---
title: jMonkeyEngine 3 Tutorial (6) - Hello Materials
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_6_-_hello_materials">jMonkeyEngine 3 Tutorial (6) - Hello Materials</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">Hello Input System</a>,
Next: <a href="/jme3/beginner/hello_animation.html" class="wikilink1" title="jme3:beginner:hello_animation">Hello Animation</a>
</p>

<p>
The term Material includes everything that influences what the surface of a 3D model looks like: The color, texture, shininess, and opacity/transparency. Plain coloring is covered in <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a>. Loading models that come with materials is covered in <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">Hello Asset</a>. In this tutorial you learn to create and use custom JME3 Material Definitions.
<a href="/resources/jme3-beginner-beginner-materials.png" class="media" title="jme3:beginner:beginner-materials.png"><img src="/resources/jme3-beginner-beginner-materials.png" class="mediacenter" alt="" width="320" height="240" /></a>
</p>

<p>
</p><p></p><div class="notetip">To use the example assets in a new jMonkeyEngine SDK project, right-click your project, select “Properties”, go to “Libraries”, press “Add Library” and add the “jme3-test-data” library.
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (6) - Hello Materials" [1-715] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.RenderState.BlendMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.queue.RenderQueue.Bucket</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Sphere</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.util.TangentBinormalGenerator</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 6 - how to give an object's surface a material and texture.
 * How to make objects transparent. How to make bumpy and shiny surfaces.  */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloMaterial <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloMaterial app <span class="sy0">=</span> <span class="kw1">new</span> HelloMaterial<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
    <span class="co3">/** A simple textured cube -- in good MIP map quality. */</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> cube1Mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> 1f,1f,1f<span class="br0">)</span><span class="sy0">;</span>
    Geometry cube1Geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"My Textured Box"</span>, cube1Mesh<span class="br0">)</span><span class="sy0">;</span>
    cube1Geo.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>3f,1.1f,0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    Material cube1Mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
        <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    Texture cube1Tex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
        <span class="st0">"Interface/Logo/Monkey.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    cube1Mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, cube1Tex<span class="br0">)</span><span class="sy0">;</span>
    cube1Geo.<span class="me1">setMaterial</span><span class="br0">(</span>cube1Mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>cube1Geo<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** A translucent/transparent texture, similar to a window frame. */</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> cube2Mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> 1f,1f,0.01f<span class="br0">)</span><span class="sy0">;</span>
    Geometry cube2Geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"window frame"</span>, cube2Mesh<span class="br0">)</span><span class="sy0">;</span>
    Material cube2Mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
        <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    cube2Mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, 
        assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/ColoredTex/Monkey.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    cube2Mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBlendMode</span><span class="br0">(</span>BlendMode.<span class="me1">Alpha</span><span class="br0">)</span><span class="sy0">;</span>
    cube2Geo.<span class="me1">setQueueBucket</span><span class="br0">(</span>Bucket.<span class="me1">Transparent</span><span class="br0">)</span><span class="sy0">;</span>
    cube2Geo.<span class="me1">setMaterial</span><span class="br0">(</span>cube2Mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>cube2Geo<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** A bumpy rock with a shiny light effect.*/</span>
    Sphere sphereMesh <span class="sy0">=</span> <span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">32</span>,<span class="nu0">32</span>, 2f<span class="br0">)</span><span class="sy0">;</span>
    Geometry sphereGeo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Shiny rock"</span>, sphereMesh<span class="br0">)</span><span class="sy0">;</span>
    sphereMesh.<span class="me1">setTextureMode</span><span class="br0">(</span>Sphere.<span class="me1">TextureMode</span>.<span class="me1">Projected</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// better quality on spheres</span>
    TangentBinormalGenerator.<span class="me1">generate</span><span class="br0">(</span>sphereMesh<span class="br0">)</span><span class="sy0">;</span>           <span class="co1">// for lighting effect</span>
    Material sphereMat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
        <span class="st0">"Common/MatDefs/Light/Lighting.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    sphereMat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"DiffuseMap"</span>, 
        assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/Pond/Pond.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    sphereMat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"NormalMap"</span>, 
        assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/Pond/Pond_normal.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    sphereMat.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"UseMaterialColors"</span>,<span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>    
    sphereMat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Diffuse"</span>,ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
    sphereMat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Specular"</span>,ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
    sphereMat.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Shininess"</span>, 64f<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// [0,128]</span>
    sphereGeo.<span class="me1">setMaterial</span><span class="br0">(</span>sphereMat<span class="br0">)</span><span class="sy0">;</span>
    sphereGeo.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">2</span>,<span class="sy0">-</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Move it a bit</span>
    sphereGeo.<span class="me1">rotate</span><span class="br0">(</span>1.6f, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>          <span class="co1">// Rotate it a bit</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>sphereGeo<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** Must add a light to make the lit object visible! */</span>
    DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="sy0">-</span><span class="nu0">2</span><span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    sun.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
 
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
You should see
</p>
<ul>
<li class="level1"><div class="li"> Left – A cube with a brown monkey texture.</div>
</li>
<li class="level1"><div class="li"> Right – A translucent monkey picture in front of a shiny bumpy rock.</div>
</li>
</ul>

<p>
Move around with the WASD keys to have a closer look at the translucency, and the rock's bumpiness.
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [716-4277] -->
<h2 class="sectionedit3" id="simple_unshaded_texture">Simple Unshaded Texture</h2>
<div class="level2">

<p>
Typically you want to give objects in your scene textures: It can be rock, grass, brick, wood, water, metal, paper… A texture is a normal image file in JPG or PNG format. In this example, you create a box with a simple unshaded Monkey texture as material.
</p>
<pre class="code java">    <span class="co3">/** A simple textured cube -- in good MIP map quality. */</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> cube1Mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> 1f,1f,1f<span class="br0">)</span><span class="sy0">;</span>
    Geometry cube1Geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"My Textured Box"</span>, cube1Mesh<span class="br0">)</span><span class="sy0">;</span>
    cube1Geo.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>3f,1.1f,0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    Material cube1Mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
        <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    Texture cube1Tex <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
        <span class="st0">"Interface/Logo/Monkey.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
    cube1Mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, cube1Tex<span class="br0">)</span><span class="sy0">;</span>
    cube1Geo.<span class="me1">setMaterial</span><span class="br0">(</span>cube1Mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>cube1Geo<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Here is what we did: to create a textured box:
</p>
<ol>
<li class="level1"><div class="li"> Create a Geometry <code>cube1Geo</code> from a Box mesh <code>cube1Mesh</code>. </div>
</li>
<li class="level1"><div class="li"> Create a Material <code>cube1Mat</code> based on jME3's default <code>Unshaded.j3md</code> material definition.</div>
</li>
<li class="level1"><div class="li"> Create a texture <code>cube1Tex</code> from the <code>Monkey.jpg</code> file in the <code>assets/Interface/Logo/</code> directory of the project. </div>
</li>
<li class="level1"><div class="li"> Load the texture <code>cube1Tex</code> into the <code>ColorMap</code> layer of the material <code>cube1Mat</code>. </div>
</li>
<li class="level1"><div class="li"> Apply the material to the cube, and attach the cube to the rootnode.</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Simple Unshaded Texture" [4278-5632] -->
<h2 class="sectionedit4" id="transparent_unshaded_texture">Transparent Unshaded Texture</h2>
<div class="level2">

<p>
<code>Monkey.png</code> is the same texture as <code>Monkey.jpg</code>, but with an added alpha channel. The alpha channel allows you to specify which areas of the texture you want to be opaque or transparent: Black areas of the alpha channel remain opaque, gray areas become translucent, and white areas become transparent. 
</p>

<p>
For a partially translucent/transparent texture, you need:
</p>
<ul>
<li class="level1"><div class="li"> A Texture with alpha channel</div>
</li>
<li class="level1"><div class="li"> A Texture with blend mode of <code>BlendMode.Alpha</code></div>
</li>
<li class="level1"><div class="li"> A Geometry in the <code>Bucket.Transparent</code> render bucket.  <br />
This bucket ensures that the transparent object is drawn on top of objects behind it, and they show up correctly under the transparent parts. </div>
</li>
</ul>
<pre class="code java">    <span class="co3">/** A translucent/transparent texture, similar to a window frame. */</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> cube2Mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> 1f,1f,0.01f<span class="br0">)</span><span class="sy0">;</span>
    Geometry cube2Geo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"window frame"</span>, cube2Mesh<span class="br0">)</span><span class="sy0">;</span>
    Material cube2Mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
    <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    cube2Mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, 
        assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/ColoredTex/Monkey.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    cube2Mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBlendMode</span><span class="br0">(</span>BlendMode.<span class="me1">Alpha</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// !</span>
    cube2Geo.<span class="me1">setQueueBucket</span><span class="br0">(</span>Bucket.<span class="me1">Transparent</span><span class="br0">)</span><span class="sy0">;</span>                        <span class="co1">// !</span>
    cube2Geo.<span class="me1">setMaterial</span><span class="br0">(</span>cube2Mat<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>cube2Geo<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For non-transparent objects, the drawing order is not so important, because the z-buffer already keeps track of whether a pixel is behind something else or not, and the color of an opaque pixel doesn't depend on the pixels under it, this is why opaque Geometries can be drawn in any order.
</p>

<p>
What you did for the transparent texture is the same as before, with only one added step for the transparency.
</p>
<ol>
<li class="level1"><div class="li"> Create a Geometry <code>cube2Geo</code> from a Box mesh <code>cube2Mesh</code>. This Box Geometry is flat upright box (because z=0.01f).</div>
</li>
<li class="level1"><div class="li"> Create a Material <code>cube2Mat</code> based on jME3's default <code>Unshaded.j3md</code> material definition.</div>
</li>
<li class="level1"><div class="li"> Create a texture <code>cube2Tex</code> from the <code>Monkey.png</code> file in the <code>assets/Textures/ColoredTex/</code> directory of the project. This PNG file must have an alpha layer.</div>
</li>
<li class="level1"><div class="li"> <strong>Activate transparency in the material by setting the blend mode to Alpha.</strong></div>
</li>
<li class="level1"><div class="li"> <strong>Set the QueueBucket of the Geometry to <code>Bucket.Transparent</code>.</strong></div>
</li>
<li class="level1"><div class="li"> Load the texture <code>cube2Tex</code> into the <code>ColorMap</code> layer of the material <code>cube2Mat</code>.</div>
</li>
<li class="level1"><div class="li"> Apply the material to the cube, and attach the cube to the rootnode.</div>
</li>
</ol>

<p>
<strong>Tip:</strong> Learn more about creating PNG images with an alpha layer in the help system of your graphic editor.
</p>

</div>
<!-- EDIT4 SECTION "Transparent Unshaded Texture" [5633-8184] -->
<h2 class="sectionedit5" id="shininess_and_bumpiness">Shininess and Bumpiness</h2>
<div class="level2">

<p>
But textures are not all. Have a close look at the shiny sphere – you cannot get such a nice bumpy material with just a plain texture. You see that JME3 also supports so-called Phong-illuminated materials:
</p>

<p>
In a lit material, the standard texture layer is refered to as <em>DiffuseMap</em>, any material can use this layer. A lit material can additionally have lighting effects such as <em>Shininess</em> used together with the <em>SpecularMap</em> layer and <em>Specular</em> color. And you can even get a realistically bumpy or cracked surface with help of the <em>NormalMap</em> layer.
</p>

<p>
Let's have a look at the part of the code example where you create the shiny bumpy rock.
</p>
<ol>
<li class="level1"><div class="li"> Create a Geometry from a Sphere shape. Note that this shape is a normal smooth sphere mesh. <pre class="code java">    Sphere sphereMesh <span class="sy0">=</span> <span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">32</span>,<span class="nu0">32</span>, 2f<span class="br0">)</span><span class="sy0">;</span>
    Geometry sphereGeo <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Shiny rock"</span>, sphereMesh<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
<ol>
<li class="level2"><div class="li"> (Only for Spheres) Change the sphere's TextureMode to make the square texture project better onto the sphere.<pre class="code java">    sphereMesh.<span class="me1">setTextureMode</span><span class="br0">(</span>Sphere.<span class="me1">TextureMode</span>.<span class="me1">Projected</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level2"><div class="li"> You must generate TangentBinormals for the mesh so you can use the NormalMap layer of the texture.<pre class="code java">    TangentBinormalGenerator.<span class="me1">generate</span><span class="br0">(</span>sphereMesh<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Create a material based on the <code>Lighting.j3md</code> default material.<pre class="code java">    Material sphereMat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
        <span class="st0">"Common/MatDefs/Light/Lighting.j3md"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
<ol>
<li class="level2"><div class="li"> Set a standard rocky texture in the <code>DiffuseMap</code> layer. <br />
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/Pond/Pond.jpg"><img src="/resources/fetch.php" class="mediaright" title="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_pond_pond.jpg" alt="jmonkeyengine.googlecode.com_svn_trunk_engine_test-data_textures_terrain_pond_pond.jpg" width="64" height="64" /></a><pre class="code java">    sphereMat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"DiffuseMap"</span>, 
        assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/Pond/Pond.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level2"><div class="li"> Set the <code>NormalMap</code> layer that contains the bumpiness. The NormalMap was generated for this particular DiffuseMap with a special tool (e.g. Blender). <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Textures/Terrain/Pond/Pond_normal.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="64" height="64" /></a> <pre class="code java">    sphereMat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"NormalMap"</span>, 
        assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/Pond/Pond_normal.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level2"><div class="li"> Set the Material's Shininess to a value between 1 and 128. For a rock, a low fuzzy shininess is appropriate. Use material colors to define the shiny Specular color. <pre class="code java">    sphereMat.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"UseMaterialColors"</span>,<span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>    
    sphereMat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Diffuse"</span>,ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// minimum material color</span>
    sphereMat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Specular"</span>,ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// for shininess</span>
    sphereMat.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Shininess"</span>, 64f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// [1,128] for shininess</span></pre>
</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Assign your newly created material to the Geometry.<pre class="code java">    sphereGeo.<span class="me1">setMaterial</span><span class="br0">(</span>sphereMat<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Let's move and rotate the geometry a bit to position it better. <pre class="code java">    sphereGeo.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">2</span>,<span class="sy0">-</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Move it a bit</span>
    sphereGeo.<span class="me1">rotate</span><span class="br0">(</span>1.6f, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>          <span class="co1">// Rotate it a bit</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>sphereGeo<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
Remember that any Lighting.j3md-based material requires a light source, as shown in the full code sample above.
</p>

<p>
<strong>Tip:</strong> To deactivate Shininess, do not set <code>Shininess</code> to 0, but instead set the <code>Specular</code> color to <code>ColorRGBA.Black</code>.
</p>

</div>
<!-- EDIT5 SECTION "Shininess and Bumpiness" [8185-11426] -->
<h2 class="sectionedit6" id="default_material_definitions">Default Material Definitions</h2>
<div class="level2">

<p>
As you have seen, you can find the following default materials in <code>jme/core-data/Common/…</code>.
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Default Definition </th><th class="col1"> Usage </th><th class="col2 leftalign"> Parameters  </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> <code>Common/MatDefs/Misc/Unshaded.j3md</code> </td><td class="col1"> Colored: Use with mat.setColor() and ColorRGBA. <br />
Textured: Use with mat.setTexture() and Texture. </td><td class="col2"> Color : Color <br />
ColorMap : Texture2D </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> <code>Common/MatDefs/Light/Lighting.j3md</code>      </td><td class="col1"> Use with shiny Textures, Bump- and NormalMaps textures. <br />
Requires a light source. </td><td class="col2"> Ambient, Diffuse, Specular : Color <br />
DiffuseMap, NormalMap, SpecularMap : Texture2D <br />
Shininess : Float </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [11566-12036] -->
<p>
For a game, you create custom Materials based on these existing MaterialDefintions – as you have just seen in the example with the shiny rock's material.
</p>

</div>
<!-- EDIT6 SECTION "Default Material Definitions" [11427-12193] -->
<h2 class="sectionedit8" id="exercises">Exercises</h2>
<div class="level2">

</div>
<!-- EDIT8 SECTION "Exercises" [12194-12216] -->
<h3 class="sectionedit9" id="exercise_1custom_j3m_material">Exercise 1: Custom .j3m Material</h3>
<div class="level3">

<p>
Look at the shiny rocky sphere above again. It takes several lines to create and set the Material.
</p>
<ul>
<li class="level1"><div class="li"> Note how it loads the <code>Lighting.j3md</code> Material definition.</div>
</li>
<li class="level1"><div class="li"> Note how it sets the <code>DiffuseMap</code> and <code>NormalMap</code> to a texture path.</div>
</li>
<li class="level1"><div class="li"> Note how it activates <code>UseMaterialColors</code> and sets <code>Specular</code> and <code>Diffuse</code> to 4 float values (RGBA color).</div>
</li>
<li class="level1"><div class="li"> Note how it sets <code>Shininess</code> to 64.</div>
</li>
</ul>

<p>
If you want to use one custom material for several models, you can store it in a .j3m file, and save a few lines of code every time. 
</p>

<p>
You create a j3m file as follows:
</p>
<ol>
<li class="level1"><div class="li"> Create a plain text file <code>assets/Materials/MyCustomMaterial.j3m</code> in your project directory, with the following content:<pre class="code">Material My shiny custom material : Common/MatDefs/Light/Lighting.j3md {
     MaterialParameters {
        DiffuseMap : Textures/Terrain/Pond/Pond.jpg
        NormalMap : Textures/Terrain/Pond/Pond_normal.png
        UseMaterialColors : true
        Specular : 1.0 1.0 1.0 1.0
        Diffuse : 1.0 1.0 1.0 1.0
        Shininess : 64.0
     }
}</pre>
</div>
<ul>
<li class="level2"><div class="li"> Note that <code>Material</code> is a fixed keyword.</div>
</li>
<li class="level2"><div class="li"> Note that <code>My shiny custom material</code> is a String that you can choose to describe the material.</div>
</li>
<li class="level2"><div class="li"> Note how the code sets all the same properties as before! </div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In the code sample, comment out the eight lines that have <code>sphereMat</code> in them.</div>
</li>
<li class="level1"><div class="li"> Below this line, add the following line: <pre class="code java">sphereGeo.<span class="me1">setMaterial</span><span class="br0">(</span><span class="br0">(</span>Material<span class="br0">)</span> assetManager.<span class="me1">loadMaterial</span><span class="br0">(</span> 
    <span class="st0">"Materials/MyCustomMaterial.j3m"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Run the app. The result is the same.</div>
</li>
</ol>

<p>
Using this new custom material <code>MyCustomMaterial.j3m</code> only takes one line. You have replaced the eight lines of an on-the-fly material definition with one line that loads a custom material from a file. Using .j3m files is very handy if you use the same material often. 
</p>

</div>
<!-- EDIT9 SECTION "Exercise 1: Custom .j3m Material" [12217-14101] -->
<h3 class="sectionedit10" id="exercise_2bumpiness_and_shininess">Exercise 2: Bumpiness and Shininess</h3>
<div class="level3">

<p>
Go back to the bumpy rock sample above:
</p>
<ol>
<li class="level1"><div class="li"> Comment out the DiffuseMap line, and run the app. (Uncomment it again.)</div>
<ul>
<li class="level2"><div class="li"> Which property of the rock is lost?</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Comment out the NormalMap line, and run the app. (Uncomment it again.)</div>
<ul>
<li class="level2"><div class="li"> Which property of the rock is lost?</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Change the value of Shininess to values like 0, 63, 127.</div>
<ul>
<li class="level2"><div class="li"> What aspect of the Shininess changes?</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT10 SECTION "Exercise 2: Bumpiness and Shininess" [14102-14529] -->
<h2 class="sectionedit11" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned how to create a Material, specify its properties, and use it on a Geometry. You know how to load an image file (.png, .jpg) as texture into a material. You know to save texture files in a subfolder of your project's <code>assets/Textures/</code> directory.
</p>

<p>
You have also learned that a material can be stored in a .j3m file. The file references a built-in MaterialDefinition and specifies values for properties of that MaterialDefinition. You know to save your custom .j3m files in your project's <code>assets/Materials/</code> directory.
</p>

<p>
Now that you know how to load models and how to assign good-looking materials to them, let's have a look at how to animate models in the next chapter, <a href="/jme3/beginner/hello_animation.html" class="wikilink1" title="jme3:beginner:hello_animation">Hello Animation</a>.
</p>
<hr />

<p>
See also
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/how_to_use_materials.html" class="wikilink1" title="jme3:intermediate:how_to_use_materials">How to Use Materials</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/material_editing.html" class="wikilink1" title="sdk:material_editing">Material Editing</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.jmonkeyengine.com/forum/index.php?topic=14179.0" class="urlextern" title="http://www.jmonkeyengine.com/forum/index.php?topic=14179.0" rel="nofollow">Materials</a> forum thread</div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.googlecode.com/files/jME3_materials.pdf" class="urlextern" title="http://jmonkeyengine.googlecode.com/files/jME3_materials.pdf" rel="nofollow">jME3 Materials documentation</a> (PDF)</div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/watch?v=Feu3-mrpolc" class="urlextern" title="http://www.youtube.com/watch?v=Feu3-mrpolc" rel="nofollow">Video Tutorial: Editing and Assigning Materials to Models in jMonkeyEngine SDK (from 2010, is there a newer one?</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.blender.org/education-help/tutorials/materials/" class="urlextern" title="http://www.blender.org/education-help/tutorials/materials/" rel="nofollow">Creating textures in Blender</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.shaders.org/ifw2_textures/whatsin10.htm" class="urlextern" title="http://www.shaders.org/ifw2_textures/whatsin10.htm" rel="nofollow">Various Material screenshots</a> (Not done with JME3, this is just to show the fantastic range of Material parameters in the hands of an expert, until we have a JME3 demo for it.)</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/model.html" class="wikilink1" title="tag:model" rel="tag">model</a>,
	<a href="/tag/material.html" class="wikilink1" title="tag:material" rel="tag">material</a>,
	<a href="/tag/color.html" class="wikilink1" title="tag:color" rel="tag">color</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>,
	<a href="/tag/transparency.html" class="wikilink1" title="tag:transparency" rel="tag">transparency</a>
</span></div>

</div>
<!-- EDIT11 SECTION "Conclusion" [14530-] -->
