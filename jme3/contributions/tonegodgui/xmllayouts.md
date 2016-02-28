---
title: Using XML to Define Layouts
---
<h3 class="sectionedit1" id="using_xml_to_define_layouts">Using XML to Define Layouts</h3>
<div class="level3">

<p>
XML Screens leverage the AbstractAppState class for managing your grouped UI components.
</p>

<p>
AppState example:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> XMLScreenSample <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
    Screen screen<span class="sy0">;</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a> inventory<span class="sy0">;</span>
 
    <span class="kw1">public</span> XMLScreenSample<span class="br0">(</span>Screen screen<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// Store a pointer to the screen</span>
        <span class="kw1">this</span>.<span class="me1">screen</span> <span class="sy0">=</span> screen<span class="sy0">;</span>
        <span class="co1">// Call the xml parser to load your new components</span>
        screen.<span class="me1">parseLayout</span><span class="br0">(</span><span class="st0">"Interface/Inventory.xml"</span>, <span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Here we can grab pointers to the loaded elements</span>
        inventory <span class="sy0">=</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+window"><span class="kw3">Window</span></a><span class="br0">)</span>screen.<span class="me1">getElementById</span><span class="br0">(</span><span class="st0">"InventoryWindowID"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// We'll hide the window initially so we can use an</span>
        <span class="co1">// effect to show it from the initialize method</span>
        inventory.<span class="me1">hide</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// grab more pointers to other elements / child elements</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Useful place for running load effects</span>
        inventory.<span class="me1">showWithEffect</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">//TODO: implement behavior during runtime</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> cleanup<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">cleanup</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// We can alter the effect to destroy our inventory window</span>
        <span class="co1">// when we unload the AppState</span>
        Effect hide <span class="sy0">=</span> <span class="kw1">new</span> Effect<span class="br0">(</span>Effect.<span class="me1">EffectType</span>.<span class="me1">FadeOut</span>, Effect.<span class="me1">EffectEvent</span>.<span class="me1">Hide</span>, 0.25f<span class="br0">)</span><span class="sy0">;</span>
        hide.<span class="me1">setDestroyOnHide</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="kw1">if</span> <span class="br0">(</span>inventory.<span class="me1">getIsVisible</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            inventory.<span class="me1">setEffect</span><span class="br0">(</span>hide<span class="br0">)</span><span class="sy0">;</span>
            inventory.<span class="me1">hideWithEffect</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
            screen.<span class="me1">removeElement</span><span class="br0">(</span>inventory<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
 
        <span class="co1">// Now our UI component scene fades out when the AppState in unloaded.</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>

<h4 id="a_look_at_the_xml_layout">A Look at the XML Layout</h4>
<div class="level4">

<p>
Below is a rather large XML layout with a bunch of different components, method calls, event methods, etc.  It is relative nonsense and just there to show the basic structure.
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;root<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;screen<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Window"</span> <span class="re0">id</span>=<span class="st0">"InventoryWindowID"</span> <span class="re0">position</span>=<span class="st0">"15%,15%"</span> <span class="re0">dimensions</span>=<span class="st0">"70%,70%"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setWindowTitle"</span> <span class="re0">param0</span>=<span class="st0">"Inventory"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Label"</span> <span class="re0">position</span>=<span class="st0">"10,40"</span> <span class="re0">dimensions</span>=<span class="st0">"20%,20"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setText"</span> <span class="re0">param0</span>=<span class="st0">"First Name:"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextAlign"</span> <span class="re0">param0</span>=<span class="st0">"Right"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextVAlign"</span> <span class="re0">param0</span>=<span class="st0">"Center"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Label"</span> <span class="re0">position</span>=<span class="st0">"10,65"</span> <span class="re0">dimensions</span>=<span class="st0">"20%,20"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setText"</span> <span class="re0">param0</span>=<span class="st0">"Last Name:"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextAlign"</span> <span class="re0">param0</span>=<span class="st0">"Right"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextVAlign"</span> <span class="re0">param0</span>=<span class="st0">"Center"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Label"</span> <span class="re0">position</span>=<span class="st0">"10,90"</span> <span class="re0">dimensions</span>=<span class="st0">"20%,20"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setText"</span> <span class="re0">param0</span>=<span class="st0">"Address:"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextAlign"</span> <span class="re0">param0</span>=<span class="st0">"Right"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextVAlign"</span> <span class="re0">param0</span>=<span class="st0">"Center"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Label"</span> <span class="re0">position</span>=<span class="st0">"10,140"</span> <span class="re0">dimensions</span>=<span class="st0">"20%,20"</span> <span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setText"</span> <span class="re0">param0</span>=<span class="st0">"City:"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextAlign"</span> <span class="re0">param0</span>=<span class="st0">"Right"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextVAlign"</span> <span class="re0">param0</span>=<span class="st0">"Center"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Label"</span> <span class="re0">position</span>=<span class="st0">"10,165"</span> <span class="re0">dimensions</span>=<span class="st0">"20%,20"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setText"</span> <span class="re0">param0</span>=<span class="st0">"State:"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextAlign"</span> <span class="re0">param0</span>=<span class="st0">"Right"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextVAlign"</span> <span class="re0">param0</span>=<span class="st0">"Center"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Label"</span> <span class="re0">position</span>=<span class="st0">"10,190"</span> <span class="re0">dimensions</span>=<span class="st0">"20%,20"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setText"</span> <span class="re0">param0</span>=<span class="st0">"Postal Code:"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextAlign"</span> <span class="re0">param0</span>=<span class="st0">"Right"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setTextVAlign"</span> <span class="re0">param0</span>=<span class="st0">"Center"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"TextField"</span> <span class="re0">id</span>=<span class="st0">"FirstName"</span> <span class="re0">position</span>=<span class="st0">"25%,40"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setType"</span> <span class="re0">param0</span>=<span class="st0">"EXCLUDE_CUSTOM"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setCustomValidation"</span> <span class="re0">param0</span>=<span class="st0">"!@#$%^*()"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"TextField"</span> <span class="re0">id</span>=<span class="st0">"LastName"</span> <span class="re0">position</span>=<span class="st0">"25%,65"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"TextField"</span> <span class="re0">id</span>=<span class="st0">"Address1"</span> <span class="re0">position</span>=<span class="st0">"25%,90"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"TextField"</span> <span class="re0">id</span>=<span class="st0">"Address2"</span> <span class="re0">position</span>=<span class="st0">"25%,115"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"TextField"</span> <span class="re0">id</span>=<span class="st0">"City"</span> <span class="re0">position</span>=<span class="st0">"25%,140"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Indicator"</span> <span class="re0">id</span>=<span class="st0">"Indicator1"</span> <span class="re0">position</span>=<span class="st0">"25%,225"</span> <span class="re0">orientation</span>=<span class="st0">"HORIZONTAL"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setAlphaMap"</span> <span class="re0">param0</span>=<span class="st0">"tonegod/gui/style/def/Common/Extras/indicator_am_x.png"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setIndicatorColor"</span> <span class="re0">param0</span>=<span class="st0">"0,0.65f,0,1"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setMaxValue"</span> <span class="re0">param0</span>=<span class="st0">"100"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setCurrentValue"</span> <span class="re0">param0</span>=<span class="st0">"50"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setDisplayValues"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"ComboBox"</span> <span class="re0">id</span>=<span class="st0">"State"</span> <span class="re0">position</span>=<span class="st0">"25%,165"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Alaska"</span> <span class="re0">param1</span>=<span class="st0">"Alaska"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Alabama"</span> <span class="re0">param1</span>=<span class="st0">"Alabama"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Arkansas"</span> <span class="re0">param1</span>=<span class="st0">"Arkansas"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Connecticut"</span> <span class="re0">param1</span>=<span class="st0">"Connecticut"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Deleware"</span> <span class="re0">param1</span>=<span class="st0">"Deleware"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Dakota, North"</span> <span class="re0">param1</span>=<span class="st0">"North Dakota"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Dakota, South"</span> <span class="re0">param1</span>=<span class="st0">"South Dakota"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Georgia"</span> <span class="re0">param1</span>=<span class="st0">"Georgia"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Kentucky"</span> <span class="re0">param1</span>=<span class="st0">"Kentucky"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Maine"</span> <span class="re0">param1</span>=<span class="st0">"Maine"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"New Jersey"</span> <span class="re0">param1</span>=<span class="st0">"New Jersey"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"New York"</span> <span class="re0">param1</span>=<span class="st0">"New York"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addListItem"</span> <span class="re0">param0</span>=<span class="st0">"Nevada"</span> <span class="re0">param1</span>=<span class="st0">"Nevada"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"TextField"</span> <span class="re0">id</span>=<span class="st0">"PostalCode"</span> <span class="re0">position</span>=<span class="st0">"25%,190"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setType"</span> <span class="re0">param0</span>=<span class="st0">"INCLUDE_CUSTOM"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setCustomValidation"</span> <span class="re0">param0</span>=<span class="st0">"1234567890-"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setMaxLength"</span> <span class="re0">param0</span>=<span class="st0">"10"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
            <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Button"</span> <span class="re0">id</span>=<span class="st0">"SubmitButton"</span> <span class="re0">position</span>=<span class="st0">"75%,87%"</span> <span class="re0">dimensions</span>=<span class="st0">"23%,10%"</span> <span class="re2">&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setText"</span> <span class="re0">param0</span>=<span class="st0">"Submit"</span> <span class="re2">/&gt;</span></span>
                <span class="sc3"><span class="re1">&lt;eventMethod</span> <span class="re0">name</span>=<span class="st0">"onButtonMouseLeftUp"</span> <span class="re0">stateMethodName</span>=<span class="st0">"invSubmitButtonClick"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Menu"</span> <span class="re0">id</span>=<span class="st0">"SubMenu1"</span> <span class="re0">position</span>=<span class="st0">"0,0"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addMenuItem"</span> <span class="re0">param0</span>=<span class="st0">"Menu Item 1"</span> <span class="re0">param1</span>=<span class="st0">"1"</span> <span class="re0">param2</span>=<span class="st0">"null"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addMenuItem"</span> <span class="re0">param0</span>=<span class="st0">"Menu Item 2"</span> <span class="re0">param1</span>=<span class="st0">"2"</span> <span class="re0">param2</span>=<span class="st0">"null"</span> <span class="re0">param3</span>=<span class="st0">"true"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addMenuItem"</span> <span class="re0">param0</span>=<span class="st0">"Menu Item 3"</span> <span class="re0">param1</span>=<span class="st0">"3"</span> <span class="re0">param2</span>=<span class="st0">"null"</span> <span class="re0">param3</span>=<span class="st0">"true"</span> <span class="re0">param4</span>=<span class="st0">"true"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addMenuItem"</span> <span class="re0">param0</span>=<span class="st0">"Menu Item 4"</span> <span class="re0">param1</span>=<span class="st0">"4"</span> <span class="re0">param2</span>=<span class="st0">"null"</span> <span class="re0">param3</span>=<span class="st0">"true"</span> <span class="re0">param4</span>=<span class="st0">"true"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;eventMethod</span> <span class="re0">name</span>=<span class="st0">"onMenuItemClicked"</span> <span class="re0">stateMethodName</span>=<span class="st0">"menu1click"</span> <span class="re2">/&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"Menu"</span> <span class="re0">id</span>=<span class="st0">"Menu1"</span> <span class="re0">position</span>=<span class="st0">"0,0"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addMenuItem"</span> <span class="re0">param0</span>=<span class="st0">"Item 1"</span> <span class="re0">param1</span>=<span class="st0">"1"</span> <span class="re0">param2</span>=<span class="st0">"SubMenu1"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"addMenuItem"</span> <span class="re0">param0</span>=<span class="st0">"Item 2"</span> <span class="re0">param1</span>=<span class="st0">"2"</span> <span class="re0">param2</span>=<span class="st0">"null"</span> <span class="re0">param3</span>=<span class="st0">"true"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;eventMethod</span> <span class="re0">name</span>=<span class="st0">"onMenuItemClicked"</span> <span class="re0">stateMethodName</span>=<span class="st0">"menu1click"</span> <span class="re2">/&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;component</span> <span class="re0">type</span>=<span class="st0">"AlertBox"</span> <span class="re0">id</span>=<span class="st0">"Alert1"</span> <span class="re0">position</span>=<span class="st0">"0,0"</span><span class="re2">&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"setWindowTitle"</span> <span class="re0">param0</span>=<span class="st0">"Hey you!"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;method</span> <span class="re0">name</span>=<span class="st0">"centerToParent"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;eventMethod</span> <span class="re0">name</span>=<span class="st0">"onButtonOkPressed"</span> <span class="re0">stateMethodName</span>=<span class="st0">"alertOkClick"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;effect</span> <span class="re0">type</span>=<span class="st0">"SlideIn"</span> <span class="re0">event</span>=<span class="st0">"Show"</span> <span class="re0">duration</span>=<span class="st0">".25f"</span> <span class="re0">direction</span>=<span class="st0">"Left"</span> <span class="re0">audioFile</span>=<span class="st0">"fade"</span> <span class="re0">volume</span>=<span class="st0">"1"</span> <span class="re2">/&gt;</span></span>
            <span class="sc3"><span class="re1">&lt;effect</span> <span class="re0">type</span>=<span class="st0">"SlideOut"</span> <span class="re0">event</span>=<span class="st0">"Hide"</span> <span class="re0">duration</span>=<span class="st0">".25f"</span> <span class="re0">direction</span>=<span class="st0">"Left"</span> <span class="re0">audioFile</span>=<span class="st0">"fade"</span> <span class="re2">/&gt;</span></span>
        <span class="sc3"><span class="re1">&lt;/component<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
<span class="sc3"><span class="re1">&lt;/root<span class="re2">&gt;</span></span></span></pre>

<p>
In the above example, you'll see that many components have defined an eventMethod tag.  The eventMethod tag defines the AppState method that will be used as a passthrough from the defined control event method.  There is no need to define parameters for these methods, as they simply forward the event methods parameters directly to the defined app state method.  Like so:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;eventMethod</span> <span class="re0">name</span>=<span class="st0">"onButtonMouseLeftUp"</span> <span class="re0">stateMethodName</span>=<span class="st0">"invSubmitButtonClick"</span> <span class="re2">/&gt;</span></span></pre>

<p>
Now we'll need to add the invSubmitButtonClick method to the AbstractAppState that called the parseLayout method, like so:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> invSubmitButtonClick<span class="br0">(</span>MouseButtonEvent evt, <span class="kw4">boolean</span> isToggled<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// We'll show the AlertBox we defined in the layout when this button is clicked</span>
    <span class="br0">(</span><span class="br0">(</span>AlertBox<span class="br0">)</span>screen.<span class="me1">getElementById</span><span class="br0">(</span><span class="st0">"Alert1"</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">showWithEffect</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
The quickest way of getting the definition of the event method you are creating, is to create a new instance of the class the event is being passed from, implementing it's abstract methods &amp; cutt/paste the needed method.  Then you simply rename it.
</p>

</div>
