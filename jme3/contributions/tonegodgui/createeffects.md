---
title: Effect
---
<h3 class="sectionedit1" id="effect">Effect</h3>
<div class="level3">

<p>
Effects are used to graphically enhance your UI with transitions, movement, image manipulation &amp; audio.<br />

<br />

</p>

</div>

<h4 id="creating_an_effect">Creating an Effect</h4>
<div class="level4">
<pre class="code java">Effect effect <span class="sy0">=</span> <span class="kw1">new</span> Effect<span class="br0">(</span>
    Effect.<span class="me1">EffectType</span>.<span class="me1">FadeIn</span>, <span class="co1">// The type of effect to use</span>
    Effect.<span class="me1">EffectEvent</span>.<span class="me1">Show</span>, <span class="co1">// The event that the effect is associated with</span>
    2.2f <span class="co1">// The duration of time over which the effect executes (2.2 seconds)</span>
<span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">setEffectElement</span><span class="br0">(</span>someElement<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// The Element to fade into the screen</span>
 
screen.<span class="me1">getEffectManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">applyEffect</span><span class="br0">(</span>effect<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Tell the effect manager to execute</span></pre>

</div>

<h4 id="creating_automated_effects">Creating Automated Effects</h4>
<div class="level4">

<p>
Some components have effects associated with them by default, for instance buttons hover and pressed states.  You can create effects for these states (or replace the existing effects defined in the style XMLs) like so:
</p>
<pre class="code java">Effect effect <span class="sy0">=</span> <span class="kw1">new</span> Effect<span class="br0">(</span>
    Effect.<span class="me1">EffectType</span>.<span class="me1">Pulse</span>, <span class="co1">// The type of effect to use</span>
    Effect.<span class="me1">EffectEvent</span>.<span class="me1">Hover</span>, <span class="co1">// The event that the effect is associated with</span>
    2.2f <span class="co1">// The duration of time over which the effect executes (2.2 seconds)</span>
<span class="br0">)</span><span class="sy0">;</span>
someButton.<span class="me1">addEffect</span><span class="br0">(</span>effect<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
At this point, the button will use the following effect anytime the user mouseovers the button, as well as manage any setting required to execute the effect properly.<br />

</p>

<p>
</p><p></p><div class="noteclassic">Some effects require a blend image (to pulse to and from in the above case)<br />

Some require a blend  color<br />

Others require a direction<br />

<br />

See below for details
</div>


</div>

<h4 id="methods_specific_to_setting_up_effects">Methods Specific to Setting Up Effects</h4>
<div class="level4">
<pre class="code java">effect.<span class="me1">setElement</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> element<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Used with Pulse, ImageSwap</span>
effect.<span class="me1">setBlendImage</span><span class="br0">(</span>Texture blendImage<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Used with PulseColor, ColorSwap</span>
effect.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA blendColor<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Used with SlideIn, SlideOut</span>
effect.<span class="me1">setEffectDirection</span><span class="br0">(</span>Effect.<span class="me1">EffectDirection</span> direction<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Used with SlideTo</span>
effect.<span class="me1">setEffectDestination</span><span class="br0">(</span>Vector2f destination<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Used with any effect</span>
effect.<span class="me1">setAudioFile</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> styleTagID<span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">setAudioVolume</span><span class="br0">(</span><span class="kw4">float</span> volume<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="other_methods_specific_to_effect">Other Methods Specific to Effect</h4>
<div class="level4">
<pre class="code java">effect.<span class="me1">getElement</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">getDuration</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">getIsActive</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">getEffectType</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">getEffectEvent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">getEffectDirection</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">getAudioFile</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
effect.<span class="me1">getAudioVolume</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Use with hide effects.  **only use if you want the element associated </span>
<span class="co1">// with the effect to be destroy &amp; garbage collected</span>
effect.<span class="me1">setDestroyOnHide</span><span class="br0">(</span><span class="kw4">boolean</span> destroyOnHide<span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="enums">Enums</h4>
<div class="level4">

<p>
Effect.EffectType
</p>
<ul>
<li class="level1"><div class="li"> FadeIn</div>
</li>
<li class="level1"><div class="li"> FadeOut</div>
</li>
<li class="level1"><div class="li"> ZoomIn</div>
</li>
<li class="level1"><div class="li"> ZoomOut</div>
</li>
<li class="level1"><div class="li"> SlideIn</div>
</li>
<li class="level1"><div class="li"> SlideOut</div>
</li>
<li class="level1"><div class="li"> SpinIn</div>
</li>
<li class="level1"><div class="li"> SpinOut</div>
</li>
<li class="level1"><div class="li"> Pulse</div>
</li>
<li class="level1"><div class="li"> ColorSwap</div>
</li>
<li class="level1"><div class="li"> PulseColor</div>
</li>
<li class="level1"><div class="li"> ImageSwap</div>
</li>
<li class="level1"><div class="li"> Saturate</div>
</li>
<li class="level1"><div class="li"> Desaturate</div>
</li>
</ul>

<p>
Effect.EffectEvent
</p>
<ul>
<li class="level1"><div class="li"> GetFocus</div>
</li>
<li class="level1"><div class="li"> LoseFocus</div>
</li>
<li class="level1"><div class="li"> Show</div>
</li>
<li class="level1"><div class="li"> Hide</div>
</li>
<li class="level1"><div class="li"> Hover</div>
</li>
<li class="level1"><div class="li"> Press</div>
</li>
<li class="level1"><div class="li"> Release</div>
</li>
<li class="level1"><div class="li"> TabFocus</div>
</li>
<li class="level1"><div class="li"> LoseTabFocus</div>
</li>
</ul>

<p>
Effect.EffectDirection
</p>
<ul>
<li class="level1"><div class="li"> Top</div>
</li>
<li class="level1"><div class="li"> Bottom</div>
</li>
<li class="level1"><div class="li"> Left</div>
</li>
<li class="level1"><div class="li"> Right</div>
</li>
</ul>

</div>
