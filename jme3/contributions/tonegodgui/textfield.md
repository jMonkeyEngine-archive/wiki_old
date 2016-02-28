---
title: TextField Class
---
<h3 class="sectionedit1" id="textfield_class">TextField Class</h3>
<div class="level3">

<p>
Textfields are single line text input fields, that provide the following functionality:
</p>
<ul>
<li class="level1"><div class="li"> Caret &amp; Text Range</div>
</li>
<li class="level1"><div class="li"> Mouse select</div>
</li>
<li class="level1"><div class="li"> Keyboard nav using:</div>
<ul>
<li class="level2"><div class="li"> arrows (nav by letter)</div>
</li>
<li class="level2"><div class="li"> SHIFT+arrows (text range by latter)</div>
</li>
<li class="level2"><div class="li"> CTRL+arrows (nav by word)</div>
</li>
<li class="level2"><div class="li"> SHIFT+CTRL+arrows (text range by word)</div>
</li>
<li class="level2"><div class="li"> etc.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Cut &amp; Paste</div>
</li>
</ul>

<p>
<strong>NOTE:</strong><br />

This control is still a work in progress and will be updated as either time permits or issues arise.  There is a known issue with the Cut &amp; Paste function as of right now and it has been disabled.<br />

<br />

TextFields provide the standard 3 constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a>.<br />

<br />

<strong>Constructor 1:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Parameters:
  * Screen screen,
  * String UID,
  * Vector2f position
  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a> text <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a><span class="br0">(</span>screen, “text”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 2:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameter:
  * Vector2f dimensions  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a> text <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a><span class="br0">(</span>screen, “text”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">150</span>, <span class="nu0">25</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Constructor 3:</strong><br />

</p>
<pre class="code java"><span class="co3">/** Additional Parameters:
  * Vector4f resizeBorders,
  * String defaultImg
  */</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a> text <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a><span class="br0">(</span>screen, “text”, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">15</span>, <span class="nu0">15</span><span class="br0">)</span>, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">150</span>, <span class="nu0">25</span><span class="br0">)</span>,
    <span class="kw1">new</span> Vector4f<span class="br0">(</span><span class="nu0">3</span>,<span class="nu0">3</span>,<span class="nu0">3</span>,<span class="nu0">3</span><span class="br0">)</span>,
    “tonegod<span class="sy0">/</span>gui<span class="sy0">/</span>style<span class="sy0">/</span>def<span class="sy0">/</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a><span class="sy0">/</span>text_field_x.<span class="me1">png</span>”
<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="validations_rules">Validations &amp; Rules</h4>
<div class="level4">

<p>
TextFields can be set to a specific Type using:
</p>
<pre class="code java">text.<span class="me1">setType</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+textfield"><span class="kw3">TextField</span></a>.<span class="me1">Type</span> type<span class="br0">)</span><span class="sy0">;</span></pre>
<div class="table sectionedit2"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Rule </th><th class="col1"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Type.DEFAULT </td><td class="col1"> Accept all characters </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Type.ALPHA </td><td class="col1"> Accept only lower case, uppercase alpha character + spacebar </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Type.ALPHA_NOSPACE </td><td class="col1"> Accept only lower case, uppercase alpha character - no spacebar </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Type.NUMERIC </td><td class="col1"> Accept only numeric values + decimal </td>
	</tr>
	<tr class="row5">
		<td class="col0"> Type.ALPHANUMERIC </td><td class="col1"> Apply both ALPHA and NUMERIC rules </td>
	</tr>
	<tr class="row6">
		<td class="col0"> Type.ALPHANUMERIC_NOSPACE </td><td class="col1"> Apply both ALPHA_NOSPACE and NUMERIC rules </td>
	</tr>
	<tr class="row7">
		<td class="col0"> Type.EXCLUDE_SPECIAL </td><td class="col1"> Exclude all spacial characters </td>
	</tr>
	<tr class="row8">
		<td class="col0"> Type.EXCLUDE_CUSTOM </td><td class="col1"> Exclude all user defined character (see below) </td>
	</tr>
	<tr class="row9">
		<td class="col0"> Type.INCLUDE_CUSTOM </td><td class="col1"> Accept only user defined characters (see below) </td>
	</tr>
</table></div>
<!-- EDIT2 TABLE [1582-2207] -->
<p>
To define a custom validation for Type.EXCLUDE_CUSTOM or Type.INCLUDE_CUSTOM, use the following method:
</p>
<pre class="code java">text.<span class="me1">setCustomValidation</span><span class="br0">(</span><span class="st0">"Character List to include/exclude"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can also limit the number of characters the TextField will accept using:
</p>
<pre class="code java">text.<span class="me1">setMaxLimit</span><span class="br0">(</span><span class="kw4">int</span> maxLimit<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can force upper and lower case by using:
</p>
<pre class="code java">text.<span class="me1">setForceUpperCase</span><span class="br0">(</span><span class="kw4">boolean</span> forceUpperCase<span class="br0">)</span><span class="sy0">;</span>
text.<span class="me1">setForceLowerCase</span><span class="br0">(</span><span class="kw4">boolean</span> forceLowerCase<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_textfield_class">Methods specific to the TextField class:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Get the TextField text</span>
text.<span class="me1">getText</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Set the TextField text !IMPORTANT! setTextFieldText is now @Deprecated, use the following instead:</span>
text.<span class="me1">setText</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> s<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Retrieve numeric values (all numeric parsers throw NumberFormatException</span>
text.<span class="me1">parseInt</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
text.<span class="me1">parseFloat</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
text.<span class="me1">parseShort</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
text.<span class="me1">parseDouble</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
text.<span class="me1">parseLong</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="hooks">Hooks:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> controlKeyPressHook<span class="br0">(</span>KeyInputEvent evt, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> text<span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span></pre>

</div>
