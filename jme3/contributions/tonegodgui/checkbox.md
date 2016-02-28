---
title: CheckBox Class
---
<h3 class="sectionedit1" id="checkbox_class">CheckBox Class</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> CheckBox’s extend the Button class and enable the Toggle setting</div>
</li>
<li class="level1"><div class="li"> They provide a default label (which is only added if the label text is set).</div>
</li>
<li class="level1"><div class="li"> They provide the abstract method onChange for executing code when the CheckBox is altered by the user.</div>
</li>
</ul>

<p>
Again, the same three options for constructor are available as show in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a>.<br />

<br />

<strong>Constructor 1:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
CheckBox cb <span class="sy0">=</span> <span class="kw1">new</span> CheckBox<span class="br0">(</span>screen, “cb”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 2:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
CheckBox cb <span class="sy0">=</span> <span class="kw1">new</span> CheckBox<span class="br0">(</span>screen, “cb”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">25</span>, <span class="nu0">25</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 3:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
CheckBox cb <span class="sy0">=</span> <span class="kw1">new</span> CheckBox<span class="br0">(</span>screen, “cb”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">25</span>, <span class="nu0">25</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">3</span>,<span class="nu0">3</span>,<span class="nu0">3</span>,<span class="nu0">3</span><span class="br0">)</span>,
    “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a><span class="sy0">/</span>checkbox_u_x.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="hover_state">Hover State</h4>
<div class="level4">

<p>
You can override the default hover state using the following method:
</p>
<pre class="code java"><span class="co1">// Override the information used by the hover effect</span>
cb.<span class="me1">setButtonHoverInfo</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> imagePath, ColorRGBA textHoverColor<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="pressed_state">Pressed State</h4>
<div class="level4">

<p>
You can override the default pressed state using the following method:
</p>
<pre class="code java"><span class="co1">// Override the information used by the pressed effect</span>
cb.<span class="me1">setButtonPressedInfo</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> imagePath, ColorRGBA textPressedColor<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onChange<span class="br0">(</span><span class="kw4">boolean</span> isChecked<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_checkbox_class">Methods Specific to the CheckBox Class:</h4>
<div class="level4">
<pre class="code java">cb.<span class="me1">setCheckboxText</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> text<span class="br0">)</span><span class="sy0">;</span>
cb.<span class="me1">getIsChecked</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
