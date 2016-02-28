---
title: ScrollArea class
---
<h3 class="sectionedit1" id="scrollarea_class">ScrollArea class</h3>
<div class="level3">

<p>
Utilizes the standard 3 constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a> with the addition of a single boolean:
</p>
<ul>
<li class="level1"><div class="li"> isTextOnly – appended to the end of the param list for each constructor</div>
</li>
</ul>

<p>
The additional parameter is appended to the end of the parameter list for each of the 3 constructors, like so:
</p>
<pre class="code java"><span class="co3">/**
  * Parameters:
  * Screen screen
  * String UID
  * Vector2f position
  * boolean isTextOnly
  */</span>
ScrollArea scrollArea <span class="sy0">=</span> <span class="kw1">new</span> ScrollArea<span class="br0">(</span>
    screen,
    “SomeID”,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw2">true</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>NOTE:</strong><br />

The ScrollArea implement Vertical Scrolling only. Why? Because I was lazy. Eventually I will add Horizontal scrolling as well.<br />

<br />

ScrollArea's can be implemented in two ways: Text Only, or an inner element that can contain nested Elements.
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
scrollArea.<span class="me1">getIsTextOnly</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
scrollArea.<span class="me1">setPadding</span><span class="br0">(</span><span class="kw4">float</span> padding<span class="br0">)</span><span class="sy0">;</span>
scrollArea.<span class="me1">getPadding</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
scrollArea.<span class="me1">getScrollableHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Pointer to VScrollBar</span>
scrollArea.<span class="me1">getVScrollBar</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//Scrolling methods</span>
scrollArea.<span class="me1">scrollYTo</span><span class="br0">(</span><span class="kw4">float</span> y<span class="br0">)</span><span class="sy0">;</span>
scrollArea.<span class="me1">scrollYBy</span><span class="br0">(</span><span class="kw4">float</span> yInc<span class="br0">)</span><span class="sy0">;</span>
scrollArea.<span class="me1">scrollToTop</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
scrollArea.<span class="me1">scrollToBottom</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
