---
title: jMonkeyEngine 3 Tutorial (3) - Hello Assets
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_3_-_hello_assets">jMonkeyEngine 3 Tutorial (3) - Hello Assets</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a>,
Next: <a href="/jme3/beginner/hello_main_event_loop.html" class="wikilink1" title="jme3:beginner:hello_main_event_loop">Hello Update Loop</a>
</p>

<p>
In this tutorial we will learn to load 3D models and text into the scene graph, using the jME <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>. You will also learn how to determine the correct paths, and which file formats to use.
</p>

<p>
<a href="/resources/jme3-beginner-beginner-assets-models.png" class="media" title="jme3:beginner:beginner-assets-models.png"><img src="/resources/jme3-beginner-beginner-assets-models.png" class="mediacenter" alt="" width="320" height="250" /></a>
</p>

<p>
</p><p></p><div class="notetip"><a href="/sdk/sample_code.html" class="wikilink1" title="sdk:sample_code">Trouble finding the files to run this sample?</a> To get the assets (3D models) used in this example, add the included <code>jME3-testdata.jar</code> to your classpath. In project created with the jMonkeyEngine SDK (recommended), simply right-click your project, choose “Properties”, go to “Libraries”, press “Add Library” and add the preconfigured “jme3-test-data” library. 
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (3) - Hello Assets" [1-837] -->
<h2 class="sectionedit2" id="code_sample">Code Sample</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapText</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 3 - how to load an OBJ model, and OgreXML model, 
 * a material/texture, or text. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloAssets <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        HelloAssets app <span class="sy0">=</span> <span class="kw1">new</span> HelloAssets<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        Spatial teapot <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Teapot/Teapot.obj"</span><span class="br0">)</span><span class="sy0">;</span>
        Material mat_default <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span> 
            assetManager, <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        teapot.<span class="me1">setMaterial</span><span class="br0">(</span>mat_default<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>teapot<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Create a wall with a simple texture from test_data</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>2.5f,2.5f,1.0f<span class="br0">)</span><span class="sy0">;</span>
        Spatial wall <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box <span class="br0">)</span><span class="sy0">;</span>
        Material mat_brick <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span> 
            assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat_brick.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, 
            assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/BrickWall/BrickWall.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        wall.<span class="me1">setMaterial</span><span class="br0">(</span>mat_brick<span class="br0">)</span><span class="sy0">;</span>
        wall.<span class="me1">setLocalTranslation</span><span class="br0">(</span>2.0f,<span class="sy0">-</span>2.5f,0.0f<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>wall<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Display a line of text with a default font</span>
        guiNode.<span class="me1">detachAllChildren</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
        BitmapText helloText <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
        helloText.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        helloText.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Hello World"</span><span class="br0">)</span><span class="sy0">;</span>
        helloText.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">300</span>, helloText.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        guiNode.<span class="me1">attachChild</span><span class="br0">(</span>helloText<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Load a model from test_data (OgreXML + material + texture)</span>
        Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
        ninja.<span class="me1">scale</span><span class="br0">(</span>0.05f, 0.05f, 0.05f<span class="br0">)</span><span class="sy0">;</span>
        ninja.<span class="me1">rotate</span><span class="br0">(</span>0.0f, <span class="sy0">-</span>3.0f, 0.0f<span class="br0">)</span><span class="sy0">;</span>
        ninja.<span class="me1">setLocalTranslation</span><span class="br0">(</span>0.0f, <span class="sy0">-</span>5.0f, <span class="sy0">-</span>2.0f<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>ninja<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// You must add a light to make the model visible</span>
        DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f, <span class="sy0">-</span>0.7f, <span class="sy0">-</span>1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Build and run the code sample. You should see a green Ninja with a colorful teapot standing behind a wall. The text on the screen should say “Hello World”.
</p>

</div>
<!-- EDIT2 SECTION "Code Sample" [838-3433] -->
<h2 class="sectionedit3" id="the_asset_manager">The Asset Manager</h2>
<div class="level2">

<p>
<strong>By game assets we mean all multi-media files, such as models, materials, textures, whole scenes, custom shaders, music and sound files, and custom fonts.</strong> JME3 comes with a handy AssetManager object that helps you access your assets. 
The AssetManager can load files from:
</p>
<ul>
<li class="level1"><div class="li"> the current classpath (the top level of your project directory), </div>
</li>
<li class="level1"><div class="li"> the <code>assets</code> directory of your project, and</div>
</li>
<li class="level1"><div class="li"> optionally, custom paths that you register.</div>
</li>
</ul>

<p>
The following is the recommended directory structure for storing assets in your project directoy: 
</p>
<pre class="code">MyGame/assets/               
MyGame/assets/Interface/
MyGame/assets/MatDefs/
MyGame/assets/Materials/
MyGame/assets/Models/       &lt;-- your .j3o models go here
MyGame/assets/Scenes/
MyGame/assets/Shaders/
MyGame/assets/Sounds/       &lt;-- your audio files go here
MyGame/assets/Textures/     &lt;-- your textures go here
MyGame/build.xml            &lt;-- Default Ant build script
MyGame/src/...              &lt;-- your Java sources go here
MyGame/...</pre>

<p>
This is just a suggested best practice, and it's what you get by default when creating a new Java project in the jMokeyEngine <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a>. You can create an <code>assets</code> directory and technically name the subdirectories whatever you like.
</p>

</div>
<!-- EDIT3 SECTION "The Asset Manager" [3434-4701] -->
<h3 class="sectionedit4" id="loading_textures">Loading Textures</h3>
<div class="level3">

<p>
Place your textures in a subdirectory of <code>assets/Textures/</code>. Load the texture into the material before you set the Material. The following code sample is from the <code>simpleInitApp()</code> method and loads a simple wall model:
</p>
<pre class="code java"><span class="co1">// Create a wall with a simple texture from test_data</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>2.5f,2.5f,1.0f<span class="br0">)</span><span class="sy0">;</span>
Spatial wall <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box <span class="br0">)</span><span class="sy0">;</span>
Material mat_brick <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span> 
    assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
mat_brick.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, 
    assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/BrickWall/BrickWall.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
wall.<span class="me1">setMaterial</span><span class="br0">(</span>mat_brick<span class="br0">)</span><span class="sy0">;</span>
wall.<span class="me1">setLocalTranslation</span><span class="br0">(</span>2.0f,<span class="sy0">-</span>2.5f,0.0f<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>wall<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
In this case, you <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">create your own Material</a> and apply it to a Geometry. You base Materials on default material descriptions (such as “Unshaded.j3md”), as shown in this example. 
</p>

</div>
<!-- EDIT4 SECTION "Loading Textures" [4702-5603] -->
<h3 class="sectionedit5" id="loading_text_and_fonts">Loading Text and Fonts</h3>
<div class="level3">

<p>
This example displays the text “Hello World” in the default font at the bottom edge of the window. You attach text to the <code>guiNode</code> – this is a special node for flat (orthogonal) display elements. You display text to show the game score, player health, etc.
The following code sample goes into the <code>simpleInitApp()</code> method.
</p>
<pre class="code java"><span class="co1">// Display a line of text with a default font</span>
guiNode.<span class="me1">detachAllChildren</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
BitmapText helloText <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
helloText.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
helloText.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Hello World"</span><span class="br0">)</span><span class="sy0">;</span>
helloText.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">300</span>, helloText.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">attachChild</span><span class="br0">(</span>helloText<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Tip:</strong> Clear existing text in the guiNode by detaching all its children.
</p>

</div>
<!-- EDIT5 SECTION "Loading Text and Fonts" [5604-6449] -->
<h3 class="sectionedit6" id="loading_a_model">Loading a Model</h3>
<div class="level3">

<p>
Export your 3D model in OgreXML format (.mesh.xml, .scene, .material, .skeleton.xml) and place it in a subdirectory of <code>assets/Models/</code>. The following code sample goes into the <code>simpleInitApp()</code> method.
</p>
<pre class="code java"><span class="co1">// Load a model from test_data (OgreXML + material + texture)</span>
Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
ninja.<span class="me1">scale</span><span class="br0">(</span>0.05f, 0.05f, 0.05f<span class="br0">)</span><span class="sy0">;</span>
ninja.<span class="me1">rotate</span><span class="br0">(</span>0.0f, <span class="sy0">-</span>3.0f, 0.0f<span class="br0">)</span><span class="sy0">;</span>
ninja.<span class="me1">setLocalTranslation</span><span class="br0">(</span>0.0f, <span class="sy0">-</span>5.0f, <span class="sy0">-</span>2.0f<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>ninja<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// You must add a directional light to make the model visible!</span>
DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f, <span class="sy0">-</span>0.7f, <span class="sy0">-</span>1.0f<span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Note that you do not need to create a Material if you exported the model with a material. Remember to add a light source, as shown, otherwise the material (and the whole model) is not visible!
</p>

</div>
<!-- EDIT6 SECTION "Loading a Model" [6450-7379] -->
<h3 class="sectionedit7" id="loading_assets_from_custom_paths">Loading Assets From Custom Paths</h3>
<div class="level3">

<p>
What if your game relies on user supplied model files, that are not included in the distribution? If a file is not located in the default location (e.g. assets directory), you can register a custom Locator and load it from any path. 
</p>

<p>
Here is a usage example of a ZipLocator that is registered to a file <code>town.zip</code> in the top level of your project directory:
</p>
<pre class="code java">    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Here is a HttpZipLocator that can download zipped models and load them:
</p>
<pre class="code java">    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span>
      <span class="st0">"http://jmonkeyengine.googlecode.com/files/wildhouse.zip"</span>, 
      HttpZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
JME3 offers ClasspathLocator, ZipLocator, FileLocator, HttpZipLocator, and UrlLocator (see <code>com.jme3.asset.plugins</code>). 
</p>

</div>
<!-- EDIT7 SECTION "Loading Assets From Custom Paths" [7380-8397] -->
<h2 class="sectionedit8" id="creating_models_and_scenes">Creating Models and Scenes</h2>
<div class="level2">

<p>
To create 3D models and scenes, you need a 3D Mesh Editor. If you don't have any tools, install Blender and the OgreXML Exporter plugin. 
Then you <a href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/UV_Map_Basics" class="urlextern" title="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/UV_Map_Basics" rel="nofollow">create fully textured models (e.g. with Blender)</a> and export them to your project.
Then you use the <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> to <a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer">load models</a>, <a href="/sdk/blender.html" class="wikilink1" title="sdk:blender">convert models</a>, and <a href="/sdk/scene_composer.html" class="wikilink1" title="sdk:scene_composer">create 3D scenes</a> from them. 
</p>

<p>
<strong>Example:</strong> From Blender, you export your models as Ogre XML meshes with materials as follows:
</p>
<ol>
<li class="level1"><div class="li"> Open the menu File &gt; Export &gt; OgreXML Exporter to open the exporter dialog.</div>
</li>
<li class="level1"><div class="li"> In the Export Materials field: Give the material the same name as the model. For example, the model <code>something.mesh.xml</code> goes with <code>something.material</code>, plus (optionally) <code>something.skeleton.xml</code> and some JPG texture files.</div>
</li>
<li class="level1"><div class="li"> In the Export Meshes field: Select a subdirectory of your <code>assets/Models/</code> directory. E.g. <code>assets/Models/something/</code>.</div>
</li>
<li class="level1"><div class="li"> Activate the following exporter settings: </div>
<ul>
<li class="level2"><div class="li"> Copy Textures: YES</div>
</li>
<li class="level2"><div class="li"> Rendering Materials: YES</div>
</li>
<li class="level2"><div class="li"> Flip Axis: YES</div>
</li>
<li class="level2"><div class="li"> Require Materials: YES</div>
</li>
<li class="level2"><div class="li"> Skeleton name follows mesh: YES</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Click export.</div>
</li>
</ol>

</div>
<!-- EDIT8 SECTION "Creating Models and Scenes" [8398-9651] -->
<h3 class="sectionedit9" id="model_file_formats">Model File Formats</h3>
<div class="level3">

<p>
JME3 can convert and load
</p>
<ul>
<li class="level1"><div class="li"> Ogre XML models + materials, </div>
</li>
<li class="level1"><div class="li"> Ogre DotScenes, </div>
</li>
<li class="level1"><div class="li"> Wavefront OBJ + MTL models, </div>
</li>
<li class="level1"><div class="li"> .Blend files.</div>
</li>
</ul>

<p>
The <code>loadModel()</code> method loads these original file formats when you run your code directly from the SDK. If you however build the executables using the default build script, then the original model files (XML, OBJ, etc) <em>are not included</em>. This means, when you run the executable outside the SDK, and load any original models directly, you get the following error message: 
</p>
<pre class="code">com.jme3.asset.DesktopAssetManager loadAsset
WARNING: Cannot locate resource: Models/Ninja/Ninja.mesh.xml
com.jme3.app.Application handleError
SEVERE: Uncaught exception thrown in Thread[LWJGL Renderer Thread,5,main]
java.lang.NullPointerException</pre>

<p>
You see that loading the <strong>XML/OBJ/Blend files</strong> directly is only acceptable during the development phase in the SDK. For example, every time your graphic designer pushes updated files to the asset directory, you can quickly review the latest version in your development environment.
</p>

<p>
But for QA test builds and for the final release build, you use <strong>.j3o files</strong> exclusively. J3o is an optimized binary format for jME3 applications. When you do QA test builds, or are ready to release, use the <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> to <a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer">convert</a> all .obj/.scene/.xml/.blend files to .j3o files, and update all code to load the .j3o files. The default build script automatically packages .j3o files in the executables.
</p>

<p>
Open your JME3 Project in the jMonkeyEngine SDK.
</p>
<ol>
<li class="level1"><div class="li"> Right-click a .Blend, .OBJ, or .mesh.xml file in the Projects window, and choose “convert to JME3 binary”. </div>
</li>
<li class="level1"><div class="li"> The .j3o file appears next to the .mesh.xml file and has the same name. </div>
</li>
<li class="level1"><div class="li"> Update all your <code>loadModel()</code> lines accordingly. For example: <pre class="code java">Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.j3o"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
</p><p></p><div class="notetip">If your executable throws a “Cannot locate resource” runtime exception, check all load paths and make sure you have converted all models to .j3o files!
</div>


</div>
<!-- EDIT9 SECTION "Model File Formats" [9652-11736] -->
<h3 class="sectionedit10" id="loading_models_and_scenes">Loading Models and Scenes</h3>
<div class="level3">
<div class="table sectionedit11"><table class="inline">
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
		<td class="col0"> Load a model without materials </td><td class="col1"> If you have a model without materials, you have to give it a material to make it visible. <pre class="code java">Spatial teapot <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Teapot/Teapot.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// default material</span>
teapot.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>teapot<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row3">
		<td class="col0"> Load a scene </td><td class="col1"> You load scenes just like you load models: <pre class="code java">Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/town/main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/town/main.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [11774-12828] -->
</div>
<!-- EDIT10 SECTION "Loading Models and Scenes" [11737-12829] -->
<h2 class="sectionedit12" id="excercise_-_how_to_load_assets">Excercise - How to Load Assets</h2>
<div class="level2">

<p>
As an exercise, let's try different ways of loading a scene. You will learn how to load the scene directly, or from a zip file.
</p>
<ol>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" rel="nofollow">Download the town.zip</a> sample scene. </div>
</li>
<li class="level1"><div class="li"> (Optional:) Unzip the town.zip to see the structure of the contained Ogre dotScene: You'll get a directory named <code>town</code>. It contains XML and texture files, and file called main.scene. (This is just for your information, you do not need to do anything with it.)</div>
</li>
<li class="level1"><div class="li"> Place the town.zip file in the top level directory of your JME3 project, like so: <pre class="code">jMonkeyProjects/MyGameProject/assets/
jMonkeyProjects/MyGameProject/build.xml
jMonkeyProjects/MyGameProject/src/
jMonkeyProjects/MyGameProject/town.zip
...</pre>
</div>
</li>
</ol>

<p>
Use the following method to load models from a zip file:
</p>
<ol>
<li class="level1"><div class="li"> Verify <code>town.zip</code> is in the project directory.</div>
</li>
<li class="level1"><div class="li"> Register a zip file locator to the project directory: Add the following code under <code>simpleInitApp() {</code><pre class="code java">    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    Spatial gameLevel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>5.2f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>gameLevel<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The loadModel() method now searches this zip directly for the files to load. <br />
(This means, do not write <code>loadModel(town.zip/main.scene)</code> or similar!)
</p>
</div>
</li>
<li class="level1"><div class="li"> Clean, build and run the project. <br />
You should now see the Ninja+wall+teapot standing in a town. </div>
</li>
</ol>

<p>
<strong>Tip:</strong> If you register new locators, make sure you do not get any file name conflicts: Don't name all scenes <code>main.scene</code> but give each scene a unique name.
</p>

<p>
Earlier in this tutorial, you loaded scenes and models from the asset directory. This is the most common way you will be loading scenes and models. Here is the typical procedure:
</p>
<ol>
<li class="level1"><div class="li"> Remove the code that you added for the previous exercise.</div>
</li>
<li class="level1"><div class="li"> Move the unzipped <code>town/</code> directory into the <code>assets/Scenes/</code> directory of your project.</div>
</li>
<li class="level1"><div class="li"> Add the following code under <code>simpleInitApp() {</code> <pre class="code java">    Spatial gameLevel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/town/main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>5.2f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>gameLevel<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Note that the path is relative to the <code>assets/…</code> directory.
</p>
</div>
</li>
<li class="level1"><div class="li"> Clean, build and run the project. Again, you should see the Ninja+wall+teapot standing in a town. </div>
</li>
</ol>

<p>
Here is a third method you must know, loading a scene/model from a .j3o file:
</p>
<ol>
<li class="level1"><div class="li"> Remove the code from the previous exercise.</div>
</li>
<li class="level1"><div class="li"> If you haven't already, open the <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> and open the project that contains the HelloAsset class.</div>
</li>
<li class="level1"><div class="li"> In the projects window, browse to the <code>assets/Scenes/town</code> directory. </div>
</li>
<li class="level1"><div class="li"> Right-click the <code>main.scene</code> and convert the scene to binary: The jMonkeyPlatform generates a main.j3o file.</div>
</li>
<li class="level1"><div class="li"> Add the following code under <code>simpleInitApp() {</code><pre class="code java">    Spatial gameLevel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/town/main.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>5.2f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>gameLevel<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Again, note that the path is relative to the <code>assets/…</code> directory.
</p>
</div>
</li>
<li class="level1"><div class="li"> Clean, Build and run the project. <br />
Again, you should see the Ninja+wall+teapot standing in a town. </div>
</li>
</ol>

</div>
<!-- EDIT12 SECTION "Excercise - How to Load Assets" [12830-16165] -->
<h2 class="sectionedit13" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
Now you know how to populate the scenegraph with static shapes and models, and how to build scenes. You have learned how to load assets using the <code>assetManager</code> and you have seen that the paths start relative to your project directory. Another important thing you have learned is to convert models to .j3o format for the executable JARs etc.
</p>

<p>
Let's add some action to the scene and continue with the <a href="/jme3/beginner/hello_main_event_loop.html" class="wikilink1" title="jme3:beginner:hello_main_event_loop">Update Loop</a>!
</p>
<hr />

<p>
<strong>See also:</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">The definitive Blender import tutorial</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">Asset pipeline introduction</a></div>
</li>
<li class="level1"><div class="li"> If you want to learn how to load sounds, see <a href="/jme3/beginner/hello_audio.html" class="wikilink1" title="jme3:beginner:hello_audio">Hello Audio</a></div>
</li>
<li class="level1"><div class="li"> If you want to learn more about loading textures and materials, see <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/lightnode.html" class="wikilink1" title="tag:lightnode" rel="tag">lightnode</a>,
	<a href="/tag/material.html" class="wikilink1" title="tag:material" rel="tag">material</a>,
	<a href="/tag/model.html" class="wikilink1" title="tag:model" rel="tag">model</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>
</span></div>

</div>
<!-- EDIT13 SECTION "Conclusion" [16166-] -->
