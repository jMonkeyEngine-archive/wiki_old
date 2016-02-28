---
title: DialogBox Class
---
<h3 class="sectionedit1" id="dialogbox_class">DialogBox Class</h3>
<div class="level3">

<p>
The DialogBox extends AlertBox adding a Cancel button with event handlers.<br />

<br />

It utilizes the 3 standard constructors as shown in the <a href="http://wiki.jmonkeyengine.org/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://wiki.jmonkeyengine.org/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a>.
</p>

<p>
<strong>Constructor 1:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
DialogBox dialog <span class="sy0">=</span> <span class="kw1">new</span> DialogBox<span class="br0">(</span>screen, “dialog”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 2:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
DialogBox dialog <span class="sy0">=</span> <span class="kw1">new</span> DialogBox<span class="br0">(</span>screen, “dialog”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">400</span>, <span class="nu0">300</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 3:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
DialogBox dialog <span class="sy0">=</span> <span class="kw1">new</span> DialogBox<span class="br0">(</span>screen, “dialog”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">400</span>, <span class="nu0">300</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">14</span>,<span class="nu0">14</span>,<span class="nu0">14</span>,<span class="nu0">14</span><span class="br0">)</span>,
    “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a><span class="sy0">/</span>panel_x.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onButtonOkPressed<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> toggled<span class="br0">)</span>
<span class="kw1">public</span> <span class="kw4">void</span> onButtonCencelPressed<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> toggled<span class="br0">)</span></pre>

</div>

<h4 id="methods_specific_to_the_dialogbox_class">Methods specific to the DialogBox class:</h4>
<div class="level4">
<pre class="code java">dialog.<span class="me1">setButtonCancelText</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> text<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
