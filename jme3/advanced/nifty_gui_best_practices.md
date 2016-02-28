---
title: Nifty GUI - Best Practices
---
<h1 class="sectionedit1" id="nifty_gui_-_best_practices">Nifty GUI - Best Practices</h1>
<div class="level1">

<p>
This page is a short list of best practices that you should know of when starting to use Nifty <abbr title="Graphical User Interface">GUI</abbr>. The JME3 tutorials focus on JME3-Nifty integration related details. You will find more features in the <a href="http://sourceforge.net/projects/nifty-gui/files/nifty-gui/nifty-gui-the-manual-v1.0.pdf/download" class="urlextern" title="http://sourceforge.net/projects/nifty-gui/files/nifty-gui/nifty-gui-the-manual-v1.0.pdf/download" rel="nofollow">Nifty GUI Manual</a>.
</p>
<ol>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI Concepts</a></div>
</li>
<li class="level1"><div class="li"> <strong>Nifty <abbr title="Graphical User Interface">GUI</abbr> Best Practices</strong></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_xml_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_xml_layout">Nifty GUI XML Layout</a> or <a href="/jme3/advanced/nifty_gui_java_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_layout">Nifty GUI Java Layout</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_overlay.html" class="wikilink1" title="jme3:advanced:nifty_gui_overlay">Nifty GUI Overlay</a> or <a href="/jme3/advanced/nifty_gui_projection.html" class="wikilink1" title="jme3:advanced:nifty_gui_projection">Nifty GUI Projection</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Nifty GUI Java Interaction</a></div>
</li>
</ol>

</div>
<!-- EDIT1 SECTION "Nifty GUI - Best Practices" [1-673] -->
<h2 class="sectionedit2" id="xml_or_java">XML or Java?</h2>
<div class="level2">

<p>
You can build Nifty GUIs using XML or Java syntax. Which one should you choose? The XML and Java syntax are equivalent, so is it an either-or choice? Not quite. You typically use XML and Java together.
</p>
<ul>
<li class="level1"><div class="li"> Build your basic static UI layout using XML - it's cleaner to write and read. </div>
</li>
<li class="level1"><div class="li"> Use Java syntax to control the dynamic parts of the <abbr title="Graphical User Interface">GUI</abbr> at runtime - it's easier to interact with object-oriented code.</div>
</li>
<li class="level1"><div class="li"> <strong>Example:</strong> You design two UIs with slightly different XML layouts for mobile and desktop. If you use the same IDs for equivalent elements, your dynamic Java code works the same no matter which of the two base XML layout you use it on. This allows you to switch between a phone and a desktop UI by simply swapping one base XML file. </div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "XML or Java?" [674-1450] -->
<h2 class="sectionedit3" id="edit_and_preview_xml_in_the_sdk">Edit and Preview XML in the SDK</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Use the <a href="/sdk.html" class="wikilink1" title="sdk">jMonkeyEngine SDK</a> New File wizard to create a new XML file (from the <abbr title="Graphical User Interface">GUI</abbr> category, “Empty Nifty File”). </div>
</li>
<li class="level1"><div class="li"> The <a href="/sdk.html" class="wikilink1" title="sdk">jMonkeyEngine SDK</a> includes an XML editor and a special previewer for Nifty <abbr title="Graphical User Interface">GUI</abbr> files. </div>
</li>
<li class="level1"><div class="li"> When you open an XML file, you can switch between XML Editor and <abbr title="Graphical User Interface">GUI</abbr> Preview mode.</div>
</li>
</ul>

<p>
Tip: The <abbr title="Graphical User Interface">GUI</abbr> category in the New File wizard also contains Nifty code samples.
</p>

</div>
<!-- EDIT3 SECTION "Edit and Preview XML in the SDK" [1451-1893] -->
<h2 class="sectionedit4" id="validate_the_xml_before_loading">Validate the XML before loading</h2>
<div class="level2">

<p>
The <a href="http://nifty-gui.sourceforge.net/projects/nifty/apidocs/de/lessvoid/nifty/Nifty.html" class="urlextern" title="http://nifty-gui.sourceforge.net/projects/nifty/apidocs/de/lessvoid/nifty/Nifty.html" rel="nofollow">Nifty class</a> has <em>validateXml()</em> method that takes the same input XML argument as <em>fromXml()</em>. Nifty does not validate the Xml by default, and will blow up in surprising ways if your XML does not conform to the schema. Adding the validation step will save you debugging time. You can validate right before loading, or in your unit tests. 
</p>

</div>
<!-- EDIT4 SECTION "Validate the XML before loading" [1894-2374] -->
<h2 class="sectionedit5" id="use_code_completion">Use Code Completion</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Include the following XML schema in the first line of your NiftyGUI XML files<pre class="code xml"><span class="sc3"><span class="re1">&lt;?xml</span> <span class="re0">version</span>=<span class="st0">"1.0"</span> <span class="re0">encoding</span>=<span class="st0">"UTF-8"</span><span class="re2">?&gt;</span></span>
<span class="sc3"><span class="re1">&lt;nifty</span> <span class="re0">xmlns</span>=<span class="st0">"http://nifty-gui.sourceforge.net/nifty-1.3.xsd"</span> <span class="re0">xmlns:xsi</span>=<span class="st0">"http://www.w3.org/2001/XMLSchema-instance"</span></span>
<span class="sc3">       <span class="re0">xsi:schemaLocation</span>=<span class="st0">"http://nifty-gui.sourceforge.net/nifty-1.3.xsd http://nifty-gui.sourceforge.net/nifty-1.3.xsd"</span><span class="re2">&gt;</span></span>
     <span class="sc-1">&lt;!-- Your IDE now tells you that one &lt;screen&gt;&lt;/screen&gt; element is expected here, etc. --&gt;</span>
<span class="sc3"><span class="re1">&lt;/nifty<span class="re2">&gt;</span></span></span></pre>
</div>
</li>
<li class="level1"><div class="li"> Now your IDE (including the jMonkeyEngine SDK) will display extra info and do code completion for the Nifty <abbr title="Graphical User Interface">GUI</abbr> <abbr title="Application Programming Interface">API</abbr>.</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Use Code Completion" [2375-3011] -->
<h2 class="sectionedit6" id="use_the_id_string_right">Use the ID String Right</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> If you want to interact with an element, give it an ID (String). </div>
</li>
<li class="level1"><div class="li"> Use transparent ID-less panels as anonymous spacers.</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Use the ID String Right" [3012-3176] -->
<h2 class="sectionedit7" id="sizing_layers_and_panels">Sizing Layers and Panels</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Specify widths and heights in percent to allow the <abbr title="Graphical User Interface">GUI</abbr> to scale.</div>
</li>
<li class="level1"><div class="li"> Use <code>*</code> instead of a fixed value to make the element fill the remaining space automatically.</div>
</li>
<li class="level1"><div class="li"> Be cautious when specifying fixed sizes, and test the outcome in various resolutions.</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Sizing Layers and Panels" [3177-3473] -->
<h2 class="sectionedit8" id="colorcode_for_clarity">Colorcode for Clarity</h2>
<div class="level2">

<p>
Screens, layers, and panels…
</p>
<ul>
<li class="level1"><div class="li"> … can have an RGBA background color. <br />
You can use temporary colors during the design phase to highlight which container is which.</div>
</li>
<li class="level1"><div class="li"> … can be transparent. <br />
In the finished <abbr title="Graphical User Interface">GUI</abbr>, screens, layers, and panels are typically transparent; the visible elements are the images, text fields, and controls, inside the panels.</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">During development (and during a tutorial), the following debug code makes all panels visible. This helps you arrange them and find errors. 

<pre class="code java">nifty.<span class="me1">setDebugOptionPanelColors</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Before the release, and during testing, set the debug view to false again.
</p></div>


</div>
<!-- EDIT8 SECTION "Colorcode for Clarity" [3474-] -->
