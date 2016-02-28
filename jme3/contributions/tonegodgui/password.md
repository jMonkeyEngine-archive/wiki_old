---
title: Password Class
---
<h3 class="sectionedit1" id="password_class">Password Class</h3>
<div class="level3">

<p>
The password class extends TextField and adds the ability to set a mask character.<br />

<br />

It uses the standard 3 constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a>.<br />

<br />

<strong>Constructor 1:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
Password pw <span class="sy0">=</span> <span class="kw1">new</span> Password<span class="br0">(</span>screen, “password”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 2:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
Password pw <span class="sy0">=</span> <span class="kw1">new</span> Password<span class="br0">(</span>screen, “password”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">150</span>, <span class="nu0">25</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 3:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
Password pw <span class="sy0">=</span> <span class="kw1">new</span> Password<span class="br0">(</span>screen, “password”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">150</span>, <span class="nu0">25</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">3</span>,<span class="nu0">3</span>,<span class="nu0">3</span>,<span class="nu0">3</span><span class="br0">)</span>,
    “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a><span class="sy0">/</span>text_field_x.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="password_specific_methods">Password specific methods:</h4>
<div class="level4">
<pre class="code java">pw.<span class="me1">setMask</span><span class="br0">(</span><span class="kw4">char</span> mask<span class="br0">)</span><span class="sy0">;</span>
pw.<span class="me1">getMask</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Returns mask character as a String</span></pre>

</div>
