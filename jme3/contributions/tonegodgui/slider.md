---
title: Slider Class
---
<h3 class="sectionedit1" id="slider_class">Slider Class</h3>
<div class="level3">

<p>
The Slider class provides the same 3 common contrustors shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a> with the addition of two extra parameters.
</p>
<ul>
<li class="level1"><div class="li"> The orientation of the Slider</div>
</li>
<li class="level1"><div class="li"> A boolean flag telling the control whether or not the track should “surround” the thumb.</div>
</li>
</ul>

<p>
The additional parameter are appended to the existing parameter list for all 3 constructors, like so:
</p>
<pre class="code java"><span class="co3">/**
  * Parameters:
  * Screen screen
  * String UID
  * Vector2f position
  * Slider.Orientation orientation
  * boolean trackSurroundsThumb
  */</span>
Slider slider1 <span class="sy0">=</span> <span class="kw1">new</span> Slider<span class="br0">(</span>
    screen,
    “SomeID”,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    Slider.<span class="me1">Orientation</span>.<span class="me1">HORIZONTAL</span>,
    <span class="kw2">true</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onChange<span class="br0">(</span><span class="kw4">int</span> selectedIndex, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_slider_class">Methods specific to the Slider class:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Adding/removing step values</span>
slider1.<span class="me1">addStepValue</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span>
slider1.<span class="me1">removeStepValue</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Selected values</span>
slider1.<span class="me1">getSelectedIndex</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can set the select Sliders position and selected value using:
</p>
<pre class="code java">slider1.<span class="me1">setSelectedIndex</span><span class="br0">(</span><span class="kw4">int</span> selectedIndex<span class="br0">)</span></pre>

</div>
