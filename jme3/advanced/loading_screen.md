---
title: Nifty Loading Screen (Progress Bar)
---
<h3 class="sectionedit1" id="nifty_loading_screen_progress_bar">Nifty Loading Screen (Progress Bar)</h3>
<div class="level3">

<p>
There is a good tutorial about creating a nifty progress bar here:
<a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Create_your_own_Control_%28A_Nifty_Progressbar%29" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Create_your_own_Control_%28A_Nifty_Progressbar%29" rel="nofollow">http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Create_your_own_Control_%28A_Nifty_Progressbar%29</a>
</p>

<p>
This example will use the existing hello terrain as an example.
It will require these 2 images inside Assets/Interface/ (save them as border.png and inner.png respectively)
</p>

<p>
<a href="/resources/jme3-advanced-inner1.png" class="media" title="jme3:advanced:inner1.png"><img src="/resources/jme3-advanced-inner1.png" class="media" alt="" /></a>
<a href="/resources/jme3-advanced-border1.png" class="media" title="jme3:advanced:border1.png"><img src="/resources/jme3-advanced-border1.png" class="media" alt="" /></a>
</p>

<p>
This is the progress bar at 90%:
</p>

<p>
<a href="/resources/jme3-advanced-loadingscreen.png" class="media" title="jme3:advanced:loadingscreen.png"><img src="/resources/jme3-advanced-loadingscreen.png" class="media" alt="" /></a>
</p>

<p>
nifty_loading.xml
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;?xml</span> <span class="re0">version</span>=<span class="st0">"1.0"</span> <span class="re0">encoding</span>=<span class="st0">"UTF-8"</span><span class="re2">?&gt;</span></span>
<span class="sc3"><span class="re1">&lt;nifty<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;useStyles</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-styles.xml"</span> <span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;useControls</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-controls.xml"</span> <span class="re2">/&gt;</span></span>
 
    <span class="sc3"><span class="re1">&lt;controlDefinition</span> name = <span class="st0">"loadingbar"</span> controller = <span class="st0">"jme3test.TestLoadingScreen"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/border.png"</span> <span class="re0">childLayout</span>=<span class="st0">"absolute"</span> </span>
<span class="sc3">               <span class="re0">imageMode</span>=<span class="st0">"resize:15,2,15,15,15,2,15,2,15,2,15,15"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">id</span>=<span class="st0">"progressbar"</span> <span class="re0">x</span>=<span class="st0">"0"</span> <span class="re0">y</span>=<span class="st0">"0"</span> <span class="re0">filename</span>=<span class="st0">"Interface/inner.png"</span> <span class="re0">width</span>=<span class="st0">"32px"</span> <span class="re0">height</span>=<span class="st0">"100%"</span></span>
<span class="sc3">                   <span class="re0">imageMode</span>=<span class="st0">"resize:15,2,15,15,15,2,15,2,15,2,15,15"</span> <span class="re2">/&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;/image<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/controlDefinition<span class="re2">&gt;</span></span></span>
 
    <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"start"</span> controller = <span class="st0">"jme3test.TestLoadingScreen"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"layer"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;panel</span> id = <span class="st0">"panel2"</span> <span class="re0">height</span>=<span class="st0">"30%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span></span>
<span class="sc3">                   <span class="re0">visibleToMouse</span>=<span class="st0">"true"</span><span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">id</span>=<span class="st0">"startGame"</span> <span class="re0">name</span>=<span class="st0">"button"</span> <span class="re0">backgroundColor</span>=<span class="st0">"#0000"</span> <span class="re0">label</span>=<span class="st0">"Load Game"</span> <span class="re0">align</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
                    <span class="sc3"><span class="re1">&lt;interact</span> <span class="re0">onClick</span>=<span class="st0">"showLoadingMenu()"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;/control<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
 
    <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"loadlevel"</span> controller = <span class="st0">"jme3test.TestLoadingScreen"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"loadinglayer"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span> <span class="re0">backgroundColor</span>=<span class="st0">"#000000"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;panel</span> id = <span class="st0">"loadingpanel"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">height</span>=<span class="st0">"32px"</span> <span class="re0">width</span>=<span class="st0">"70%"</span><span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"loadingbar"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">id</span>=<span class="st0">"loadingtext"</span> <span class="re0">name</span>=<span class="st0">"label"</span> <span class="re0">align</span>=<span class="st0">"center"</span> </span>
<span class="sc3">                         <span class="re0">text</span>=<span class="st0">"                                                  "</span><span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
 
    <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"end"</span> controller = <span class="st0">"jme3test.TestLoadingScreen"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
 
<span class="sc3"><span class="re1">&lt;/nifty<span class="re2">&gt;</span></span></span></pre>

</div>

<h4 id="understanding_nifty_xml">Understanding Nifty XML</h4>
<div class="level4">

<p>
The progress bar and text is done statically using nifty XML.
A custom control is created, which represents the progress bar.
</p>
<pre class="code xml">    <span class="sc3"><span class="re1">&lt;controlDefinition</span> name = <span class="st0">"loadingbar"</span> controller = <span class="st0">"jme3test.TestLoadingScreen"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">filename</span>=<span class="st0">"Interface/border.png"</span> <span class="re0">childLayout</span>=<span class="st0">"absolute"</span> </span>
<span class="sc3">               <span class="re0">imageMode</span>=<span class="st0">"resize:15,2,15,15,15,2,15,2,15,2,15,15"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;image</span> <span class="re0">id</span>=<span class="st0">"progressbar"</span> <span class="re0">x</span>=<span class="st0">"0"</span> <span class="re0">y</span>=<span class="st0">"0"</span> <span class="re0">filename</span>=<span class="st0">"Interface/inner.png"</span> <span class="re0">width</span>=<span class="st0">"32px"</span> <span class="re0">height</span>=<span class="st0">"100%"</span></span>
<span class="sc3">                   <span class="re0">imageMode</span>=<span class="st0">"resize:15,2,15,15,15,2,15,2,15,2,15,15"</span><span class="re2">/&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;/image<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/controlDefinition<span class="re2">&gt;</span></span></span></pre>

<p>
This screen simply displays a button in the middle of the screen, which could be seen as a simple main menu UI.
</p>
<pre class="code xml">    <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"start"</span> controller = <span class="st0">"jme3test.TestLoadingScreen"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"layer"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;panel</span> id = <span class="st0">"panel2"</span> <span class="re0">height</span>=<span class="st0">"30%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span></span>
<span class="sc3">                   <span class="re0">visibleToMouse</span>=<span class="st0">"true"</span><span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">id</span>=<span class="st0">"startGame"</span> <span class="re0">name</span>=<span class="st0">"button"</span> <span class="re0">backgroundColor</span>=<span class="st0">"#0000"</span> <span class="re0">label</span>=<span class="st0">"Load Game"</span> <span class="re0">align</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>
                    <span class="sc3"><span class="re1">&lt;interact</span> <span class="re0">onClick</span>=<span class="st0">"showLoadingMenu()"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;/control<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span></pre>

<p>
This screen displays our custom progress bar control with a text control
</p>
<pre class="code xml">    <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"loadlevel"</span> controller = <span class="st0">"jme3test.TestLoadingScreen"</span><span class="re2">&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;layer</span> <span class="re0">id</span>=<span class="st0">"loadinglayer"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span> <span class="re0">backgroundColor</span>=<span class="st0">"#000000"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;panel</span> id = <span class="st0">"loadingpanel"</span> <span class="re0">childLayout</span>=<span class="st0">"vertical"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">height</span>=<span class="st0">"32px"</span> <span class="re0">width</span>=<span class="st0">"400px"</span><span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"loadingbar"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">width</span>=<span class="st0">"400px"</span> <span class="re0">height</span>=<span class="st0">"32px"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">id</span>=<span class="st0">"loadingtext"</span> <span class="re0">name</span>=<span class="st0">"label"</span> <span class="re0">align</span>=<span class="st0">"center"</span></span>
<span class="sc3">                          <span class="re0">text</span>=<span class="st0">"                                                  "</span><span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/layer<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span></pre>

</div>
<!-- EDIT1 SECTION "Nifty Loading Screen (Progress Bar)" [1-4344] -->
<h3 class="sectionedit2" id="creating_the_bindings_to_use_the_nifty_xml">Creating the bindings to use the Nifty XML</h3>
<div class="level3">

<p>
There are 3 main ways to update a progress bar. To understand why these methods are necessary, an understanding of the graphics pipeline is needed. 
</p>

<p>
Something like this in a single thread will not work:
</p>
<pre class="code java">load_scene<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
update_bar<span class="br0">(</span><span class="nu0">30</span><span class="sy0">%</span><span class="br0">)</span><span class="sy0">;</span>
load_characters<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
update_bar<span class="br0">(</span><span class="nu0">60</span><span class="sy0">%</span><span class="br0">)</span><span class="sy0">;</span>
load_sounds<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
update_bar<span class="br0">(</span><span class="nu0">100</span><span class="sy0">%</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
If you do all of this in a single frame, then it is sent to the graphics card only after the whole code block has executed. By this time the bar has reached 100% and the game has already begun – for the user, the progressbar on the screen would not have visibly changed.
</p>

<p>
The 2 main good solutions are:
</p>
<ol>
<li class="level1"><div class="li"> Updating explicitly over many frames</div>
</li>
<li class="level1"><div class="li"> Multi-threading</div>
</li>
</ol>

</div>

<h4 id="updating_progress_bar_over_a_number_of_frames">Updating progress bar over a number of frames</h4>
<div class="level4">

<p>
The idea is to break down the loading of the game into discrete parts
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.niftygui.NiftyJmeDisplay</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.Nifty</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.elements.Element</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.input.NiftyInputEvent</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.screen.Screen</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.screen.ScreenController</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.tools.SizeValue</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainLodControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.AbstractHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainQuad</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.ImageBasedHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture.WrapMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.controls.Controller</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.elements.render.TextRenderer</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.xml.xpp3.Attributes</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.ArrayList</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.List</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.Properties</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">jme3tools.converters.ImageToAwt</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> TestLoadingScreen <span class="kw1">extends</span> SimpleApplication <span class="kw1">implements</span> ScreenController, Controller <span class="br0">{</span>
 
    <span class="kw1">private</span> NiftyJmeDisplay niftyDisplay<span class="sy0">;</span>
    <span class="kw1">private</span> Nifty nifty<span class="sy0">;</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> progressBarElement<span class="sy0">;</span>
    <span class="kw1">private</span> TerrainQuad terrain<span class="sy0">;</span>
    <span class="kw1">private</span> Material mat_terrain<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">float</span> frameCount <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> load <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> TextRenderer textRenderer<span class="sy0">;</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        TestLoadingScreen app <span class="sy0">=</span> <span class="kw1">new</span> TestLoadingScreen<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
        niftyDisplay <span class="sy0">=</span> <span class="kw1">new</span> NiftyJmeDisplay<span class="br0">(</span>assetManager,
                inputManager,
                audioRenderer,
                guiViewPort<span class="br0">)</span><span class="sy0">;</span>
        nifty <span class="sy0">=</span> niftyDisplay.<span class="me1">getNifty</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        nifty.<span class="me1">fromXml</span><span class="br0">(</span><span class="st0">"Interface/nifty_loading.xml"</span>, <span class="st0">"start"</span>, <span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
 
        guiViewPort.<span class="me1">addProcessor</span><span class="br0">(</span>niftyDisplay<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
 
        <span class="kw1">if</span> <span class="br0">(</span>load<span class="br0">)</span> <span class="br0">{</span> <span class="co1">//loading is done over many frames</span>
            <span class="kw1">if</span> <span class="br0">(</span>frameCount <span class="sy0">==</span> <span class="nu0">1</span><span class="br0">)</span> <span class="br0">{</span>
                <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element <span class="sy0">=</span> nifty.<span class="me1">getScreen</span><span class="br0">(</span><span class="st0">"loadlevel"</span><span class="br0">)</span>.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"loadingtext"</span><span class="br0">)</span><span class="sy0">;</span>
                textRenderer <span class="sy0">=</span> element.<span class="me1">getRenderer</span><span class="br0">(</span>TextRenderer.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
 
                mat_terrain <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Terrain/Terrain.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
                mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Alpha"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/alphamap.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                setProgress<span class="br0">(</span>0.2f, <span class="st0">"Loading grass"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>frameCount <span class="sy0">==</span> <span class="nu0">2</span><span class="br0">)</span> <span class="br0">{</span>
                Texture grass <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/grass.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
                grass.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
                mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex1"</span>, grass<span class="br0">)</span><span class="sy0">;</span>
                mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex1Scale"</span>, 64f<span class="br0">)</span><span class="sy0">;</span>
                setProgress<span class="br0">(</span>0.4f, <span class="st0">"Loading dirt"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>frameCount <span class="sy0">==</span> <span class="nu0">3</span><span class="br0">)</span> <span class="br0">{</span>
                Texture dirt <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/dirt.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
 
                dirt.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
                mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex2"</span>, dirt<span class="br0">)</span><span class="sy0">;</span>
                mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex2Scale"</span>, 32f<span class="br0">)</span><span class="sy0">;</span>
                setProgress<span class="br0">(</span>0.5f, <span class="st0">"Loading rocks"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>frameCount <span class="sy0">==</span> <span class="nu0">4</span><span class="br0">)</span> <span class="br0">{</span>
                Texture rock <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/road.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
 
                rock.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
 
                mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex3"</span>, rock<span class="br0">)</span><span class="sy0">;</span>
                mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex3Scale"</span>, 128f<span class="br0">)</span><span class="sy0">;</span>
                setProgress<span class="br0">(</span>0.6f, <span class="st0">"Creating terrain"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>frameCount <span class="sy0">==</span> <span class="nu0">5</span><span class="br0">)</span> <span class="br0">{</span>
                AbstractHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
                Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/mountains512.png"</span><span class="br0">)</span><span class="sy0">;</span>
                heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
                heightmap.<span class="me1">load</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                terrain <span class="sy0">=</span> <span class="kw1">new</span> TerrainQuad<span class="br0">(</span><span class="st0">"my terrain"</span>, <span class="nu0">65</span>, <span class="nu0">513</span>, heightmap.<span class="me1">getHeightMap</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                setProgress<span class="br0">(</span>0.8f, <span class="st0">"Positioning terrain"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>frameCount <span class="sy0">==</span> <span class="nu0">6</span><span class="br0">)</span> <span class="br0">{</span>
                terrain.<span class="me1">setMaterial</span><span class="br0">(</span>mat_terrain<span class="br0">)</span><span class="sy0">;</span>
 
                terrain.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">100</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
                terrain.<span class="me1">setLocalScale</span><span class="br0">(</span>2f, 1f, 2f<span class="br0">)</span><span class="sy0">;</span>
                rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span>
                setProgress<span class="br0">(</span>0.9f, <span class="st0">"Loading cameras"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>frameCount <span class="sy0">==</span> <span class="nu0">7</span><span class="br0">)</span> <span class="br0">{</span>
                List<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span> cameras <span class="sy0">=</span> <span class="kw1">new</span> ArrayList<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                cameras.<span class="me1">add</span><span class="br0">(</span>getCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                TerrainLodControl control <span class="sy0">=</span> <span class="kw1">new</span> TerrainLodControl<span class="br0">(</span>terrain, cameras<span class="br0">)</span><span class="sy0">;</span>
                terrain.<span class="me1">addControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
                setProgress<span class="br0">(</span>1f, <span class="st0">"Loading complete"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>frameCount <span class="sy0">==</span> <span class="nu0">8</span><span class="br0">)</span> <span class="br0">{</span>
                nifty.<span class="me1">gotoScreen</span><span class="br0">(</span><span class="st0">"end"</span><span class="br0">)</span><span class="sy0">;</span>
                nifty.<span class="me1">exit</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                guiViewPort.<span class="me1">removeProcessor</span><span class="br0">(</span>niftyDisplay<span class="br0">)</span><span class="sy0">;</span>
                flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
                flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span><span class="nu0">50</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
 
            frameCount<span class="sy0">++;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> setProgress<span class="br0">(</span><span class="kw1">final</span> <span class="kw4">float</span> progress, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> loadingText<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">final</span> <span class="kw4">int</span> MIN_WIDTH <span class="sy0">=</span> <span class="nu0">32</span><span class="sy0">;</span>
        <span class="kw4">int</span> pixelWidth <span class="sy0">=</span> <span class="br0">(</span><span class="kw4">int</span><span class="br0">)</span> <span class="br0">(</span>MIN_WIDTH <span class="sy0">+</span> <span class="br0">(</span>progressBarElement.<span class="me1">getParent</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">-</span> MIN_WIDTH<span class="br0">)</span> <span class="sy0">*</span> progress<span class="br0">)</span><span class="sy0">;</span>
        progressBarElement.<span class="me1">setConstraintWidth</span><span class="br0">(</span><span class="kw1">new</span> SizeValue<span class="br0">(</span>pixelWidth <span class="sy0">+</span> <span class="st0">"px"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        progressBarElement.<span class="me1">getParent</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">layoutElements</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        textRenderer.<span class="me1">setText</span><span class="br0">(</span>loadingText<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> showLoadingMenu<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        nifty.<span class="me1">gotoScreen</span><span class="br0">(</span><span class="st0">"loadlevel"</span><span class="br0">)</span><span class="sy0">;</span>
        load <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onStartScreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onEndScreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> bind<span class="br0">(</span>Nifty nifty, Screen screen<span class="br0">)</span> <span class="br0">{</span>
        progressBarElement <span class="sy0">=</span> nifty.<span class="me1">getScreen</span><span class="br0">(</span><span class="st0">"loadlevel"</span><span class="br0">)</span>.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"progressbar"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">// methods for Controller</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">boolean</span> inputEvent<span class="br0">(</span><span class="kw1">final</span> NiftyInputEvent inputEvent<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> bind<span class="br0">(</span>Nifty nifty, Screen screen, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> elmnt, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+properties"><span class="kw3">Properties</span></a> prprts, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+attributes"><span class="kw3">Attributes</span></a> atrbts<span class="br0">)</span> <span class="br0">{</span>
        progressBarElement <span class="sy0">=</span> elmnt.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"progressbar"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> init<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+properties"><span class="kw3">Properties</span></a> prprts, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+attributes"><span class="kw3">Attributes</span></a> atrbts<span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onFocus<span class="br0">(</span><span class="kw4">boolean</span> getFocus<span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Note:
</p>
<ul>
<li class="level1"><div class="li"> Try and add all controls near the end, as their update loops may begin executing</div>
</li>
</ul>

</div>

<h4 id="using_multithreading">Using multithreading</h4>
<div class="level4">

<p>
For more info on multithreading: <a href="/jme3/advanced/multithreading.html" class="wikilink1" title="jme3:advanced:multithreading">The jME3 Threading Model</a>
</p>

<p>
Make sure to change the XML file to point the controller to TestLoadingScreen<strong>1</strong>
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.niftygui.NiftyJmeDisplay</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.Nifty</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.elements.Element</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.input.NiftyInputEvent</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.screen.Screen</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.screen.ScreenController</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.tools.SizeValue</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.Camera</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainLodControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.AbstractHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.geomipmap.TerrainQuad</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.terrain.heightmap.ImageBasedHeightMap</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.texture.Texture.WrapMode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.controls.Controller</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.elements.render.TextRenderer</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.xml.xpp3.Attributes</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.ArrayList</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.List</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.Properties</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.concurrent.Callable</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.concurrent.Future</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.concurrent.ScheduledThreadPoolExecutor</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">jme3tools.converters.ImageToAwt</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> TestLoadingScreen1 <span class="kw1">extends</span> SimpleApplication <span class="kw1">implements</span> ScreenController, Controller <span class="br0">{</span>
 
    <span class="kw1">private</span> NiftyJmeDisplay niftyDisplay<span class="sy0">;</span>
    <span class="kw1">private</span> Nifty nifty<span class="sy0">;</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> progressBarElement<span class="sy0">;</span>
    <span class="kw1">private</span> TerrainQuad terrain<span class="sy0">;</span>
    <span class="kw1">private</span> Material mat_terrain<span class="sy0">;</span>
    <span class="kw1">private</span> <span class="kw4">boolean</span> load <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="kw1">private</span> ScheduledThreadPoolExecutor exec <span class="sy0">=</span> <span class="kw1">new</span> ScheduledThreadPoolExecutor<span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">private</span> Future loadFuture <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
    <span class="kw1">private</span> TextRenderer textRenderer<span class="sy0">;</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        TestLoadingScreen1 app <span class="sy0">=</span> <span class="kw1">new</span> TestLoadingScreen1<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
        niftyDisplay <span class="sy0">=</span> <span class="kw1">new</span> NiftyJmeDisplay<span class="br0">(</span>assetManager,
                inputManager,
                audioRenderer,
                guiViewPort<span class="br0">)</span><span class="sy0">;</span>
        nifty <span class="sy0">=</span> niftyDisplay.<span class="me1">getNifty</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        nifty.<span class="me1">fromXml</span><span class="br0">(</span><span class="st0">"Interface/nifty_loading.xml"</span>, <span class="st0">"start"</span>, <span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
 
        guiViewPort.<span class="me1">addProcessor</span><span class="br0">(</span>niftyDisplay<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>load<span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>loadFuture <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
                <span class="co1">//if we have not started loading yet, submit the Callable to the executor</span>
                loadFuture <span class="sy0">=</span> exec.<span class="me1">submit</span><span class="br0">(</span>loadingCallable<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
            <span class="co1">//check if the execution on the other thread is done</span>
            <span class="kw1">if</span> <span class="br0">(</span>loadFuture.<span class="me1">isDone</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                <span class="co1">//these calls have to be done on the update loop thread, </span>
                <span class="co1">//especially attaching the terrain to the rootNode</span>
                <span class="co1">//after it is attached, it's managed by the update loop thread </span>
                <span class="co1">// and may not be modified from any other thread anymore!</span>
                nifty.<span class="me1">gotoScreen</span><span class="br0">(</span><span class="st0">"end"</span><span class="br0">)</span><span class="sy0">;</span>
                nifty.<span class="me1">exit</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                guiViewPort.<span class="me1">removeProcessor</span><span class="br0">(</span>niftyDisplay<span class="br0">)</span><span class="sy0">;</span>
                flyCam.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
                flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span><span class="nu0">50</span><span class="br0">)</span><span class="sy0">;</span>
                rootNode.<span class="me1">attachChild</span><span class="br0">(</span>terrain<span class="br0">)</span><span class="sy0">;</span>
                load <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
    <span class="co1">//this is the callable that contains the code that is run on the other thread.</span>
    <span class="co1">//since the assetmananger is threadsafe, it can be used to load data from any thread</span>
    <span class="co1">//we do *not* attach the objects to the rootNode here!</span>
    Callable<span class="sy0">&lt;</span>Void<span class="sy0">&gt;</span> loadingCallable <span class="sy0">=</span> <span class="kw1">new</span> Callable<span class="sy0">&lt;</span>Void<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+void"><span class="kw3">Void</span></a> call<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element <span class="sy0">=</span> nifty.<span class="me1">getScreen</span><span class="br0">(</span><span class="st0">"loadlevel"</span><span class="br0">)</span>.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"loadingtext"</span><span class="br0">)</span><span class="sy0">;</span>
            textRenderer <span class="sy0">=</span> element.<span class="me1">getRenderer</span><span class="br0">(</span>TextRenderer.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
 
            mat_terrain <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Terrain/Terrain.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
            mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Alpha"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/alphamap.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co1">//setProgress is thread safe (see below)</span>
            setProgress<span class="br0">(</span>0.2f, <span class="st0">"Loading grass"</span><span class="br0">)</span><span class="sy0">;</span>
 
            Texture grass <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/grass.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
            grass.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
            mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex1"</span>, grass<span class="br0">)</span><span class="sy0">;</span>
            mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex1Scale"</span>, 64f<span class="br0">)</span><span class="sy0">;</span>
            setProgress<span class="br0">(</span>0.4f, <span class="st0">"Loading dirt"</span><span class="br0">)</span><span class="sy0">;</span>
 
            Texture dirt <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/dirt.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
 
            dirt.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
            mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex2"</span>, dirt<span class="br0">)</span><span class="sy0">;</span>
            mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex2Scale"</span>, 32f<span class="br0">)</span><span class="sy0">;</span>
            setProgress<span class="br0">(</span>0.5f, <span class="st0">"Loading rocks"</span><span class="br0">)</span><span class="sy0">;</span>
 
            Texture rock <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/road.jpg"</span><span class="br0">)</span><span class="sy0">;</span>
 
            rock.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">Repeat</span><span class="br0">)</span><span class="sy0">;</span>
 
            mat_terrain.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Tex3"</span>, rock<span class="br0">)</span><span class="sy0">;</span>
            mat_terrain.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Tex3Scale"</span>, 128f<span class="br0">)</span><span class="sy0">;</span>
            setProgress<span class="br0">(</span>0.6f, <span class="st0">"Creating terrain"</span><span class="br0">)</span><span class="sy0">;</span>
 
            AbstractHeightMap heightmap <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
            Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/splat/mountains512.png"</span><span class="br0">)</span><span class="sy0">;</span>
            heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
            heightmap.<span class="me1">load</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            terrain <span class="sy0">=</span> <span class="kw1">new</span> TerrainQuad<span class="br0">(</span><span class="st0">"my terrain"</span>, <span class="nu0">65</span>, <span class="nu0">513</span>, heightmap.<span class="me1">getHeightMap</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
            setProgress<span class="br0">(</span>0.8f, <span class="st0">"Positioning terrain"</span><span class="br0">)</span><span class="sy0">;</span>
 
            terrain.<span class="me1">setMaterial</span><span class="br0">(</span>mat_terrain<span class="br0">)</span><span class="sy0">;</span>
 
            terrain.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">100</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
            terrain.<span class="me1">setLocalScale</span><span class="br0">(</span>2f, 1f, 2f<span class="br0">)</span><span class="sy0">;</span>
            setProgress<span class="br0">(</span>0.9f, <span class="st0">"Loading cameras"</span><span class="br0">)</span><span class="sy0">;</span>
 
            List<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span> cameras <span class="sy0">=</span> <span class="kw1">new</span> ArrayList<span class="sy0">&lt;</span>Camera<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            cameras.<span class="me1">add</span><span class="br0">(</span>getCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
            TerrainLodControl control <span class="sy0">=</span> <span class="kw1">new</span> TerrainLodControl<span class="br0">(</span>terrain, cameras<span class="br0">)</span><span class="sy0">;</span>
            terrain.<span class="me1">addControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
            setProgress<span class="br0">(</span>1f, <span class="st0">"Loading complete"</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span><span class="sy0">;</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> setProgress<span class="br0">(</span><span class="kw1">final</span> <span class="kw4">float</span> progress, <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> loadingText<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">//since this method is called from another thread, we enqueue the changes to the progressbar to the update loop thread</span>
        enqueue<span class="br0">(</span><span class="kw1">new</span> Callable<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
            <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> call<span class="br0">(</span><span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> <span class="br0">{</span>
                <span class="kw1">final</span> <span class="kw4">int</span> MIN_WIDTH <span class="sy0">=</span> <span class="nu0">32</span><span class="sy0">;</span>
                <span class="kw4">int</span> pixelWidth <span class="sy0">=</span> <span class="br0">(</span><span class="kw4">int</span><span class="br0">)</span> <span class="br0">(</span>MIN_WIDTH <span class="sy0">+</span> <span class="br0">(</span>progressBarElement.<span class="me1">getParent</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">-</span> MIN_WIDTH<span class="br0">)</span> <span class="sy0">*</span> progress<span class="br0">)</span><span class="sy0">;</span>
                progressBarElement.<span class="me1">setConstraintWidth</span><span class="br0">(</span><span class="kw1">new</span> SizeValue<span class="br0">(</span>pixelWidth <span class="sy0">+</span> <span class="st0">"px"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                progressBarElement.<span class="me1">getParent</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">layoutElements</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
                textRenderer.<span class="me1">setText</span><span class="br0">(</span>loadingText<span class="br0">)</span><span class="sy0">;</span>
                <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> showLoadingMenu<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        nifty.<span class="me1">gotoScreen</span><span class="br0">(</span><span class="st0">"loadlevel"</span><span class="br0">)</span><span class="sy0">;</span>
        load <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onStartScreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onEndScreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> bind<span class="br0">(</span>Nifty nifty, Screen screen<span class="br0">)</span> <span class="br0">{</span>
        progressBarElement <span class="sy0">=</span> nifty.<span class="me1">getScreen</span><span class="br0">(</span><span class="st0">"loadlevel"</span><span class="br0">)</span>.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"progressbar"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">// methods for Controller</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">boolean</span> inputEvent<span class="br0">(</span><span class="kw1">final</span> NiftyInputEvent inputEvent<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> bind<span class="br0">(</span>Nifty nifty, Screen screen, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> elmnt, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+properties"><span class="kw3">Properties</span></a> prprts, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+attributes"><span class="kw3">Attributes</span></a> atrbts<span class="br0">)</span> <span class="br0">{</span>
        progressBarElement <span class="sy0">=</span> elmnt.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"progressbar"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> init<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+properties"><span class="kw3">Properties</span></a> prprts, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+attributes"><span class="kw3">Attributes</span></a> atrbts<span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onFocus<span class="br0">(</span><span class="kw4">boolean</span> getFocus<span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> stop<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">stop</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//the pool executor needs to be shut down so the application properly exits.</span>
        exec.<span class="me1">shutdown</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "Creating the bindings to use the Nifty XML" [4345-] -->
