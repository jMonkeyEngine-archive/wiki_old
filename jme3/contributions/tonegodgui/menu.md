---
title: Menu Class
---
<h3 class="sectionedit1" id="menu_class">Menu Class</h3>
<div class="level3">

<p>
The Menu class extends ScrollArea as Menu’s can be resizable and scrollable if the behaviors are enabled.<br />

<br />

Menus contain a list of MenuItems, which provide mapping for sub-menus. This implementation of menu’s negates the need for any form of Menu Manager as the Screen, by default, handles delegating Mouse Events and therefore is (in a sense) a Menu Manager. Menus utilize a single text element with separate highlight element, to keep the rendered meshes to count of 3 for any length menu.<br />

<br />

Features:
</p>
<ul>
<li class="level1"><div class="li"> Unlimited menu item list</div>
</li>
<li class="level1"><div class="li"> Unlimited sub-menu mapping</div>
</li>
<li class="level1"><div class="li"> MenuItem toggle states (semi-work-in-progress here)</div>
</li>
</ul>

<p>
Menu utilizes the standard 3 constructors as shown in the <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:contributions:tonegodgui:quickstart" rel="nofollow">Quick Start Guide</a> with the addition of a single boolean:
</p>
<ul>
<li class="level1"><div class="li"> isScrollable – appended to the end of the parameter list in each constructor</div>
</li>
</ul>

</div>

<h4 id="abstract_event_methods">Abstract Event Methods:</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onMenuItemClicked<span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_menu_class">Methods specific to the Menu Class:</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Menu manipulation</span>
menu.<span class="me1">addMenuItem</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> subMenu<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// null if no sub-menu</span>
menu.<span class="me1">addMenuItem</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> subMenu, <span class="kw4">boolean</span> isToggleItem<span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">addMenuItem</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> subMenu, <span class="kw4">boolean</span> isToggleItem, <span class="kw4">boolean</span> isToggled<span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">insertMenuItem</span><span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> subMenu<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// null if no sub-menu</span>
menu.<span class="me1">insertMenuItem</span><span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> subMenu, <span class="kw4">boolean</span> isToggleItem<span class="br0">)</span>
menu.<span class="me1">insertMenuItem</span><span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> subMenu, <span class="kw4">boolean</span> isToggleItem, <span class="kw4">boolean</span> isToggled<span class="br0">)</span>
menu.<span class="me1">removeMenuItem</span><span class="br0">(</span><span class="kw4">int</span> index<span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">removeMenuItem</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> caption<span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">removeMenuItem</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value<span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">removeFirstMenuItem</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">removeLastMenuItem</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Configuration related methods</span>
menu.<span class="me1">setMenuOverhang</span><span class="br0">(</span><span class="kw4">float</span> menuOverhang<span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">getMenuOverhang</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">getMenuItemHeight</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">getMenuPadding</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">setPreferredSize</span><span class="br0">(</span>Vector2f preferredSize<span class="br0">)</span>
 
<span class="co1">//Menu item related methods</span>
menu.<span class="me1">getMenuItems</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// point to menu item list</span>
menu.<span class="me1">getMenuItem</span><span class="br0">(</span><span class="kw4">int</span> index<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Hide/show methods</span>
menu.<span class="me1">showMenu</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> caller, <span class="kw4">float</span> x, <span class="kw4">float</span> y<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Caller is null if not show by another menu</span>
menu.<span class="me1">hideMenu</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Setting &amp; retrieving an external caller element</span>
menu.<span class="me1">setCallerElement</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> el<span class="br0">)</span><span class="sy0">;</span>
menu.<span class="me1">getCallerElement</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="hooks">Hooks</h4>
<div class="level4">
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> controlHideHook<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span></pre>

</div>
<!-- EDIT1 SECTION "Menu Class" [1-2493] -->
<h3 class="sectionedit2" id="menu_examples">Menu Examples:</h3>
<div class="level3">

<p>
Cut &amp; Paste the code below into the simpleInitApp() method of a new JME project to try it out.
</p>
<pre class="code java">flyCam.<span class="me1">setDragToRotate</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
inputManager.<span class="me1">setCursorVisible</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
 
screen <span class="sy0">=</span> <span class="kw1">new</span> Screen<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">addControl</span><span class="br0">(</span>screen<span class="br0">)</span><span class="sy0">;</span>
 
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> subMenu <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a><span class="br0">(</span>
    screen,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span>,
    <span class="kw2">false</span>
<span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onMenuItemClicked<span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <span class="kw4">boolean</span> isToggled<span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
<span class="co1">// Add a menu item</span>
subMenu.<span class="me1">addMenuItem</span><span class="br0">(</span><span class="st0">"Some string caption 1"</span>, <span class="kw2">null</span>, <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Add a toggle-able menu item (checkbox)</span>
subMenu.<span class="me1">addMenuItem</span><span class="br0">(</span><span class="st0">"Some string caption 2"</span>, <span class="kw2">null</span>, <span class="kw2">null</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Add a toggle-able menu item and set the default state of the checkbox to checked</span>
subMenu.<span class="me1">addMenuItem</span><span class="br0">(</span><span class="st0">"Some string caption 3"</span>, <span class="kw2">null</span>, <span class="kw2">null</span>, <span class="kw2">true</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">addElement</span><span class="br0">(</span>subMenu<span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> menu <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a><span class="br0">(</span>
    screen,
    <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span>,
    <span class="kw2">false</span>
<span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onMenuItemClicked<span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <span class="kw4">boolean</span> isToggled<span class="br0">)</span> <span class="br0">{</span>  <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
<span class="co1">// Add subMenu as a sub-menu to this menu item</span>
menu.<span class="me1">addMenuItem</span><span class="br0">(</span><span class="st0">"Some caption"</span>, <span class="kw2">null</span>, subMenu<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">addElement</span><span class="br0">(</span>menu<span class="br0">)</span><span class="sy0">;</span>
 
ButtonAdapter b <span class="sy0">=</span> <span class="kw1">new</span> ButtonAdapter<span class="br0">(</span>screen, <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">50</span>,<span class="nu0">50</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onButtonMouseLeftUp<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> isToggled<span class="br0">)</span> <span class="br0">{</span>
        menu.<span class="me1">showMenu</span><span class="br0">(</span><span class="kw2">null</span>, getAbsoluteX<span class="br0">(</span><span class="br0">)</span>, getAbsoluteY<span class="br0">(</span><span class="br0">)</span><span class="sy0">-</span>menu.<span class="me1">getHeight</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
b.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Show Menu"</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">addElement</span><span class="br0">(</span>b<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT2 SECTION "Menu Examples:" [2494-] -->
