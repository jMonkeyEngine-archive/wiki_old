---
title: SelectBox & ComboBox
---
<h3 class="sectionedit1" id="selectbox_combobox">SelectBox &amp; ComboBox</h3>
<div class="level3">

<p>
The combo box and select box works exactly like any other combo box or select box:
</p>
<ul>
<li class="level1"><div class="li"> They both provides the standard 3 constructors</div>
</li>
<li class="level1"><div class="li"> The only difference between the two is the SelectBox’s text field is disabled.</div>
</li>
<li class="level1"><div class="li"> The SelectBox still allows for arrow key navigation and enter select, though other key input is disabled.</div>
</li>
</ul>

</div>

<h4 id="usage_is_as_follows">Usage is as follows:</h4>
<div class="level4">
<pre class="code java">ComboBox combo <span class="sy0">=</span> <span class="kw1">new</span> ComboBox<span class="br0">(</span>
    screen,
    “SomeID”,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">5</span>,<span class="nu0">5</span><span class="br0">)</span>
<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">addListItem</span><span class="br0">(</span>“Some caption”, “Some value”<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">addListItem</span><span class="br0">(</span>“Some caption”, “Some value”<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">addListItem</span><span class="br0">(</span>“Some caption”, “Some value”<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">addListItem</span><span class="br0">(</span>“Some caption”, “Some value”<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">addListItem</span><span class="br0">(</span>“Some caption”, “Some value”<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">addListItem</span><span class="br0">(</span>“Some caption”, “Some value”<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onChange<span class="br0">(</span><span class="kw4">int</span> selectedIndex, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="hooks">Hooks:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Overridable hook for keyboard input events</span>
<span class="kw1">public</span> <span class="kw4">void</span> controlKeyPressHook<span class="br0">(</span>KeyInputEvent evt, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> text<span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span></pre>

</div>

<h4 id="set_selected_index_via_code">Set Selected Index via Code</h4>
<div class="level4">
<pre class="code java">combo.<span class="me1">setSelectedIndex</span><span class="br0">(</span><span class="kw4">int</span> index<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">getSelectedIndex</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_combo_select_boxes">Methods specific to Combo &amp; Select Boxes:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Add a list item</span>
combo.<span class="me1">addListItem</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Insert a list item</span>
combo.<span class="me1">insertListItem</span><span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Remove a list item</span>
combo.<span class="me1">removeListItem</span><span class="br0">(</span><span class="kw4">int</span> index<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">removeListItem</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption<span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">removeListIten</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Sorting methods</span>
combo.<span class="me1">sortList</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Sorts drop-down list standard alpha-numeric</span>
combo.<span class="me1">sortListNumeric</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Sorts drop-down list true numeric</span>
 
<span class="co1">// Drop-down list validation</span>
combo.<span class="me1">validateListSize</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//returns false if null or size 0, else returns true;</span>
 
<span class="co1">// Force drop-down list to hide</span>
combo.<span class="me1">hideDropDownList</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Retrieve List Items</span>
combo.<span class="me1">getSelectedListItem</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
combo.<span class="me1">getListItemByIndex</span><span class="br0">(</span><span class="kw4">int</span> index<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
