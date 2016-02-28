---
title: Panel Class
---
<h3 class="sectionedit1" id="panel_class">Panel Class</h3>
<div class="level3">

<p>
The Panel class extends Element and, like the Label class, it’s only purpose is to provide:
</p>
<ol>
<li class="level1"><div class="li"> The 3 standard constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a></div>
</li>
<li class="level1"><div class="li"> Default style information</div>
</li>
</ol>

<p>
<strong>Constructor 1:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a> panel <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a><span class="br0">(</span>screen, “panel”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 2:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a> panel <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a><span class="br0">(</span>screen, “panel”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">400</span>, <span class="nu0">300</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 3:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a> panel <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a><span class="br0">(</span>screen, “panel”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">400</span>, <span class="nu0">300</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">14</span>,<span class="nu0">14</span>,<span class="nu0">14</span>,<span class="nu0">14</span><span class="br0">)</span>,
    “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a><span class="sy0">/</span>panel_x.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The Panel class creates a resizable, movable panel (<a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:window" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:window" rel="nofollow">Window</a> without a dragbar). The entire panel is clickable for moving unless otherwise covered by added child Elements that have not called:
</p>
<pre class="code java">setIgnoreMouse<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can disable any of the default behaviors of the Panel class by using the methods described in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:element" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:element" rel="nofollow">Element</a> class.
</p>

</div>
