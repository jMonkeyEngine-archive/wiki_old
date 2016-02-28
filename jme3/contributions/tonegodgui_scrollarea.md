---
title: ScrollArea class
---
<h3 class="sectionedit1" id="scrollarea_class">ScrollArea class</h3>
<div class="level3">

<p>
Utilizes the standard 3 constructors as shown in the  with the addition of a single boolean:
</p>
<ul>
<li class="level1"><div class="li"> isTextOnly – appended to the end of the param list for each constructor</div>
</li>
</ul>

<p>
<strong>NOTE:</strong><br />

The scrollArea implement Vertical Scrolling only. Why? Because I was lazy. Eventually I will add Horizontal scrolling as well.<br />

<br />

ScrollArea s can be implemented in two ways: Text Only, or an inner element that can contain nested Elements.
</p>
<ol>
<li class="level1"><div class="li"> The text only version uses the Element setText() method for adding to the scrollable content.</div>
</li>
<li class="level1"><div class="li"> The inner Element method uses addScrollableChild() as well as setText() to add scrollable content</div>
</li>
</ol>

<p>
When using a scroll area for building Custom Controls, consider the potential uses of the ScrollArea to alleviate unnecessary overhead. If the text only version will suffice… USE IT! No reason to create the extra Element if it will not be used.<br />

</p>

</div>

<h4 id="methods_specific_to_the_scrollarea_class">Methods specific to the ScrollArea class:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Config methods</span>
getIsTextOnly<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
setPadding<span class="br0">(</span><span class="kw4">float</span> padding<span class="br0">)</span><span class="sy0">;</span>
getPadding<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
getScrollableHeight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Pointer to VScrollBar</span>
getVScrollBar<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Scrolling methods</span>
scrollYTo<span class="br0">(</span><span class="kw4">float</span> y<span class="br0">)</span><span class="sy0">;</span>
scrollYBy<span class="br0">(</span><span class="kw4">float</span> yInc<span class="br0">)</span><span class="sy0">;</span>
scrollToTop<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
scrollToBottom<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
