---
title: Rendering Water as Post-Process Effect
---
<h1 class="sectionedit1" id="rendering_water_as_post-process_effect">Rendering Water as Post-Process Effect</h1>
<div class="level1">

<p>
The awesome SeaMonkey WaterFilter is highly configurable. It can render any type of water and also simulates the underwater part of the effect, including light effects called caustics. The effect is based on <a href="http://www.gamedev.net/page/reference/index.html/_//feature/fprogramming/rendering-water-as-a-post-process-effect-r2642" class="urlextern" title="http://www.gamedev.net/page/reference/index.html/_//feature/fprogramming/rendering-water-as-a-post-process-effect-r2642" rel="nofollow">Wojciech Toman’s Rendering Water as a Post-process Effect</a> published on gamedev.net. Here's a video:
</p>

<p>
<a href="/resources/jme3-advanced-water-post.png" class="media" title="http://www.youtube.com/watch?v=AWlUzgRN3Pc" rel="nofollow"><img src="/resources/jme3-advanced-water-post.png" class="mediacenter" alt="" /></a>
</p>

<p>
</p><p></p><div class="noteclassic">The SeaMonkey WaterFilter is ideal for oceans and lakes, and especially for under-water scenes. If you only need a small simple water surface, such as a water trough or a shallow fountain, the <a href="/jme3/advanced/water.html" class="wikilink1" title="jme3:advanced:water">SimpleWaterProcessor</a> may already be all you need.
</div>


</div>
<!-- EDIT1 SECTION "Rendering Water as Post-Process Effect" [1-855] -->
<h2 class="sectionedit2" id="the_theory">The Theory</h2>
<div class="level2">

<p>
The effect is part of a deferred rendering process, taking advantage of the pre-computed position buffer and back buffer (a texture representing the screen’s pixels position in view space, and a texture of the rendered scene).
</p>

<p>
After some calculation, this allows to reconstruct the position in world space for each pixel on the screen. “If a pixel is under a given water height, let’s render it as a blue pixel!” Blue pixel? Not exactly, we want waves, we want ripples, we want foam, we want reflection and refraction.
</p>

<p>
The GameDev.net article describes how those effects are achieved, but the main idea is to generate waves from a height map, create ripples from a normal map, blend in the foam texture when the water depth is below a certain height, compute the refraction color with a clever color extinction algorithm, and then, display the reflection and specular effect by computing a Fresnel term (like in the simple water effect). In addition, this effect allows to blend the water shore with the ground to avoid the hard edges of classic water effects based on grids or quads.
</p>

</div>
<!-- EDIT2 SECTION "The Theory" [856-1971] -->
<h2 class="sectionedit3" id="how_did_we_implement_it_in_jme3">How Did We Implement it in jME3?</h2>
<div class="level2">

<p>
jME3 default behavior is to use a forward rendering process, so there is no position buffer rendered that we can take advantage of. But while rendering the main scene to a frame buffer in the FilterPostPorcessor, we can write the hardware depth buffer to a texture, with nearly no additional cost.
</p>

<p>
There are several ways of reconstructing the world space position of a pixel from the depth buffer. The computational cost is higher than just fetching the position from a position buffer, but the bandwidth and the memory required is a lot lower.
</p>

<p>
Now we have the rendered scene in a texture, and we can reconstruct the position in world space of each pixel. We’re good to go!
</p>

<p>
– Nehon
</p>

</div>
<!-- EDIT3 SECTION "How Did We Implement it in jME3?" [1972-2707] -->
<h2 class="sectionedit4" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
There are two test cases in the jME3 repository:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestPostWater.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestPostWater.java" rel="nofollow">jme3/src/test/jme3test/water/TestPostWater.java</a> (ocean island)</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestPostWaterLake.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestPostWaterLake.java" rel="nofollow">jme3/src/test/jme3test/water/TestPostWaterLake.java</a> (calm and muddy water pond)</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestMultiPostWater.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestMultiPostWater.java" rel="nofollow">jme3/src/test/jme3test/water/TestMultiPostWater.java</a> (several ponds of different sizes at different heights etc)</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Sample Code" [2708-3399] -->
<h3 class="sectionedit5" id="using_the_water_filter">Using the Water Filter</h3>
<div class="level3">

<p>
In the <code>simpleInitApp()</code> method, you attach your scene to the rootNode, typically a terrain with a sky. Remember to add a directional light, since the water relies on the light direction vector. The WaterFilter constructor expects a node with the scene attached that should be reflected in the water, and vector information from the light source's direction.
</p>

<p>
This is how you use the water filter post-processor code in your code:
</p>
<pre class="code java"><span class="kw1">private</span> FilterPostProcessor fpp<span class="sy0">;</span>
<span class="kw1">private</span> WaterFilter water<span class="sy0">;</span>
<span class="kw1">private</span> Vector3f lightDir <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>4.9f, <span class="sy0">-</span>1.3f, 5.9f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// same as light source</span>
<span class="kw1">private</span> <span class="kw4">float</span> initialWaterHeight <span class="sy0">=</span> 0.8f<span class="sy0">;</span> <span class="co1">// choose a value for your scene</span>
...
 
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  ...
  <span class="me1">fpp</span> <span class="sy0">=</span> <span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span>
  water <span class="sy0">=</span> <span class="kw1">new</span> WaterFilter<span class="br0">(</span>rootNode, lightDir<span class="br0">)</span><span class="sy0">;</span>
  water.<span class="me1">setWaterHeight</span><span class="br0">(</span>initialWaterHeight<span class="br0">)</span><span class="sy0">;</span>
  fpp.<span class="me1">addFilter</span><span class="br0">(</span>water<span class="br0">)</span><span class="sy0">;</span>
  viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>fpp<span class="br0">)</span><span class="sy0">;</span>
  ...
<span class="br0">}</span></pre>

<p>
Usually you make the water reflect everything attached to the rootNode. But you can also give a custom node (a subnode of the rootNode) to the WaterFilter constructor that has only a subset of scene nodes attached. This would be a relevant optimization if you have lots of nodes that are far away from the water, or covered, and will never be reflected.
</p>

</div>
<!-- EDIT5 SECTION "Using the Water Filter" [3400-4704] -->
<h3 class="sectionedit6" id="optionalwaves">Optional: Waves</h3>
<div class="level3">

<p>
If you want waves, set the water height in the update loop. We reuse the initialWaterHeight variable, and repeatedly reset the waterHeight value according to time. This causes the waves.
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw4">float</span> time <span class="sy0">=</span> 0.0f<span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">float</span> waterHeight <span class="sy0">=</span> 0.0f<span class="sy0">;</span> 
 
@Override
<span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">super</span>.<span class="me1">simpleUpdate</span><span class="br0">(</span>tpf<span class="br0">)</span><span class="sy0">;</span>
  time <span class="sy0">+=</span> tpf<span class="sy0">;</span>
  waterHeight <span class="sy0">=</span> <span class="br0">(</span><span class="kw4">float</span><span class="br0">)</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+math"><span class="kw3">Math</span></a>.<span class="me1">cos</span><span class="br0">(</span><span class="br0">(</span><span class="br0">(</span>time <span class="sy0">*</span> 0.6f<span class="br0">)</span> <span class="sy0">%</span> FastMath.<span class="me1">TWO_PI</span><span class="br0">)</span><span class="br0">)</span> <span class="sy0">*</span> 1.5f<span class="sy0">;</span>
  water.<span class="me1">setWaterHeight</span><span class="br0">(</span>initialWaterHeight <span class="sy0">+</span> waterHeight<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "Optional: Waves" [4705-5229] -->
<h3 class="sectionedit7" id="optionalwater_wave_and_color_effects">Optional: Water Wave and Color Effects</h3>
<div class="level3">

<p>
<a href="/resources/jme3-advanced-water-post-muddy.png" class="media" title="jme3:advanced:water-post-muddy.png"><img src="/resources/jme3-advanced-water-post-muddy.png" class="mediacenter" alt="" width="220" height="172" /></a>
</p>

<p>
All these effects are optional. Every setter also has a getter.
</p>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Water method example</th><th class="col1">Effects: Waves </th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">water.setWaterHeight(-6);</td><td class="col1">Use this waterheight method for causing waves.</td><td class="col2">0.0f</td>
	</tr>
	<tr class="row2">
		<td class="col0">water.setMaxAmplitude(0.3f);</td><td class="col1">How high the highest waves are.</td><td class="col2">1.0f</td>
	</tr>
	<tr class="row3">
		<td class="col0">water.setWaveScale(0.008f);</td><td class="col1">Sets the scale factor of the waves height map. The smaller the value, the bigger the waves!</td><td class="col2"> 0.005f </td>
	</tr>
	<tr class="row4">
		<td class="col0">water.setWindDirection(new Vector2f(0,1))</td><td class="col1">Sets the wind direction, which is the direction where the waves move</td><td class="col2">Vector2f(0.0f, -1.0f)</td>
	</tr>
	<tr class="row5">
		<td class="col0">water.setSpeed(0.7f);</td><td class="col1">How fast the waves move. Set it to 0.0f for still water.</td><td class="col2">1.0f</td>
	</tr>
	<tr class="row6">
		<td class="col0">water.setHeightTexture( (Texture2D) <br />
manager.loadTexture(“Textures/waveheight.png”) )</td><td class="col1">This height map describes the shape of the waves</td><td class="col2">“Common/MatDefs/Water/Textures/heightmap.jpg”</td>
	</tr>
	<tr class="row7">
		<td class="col0">water.setNormalTexture( (Texture2D) <br />
manager.loadTexture(“Textures/wavenormals.png”) )</td><td class="col1">This normal map describes the shape of the waves</td><td class="col2">“Common/MatDefs/Water/Textures/gradient_map.jpg”</td>
	</tr>
	<tr class="row8">
		<td class="col0">water.setUseRipples(false);</td><td class="col1">Switches the ripples effect on or off.</td><td class="col2">true</td>
	</tr>
	<tr class="row9">
		<td class="col0">water.setNormalScale(0.5f)</td><td class="col1">Sets the normal scaling factors to apply to the normal map. The higher the value, the more small ripples will be visible on the waves.</td><td class="col2">1.0f</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [5396-6560] --><div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Water method example</th><th class="col1"> Effects: Color</th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">water.setLightDirection(new Vector3f(-0.37f,-0.50f,-0.78f))</td><td class="col1">Usually you set this to the same as the light source's direction. Use this to set the light direction if the sun is moving.</td><td class="col2">Value given to WaterFilter() constructor.</td>
	</tr>
	<tr class="row2">
		<td class="col0">water.setLightColor(ColorRGBA.White)</td><td class="col1">Usually you set this to the same as the light source's color.</td><td class="col2">RGBA.White</td>
	</tr>
	<tr class="row3">
		<td class="col0">water.setWaterColor(ColorRGBA.Brown.mult(2.0f));</td><td class="col1">Sets the main water color.</td><td class="col2">greenish blue <br />
ColorRGBA(0.0f,0.5f,0.5f,1.0f)</td>
	</tr>
	<tr class="row4">
		<td class="col0">water.setDeepWaterColor(ColorRGBA.Brown);</td><td class="col1">Sets the deep water color.</td><td class="col2">dark blue <br />
ColorRGBA(0.0f, 0.0f,0.2f,1.0f)</td>
	</tr>
	<tr class="row5">
		<td class="col0">water.setWaterTransparency(0.2f);</td><td class="col1">Sets how fast colors fade out. use this to control how clear (e.g. 0.05f) or muddy (0.2f) water is.</td><td class="col2"> 0.1f </td>
	</tr>
	<tr class="row6">
		<td class="col0">water.setColorExtinction(new Vector3f(10f,20f,30f));</td><td class="col1">Sets At what depth the refraction color extincts. The three values are RGB (red, green, blue) in this order. Play with these parameters to “muddy” the water.</td><td class="col2">Vector3f(5f,20f,30f)</td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [6562-7568] --><div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Water method example</th><th class="col1"> Effects: Shore</th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">water.setCenter(Vector3f.ZERO); <br />
water.setRadius(260);</td><td class="col1">Limit the water filter to a semisphere with the given center and radius. Use this for lakes and smaller bodies of water. Skip this for oceans.</td><td class="col2">unused</td>
	</tr>
	<tr class="row2">
		<td class="col0">water.setShoreHardness(1.0f);</td><td class="col1">Sets how soft the transition between shore and water should be. High values mean a harder transition between shore and water.</td><td class="col2">0.1f</td>
	</tr>
	<tr class="row3">
		<td class="col0">water.setUseHQShoreline(false);</td><td class="col1">Renders shoreline with better quality ?</td><td class="col2">true</td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [7570-8068] --><div class="table sectionedit11"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Water method example</th><th class="col1"> Effects: Foam</th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">water.setUseFoam(false);</td><td class="col1">Switches the white foam on or off</td><td class="col2">true</td>
	</tr>
	<tr class="row2">
		<td class="col0">water.setFoamHardness(0.5f)</td><td class="col1">Sets how much the foam will blend with the shore to avoid a hard edged water plane.</td><td class="col2">1.0f</td>
	</tr>
	<tr class="row3">
		<td class="col0">water.setFoamExistence(new Vector3f(0.5f,5f,1.0f))</td><td class="col1">The three values describe what depth foam starts to fade out, at what depth it is completely invisible, at what height foam for waves appears (+ waterHeight).</td><td class="col2">Vector3f(0.45f,4.35f,1.0f)</td>
	</tr>
	<tr class="row4">
		<td class="col0">water.setFoamTexture( (Texture2D) <br />
manager.loadTexture(“Textures/foam.png”) )</td><td class="col1">This foam texture will be used with WrapMode.Repeat</td><td class="col2">“Common/MatDefs/Water/Textures/foam.jpg”</td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [8070-8715] --><div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Water method example</th><th class="col1"> Effects: Light</th><th class="col2">Default</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">water.setSunScale(1f);</td><td class="col1">Sets how big the sun should appear in the light's specular effect on the water.</td><td class="col2">3.0f</td>
	</tr>
	<tr class="row2">
		<td class="col0">water.setUseSpecular(false)</td><td class="col1">Switches specular effect on or off</td><td class="col2">true</td>
	</tr>
	<tr class="row3">
		<td class="col0">water.setShininess(0.8f)</td><td class="col1">Sets the shininess of the water reflections</td><td class="col2">0.7f</td>
	</tr>
	<tr class="row4">
		<td class="col0">water.setUseRefraction(true)</td><td class="col1">Switches the refraction effect on or off.</td><td class="col2">true</td>
	</tr>
	<tr class="row5">
		<td class="col0">water.setRefractionConstant(0.2f);</td><td class="col1">The lower the value, the less reflection can be seen on water. This is a constant related to the index of refraction (IOR) used to compute the fresnel term.</td><td class="col2">0.3f</td>
	</tr>
	<tr class="row6">
		<td class="col0">water.setRefractionStrength(-0.1)</td><td class="col1">This value modifies the current Fresnel term. If you want to weaken reflections use bigger value. If you want to empasize them, use a value smaller than 0.</td><td class="col2">0.0f</td>
	</tr>
	<tr class="row7">
		<td class="col0">water.setReflectionMapSize(256)</td><td class="col1">Sets the size of the reflection map. The higher, the better the quality, but the slower the effect.</td><td class="col2">512</td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [8717-9632] -->
</div>
<!-- EDIT7 SECTION "Optional: Water Wave and Color Effects" [5230-9634] -->
<h3 class="sectionedit13" id="sound_effects">Sound Effects</h3>
<div class="level3">

<p>
You should also add audio nodes with water sounds to complete the effect.
</p>
<pre class="code java">AudioNode waves <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sounds/Environment/Ocean Waves.ogg"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
waves.<span class="me1">setLooping</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
audioRenderer.<span class="me1">playSource</span><span class="br0">(</span>waves<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
See also: <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">audio</a>. 
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/2011/01/15/new-advanced-water-effect-for-jmonkeyengine-3/#comment-609" class="urlextern" title="http://jmonkeyengine.org/2011/01/15/new-advanced-water-effect-for-jmonkeyengine-3/#comment-609" rel="nofollow">JME3's Water Post-Process Effect</a> by Nehon</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/water.html" class="wikilink1" title="jme3:advanced:water">Simple water</a></div>
</li>
</ul>

</div>
<!-- EDIT13 SECTION "Sound Effects" [9635-] -->
