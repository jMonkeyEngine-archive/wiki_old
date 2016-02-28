---
title: Laying Out the GUI in Java
---
<h1 class="sectionedit1" id="laying_out_the_gui_in_java">Laying Out the GUI in Java</h1>
<div class="level1">
<ol>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI Concepts</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_best_practices.html" class="wikilink1" title="jme3:advanced:nifty_gui_best_practices">Nifty GUI Best Practices</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_xml_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_xml_layout">Nifty GUI XML Layout</a> or <strong>Nifty <abbr title="Graphical User Interface">GUI</abbr> Java Layout</strong></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_overlay.html" class="wikilink1" title="jme3:advanced:nifty_gui_overlay">Nifty GUI Overlay</a> or <a href="/jme3/advanced/nifty_gui_projection.html" class="wikilink1" title="jme3:advanced:nifty_gui_projection">Nifty GUI Projection</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_java_interaction.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_interaction">Interact with the GUI from Java</a></div>
</li>
</ol>

<p>
<strong>Work in progress</strong> You can “draw” the <abbr title="Graphical User Interface">GUI</abbr> to the screen by writing Java code – alternatively to using XML. Typically you lay out the static base <abbr title="Graphical User Interface">GUI</abbr> in XML, and use Java commands if you need to change the <abbr title="Graphical User Interface">GUI</abbr> dynamically at runtime. In theory, you can also lay out the whole <abbr title="Graphical User Interface">GUI</abbr> in Java (but we don't cover that here).
</p>

</div>
<!-- EDIT1 SECTION "Laying Out the GUI in Java" [1-690] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
Sample project
</p>
<ul>
<li class="level1"><div class="li"> <strong>Original Source Code:</strong> <a href="http://nifty-gui.svn.sourceforge.net/viewvc/nifty-gui/nifty-default-controls-examples/trunk/src/main/java/de/lessvoid/nifty/examples/" class="urlextern" title="http://nifty-gui.svn.sourceforge.net/viewvc/nifty-gui/nifty-default-controls-examples/trunk/src/main/java/de/lessvoid/nifty/examples/" rel="nofollow">/nifty-default-controls-examples/trunk/src/main/java/de/lessvoid/nifty/examples/</a>. <br />
</div>
</li>
<li class="level1"><div class="li"> <strong>Download demo project:</strong> <a href="http://files.seapegasus.org/NiftyGuiDemo.zip" class="urlextern" title="http://files.seapegasus.org/NiftyGuiDemo.zip" rel="nofollow">http://files.seapegasus.org/NiftyGuiDemo.zip</a> (jme3-ready) <br />
The full demo ZIP is based on <code>de.lessvoid.nifty.examples.controls.ControlsDemo.java</code>.</div>
<ol>
<li class="level2"><div class="li"> The demo is a SimpleApplication-based game (use e.g. the BasicGame template in the jMonkeyEngine SDK).</div>
</li>
<li class="level2"><div class="li"> Copy images and sound files into your project's <code>assets/Interface/</code> directory. (In this example, I copied them from <code>nifty-default-controls-examples/trunk/src/main/resources/</code> to <code>assets/Interface/</code>).</div>
</li>
<li class="level2"><div class="li"> Make sure to use paths relative to your project's <code>assets/</code> directory.</div>
<ul>
<li class="level3"><div class="li"> E.g. for .fnt/.png/.jpg files use <code>filename(“Interface/yang.png”);</code> ( not <code>filename(“yang.png”);</code>).</div>
</li>
<li class="level3"><div class="li"> E.g. for .wav/.ogg files use <code>filename(“Interface/sounds/gong.wav”);</code> (not <code>filename(“sounds/gong.wav”);</code>).</div>
</li>
</ul>
</li>
</ol>
</li>
</ul>

<p>
Just so you get a quick picture what Nifty <abbr title="Graphical User Interface">GUI</abbr>'s Java Syntax looks like, here is the most basic example. It creates a screen with a layer and a panel that contains a button. 
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">mygame</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.niftygui.NiftyJmeDisplay</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.Nifty</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.builder.ScreenBuilder</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.builder.LayerBuilder</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.builder.PanelBuilder</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.controls.button.builder.ButtonBuilder</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.screen.DefaultScreenController</span><span class="sy0">;</span>
 
<span class="co3">/**
 * @author iamcreasy  
*/</span>
<span class="kw1">public</span> <span class="kw1">class</span> Main <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        Main app <span class="sy0">=</span> <span class="kw1">new</span> Main<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    NiftyJmeDisplay niftyDisplay <span class="sy0">=</span> <span class="kw1">new</span> NiftyJmeDisplay<span class="br0">(</span>
            assetManager, inputManager, audioRenderer, guiViewPort<span class="br0">)</span><span class="sy0">;</span>
    Nifty nifty <span class="sy0">=</span> niftyDisplay.<span class="me1">getNifty</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    guiViewPort.<span class="me1">addProcessor</span><span class="br0">(</span>niftyDisplay<span class="br0">)</span><span class="sy0">;</span>
    flyCam.<span class="me1">setDragToRotate</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
 
    nifty.<span class="me1">loadStyleFile</span><span class="br0">(</span><span class="st0">"nifty-default-styles.xml"</span><span class="br0">)</span><span class="sy0">;</span>
    nifty.<span class="me1">loadControlFile</span><span class="br0">(</span><span class="st0">"nifty-default-controls.xml"</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co1">// &lt;screen&gt;</span>
    nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"Screen_ID"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"Hello Nifty Screen"</span><span class="br0">)</span><span class="br0">{</span><span class="br0">{</span>
        controller<span class="br0">(</span><span class="kw1">new</span> DefaultScreenController<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Screen properties       </span>
 
        <span class="co1">// &lt;layer&gt;</span>
        layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"Layer_ID"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
            childLayoutVertical<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// layer properties, add more...</span>
 
            <span class="co1">// &lt;panel&gt;</span>
            panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"Panel_ID"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
               childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// panel properties, add more...               </span>
 
                <span class="co1">// GUI elements</span>
                control<span class="br0">(</span><span class="kw1">new</span> ButtonBuilder<span class="br0">(</span><span class="st0">"Button_ID"</span>, <span class="st0">"Hello Nifty"</span><span class="br0">)</span><span class="br0">{</span><span class="br0">{</span>
                    alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"5%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"15%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
                <span class="co1">//.. add more GUI elements here              </span>
 
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co1">// &lt;/panel&gt;</span>
          <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// &lt;/layer&gt;</span>
      <span class="br0">}</span><span class="br0">}</span>.<span class="me1">build</span><span class="br0">(</span>nifty<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">// &lt;/screen&gt;</span>
 
    nifty.<span class="me1">gotoScreen</span><span class="br0">(</span><span class="st0">"Screen_ID"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// start the screen</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "Sample Code" [691-3958] -->
<h2 class="sectionedit3" id="implement_your_gui_layout">Implement Your GUI Layout</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-gui-layout-draft.png" class="media" title="jme3:advanced:gui-layout-draft.png"><img src="/resources/jme3-advanced-gui-layout-draft.png" class="mediaright" alt="" /></a>
</p>

<p>
In this tutorial, you recreate the same screen as in the Nifty <abbr title="Graphical User Interface">GUI</abbr> XML example.
</p>

<p>
Create an Screen.Java file in the <code>assets/Interfaces/</code> directory of your project. One Java file can contain several, or even all screens. As a reminder: Nifty displays one screen at a time; a screen contains several layers on top of one another; each layer contains panels that are embedded into another; the panels contain the actual content (text, images, or controls).
</p>

</div>
<!-- EDIT3 SECTION "Implement Your GUI Layout" [3959-4495] -->
<h3 class="sectionedit4" id="make_screens">Make Screens</h3>
<div class="level3">

<p>
The following minimal Java file contains a start screen and a HUD screen. (Neither has been defined yet.)
</p>
<pre class="code java">nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"start"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"start"</span><span class="br0">)</span><span class="br0">{</span><span class="br0">{</span>
    controller<span class="br0">(</span><span class="kw1">new</span> DefaultScreenController<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">// &lt;!-- ... --&gt;</span>
  <span class="br0">}</span><span class="br0">}</span>.<span class="me1">build</span><span class="br0">(</span>nifty<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"hud"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"hud"</span><span class="br0">)</span><span class="br0">{</span><span class="br0">{</span>
    controller<span class="br0">(</span><span class="kw1">new</span> DefaultScreenController<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">// &lt;!-- ... --&gt;</span>
  <span class="br0">}</span><span class="br0">}</span>.<span class="me1">build</span><span class="br0">(</span>nifty<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Every Nifty <abbr title="Graphical User Interface">GUI</abbr> must have a start screen. The others (in this example, the HUD screen) are optional. 
</p>

</div>
<!-- EDIT4 SECTION "Make Screens" [4496-5030] -->
<h3 class="sectionedit5" id="make_layers">Make Layers</h3>
<div class="level3">

<p>
The following Java code shows how we add layers to the start screen and HUD screen:
</p>
<pre class="code java">nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"start"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"start"</span><span class="br0">)</span><span class="br0">{</span><span class="br0">{</span>
        controller<span class="br0">(</span><span class="kw1">new</span> DefaultScreenController<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
         <span class="co1">// layer added</span>
         layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"background"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
            childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            backgroundColor<span class="br0">(</span><span class="st0">"#000f"</span><span class="br0">)</span><span class="sy0">;</span>  
 
            <span class="co1">// &lt;!-- ... --&gt;</span>
         <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
         layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"foreground"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutVertical<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#0000"</span><span class="br0">)</span><span class="sy0">;</span>        
 
            <span class="co1">// &lt;!-- ... --&gt;</span>
         <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
         <span class="co1">// layer added</span>
 
      <span class="br0">}</span><span class="br0">}</span>.<span class="me1">build</span><span class="br0">(</span>nifty<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Repeat the same, but use 
</p>
<pre class="code">nifty.addScreen("hud", new ScreenBuilder("hud"){{</pre>

<p>
 for the HUD screen.
</p>

<p>
In a layer, you can now add panels and arrange them. Panels are containers that mark the areas where you want to display text, images, or controls (buttons etc) later. 
</p>

</div>
<!-- EDIT5 SECTION "Make Layers" [5031-5968] -->
<h3 class="sectionedit6" id="make_panels">Make Panels</h3>
<div class="level3">

<p>
A panel is the inner-most container (that will contain the actual content: text, images, or controls). You place panels inside layers. The following panels go into in the <code>start</code> screen:
</p>
<pre class="code java">    nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"start"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"start"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
        controller<span class="br0">(</span><span class="kw1">new</span> DefaultScreenController<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"background"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
            childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            backgroundColor<span class="br0">(</span><span class="st0">"#000f"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co1">// &lt;!-- ... --&gt;</span>
        <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
        layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"foreground"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutVertical<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#0000"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="co1">// panel added</span>
            panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_top"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#f008"</span><span class="br0">)</span><span class="sy0">;</span>
                height<span class="br0">(</span><span class="st0">"25%"</span><span class="br0">)</span><span class="sy0">;</span>
                width<span class="br0">(</span><span class="st0">"75%"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
            panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_mid"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#0f08"</span><span class="br0">)</span><span class="sy0">;</span>
                height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                width<span class="br0">(</span><span class="st0">"75%"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
            panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_bottom"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutHorizontal<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#00f8"</span><span class="br0">)</span><span class="sy0">;</span>
                height<span class="br0">(</span><span class="st0">"25%"</span><span class="br0">)</span><span class="sy0">;</span>
                width<span class="br0">(</span><span class="st0">"75%"</span><span class="br0">)</span><span class="sy0">;</span>
 
                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_bottom_left"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#44f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_bottom_right"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#88f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// panel added</span>
        <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span><span class="br0">}</span>.<span class="me1">build</span><span class="br0">(</span>nifty<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The following panels go into in the <code>hud</code> screen:
</p>
<pre class="code Java">    nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"hud"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"hud"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
        controller<span class="br0">(</span><span class="kw1">new</span> DefaultScreenController<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"background"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
            childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            backgroundColor<span class="br0">(</span><span class="st0">"#000f"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co1">// &lt;!-- ... --&gt;</span>
        <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
        layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"foreground"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
            childLayoutHorizontal<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            backgroundColor<span class="br0">(</span><span class="st0">"#0000"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="co1">// panel added</span>
            panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_left"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutVertical<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#0f08"</span><span class="br0">)</span><span class="sy0">;</span>
                height<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                width<span class="br0">(</span><span class="st0">"80%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="co1">// &lt;!-- spacer --&gt;</span>
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
            panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_right"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutVertical<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#00f8"</span><span class="br0">)</span><span class="sy0">;</span>
                height<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                width<span class="br0">(</span><span class="st0">"20%"</span><span class="br0">)</span><span class="sy0">;</span>
 
                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_top_right1"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#00f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"15%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_top_right2"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#44f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"15%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_bot_right"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#88f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"70%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// panel added</span>
        <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span><span class="br0">}</span>.<span class="me1">build</span><span class="br0">(</span>nifty<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Try the sample. Remember to activate a screen using <code>nifty.gotoScreen(“start”);</code> or <code>hud</code> respectively.
The result should look as follows:
</p>

<p>
<a href="/resources/jme3-advanced-nifty-gui-panels.png" class="media" title="jme3:advanced:nifty-gui-panels.png"><img src="/resources/jme3-advanced-nifty-gui-panels.png" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT6 SECTION "Make Panels" [5969-9926] -->
<h2 class="sectionedit7" id="adding_content_to_panels">Adding Content to Panels</h2>
<div class="level2">

<p>
See also <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Layout_Introduction" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Layout_Introduction" rel="nofollow">Layout Introduction</a> on the Nifty <abbr title="Graphical User Interface">GUI</abbr> site.
</p>

</div>
<!-- EDIT7 SECTION "Adding Content to Panels" [9927-10105] -->
<h3 class="sectionedit8" id="add_images">Add Images</h3>
<div class="level3">

<p>
The start-background.png image is a fullscreen background picture. In the <code>start</code> screen, add the following image element:
</p>
<pre class="code java">    nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"start"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"start"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
        controller<span class="br0">(</span><span class="kw1">new</span> DefaultScreenController<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"background"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
            childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            backgroundColor<span class="br0">(</span><span class="st0">"#000f"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="co1">// add image</span>
            image<span class="br0">(</span><span class="kw1">new</span> ImageBuilder<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                filename<span class="br0">(</span><span class="st0">"Interface/tutorial/start-background.png"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The hud-frame.png image is a transparent frame that we use as HUD decoration. In the <code>hud</code> screen, add the following image element:
</p>
<pre class="code java">    nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"hud"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"hud"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
        controller<span class="br0">(</span><span class="kw1">new</span> DefaultScreenController<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        layer<span class="br0">(</span><span class="kw1">new</span> LayerBuilder<span class="br0">(</span><span class="st0">"background"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
            childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            backgroundColor<span class="br0">(</span><span class="st0">"#000f"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="co1">// add image</span>
            image<span class="br0">(</span><span class="kw1">new</span> ImageBuilder<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                filename<span class="br0">(</span><span class="st0">"Interface/tutorial/hud-frame.png"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The face1.png image is an image that you want to use as a status icon. 
In the <code>hud</code> screen's <code>foreground</code> layer, add the following image element:
</p>
<pre class="code java">                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_top_right2"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#44f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"15%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
 
                    <span class="co1">// add image</span>
                    image<span class="br0">(</span><span class="kw1">new</span> ImageBuilder<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                        filename<span class="br0">(</span><span class="st0">"Interface/tutorial/face1.png"</span><span class="br0">)</span><span class="sy0">;</span>
                        valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                        alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                        height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                        width<span class="br0">(</span><span class="st0">"30%"</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This image is scaled to use 50% of the height and 30% of the width of its container.
</p>

</div>
<!-- EDIT8 SECTION "Add Images" [10106-12093] -->
<h3 class="sectionedit9" id="add_static_text">Add Static Text</h3>
<div class="level3">

<p>
The game title is a typical example of static text. In the <code>start</code> screen, add the following text element:
</p>
<pre class="code java">           <span class="co1">// panel added</span>
            panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_top"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#f008"</span><span class="br0">)</span><span class="sy0">;</span>
                height<span class="br0">(</span><span class="st0">"25%"</span><span class="br0">)</span><span class="sy0">;</span>
                width<span class="br0">(</span><span class="st0">"75%"</span><span class="br0">)</span><span class="sy0">;</span>
 
                <span class="co1">// add text</span>
                text<span class="br0">(</span><span class="kw1">new</span> TextBuilder<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    text<span class="br0">(</span><span class="st0">"My Cool Game"</span><span class="br0">)</span><span class="sy0">;</span>
                    font<span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For longer pieces of static text, such as an introduction, you can use wrap=“true”. Add the following text element to the <code>Start screen</code>:
</p>
<pre class="code java">            panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_mid"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                backgroundColor<span class="br0">(</span><span class="st0">"#0f08"</span><span class="br0">)</span><span class="sy0">;</span>
                height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                width<span class="br0">(</span><span class="st0">"75%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="co1">// add text</span>
                text<span class="br0">(</span><span class="kw1">new</span> TextBuilder<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    text<span class="br0">(</span><span class="st0">"Here goes some text describing the game and the rules and stuff. "</span><span class="sy0">+</span>
                         <span class="st0">"Incidentally, the text is quite long and needs to wrap at the end of lines. "</span><span class="br0">)</span><span class="sy0">;</span>
                    font<span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
                    wrap<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The font used is jME3's default font “Interface/Fonts/Default.fnt” which is included in the jMonkeyEngine.JAR. You can add your own fonts to your own <code>assets/Interface</code> directory.
</p>

</div>
<!-- EDIT9 SECTION "Add Static Text" [12094-13843] -->
<h3 class="sectionedit10" id="add_controls">Add Controls</h3>
<div class="level3">

<p>
Before you can use any control, you must load a Control Definition first. Add the following two lines <em>before</em> your screen definitions:
</p>
<pre class="code java">    nifty.<span class="me1">loadStyleFile</span><span class="br0">(</span><span class="st0">"nifty-default-styles.xml"</span><span class="br0">)</span><span class="sy0">;</span>
    nifty.<span class="me1">loadControlFile</span><span class="br0">(</span><span class="st0">"nifty-default-controls.xml"</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="label_control">Label Control</h4>
<div class="level4">

<p>
Use label controls for text that you want to edit dynamically from Java. One example for this is the score display.
In the <code>hud</code> screen's <code>foreground</code> layer, add the following text element:
</p>
<pre class="code java">                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_top_right1"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#00f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"15%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
 
                    control<span class="br0">(</span><span class="kw1">new</span> LabelBuilder<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span><span class="br0">{</span>
                        color<span class="br0">(</span><span class="st0">"#000"</span><span class="br0">)</span><span class="sy0">;</span> 
                        text<span class="br0">(</span><span class="st0">"123"</span><span class="br0">)</span><span class="sy0">;</span> 
                        width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span> 
                        height<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Note that the width and height do not scale the bitmap font, but make indirectly certain it is centered. If you want a different size for the font, you need to provide an extra bitmap font (they come with fixes sizes and don't scale well).
</p>

</div>

<h4 id="button_control">Button Control</h4>
<div class="level4">

<p>
Our <abbr title="Graphical User Interface">GUI</abbr> plan asks for two buttons on the start screen. You add the Start and Quit buttons to the bottom panel of the <code>start</code> screen using the <code>&lt;control&gt;</code> element:
</p>
<pre class="code java">                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_bottom_left"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#44f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
 
                    <span class="co1">// add control</span>
                    control<span class="br0">(</span><span class="kw1">new</span> ButtonBuilder<span class="br0">(</span><span class="st0">"StartButton"</span>, <span class="st0">"Start"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                      alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                      valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                      height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                      width<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
                panel<span class="br0">(</span><span class="kw1">new</span> PanelBuilder<span class="br0">(</span><span class="st0">"panel_bottom_right"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                    childLayoutCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    backgroundColor<span class="br0">(</span><span class="st0">"#88f8"</span><span class="br0">)</span><span class="sy0">;</span>
                    height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                    width<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
 
                    <span class="co1">// add control</span>
                    control<span class="br0">(</span><span class="kw1">new</span> ButtonBuilder<span class="br0">(</span><span class="st0">"QuitButton"</span>, <span class="st0">"Quit"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
                      alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                      valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                      height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                      width<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
                <span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Note that these controls don't do anything yet – we'll get to that soon.
</p>

</div>

<h4 id="other_controls">Other Controls</h4>
<div class="level4">

<p>
Nifty additionally offers many customizable controls such as check boxes, text fields, menus, chats, tabs, … See also <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Elements" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Elements" rel="nofollow">Elements</a> on the Nifty <abbr title="Graphical User Interface">GUI</abbr> site.
</p>

</div>
<!-- EDIT10 SECTION "Add Controls" [13844-16777] -->
<h2 class="sectionedit11" id="intermediate_result">Intermediate Result</h2>
<div class="level2">

<p>
When you preview this code in the jMonkeyEngine SDK, our tutorial demo should looks as follows: A start screen with two buttons, and a game screen with a simple HUD frame and a blue cube (which stands for any jME3 game content). 
</p>

<p>
<strong>Tip:</strong> Remove all lines that set background colors, you only needed them to see the arrangement.
</p>

<p>
<a href="/resources/jme3-advanced-nifty-gui-simple-demo.png" class="media" title="jme3:advanced:nifty-gui-simple-demo.png"><img src="/resources/jme3-advanced-nifty-gui-simple-demo.png" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT11 SECTION "Intermediate Result" [16778-17190] -->
<h2 class="sectionedit12" id="nifty_java_settings">Nifty Java Settings</h2>
<div class="level2">

<p>
Before initializing the nifty screens, you set up properties and register media.
</p>
<div class="table sectionedit13"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Nifty Method </th><th class="col1"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> registerSound(“mysound”, “Interface/abc.wav”); </td><td class="col1"> </td>
	</tr>
	<tr class="row2">
		<td class="col0"> registerMusic(“mymusic”, “Interface/xyz.ogg”); </td><td class="col1"> </td>
	</tr>
	<tr class="row3">
		<td class="col0"> registerMouseCursor(“mypointer”, “Interface/abc.png”, 5, 4); </td><td class="col1"> </td>
	</tr>
	<tr class="row4">
		<td class="col0"> registerEffect(?); </td><td class="col1"> ? </td>
	</tr>
	<tr class="row5">
		<td class="col0"> setDebugOptionPanelColors(true);</td><td class="col1"> Highlight all panels, makes it easier to arrange them. </td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [17305-17628] -->
<p>
Example: 
</p>
<pre class="code java">nifty.<span class="me1">registerMouseCursor</span><span class="br0">(</span><span class="st0">"hand"</span>, <span class="st0">"Interface/mouse-cursor-hand.png"</span>, <span class="nu0">5</span>, <span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT12 SECTION "Nifty Java Settings" [17191-17733] -->
<h2 class="sectionedit14" id="next_steps">Next Steps</h2>
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
<!-- EDIT14 SECTION "Next Steps" [17734-] -->
