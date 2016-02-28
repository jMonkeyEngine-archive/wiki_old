---
title: Creating Custom Controls
---
<h3 class="sectionedit1" id="creating_custom_controls">Creating Custom Controls</h3>
<div class="level3">

<p>
In this section, I'm going to walk you through creating a custom control and hopefully pass along a few tip and help standardize how controls are built.  This way (if you feel so inclined) you can share your controls with other and all will know exactly how to use your control.<br />

<br />

</p>

</div>

<h4 id="a_reusable_contextual_menu">A Reusable Contextual Menu</h4>
<div class="level4">

<p>
We're going to be building a reusable contextual right-click menu that will:
</p>
<ul>
<li class="level1"><div class="li"> lock and unlock certain features of a standard window/panel</div>
</li>
<li class="level1"><div class="li"> Allow you to add/remove menu items specific to each window as it is called.</div>
</li>
</ul>

</div>

<h5 id="step_1adding_the_framework_for_the_new_class">STEP 1: Adding the framework for the new class.</h5>
<div class="level5">

<p>
First, we'll set up the class and add the three standard constructors.  We'll be using the default Menu style information.  The class will remain abstract to leverage the existing callback method of the super class Menu.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">abstract</span> <span class="kw1">class</span> ContextualMenu <span class="kw1">extends</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+menu"><span class="kw3">Menu</span></a> <span class="br0">{</span>
    <span class="kw1">public</span> ContextualMenu<span class="br0">(</span>Screen screen, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+uid"><span class="kw3">UID</span></a>, Vector2f position, <span class="kw4">boolean</span> isScrollable<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">this</span><span class="br0">(</span>screen, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+uid"><span class="kw3">UID</span></a>, position,
            screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"Menu"</span><span class="br0">)</span>.<span class="me1">getVector2f</span><span class="br0">(</span><span class="st0">"defaultSize"</span><span class="br0">)</span>,
            screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"Menu"</span><span class="br0">)</span>.<span class="me1">getVector4f</span><span class="br0">(</span><span class="st0">"resizeBorders"</span><span class="br0">)</span>,
            screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"Menu"</span><span class="br0">)</span>.<span class="me1">getString</span><span class="br0">(</span><span class="st0">"defaultImg"</span><span class="br0">)</span>,
            isScrollable
        <span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> ContextualMenu<span class="br0">(</span>Screen screen, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+uid"><span class="kw3">UID</span></a>, Vector2f position, Vector2f dimensions, 
            <span class="kw4">boolean</span> isScrollable<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">this</span><span class="br0">(</span>screen, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+uid"><span class="kw3">UID</span></a>, position, dimensions,
            screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"Menu"</span><span class="br0">)</span>.<span class="me1">getVector4f</span><span class="br0">(</span><span class="st0">"resizeBorders"</span><span class="br0">)</span>,
            screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"Menu"</span><span class="br0">)</span>.<span class="me1">getString</span><span class="br0">(</span><span class="st0">"defaultImg"</span><span class="br0">)</span>,
            isScrollable
        <span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> ContextualMenu<span class="br0">(</span>Screen screen, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+uid"><span class="kw3">UID</span></a>, Vector2f position, Vector2f dimensions, 
            Vector4f resizeBorders, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> defaultImg, <span class="kw4">boolean</span> isScrollable<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// Call the super class to construct our basic menu</span>
        <span class="kw1">super</span><span class="br0">(</span>screen, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+uid"><span class="kw3">UID</span></a>, position, dimensions, resizeBorders, defaultImg, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>

<h5 id="step_2adding_a_public_method_for_building_standard_options">STEP 2: Adding a public method for building standard options</h5>
<div class="level5">

<p>
This method will be used by calling windows to ensure the menu starts with only the default options.  If the particular calling window needs extra options, we can add them once this method is called.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> resetMenuOptions<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// First, clear the current menuItems</span>
    getMenuItems<span class="br0">(</span><span class="br0">)</span>.<span class="me1">clear</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">// Now add the default items</span>
    <span class="co3">/** Parameters:
      * String caption
      * Object value - We'll store a String that gives us a hint as to the menu item function
      * Menu subMenu - null, because there isn't one
      * boolean isToggleItem - adds a CheckBox to the menu item
      */</span>
    addMenuItem<span class="br0">(</span><span class="st0">"Lock window position"</span>, <span class="st0">"position"</span>, <span class="kw2">null</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    addMenuItem<span class="br0">(</span><span class="st0">"Lock window size"</span>, <span class="st0">"dimensions"</span>, <span class="kw2">null</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    addMenuItem<span class="br0">(</span><span class="st0">"Lock current alpha setting"</span>, <span class="st0">"alpha"</span>, <span class="kw2">null</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>

<h4 id="adding_our_new_control_to_the_screen">Adding Our New Control to the Screen</h4>
<div class="level4">
<pre class="code java"><span class="co1">// Create a single instance of the reusable contextual menu</span>
ContextualMenu rcMenu <span class="sy0">=</span> <span class="kw1">new</span> ContextualMenu<span class="br0">(</span>screen, <span class="st0">"rcMenu"</span>, Vector2f.<span class="me1">ZERO</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// Override the abstract event method</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onMenuItemClicked<span class="br0">(</span><span class="kw4">int</span> index, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> value, <span class="kw4">boolean</span> isToggled<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// Now we will pass this through to our calling window.</span>
        getCallerElement<span class="br0">(</span><span class="br0">)</span>.<span class="me1">setOption</span><span class="br0">(</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">)</span>value, isToggled<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span>
rcMenu.<span class="me1">resetMenuOptions</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">add</span><span class="br0">(</span>rcMenu<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="extending_the_window_class_to_utilize_our_control">Extending the Window Class to Utilize Our Control</h4>
<div class="level4">

</div>

<h5 id="step_1extend_the_window_class_and_add_a_few_methods">STEP 1: Extend the window class and add a few methods</h5>
<div class="level5">

<p>
We need to entend the window class in order to add right-click event handling and handle the setOption() method call from our ContextualMenu class.<br />

<br />

</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">abstract</span> <span class="kw1">class</span> ContextualWindow <span class="kw1">extends</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a> <span class="kw1">implements</span> MouseButtonListener <span class="br0">{</span>
    <span class="co1">// Add the 3 standard contructors from the Window class and rename them</span>
 
    <span class="co1">// implement all abstract methods from the listener and add the following to right mouse button up:</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onRightMouseReleased<span class="br0">(</span>MouseButtonEvent evt<span class="br0">)</span> <span class="br0">{</span>
        ContextualMenu rcMenu <span class="sy0">=</span> screen.<span class="me1">getElementById</span><span class="br0">(</span><span class="st0">"rcMenu"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// set the toggle state for each of the options</span>
        rcMenu.<span class="me1">getMenuItem</span><span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span>.<span class="me1">setIsToggled</span><span class="br0">(</span>getIsMovable<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rcMenu.<span class="me1">getMenuItem</span><span class="br0">(</span><span class="nu0">1</span><span class="br0">)</span>.<span class="me1">setIsToggled</span><span class="br0">(</span>getIsResizable<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rcMenu.<span class="me1">getMenuItem</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span>.<span class="me1">setIsToggled</span><span class="br0">(</span>getIgnoreGlobalAlpha<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// Show the menu</span>
        rcMenu.<span class="me1">showMenu</span><span class="br0">(</span><span class="kw1">this</span>, screen.<span class="me1">getMouseXY</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">x</span>, screen.<span class="me1">getMouseXY</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">y</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">// Add the setOption method tohandle menu item events</span>
    <span class="kw1">public</span> <span class="kw4">void</span> setOption<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> value, <span class="kw4">boolean</span> isToggled<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>value.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"position"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            setIsMovable<span class="br0">(</span>isToggled<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>value.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"dimensions"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            setIsResizable<span class="br0">(</span>isToggled<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>value.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"alpha"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            setIgnoreGlobalAlpha<span class="br0">(</span>isToggled<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
