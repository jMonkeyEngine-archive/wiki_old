---
title: The Screen Class
---
<h3 class="sectionedit1" id="the_screen_class">The Screen Class</h3>
<div class="level3">

<p>
You can create a screen using one of the two provided constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a>.<br />

</p>
<pre class="code java"><span class="co1">// this = any JME Application</span>
Screen screen <span class="sy0">=</span> <span class="kw1">new</span> Screen<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">addControl</span><span class="br0">(</span>screen<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Optionally, you can provide a path to a custom Style theme:
</p>
<pre class="code java"><span class="co1">// this = any JME Application</span>
Screen screen <span class="sy0">=</span> <span class="kw1">new</span> Screen<span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"tonegod/gui/style/def/style_map.xml"</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">addControl</span><span class="br0">(</span>screen<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To make use of custom cursors, call this method prior to initializing the screen:
</p>
<pre class="code java">screen.<span class="me1">setUseCustomCursors</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can disable and re-enable custom cursors at any point, but they must be initialized with the screen to be loaded.<br />

<br />

</p>

<p>
Cursor Effects can be enabled/disabled at anytime by calling:
</p>
<pre class="code java">screen.<span class="me1">setUseCursorEffects</span><span class="br0">(</span><span class="kw4">boolean</span> useCursorEffects<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="noteclassic">More info on: <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:cursoreffects" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:cursoreffects" rel="nofollow">Cursor Effects</a>.
</div>


<p>
Tool Tips can be enabled/disabled at anytime by calling:
</p>
<pre class="code java">screen.<span class="me1">setUseToolTips</span><span class="br0">(</span><span class="kw4">boolean</span> useToolTips<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="noteclassic">More info on: <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:tooltips" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:tooltips" rel="nofollow">Tool Tips</a>.
</div>


<p>
Audio can be enabled/disabled at anytime by calling:
</p>
<pre class="code java">screen.<span class="me1">setUseUIAudio</span><span class="br0">(</span><span class="kw4">boolean</span> useUIAudio<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="noteclassic">More info on: <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:audio" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:audio" rel="nofollow">Audio Support</a>.
</div>


</div>

<h4 id="application_quick_references_methods">Application quick references methods:</h4>
<div class="level4">
<pre class="code java">screen.<span class="me1">getApplication</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Screen dimensions</span>
screen.<span class="me1">getWidth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Mouse position</span>
screen.<span class="me1">getMouseXY</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// returns a Vector2f containing current mouse x/y</span></pre>

</div>

<h4 id="methods_for_adding_remove_base_level_controls">Methods for adding remove base level controls:</h4>
<div class="level4">
<pre class="code java">screen.<span class="me1">addElement</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">removeElement</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="z-order_methods">Z-Order Methods:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Bring the specified Element to the front</span>
screen.<span class="me1">updateZOrder</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> topMost<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="accessing_the_effectmanager">Accessing the EffectManager:</h4>
<div class="level4">
<pre class="code java">screen.<span class="me1">getEffectManager</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="retrieving_a_style">Retrieving a Style:</h4>
<div class="level4">
<pre class="code java">screen.<span class="me1">getStyle</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> tagName<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="custom_cursor_related_methods">Custom Cursor Related Methods:</h4>
<div class="level4">
<pre class="code java">screen.<span class="me1">setCursor</span><span class="br0">(</span>Screen.<span class="me1">CursorType</span> cur<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// called by controls</span>
screen.<span class="me1">setForcedCursor</span><span class="br0">(</span>Screen.<span class="me1">CursorType</span> cur<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Overrides control manipulation of cursor.</span>
screen.<span class="me1">releaseForcedCursor</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Release cursor manipulation back to controls</span></pre>

</div>

<h4 id="retrieving_elements">Retrieving Elements</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Recursive search</span>
screen.<span class="me1">getElementById</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+uid"><span class="kw3">UID</span></a><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="ui_global_alpha_settings">UI Global Alpha Settings:</h4>
<div class="level4">
<pre class="code java">screen.<span class="me1">setGlobalAlpha</span><span class="br0">(</span><span class="kw4">float</span> globalAlpha<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">getGlobalAlpha</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="ui_global_audio_settings">UI Global Audio Settings:</h4>
<div class="level4">
<pre class="code java">screen.<span class="me1">setUseUIAudio</span><span class="br0">(</span><span class="kw4">boolean</span> useUIAudio<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">getUseUIAudio</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">setUIAudioVolume</span><span class="br0">(</span><span class="kw4">float</span> uiAudioVolume<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">getUIAudioVolume</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">playAudioNode</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> key, <span class="kw4">float</span> volume<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="enabling_global_texture_atlas_use">Enabling Global Texture Atlas Use</h4>
<div class="level4">

<p>
Keep in mind, that it is possible to enable texture atlas usage per element without enabling global texture atlas use.
</p>
<pre class="code java">screen.<span class="me1">setUseTextureAtlas</span><span class="br0">(</span><span class="kw4">boolean</span> useTextureAtlas, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> texturePath<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">getUseTextureAtlas</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">getAtlasTexture</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
