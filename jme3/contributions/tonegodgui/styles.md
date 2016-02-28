---
title: Creating a new Theme
---
<h3 class="sectionedit1" id="creating_a_new_theme">Creating a new Theme</h3>
<div class="level3">

</div>

<h4 id="understanding_styles">Understanding Styles</h4>
<div class="level4">

<p>
The Style class is set up to be as open ended as possible for creating custom controls.<br />

<br />

Each property of a style can be one of the following data type:
</p>
<ul>
<li class="level1"><div class="li"> String</div>
</li>
<li class="level1"><div class="li"> float</div>
</li>
<li class="level1"><div class="li"> int</div>
</li>
<li class="level1"><div class="li"> boolean</div>
</li>
<li class="level1"><div class="li"> ColorRGBA</div>
</li>
<li class="level1"><div class="li"> Vector2f</div>
</li>
<li class="level1"><div class="li"> Vector3f</div>
</li>
<li class="level1"><div class="li"> Vector4f</div>
</li>
<li class="level1"><div class="li"> Effect</div>
</li>
<li class="level1"><div class="li"> Object</div>
</li>
</ul>

<p>
To retrieve a tag from a style you must use the get method for the data type you trying to retrieve like so:
</p>
<pre class="code java">screen.<span class="me1">getStyle</span><span class="br0">(</span>“StyleName”<span class="br0">)</span>.<span class="me1">getColorRGBA</span><span class="br0">(</span>“TagNameInStyle”<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
These can be used as flags for configuring you control, or style specific info for default Look &amp; Feel<br />

<br />

Lets look at the Button.xml file as an example:
</p>
<pre class="code html4strict"><span class="sc2">&lt;root&gt;</span>
    <span class="sc2">&lt;element <span class="kw3">name</span><span class="sy0">=</span>”Button”&gt;</span>
        <span class="sc2">&lt;<a href="http://december.com/html/4/element/font.html"><span class="kw2">font</span></a>&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”fontSize” <span class="kw3">type</span><span class="sy0">=</span>”float” <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">18</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”fontColor” <span class="kw3">type</span><span class="sy0">=</span>”ColorRGBA”&gt;</span>
                <span class="sc2">&lt;r <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">0.8</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;g <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">0.8</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;<a href="http://december.com/html/4/element/b.html"><span class="kw2">b</span></a> <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">0.8</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;<a href="http://december.com/html/4/element/a.html"><span class="kw2">a</span></a> <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">1.0</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”textAlign” <span class="kw3">type</span><span class="sy0">=</span>”String” <span class="kw3">value</span><span class="sy0">=</span>”Center” <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”textVAlign” <span class="kw3">type</span><span class="sy0">=</span>”String” <span class="kw3">value</span><span class="sy0">=</span>”Center” <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”textWrap” <span class="kw3">type</span><span class="sy0">=</span>”String” <span class="kw3">value</span><span class="sy0">=</span>”Clip” <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”hoverColor” <span class="kw3">type</span><span class="sy0">=</span>”ColorRGBA”&gt;</span>
                <span class="sc2">&lt;r <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">1.0</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;g <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">1.0</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;<a href="http://december.com/html/4/element/b.html"><span class="kw2">b</span></a> <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">1.0</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;<a href="http://december.com/html/4/element/a.html"><span class="kw2">a</span></a> <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">1.0</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”pressedColor” <span class="kw3">type</span><span class="sy0">=</span>”ColorRGBA”&gt;</span>
                <span class="sc2">&lt;r <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">0.6</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;g <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">0.6</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;<a href="http://december.com/html/4/element/b.html"><span class="kw2">b</span></a> <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">0.6</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;<a href="http://december.com/html/4/element/a.html"><span class="kw2">a</span></a> <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">1.0</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span>
        <span class="sc2">&lt;<span class="sy0">/</span><a href="http://december.com/html/4/element/font.html"><span class="kw2">font</span></a>&gt;</span>
        <span class="sc2">&lt;attributes&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”resizeBorders” <span class="kw3">type</span><span class="sy0">=</span>”Vector4f”&gt;</span>
                <span class="sc2">&lt;x <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">5</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;y <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">5</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;z <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">5</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;w <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">5</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”defaultSize” <span class="kw3">type</span><span class="sy0">=</span>”Vector2f”&gt;</span>
                <span class="sc2">&lt;x <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">100</span>″ <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;y <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">30</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span>
        <span class="sc2">&lt;<span class="sy0">/</span>attributes&gt;</span>
        <span class="sc2">&lt;images&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”defaultImg” <span class="kw3">type</span><span class="sy0">=</span>”String” <span class="kw3">value</span><span class="sy0">=</span>”tonegod<span class="sy0">/</span>gui<span class="sy0">/</span><span class="kw3">style</span><span class="sy0">/</span>def<span class="sy0">/</span>Button<span class="sy0">/</span>button_x_u.png” <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”hoverImg” <span class="kw3">type</span><span class="sy0">=</span>”String” <span class="kw3">value</span><span class="sy0">=</span>”tonegod<span class="sy0">/</span>gui<span class="sy0">/</span><span class="kw3">style</span><span class="sy0">/</span>def<span class="sy0">/</span>Button<span class="sy0">/</span>button_x_h.png” <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”pressedImg” <span class="kw3">type</span><span class="sy0">=</span>”String” <span class="kw3">value</span><span class="sy0">=</span>”tonegod<span class="sy0">/</span>gui<span class="sy0">/</span><span class="kw3">style</span><span class="sy0">/</span>def<span class="sy0">/</span>Button<span class="sy0">/</span>button_x_d.png” <span class="sy0">/</span>&gt;</span>
        <span class="sc2">&lt;<span class="sy0">/</span>images&gt;</span>
        <span class="sc2">&lt;effects&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”event0″ <span class="kw3">type</span><span class="sy0">=</span>”Effect”&gt;</span>
                <span class="sc2">&lt;event <span class="kw3">value</span><span class="sy0">=</span>”Hover” <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;effect <span class="kw3">value</span><span class="sy0">=</span>”Pulse” <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;speed <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">3</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”event1″ <span class="kw3">type</span><span class="sy0">=</span>”Effect”&gt;</span>
                <span class="sc2">&lt;event <span class="kw3">value</span><span class="sy0">=</span>”Press” <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;effect <span class="kw3">value</span><span class="sy0">=</span>”ImageSwap” <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;speed <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">0</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span>
            <span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”event2″ <span class="kw3">type</span><span class="sy0">=</span>”Effect”&gt;</span>
                <span class="sc2">&lt;event <span class="kw3">value</span><span class="sy0">=</span>”LoseFocus” <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;effect <span class="kw3">value</span><span class="sy0">=</span>”ImageSwap” <span class="sy0">/</span>&gt;</span>
                <span class="sc2">&lt;speed <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">0</span>″ <span class="sy0">/</span>&gt;</span>
            <span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span>
        <span class="sc2">&lt;<span class="sy0">/</span>effects&gt;</span>
    <span class="sc2">&lt;<span class="sy0">/</span>element&gt;</span>
<span class="sc2">&lt;<span class="sy0">/</span>root&gt;</span></pre>
<p>
The Style XML file for any given control can contain as many element tags as you would like.  Each becomes another style that can be retrieved via:
</p>
<pre class="code java">screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"styleName"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Each element tag is divided into 4 sections:
</p>
<ul>
<li class="level1"><div class="li"> fonts</div>
</li>
<li class="level1"><div class="li"> attributes</div>
</li>
<li class="level1"><div class="li"> images</div>
</li>
<li class="level1"><div class="li"> effects</div>
</li>
</ul>

<p>
The first 3 are interchangeable and only there for organizational purposes.<br />

<br />

The 4th (effects) is more specific, as the effects are stored and retrieved via the EffectManage of the Screen.<br />

<br />

The tags for storing properties are fomatted as follows:
</p>
<ul>
<li class="level1"><div class="li"> if the data type has a single value, the value is stored in the single property tag:</div>
</li>
</ul>
<pre class="code html4strict"><span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"ID"</span> <span class="kw3">type</span><span class="sy0">=</span><span class="st0">"float"</span> <span class="kw3">value</span><span class="sy0">=</span><span class="st0">"0.5"</span> <span class="sy0">/</span>&gt;</span></pre><ul>
<li class="level1"><div class="li"> If the data type has multiple value, the property tag would contain inner tags named after the value, like such:</div>
</li>
</ul>
<pre class="code html4strict"><span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span><span class="st0">"ID"</span> <span class="kw3">type</span><span class="sy0">=</span><span class="st0">"Vector4f /&gt;</span></span>
    <span class="sc2">&lt;x <span class="kw3">value</span><span class="sy0">=</span><span class="st0">"0.5 /&gt;</span></span> 
    <span class="sc2">&lt;y <span class="kw3">value</span><span class="sy0">=</span><span class="st0">"0.5 /&gt;</span></span> 
    <span class="sc2">&lt;z <span class="kw3">value</span><span class="sy0">=</span><span class="st0">"0.5 /&gt;</span></span> 
    <span class="sc2">&lt;w <span class="kw3">value</span><span class="sy0">=</span><span class="st0">"0.5 /&gt;</span></span> 
<span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span></pre>
<p>
Again, to retrieve this you would call:
</p>
<pre class="code java">screen.<span class="me1">getStyle</span><span class="br0">(</span><span class="st0">"styleName"</span><span class="br0">)</span>.<span class="me1">getVector4f</span><span class="br0">(</span><span class="st0">"ID"</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="the_effects_tag">The 'effects' Tag</h4>
<div class="level4">

<p>
To add a default effect to a control, you would add a property tag under the 'effects' tag, like so:
</p>
<pre class="code html4strict"><span class="sc2">&lt;property <span class="kw3">name</span><span class="sy0">=</span>”event0″ <span class="kw3">type</span><span class="sy0">=</span>”Effect”&gt;</span>
    <span class="sc2">&lt;event <span class="kw3">value</span><span class="sy0">=</span>”Hover” <span class="sy0">/</span>&gt;</span>
    <span class="sc2">&lt;effect <span class="kw3">value</span><span class="sy0">=</span>”Pulse” <span class="sy0">/</span>&gt;</span>
    <span class="sc2">&lt;speed <span class="kw3">value</span><span class="sy0">=</span>”<span class="nu0">3</span>″ <span class="sy0">/</span>&gt;</span>
<span class="sc2">&lt;<span class="sy0">/</span>property&gt;</span></pre>
<p>
Using Effects can be found HERE.
</p>

</div>

<h4 id="style_mapxml">style_map.xml</h4>
<div class="level4">

<p>
The style_map.xml file consists of a list of all other XML documents that contain style information for controls. All other XMLdocs could very well could be a single XML document containing all styles, however, for organization purposes, I read in as many from this list as you would like to add.<br />

<br />

Each entry in the style_map.xml file are formatted as follows:
</p>
<pre class="code html4strict"><span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span>”CustomControl” path<span class="sy0">=</span>”somePath<span class="sy0">/</span>MyNewControl.xml” <span class="sy0">/</span>&gt;</span></pre>
<p>
</p><p></p><div class="noteclassic">The control= property is not enforced, it is their for you to keep track of what XML file is used for what control.
</div>


</div>

<h4 id="to_set_up_a_custom_global_look_feel_for_your_ui">To set up a custom global Look &amp; Feel for your UI</h4>
<div class="level4">

</div>

<h5 id="step_1copy_the_style_mapxml_file_to_a_local_directory_in_your_project_assets_folder">STEP 1: Copy the style_map.xml file to a local directory in your Project Assets folder.</h5>
<div class="level5">
<pre class="code html4strict"><span class="sc2">&lt;?xml <span class="kw3">version</span><span class="sy0">=</span><span class="st0">"1.0"</span> encoding<span class="sy0">=</span><span class="st0">"UTF-8"</span>?&gt;</span>
<span class="sc2">&lt;root&gt;</span>
	<span class="sc2">&lt;cursors path<span class="sy0">=</span><span class="st0">"somePath/Cursors.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;audio path<span class="sy0">=</span><span class="st0">"somePath/Audio.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Font"</span> path<span class="sy0">=</span><span class="st0">"somePath/Fonts.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Common"</span> path<span class="sy0">=</span><span class="st0">"somePath/Common.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Scrolling"</span> path<span class="sy0">=</span><span class="st0">"somePath/Scrolling.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Window"</span> path<span class="sy0">=</span><span class="st0">"somePath/Window.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Button"</span> path<span class="sy0">=</span><span class="st0">"somePath/Button.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Menu"</span> path<span class="sy0">=</span><span class="st0">"somePath/Menu.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Label"</span> path<span class="sy0">=</span><span class="st0">"somePath/Label.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Slider"</span> path<span class="sy0">=</span><span class="st0">"somePath/Slider.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"TextField"</span> path<span class="sy0">=</span><span class="st0">"somePath/TextField.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"ChatBox"</span> path<span class="sy0">=</span><span class="st0">"somePath/ChatBox.xml"</span> <span class="sy0">/</span>&gt;</span>
	<span class="sc2">&lt;<a href="http://december.com/html/4/element/style.html"><span class="kw2">style</span></a> control<span class="sy0">=</span><span class="st0">"Indicator"</span> path<span class="sy0">=</span><span class="st0">"somePath/Indicator.xml"</span> <span class="sy0">/</span>&gt;</span>
<span class="sc2">&lt;<span class="sy0">/</span>root&gt;</span></pre>
</div>

<h5 id="step_2point_your_screen_class_to_the_new_style_mapxml_file">STEP 2: Point your Screen class to the new style_map.xml file.</h5>
<div class="level5">
<pre class="code java">Screen screen <span class="sy0">=</span> <span class="kw1">new</span> Screen<span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"somePath/style_map.xml"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<br />

You can now copy the existing XML docs for each listed in the style_map.xml file and make the adjustments you would like as default styles.
</p>

<p>
</p><p></p><div class="noteimportant">Don't forget to update the path in the style_map.xml file to point to your local copy for each control XML file you copy/edit.
</div>


</div>
