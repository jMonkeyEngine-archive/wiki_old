---
title: RadioButtonGroup Class
---
<h3 class="sectionedit1" id="radiobuttongroup_class">RadioButtonGroup Class</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Manages the interaction between any number of Button derived classes</div>
</li>
<li class="level1"><div class="li"> Provides the abstract method onSelect for executing code when a Radio Button is selected by the user.</div>
</li>
</ul>

<p>
<br />

<strong>Sample Usage:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Form form
  */</span>
RadioButtonGroup rbg <span class="sy0">=</span> <span class="kw1">new</span> RadioButtonGroup<span class="br0">(</span>screen, <span class="st0">"rbg"</span><span class="br0">)</span> <span class="br0">{</span>
	@Override
	<span class="kw1">public</span> <span class="kw4">void</span> onSelect<span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a> value<span class="br0">)</span> <span class="br0">{</span>
		<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">)</span>value<span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
<span class="co3">/** Parameters:
  * Vector2f position
  * String caption
  * Object value
  */</span>
rbg.<span class="me1">addButton</span><span class="br0">(</span><span class="kw1">new</span> ButtonAdapter<span class="br0">(</span>screen, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">10</span>,<span class="nu0">10</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rbg.<span class="me1">addButton</span><span class="br0">(</span><span class="kw1">new</span> CheckBox<span class="br0">(</span>screen, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">10</span>,<span class="nu0">30</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rbg.<span class="me1">addButton</span><span class="br0">(</span><span class="kw1">new</span> RadioButton<span class="br0">(</span>screen, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">10</span>,<span class="nu0">50</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rbg.<span class="me1">setDisplayElement</span><span class="br0">(</span><span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// null adds the button list to the screen layer</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onSelect<span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a> value<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_checkbox_class">Methods Specific to the CheckBox Class:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Adds all radio buttons as children of specified Element.  Use null to add to screen</span>
rbg.<span class="me1">setDisplayElement</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Selects a radio button via code</span>
rbg.<span class="me1">setSelected</span><span class="br0">(</span><span class="kw4">int</span> index<span class="br0">)</span><span class="sy0">;</span>
rbg.<span class="me1">setSelected</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a> button<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
