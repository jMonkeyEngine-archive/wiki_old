---
title: Laying out the GUI in XML
---
<h1 class="sectionedit1" id="laying_out_the_gui_in_xml">Laying out the GUI in XML</h1>
<div class="level1">
<ol>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI Concepts</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_best_practices.html" class="wikilink1" title="jme3:advanced:nifty_gui_best_practices">Nifty GUI Best Practices</a></div>
</li>
<li class="level1"><div class="li"> <strong>Nifty <abbr title="Graphical User Interface">GUI</abbr> XML Layout</strong> or <a href="/jme3/advanced/nifty_gui_java_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_layout">Nifty GUI Java Layout</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_overlay.html" class="wikilink1" title="jme3:advanced:nifty_gui_overlay">Nifty GUI Overlay</a> or <a href="/jme3/advanced/nifty_gui_projection.html" class="wikilink1" title="jme3:advanced:nifty_gui_projection">Nifty GUI Projection</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Interact with the GUI from Java</a></div>
</li>
</ol>

<p>
You can “draw” the <abbr title="Graphical User Interface">GUI</abbr> to the screen by writing XML code (alternatively you can also use Java).
</p>

</div>
<!-- EDIT1 SECTION "Laying out the GUI in XML" [1-478] -->
<h2 class="sectionedit2" id="plan_your_gui_layout">Plan Your GUI Layout</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-gui-layout-draft.png" class="media" title="jme3:advanced:gui-layout-draft.png"><img src="/resources/jme3-advanced-gui-layout-draft.png" class="mediaright" alt="" /></a>
</p>

<p>
In this tutorial, you want to create two game screens: An out-of-game StartScreen that the players see before the game starts; and an in-game <a href="http://en.wikipedia.org/wiki/HUD_%28video_gaming%29" class="urlextern" title="http://en.wikipedia.org/wiki/HUD_%28video_gaming%29" rel="nofollow">HUD</a> that displays info during the game. Before writing code, you plan the <abbr title="Graphical User Interface">GUI</abbr> layout, either on paper or in a graphic application.
</p>

<p>
The StartScreen contains:
</p>
<ul>
<li class="level1"><div class="li"> The background layer has a centered layout and contains an image.</div>
</li>
<li class="level1"><div class="li"> The top layer has a vertical layout, containing 3 panels: </div>
<ul>
<li class="level2"><div class="li"> The top panel contains a label with the game title, </div>
</li>
<li class="level2"><div class="li"> The middle panel contains a text field with the game description. </div>
</li>
<li class="level2"><div class="li"> The bottom panel has a horizontal layout and contains two more panels:</div>
<ul>
<li class="level3"><div class="li"> The left panel contains a Start button.</div>
</li>
<li class="level3"><div class="li"> The right panel contains a Quit button.</div>
</li>
</ul>
</li>
</ul>
</li>
</ul>

<p>
The HUD contains:
</p>
<ul>
<li class="level1"><div class="li"> The background layer has a centered layout, and contains the partially transparent HUD image.</div>
</li>
<li class="level1"><div class="li"> The top layer has a horizontal layout, containing 2 panels: </div>
<ul>
<li class="level2"><div class="li"> The left panel as transparent spacer.</div>
</li>
<li class="level2"><div class="li"> The right panel has a vertical layout containing 2 panels, a label and an image.</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Plan Your GUI Layout" [479-1663] -->
<h2 class="sectionedit3" id="implement_your_gui_layout">Implement Your GUI Layout</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-nifty-screen-layer-panel.png" class="media" title="jme3:advanced:nifty-screen-layer-panel.png"><img src="/resources/jme3-advanced-nifty-screen-layer-panel.png" class="mediaright" alt="" width="366" height="136" /></a>
</p>

<p>
Create an empty <strong>screen</strong>.xml file in the <code>assets/Interface/</code> directory of your project. ( Rightclick on Interface → New → Other… → <abbr title="Graphical User Interface">GUI</abbr> → Empty NiftyGui file)
Afterwards create the directory <code>assets/Interface/Fonts</code> and add a new font e.g. Arial. ( <strong>Rightclick on Interface → New → Other… →</strong> Other → Folder and <abbr title="Graphical User Interface">GUI</abbr> → Font)
</p>

<p>
One XML file can contain several, or even all screens. As a reminder: Nifty displays one screen at a time; a screen contains several layers on top of one another; each layer contains panels that are embedded into another; the panels contain the actual content (text, images, or controls).
</p>

</div>
<!-- EDIT3 SECTION "Implement Your GUI Layout" [1664-2394] -->
<h3 class="sectionedit4" id="make_screens">Make Screens</h3>
<div class="level3">

<p>
The following minimal XML file contains a start screen and a HUD screen. (Neither has been defined yet.)
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;?xml</span> <span class="re0">version</span>=<span class="st0">"1.0"</span> <span class="re0">encoding</span>=<span class="st0">"UTF-8"</span><span class="re2">?&gt;</span></span>
<span class="sc3"><span class="re1">&lt;nifty</span> <span class="re0">xmlns</span>=<span class="st0">"http://nifty-gui.sourceforge.net/nifty-1.3.xsd"</span> <span class="re0">xmlns:xsi</span>=<span class="st0">"http://www.w3.org/2001/XMLSchema-instance"</span> <span class="re0">xsi:schemaLocation</span>=<span class="st0">"http://nifty-gui.sourceforge.net/nifty-1.3.xsd http://nifty-gui.sourceforge.net/nifty-1.3.xsd"</span><span class="re2">&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"start"</span><span class="re2">&gt;</span></span>
    <span class="sc-1">&lt;!-- ... --&gt;</span>
  <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"hud"</span><span class="re2">&gt;</span></span>
    <span class="sc-1">&lt;!-- ... --&gt;</span>
  <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
<span class="sc3"><span class="re1">&lt;/nifty<span class="re2">&gt;</span></span></span></pre>

<p>
Every Nifty <abbr title="Graphical User Interface">GUI</abbr> must have a start screen. The others (in this example, the HUD screen) are optional. 
</p>

<p>
<strong>Note:</strong> In the following examples, the XML schema header is abbreviated to just <code>&lt;nifty&gt;</code>.
</p>

</div>
<!-- EDIT4 SECTION "Make Screens" [2395-3123] -->
<h3 class="sectionedit5" id="make_layers">Make Layers</h3>
<div class="level3">

<p>
The following minimal XML file shows how we added layers to the start screen and HUD screen.
Delete all from the file and add following code:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;nifty<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"start"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"background"</span> <span class="re0">backgroundColor</span>=<span class="st0">"#000f"</span><span class="re2">&gt;</span></span>
      <span class="sc-1">&lt;!-- ... --&gt;</span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"foreground"</span> <span class="re0">backgroundColor</span>=<span class="st0">"#0000"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span><span class="re2">&gt;</span></span>
      <span class="sc-1">&lt;!-- ... --&gt;</span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"hud"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"background"</span> <span class="re0">backgroundColor</span>=<span class="st0">"#000f"</span><span class="re2">&gt;</span></span>
      <span class="sc-1">&lt;!-- ... --&gt;</span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"foreground"</span> <span class="re0">backgroundColor</span>=<span class="st0">"#0000"</span> <span class="re0">childLayout</span>=<span class="st0">"horizontal"</span><span class="re2">&gt;</span></span>
      <span class="sc-1">&lt;!-- ... --&gt;</span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
<span class="sc3"><span class="re1">&lt;/nifty<span class="re2">&gt;</span></span></span></pre>

<p>
In a layer, you can now add panels and arrange them. Panels are containers that mark the areas where you want to display text, images, or controls (buttons etc) later. 
</p>

</div>
<!-- EDIT5 SECTION "Make Layers" [3124-3946] -->
<h3 class="sectionedit6" id="make_panels">Make Panels</h3>
<div class="level3">

<p>
A panel is the inner-most container (that will contain the actual content: text, images, or controls). You place panels inside layers. The following panels go into in the <code>start</code> screen's <code>foreground</code> layer:
</p>
<pre class="code xml">      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top"</span> <span class="re0">height</span>=<span class="st0">"25%"</span> <span class="re0">width</span>=<span class="st0">"75%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span></span>
<span class="sc3">             <span class="re0">backgroundColor</span>=<span class="st0">"#f008"</span><span class="re2">&gt;</span></span>  
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_mid"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"75%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span></span>
<span class="sc3">             <span class="re0">backgroundColor</span>=<span class="st0">"#0f08"</span><span class="re2">&gt;</span></span>  
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom"</span> <span class="re0">height</span>=<span class="st0">"25%"</span> <span class="re0">width</span>=<span class="st0">"75%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"horizontal"</span></span>
<span class="sc3">             <span class="re0">backgroundColor</span>=<span class="st0">"#00f8"</span><span class="re2">&gt;</span></span>  
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom_left"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span> </span>
<span class="sc3">             <span class="re0">backgroundColor</span>=<span class="st0">"#44f8"</span><span class="re2">&gt;</span></span>  
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom_right"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span></span>
<span class="sc3">             <span class="re0">backgroundColor</span>=<span class="st0">"#88f8"</span><span class="re2">&gt;</span></span>  
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
The following panels go into in the <code>hud</code> screen's <code>foreground</code> layer:
</p>
<pre class="code xml">      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_left"</span> <span class="re0">width</span>=<span class="st0">"80%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span> </span>
<span class="sc3">      <span class="re0">backgroundColor</span>=<span class="st0">"#0f08"</span><span class="re2">&gt;</span></span>  
        <span class="sc-1">&lt;!-- spacer --&gt;</span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_right"</span> <span class="re0">width</span>=<span class="st0">"20%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span> </span>
<span class="sc3">      <span class="re0">backgroundColor</span>=<span class="st0">"#00f8"</span> <span class="re2">&gt;</span></span>  
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top_right1"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"15%"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span></span>
<span class="sc3">             <span class="re0">backgroundColor</span>=<span class="st0">"#00f8"</span><span class="re2">&gt;</span></span>  
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top_right2"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"15%"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span></span>
<span class="sc3">             <span class="re0">backgroundColor</span>=<span class="st0">"#44f8"</span><span class="re2">&gt;</span></span>  
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bot_right"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"70%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span></span>
<span class="sc3">             <span class="re0">backgroundColor</span>=<span class="st0">"#88f8"</span><span class="re2">&gt;</span></span>  
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
The result should look as follows:
</p>

<p>
<a href="/resources/jme3-advanced-nifty-gui-panels.png" class="media" title="jme3:advanced:nifty-gui-panels.png"><img src="/resources/jme3-advanced-nifty-gui-panels.png" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT6 SECTION "Make Panels" [3947-5829] -->
<h2 class="sectionedit7" id="adding_content_to_panels">Adding Content to Panels</h2>
<div class="level2">

<p>
See also <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Layout_Introduction" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Layout_Introduction" rel="nofollow">Layout Introduction</a> on the Nifty <abbr title="Graphical User Interface">GUI</abbr> site.
</p>

</div>
<!-- EDIT7 SECTION "Adding Content to Panels" [5830-6008] -->
<h3 class="sectionedit8" id="add_images">Add Images</h3>
<div class="level3">

<p>
The <a href="http://hub.jmonkeyengine.org/wiki/lib/exe/fetch.php/jme3:advanced:start-background.png" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/lib/exe/fetch.php/jme3:advanced:start-background.png" rel="nofollow">start-background.png</a> image is a fullscreen background picture. Add it to <code>Interface</code>. In the <code>start</code> screen, add the following image element:
</p>
<pre class="code xml">    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"background"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/start-background.png"</span><span class="re2">&gt;</span><span class="re1">&lt;/image<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span></pre>

<p>
The <a href="http://hub.jmonkeyengine.org/wiki/lib/exe/fetch.php/jme3:advanced:hud-frame.png" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/lib/exe/fetch.php/jme3:advanced:hud-frame.png" rel="nofollow">hud-frame.png</a> image is a transparent frame that we use as HUD decoration. Add it to <code>Interface</code>. In the <code>hud</code> screen, add the following image element:
</p>
<pre class="code xml">    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"background"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/hud-frame.png"</span><span class="re2">&gt;</span><span class="re1">&lt;/image<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span></pre>

<p>
In order to make the hud-frame.png independent of the screen resolution you are using, you could use the <code>imageMode</code> attribute on the image element <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Resizable_Images_(ImageMode%3Dresize)_explained" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Resizable_Images_(ImageMode%3Dresize)_explained" rel="nofollow"> Resizable Images (ImageMode=resize) explained</a>
</p>
<pre class="code xml">    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"background"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/hud-frame.png"</span> <span class="re0">imageMode</span>=<span class="st0">"resize:40,490,110,170,40,560,40,270,40,560,40,40"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span></pre>

<p>
The <a href="http://hub.jmonkeyengine.org/wiki/lib/exe/fetch.php/jme3:advanced:face1.png" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/lib/exe/fetch.php/jme3:advanced:face1.png" rel="nofollow">face1.png</a> image is an image that you want to use as a status icon. Add it to <code>Interface</code>.
In the <code>hud</code> screen's <code>foreground</code> layer, add the following image element:
</p>
<pre class="code xml">        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top_right2"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"15%"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/face1.png"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"30%"</span> <span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/image<span class="re2">&gt;</span></span></span>  
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
This image is scaled to use 50% of the height and 30% of the width of its container.
</p>

</div>
<!-- EDIT8 SECTION "Add Images" [6009-7930] -->
<h3 class="sectionedit9" id="add_static_text">Add Static Text</h3>
<div class="level3">

<p>
The game title is a typical example of static text. In the <code>start</code> screen, add the following text element:
</p>
<pre class="code xml">      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top"</span> <span class="re0">height</span>=<span class="st0">"25%"</span> <span class="re0">width</span>=<span class="st0">"75%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>  
          <span class="sc3"><span class="re1">&lt;text</span> <span class="re0">text</span>=<span class="st0">"My Cool Game"</span> <span class="re0">font</span>=<span class="st0">"Interface/Fonts/Default.fnt"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re2">/&gt;</span></span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
For longer pieces of static text, such as an introduction, you can use wrap=“true”. Add the following text element to the <code>Start screen</code>:
</p>
<pre class="code xml">      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_mid"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"75%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>       
        <span class="sc3"><span class="re1">&lt;text</span> <span class="re0">text</span>=<span class="st0">"Here goes some text describing the game and the rules and stuff. Incidentally, </span>
<span class="sc3">         the text is quite long and needs to wrap at the end of lines. ..."</span> </span>
<span class="sc3">        <span class="re0">font</span>=<span class="st0">"Interface/Fonts/Default.fnt"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re0">wrap</span>=<span class="st0">"true"</span> <span class="re2">/&gt;</span></span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
The font used is jME3's default font “Interface/Fonts/Default.fnt” which is included in the jMonkeyEngine.JAR. You can add your own fonts to your own <code>assets/Interface/Fonts</code> directory.
Adjust the path to your font-name.
</p>

</div>
<!-- EDIT9 SECTION "Add Static Text" [7931-9052] -->
<h3 class="sectionedit10" id="add_controls">Add Controls</h3>
<div class="level3">

<p>
Before you can use any control, you must load a Control Definition first. Add the following two lines <em>before</em> your screen definitions:
</p>
<pre class="code xml">  <span class="sc3"><span class="re1">&lt;useStyles</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-styles.xml"</span> <span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;useControls</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-controls.xml"</span> <span class="re2">/&gt;</span></span></pre>

<p>
Note that the useStyles tag must be the first child of the nifty tag, otherwise you will see an error in design view.
</p>

</div>

<h4 id="label_control">Label Control</h4>
<div class="level4">

<p>
Use label controls for text that you want to edit dynamically from Java. One example for this is the score display.
In the <code>hud</code> screen's <code>foreground</code> layer, add the following text element:
</p>
<pre class="code xml">        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top_right"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re0">width</span>=<span class="st0">"15%"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>  
            <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"label"</span> <span class="re0">color</span>=<span class="st0">"#000"</span> <span class="re0">text</span>=<span class="st0">"123"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re2">/&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
Note that the width and height do not scale the bitmap font, but indirectly make certain it is centered. If you want a different size for the font, you need to provide an extra bitmap font (they come with fixed sizes and don't scale well).
</p>

</div>

<h4 id="button_control">Button Control</h4>
<div class="level4">

<p>
Our <abbr title="Graphical User Interface">GUI</abbr> plan asks for two buttons on the start screen. You add the Start and Quit buttons to the bottom panel of the <code>start</code> screen using the <code>&lt;control&gt;</code> element:
</p>
<pre class="code xml">        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom_left"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>  
          <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"button"</span> <span class="re0">label</span>=<span class="st0">"Start"</span> <span class="re0">id</span>=<span class="st0">"StartButton"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span> 
          <span class="sc3"><span class="re1">&lt;/control<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom_right"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>  
          <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"button"</span> <span class="re0">label</span>=<span class="st0">"Quit"</span> <span class="re0">id</span>=<span class="st0">"QuitButton"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span> 
          <span class="sc3"><span class="re1">&lt;/control<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
Note that these controls don't do anything yet – we'll get to that soon.
</p>

<p>
Now remove all <strong>backgroundColor=““</strong> tags from your code. They were only needed to show the layout.
</p>

<p>
Your screen.xml should look like this:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;?xml</span> <span class="re0">version</span>=<span class="st0">"1.0"</span> <span class="re0">encoding</span>=<span class="st0">"UTF-8"</span><span class="re2">?&gt;</span></span>
<span class="sc3"><span class="re1">&lt;nifty</span> <span class="re0">xmlns</span>=<span class="st0">"http://nifty-gui.sourceforge.net/nifty-1.3.xsd"</span> <span class="re0">xmlns:xsi</span>=<span class="st0">"http://www.w3.org/2001/XMLSchema-instance"</span> <span class="re0">xsi:schemaLocation</span>=<span class="st0">"http://nifty-gui.sourceforge.net/nifty-1.3.xsd http://nifty-gui.sourceforge.net/nifty-1.3.xsd"</span><span class="re2">&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;useStyles</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-styles.xml"</span> <span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;useControls</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-controls.xml"</span> <span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"start"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"background"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
      <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/start-background.png"</span><span class="re2">&gt;</span><span class="re1">&lt;/image<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"foreground"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span><span class="re2">&gt;</span></span>
      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top"</span> <span class="re0">height</span>=<span class="st0">"25%"</span> <span class="re0">width</span>=<span class="st0">"75%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;text</span> <span class="re0">text</span>=<span class="st0">"My Cool Game"</span> <span class="re0">font</span>=<span class="st0">"Interface/Fonts/Default.fnt"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re2">/&gt;</span></span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_mid"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"75%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;text</span> <span class="re0">text</span>=<span class="st0">"Here goes some text describing the game and the rules and stuff. Incidentally, the text is quite long and needs to wrap at the end of lines. ..."</span> <span class="re0">font</span>=<span class="st0">"Interface/Fonts/Default.fnt"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re0">wrap</span>=<span class="st0">"true"</span> <span class="re2">/&gt;</span></span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom"</span> <span class="re0">height</span>=<span class="st0">"25%"</span> <span class="re0">width</span>=<span class="st0">"75%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"horizontal"</span> <span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom_left"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
          <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"button"</span> <span class="re0">label</span>=<span class="st0">"Start"</span> <span class="re0">id</span>=<span class="st0">"StartButton"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span><span class="re2">&gt;</span><span class="re1">&lt;/control<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom_right"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
          <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"button"</span> <span class="re0">label</span>=<span class="st0">"Quit"</span> <span class="re0">id</span>=<span class="st0">"QuitButton"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span><span class="re2">&gt;</span><span class="re1">&lt;/control<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"hud"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"background"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
      <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/hud-frame.png"</span><span class="re2">&gt;</span><span class="re1">&lt;/image<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"foreground"</span> <span class="re0">childLayout</span>=<span class="st0">"horizontal"</span><span class="re2">&gt;</span></span>
      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_left"</span> <span class="re0">width</span>=<span class="st0">"80%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span> <span class="re2">&gt;</span><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_right"</span> <span class="re0">width</span>=<span class="st0">"20%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top_right1"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"15%"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
          <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"label"</span> <span class="re0">color</span>=<span class="st0">"#000"</span> <span class="re0">text</span>=<span class="st0">"123"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re2">/&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_top_right2"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"15%"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
          <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/face1.png"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"30%"</span> <span class="re2">&gt;</span><span class="re1">&lt;/image<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bot_right"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"70%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re2">&gt;</span><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
      <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
<span class="sc3"><span class="re1">&lt;/nifty<span class="re2">&gt;</span></span></span></pre>

</div>

<h4 id="other_controls">Other Controls</h4>
<div class="level4">

<p>
Nifty additionally offers many customizable controls such as check boxes, text fields, menus, chats, tabs, … See also <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Elements" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Elements" rel="nofollow">Elements</a> on the Nifty <abbr title="Graphical User Interface">GUI</abbr> site.
</p>

</div>
<!-- EDIT10 SECTION "Add Controls" [9053-13918] -->
<h2 class="sectionedit11" id="intermediate_result">Intermediate Result</h2>
<div class="level2">

<p>
When you preview this code in the jMonkeyEngine SDK, our tutorial demo should looks as follows: A start screen with two buttons, and a game screen with a simple HUD frame and a blue cube (which stands for any jME3 game content).
</p>

<p>
<a href="/resources/jme3-advanced-nifty-gui-simple-demo.png" class="media" title="jme3:advanced:nifty-gui-simple-demo.png"><img src="/resources/jme3-advanced-nifty-gui-simple-demo.png" class="mediacenter" alt="" /></a>
</p>

<p>
Compare this result with the layout draft above.
</p>

</div>
<!-- EDIT11 SECTION "Intermediate Result" [13919-14279] -->
<h2 class="sectionedit12" id="next_steps">Next Steps</h2>
<div class="level2">

<p>
Integrate the <abbr title="Graphical User Interface">GUI</abbr> into the game. Typically, you will overlay the <abbr title="Graphical User Interface">GUI</abbr>.
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_overlay.html" class="wikilink1" title="jme3:advanced:nifty_gui_overlay">Nifty GUI Overlay</a> (recommended)</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_projection.html" class="wikilink1" title="jme3:advanced:nifty_gui_projection">Nifty GUI Projection</a> (optional)</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/nifty.html" class="wikilink1" title="tag:nifty" rel="tag">nifty</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>
</span></div>

</div>
<!-- EDIT12 SECTION "Next Steps" [14280-] -->
