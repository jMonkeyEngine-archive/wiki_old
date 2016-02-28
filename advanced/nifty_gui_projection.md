---
title: Integrating Nifty GUI: Projection
---
<h1 class="sectionedit1" id="integrating_nifty_guiprojection">Integrating Nifty GUI: Projection</h1>
<div class="level1">
<ol>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI Concepts</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_best_practices.html" class="wikilink1" title="jme3:advanced:nifty_gui_best_practices">Nifty GUI Best Practices</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_xml_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_xml_layout">Nifty GUI XML Layout</a> or <a href="/jme3/advanced/nifty_gui_java_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_layout">Nifty GUI Java Layout</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_overlay.html" class="wikilink1" title="jme3:advanced:nifty_gui_overlay">Nifty GUI Overlay</a> or <strong>Nifty <abbr title="Graphical User Interface">GUI</abbr> Projection</strong></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Interact with the GUI from Java</a></div>
</li>
</ol>

<p>
<a href="/resources/jme3-advanced-nifty-gui.png" class="media" title="jme3:advanced:nifty-gui.png"><img src="/resources/jme3-advanced-nifty-gui.png" class="medialeft" alt="" width="310" height="250" /></a>
</p>

<p>
Typically you define a key (for example escape) to switch the <abbr title="Graphical User Interface">GUI</abbr> on and off. Then you <a href="/jme3/advanced/nifty_gui_overlay.html" class="wikilink1" title="jme3:advanced:nifty_gui_overlay">overlay</a> the running game with the <abbr title="Graphical User Interface">GUI</abbr> (you will most likely pause the game then). 
</p>

<p>
Alternatively, you can also project the <abbr title="Graphical User Interface">GUI</abbr> as a texture onto a mesh textures inside the game. Allthough this looks cool and “immersive”, this approach is rarely used since it is difficult to record clicks this way. You can only interact with this projected <abbr title="Graphical User Interface">GUI</abbr> by keyboard, or programmatically. You can select input fields using the arrow keys, and trigger actions using the return key. 
</p>

<p>
This <abbr title="Graphical User Interface">GUI</abbr> projection variant is less commonly used than the <abbr title="Graphical User Interface">GUI</abbr> overlay variant. Usecases for <abbr title="Graphical User Interface">GUI</abbr> projection are, for example, a player avatar using an in-game computer screen.
</p>

</div>
<!-- EDIT1 SECTION "Integrating Nifty GUI: Projection" [1-1192] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/niftygui/TestNiftyToMesh.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/niftygui/TestNiftyToMesh.java" rel="nofollow">TestNiftyToMesh.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [1193-1360] -->
<h2 class="sectionedit3" id="projecting_the_user_interface_onto_a_texture">Projecting the User Interface Onto a Texture</h2>
<div class="level2">

<p>
You can project the Nifty <abbr title="Graphical User Interface">GUI</abbr> onto a texture, load the texture into a material, and assign it to a Geometry (Quads or Boxes are best). 
</p>
<pre class="code java"><span class="co3">/** Create a special viewport for the Nifty GUI */</span>
ViewPort niftyView <span class="sy0">=</span> renderManager.<span class="me1">createPreView</span><span class="br0">(</span><span class="st0">"NiftyView"</span>, <span class="kw1">new</span> Camera<span class="br0">(</span><span class="nu0">1024</span>, <span class="nu0">768</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
niftyView.<span class="me1">setClearEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co3">/** Create a new NiftyJmeDisplay for the integration */</span>
NiftyJmeDisplay niftyDisplay <span class="sy0">=</span> <span class="kw1">new</span> NiftyJmeDisplay<span class="br0">(</span>
  assetManager,  inputManager,  audioRenderer,  niftyView<span class="br0">)</span><span class="sy0">;</span>
<span class="co3">/** Create a new NiftyGUI object */</span>
Nifty nifty <span class="sy0">=</span> niftyDisplay.<span class="me1">getNifty</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co3">/** Read your XML and initialize your custom ScreenController */</span>
nifty.<span class="me1">fromXml</span><span class="br0">(</span><span class="st0">"Interface/helloworld.xml"</span>, <span class="st0">"start"</span>, <span class="kw1">new</span> MySettingsScreen<span class="br0">(</span>data<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co3">/** Prepare a framebuffer for the texture niftytex */</span>
niftyView.<span class="me1">addProcessor</span><span class="br0">(</span>niftyDisplay<span class="br0">)</span><span class="sy0">;</span>
FrameBuffer fb <span class="sy0">=</span> <span class="kw1">new</span> FrameBuffer<span class="br0">(</span><span class="nu0">1024</span>, <span class="nu0">768</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
fb.<span class="me1">setDepthBuffer</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+format"><span class="kw3">Format</span></a>.<span class="me1">Depth</span><span class="br0">)</span><span class="sy0">;</span>
Texture2D niftytex <span class="sy0">=</span> <span class="kw1">new</span> Texture2D<span class="br0">(</span><span class="nu0">1024</span>, <span class="nu0">768</span>, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+format"><span class="kw3">Format</span></a>.<span class="me1">RGB8</span><span class="br0">)</span><span class="sy0">;</span>
fb.<span class="me1">setColorTexture</span><span class="br0">(</span>niftytex<span class="br0">)</span><span class="sy0">;</span>
niftyView.<span class="me1">setClearEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
niftyView.<span class="me1">setOutputFrameBuffer</span><span class="br0">(</span>fb<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co3">/** This is the 3D cube we project the GUI on */</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"m_ColorMap"</span>, niftytex<span class="br0">)</span><span class="sy0">;</span> <span class="co3">/** Here comes the texture! */</span>
geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The MySettingsScreen class is a custom de.lessvoid.nifty.screen.ScreenController in which you implement your <abbr title="Graphical User Interface">GUI</abbr> behaviour.  The variable <code>data</code> contains an object that you use to exchange state info with the game. See <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Nifty GUI Java Interaction</a> for details on how to create this class.
</p>

<p>
Run the code sample. You select buttons on this <abbr title="Graphical User Interface">GUI</abbr> with the arrow keys and then press return. Note that clicking on the texture will not work!
</p>

</div>
<!-- EDIT3 SECTION "Projecting the User Interface Onto a Texture" [1361-3239] -->
<h2 class="sectionedit4" id="next_steps">Next Steps</h2>
<div class="level2">

<p>
Now that you have layed out and integrated the <abbr title="Graphical User Interface">GUI</abbr> in your app, you want to respond to user input and display the current game.
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Interact with the GUI from Java</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/nifty.html" class="wikilink1" title="tag:nifty" rel="tag">nifty</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Next Steps" [3240-] -->
