---
title: EffectManager
---
<h3 class="sectionedit1" id="effectmanager">EffectManager</h3>
<div class="level3">

<p>
The EffectManager can be used to execute Effects, BatchEffects and EffectQueues against a single Element or a group of nested or separate Elements.  Effects include shader-based effects, geometry-based effects and can include an audio event if UIAudio has been enabled.<br />

<br />

The EffectManager is accessed through the Screen class, like so:
</p>
<pre class="code java">screen.<span class="me1">getEffectManager</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="methods_specific_to_the_effectmanager">Methods specific to the EffectMAnager</h4>
<div class="level4">
<pre class="code java">screen.<span class="me1">getEffectManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">applyEffect</span><span class="br0">(</span>Effect effect<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">getEffectManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">applyEffectQueue</span><span class="br0">(</span>EffectQueue queue<span class="br0">)</span><span class="sy0">;</span>
screen.<span class="me1">getEffectManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">applyBatchEffect</span><span class="br0">(</span>BatchEffect batch<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
