---
title: Integrating Nifty GUI: Overlay
---
<h1 class="sectionedit1" id="integrating_nifty_guioverlay">Integrating Nifty GUI: Overlay</h1>
<div class="level1">
<ol>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI Concepts</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_best_practices.html" class="wikilink1" title="jme3:advanced:nifty_gui_best_practices">Nifty GUI Best Practices</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_xml_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_xml_layout">Nifty GUI XML Layout</a> or <a href="/jme3/advanced/nifty_gui_java_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_layout">Nifty GUI Java Layout</a></div>
</li>
<li class="level1"><div class="li"> <strong>Nifty <abbr title="Graphical User Interface">GUI</abbr> Overlay</strong> or <a href="/jme3/advanced/nifty_gui_projection.html" class="wikilink1" title="jme3:advanced:nifty_gui_projection">Nifty GUI Projection</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Interact with the GUI from Java</a></div>
</li>
</ol>

<p>
<a href="/resources/jme3-advanced-nifty-gui-example.png" class="media" title="jme3:advanced:nifty-gui-example.png"><img src="/resources/jme3-advanced-nifty-gui-example.png" class="medialeft" alt="" width="300" height="200" /></a>
</p>

<p>
Typically, you define a key (for example escape) that switches the <abbr title="Graphical User Interface">GUI</abbr> on and off. The <abbr title="Graphical User Interface">GUI</abbr> can be a StartScreen, OptionsScreen, CharacterCreationScreen, etc. While the <abbr title="Graphical User Interface">GUI</abbr> is up, you pause the running game, and then overlay the <abbr title="Graphical User Interface">GUI</abbr>. You also must switch to a different set of user inputs while the game is paused, so the player can use the mouse pointer and keyboard to interact with the <abbr title="Graphical User Interface">GUI</abbr>.
</p>

<p>
You can also <a href="/jme3/advanced/nifty_gui_projection.html" class="wikilink1" title="jme3:advanced:nifty_gui_projection">project</a> the <abbr title="Graphical User Interface">GUI</abbr> as a texture onto a mesh texture (but then you cannot click to select).
On this page, we look at the overlay variant, which is more commonly used in games.
</p>

</div>
<!-- EDIT1 SECTION "Integrating Nifty GUI: Overlay" [1-1043] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/niftygui/TestNiftyGui.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/niftygui/TestNiftyGui.java" rel="nofollow">TestNiftyGui.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [1044-1206] -->
<h2 class="sectionedit3" id="overlaying_the_user_interface_over_the_screen">Overlaying the User Interface Over the Screen</h2>
<div class="level2">

<p>
This code shows you how to overlay anything on the screen with the <abbr title="Graphical User Interface">GUI</abbr>. This is the most common usecase.
</p>
<pre class="code java">NiftyJmeDisplay niftyDisplay <span class="sy0">=</span> <span class="kw1">new</span> NiftyJmeDisplay<span class="br0">(</span>
    assetManager, inputManager, audioRenderer, guiViewPort<span class="br0">)</span><span class="sy0">;</span>
<span class="co3">/** Create a new NiftyGUI object */</span>
Nifty nifty <span class="sy0">=</span> niftyDisplay.<span class="me1">getNifty</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co3">/** Read your XML and initialize your custom ScreenController */</span>
nifty.<span class="me1">fromXml</span><span class="br0">(</span><span class="st0">"Interface/tutorial/step2/screen.xml"</span>, <span class="st0">"start"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// nifty.fromXml("Interface/helloworld.xml", "start", new MySettingsScreen(data));</span>
<span class="co1">// attach the Nifty display to the gui view port as a processor</span>
guiViewPort.<span class="me1">addProcessor</span><span class="br0">(</span>niftyDisplay<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// disable the fly cam</span>
flyCam.<span class="me1">setDragToRotate</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Currently you do not have a ScreenController – we will create one in the next exercise. As soon  as you have a screen controller, you will use the commented variant of the XML loading method:
</p>
<pre class="code java">nifty.<span class="me1">fromXml</span><span class="br0">(</span><span class="st0">"Interface/helloworld.xml"</span>, <span class="st0">"start"</span>, <span class="kw1">new</span> MySettingsScreen<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The <code>MySettingsScreen</code> class is a custom de.lessvoid.nifty.screen.ScreenController in which you will implement your <abbr title="Graphical User Interface">GUI</abbr> behaviour. 
</p>

<p>
If you have many screens or you want to keep them organized in separate files there is a method available that will just load an additional XML file. The content of the files are
simply added to whatever XML data has been loaded before.
</p>
<pre class="code java">nifty.<span class="me1">addXml</span><span class="br0">(</span><span class="st0">"Interface/mysecondscreen.xml"</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT3 SECTION "Overlaying the User Interface Over the Screen" [1207-2675] -->
<h2 class="sectionedit4" id="next_steps">Next Steps</h2>
<div class="level2">

<p>
Now that you have layed out and integrated the <abbr title="Graphical User Interface">GUI</abbr> in your app, you want to respond to user input and display the current game. Time to create a ScreenController!
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Interact with the GUI from Java</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/nifty.html" class="wikilink1" title="tag:nifty" rel="tag">nifty</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Next Steps" [2676-] -->
