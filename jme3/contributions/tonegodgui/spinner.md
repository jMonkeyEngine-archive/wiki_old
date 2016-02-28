---
title: Spinner Class
---
<h3 class="sectionedit1" id="spinner_class">Spinner Class</h3>
<div class="level3">

<p>
The Spinner class provides:<br />

</p>
<ul>
<li class="level1"><div class="li"> A display area for the current step value</div>
</li>
<li class="level1"><div class="li"> An increment button</div>
</li>
<li class="level1"><div class="li"> A Decrement button</div>
</li>
<li class="level1"><div class="li"> It can be set to cycle (when it reaches heighest step value it cycles to index 0, and reversed for decrement.</div>
</li>
</ul>

<p>
The Spinner class provides the same 3 common constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a> with the addition of two extra parameters.
</p>
<ul>
<li class="level1"><div class="li"> The orientation of the Spinner</div>
</li>
<li class="level1"><div class="li"> A boolean flag enabling/disabling Spinner cycling.</div>
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
  * Spinner.Orientation orientation
  * boolean cycle
  */</span>
Spinner spinner1 <span class="sy0">=</span> <span class="kw1">new</span> Spinner<span class="br0">(</span>
    screen,
    “SomeID”,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    Spinner.<span class="me1">Orientation</span>.<span class="me1">HORIZONTAL</span>,
    <span class="kw2">true</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onChange<span class="br0">(</span><span class="kw4">int</span> selectedIndex, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_spinner_class">Methods specific to the Spinner class:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Quickly set interval info for both button</span>
spinner1.<span class="me1">setInterval</span><span class="br0">(</span><span class="kw4">float</span> callsPerSecond<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Adding removing list info</span>
spinner1.<span class="me1">addStepValue</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span>
spinner1.<span class="me1">removeStepValue</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Quickly populate step values with integers/floats</span>
spinner1.<span class="me1">setStepIntegerRange</span><span class="br0">(</span><span class="kw4">int</span> min, <span class="kw4">int</span> max, <span class="kw4">int</span> inc<span class="br0">)</span><span class="sy0">;</span>
spinner1.<span class="me1">setStepFloatRange</span><span class="br0">(</span><span class="kw4">float</span> min, <span class="kw4">float</span> max, <span class="kw4">float</span> inc<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Retrieval of current selected step</span>
spinner1.<span class="me1">getSelectedIndex</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can set the select Spinner's displayed and selected value using:
</p>
<pre class="code java">spinner1.<span class="me1">setSelectedIndex</span><span class="br0">(</span><span class="kw4">int</span> selectedIndex<span class="br0">)</span></pre>

</div>
