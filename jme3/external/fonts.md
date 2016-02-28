---
title: Font Creator
---
<h1 class="sectionedit1" id="font_creator">Font Creator</h1>
<div class="level1">

<p>
This SDK plugin provides font support for jMonkeyEngine games. It creates AngelFont files from system fonts. Make sure you have the rights/license to use this font! You can <a href="https://www.google.com/search?q=free+fonts" class="urlextern" title="https://www.google.com/search?q=free+fonts" rel="nofollow">search for and download free fonts</a> from many sites.
</p>

</div>
<!-- EDIT1 SECTION "Font Creator" [1-301] -->
<h2 class="sectionedit2" id="installation">Installation</h2>
<div class="level2">

<p>
If the plugin is installed, you see it under <code>Plugins → Installed</code>
</p>

<p>
<a href="/resources/jme3-external-install-font-plugin.png" class="media" title="jme3:external:install-font-plugin.png"><img src="/resources/jme3-external-install-font-plugin.png" class="mediacenter" alt="" width="450" height="275" /></a>
</p>

<p>
(If you don't see it, go to <code>Tools → Plugins → Available Plugins</code> to install Font Creator.)
</p>

</div>
<!-- EDIT2 SECTION "Installation" [302-550] -->
<h2 class="sectionedit3" id="create_font">Create Font</h2>
<div class="level2">

<p>
The following example creates the custom font <code>Orbitron.fnt</code> in the <code>assets/Interface/Fonts</code> directory.
</p>

<p>
<a href="/resources/jme3-external-font-1.png" class="media" title="jme3:external:font-1.png"><img src="/resources/jme3-external-font-1.png" class="mediacenter" alt="" /></a>
</p>

<p>
<a href="/resources/jme3-external-font-2.png" class="media" title="jme3:external:font-2.png"><img src="/resources/jme3-external-font-2.png" class="mediacenter" alt="" /></a>
</p>

<p>
<a href="/resources/jme3-external-font-3.png" class="media" title="jme3:external:font-3.png"><img src="/resources/jme3-external-font-3.png" class="mediacenter" alt="" /></a>
</p>

<p>
<a href="/resources/jme3-external-font-4.png" class="media" title="jme3:external:font-4.png"><img src="/resources/jme3-external-font-4.png" class="mediacenter" alt="" /></a>
</p>

<p>
<a href="/resources/jme3-external-font-5.png" class="media" title="jme3:external:font-5.png"><img src="/resources/jme3-external-font-5.png" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT3 SECTION "Create Font" [551-849] -->
<h2 class="sectionedit4" id="use_font">Use Font</h2>
<div class="level2">

<p>
The following example loads text in the custom font <code>Orbitron.fnt</code> from the <code>assets/Interface/Fonts</code> directory. You use <code>com.jme3.font.*</code> package to handle text on the screen. <code>guiNode</code> is a preconfigured node in any <code>SimpleApplication</code>-based game.
</p>
<pre class="code java">BitmapFont myFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Orbitron.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
BitmapText hudText <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>myFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
hudText.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"You can write any string here"</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">attachChild</span><span class="br0">(</span>hudText<span class="br0">)</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Use Font" [850-] -->
