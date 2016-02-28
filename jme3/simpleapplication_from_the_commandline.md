---
title: Starting a JME3 application from the Commandline
---
<h1 class="sectionedit1" id="starting_a_jme3_application_from_the_commandline">Starting a JME3 application from the Commandline</h1>
<div class="level1">

<p>
Although we recommend the jMonkeyEngine <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> for developing JME3 games, you can use any IDE (integrated development environment) such as <a href="/jme3/setting_up_netbeans_and_jme3.html" class="wikilink1" title="jme3:setting_up_netbeans_and_jme3">NetBeans</a> or <a href="/jme3/setting_up_jme3_in_eclipse.html" class="wikilink1" title="jme3:setting_up_jme3_in_eclipse">Eclipse</a>, and even work freely from the commandline. Here is a generic IDE-independent “getting started” tutorial. 
</p>

<p>
This example shows how to set up and run a simple application (HelloJME3) that depends on the jMonkeyEngine3 libraries. 
</p>

<p>
The directory structure will look as follows:
</p>
<pre class="code">jme3/
jme3/lib
jme3/src
...
HelloJME3/
HelloJME3/lib
HelloJME3/assets
HelloJME3/src
...</pre>

</div>
<!-- EDIT1 SECTION "Starting a JME3 application from the Commandline" [1-678] -->
<h2 class="sectionedit2" id="installing_the_jme3_framework">Installing the JME3 Framework</h2>
<div class="level2">

<p>
To install the development version of jme3, <a href="http://updates.jmonkeyengine.org/stable/3.0/engine" class="urlextern" title="http://updates.jmonkeyengine.org/stable/3.0/engine" rel="nofollow">download the nightly build</a>, unzip the folder into a directory named <code>jme3</code>. The filenames here are just an example, but they will always be something like <code>jME3_xx-xx-2011</code>. 
</p>
<pre class="code">mkdir jme3
cd jme3
unzip jME3_01-18-2011.zip</pre>

<p>
Alternatively, you can build JME3 from the sources. (Recommended for JME3 developers.)
</p>
<pre class="code">svn checkout https://jmonkeyengine.googlecode.com/svn/branches/3.0final/engine jme3
cd jme3
ant run
cd ..</pre>

<p>
If you see a Test Chooser application open now, the build was successful. <strong>Tip:</strong> Use just <code>ant</code> instead of <code>ant run</code> to build the libraries without running the demos.
</p>

</div>
<!-- EDIT2 SECTION "Installing the JME3 Framework" [679-1445] -->
<h2 class="sectionedit3" id="sample_project_directory_structure">Sample Project Directory Structure</h2>
<div class="level2">

<p>
First we set up the directory and source package structure for your game project. Note that the game project directory <code>HelloJME3</code> is on the same level as your <code>jme3</code> checkout. In this example, we create a Java package that we call <code>hello</code> in the source directory.
</p>
<pre class="code">mkdir HelloJME3
mkdir HelloJME3/src
mkdir HelloJME3/src/hello</pre>

</div>
<!-- EDIT3 SECTION "Sample Project Directory Structure" [1446-1843] -->
<h2 class="sectionedit4" id="libraries">Libraries</h2>
<div class="level2">

<p>
Next you copy the necessary JAR libraries from the download to your project. You only have to do this set of steps once every time you download a new JME3 build. For a detailed description of the separate jar files see <a href="/jme3/jme3_source_structure.html" class="wikilink1" title="jme3:jme3_source_structure">this list</a>.
</p>
<pre class="code">mkdir HelloJME3/build 
mkdir HelloJME3/lib
cp jme3/lib/*.* HelloJME3/lib</pre>

<p>
If you have built JME3 from the sources, then the copy paths are different:
</p>
<pre class="code">mkdir HelloJME3/build 
mkdir HelloJME3/lib
cp jme3/dist/*.* HelloJME3/lib</pre>

</div>
<!-- EDIT4 SECTION "Libraries" [1844-2418] -->
<h3 class="sectionedit5" id="sample_code">Sample Code</h3>
<div class="level3">

<p>
To test your setup, create the file <code>HelloJME3/src/hello/HelloJME3.java</code> with any text editor, paste the following sample code, and save.
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">hello</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> HelloJME3 <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "Sample Code" [2419-3352] -->
<h2 class="sectionedit6" id="build_and_run">Build and Run</h2>
<div class="level2">

<p>
We build the sample application into the build directory…
</p>
<pre class="code">cd HelloJME3
javac -d build -cp "lib/eventbus-1.4.jar:lib/j-ogg-oggd.jar:lib/j-ogg-vorbisd.jar:lib/jME3-lwjgl-natives.jar:lib/jbullet.jar:lib/jinput.jar:lib/lwjgl.jar:lib/stack-alloc.jar:lib/vecmath.jar:lib/xmlpull-xpp3-1.1.4c.jar:lib/jME3-blender.jar:lib/jME3-core.jar:lib/jME3-desktop.jar:lib/jME3-jogg.jar:lib/jME3-plugins.jar:lib/jME3-terrain.jar:lib/jME3-testdata.jar:lib/jME3-niftygui.jar:lib/nifty-default-controls.jar:lib/nifty-examples.jar:lib/nifty-style-black.jar:lib/nifty.jar:." src/hello/HelloJME3.java </pre>

<p>
… and run it.
</p>
<pre class="code">cd build
java -cp "../lib/eventbus-1.4.jar:../lib/j-ogg-oggd.jar:../lib/j-ogg-vorbisd.jar:../lib/jME3-lwjgl-natives.jar:../lib/jbullet.jar:../lib/jinput.jar:../lib/lwjgl.jar:../lib/stack-alloc.jar:../lib/vecmath.jar:../lib/xmlpull-xpp3-1.1.4c.jar:../lib/jME3-blender.jar:../lib/jME3-core.jar:../lib/jME3-desktop.jar:../lib/jME3-jogg.jar:../lib/jME3-plugins.jar:../lib/jME3-terrain.jar:../lib/jME3-testdata.jar:../lib/jME3-niftygui.jar:../lib/nifty-default-controls.jar:../lib/nifty-examples.jar:../lib/nifty-style-black.jar:../lib/nifty.jar:." hello/HelloJME3</pre>

<p>
Note: If you use Windows, the classpath separator is “;” instead of “:”.
</p>

<p>
If a settings dialog pops up, confirm the default settings. You should now see a simple window with a 3-D cube. Use the mouse and the WASD keys to move. It works! 
</p>

</div>
<!-- EDIT6 SECTION "Build and Run" [3353-4805] -->
<h2 class="sectionedit7" id="recommended_asset_directory_structure">Recommended Asset Directory Structure</h2>
<div class="level2">

<p>
For <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">multi-media files, models, and other assets</a>, we recommend creating the following project structure:
</p>
<pre class="code">cd HelloJME3
mkdir assets
mkdir assets/Interface
mkdir assets/Materials
mkdir assets/MatDefs
mkdir assets/Models
mkdir assets/Scenes
mkdir assets/Shaders
mkdir assets/Sounds
mkdir assets/Textures</pre>

<p>
This directory structure will allow <a href="/jme3/intermediate/simpleapplication.html" class="wikilink1" title="jme3:intermediate:simpleapplication">SimpleApplication</a>'s default <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">AssetManager</a> to load media files from your <code>assets</code> directory, like in this example:
</p>
<pre class="code">import com.jme3.scene.Spatial;
...
  Spatial elephant = assetManager.loadModel("Models/Elephant/Elephant.meshxml");
  rootNode.attachChild(elephant);
...</pre>

<p>
You will learn more about the asset manager and how to customize it later. For now feel free to structure your assets (images, textures, models) into further sub-directories, like in this example the <code>assets/models/Elephant</code> directory that contains the <code>elephant.meshxml</code> model and its materials.
</p>

</div>
<!-- EDIT7 SECTION "Recommended Asset Directory Structure" [4806-5922] -->
<h2 class="sectionedit8" id="next_steps">Next Steps</h2>
<div class="level2">

<p>
Now follow the <a href="/jme3.html" class="wikilink1" title="jme3">tutorials</a> and write your first jMonkeyEngine game.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Next Steps" [5923-] -->
