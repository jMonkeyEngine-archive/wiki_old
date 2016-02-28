---
title: Indicator Class
---
<h3 class="sectionedit1" id="indicator_class">Indicator Class</h3>
<div class="level3">

<p>
An indicator is a highly customizable progress bar, which can be used showing/displaying player stats, etc
</p>

<p>
The Indicator uses the 3 standard constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a> with the addition of one extra parameter:
</p>
<ul>
<li class="level1"><div class="li"> Orientation appended to the end of the param list for each</div>
</li>
</ul>

<p>
<strong>Features include:</strong><br />

</p>
<ul>
<li class="level1"><div class="li"> Clipping + an alpha mask to create any shaped indicator you would like</div>
</li>
<li class="level1"><div class="li"> Display the indicator in any color you choose.</div>
</li>
<li class="level1"><div class="li"> Image based indicators in place of color+clipping</div>
</li>
<li class="level1"><div class="li"> An overlay image for transparent indicator containers</div>
</li>
</ul>

</div>

<h4 id="constructor_example">Constructor example:</h4>
<div class="level4">
<pre class="code java"><span class="co3">/**
  * Parameters:
  * Screen screen
  * String UID
  * Vector2f position
  * Orientation orientation
  */</span>
Indicator ind <span class="sy0">=</span> <span class="kw1">new</span> Indicator<span class="br0">(</span>
    screen,
    “SomeID”,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">10</span>,<span class="nu0">10</span><span class="br0">)</span>,
   Orientation.<span class="me1">VERTICAL</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="changing_reshaping_the_indicator">Changing &amp; Reshaping the Indicator</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Using an image in place of a colored indicator</span>
ind.<span class="me1">setBaseImage</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> imgPath<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Use a clipped image for the indicator</span>
ind.<span class="me1">setIndicatorImage</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> imgPath<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Changing the color of the indicator or colorize the image-based indicator</span>
ind.<span class="me1">setIndicatorColor</span><span class="br0">(</span>ColorRGBA indicatorColor<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Add padding (margins) to the indicator portion of the indicator</span>
ind.<span class="me1">setIndicatorPadding</span><span class="br0">(</span>Vector4f padding<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Reshape the indicator !IMPORTANT! setIndicatorAlphaMap is now @Deprecated, use this instead:</span>
ind.<span class="me1">setAlphaMap</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> alphaMapPath<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_indicator_class">Methods specific to the Indicator class</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Get the indicators oritentation</span>
ind.<span class="me1">getOrientation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Adjust value ranges</span>
ind.<span class="me1">setMaxValue</span><span class="br0">(</span><span class="kw4">float</span> maxValue<span class="br0">)</span><span class="sy0">;</span>
ind.<span class="me1">setCurrentValue</span><span class="br0">(</span><span class="kw4">float</span> currentValue<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Get current info</span>
ind.<span class="me1">getCurrentPercentage</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
ind.<span class="me1">getCurrentValue</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
ind.<span class="me1">getMaxValue</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
ind.<span class="me1">getTextDisplayElement</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Return the text element for formatting purposes</span>
ind.<span class="me1">setDisplayValues</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Display value in format:  current/max or 10/100</span>
ind.<span class="me1">setDisplayPercentage</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Displays percentage:  82% etc</span>
ind.<span class="me1">setHideText</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// removes display text (default)</span></pre>

</div>
<!-- EDIT1 SECTION "Indicator Class" [1-2131] -->
<h3 class="sectionedit2" id="indicator_examples">Indicator Examples</h3>
<div class="level3">

<p>
Cut &amp; Paste the following code into the simpleInitApp method of a new JME project.  Use the slider to adjust the indicator.
</p>
<pre class="code java">flyCam.<span class="me1">setDragToRotate</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
inputManager.<span class="me1">setCursorVisible</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
 
screen <span class="sy0">=</span> <span class="kw1">new</span> Screen<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">addControl</span><span class="br0">(</span>screen<span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">final</span> ColorRGBA color <span class="sy0">=</span> <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">final</span> Indicator ind <span class="sy0">=</span> <span class="kw1">new</span> Indicator<span class="br0">(</span>
    screen,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">50</span>,<span class="nu0">50</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">300</span>,<span class="nu0">30</span><span class="br0">)</span>,
    Orientation.<span class="me1">HORIZONTAL</span>
<span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onChange<span class="br0">(</span><span class="kw4">float</span> currentValue, <span class="kw4">float</span> currentPercentage<span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
ind.<span class="me1">setBaseImage</span><span class="br0">(</span>screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"Window"</span><span class="br0">)</span>.<span class="me1">getString</span><span class="br0">(</span><span class="st0">"defaultImg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//ind.setIndicatorImage(screen.getStyle("Window").getString("defaultImg"));</span>
ind.<span class="me1">setIndicatorColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">randomColor</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
ind.<span class="me1">setAlphaMap</span><span class="br0">(</span>screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"Indicator"</span><span class="br0">)</span>.<span class="me1">getString</span><span class="br0">(</span><span class="st0">"alphaImg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
ind.<span class="me1">setIndicatorPadding</span><span class="br0">(</span><span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">7</span>,<span class="nu0">7</span>,<span class="nu0">7</span>,<span class="nu0">7</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
ind.<span class="me1">setMaxValue</span><span class="br0">(</span><span class="nu0">100</span><span class="br0">)</span><span class="sy0">;</span>
ind.<span class="me1">setDisplayPercentage</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
screen.<span class="me1">addElement</span><span class="br0">(</span>ind<span class="br0">)</span><span class="sy0">;</span>
 
Slider slider <span class="sy0">=</span> <span class="kw1">new</span> Slider<span class="br0">(</span>screen, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">100</span>,<span class="nu0">100</span><span class="br0">)</span>, Orientation.<span class="me1">HORIZONTAL</span>, <span class="kw2">true</span><span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onChange<span class="br0">(</span><span class="kw4">int</span> selectedIndex, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw4">float</span> blend <span class="sy0">=</span> selectedIndex<span class="sy0">*</span>0.01f<span class="sy0">;</span>
        color.<span class="me1">interpolate</span><span class="br0">(</span>ColorRGBA.<span class="me1">Red</span>, ColorRGBA.<span class="me1">Green</span>, blend<span class="br0">)</span><span class="sy0">;</span>
        ind.<span class="me1">setIndicatorColor</span><span class="br0">(</span>color<span class="br0">)</span><span class="sy0">;</span>
        ind.<span class="me1">setCurrentValue</span><span class="br0">(</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+integer"><span class="kw3">Integer</span></a><span class="br0">)</span>value<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
 
screen.<span class="me1">addElement</span><span class="br0">(</span>slider<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<a href="/resources/jme3-contributions-tonegodgui-indicatorexample.png" class="media" title="jme3:contributions:tonegodgui:indicatorexample.png"><img src="/resources/jme3-contributions-tonegodgui-indicatorexample.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT2 SECTION "Indicator Examples" [2132-] -->
