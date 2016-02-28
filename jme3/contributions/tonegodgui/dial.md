---
title: Dial Class
---
<h3 class="sectionedit1" id="dial_class">Dial Class</h3>
<div class="level3">

<p>
The Dial class provides:
</p>
<ul>
<li class="level1"><div class="li"> A rotating knob for selecting step values</div>
</li>
</ul>

<p>
The Dial class provides the standard 3 common constructors as sown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a>.
</p>

<p>
<br />

<strong>Constructor 1:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
Dial dial <span class="sy0">=</span> <span class="kw1">new</span> Dial<span class="br0">(</span>screen, “dial”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 2:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
Dial dial <span class="sy0">=</span> <span class="kw1">new</span> Dial<span class="br0">(</span>screen, “dial”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">35</span>, <span class="nu0">35</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 3:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
Dial dial <span class="sy0">=</span> <span class="kw1">new</span> Dial<span class="br0">(</span>screen, “dial”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">35</span>, <span class="nu0">35</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span>,
    “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span>Dial<span class="sy0">/</span>dial_x.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onChange<span class="br0">(</span><span class="kw4">int</span> selectedIndex, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_dial_class">Methods specific to the Dial class:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Adding removing list info</span>
dial.<span class="me1">addStepValue</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span>
dial.<span class="me1">removeStepValue</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Retrieval of current selected step</span>
dial.<span class="me1">getSelectedIndex</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
