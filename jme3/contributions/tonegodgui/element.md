---
title: The Element Class
---
<h3 class="sectionedit1" id="the_element_class">The Element Class</h3>
<div class="level3">

<p>
All controls are extensions of the Element class and thus, provide common methods for handling common features.  Before getting to specific controls, I thought it might be a good idea to cover some of the common methods for changing basic properties… such as: text, etc.<br />

<br />

</p>

</div>

<h4 id="constructors">Constructors</h4>
<div class="level4">

<p>
The Element class only provides a single constructor using all 6 of the common parameters:<br />

</p>
<pre class="code java"><span class="co3">/**
  * Parameters:
  * Screen screen
  * String UID
  * Vector2f position
  * Vector2f dimensions
  *  Vector4f resizeBorders
  * String defaultImgPath
  */</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> el <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a><span class="br0">(</span>
    screen,
    “SomeID”,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">5</span>,<span class="nu0">5</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">100</span>,<span class="nu0">100</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">5</span>,<span class="nu0">5</span>,<span class="nu0">5</span>,<span class="nu0">5</span><span class="br0">)</span>,
    “someImgPath.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Note:</strong><br />

All setter provide getters.
</p>

</div>

<h4 id="text_font_related_methods">Text/Font Related Methods</h4>
<div class="level4">
<pre class="code java">element.<span class="me1">setFont</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> font path<span class="br0">)</span>
element.<span class="me1">setFontSize</span><span class="br0">(</span><span class="kw4">float</span> fontSize<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setFontColor</span><span class="br0">(</span>ColorRGBA fontColor<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setTextAlign</span><span class="br0">(</span>BitmapFont.<span class="me1">Align</span> textAlign<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setTextVAlign</span><span class="br0">(</span>BitmapFont.<span class="me1">VAlign</span> textVAlign<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setTextWrap</span><span class="br0">(</span>LineWrapMode textWrap<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setTextPosition</span><span class="br0">(</span><span class="kw4">float</span> x, <span class="kw4">float</span> y<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setTextPadding</span><span class="br0">(</span><span class="kw4">float</span> textPadding<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setText</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> text<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="element_positions_dimensions_related_methods">Element Positions/Dimensions Related Methods</h4>
<div class="level4">
<pre class="code java">element.<span class="me1">setPosition</span><span class="br0">(</span>Vector2f position<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setPosition</span><span class="br0">(</span><span class="kw4">float</span> x, <span class="kw4">float</span> y<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setX</span><span class="br0">(</span><span class="kw4">float</span> x<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setY</span><span class="br0">(</span><span class="kw4">float</span> y<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setDimensions</span><span class="br0">(</span>Vector2f dimensions<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setDimensions</span><span class="br0">(</span><span class="kw4">float</span> w, <span class="kw4">float</span> h<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setWidth</span><span class="br0">(</span><span class="kw4">float</span> width<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setHeight</span><span class="br0">(</span><span class="kw4">float</span> height<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">setMinDimensions</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="kw4">float</span> x, <span class="kw4">float</span> y<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="other_positions_dimensions_related_methods">Other Positions/Dimensions Related Methods</h4>
<div class="level4">

<p>
Since position and dimensions are relative to the Element’s parent Element, there are additional getters provided for retrieving absolute X, Y, Width &amp; Height (absolute positions start from screen coords 0, 0)
</p>
<pre class="code java">element.<span class="me1">getAbsoluteX</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">getAbsoluteY</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">getAbsoluteWidth</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">getAbsoluteHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="child_elements">Child Elements</h4>
<div class="level4">

<p>
There are additional methods that provide recursive updates to child Elements:
</p>
<pre class="code java">element.<span class="me1">moveTo</span><span class="br0">(</span><span class="kw4">float</span> x, <span class="kw4">float</span> y<span class="br0">)</span><span class="sy0">;</span>
element.<span class="me1">resize</span><span class="br0">(</span><span class="kw4">float</span> diffX, floar diffY, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a>.<span class="me1">Borders</span> dir<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="element_display_methods">Element Display Methods</h4>
<div class="level4">
<pre class="code java">el.<span class="me1">show</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
el.<span class="me1">showWithEffect</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
el.<span class="me1">hide</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
el.<span class="me1">hideWithEffect</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="hooks">Hooks</h4>
<div class="level4">

<p>
Overridable hooks are provided for default behavoirs:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> controlResizeHook<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span>
<span class="kw1">public</span> <span class="kw4">void</span> controlMoveHook<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span>
<span class="kw1">public</span> <span class="kw4">void</span> controlCleanupHook<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span></pre>

</div>

<h4 id="clipping">Clipping</h4>
<div class="level4">

<p>
To have the element be clipped by another element's bounds, use:
</p>
<pre class="code java">el.<span class="me1">setClippingLayer</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To set the clipping layer of the Element and propagate clipping to all children of the Element, use:
</p>
<pre class="code java">el.<span class="me1">setControlClippingLayer</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="accessing_the_element_s_components">Accessing the Element's Components</h4>
<div class="level4">
<pre class="code java">el.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// The element's Geometry</span>
el.<span class="me1">getModel</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// The element's mesh</span>
el.<span class="me1">getTextElement</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// BitmapText (null if setText() has not been previously called)</span></pre>

</div>

<h4 id="modifying_the_material">Modifying the Material</h4>
<div class="level4">

<p>
There are plenty of methods that allow for modifying the look &amp; feel of the Element:
</p>
<pre class="code java"><span class="co1">// Accessing the element's material</span>
el.<span class="me1">getElementMaterial</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Updating the texture:</span>
el.<span class="me1">setColorMap</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> imgPath<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// To modify the element's base texture</span>
el.<span class="me1">setAlphaMap</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> imgPath<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// To set the element's alphamap</span>
 
<span class="co1">// Using gradient fills:</span>
el.<span class="me1">getModel</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setGradientFillHorizontal</span><span class="br0">(</span>ColorRGBA start, ColorRGBA end<span class="br0">)</span><span class="sy0">;</span>
el.<span class="me1">getModel</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setGradientFillVertical</span><span class="br0">(</span>ColorRGBA start, ColorRGBA end<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Defining each vertex color</span>
el.<span class="me1">getModel</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setColorBuffer</span><span class="br0">(</span>FloatBuffer colors<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Adjusting the element's alpha</span>
el.<span class="me1">setGlobalAlpha</span><span class="br0">(</span><span class="kw4">float</span> alpha<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="effect_related_methods">Effect Related Methods</h4>
<div class="level4">
<pre class="code java">el.<span class="me1">addEffect</span><span class="br0">(</span>Effect effect<span class="br0">)</span><span class="sy0">;</span>
el.<span class="me1">removeEffect</span><span class="br0">(</span>Effect.<span class="me1">EffectEvent</span> effectEvent<span class="br0">)</span><span class="sy0">;</span>
el.<span class="me1">populateEffects</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> styleName<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Loads all effects associated with a Style</span></pre>

</div>

<h4 id="drag_drop_related_methods">Drag &amp; Drop Related Methods</h4>
<div class="level4">
<pre class="code java">el.<span class="me1">setIsDragDropDragElement</span><span class="br0">(</span><span class="kw4">boolean</span> isDragElement<span class="br0">)</span><span class="sy0">;</span>
el.<span class="me1">setIsDragDropDropElement</span><span class="br0">(</span><span class="kw4">boolean</span> isDropElement<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// for retrieving the current drop object under the element, use:</span>
screen.<span class="me1">getDropObject</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="noteclassic">You must manage your own list of acceptable drop objects as any Element flagged as isDropObject will be returned
</div>


</div>

<h4 id="storing_retrieving_custom_data">Storing &amp; Retrieving  Custom Data</h4>
<div class="level4">
<pre class="code java">el.<span class="me1">setElementUserData</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> data<span class="br0">)</span><span class="sy0">;</span>
el.<span class="me1">getElementUserData</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
