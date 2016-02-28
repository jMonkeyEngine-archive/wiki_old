---
title: Button Class
---
<h3 class="sectionedit1" id="button_class">Button Class</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Buttons have a default state, a hover state and a pressed state.</div>
</li>
<li class="level1"><div class="li"> They implement the tonegodGUI MouseButtonListener &amp; MouseFocusListener interfaces</div>
</li>
<li class="level1"><div class="li"> They provide an optional stillPressed event</div>
</li>
<li class="level1"><div class="li"> Can either consist of text label or icon</div>
</li>
<li class="level1"><div class="li"> They can be set to Toggle mode.</div>
</li>
<li class="level1"><div class="li"> They have default effects set for Hover, Pressed &amp; LoseFocus</div>
</li>
<li class="level1"><div class="li"> Buttons are an abstract class providing methods for handling user input</div>
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
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a> button <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a><span class="br0">(</span>screen, “button”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 2:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a> button <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a><span class="br0">(</span>screen, “button”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">100</span>, <span class="nu0">25</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 3:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a> button <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a><span class="br0">(</span>screen, “button”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">100</span>, <span class="nu0">25</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">5</span>,<span class="nu0">5</span>,<span class="nu0">5</span>,<span class="nu0">5</span><span class="br0">)</span>,
    “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+button"><span class="kw3">Button</span></a><span class="sy0">/</span>button_u_x.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="hover_state">Hover State</h4>
<div class="level4">

<p>
You can override the default hover state using the following method:
</p>
<pre class="code java"><span class="co1">// Override the information used by the hover effect</span>
button.<span class="me1">setButtonHoverInfo</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> imagePath, ColorRGBA textHoverColor<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="pressed_state">Pressed State</h4>
<div class="level4">

<p>
You can override the default pressed state using the following method:
</p>
<pre class="code java"><span class="co1">// Override the information used by the pressed effect</span>
button.<span class="me1">setButtonPressedInfo</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> imagePath, ColorRGBA textPressedColor<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onButtonMouseLeftDown<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> toggled<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw4">void</span> onButtonMouseRightDown<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> toggled<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw4">void</span> onButtonMouseLeftUp<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> toggled<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw4">void</span> onButtonMouseRightUp<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> toggled<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw4">void</span> onButtonFocus<span class="br0">(</span>MouseMotionEvent evt<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw4">void</span> onButtonLostFocus<span class="br0">(</span>MouseMotionEvent evt<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw4">void</span> onButtonStillPressedInterval<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="adding_an_icon">Adding an Icon</h4>
<div class="level4">

<p>
In place of text, you can use an image icon by calling the following method:
</p>
<pre class="code java">button.<span class="me1">setButtonIcon</span><span class="br0">(</span><span class="kw4">float</span> width, <span class="kw4">float</span> height, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> texturePath<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_button_class">Methods specific to the Button class</h4>
<div class="level4">
<pre class="code java"><span class="co1">//Toggle info</span>
button.<span class="me1">setIsToggleButton</span><span class="br0">(</span><span class="kw4">boolean</span> isToggleButton<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Also provides a getter</span>
button.<span class="me1">getIsToggleButton</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
button.<span class="me1">getIsToggled</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Additional state info</span>
button.<span class="me1">clearAltImages</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Enabling/disabling invternal calls (StillPressed event)</span>
button.<span class="me1">setInterval</span><span class="br0">(</span><span class="kw4">float</span> intervalsPerSecond<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 0 deactivates</span></pre>

<p>
</p><p></p><div class="noteclassic">When not otherwise specified, use the primitive Element method for setting the text of a control. For instance, to set the text of the Button instance, you simply call:
</div>

<pre class="code java">button.<span class="me1">setText</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> text<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT1 SECTION "Button Class" [1-3113] -->
<h3 class="sectionedit2" id="buttonadapter_class">ButtonAdapter Class</h3>
<div class="level3">

<p>
</p><p></p><div class="notetip">Tips for using the Button class
</div>

<ol>
<li class="level1"><div class="li"> Create a button</div>
</li>
<li class="level1"><div class="li"> Implement all abstract methods</div>
</li>
<li class="level1"><div class="li"> Write your code for the event handlers you wish to use</div>
</li>
<li class="level1"><div class="li"> Change the Button to a ButtonAdapter</div>
</li>
<li class="level1"><div class="li"> Remove all unused event handler methods</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "ButtonAdapter Class" [3114-] -->
