---
title: Frequently Asked Questions
---
<h1 class="sectionedit1" id="frequently_asked_questions">Frequently Asked Questions</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Frequently Asked Questions" [1-41] -->
<h2 class="sectionedit2" id="i_want_to_create_and_configure_a_jme3_application">I want to create and configure a jME3 Application</h2>
<div class="level2">

</div>
<!-- EDIT2 SECTION "I want to create and configure a jME3 Application" [42-103] -->
<h3 class="sectionedit3" id="how_do_i_start_writing_a_preconfigured_jme_game">How do I start writing a preconfigured jME game?</h3>
<div class="level3">

<p>
Write a Java class that extends <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/app/SimpleApplication.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/app/SimpleApplication.java" rel="nofollow">com.jme3.app.SimpleApplication</a>.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_simpleapplication.html" class="wikilink1" title="jme3:beginner:hello_simpleapplication">Hello SimpleApplication</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/app/TestAppStateLifeCycle.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/app/TestAppStateLifeCycle.java" rel="nofollow">TestAppStateLifeCycle</a>.
</p>

</div>
<!-- EDIT3 SECTION "How do I start writing a preconfigured jME game?" [104-566] -->
<h3 class="sectionedit4" id="how_do_i_change_the_background_color">How do I change the background color?</h3>
<div class="level3">
<pre class="code java">viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "How do I change the background color?" [567-677] -->
<h3 class="sectionedit5" id="can_i_customize_the_simpleapplication_class">Can I customize the SimpleApplication class?</h3>
<div class="level3">

<p>
Yes! Actually, you MUST customize it! For your own games, you always create a custom base class that extends <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/app/SimpleApplication.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/app/SimpleApplication.java" rel="nofollow">com.jme3.app.SimpleApplication</a> class. From now on it's no longer a “simple application” – it's now your game. Configure your <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">application settings</a>, implement methods, and customize away!
<br />
<strong>Learn more:</strong> <a href="/jme3/intermediate/simpleapplication.html" class="wikilink1" title="jme3:intermediate:simpleapplication">SimpleApplication</a>, <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">AppSettings</a>.
</p>

</div>
<!-- EDIT5 SECTION "Can I customize the SimpleApplication class?" [678-1274] -->
<h3 class="sectionedit6" id="how_can_i_switch_between_screens_or_states">How can I switch between screens or states?</h3>
<div class="level3">

<p>
You should break down your application logic into components by spreading it out over individual AppStates. AppStates can be attached to and detached from the game. AppStates have access to all objects (rootNode, PhysicsSpace, inputManager, etc) and methods in your main application. So each AppState can bring its own subset of input handlers, <abbr title="Graphical User Interface">GUI</abbr> nodes, spatial nodes, and even its own subset of game mechanics in the update() loop.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a>.
</p>

</div>
<!-- EDIT6 SECTION "How can I switch between screens or states?" [1275-1820] -->
<h3 class="sectionedit7" id="how_do_i_pause_unpause_a_game">How do I pause/unpause a game?</h3>
<div class="level3">

<p>
You split up your application into several AppStates and implement the setEnabled() methods for each state. Then you create, for example, a GameRunningAppState and a GamePausedAppState. GamePausedAppState's job is to attach all your AppStates that contain the logic and <abbr title="Graphical User Interface">GUI</abbr> of the pause screen, and to detach all the AppStates that contain logic and <abbr title="Graphical User Interface">GUI</abbr> of the running game. GameRunningAppState does the opposite. By attaching one or the other to the game, you switch between the paused and unpaused states.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a>.
</p>

</div>
<!-- EDIT7 SECTION "How do I pause/unpause a game?" [1821-2426] -->
<h3 class="sectionedit8" id="how_do_i_disable_logger_output_to_the_console">How do I disable logger output to the console?</h3>
<div class="level3">

<p>
During development, you can switch the severity level of the default logger to no longer print FINE warnings, but only WARNINGs.
</p>
<pre class="code java">java.<span class="me1">util</span>.<span class="me1">logging</span>.<span class="me1">Logger</span>.<span class="me1">getLogger</span><span class="br0">(</span><span class="st0">""</span><span class="br0">)</span>.<span class="me1">setLevel</span><span class="br0">(</span>Level.<span class="me1">WARNING</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For the release, switch the severity level of the default logger to print only SEVERE errors.
</p>
<pre class="code java">java.<span class="me1">util</span>.<span class="me1">logging</span>.<span class="me1">Logger</span>.<span class="me1">getLogger</span><span class="br0">(</span><span class="st0">""</span><span class="br0">)</span>.<span class="me1">setLevel</span><span class="br0">(</span>Level.<span class="me1">SEVERE</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Learn more:</strong>  <a href="/jme3/advanced/logging.html" class="wikilink1" title="jme3:advanced:logging">Logging</a>.
</p>

</div>
<!-- EDIT8 SECTION "How do I disable logger output to the console?" [2427-2913] -->
<h3 class="sectionedit9" id="why_does_the_executable_crash_with_cannot_locate_resource">Why does the executable crash with "Cannot locate resource"?</h3>
<div class="level3">

<p>
Make sure to only load() models converted to .j3o binary format, not the original Ogre or Wavefront formats. If you load assets from zip files, make sure to ammend the build script to copy them to the build directory.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>
</p>

</div>
<!-- EDIT9 SECTION "Why does the executable crash with Cannot locate resource?" [2914-3253] -->
<h3 class="sectionedit10" id="what_is_javalanglinkageerrorversion_mismatch">What is java.lang.LinkageError: Version mismatch?</h3>
<div class="level3">

<p>
This rare exception shows a message similar to the following: <code>Exception in thread “LWJGL Renderer Thread” java.lang.LinkageError: Version mismatch: jar version is (number), native library version is (another number)</code>. jME3 needs native libraries (.dll, .jnilib, lib*.so files) to run LWJGL and jBullet. The correct versions of these libraries are included when you install the SDK or download the binaries. However there are circumstances where jME3 cannot determine which copy of the native library it should use: <br />
If you install another application that needs a different version of a native library, and this app globally installs its version over jME3's; or if an old copy of a native library is in your project directory, your home directory, or Java library path, or in the classpath; or if you permanently linked an old copy in your IDE's settings; then Java assumes you prefer these native libraries over the bundled ones, and your jME3 application ends up running with the wrong version. <br />
To fix this, search for .dll (Windows), .jnilib (Mac), and .so (Linux) files for jBullet and LWJGL on your harddrive and in your path and IDE settings, and verify they don't interfere. (If you have other jME  versions installed and linked somehow, the outdated natives may also be in a lwjgl.jar or jbullet.jar file!) 
</p>

</div>
<!-- EDIT10 SECTION "What is java.lang.LinkageError: Version mismatch?" [3254-4637] -->
<h2 class="sectionedit11" id="i_want_to_load_my_scene">I want to load my scene</h2>
<div class="level2">

</div>
<!-- EDIT11 SECTION "I want to load my scene" [4638-4673] -->
<h3 class="sectionedit12" id="how_do_i_make_objects_appear_disappear_in_the_3d_scene">How do I make objects appear / disappear in the 3D scene?</h3>
<div class="level3">

<p>
To make a spatial appear in the scene, you attach it to the rootNode (or to a node that is attached to the rootnode). To remove a spatial, you detach it from its parent node.
</p>
<pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>spatial<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// appear in scene</span></pre>
<pre class="code java">rootNode.<span class="me1">detachChild</span><span class="br0">(</span>spatial<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// remove from scene</span></pre>

<p>
<strong>Learn more:</strong> <a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph">The Scene Graph</a>, <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a>, <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">Hello Asset</a>, <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/Node.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/Node.java" rel="nofollow">com.jme3.scene.Node</a> and <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/Geometry.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/Geometry.java" rel="nofollow">com.jme3.scene.Geometry</a>.
</p>

</div>
<!-- EDIT12 SECTION "How do I make objects appear / disappear in the 3D scene?" [4674-5466] -->
<h3 class="sectionedit13" id="why_do_i_get_assetnotfoundexception_when_loading_x">Why do I get AssetNotFoundException when loading X ?</h3>
<div class="level3">

<p>
First check whether the file path of the asset is correct. By default it is relative to your project's assets directory:
</p>
<pre class="code java"><span class="co1">// To load .../jMonkeyProjects/MyGame/assets/Models/Ninja/Ninja.j3o</span>
Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.j3o"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
If you are not using the default <code>assets</code> directory, verify that you have registered a locator to the AssetManager. <a href="http://jmonkeyengine.org/javadoc/com/jme3/asset/plugins/package-summary.html" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/asset/plugins/package-summary.html" rel="nofollow">Different Locator types</a> are available.
</p>
<pre class="code java"><span class="kw1">this</span>.<span class="me1">assetManager</span>.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"assets/"</span>, FileLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// default</span>
<span class="kw1">this</span>.<span class="me1">assetManager</span>.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"c:/jme3User/JMEisSoCool/myAwesomeFolder/"</span>, FileLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">this</span>.<span class="me1">assetManager</span>.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Note that you should not register every single folder containing a texture as the assetmanager will not be able to discern between images with the same name anymore.
<strong>Learn more:</strong> <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>
</p>

</div>
<!-- EDIT13 SECTION "Why do I get AssetNotFoundException when loading X ?" [5467-6515] -->
<h3 class="sectionedit14" id="how_do_i_create_3-d_models_textures_sounds">How do I Create 3-D models, textures, sounds?</h3>
<div class="level3">

<p>
Follow our best practices for the <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">multi-media asset pipeline</a>. <br />

You create 3-D models in a 3-D mesh editor, for example Blender, and export it in Ogre Mesh XML (animated objects, scenes) or Wavefront OBJ format (static objects, scenes). 
You create textures in a graphic editor, for example Gimp, and export them as PNG or JPG.
You create sounds in an audio editor, for example, Audacity, and export them as WAVE or OGG.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/3d_models.html" class="wikilink1" title="jme3:advanced:3d_models">3D Models</a>,  <a href="/jme3/intermediate/multi-media_asset_pipeline.html" class="wikilink1" title="jme3:intermediate:multi-media_asset_pipeline">Multi-Media Asset Pipeline</a>, <a href="/sdk/blender.html" class="wikilink1" title="sdk:blender">JME3's blend-to-j3o importer</a>; <br />
<a href="http://blender.org" class="urlextern" title="http://blender.org" rel="nofollow">Download Blender</a>, <a href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro" class="urlextern" title="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro" rel="nofollow">Blender intro tutorial</a>, <a href="http://www.ogre3d.org/wiki/index.php/Blender_Exporter" class="urlextern" title="http://www.ogre3d.org/wiki/index.php/Blender_Exporter" rel="nofollow">Blender-to-Ogre plugin</a>, <a href="http://en.wikipedia.org/wiki/Comparison_of_3D_computer_graphics_software#Features" class="urlextern" title="http://en.wikipedia.org/wiki/Comparison_of_3D_computer_graphics_software#Features" rel="nofollow">Comparison of 3D graphic software features (Wikipedia)</a>.
</p>

</div>
<!-- EDIT14 SECTION "How do I Create 3-D models, textures, sounds?" [6516-7513] -->
<h3 class="sectionedit15" id="how_do_i_load_a_3-d_model_into_the_scene">How do I load a 3-D model into the scene?</h3>
<div class="level3">

<p>
Use the jMonkeyEngine SDK to convert models from Ogre XML or Wavefront OBJ formats to .j3o binary format. Load the .j3o file using the AssetManager.
</p>
<pre class="code java"><span class="co1">// To load .../jMonkeyProjects/MyGame/assets/Models/Ninja/Ninja.j3o</span>
Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.j3o"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">Hello Asset</a>, <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/asset/AssetManager.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/asset/AssetManager.java" rel="nofollow">come.jme3.assets.AssetManager</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/Geometry.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/scene/Geometry.java" rel="nofollow">com.jme3.scene.Geometry</a>, <a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer">jMonkeyEngine SDK j3o converter</a>,
<br />
<strong>Code sample:</strong> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/TestOgreLoading.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/model/TestOgreLoading.java" rel="nofollow">TestOgreLoading.java</a>, <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/export/TestOgreConvert.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/export/TestOgreConvert.java" rel="nofollow">TestOgreConvert.java</a>.
</p>

</div>
<!-- EDIT15 SECTION "How do I load a 3-D model into the scene?" [7514-8599] -->
<h3 class="sectionedit16" id="how_do_initialize_the_scene">How do initialize the scene?</h3>
<div class="level3">

<p>
Use the simpleInitApp() method in SimpleApplication (or initApp() in Application).
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_simpleapplication.html" class="wikilink1" title="jme3:beginner:hello_simpleapplication">Hello SimpleApplication</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/app/SimpleApplication.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/app/SimpleApplication.java" rel="nofollow">SimpleApplication.java</a>.
</p>

</div>
<!-- EDIT16 SECTION "How do initialize the scene?" [8600-8932] -->
<h2 class="sectionedit17" id="i_want_to_transform_objects_in_the_scene">I want to transform objects in the scene</h2>
<div class="level2">

</div>
<!-- EDIT17 SECTION "I want to transform objects in the scene" [8933-8985] -->
<h3 class="sectionedit18" id="how_do_i_move_or_turn_or_resize_a_spatial">How do I move or turn or resize a spatial?</h3>
<div class="level3">

<p>
To move or turn or resize a spatial you use transformations. You can concatenate transformations (e.g. perform rotations around several axes in one step using a Quaternion with <code>slerp()</code> or a com.jme3.math.Transform with interpolateTransforms().
</p>
<pre class="code java">spatial.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">1</span>,<span class="sy0">-</span><span class="nu0">3</span>,2.5f<span class="br0">)</span><span class="sy0">;</span> spatial.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>,3.14f,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> spatial.<span class="me1">scale</span><span class="br0">(</span><span class="nu0">2</span>,<span class="nu0">2</span>,<span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a>, <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a>, <a href="/jme3/math_for_dummies.html" class="wikilink1" title="jme3:math_for_dummies">math_for_dummies</a>.
</p>

</div>
<!-- EDIT18 SECTION "How do I move or turn or resize a spatial?" [8986-9495] -->
<h3 class="sectionedit19" id="how_do_i_make_a_spatial_move_by_itself">How do I make a spatial move by itself?</h3>
<div class="level3">

<p>
Change the geometry's translation (position) live in the update loop using setLocalTranslation() for non-physical and applyForce() or setWalkDirection() for physical objects. You can also define and remote-control a spatial's motion using <a href="/jme3/advanced/cinematics.html" class="wikilink1" title="jme3:advanced:cinematics">Cinematics</a>, e.g. to record cutscenes, or to implement mobile platforms, elevators, airships, etc.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_main_event_loop.html" class="wikilink1" title="jme3:beginner:hello_main_event_loop">Hello Loop</a>, <a href="/jme3/advanced/update_loop.html" class="wikilink1" title="jme3:advanced:update_loop">Update Loop</a>, <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a>, <a href="/jme3/advanced/cinematics.html" class="wikilink1" title="jme3:advanced:cinematics">Cinematics</a>
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/material/TestBumpModel.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/material/TestBumpModel.java" rel="nofollow">TestBumpModel.java</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/model/TestOgreLoading.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/model/TestOgreLoading.java" rel="nofollow">TestOgreLoading.java</a>
</p>

</div>
<!-- EDIT19 SECTION "How do I make a spatial move by itself?" [9496-10383] -->
<h3 class="sectionedit20" id="how_do_i_access_a_named_sub-mesh_in_model">How do I access a named sub-mesh in Model?</h3>
<div class="level3">
<pre class="code java">Geometry submesh <span class="sy0">=</span> <span class="br0">(</span>Geometry<span class="br0">)</span> model.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"door 12"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Learn more:</strong> <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a>
</p>

</div>
<!-- EDIT20 SECTION "How do I access a named sub-mesh in Model?" [10384-10553] -->
<h3 class="sectionedit21" id="how_do_i_make_procedural_or_custom_shapes">How do I make procedural or custom shapes?</h3>
<div class="level3">

<p>
You can programmatically create com.jme3.scene.Mesh'es.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/custom_meshes.html" class="wikilink1" title="jme3:advanced:custom_meshes">Custom Meshes</a>
</p>

</div>
<!-- EDIT21 SECTION "How do I make procedural or custom shapes?" [10554-10714] -->
<h2 class="sectionedit22" id="i_want_to_change_the_surface_of_objects_in_the_scene">I want to change the surface of objects in the scene</h2>
<div class="level2">

</div>
<!-- EDIT22 SECTION "I want to change the surface of objects in the scene" [10715-10779] -->
<h3 class="sectionedit23" id="why_is_my_uv_wrapping_texture_appearance_all_wrong">Why is my UV wrapping / texture appearance all wrong?</h3>
<div class="level3">

<p>
The most likely reason is the flipping of textures. You may be using the following default method:
</p>
<pre class="code java">  material.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"myTexture.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can set the boolean value in the constructor of TextureKey to flipped or not flipped. Toggle the boolean to see if it fixes your UV wrapping/texture problem:
</p>
<pre class="code java">  material.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, <span class="kw1">this</span>.<span class="me1">assetManager</span>.<span class="me1">loadTexture</span><span class="br0">(</span><span class="kw1">new</span> TextureKey<span class="br0">(</span><span class="st0">"myTexture.jpg"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT23 SECTION "Why is my UV wrapping / texture appearance all wrong?" [10780-11329] -->
<h3 class="sectionedit24" id="how_do_i_scale_mirror_or_wrap_a_texture">How do I scale, mirror, or wrap a texture?</h3>
<div class="level3">

<p>
You cannot scale a texture, but you scale the texture coordinates of the mesh the texture is applied to:
</p>
<pre class="code java">mesh.<span class="me1">scaleTextureCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">2</span>,<span class="nu0">2</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can choose among various <code>com.jme3.texture.Texture.WrapMode</code>s for individual texture maps of a material: BorderClamp, EdgeClamp, Clamp; MirrorBorderClamp, MirrorEdgeClamp, MirrorClamp; Repeat, MirroredRepeat.
</p>
<pre class="code java">material.<span class="me1">getTextureParam</span><span class="br0">(</span><span class="st0">"DiffuseMap"</span><span class="br0">)</span>.<span class="me1">getTextureValue</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT24 SECTION "How do I scale, mirror, or wrap a texture?" [11330-11871] -->
<h3 class="sectionedit25" id="how_do_i_change_color_or_shininess_of_an_material">How do I change color or shininess of an material?</h3>
<div class="level3">

<p>
Use the AssetManager to load Materials, and change material settings.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a>, <a href="/jme3/intermediate/how_to_use_materials.html" class="wikilink1" title="jme3:intermediate:how_to_use_materials">How To Use Materials</a>, <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a>, <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>.
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/material/TestNormalMapping.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/material/TestNormalMapping.java" rel="nofollow">TestNormalMapping.java</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/model/shape/TestSphere.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/model/shape/TestSphere.java" rel="nofollow">TestSphere.java</a>.
</p>

</div>
<!-- EDIT25 SECTION "How do I change color or shininess of an material?" [11872-12492] -->
<h3 class="sectionedit26" id="how_do_i_make_a_surface_wood_stone_metal_etc">How do I make a surface wood, stone, metal, etc?</h3>
<div class="level3">

<p>
Create Textures as image files. Use the AssetManager to load a Material and use texture mapping for improved looks.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a>, <a href="/jme3/intermediate/how_to_use_materials.html" class="wikilink1" title="jme3:intermediate:how_to_use_materials">How To Use Materials</a>, <a href="/jme3/advanced/materials_overview.html" class="wikilink1" title="jme3:advanced:materials_overview">Materials Overview</a>, <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a>, <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/asset/AssetManager.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/asset/AssetManager.java" rel="nofollow">come.jme3.assets.AssetManager</a>, <a href="http://wiki.blender.org/index.php/Doc:Manual/Textures/Maps/Bump_and_Normal_Maps" class="urlextern" title="http://wiki.blender.org/index.php/Doc:Manual/Textures/Maps/Bump_and_Normal_Maps" rel="nofollow">Blender: Creating Bump Maps and Normal Maps</a>
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/material/TestSimpleBumps.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/material/TestSimpleBumps.java" rel="nofollow">TestSimpleBumps.java</a>
</p>

</div>
<!-- EDIT26 SECTION "How do I make a surface wood, stone, metal, etc?" [12493-13278] -->
<h3 class="sectionedit27" id="why_are_materials_too_bright_too_dark_or_flickering">Why are materials too bright, too dark, or flickering?</h3>
<div class="level3">

<p>
If you use a lit material (based on Lighting.j3md) then you must attach a light source to the rootNode, otherwise you see nothing. If you use lit material colors, make sure you have specified an Ambient color (can be the same as the Diffuse color) if you use an AmbientLight. If you see objects, but they are gray or too dark, set the light color to white, or make it brighter (you can multiply the color value with a scalar), or add a global white light source (AmbientLight). Similarly, if everything is too white, tune down the lights. If materials flicker under a directional light, change the light direction vector. Change the background color (which is independent of light sources) to get a better contrast while debugging a light problem.
</p>

</div>
<!-- EDIT27 SECTION "Why are materials too bright, too dark, or flickering?" [13279-14092] -->
<h3 class="sectionedit28" id="how_do_i_make_geometries_cast_a_shadow">How do I make geometries cast a shadow?</h3>
<div class="level3">

<p>
Use com.jme3.shadow.BasicShadowRenderer together with com.jme3.light.DirectionalLight, and setShadowMode().
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/light_and_shadow.html" class="wikilink1" title="jme3:advanced:light_and_shadow">Light and Shadow</a>
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/effect/TestEverything.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/effect/TestEverything.java" rel="nofollow">TestEverything.java</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/light/TestShadow.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/light/TestShadow.java" rel="nofollow">TestShadow.java</a>
</p>

</div>
<!-- EDIT28 SECTION "How do I make geometries cast a shadow?" [14093-14611] -->
<h3 class="sectionedit29" id="how_do_i_make_materials_transparent">How do I make materials transparent?</h3>
<div class="level3">

<p>
Assign a texture with an alpha channel to a Material and set the Material's blend mode to alpha. Use this to create transparent or translucent materials such as glass, window panes, water, tree leaves, etc.
</p>
<pre class="code java">material.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBlendMode</span><span class="br0">(</span>BlendMode.<span class="me1">Alpha</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Learn more:</strong>  <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">Hello Material</a>, <a href="/jme3/intermediate/how_to_use_materials.html" class="wikilink1" title="jme3:intermediate:how_to_use_materials">How To Use Materials</a>, 
</p>

</div>
<!-- EDIT29 SECTION "How do I make materials transparent?" [14612-15048] -->
<h3 class="sectionedit30" id="how_do_i_force_or_disable_culling">How do I force or disable culling?</h3>
<div class="level3">

<p>
While debugging custom meshes, you can switch the <code>com.jme3.material.RenderState.FaceCullMode</code> off to see the inside and outside of the mesh. 
</p>
<pre class="code java">someMaterial.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setFaceCullMode</span><span class="br0">(</span>FaceCullMode.<span class="me1">Off</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can also deactivate the <code>com.jme3.scene.Spatial.CullHint</code> of a whole spatial to force jme to calculate it even if it is behind the camera and outside of view. 
</p>
<pre class="code java">someNode.<span class="me1">setCullHint</span><span class="br0">(</span>CullHint.<span class="me1">Never</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Learn more:</strong>  <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a>
</p>

</div>
<!-- EDIT30 SECTION "How do I force or disable culling?" [15049-15597] -->
<h3 class="sectionedit31" id="can_i_draw_only_an_outline_of_the_scene">Can I draw only an outline of the scene?</h3>
<div class="level3">

<p>
Add a renders state to the material's and activate <code>Wireframe</code>.
</p>
<pre class="code java">material.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Learn more:</strong> <a href="/jme3/advanced/debugging.html" class="wikilink1" title="jme3:advanced:debugging">Debugging</a>.
</p>

</div>
<!-- EDIT31 SECTION "Can I draw only an outline of the scene?" [15598-15834] -->
<h2 class="sectionedit32" id="i_want_to_control_the_camera">I want to control the camera</h2>
<div class="level2">

<p>
The default camera <code>cam</code> is an instance of the <code>Camera</code> class. <strong>Learn more:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/renderer/Camera.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-core/src/main/java/com/jme3/renderer/Camera.java" rel="nofollow">com.jme3.renderer.Camera</a>
</p>

</div>
<!-- EDIT32 SECTION "I want to control the camera" [15835-16100] -->
<h3 class="sectionedit33" id="how_do_i_keep_the_camera_from_moving">How do I keep the camera from moving?</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> SimpleApplication activates <code>flyCam</code> (an instance of <code>FlyByCamera</code>) by default. flyCam causes the camera to move with the mouse and the WASD keys. You can disable flyCam as follows:<pre class="code java">flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>

</div>
<!-- EDIT33 SECTION "How do I keep the camera from moving?" [16101-16382] -->
<h3 class="sectionedit34" id="how_do_i_switch_between_third-person_and_first-person_view">How do I switch between third-person and first-person view ?</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> You can activate the FlyBy Cam as a first-person camera. <br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a>. <br />
<strong>Code sample:</strong>  <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/input/FlyByCam.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/input/FlyByCam.java" rel="nofollow">com.jme3.input.FlyByCamera</a> <pre class="code java">flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> You can also create a third-person chase cam. <br />
<strong>Learn more:</strong> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/input/ChaseCamera.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/core/com/jme3/input/ChaseCamera.java" rel="nofollow">com.jme3.input.ChaseCamera</a> <br />
<strong>Code sample:</strong> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestChaseCamera.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestChaseCamera.java" rel="nofollow">jme3test/input/TestChaseCamera.java</a>. <pre class="code java">flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
chaseCam <span class="sy0">=</span> <span class="kw1">new</span> ChaseCamera<span class="br0">(</span>cam, spatial, inputManager<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>

</div>
<!-- EDIT34 SECTION "How do I switch between third-person and first-person view ?" [16383-17247] -->
<h3 class="sectionedit35" id="how_do_i_increase_camera_speed">How do I increase camera speed?</h3>
<div class="level3">
<pre class="code java">flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span>50f<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT35 SECTION "How do I increase camera speed?" [17248-17334] -->
<h2 class="sectionedit36" id="actions_interactions_physics">Actions, Interactions, Physics</h2>
<div class="level2">

</div>
<!-- EDIT36 SECTION "Actions, Interactions, Physics" [17335-17377] -->
<h3 class="sectionedit37" id="how_do_i_implement_game_logic_game_mechanics">How do I implement game logic / game mechanics?</h3>
<div class="level3">

<p>
Use Controls to define the behaviour of types of Spatials. Use Application States to implement global behaviour, to group subsets of input handlers or <abbr title="Graphical User Interface">GUI</abbr> screens, etc. Use the <code>simpleUpdate()</code> and <code>update()</code> loops for tests and interactions. Use Cinematics to remote-control objects in scenes.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_main_event_loop.html" class="wikilink1" title="jme3:beginner:hello_main_event_loop">Hello Loop</a>, <a href="/jme3/advanced/update_loop.html" class="wikilink1" title="jme3:advanced:update_loop">Update Loop</a>, <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a>, <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a>, <a href="/jme3/advanced/cinematics.html" class="wikilink1" title="jme3:advanced:cinematics">Cinematics</a>
</p>

</div>
<!-- EDIT37 SECTION "How do I implement game logic / game mechanics?" [17378-17939] -->
<h3 class="sectionedit38" id="how_do_i_let_players_interact_via_keyboard">How do I let players interact via keyboard?</h3>
<div class="level3">

<p>
Use com.jme3.input.KeyInput and a Input Listener.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">Hello Input</a>, <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">Input Handling</a>
</p>

</div>
<!-- EDIT38 SECTION "How do I let players interact via keyboard?" [17940-18147] -->
<h3 class="sectionedit39" id="how_do_i_let_players_interact_by_clicking">How do I let players interact by clicking?</h3>
<div class="level3">

<p>
Players typically click the mouse to pick up objects, to open doors, to shoot a weapon, etc. Use an Input Listener to respond to mouse clicks, then cast a ray from the player; if it intersects with the bounding volume of a spatial, this is the selected target. The links below contain code samples for both “fixed crosshair” picking and “free mouse pointer” picking.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_picking.html" class="wikilink1" title="jme3:beginner:hello_picking">Hello Picking</a>, <a href="/jme3/advanced/mouse_picking.html" class="wikilink1" title="jme3:advanced:mouse_picking">Mouse Picking</a>, <a href="/jme3/advanced/collision_and_intersection.html" class="wikilink1" title="jme3:advanced:collision_and_intersection">Collision and Intersection</a>, <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">Input Handling</a>, com.jme3.bounding.*, com.jme3.math.Ray, com.jme3.collision.CollisionResults.
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bounding/TestRayCollision.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bounding/TestRayCollision.java" rel="nofollow">TestRayCollision.java</a>
</p>

</div>
<!-- EDIT39 SECTION "How do I let players interact by clicking?" [18148-18984] -->
<h3 class="sectionedit40" id="how_do_i_animate_characters">How do I animate characters?</h3>
<div class="level3">

<p>
Create an animated OgreMesh model with bones in a 3-D mesh editor (e.g. Blender).
<br />
<strong>Learn more:</strong> com.jme3.animation.*, <a href="/jme3/beginner/hello_animation.html" class="wikilink1" title="jme3:beginner:hello_animation">Hello Animation</a>, <a href="/jme3/advanced/animation.html" class="wikilink1" title="jme3:advanced:animation">Animation</a>, <a href="http://wiki.blender.org/index.php/Doc:Tutorials/Animation/BSoD/Character_Animation" class="urlextern" title="http://wiki.blender.org/index.php/Doc:Tutorials/Animation/BSoD/Character_Animation" rel="nofollow">Blender animation tutorial</a>
<br />
<strong>Code sample:</strong>  <a href="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/model/anim" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/model/anim" rel="nofollow">animation</a>
</p>

</div>
<!-- EDIT40 SECTION "How do I animate characters?" [18985-19467] -->
<h3 class="sectionedit41" id="how_do_i_keep_players_from_falling_through_walls_and_floors">How do I keep players from falling through walls and floors?</h3>
<div class="level3">

<p>
Use collision detection. The most common solution is to use jme's physics integration, jBullet.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_collision.html" class="wikilink1" title="jme3:beginner:hello_collision">Hello Collision</a>, <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">Physics</a>, com.jme3.bullet.*, CapsuleCollisionShape versus CompoundCollisionShape, CharacterControl versus RigidBodyControl.
</p>

</div>
<!-- EDIT41 SECTION "How do I keep players from falling through walls and floors?" [19468-19830] -->
<h3 class="sectionedit42" id="how_do_i_make_balls_wheels_etc_bounce_and_roll">How do I make balls/wheels/etc bounce and roll?</h3>
<div class="level3">

<p>
Add physics controls to Spatials and give them spherical or cylindrical bounding volumes.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_physics.html" class="wikilink1" title="jme3:beginner:hello_physics">Hello Physics</a>, <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">Physics</a>, com.jme3.bounding.*, com.jme3.bullet.collisions, com.jme3.bullet.controls.RigidBodyControl,
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestSimplePhysics.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestSimplePhysics.java" rel="nofollow">TestSimplePhysics.java</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/bullet" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/bullet" rel="nofollow">more physics samples</a>
</p>

</div>
<!-- EDIT42 SECTION "How do I make balls/wheels/etc bounce and roll?" [19831-20452] -->
<h3 class="sectionedit43" id="how_do_i_debug_weird_physics_behaviour">How do I debug weird Physics behaviour?</h3>
<div class="level3">

<p>
Maybe your collision shapes overlap – or they are not where you think they are. Make the collision shapes visible by adding the following line after the bulletAppState initialization: 
</p>
<pre class="code java">bulletAppState.<span class="me1">getPhysicsSpace</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">enableDebug</span><span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT43 SECTION "How do I debug weird Physics behaviour?" [20453-20766] -->
<h3 class="sectionedit44" id="how_do_i_make_a_walking_character">How do I make a walking character?</h3>
<div class="level3">

<p>
You can use jBullet's CharacterControl that locks a physical object upright, so it does not tip over when moving/walking (as tall physical objects are typically wanted to).
<br />
<strong>Learn more:</strong> CharacterControl
<br />
Code samples: <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestQ3.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestQ3.java" rel="nofollow">TestQ3.java</a> (first-person), <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsCharacter.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsCharacter.java" rel="nofollow">TestPhysicsCharacter.java</a> (third-person)
</p>

</div>
<!-- EDIT44 SECTION "How do I make a walking character?" [20767-21358] -->
<h3 class="sectionedit45" id="how_do_i_steer_vehicles">How do I steer vehicles?</h3>
<div class="level3">

<p>
Use a VehicleControl that supports suspension behavior.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/vehicles.html" class="wikilink1" title="jme3:advanced:vehicles">Vehicles</a>, com.jme3.bullet.*, VehicleControl
<br />
Code samples: <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestFancyCar.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestFancyCar.java" rel="nofollow">TestFancyCar.java</a>, (Press HUJK keys to steer, spacebar to jump.)
</p>

</div>
<!-- EDIT45 SECTION "How do I steer vehicles?" [21359-21738] -->
<h3 class="sectionedit46" id="can_objects_swing_like_a_pendulums_chains_ropebridges">Can objects swing like a pendulums, chains, ropebridges?</h3>
<div class="level3">

<p>
Use a PhysicsControl's hinges and joints.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/hinges_and_joints.html" class="wikilink1" title="jme3:advanced:hinges_and_joints">Hinges and Joints</a>, com.jme3.bullet.joints.PhysicsHingeJoint,
<a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsHingeJoint.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsHingeJoint.java" rel="nofollow">TestPhysicsHingeJoint.java</a> (Press HK keys to turn, spacebar to swing.)
</p>

</div>
<!-- EDIT46 SECTION "Can objects swing like a pendulums, chains, ropebridges?" [21739-22151] -->
<h2 class="sectionedit47" id="default_gui_display">Default GUI Display</h2>
<div class="level2">

</div>
<!-- EDIT47 SECTION "Default GUI Display" [22152-22183] -->
<h3 class="sectionedit48" id="what_are_these_fps_objects_vertices_triangles_statistics">What are these FPS/Objects/Vertices/Triangles statistics?</h3>
<div class="level3">

<p>
At the bottom left of every default SimpleGame, you see the <a href="/jme3/advanced/statsview.html" class="wikilink1" title="jme3:advanced:statsview">StatsView</a> and the FPS (frames per seconds) view. These views provide you with extra information during the development phase. For example, if you notice the object count is increasing and the FPS is decreasing, then you know that your code attaches too many objects and does not detach enough of them again (maybe a loop gone wild?).
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/statsview.html" class="wikilink1" title="jme3:advanced:statsview">StatsView</a>
</p>

</div>
<!-- EDIT48 SECTION "What are these FPS/Objects/Vertices/Triangles statistics?" [22184-22711] -->
<h3 class="sectionedit49" id="how_do_i_get_rid_of_the_fps_objects_statistics">How do I get rid of the FPS/Objects statistics?</h3>
<div class="level3">

<p>
In the application's simpleInitApp() method, call: 
</p>
<pre class="code">setDisplayFps(false); // to hide the FPS
setDisplayStatView(false); // to hide the statistics </pre>

</div>
<!-- EDIT49 SECTION "How do I get rid of the FPS/Objects statistics?" [22712-22928] -->
<h3 class="sectionedit50" id="how_do_i_display_score_health_mini-maps_status_icons">How do I display score, health, mini-maps, status icons?</h3>
<div class="level3">

<p>
Attach text and pictures to the orthogonal <code>guiNode</code> to create a heads-up display (<a href="http://en.wikipedia.org/wiki/HUD_%28video_gaming%29" class="urlextern" title="http://en.wikipedia.org/wiki/HUD_%28video_gaming%29" rel="nofollow">HUD</a>).
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/hud.html" class="wikilink1" title="jme3:advanced:hud">HUD</a>, com.jme3.font.*, com.jme3.ui.Picture, guiNode.attachChild()
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/gui/TestOrtho.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/gui/TestOrtho.java" rel="nofollow">TestOrtho.java</a>, 
<a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/gui/TestBitmapFont.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/gui/TestBitmapFont.java" rel="nofollow">TestBitmapFont.java</a> |
</p>

</div>
<!-- EDIT50 SECTION "How do I display score, health, mini-maps, status icons?" [22929-23546] -->
<h3 class="sectionedit51" id="how_do_i_display_buttons_and_ui_controls">How do I display buttons and UI controls?</h3>
<div class="level3">

<p>
You may want to display buttons to let the player switch between the game, settings screen, and score screens. For buttons and other more advanced UI controls, jME supports the Nifty <abbr title="Graphical User Interface">GUI</abbr> library.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI</a>
<br />
Sample Code: <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/niftygui/TestNiftyGui.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/niftygui/TestNiftyGui.java" rel="nofollow">TestNiftyGui.java</a>
</p>

</div>
<!-- EDIT51 SECTION "How do I display buttons and UI controls?" [23547-24003] -->
<h3 class="sectionedit52" id="how_do_i_display_a_loading_screen">How do i display a loading screen?</h3>
<div class="level3">

<p>
Instead of having a frozen frame while your games loads, you can have a loading screen while it loads. 
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/loading_screen.html" class="wikilink1" title="jme3:advanced:loading_screen">Loading screen</a>
</p>

</div>
<!-- EDIT52 SECTION "How do i display a loading screen?" [24004-24220] -->
<h2 class="sectionedit53" id="nifty_gui">Nifty GUI</h2>
<div class="level2">

</div>
<!-- EDIT53 SECTION "Nifty GUI" [24221-24242] -->
<h3 class="sectionedit54" id="i_get_nosuchelementexception_when_adding_controls_buttons_etc">I get NoSuchElementException when adding controls (buttons etc)!</h3>
<div class="level3">

<p>
Verify that you include a controls definition file link in your XML: This is the default:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;useControls</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-controls.xml"</span><span class="re2">/&gt;</span></span></pre>

</div>
<!-- EDIT54 SECTION "I get NoSuchElementException when adding controls (buttons etc)!" [24243-24478] -->
<h3 class="sectionedit55" id="where_can_i_find_example_code_of_nifty_gui_s_xml_and_java_classes">Where can I find example code of Nifty GUI's XML and Java classes?</h3>
<div class="level3">

<p>
<a href="http://nifty-gui.svn.sourceforge.net/viewvc/nifty-gui/nifty-examples/trunk/src/main/" class="urlextern" title="http://nifty-gui.svn.sourceforge.net/viewvc/nifty-gui/nifty-examples/trunk/src/main/" rel="nofollow">http://nifty-gui.svn.sourceforge.net/viewvc/nifty-gui/nifty-examples/trunk/src/main/</a>
</p>

</div>
<!-- EDIT55 SECTION "Where can I find example code of Nifty GUI's XML and Java classes?" [24479-24641] -->
<h3 class="sectionedit56" id="is_there_java_doc_for_nifty_gui">Is there Java Doc for Nifty GUI?</h3>
<div class="level3">

<p>
<a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Nifty GUI 1.3 Java docs</a>
</p>

</div>
<!-- EDIT56 SECTION "Is there Java Doc for Nifty GUI?" [24642-24767] -->
<h2 class="sectionedit57" id="i_want_to_create_an_environment_with_sounds_effects_and_landscapes">I want to create an environment with sounds, effects, and landscapes</h2>
<div class="level2">

</div>
<!-- EDIT57 SECTION "I want to create an environment with sounds, effects, and landscapes" [24768-24848] -->
<h3 class="sectionedit58" id="how_do_i_play_sounds_and_noises">How do I play sounds and noises?</h3>
<div class="level3">

<p>
Use AudioRenderer, Listener, and AudioNode from com.jme3.audio.*.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_audio.html" class="wikilink1" title="jme3:beginner:hello_audio">Hello Audio</a>, <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">Audio</a>
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/audio" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/audio" rel="nofollow">audio</a>
</p>

</div>
<!-- EDIT58 SECTION "How do I play sounds and noises?" [24849-25164] -->
<h3 class="sectionedit59" id="how_do_i_make_fire_smoke_explosions_swarms_magic_spells">How do I make fire, smoke, explosions, swarms, magic spells?</h3>
<div class="level3">

<p>
For swarm like effects you use particle emitters.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_effects.html" class="wikilink1" title="jme3:beginner:hello_effects">Hello Effects</a>, <a href="/jme3/advanced/particle_emitters.html" class="wikilink1" title="jme3:advanced:particle_emitters">Particle Emitters</a>, <a href="/jme3/advanced/bloom_and_glow.html" class="wikilink1" title="jme3:advanced:bloom_and_glow">Bloom and Glow</a>, <a href="/jme3/advanced/effects_overview.html" class="wikilink1" title="jme3:advanced:effects_overview">Effects Overview</a>, com.jme3.effect.EmitterSphereShape, com.jme3.effect.ParticleEmitter
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/effect/TestExplosionEffect.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/effect/TestExplosionEffect.java" rel="nofollow">TestExplosionEffect.java</a>, 
<a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/effect/TestMovingParticle.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/effect/TestMovingParticle.java" rel="nofollow">TestMovingParticle.java</a>,
<a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/effect/TestSoftParticles.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/effect/TestSoftParticles.java" rel="nofollow">TestSoftParticle.java</a>
</p>

</div>
<!-- EDIT59 SECTION "How do I make fire, smoke, explosions, swarms, magic spells?" [25165-26004] -->
<h3 class="sectionedit60" id="how_do_i_make_water_waves_reflections">How do I make water, waves, reflections?</h3>
<div class="level3">

<p>
Use a special post-processor renderer from com.jme3.water.*.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/water.html" class="wikilink1" title="jme3:advanced:water">Water</a>, <a href="/jme3/advanced/post-processor_water.html" class="wikilink1" title="jme3:advanced:post-processor_water">Post-Processor Water</a>
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/water/TestSimpleWater.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/water/TestSimpleWater.java" rel="nofollow">TestSimpleWater.java</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/water/TestSceneWater.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/water/TestSceneWater.java" rel="nofollow">TestSceneWater.java</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/water/TestPostWaterLake.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/water/TestPostWaterLake.java" rel="nofollow">TestPostWaterLake.java</a>, <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/water/TestPostWater.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/water/TestPostWater.java" rel="nofollow">TestPostWater.java</a>
</p>

</div>
<!-- EDIT60 SECTION "How do I make water, waves, reflections?" [26005-26813] -->
<h3 class="sectionedit61" id="how_do_i_make_fog_bloom_blur_light_scattering">How do I make fog, bloom, blur, light scattering?</h3>
<div class="level3">

<p>
Use special post-processor renderers from com.jme3.post.*.
<br />
<strong>Learn more:</strong> <a href="/jme3/advanced/effects_overview.html" class="wikilink1" title="jme3:advanced:effects_overview">effects_overview</a>
</p>

</div>
<!-- EDIT61 SECTION "How do I make fog, bloom, blur, light scattering?" [26814-26988] -->
<h3 class="sectionedit62" id="how_do_i_generate_a_terrain">How do I generate a terrain?</h3>
<div class="level3">

<p>
Use com.jme3.terrain.*. The JMonkeyEngine also provides you with a Terrain Editor plugin.
<br />
<strong>Learn more:</strong> <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">Hello Terrain</a>, <a href="/jme3/advanced/terrain.html" class="wikilink1" title="jme3:advanced:terrain">Terrain</a>, <a href="/sdk/terrain_editor.html" class="wikilink1" title="sdk:terrain_editor">Terrain Editor</a>
<br />
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/terrain/TerrainTest.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/terrain/TerrainTest.java" rel="nofollow">TerrainTest.java</a>
</p>

</div>
<!-- EDIT62 SECTION "How do I generate a terrain?" [26989-27384] -->
<h3 class="sectionedit63" id="how_do_i_make_a_sky">How do I make a sky?</h3>
<div class="level3">

<p>
<strong>Code sample:</strong> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/texture/TestSkyLoading.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/texture/TestSkyLoading.java" rel="nofollow">TestSkyLoading.java</a>
</p>
<pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>SkyFactory.<span class="me1">createSky</span><span class="br0">(</span> assetManager,
       <span class="st0">"Textures/Sky/Bright/BrightSky.dds"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
skyGeo.<span class="me1">setQueueBucket</span><span class="br0">(</span>Bucket.<span class="me1">Sky</span><span class="br0">)</span> </pre>

<p>
<strong>Learn more:</strong> <a href="/jme3/advanced/sky.html" class="wikilink1" title="jme3:advanced:sky">Sky</a>
</p>

</div>
<!-- EDIT63 SECTION "How do I make a sky?" [27385-27782] -->
<h2 class="sectionedit64" id="i_want_to_access_to_back-end_properties">I want to access to back-end properties</h2>
<div class="level2">

</div>
<!-- EDIT64 SECTION "I want to access to back-end properties" [27783-27834] -->
<h3 class="sectionedit65" id="how_do_i_read_out_graphic_card_capabilities">How do I read out graphic card capabilities?</h3>
<div class="level3">

<p>
If your game is heavily using features that older cards do not support, you can <a href="/jme3/advanced/read_graphic_card_capabilites.html" class="wikilink1" title="jme3:advanced:read_graphic_card_capabilites">Read Graphic Card Capabilites</a> in the beginning before starting the app, and then decide how to proceed.
</p>
<pre class="code java">Collection<span class="sy0">&lt;</span>com.<span class="me1">jme3</span>.<span class="me1">renderer</span>.<span class="me1">Caps</span><span class="sy0">&gt;</span> caps <span class="sy0">=</span> renderer.<span class="me1">getCaps</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Logger.<span class="me1">getLogger</span><span class="br0">(</span>HelloJME3.<span class="kw1">class</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">log</span><span class="br0">(</span>Level.<span class="me1">INFO</span>, <span class="st0">"Capabilities: {0}"</span>, caps.<span class="me1">toString</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT65 SECTION "How do I read out graphic card capabilities?" [27835-28270] -->
<h3 class="sectionedit66" id="how_do_i_run_jmonkeyengine_3_with_opengl1">How do I Run jMonkeyEngine 3 with OpenGL1?</h3>
<div class="level3">

<p>
In your game, add 
</p>
<pre class="code java">settings.<span class="me1">setRenderer</span><span class="br0">(</span>AppSettings.<span class="me1">LWJGL_OPENGL1</span><span class="br0">)</span></pre>

<p>
 to the <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">AppSettings</a> (see details there). <br />

For the jMonkeyEngine SDK itself, choose Options &gt; OpenGL, and check OpenGL1.
</p>

</div>
<!-- EDIT66 SECTION "How do I Run jMonkeyEngine 3 with OpenGL1?" [28271-28551] -->
<h3 class="sectionedit67" id="how_do_i_optimize_the_heck_out_of_the_scene_graph">How do I optimize the heck out of the Scene Graph?</h3>
<div class="level3">

<p>
You can batch all Geometries in a scene (or a subnode) that remains static.
</p>
<pre class="code java">jme3tools.<span class="me1">optimize</span>.<span class="me1">GeometryBatchFactory</span>.<span class="me1">optimize</span><span class="br0">(</span>rootNode<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Batching means that all Geometries with the same Material are combined into one mesh. This optimization only has an effect if you use only few (roughly up to 32) Materials total. The pay-off is that batching takes extra time when the game is initialized.
</p>

</div>
<!-- EDIT67 SECTION "How do I optimize the heck out of the Scene Graph?" [28552-29021] -->
<h3 class="sectionedit68" id="how_do_i_prevent_users_from_unzipping_my_jar">How do I prevent users from unzipping my JAR?</h3>
<div class="level3">

<p>
Add an <a href="http://netbeans.dzone.com/tips/obfuscating-netbeans-java-appl" class="urlextern" title="http://netbeans.dzone.com/tips/obfuscating-netbeans-java-appl" rel="nofollow">obfuscator to the Ant script</a>. The SDK comes with a basic obfuscation script that you can enable in the project settings.
</p>

</div>
<!-- EDIT68 SECTION "How do I prevent users from unzipping my JAR?" [29022-29271] -->
<h2 class="sectionedit69" id="i_want_to_do_maths">I want to do maths</h2>
<div class="level2">

</div>
<!-- EDIT69 SECTION "I want to do maths" [29272-29302] -->
<h3 class="sectionedit70" id="what_does_addlocal_multlocal_etc_mean">What does addLocal() / multLocal() etc mean?</h3>
<div class="level3">

<p>
Many maths functions (mult(), add(), subtract(), etc) come as local and a non-local variant (multLocal(), addLocal(), subtractLocal(), etc).
</p>
<ol>
<li class="level1"><div class="li"> Non-local means a new independent object is created (similar to clone()) as a return value. Use non-local methods if you want to keep using the old value of the object calling the method.</div>
<ul>
<li class="level2"><div class="li"> Example 1:  <code>Quaternion q1 = q2.mult(q3);</code></div>
<ul>
<li class="level3"><div class="li"> Returns the result as a new Quaternion q1.</div>
</li>
<li class="level3"><div class="li"> The involved objects q2 and q3 stay as they are and can be reused.</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> Example 2: <code>v.mult(b).add(b);</code> <img src="/lib/images/smileys/icon_exclaim.gif" class="icon" alt=":!:" /></div>
<ul>
<li class="level3"><div class="li"> <strong>Watch out:</strong> This calculates the expected result, but unless you actually use the return value, it is discarded!</div>
</li>
</ul>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Local means that no new objects are created, instead, the calling object is modified. Use this if you are sure you no longer need the old value of the calling object.</div>
<ul>
<li class="level2"><div class="li"> Example 1: <code>q2.multLocal(q3)</code></div>
<ul>
<li class="level3"><div class="li"> Calculates q2*q3 without creating temp objects.</div>
</li>
<li class="level3"><div class="li"> The result is stored in the calling object q2. The old value of q2 is gone.</div>
</li>
<li class="level3"><div class="li"> Object q3 stays as it was.</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> Example 2:<code>v.multLocal(a).addLocal(b);</code></div>
<ul>
<li class="level3"><div class="li"> Calculates the expected result without creating temp objects.</div>
</li>
<li class="level3"><div class="li"> The result is stored in the calling object v. The old value of v is gone.</div>
</li>
<li class="level3"><div class="li"> The objects a and b stay as they were.</div>
</li>
</ul>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT70 SECTION "What does addLocal() / multLocal() etc mean?" [29303-30664] -->
<h3 class="sectionedit71" id="what_is_the_difference_between_world_and_local_coordinates">What is the difference between World and Local coordinates?</h3>
<div class="level3">

<p>
World coordinates of a Spatial are its absolute coordinates in the 3D scene (this is like giving GPS coordinates). Local coordinates are relative to the Spatial's parent Spatial (this is like saying, “I'm ten meters left of the entrance”).
</p>

</div>
<!-- EDIT71 SECTION "What is the difference between World and Local coordinates?" [30665-30974] -->
<h3 class="sectionedit72" id="how_do_i_convert_degrees_to_radians">How do I convert Degrees to Radians?</h3>
<div class="level3">

<p>
Multiply degree value by FastMath.DEG_TO_RAD to convert it to radians.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/faq.html" class="wikilink1" title="tag:faq" rel="tag">faq</a>
</span></div>

</div>
<!-- EDIT72 SECTION "How do I convert Degrees to Radians?" [30975-] -->
