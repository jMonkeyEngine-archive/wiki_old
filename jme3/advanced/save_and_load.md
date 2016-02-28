---
title: Saving and Loading Games (.j3o)
---
<h1 class="sectionedit1" id="saving_and_loading_games_j3o">Saving and Loading Games (.j3o)</h1>
<div class="level1">

<p>
Spatials (that is Nodes and Geometries) can contain audio and light nodes, particle emitters, controls, and user data (player score, health, inventory, etc). For your game distribution, you must convert all original models to a faster binary format. You save individual Spatials as well as scenes using <code>com.jme3.export.binary.BinaryExporter</code>. 
</p>

<p>
The jMonkeyEngine's binary file format is called <code>.j3o</code>. You can convert, view and edit .j3o files and their materials in the jMonkeyEngine <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> and compose scenes (this does not include editing meshes). For the conversion, you can either use the BinaryExporters, or a context menu in the SDK.
</p>

<p>
</p><p></p><div class="noteimportant">The jMonkeyEngine's serialization system is the <code>com.jme3.export.Savable</code> interface. JME3's BinaryExporter can write standard Java objects, JME3 objects, and primitive data types that are included in a <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">spatial's user data</a>. If you use custom game data classes, see below how to make them “Savable”.
</div>


<p>
There is also a com.jme3.export.xml.XMLExporter and com.jme3.export.xml.XMLImporter that similarly converts jme3 spatials to an XML format. But you wouldn't use that to load models at runtime (quite slow).
</p>

</div>
<!-- EDIT1 SECTION "Saving and Loading Games (.j3o)" [1-1239] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/tools/TestSaveGame.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/tools/TestSaveGame.java" rel="nofollow">TestSaveGame.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [1240-1409] -->
<h2 class="sectionedit3" id="saving_a_node">Saving a Node</h2>
<div class="level2">

<p>
The following example overrides <code>stop()</code> in SimpleApplication to save the rootNode to a file when the user quits the application. The saved rootNode is a normal .j3o binary file that you can open in the <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a>.
</p>

<p>
</p><p></p><div class="notewarning">Note that when you save a model that has textures, the references to those textures are stored as absolute paths, so when loading the j3o file again, the textures have to be accessible at the exact location (relative to the assetmanager root, by default the <code>assets</code> directory) they were loaded from. This is why the SDK manages the conversion on the project level.
</div>

<pre class="code java">  <span class="coMULTI">/* This is called when the user quits the app. */</span>
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> stop<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> userHome <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"user.home"</span><span class="br0">)</span><span class="sy0">;</span>
    BinaryExporter exporter <span class="sy0">=</span> BinaryExporter.<span class="me1">getInstance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> file <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a><span class="br0">(</span>userHome<span class="sy0">+</span><span class="st0">"/Models/"</span><span class="sy0">+</span><span class="st0">"MyModel.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">try</span> <span class="br0">{</span>
      exporter.<span class="me1">save</span><span class="br0">(</span>rootNode, file<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> ex<span class="br0">)</span> <span class="br0">{</span>
      Logger.<span class="me1">getLogger</span><span class="br0">(</span>Main.<span class="kw1">class</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">log</span><span class="br0">(</span>Level.<span class="me1">SEVERE</span>, <span class="st0">"Error: Failed to save game!"</span>, ex<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">super</span>.<span class="me1">stop</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// continue quitting the game</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Saving a Node" [1410-2560] -->
<h2 class="sectionedit4" id="loading_a_node">Loading a Node</h2>
<div class="level2">

<p>
The following example overrides <code>simpleInitApp()</code> in SimpleApplication to load <code>Models/MyModel.j3o</code> when the game is initialized.
</p>
<pre class="code java">  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
     <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> userHome <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"user.home"</span><span class="br0">)</span><span class="sy0">;</span>
     assetManager.<span class="me1">registerLocator</span><span class="br0">(</span>userHome, FileLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
     Node loadedNode <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span>assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/MyModel.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
     loadedNode.<span class="me1">setName</span><span class="br0">(</span><span class="st0">"loaded node"</span><span class="br0">)</span><span class="sy0">;</span>
     rootNode.<span class="me1">attachChild</span><span class="br0">(</span>loadedNode<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 </pre>

<p>
</p><p></p><div class="notetip">Here you see why we save user data inside spatials – so it can be saved and loaded together with the .j3o file. If you have game data outside Spatials, you have to remember to save() and load(), and get() and set() it yourself.
</div>


</div>
<!-- EDIT4 SECTION "Loading a Node" [2561-3314] -->
<h2 class="sectionedit5" id="custom_savable_class">Custom Savable Class</h2>
<div class="level2">

<p>
JME's BinaryExporter can write standard Java objects (String, ArrayList, buffers, etc), JME objects (Savables, such as Material), and primitive data types (int, float, etc). If you are using any custom class together with a Spatial, then the custom class must implement the <code>com.jme3.export.Savable</code> interface. There are two common cases where this is relevant:
</p>
<ul>
<li class="level1"><div class="li"> The Spatial is carrying any <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a>. <br />
Example: You used something like <code>mySpatial.addControl(myControl);</code></div>
</li>
<li class="level1"><div class="li"> The Spatial's user data can contain a custom Java object. <br />
Example: You used something like <code>mySpatial.setUserData(“inventory”, myInventory);</code></div>
</li>
</ul>

<p>
If your custom classes (the user data or the Controls) do not implement Savable, then the BinaryImporter/BinaryExporter cannot save the Spatial!
</p>

<p>
So every time you create a custom Control or custom user data class, remember to implement Savable:
</p>
<pre class="code java"><span class="kw1">import</span> <span class="co2">com.jme3.export.InputCapsule</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.export.JmeExporter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.export.JmeImporter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.export.OutputCapsule</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.export.Savable</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.io.IOException</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> MyCustomClass <span class="kw1">implements</span> Savable <span class="br0">{</span>
    <span class="kw1">private</span> <span class="kw4">int</span>      someIntValue<span class="sy0">;</span>   <span class="co1">// some custom user data</span>
    <span class="kw1">private</span> <span class="kw4">float</span>    someFloatValue<span class="sy0">;</span> <span class="co1">// some custom user data</span>
    <span class="kw1">private</span> Material someJmeObject<span class="sy0">;</span>  <span class="co1">// some custom user data</span>
 
    ...
    <span class="co1">// your other code...</span>
    ...
 
    <span class="kw1">public</span> <span class="kw4">void</span> write<span class="br0">(</span>JmeExporter ex<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
        OutputCapsule capsule <span class="sy0">=</span> ex.<span class="me1">getCapsule</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
        capsule.<span class="me1">write</span><span class="br0">(</span>someIntValue,   <span class="st0">"someIntValue"</span>,   <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        capsule.<span class="me1">write</span><span class="br0">(</span>someFloatValue, <span class="st0">"someFloatValue"</span>, 0f<span class="br0">)</span><span class="sy0">;</span>
        capsule.<span class="me1">write</span><span class="br0">(</span>someJmeObject,  <span class="st0">"someJmeObject"</span>,  <span class="kw1">new</span> Material<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> read<span class="br0">(</span>JmeImporter im<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
        InputCapsule capsule <span class="sy0">=</span> im.<span class="me1">getCapsule</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
        someIntValue   <span class="sy0">=</span> capsule.<span class="me1">readInt</span><span class="br0">(</span>    <span class="st0">"someIntValue"</span>,   <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        someFloatValue <span class="sy0">=</span> capsule.<span class="me1">readFloat</span><span class="br0">(</span>  <span class="st0">"someFloatValue"</span>, 0f<span class="br0">)</span><span class="sy0">;</span>
        someJmeObject  <span class="sy0">=</span> capsule.<span class="me1">readSavable</span><span class="br0">(</span><span class="st0">"someJmeObject"</span>,  <span class="kw1">new</span> Material<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
To make a custom class savable:
</p>
<ol>
<li class="level1"><div class="li"> Implement <code>Savable</code> and add the <code>write()</code> and <code>read()</code> methods as shown in the example above.</div>
</li>
<li class="level1"><div class="li"> Do the following for each non-temporary class field: </div>
<ul>
<li class="level2"><div class="li"> Add one line that <code>write()</code>s the data to the JmeExport output capsule. </div>
<ul>
<li class="level3"><div class="li"> Specify the variable to save, give it a String name (can be the same as the variable name), and specify a default value.</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> Add one line that <code>read…()</code>s the data to the JmeImport input capsule. </div>
<ul>
<li class="level3"><div class="li"> On the left side of the assignment, specify the class field that you are restoring</div>
</li>
<li class="level3"><div class="li"> On the right side, use the appropriate <code>capsule.read…()</code> method for the data type. Specify the String name of the variable (must be the same as you used in the <code>write() method</code>), and again specify a default value.</div>
</li>
</ul>
</li>
</ul>
</li>
</ol>

<p>
</p><p></p><div class="noteimportant">As with all serialization, remember that if you ever change data types in custom classes, the updated read() methods will no longer be able to read your old files. Also there has to be a constructor that takes no Parameters.
</div>

<div class="tags"><span>
	<a href="/tag/convert.html" class="wikilink1" title="tag:convert" rel="tag">convert</a>,
	<a href="/tag/j3o.html" class="wikilink1" title="tag:j3o" rel="tag">j3o</a>,
	<a href="/tag/models.html" class="wikilink1" title="tag:models" rel="tag">models</a>,
	<a href="/tag/load.html" class="wikilink1" title="tag:load" rel="tag">load</a>,
	<a href="/tag/save.html" class="wikilink1" title="tag:save" rel="tag">save</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/serialization.html" class="wikilink1" title="tag:serialization" rel="tag">serialization</a>,
	<a href="/tag/import.html" class="wikilink1" title="tag:import" rel="tag">import</a>,
	<a href="/tag/export.html" class="wikilink1" title="tag:export" rel="tag">export</a>,
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>
</span></div>

</div>
<!-- EDIT5 SECTION "Custom Savable Class" [3315-] -->
