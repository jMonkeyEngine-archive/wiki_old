---
title: ShaderBlow
---
<h1 class="sectionedit1" id="shaderblow">ShaderBlow</h1>
<div class="level1">

<p>
<a href="/resources/sdk-plugin-shaderblow_intro_01.jpg" class="media" title="sdk:plugin:shaderblow_intro_01.jpg"><img src="/resources/sdk-plugin-shaderblow_intro_01.jpg" class="media" alt="" /></a>
</p>

<p>
 Collections of effects for jMonkeyEngine 3. To install the ShaderBlow plugin into the jMonkeyEngine SDK, go to Tools→Plugins→Available Plugins. 
 You can always get the source of ShaderBlow project here:  
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/#svn%2Ftrunk%2Fshaderblowlib%2FShaderBlow" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/#svn%2Ftrunk%2Fshaderblowlib%2FShaderBlow" rel="nofollow">ShaderBlow project SVN</a>
</p>

<p>
The source has many examples and tests to explain the capacity of shaders much better.
</p>
<ul>
<li class="level1"><div class="li"> Filters:</div>
<ul>
<li class="level2"><div class="li"> Basic SSAO</div>
</li>
<li class="level2"><div class="li"> ColorScale (added by @H)</div>
</li>
<li class="level2"><div class="li"> GrayScale (added by @H)</div>
</li>
<li class="level2"><div class="li"> Simple Refraction (added by @mifth)</div>
</li>
<li class="level2"><div class="li"> Old Film Effect (added by @H)</div>
</li>
<li class="level2"><div class="li"> Night Vision (added by @wezrule)</div>
</li>
<li class="level2"><div class="li"> Predator Thermal Vision (added by @wezrule)</div>
</li>
<li class="level2"><div class="li"> Frosted Glass effect (added by @wezrule)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Shaders</div>
<ul>
<li class="level2"><div class="li"> Dissolver (added by @thetoucher)</div>
</li>
<li class="level2"><div class="li"> FakeParticleBlow (added by @mifth)</div>
</li>
<li class="level2"><div class="li"> Forceshield (added by @ficik)</div>
</li>
<li class="level2"><div class="li"> MatCap (added by @mifth)</div>
</li>
<li class="level2"><div class="li"> Glass (added by @mifth)</div>
</li>
<li class="level2"><div class="li"> Texture Bombing (added by @wezrule)</div>
</li>
</ul>
</li>
</ul>

<p>
</p><p></p><div class="noteclassic">Official Forum: <a href="http://hub.jmonkeyengine.org/forum/topic/shaderblow-project/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/shaderblow-project/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/shaderblow-project/</a>
Or you can use the forum threads of shaders.
</div>

<hr />

</div>
<!-- EDIT1 SECTION "ShaderBlow" [1-1186] -->
<h3 class="sectionedit2" id="colorscale_filter">ColorScale Filter</h3>
<div class="level3">

<p>
The ColorScale filter applys a color to the render image. You can use this filter to tint the render according to one particular color without change any material (underwater scene, night scene, fire scene) or to achieve fade-in/fade-out effect.
</p>

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Allow to set the color to apply. Default is red.</div>
</li>
<li class="level1"><div class="li"> Allow to set intensity of the color. Default is 0.7f. Frag shader clamps color intensity between 0 and 1.</div>
</li>
</ul>
<div class="table sectionedit3"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/resources/sdk-plugin-colorfilter2.png" class="media" title="sdk:plugin:colorfilter2.png"><img src="/resources/sdk-plugin-colorfilter2.png" class="media" title="ColorScale Filter OFF" alt="ColorScale Filter OFF" width="400" /></a></td><td class="col1"><a href="/resources/sdk-plugin-colorfilter1.png" class="media" title="sdk:plugin:colorfilter1.png"><img src="/resources/sdk-plugin-colorfilter1.png" class="media" title="ColorScale filter ON" alt="ColorScale filter ON" width="400" /></a></td>
	</tr>
	<tr class="row1">
		<td class="col0"><a href="/resources/sdk-plugin-colorfilter3.png" class="media" title="sdk:plugin:colorfilter3.png"><img src="/resources/sdk-plugin-colorfilter3.png" class="media" title="ColorScale Filter ON" alt="ColorScale Filter ON" width="400" /></a></td><td class="col1"><a href="/resources/sdk-plugin-colorfilter4.png" class="media" title="sdk:plugin:colorfilter4.png"><img src="/resources/sdk-plugin-colorfilter4.png" class="media" title="ColorScale Filter" alt="ColorScale Filter" width="400" /></a></td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [1636-1869] -->
</div>

<h4 id="usage">Usage</h4>
<div class="level4">

<p>
Add a <a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/src/com/shaderblow/filter/colorscale/ColorScaleFilter.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/src/com/shaderblow/filter/colorscale/ColorScaleFilter.java" rel="nofollow">ColorScaleFilter</a> instance to a FilterPostProccesor instance. Set color and color intensity. Then add the FilterPostProccesor instance to Application's viewPort attribute.
</p>
<pre class="code java">		<span class="kw1">this</span>.<span class="me1">fpp</span> <span class="sy0">=</span> <span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">assetManager</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="kw1">this</span>.<span class="me1">fpp</span>.<span class="me1">setNumSamples</span><span class="br0">(</span><span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="kw1">this</span>.<span class="me1">colorScale</span> <span class="sy0">=</span> <span class="kw1">new</span> ColorScaleFilter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="kw1">this</span>.<span class="me1">fpp</span>.<span class="me1">addFilter</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">colorScale</span><span class="br0">)</span><span class="sy0">;</span>
 
		<span class="co1">// colorScale.setFilterColor(ColorRGBA.Red.clone()); // Set Filter color</span>
		<span class="co1">// colorScale.setColorDensity(0.5f); // Set Color intensity (between 0 and 1);</span>
 
		<span class="kw1">this</span>.<span class="me1">viewPort</span>.<span class="me1">addProcessor</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">fpp</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/filter/color/TestColorScale.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/filter/color/TestColorScale.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://jmonkeyengine.org/groups/contribution-depot-jme3/forum/topic/colorscale-filter/" class="urlextern" title="http://jmonkeyengine.org/groups/contribution-depot-jme3/forum/topic/colorscale-filter/" rel="nofollow">Forum threat</a>
</p>
<hr />

</div>
<!-- EDIT2 SECTION "ColorScale Filter" [1187-2871] -->
<h3 class="sectionedit4" id="grayscale_filter">GrayScale Filter</h3>
<div class="level3">

<p>
The GrayScale filter converts the render image to grayscale.
</p>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> <strong>GrayScale Filter OFF</strong> </th><th class="col1"> <strong>GrayScale Filter ON</strong> </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"><a href="/resources/sdk-plugin-grayscalefilter-off.jpg" class="media" title="sdk:plugin:grayscalefilter-off.jpg"><img src="/resources/sdk-plugin-grayscalefilter-off.jpg" class="media" title="GrayScale Filter OFF" alt="GrayScale Filter OFF" width="400" /></a></td><td class="col1"><a href="/resources/sdk-plugin-grayscalefilter-on.png" class="media" title="sdk:plugin:grayscalefilter-on.png"><img src="/resources/sdk-plugin-grayscalefilter-on.png" class="media" title="GrayScale Filter ON" alt="GrayScale Filter ON" width="400" /></a></td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [2961-3145] -->
</div>

<h4 id="usage1">Usage</h4>
<div class="level4">

<p>
Add a <a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/src/com/shaderblow/filter/grayscale/GrayScaleFilter.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/src/com/shaderblow/filter/grayscale/GrayScaleFilter.java" rel="nofollow">GrayScaleFilter</a> instance to a FilterPostProccesor instance. Then add the FilterPostProccesor instance to Application's viewPort attribute.
</p>
<pre class="code java">        <span class="kw1">this</span>.<span class="me1">fpp</span> <span class="sy0">=</span> <span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">assetManager</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Create FilterPostProcessor instance</span>
        <span class="kw1">this</span>.<span class="me1">grayScale</span> <span class="sy0">=</span> <span class="kw1">new</span> GrayScaleFilter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// Create GrayScaleFilter instance</span>
        <span class="kw1">this</span>.<span class="me1">fpp</span>.<span class="me1">addFilter</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">grayScale</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// Add GrayScaleFilter instance to FilterPostProcessor instance</span>
        <span class="kw1">this</span>.<span class="me1">viewPort</span>.<span class="me1">addProcessor</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">fpp</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// Add FilterPostProcessor instance to ViewPort</span></pre>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/filter/grayscale/TestGrayScale.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/filter/grayscale/TestGrayScale.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://jmonkeyengine.org/forum/topic/solved-grayscale-filter/" class="urlextern" title="http://jmonkeyengine.org/forum/topic/solved-grayscale-filter/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT4 SECTION "GrayScale Filter" [2872-4115] -->
<h3 class="sectionedit6" id="old_film_effect_filter">Old Film Effect Filter</h3>
<div class="level3">

<p>
Old Film filter simulate the effect of a classic looking film effect. It's a port of this <a href="http://devmaster.net/posts/2989/shader-effects-old-film" class="urlextern" title="http://devmaster.net/posts/2989/shader-effects-old-film" rel="nofollow">shader effect</a>.
</p>

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Allow to set the <strong>filter's color</strong>. Default is sepia (ColorRGBA(112f / 255f, 66f / 255f, 20f / 255f, 1.0f)).</div>
</li>
<li class="level1"><div class="li"> Allow to set the <strong>color's density</strong>. Default is 0.7. Shader clamps this value between 0 to 1. The color image gets grayscale when color's densite is set to 0.</div>
</li>
<li class="level1"><div class="li"> Allow to set the <strong>noise's density</strong>. Default is 0.4. Shader clamps this value between 0 to 1.</div>
</li>
<li class="level1"><div class="li"> Allow to set the <strong>scratches' density</strong>. Default is 0.3. Shader clamps this value between 0 to 1.</div>
</li>
<li class="level1"><div class="li"> Allow to set the <strong>vignetting's diameter</strong>. Default is 0.9. Shader clamps this value between 0 to 1.4. Vignetting effect is made using two circles. The inner circle represents the region untouched by vignetting. The region between the inner and outer circle represent the area where vignetting starts to take place, which is a gradual fade to black from the inner to outer ring. Any part of the frame outside of the outer ring would be completely black.</div>
</li>
</ul>

<p>
<strong>NOTE</strong>: I chose to clamp this value inside the frag shader code instead of using java code because I thought this way is faster (better from preformace point of view). You can clamp this values using java code if you want.
</p>
<div class="table sectionedit7"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_cgfzhkq-mkk" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_cgfzhkq-mkk">youtube_cgfzhkq-mkk</a></td><td class="col1"> </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [5489-5516] -->
</div>

<h4 id="usage2">Usage</h4>
<div class="level4">

<p>
Add a <a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/src/com/shaderblow/filter/oldfilm/OldFilmFilter.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/src/com/shaderblow/filter/oldfilm/OldFilmFilter.java" rel="nofollow">OldFilmFilter</a> instance to a FilterPostProccesor instance. Then add the FilterPostProccesor instance to Application's viewPort attribute.
</p>
<pre class="code java">        <span class="kw1">this</span>.<span class="me1">fpp</span> <span class="sy0">=</span> <span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">assetManager</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Create FilterPostProcessor instance</span>
        <span class="kw1">this</span>.<span class="me1">oldFilmFilter</span><span class="sy0">=</span> <span class="kw1">new</span> OldFilmFilter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// Create OldFilmFilter instance</span>
        <span class="kw1">this</span>.<span class="me1">fpp</span>.<span class="me1">addFilter</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">oldFilmFilter</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// Add OldFilmFilter instance to FilterPostProcessor instance</span>
        <span class="kw1">this</span>.<span class="me1">viewPort</span>.<span class="me1">addProcessor</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">fpp</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// Add FilterPostProcessor instance to ViewPort</span></pre>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/oldfilm/TestOldFilm.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/oldfilm/TestOldFilm.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://jmonkeyengine.org/forum/topic/old-film-effect-filter/" class="urlextern" title="http://jmonkeyengine.org/forum/topic/old-film-effect-filter/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT6 SECTION "Old Film Effect Filter" [4116-6506] -->
<h3 class="sectionedit8" id="lightblow_shader">LightBlow Shader</h3>
<div class="level3">

<p>
The Lightblow shader is an improved Lighting shader for JME. 
</p>

<p>
Features: 
 * Improved lighting calculations. 
 * Improved reflection calculations. 
 * Reflection map implementation with alpha normal map. 
 * Improved Minnaert calculations. 
 * Hemispherical lighting. 
 * Image Based Lighting with Albedo. 
 * Emissive map implementation with diffuse alpha. 
 * normalization of normals by default. 
 * Specular map implementation with normal map alpha. 
 * Specular intensity implementation. 
 * Switching -x/-y/-z normals for different normal maps. (3dmax, blender, xnormal have different approaches). 
 * Specular Color now works with specular maps 
 * Glowblow fragment shader is added with m_GlowIntensity? uniform. It's possible to change glow intensity  for objects. Please, use DiffuseMap? as GlowMap? instead of new additional Glow rgb texture. 
 * Lightmaps are added. 
 * Rim Lighting is added. Thanks to Thetoucher from JME Blog! 
 * Fog is added. Fog is used without post-processing! 
 * Texture Blending: 4 diffuse, 4 normal textures can be blended (Like Terrain System). 
</p>

<p>
Forum: <a href="http://jmonkeyengine.org/forum/topic/lightblow-shader/" class="urlextern" title="http://jmonkeyengine.org/forum/topic/lightblow-shader/" rel="nofollow">http://jmonkeyengine.org/forum/topic/lightblow-shader/</a>
Software for NormalMaps? making: <a href="http://shadermap.com/shadermap_pro.php" class="urlextern" title="http://shadermap.com/shadermap_pro.php" rel="nofollow">http://shadermap.com/shadermap_pro.php</a>
Software for CubeMaps? editing: <a href="http://developer.amd.com/archive/gpu/cubemapgen/pages/default.aspx" class="urlextern" title="http://developer.amd.com/archive/gpu/cubemapgen/pages/default.aspx" rel="nofollow">http://developer.amd.com/archive/gpu/cubemapgen/pages/default.aspx</a>
Watch following videos:
</p>
<div class="table sectionedit9"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_knroh_3o2uo" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_knroh_3o2uo">youtube_knroh_3o2uo</a></td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [7884-7909] -->
<p>
<a href="http://jmonkeyengine.org/forum/topic/lightblow-shader/" class="urlextern" title="http://jmonkeyengine.org/forum/topic/lightblow-shader/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT8 SECTION "LightBlow Shader" [6507-7993] -->
<h3 class="sectionedit10" id="dissolver_shader">Dissolver Shader</h3>
<div class="level3">

<p>
The Dissolve Shader uses a simple grey scale image as an animated mask to hide a material.
</p>

<p>
The shader incrementally clamps off the colour value, dark to light, and uses that for a masking texture to discard pixels.
It is currently capped for convenience at 255 frames of animation and is only using one colour channel.
In simple terms, in starts by only discarding the darkest parts of the texture map, then the slightly lighter parts, then the slightly lighter again and again until it eventually cant get any lighter (white), at which point the proccess is complete.
</p>
<div class="table sectionedit11"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/resources/sdk-plugin-dissolver-screen.png" class="media" title="sdk:plugin:dissolver-screen.png"><img src="/resources/sdk-plugin-dissolver-screen.png" class="media" title="Dissolver screenshot" alt="Dissolver screenshot" width="400" /></a></td><td class="col1"><a href="/resources/sdk-plugin-dissolver-maps.png" class="media" title="sdk:plugin:dissolver-maps.png"><img src="/resources/sdk-plugin-dissolver-maps.png" class="media" title="Mask maps" alt="Mask maps" width="400" /></a></td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [8593-8705] -->
<p>
Starting at the top left we have: simple linear dissolve, organic dissolve and pixel dissolve.
And bottom row: organic growth, texture masking, organic burn.
Mask texture maps on the second image.
</p>

<p>
The test is occolating the dissolve amount between 0 and 1. It demonstrates 6 different uses for the shader, all running at the same speed. The top row are straight forward dissolves. The bottom row shows 3 potential applications:
</p>
<ol>
<li class="level1"><div class="li"> Organic Growth (bottom left) over a mesh, this could work both animating rapidly for a fast grow effect, or set to a fixed value e.g. set to 0.5f is “50% covered in growth”;</div>
</li>
<li class="level1"><div class="li"> Texture Masking (bottom middle) , I see this is probably where the most practical applications will come from. The demonstration shows a poorely photoshoped clean street, peices of garbage are then scattered around dependant on the dissolve amount, this would work best with a fixed value eg set to .75 is “75% dirty”. Texture Masking could be also be used for:</div>
<ol>
<li class="level2"><div class="li"> paint damage on a car;</div>
</li>
<li class="level2"><div class="li"> lacerations on a character;</div>
</li>
<li class="level2"><div class="li"> the blood shot eye effect that creeps in from the sides of the screen when you’ve taken too much damage in a modern FPS.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Organic Burn (bottom right) is comprised of 2 cubes, one blue, one orange, both with the same organic dissolve, however the orange one is slightly offset ahead of the blue so it shows first (ie the dissolve amount is always slight advanced).</div>
</li>
</ol>

<p>
Watch following videos:
</p>
<div class="table sectionedit12"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_ry0r_qwfqlq" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_ry0r_qwfqlq">youtube_ry0r_qwfqlq</a></td><td class="col1"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_wufmcn1uv48" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_wufmcn1uv48">youtube_wufmcn1uv48</a></td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [10153-10202] -->
</div>

<h4 id="usage3">Usage</h4>
<div class="level4">

<p>
The shader requires 2 parameters:
</p>
<ul>
<li class="level1"><div class="li"> a Texture2D texture map to use as the dissolve map; and</div>
</li>
<li class="level1"><div class="li"> a Vector2 of internal params params:</div>
<ul>
<li class="level2"><div class="li"> the first is a float value being the amount of dissolve, a value from 0-1 : 0 being no dissolve, being fully dissolved; and</div>
</li>
<li class="level2"><div class="li"> the second value is an int use as an inversion switch, 1 to invert the dissolve/discard, 0 to leave as is.</div>
</li>
</ul>
</li>
</ul>

<p>
</p><p></p><div class="noteclassic">Dissolver is based on Common/MatDefs/Lighting.j3md. So, all Common/MatDefs/Lighting.j3md features should be available on the dissolver too.
</div>

<pre class="code java">        <span class="co1">// Create a material instance using ShaderBlow's Lighting.j3md</span>
        <span class="kw1">final</span> Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">assetManager</span>, <span class="st0">"ShaderBlow/MatDefs/Dissolve/Lighting.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Ambient"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Diffuse"</span>, ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Specular"</span>, ColorRGBA.<span class="me1">Black</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"UseMaterialColors"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="kw1">this</span>.<span class="me1">assetManager</span>.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"TestTextures/Dissolve/burnMap.png"</span>
        mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"DissolveMap"</span>, map<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set mask texture map</span>
 
        <span class="kw1">this</span>.<span class="me1">DSParams</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector2f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// standard dissolver</span>
        <span class="co1">//this.DSParamsInv = new Vector2f(0, 1); // inverted dissolver</span>
        mat.<span class="me1">setVector2</span><span class="br0">(</span><span class="st0">"DissolveParams"</span>, <span class="kw1">this</span>.<span class="me1">DSParams</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set params</span>
 
        <span class="kw1">final</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">final</span> Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/dissolve/TestDissolve.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/dissolve/TestDissolve.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://jmonkeyengine.org/groups/user-code-projects/forum/topic/dissolve-shader-1/" class="urlextern" title="http://jmonkeyengine.org/groups/user-code-projects/forum/topic/dissolve-shader-1/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT10 SECTION "Dissolver Shader" [7994-11920] -->
<h3 class="sectionedit13" id="fakeparticleblow_shader">FakeParticleBlow Shader</h3>
<div class="level3">

<p>
 Effect for fire or engine of a ship. Such an effect is used in the “Eve Online” game for ship engines.
</p>

<p>
Features:
</p>
<ol>
<li class="level1"><div class="li"> GPU animation (now you don’t need simpleUpdate(float tpf) for the shader). Animation is made displacing the texture according to X and/or Y axis.</div>
</li>
<li class="level1"><div class="li"> X and/or Y animation direction. No animation is supported also.</div>
</li>
<li class="level1"><div class="li"> Animation direction changer. By default the Y axis animation's direction is up-to-down and the X axis animation's direction is right-to-left.</div>
</li>
<li class="level1"><div class="li"> Allow to set animation speed.</div>
</li>
<li class="level1"><div class="li"> Allow to set mask texture in order to set particle shape.</div>
</li>
<li class="level1"><div class="li"> Allow to set particle color.</div>
</li>
<li class="level1"><div class="li"> Allow to set fog color. Fog color is applyed to the material using for color's alpha value as fog distance factor.</div>
</li>
</ol>
<div class="table sectionedit14"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/resources/sdk-plugin-fakeparticleblow.png" class="media" title="sdk:plugin:fakeparticleblow.png"><img src="/resources/sdk-plugin-fakeparticleblow.png" class="media" title="FakeParticleBlow" alt="FakeParticleBlow" width="400" /></a></td><td class="col1"><a href="/resources/sdk-plugin-fakeparticleblow3.png" class="media" title="sdk:plugin:fakeparticleblow3.png"><img src="/resources/sdk-plugin-fakeparticleblow3.png" class="media" title="FakeParticleBlow" alt="FakeParticleBlow" width="400" /></a> Fog applyed to blue fire</td>
	</tr>
	<tr class="row1">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_hdqop4yz-la" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_hdqop4yz-la">youtube_hdqop4yz-la</a></td><td class="col1"></td>
	</tr>
</table></div>
<!-- EDIT14 TABLE [12686-12855] -->
</div>

<h4 id="usage4">Usage</h4>
<div class="level4">

<p>
Create a material (by SDK or by code) using <a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/assets/ShaderBlow/MatDefs/FakeParticleBlow/FakeParticleBlow.j3md" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/assets/ShaderBlow/MatDefs/FakeParticleBlow/FakeParticleBlow.j3md" rel="nofollow">FakeParticleBlow.j3md</a>.
Set material's parameters and set the material to a spatial.
</p>

<p>
Most of the cases the spatial will be 4 to 10 planes in the same location but rotated on Y axis using different angles for each plane. Something similar to this:
</p>

<p>
<a href="/resources/sdk-plugin-fakeobject.png" class="media" title="sdk:plugin:fakeobject.png"><img src="/resources/sdk-plugin-fakeobject.png" class="media" alt="" width="100" /></a>
</p>

<p>
</p><p></p><div class="noteimportant">Remenber to set the queue bucket to transparent for the spatial.
</div>

<pre class="code java">        <span class="co1">// Create the material</span>
        <span class="kw1">final</span> Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">assetManager</span>,
                <span class="st0">"ShaderBlow/MatDefs/FakeParticleBlow/FakeParticleBlow.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Create the mask texture to use</span>
        <span class="kw1">final</span> Texture maskTex <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">assetManager</span>.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"TestTextures/FakeParticleBlow/mask.png"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"MaskMap"</span>, maskTex<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Create the texture to use for the spatial.</span>
        <span class="kw1">final</span> Texture aniTex <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">assetManager</span>.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"TestTextures/FakeParticleBlow/particles.png"</span><span class="br0">)</span><span class="sy0">;</span>
        aniTex.<span class="me1">setWrap</span><span class="br0">(</span>WrapMode.<span class="me1">MirroredRepeat</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// NOTE: Set WrapMode = MirroredRepeat in order to animate the texture</span>
        mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"AniTexMap"</span>, aniTex<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set texture</span>
 
        mat.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"TimeSpeed"</span>, <span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set animation speed</span>
 
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"BaseColor"</span>, ColorRGBA.<span class="me1">Green</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set base color to apply to the texture</span>
 
        <span class="co1">// mat.setBoolean("Animation_X", true); // Enable X axis animation</span>
        mat.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"Animation_Y"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Enable Y axis animation</span>
        mat.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"Change_Direction"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Change direction of the texture animation</span>
 
        mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setFaceCullMode</span><span class="br0">(</span>FaceCullMode.<span class="me1">Off</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Allow to see both sides of a face</span>
        mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBlendMode</span><span class="br0">(</span>BlendMode.<span class="me1">Additive</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="kw1">final</span> ColorRGBA fogColor <span class="sy0">=</span> ColorRGBA.<span class="me1">Black</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        fogColor.<span class="me1">a</span> <span class="sy0">=</span> <span class="nu0">10</span><span class="sy0">;</span> <span class="co1">// fogColor's alpha value is used to calculate the intensity of the fog (distance to apply fog)</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"FogColor"</span>, fogColor<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set fog color to apply to the spatial.</span>
 
        <span class="kw1">final</span> Quad quad <span class="sy0">=</span> <span class="kw1">new</span> Quad<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Create an spatial. A plane in this case</span>
        <span class="kw1">final</span> Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Particle"</span>, quad<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Assign the material to the spatial</span>
        TangentBinormalGenerator.<span class="me1">generate</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setQueueBucket</span><span class="br0">(</span>Bucket.<span class="me1">Transparent</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Remenber to set the queue bucket to transparent for the spatial</span></pre>

<p>
To get green/yellow/blue fog (not transparency):
</p>
<pre class="code java">        mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBlendMode</span><span class="br0">(</span>BlendMode.<span class="me1">AlphaAdditive</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">final</span> ColorRGBA fogColor <span class="sy0">=</span> ColorRGBA.<span class="me1">Blue</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Several planes geometries will be required as there will be AlphaAdditive material.
</p>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/fakeparticleblow/TestFakeParticleBlow.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/fakeparticleblow/TestFakeParticleBlow.java" rel="nofollow">TestCase 1</a>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/fakeparticleblow/TestFakeParticleBlow2.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/fakeparticleblow/TestFakeParticleBlow2.java" rel="nofollow">TestCase 2</a>
</p>

<p>
<a href="http://jmonkeyengine.org/groups/contribution-depot-jme3/forum/topic/fakeparticleblow-shader/" class="urlextern" title="http://jmonkeyengine.org/groups/contribution-depot-jme3/forum/topic/fakeparticleblow-shader/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT13 SECTION "FakeParticleBlow Shader" [11921-16172] -->
<h3 class="sectionedit15" id="forceshield_shader">Forceshield Shader</h3>
<div class="level3">

<p>
Forcefield shader adds shield effect to a spatial.
The spatial will be a sphere most of the cases, but box or oval should be possible to use. Only problem is that it has to be higher-poly because distace is calculated from vertex.
</p>

<p>
Hits are registred as contact point position using this control and effect animation is based on distance from contact point and time.
Max number of hits displayed is 4.
</p>

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Allow to set texture of the shield.</div>
</li>
<li class="level1"><div class="li"> Allow to set color of the shield.</div>
</li>
<li class="level1"><div class="li"> Allow to set minimal visibility (similar to alpha value). Default is 0, that means shield is no displayed, only hit animations.</div>
</li>
<li class="level1"><div class="li"> Allow to set effect duration. Default is 0.5s.</div>
</li>
<li class="level1"><div class="li"> Allow to set effect size. Default is 1.</div>
</li>
<li class="level1"><div class="li"> Allow to enable/disable hit animations.</div>
</li>
</ul>
<div class="table sectionedit16"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_uu2nbabm9pk" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_uu2nbabm9pk">youtube_uu2nbabm9pk</a></td><td class="col1"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_urzmiuehscc" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_urzmiuehscc">youtube_urzmiuehscc</a></td>
	</tr>
</table></div>
<!-- EDIT16 TABLE [16966-17015] -->
</div>

<h4 id="usage5">Usage</h4>
<div class="level4">

<p>
Create a Spatial instance. Create a <a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/src/com/shaderblow/forceshield/ForceShieldControl.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/src/com/shaderblow/forceshield/ForceShieldControl.java" rel="nofollow">ForceShieldControl</a> instance.
Add the control instance to the spatial.
</p>

<p>
</p><p></p><div class="noteimportant">If you experience problems, try higher polygon object.
</div>

<pre class="code java">        <span class="co1">// Create spatial to be the shield</span>
        <span class="kw1">final</span> Sphere sphere <span class="sy0">=</span> <span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">30</span>, <span class="nu0">30</span>, 1.2f<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">final</span> Geometry shield <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"forceshield"</span>, sphere<span class="br0">)</span><span class="sy0">;</span>
        shield.<span class="me1">setQueueBucket</span><span class="br0">(</span>Bucket.<span class="me1">Transparent</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Remenber to set the queue bucket to transparent for the spatial</span>
 
        <span class="co1">// Create ForceShieldControl</span>
        <span class="kw1">this</span>.<span class="me1">forceShieldControl</span> <span class="sy0">=</span> <span class="kw1">new</span> ForceShieldControl<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">assetManager</span>, 0.5f<span class="br0">)</span><span class="sy0">;</span>
        shield.<span class="me1">addControl</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">forceShieldControl</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Add the control to the spatial</span>
        <span class="kw1">this</span>.<span class="me1">forceShieldControl</span>.<span class="me1">setEffectSize</span><span class="br0">(</span>2f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set the effect size</span>
        <span class="kw1">this</span>.<span class="me1">forceShieldControl</span>.<span class="me1">setColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">3</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set effect color</span>
        <span class="kw1">this</span>.<span class="me1">forceShieldControl</span>.<span class="me1">setVisibility</span><span class="br0">(</span>0.1f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Set shield visibility.</span>
 
        <span class="co1">// Set a texture to the shield</span>
        <span class="kw1">this</span>.<span class="me1">forceShieldControl</span>.<span class="me1">setTexture</span><span class="br0">(</span><span class="kw1">this</span>.<span class="me1">assetManager</span>.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"TestTextures/ForceShield/fs_texture.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// this.forceShieldControl.setEnabled(false); // Enable, disable animation.</span></pre>

<p>
Use <em>forceShieldControl.registerHit(final Vector3f position)</em> method to register a hit.
</p>
<pre class="code java">            <span class="kw1">final</span> CollisionResults crs <span class="sy0">=</span> <span class="kw1">new</span> CollisionResults<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">this</span>.<span class="me1">rootNode</span>.<span class="me1">collideWith</span><span class="br0">(</span><span class="kw1">new</span> Ray<span class="br0">(</span><span class="kw1">this</span>.<span class="me1">cam</span>.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span>, <span class="kw1">this</span>.<span class="me1">cam</span>.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>, crs<span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">if</span> <span class="br0">(</span>crs.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
 
                <span class="co1">// Register a hit</span>
                <span class="kw1">this</span>.<span class="me1">forceShieldControl</span>.<span class="me1">registerHit</span><span class="br0">(</span>crs.<span class="me1">getClosestCollision</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getContactPoint</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span></pre>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/forceshield/TestShield.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/forceshield/TestShield.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://jmonkeyengine.org/groups/user-code-projects/forum/topic/forceshield-my-very-first-shader/" class="urlextern" title="http://jmonkeyengine.org/groups/user-code-projects/forum/topic/forceshield-my-very-first-shader/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT15 SECTION "Forceshield Shader" [16173-19119] -->
<h3 class="sectionedit17" id="matcap_shader">MatCap Shader</h3>
<div class="level3">

<p>
MatCap shader will be very useful for scrollshooters to imitate different materials like glass, gold, metals.
The shader does not use any lights, only one texture.
</p>

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Fog color and fog skybox.</div>
</li>
<li class="level1"><div class="li"> Toon edge effect.</div>
</li>
<li class="level1"><div class="li"> Multiply color: set a color to change texture's color.</div>
</li>
<li class="level1"><div class="li"> Normal map.</div>
</li>
</ul>
<div class="table sectionedit18"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/resources/sdk-plugin-shaderblow_matcap.jpg" class="media" title="sdk:plugin:shaderblow_matcap.jpg"><img src="/resources/sdk-plugin-shaderblow_matcap.jpg" class="media" title="MatCap shader" alt="MatCap shader" width="400" /></a></td><td class="col1"><a href="/resources/sdk-plugin-matcap3.png" class="media" title="sdk:plugin:matcap3.png"><img src="/resources/sdk-plugin-matcap3.png" class="media" title="Multiply color" alt="Multiply color" width="400" /></a></td>
	</tr>
	<tr class="row1">
		<td class="col0"><a href="/resources/sdk-plugin-matcap1.png" class="media" title="sdk:plugin:matcap1.png"><img src="/resources/sdk-plugin-matcap1.png" class="media" title="Toon edge effect" alt="Toon edge effect" width="400" /></a></td><td class="col1"><a href="/resources/sdk-plugin-matcap2.png" class="media" title="sdk:plugin:matcap2.png"><img src="/resources/sdk-plugin-matcap2.png" class="media" title="Fog effect" alt="Fog effect" width="400" /></a></td>
	</tr>
</table></div>
<!-- EDIT18 TABLE [19448-19646] -->
</div>

<h4 id="usage6">Usage</h4>
<div class="level4">

<p>
Create a material (by SDK or by code) using <a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/assets/ShaderBlow/MatDefs/MatCap/MatCap.j3md" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/assets/ShaderBlow/MatDefs/MatCap/MatCap.j3md" rel="nofollow">MatCap.j3md</a>. Set material's parameters and set the material to a spatial.
</p>

<p>
</p><p></p><div class="noteimportant">Remember to add a DirectionalLight if you want to use toon edge effect.
</div>

<pre class="code">Material My Material : ShaderBlow/MatDefs/MatCap/MatCap.j3md {
     MaterialParameters {
        DiffuseMap : Flip TestTextures/matcaps/met2.png
        Nor_Inv_Y : true
        Nor_Inv_X : false
        Nor_Inv_Z : false
        NormalMap : TestModels/LightBlow/jme_lightblow_nor.png
        FogSkyBox : Flip TestTextures/Water256.dds
        
        Toon : true
        EdgesColor : 1.0 0.0 0.0 1.0
        EdgeSize : 0.01
        Fog_Edges : true
     }
    AdditionalRenderState {
    }
}</pre>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/matcap/TestMatCap.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/matcap/TestMatCap.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://jmonkeyengine.org/groups/graphics/forum/topic/glsl-matcap-shader-advice-needed/" class="urlextern" title="http://jmonkeyengine.org/groups/graphics/forum/topic/glsl-matcap-shader-advice-needed/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT17 SECTION "MatCap Shader" [19120-20785] -->
<h3 class="sectionedit19" id="glass_shader">Glass Shader</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Fog color and fog skybox.</div>
</li>
<li class="level1"><div class="li"> Toon edge effect.</div>
</li>
<li class="level1"><div class="li"> Multiply color: set a color to change texture's color.</div>
</li>
<li class="level1"><div class="li"> Normal map.</div>
</li>
</ul>
<div class="table sectionedit20"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/resources/sdk-plugin-glass-shader.png" class="media" title="sdk:plugin:glass-shader.png"><img src="/resources/sdk-plugin-glass-shader.png" class="media" title="Glass shader" alt="Glass shader" width="400" /></a></td><td class="col1"><a href="/resources/sdk-plugin-glass-shader2.png" class="media" title="sdk:plugin:glass-shader2.png"><img src="/resources/sdk-plugin-glass-shader2.png" class="media" title="Glass Shader and Fog Color effect" alt="Glass Shader and Fog Color effect" width="400" /></a></td>
	</tr>
</table></div>
<!-- EDIT20 TABLE [20950-21073] -->
</div>

<h4 id="usage7">Usage</h4>
<div class="level4">

<p>
Create a material (by SDK or by code) using <a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/assets/ShaderBlow/MatDefs/Glass/Glass.j3md" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/assets/ShaderBlow/MatDefs/Glass/Glass.j3md" rel="nofollow">Glass.j3md</a>. Set material's parameters and set the material to a spatial.
</p>

<p>
</p><p></p><div class="noteimportant">Remember to add a DirectionalLight if you want to use toon edge effect.
</div>

<pre class="code">Material My Material : ShaderBlow/MatDefs/Glass/Glass.j3md {
     MaterialParameters {

        RefMap : Flip TestTextures/Water256.dds
        Multiply_Color : 1.1 1.5 1.1 1.0
        colorIntensity : 0.79999995
        Nor_Inv_Y : true
        NormalMap : TestModels/LightBlow/jme_lightblow_nor.png
        ChromaticAbberation : true
        abberIndex : 0.04
        specularIntensity : 0.59999996
        
        Toon : true
        EdgesColor : 0.2 1.0 0.0 1.0
        EdgeSize : 0.01
        Fog_Edges : true
     }
    AdditionalRenderState {
    }
}</pre>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/glass/TestGlass.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/ShaderBlow/test-src/com/shaderblow/test/glass/TestGlass.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://jmonkeyengine.org/groups/graphics/forum/topic/glsl-glass-shader-advice-is-needed/" class="urlextern" title="http://jmonkeyengine.org/groups/graphics/forum/topic/glsl-glass-shader-advice-is-needed/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT19 SECTION "Glass Shader" [20786-22274] -->
<h3 class="sectionedit21" id="simplerefraction_postprocessor_filter">SimpleRefraction PostProcessor/Filter</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Cool refraction effect</div>
</li>
</ul>
<div class="table sectionedit22"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_eaukcu5grmc" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_eaukcu5grmc">youtube_eaukcu5grmc</a></td>
	</tr>
</table></div>
<!-- EDIT22 TABLE [22362-22387] -->
</div>

<h4 id="usage8">Usage</h4>
<div class="level4">

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/simplerefraction/TestSimpleRefraction.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/simplerefraction/TestSimpleRefraction.java" rel="nofollow">TestCase for PostProcessor</a>
</p>

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/simplerefractionfilter/TestSimpleRefractionFilter.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/simplerefractionfilter/TestSimpleRefractionFilter.java" rel="nofollow">TestCase for Filter</a>
</p>
<hr />

</div>
<!-- EDIT21 SECTION "SimpleRefraction PostProcessor/Filter" [22275-22833] -->
<h3 class="sectionedit23" id="basicssao_filter">BasicSSAO Filter</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Cool Shadows.</div>
</li>
</ul>
<div class="table sectionedit24"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/resources/sdk-plugin-shaderblow_ssao.png" class="media" title="sdk:plugin:shaderblow_ssao.png"><img src="/resources/sdk-plugin-shaderblow_ssao.png" class="media" title="Glass shader" alt="Glass shader" width="400" /></a></td>
	</tr>
</table></div>
<!-- EDIT24 TABLE [22893-22947] -->
</div>

<h4 id="usage9">Usage</h4>
<div class="level4">

<p>
<a href="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/basicssao/TestBasicSSAO.java" class="urlextern" title="http://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/basicssao/TestBasicSSAO.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://jmonkeyengine.org/groups/user-code-projects/forum/topic/wip-custom-ambient-occlusion-filter/" class="urlextern" title="http://jmonkeyengine.org/groups/user-code-projects/forum/topic/wip-custom-ambient-occlusion-filter/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT23 SECTION "BasicSSAO Filter" [22834-23270] -->
<h3 class="sectionedit25" id="electricity_shaders">Electricity Shaders</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Cool Electricity effect</div>
</li>
</ul>
<div class="table sectionedit26"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_jdtes95hnpe" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_jdtes95hnpe">youtube_jdtes95hnpe</a></td>
	</tr>
</table></div>
<!-- EDIT26 TABLE [23341-23366] -->
<p>
<a href="http://jmonkeyengine.org/forum/topic/electricity-shaders/" class="urlextern" title="http://jmonkeyengine.org/forum/topic/electricity-shaders/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT25 SECTION "Electricity Shaders" [23271-23449] -->
<h3 class="sectionedit27" id="simplesprite_shader">SimpleSprite Shader</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> GPU animated texture.</div>
</li>
</ul>
<div class="table sectionedit28"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/resources/sdk-plugin-shaderblow_simplesprite_shader.png" class="media" title="sdk:plugin:shaderblow_simplesprite_shader.png"><img src="/resources/sdk-plugin-shaderblow_simplesprite_shader.png" class="media" title="Glass shader" alt="Glass shader" width="400" /></a></td>
	</tr>
</table></div>
<!-- EDIT28 TABLE [23518-23587] --><div class="table sectionedit29"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_7xfxbt-dw3i" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_7xfxbt-dw3i">youtube_7xfxbt-dw3i</a></td>
	</tr>
</table></div>
<!-- EDIT29 TABLE [23589-23614] -->
<p>
<a href="http://jmonkeyengine.org/groups/graphics/forum/topic/texture-animation-shader-help-needed/" class="urlextern" title="http://jmonkeyengine.org/groups/graphics/forum/topic/texture-animation-shader-help-needed/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT27 SECTION "SimpleSprite Shader" [23450-23730] -->
<h3 class="sectionedit30" id="bubble_shader">Bubble Shader</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Cool nice bubble.</div>
</li>
</ul>
<div class="table sectionedit31"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_rkfblz1eohg" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_rkfblz1eohg">youtube_rkfblz1eohg</a></td>
	</tr>
</table></div>
<!-- EDIT31 TABLE [23790-23815] -->
<p>
<a href="http://jmonkeyengine.org/forum/topic/bubble-shader/" class="urlextern" title="http://jmonkeyengine.org/forum/topic/bubble-shader/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT30 SECTION "Bubble Shader" [23731-23891] -->
<h3 class="sectionedit32" id="simplespriteparticle_shader">SimpleSpriteParticle Shader</h3>
<div class="level3">

<p>
Features:
static sprite speed: can render 1500000 sprites at 149 fps ( 0% cpu load, speed limited only by graphics card ). As long as you don’t change them (add, move, delete, change image). 
FULL LIBRARY PLUGIN: <a href="http://code.google.com/p/petomancer/downloads/detail?name=SpriteLibrary.zip&amp;can=2&amp;q=" class="urlextern" title="http://code.google.com/p/petomancer/downloads/detail?name=SpriteLibrary.zip&amp;can=2&amp;q=" rel="nofollow">http://code.google.com/p/petomancer/downloads/detail?name=SpriteLibrary.zip&amp;can=2&amp;q=</a>
</p>

<p>
<a href="/resources/sdk-plugin-shaderblow_simplespriteparticle_shader.png" class="media" title="sdk:plugin:shaderblow_simplespriteparticle_shader.png"><img src="/resources/sdk-plugin-shaderblow_simplespriteparticle_shader.png" class="media" alt="" width="400" /></a>
</p>

<p>
<a href="http://jmonkeyengine.org/groups/contribution-depot-jme3/forum/topic/spritelibrary-efficient-render-of-sprites/" class="urlextern" title="http://jmonkeyengine.org/groups/contribution-depot-jme3/forum/topic/spritelibrary-efficient-render-of-sprites/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT32 SECTION "SimpleSpriteParticle Shader" [23892-24432] -->
<h3 class="sectionedit33" id="texture_bombing">Texture Bombing</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Applying random images from a texture atlas to a model by dividing up the model's UV textures into cells.</div>
</li>
</ul>
<div class="table sectionedit34"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_3lbhu2c5v8o" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_3lbhu2c5v8o">youtube_3lbhu2c5v8o</a></td>
	</tr>
</table></div>
<!-- EDIT34 TABLE [24583-24608] -->
</div>

<h4 id="usage10">Usage</h4>
<div class="level4">

<p>
<a href="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/texturebombing/TestTextureBombing.java" class="urlextern" title="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/texturebombing/TestTextureBombing.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://hub.jmonkeyengine.org/forum/topic/textureglyph-bombing-shader/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/textureglyph-bombing-shader/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT33 SECTION "Texture Bombing" [24433-24904] -->
<h3 class="sectionedit35" id="night_vision">Night Vision</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Apply a mask (Binoculars) and color to emulate night vision mode.</div>
</li>
</ul>
<div class="table sectionedit36"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_mnsjavutdps" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_mnsjavutdps">youtube_mnsjavutdps</a></td>
	</tr>
</table></div>
<!-- EDIT36 TABLE [25012-25037] -->
</div>

<h4 id="usage11">Usage</h4>
<div class="level4">

<p>
<a href="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/nightvision/TestNightVision.java" class="urlextern" title="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/nightvision/TestNightVision.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://hub.jmonkeyengine.org/forum/topic/night-vision-filter-available-in-shaderblow-plugin/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/night-vision-filter-available-in-shaderblow-plugin/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT35 SECTION "Night Vision" [24905-25357] -->
<h3 class="sectionedit37" id="predator_thermal_vision">Predator Thermal Vision</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Changes the color in the scene to emulate the predator thermal vision effect</div>
</li>
</ul>
<div class="table sectionedit38"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_dqbwcwvwtfq" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_dqbwcwvwtfq">youtube_dqbwcwvwtfq</a></td>
	</tr>
</table></div>
<!-- EDIT38 TABLE [25487-25512] -->
</div>

<h4 id="usage12">Usage</h4>
<div class="level4">

<p>
<a href="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/predatorvision/TestPredatorVision.java?spec=svn1097&amp;r=1097" class="urlextern" title="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/predatorvision/TestPredatorVision.java?spec=svn1097&amp;r=1097" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://hub.jmonkeyengine.org/forum/topic/predator-thermal-vision-filter-available-in-the-shaderblow-plugin/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/predator-thermal-vision-filter-available-in-the-shaderblow-plugin/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT37 SECTION "Predator Thermal Vision" [25358-25873] -->
<h3 class="sectionedit39" id="frosted_glass_effect">Frosted glass effect</h3>
<div class="level3">

<p>
Features:
</p>
<ul>
<li class="level1"><div class="li"> Displays a frosted glass effect over the current scene</div>
</li>
</ul>
<div class="table sectionedit40"><table class="inline">
	<tr class="row0">
		<td class="col0"><a href="/lib/exe/fetch.php/sdk:plugin:youtube_bb0jvjqvurw" class="media mediafile mf_ wikilink2" title="sdk:plugin:youtube_bb0jvjqvurw">youtube_bb0jvjqvurw</a></td>
	</tr>
</table></div>
<!-- EDIT40 TABLE [25978-26003] -->
</div>

<h4 id="usage13">Usage</h4>
<div class="level4">

<p>
<a href="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/frostedglass/TestFrostedGlass.java" class="urlextern" title="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/trunk/shaderblowlib/ShaderBlow/test-src/com/shaderblow/test/filter/frostedglass/TestFrostedGlass.java" rel="nofollow">TestCase</a>
</p>

<p>
<a href="http://hub.jmonkeyengine.org/forum/topic/frosted-glass-filter-available-in-the-shaderblow-plugin/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/frosted-glass-filter-available-in-the-shaderblow-plugin/" rel="nofollow">Forum thread</a>
</p>
<hr />

</div>
<!-- EDIT39 SECTION "Frosted glass effect" [25874-] -->
