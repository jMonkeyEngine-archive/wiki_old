---
title: DragElement Class
---
<h3 class="sectionedit1" id="dragelement_class">DragElement Class</h3>
<div class="level3">

<p>
Contrary to hearsay, the DragElement is &lt;strong&gt;NOT&lt;/strong&gt; a male Element dressed in women's clothing.  It simply provides an easy-to-use Element pre-configured for managing Drag &amp; Drop interaction, with a few extra features.<br />

<br />

The DragElement class uses the single constructor of the Element class and configures the Element to:<br />

</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a>.<span class="me1">setIsDragDropDragElement</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a>.<span class="me1">setIsMovable</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
It also provides a way of managing multiple drop elements and reacting to the appropriately.
</p>

</div>

<h4 id="enable_disable_the_dragelement">Enable/Disable the DragElement</h4>
<div class="level4">
<pre class="code java">dragEl.<span class="me1">setIsEnabled</span><span class="br0">(</span><span class="kw4">boolean</span> isEnabled<span class="br0">)</span><span class="sy0">;</span>
dragEl.<span class="me1">getIsEnabled</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="managing_drop_elements">Managing Drop Elements</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Add an element as a valid drop Element</span>
dragEl.<span class="me1">addDropElement</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Retrieve an element(s)</span>
dragEl.<span class="me1">getDropElements</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Return all drop elements</span>
dragEl.<span class="me1">getDropElement</span><span class="br0">(</span><span class="kw4">int</span> index<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Returns a single drop element by index</span>
 
<span class="co1">// Remove drop elements</span>
dragEl.<span class="me1">removeDropElement</span><span class="br0">(</span><span class="kw4">int</span> index<span class="br0">)</span><span class="sy0">;</span>
dragEl.<span class="me1">removeDropElement</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="responding_to_incorrect_drops">Responding to Incorrect Drops</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Enable/disable springback (returns drag element to original position)</span>
dragEl.<span class="me1">setUseSpringBack</span><span class="br0">(</span><span class="kw4">boolean</span> useSpringBack<span class="br0">)</span><span class="sy0">;</span>
dragEl.<span class="me1">getUseSpringBack</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Use SlideTo effect when springback is called</span>
dragEl.<span class="me1">setUseSpringBackEffect</span><span class="br0">(</span><span class="kw4">boolean</span> useSpringBackEffect<span class="br0">)</span><span class="sy0">;</span>
dragEl.<span class="me1">getUseSpringBackEffect</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="responding_to_correct_drops">Responding to Correct Drops</h4>
<div class="level4">
<pre class="code java"><span class="co1">//Position the DragElement in the center of drop element</span>
dragEl.<span class="me1">setUseLockToDropElementCenter</span><span class="br0">(</span><span class="kw4">boolean</span> lockToDropElementCenter<span class="br0">)</span><span class="sy0">;</span>
dragEl.<span class="me1">getUseLockToDropElementCenter</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Use SlideTo effect when centering</span>
dragEl.<span class="me1">setUseLockToDropElementEffect</span><span class="br0">(</span><span class="kw4">boolean</span> useLockToDropElementEffect<span class="br0">)</span><span class="sy0">;</span>
dragEl.<span class="me1">getUseLockToDropElementEffect</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">abstract</span> <span class="kw4">void</span> onDragStart<span class="br0">(</span>MouseButtonEvent evt<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw1">abstract</span> <span class="kw4">void</span> onDragEnd<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> dropElement<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
