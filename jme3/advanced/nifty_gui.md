---
title: Creating JME3 User Interfaces with Nifty GUI
---
<h1 class="sectionedit1" id="creating_jme3_user_interfaces_with_nifty_gui">Creating JME3 User Interfaces with Nifty GUI</h1>
<div class="level1">

<p>
<a href="/resources/jme3-advanced-nifty-gui-13.png" class="media" title="jme3:advanced:nifty-gui-13.png"><img src="/resources/jme3-advanced-nifty-gui-13.png" class="medialeft" alt="" width="276" height="217" /></a>
</p>

<p>
You may want your players to press a button to save a game, you want a scrolling text field for highscores, a text label to display the score, drop-downs to select keymap preferences, or checkboxes to specify multi-media options. Usually you solve these tasks by using Swing controls. Although it is possible to embed a <a href="/jme3/advanced/swing_canvas.html" class="wikilink1" title="jme3:advanced:swing_canvas">jME3 canvas</a> in a Swing <abbr title="Graphical User Interface">GUI</abbr>, a 3D game typically runs full-screen, or in a window of its own. 
</p>

<p>
This document introduces you to <a href="http://nifty-gui.lessvoid.com/" class="urlextern" title="http://nifty-gui.lessvoid.com/" rel="nofollow">Nifty GUI</a>, a Java library for building interactive graphical user interfaces (GUIs) for games or similar applications. Nifty <abbr title="Graphical User Interface">GUI</abbr> (the <code>de.lessvoid.nifty</code> package) is well integrated with jME3 through the <code>com.jme3.niftygui</code> package. You define the base <abbr title="Graphical User Interface">GUI</abbr> layout in XML, and control it dynamically from your Java code. The necessary JAR libraries are included in your jME3 download, you do not need to install anything extra. (Just make sure they are on the classpath.)
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://vimeo.com/25637085" class="urlextern" title="http://vimeo.com/25637085" rel="nofollow">Video demo of Nifty GUI 1.3</a> </div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "Creating JME3 User Interfaces with Nifty GUI" [1-1159] -->
<h2 class="sectionedit2" id="tutorial_overview">Tutorial Overview</h2>
<div class="level2">

<p>
Learn to add a Nifty <abbr title="Graphical User Interface">GUI</abbr> to your jME3 game by going through this multi-part tutorial:
</p>
<ol>
<li class="level1"><div class="li"> <span class="curid"><a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Understand the Nifty GUI Concepts</a></span> described on this page.</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_best_practices.html" class="wikilink1" title="jme3:advanced:nifty_gui_best_practices">Browse this short list of Best Practices</a></div>
</li>
<li class="level1"><div class="li"> Lay out your graphical user interface:</div>
<ul>
<li class="level2"><div class="li"> <a href="/jme3/advanced/nifty_gui_xml_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_xml_layout">Lay out the GUI in XML</a> – or –</div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_layout">Lay out the GUI in Java</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Integrate the <abbr title="Graphical User Interface">GUI</abbr> into the game:</div>
<ul>
<li class="level2"><div class="li"> <a href="/jme3/advanced/nifty_gui_overlay.html" class="wikilink1" title="jme3:advanced:nifty_gui_overlay">Overlay the User Interface Over the Screen</a>  – or –</div>
</li>
<li class="level2"><div class="li"> <a href="/jme3/advanced/nifty_gui_projection.html" class="wikilink1" title="jme3:advanced:nifty_gui_projection">Project the User Interface Onto a Texture</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Interact with the GUI from Java</a></div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Tutorial Overview" [1160-1952] -->
<h2 class="sectionedit3" id="must_knownifty_gui_concepts">Must Know: Nifty GUI Concepts</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-nifty-screen-layer-panel.png" class="media" title="jme3:advanced:nifty-screen-layer-panel.png"><img src="/resources/jme3-advanced-nifty-screen-layer-panel.png" class="media" alt="" /></a>
</p>

<p>
Nifty GUIs are made up of the following <strong>elements</strong>:
</p>
<ul>
<li class="level1"><div class="li"> A Nifty <abbr title="Graphical User Interface">GUI</abbr> contains one or more <strong>screens</strong>.</div>
<ul>
<li class="level2"><div class="li"> Only one screen is visible at a time.</div>
</li>
<li class="level2"><div class="li"> Name the first screen <code>start</code>. Name any others whatever you like.</div>
</li>
<li class="level2"><div class="li"> Screen are <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">controlled by a Java Controller class</a>.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> A screen contains one or more <strong>layers</strong>.</div>
<ul>
<li class="level2"><div class="li"> Layers are containers that impose alignment on their contents (vertical, horizontal, or centered)</div>
</li>
<li class="level2"><div class="li"> Layers can overlap (z-order), and cannot be nested.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> A layer contains <strong>panels</strong>.</div>
<ul>
<li class="level2"><div class="li"> Panels are containers that impose alignment on their contents (vertical, horizontal, or centered)</div>
</li>
<li class="level2"><div class="li"> Panels can be nested, and cannot overlap.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> A panel contains <strong>images, text, or controls (buttons, etc)</strong>.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Must Know: Nifty GUI Concepts" [1953-2830] -->
<h2 class="sectionedit4" id="resources">Resources</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_best_practices.html" class="wikilink1" title="jme3:advanced:nifty_gui_best_practices">Browse this short list of Best Practices before you start</a></div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Resources" [2831-2960] -->
<h3 class="sectionedit5" id="jme-nifty_sample_code">JME-Nifty Sample Code</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> XML examples</div>
<ul>
<li class="level2"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/test-data/Interface/Nifty/HelloJme.xml" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/test-data/Interface/Nifty/HelloJme.xml" rel="nofollow">HelloJme.xml</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Java examples</div>
<ul>
<li class="level2"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/niftygui/TestNiftyGui.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/niftygui/TestNiftyGui.java" rel="nofollow">TestNiftyGui.java</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/niftygui/TestNiftyToMesh.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/niftygui/TestNiftyToMesh.java" rel="nofollow">TestNiftyToMesh.java</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> jME3-ready version of the Nifty <abbr title="Graphical User Interface">GUI</abbr> 1.3 demo (sample code, Java)</div>
<ul>
<li class="level2"><div class="li"> <a href="http://files.seapegasus.org/NiftyGuiDemo.zip" class="urlextern" title="http://files.seapegasus.org/NiftyGuiDemo.zip" rel="nofollow">NiftyGuiDemo.zip</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Find more sample code in the <a href="http://nifty-gui.svn.sourceforge.net/viewvc/nifty-gui/nifty-default-controls-examples/trunk/" class="urlextern" title="http://nifty-gui.svn.sourceforge.net/viewvc/nifty-gui/nifty-default-controls-examples/trunk/" rel="nofollow">Nifty GUI source repository</a></div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "JME-Nifty Sample Code" [2961-3740] -->
<h3 class="sectionedit6" id="external_documentation">External Documentation</h3>
<div class="level3">

<p>
Learn more from the NiftyGUI page:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://sourceforge.net/projects/nifty-gui/files/nifty-gui/1.3.2/nifty-gui-the-manual-1.3.2.pdf/download" class="urlextern" title="http://sourceforge.net/projects/nifty-gui/files/nifty-gui/1.3.2/nifty-gui-the-manual-1.3.2.pdf/download" rel="nofollow">Nifty GUI - the Manual</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://nifty-gui.sourceforge.net/projects/1.3-SNAPSHOT/nifty/apidocs/index.html" class="urlextern" title="http://nifty-gui.sourceforge.net/projects/1.3-SNAPSHOT/nifty/apidocs/index.html" rel="nofollow">Nifty 1.3 JavaDoc</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://nifty-gui.sourceforge.net/projects/1.3-SNAPSHOT/nifty-default-controls/apidocs/" class="urlextern" title="http://nifty-gui.sourceforge.net/projects/1.3-SNAPSHOT/nifty-default-controls/apidocs/" rel="nofollow">Nifty 1.3 Controls JavaDoc</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/groups/gui/forum/topic/anyone-succeeded-in-changing-text-in-nifty-programatically/#post-109510" class="urlextern" title="http://jmonkeyengine.org/groups/gui/forum/topic/anyone-succeeded-in-changing-text-in-nifty-programatically/#post-109510" rel="nofollow">Forum post: Changing Text in Nifty GUIs programmatically</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:nifty_gui:editor" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:nifty_gui:editor" rel="nofollow">Official Nifty GUI Editor</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:nifty_gui:new_editor" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:nifty_gui:new_editor" rel="nofollow">New Nifty GUI Editor</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:nifty_gui:groovy" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:nifty_gui:groovy" rel="nofollow">Nifty GUI with Groovy</a></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "External Documentation" [3741-4677] -->
<h2 class="sectionedit7" id="next_steps">Next Steps</h2>
<div class="level2">

<p>
Now that you understand the concepts and know where to find more information, learn how to lay out a simple graphical user interface. Typically, you start doing this in XML.
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_xml_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_xml_layout">Lay out the GUI in XML</a> (recommended)</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_layout">Lay out the GUI in Java</a> (optional)</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_editor.html" class="wikilink1" title="jme3:advanced:nifty_gui_editor">Lay out the GUI in Editor</a> (experimental)</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Next Steps" [4678-5117] -->
<h2 class="sectionedit8" id="nifty_logging_nifty_131">Nifty Logging (Nifty 1.3.1)</h2>
<div class="level2">

<p>
If you want to disable the nifty log lines, add this code after you created nifty:
</p>
<pre class="code">Logger.getLogger("de.lessvoid.nifty").setLevel(Level.SEVERE); 
Logger.getLogger("NiftyInputEventHandlingLog").setLevel(Level.SEVERE); </pre>
<div class="tags"><span>
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/nifty.html" class="wikilink1" title="tag:nifty" rel="tag">nifty</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Nifty Logging (Nifty 1.3.1)" [5118-] -->
