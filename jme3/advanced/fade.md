---
title: Fade-in / Fade-out Effect
---
<h1 class="sectionedit1" id="fade-in_fade-out_effect">Fade-in / Fade-out Effect</h1>
<div class="level1">

<p>
You can use a fade in/fade out effect to make smooth transitions, for example between game levels. The effect fades in from black to the initialized scene, or fades out from the scene to black.
The effect uses com.jme3.post.FilterPostProcessor and com.jme3.post.filters.FadeFilter.
</p>

</div>
<!-- EDIT1 SECTION "Fade-in / Fade-out Effect" [1-320] -->
<h2 class="sectionedit2" id="setting_up">Setting up</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Create one FilterPostProcessor object per application.</div>
</li>
<li class="level1"><div class="li"> Create a FadeFilter object.</div>
</li>
<li class="level1"><div class="li"> Give the FadeFilter constructor the fade duration in seconds as parameter. If you use the parameter-less constructor, the duration is 1 sec by default.</div>
</li>
<li class="level1"><div class="li"> Add the FadeFilter to the FilterPostProcessor.</div>
</li>
<li class="level1"><div class="li"> Add the FilterPostProcessor to the default viewPort.</div>
</li>
</ol>
<pre class="code java"><span class="kw1">private</span> FilterPostProcessor fpp<span class="sy0">;</span>
<span class="kw1">private</span> FadeFilter fade<span class="sy0">;</span>
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="me1">fpp</span> <span class="sy0">=</span> <span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span>
  fade <span class="sy0">=</span> <span class="kw1">new</span> FadeFilter<span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// e.g. 2 seconds</span>
  fpp.<span class="me1">addFilter</span><span class="br0">(</span>fade<span class="br0">)</span><span class="sy0">;</span>
  viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>fpp<span class="br0">)</span><span class="sy0">;</span>
  ...
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "Setting up" [321-965] -->
<h2 class="sectionedit3" id="fading_in_and_out">Fading in and out</h2>
<div class="level2">

<p>
Now call the <code>fade.fadeIn()</code> and <code>fade.fadeOut()</code> methods to trigger the effect.
You can also change the fade duration using <code>fade.setDuration()</code>.
</p>

</div>
<!-- EDIT3 SECTION "Fading in and out" [966-] -->
