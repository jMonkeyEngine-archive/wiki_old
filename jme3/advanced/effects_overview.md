---
title: jME3 Special Effects Overview
---
<h1 class="sectionedit1" id="jme3_special_effects_overview">jME3 Special Effects Overview</h1>
<div class="level1">

<p>
jME3 supports several types of special effects: Post-Processor Filters, SceneProcessors, and Particle Emitters (also known as particle systems). This list contains screenshots and links to sample code that demonstrates how to add the effect to a scene.
</p>

</div>
<!-- EDIT1 SECTION "jME3 Special Effects Overview" [1-299] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> There is one <code>com.jme3.effect.ParticleEmitter</code> class for all Particle Systems. </div>
</li>
<li class="level1"><div class="li"> There is one <code>com.jme3.post.FilterPostProcessor</code> class and several <code>com.jme3.post.filters.*</code> classes (all Filters have <code>*Filter</code> in their names). </div>
</li>
<li class="level1"><div class="li"> There are several <code>SceneProcessor</code> classes in various packages, including e.g. <code>com.jme3.shadow.*</code> and <code>com.jme3.water.*</code> (SceneProcessor have <code>*Processor</code> or <code>*Renderer</code> in their names).</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [300-768] -->
<h3 class="sectionedit3" id="particle_emitter">Particle Emitter</h3>
<div class="level3">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyGame <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ParticleEmitter pm <span class="sy0">=</span> <span class="kw1">new</span> ParticleEmitter<span class="br0">(</span><span class="st0">"my particle effect"</span>, Type.<span class="me1">Triangle</span>, <span class="nu0">60</span><span class="br0">)</span><span class="sy0">;</span>
    Material pmMat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Particle.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    pmMat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Texture"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Effects/spark.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    pm.<span class="me1">setMaterial</span><span class="br0">(</span>pmMat<span class="br0">)</span><span class="sy0">;</span>
    pm.<span class="me1">setImagesX</span><span class="br0">(</span><span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    pm.<span class="me1">setImagesY</span><span class="br0">(</span><span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pm<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// attach one or more emitters to any node</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Particle Emitter" [769-1298] -->
<h3 class="sectionedit4" id="scene_processor">Scene Processor</h3>
<div class="level3">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyGame <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
    <span class="kw1">private</span> BasicShadowRenderer bsr<span class="sy0">;</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        bsr <span class="sy0">=</span> <span class="kw1">new</span> BasicShadowRenderer<span class="br0">(</span>assetManager, <span class="nu0">1024</span><span class="br0">)</span><span class="sy0">;</span>
        bsr.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>.3f, <span class="sy0">-</span>0.5f, <span class="sy0">-</span>0.5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>bsr<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// add one or more sceneprocessor to viewport</span>
    <span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "Scene Processor" [1299-1674] -->
<h3 class="sectionedit5" id="post-processor_filter">Post-Processor Filter</h3>
<div class="level3">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyGame <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
    <span class="kw1">private</span> FilterPostProcessor fpp<span class="sy0">;</span> <span class="co1">// one FilterPostProcessor per app</span>
    <span class="kw1">private</span> SomeFilter sf<span class="sy0">;</span>           <span class="co1">// one or more Filters per app</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        fpp <span class="sy0">=</span> <span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span>
        viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>fpp<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// add one FilterPostProcessor to viewPort</span>
 
        sf <span class="sy0">=</span> <span class="kw1">new</span> SomeFilter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        fpp.<span class="me1">addFilter</span><span class="br0">(</span>sf<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// add one or more Filters to FilterPostProcessor</span>
    <span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "Post-Processor Filter" [1675-2201] -->
<h2 class="sectionedit6" id="water">Water</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-water-post.png" class="media" title="jme3:advanced:water-post.png"><img src="/resources/jme3-advanced-water-post.png" class="mediaright" alt="" width="150" height="100" /></a><a href="/resources/jme3-advanced-water.png" class="media" title="jme3:advanced:water.png"><img src="/resources/jme3-advanced-water.png" class="mediaright" alt="" width="150" height="100" /></a>
The jMonkeyEngine's <a href="/jme3/advanced/water.html" class="wikilink1" title="jme3:advanced:water">"SeaMonkey" WaterFilter</a> simulates ocean waves, foam, including cool underwater caustics. 
Use the SimpleWaterProcessor (SceneProcessor) for small, limited bodies of water, such as puddles, drinking troughs, pools, fountains.
</p>

<p>
See also the <a href="http://jmonkeyengine.org/2011/01/15/new-advanced-water-effect-for-jmonkeyengine-3" class="urlextern" title="http://jmonkeyengine.org/2011/01/15/new-advanced-water-effect-for-jmonkeyengine-3" rel="nofollow">Rendering Water as Post-Process Effect</a> announcement with video.
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestSceneWater.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestSceneWater.java" rel="nofollow">jme3/src/test/jme3test/water/TestSceneWater.java</a> – SimpleWaterProcessor (SceneProcessor)</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestSimpleWater.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestSimpleWater.java" rel="nofollow">jme3/src/test/jme3test/water/TestSimpleWater.java</a> – SimpleWaterProcessor (SceneProcessor)</div>
</li>
</ul>

<p>
<a href="/resources/jme3-advanced-water-reflection-muddy.png" class="media" title="jme3:advanced:water-reflection-muddy.png"><img src="/resources/jme3-advanced-water-reflection-muddy.png" class="mediaright" alt="" width="150" height="100" /></a><a href="/resources/jme3-advanced-underwater2.jpg" class="media" title="jme3:advanced:underwater2.jpg"><img src="/resources/jme3-advanced-underwater2.jpg" class="mediaright" title="underwater2.jpg" alt="underwater2.jpg" width="150" height="100" /></a>
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestPostWater.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestPostWater.java" rel="nofollow">jme3/src/test/jme3test/water/TestPostWater.java</a> – WaterFilter</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestPostWaterLake.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/water/TestPostWaterLake.java" rel="nofollow">jme3/src/test/jme3test/water/TestPostWaterLake.java</a> – WaterFilter</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Water" [2202-3620] -->
<h2 class="sectionedit7" id="environment_effects">Environment Effects</h2>
<div class="level2">

</div>
<!-- EDIT7 SECTION "Environment Effects" [3621-3653] -->
<h3 class="sectionedit8" id="depth_of_field_blur">Depth of Field Blur</h3>
<div class="level3">

<p>
<a href="/resources/jme3-advanced-dof-blur.png" class="media" title="jme3:advanced:dof-blur.png"><img src="/resources/jme3-advanced-dof-blur.png" class="mediaright" alt="" width="150" height="100" /></a><a href="/resources/jme3-advanced-light-scattering-filter.png" class="media" title="jme3:advanced:light-scattering-filter.png"><img src="/resources/jme3-advanced-light-scattering-filter.png" class="mediaright" alt="" width="150" height="100" /></a>
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestDepthOfField.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestDepthOfField.java" rel="nofollow">jme3/src/test/jme3test/post/TestDepthOfField.java</a> – DepthOfFieldFilter</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Depth of Field Blur" [3654-3972] -->
<h3 class="sectionedit9" id="fog">Fog</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestFog.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestFog.java" rel="nofollow">jme3/src/test/jme3test/post/TestFog.java</a> – FogFilter</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Fog" [3973-4152] -->
<h3 class="sectionedit10" id="light_scattering">Light Scattering</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestLightScattering.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestLightScattering.java" rel="nofollow">jme3/src/test/jme3test/post/TestLightScattering.java</a> – LightScatteringFilter</div>
</li>
</ul>

</div>
<!-- EDIT10 SECTION "Light Scattering" [4153-4381] -->
<h3 class="sectionedit11" id="vegetation">Vegetation</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Contribution: <a href="/jme3/contributions/vegetationsystem/grass.html" class="wikilink1" title="jme3:contributions:vegetationsystem:grass">Grass System</a></div>
</li>
<li class="level1"><div class="li"> Contribution: <a href="http://jmonkeyengine.org/groups/user-code-projects/forum/topic/generating-vegetation-paged-geometry-style/" class="urlextern" title="http://jmonkeyengine.org/groups/user-code-projects/forum/topic/generating-vegetation-paged-geometry-style/" rel="nofollow">Trees (WIP)</a></div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "Vegetation" [4382-4619] -->
<h2 class="sectionedit12" id="light_and_shadows">Light and Shadows</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-tanlglow1.png" class="media" title="jme3:advanced:tanlglow1.png"><img src="/resources/jme3-advanced-tanlglow1.png" class="mediaright" alt="" width="150" height="100" /></a><a href="/resources/jme3-advanced-shadow-sponza-ssao.png" class="media" title="jme3:advanced:shadow-sponza-ssao.png"><img src="/resources/jme3-advanced-shadow-sponza-ssao.png" class="mediaright" alt="" width="150" height="100" /></a>
</p>

</div>
<!-- EDIT12 SECTION "Light and Shadows" [4620-4743] -->
<h3 class="sectionedit13" id="bloom_and_glow">Bloom and Glow</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestBloom.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestBloom.java" rel="nofollow">jme3/src/test/jme3test/post/TestBloom.java</a></div>
</li>
<li class="level1"><div class="li"> More details: <a href="/jme3/advanced/bloom_and_glow.html" class="wikilink1" title="jme3:advanced:bloom_and_glow">Bloom and Glow</a> – BloomFilter</div>
</li>
</ul>

</div>
<!-- EDIT13 SECTION "Bloom and Glow" [4744-4990] -->
<h3 class="sectionedit14" id="light">Light</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestSimpleLighting.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestSimpleLighting.java" rel="nofollow">jme3/src/test/jme3test/light/TestSimpleLighting.java</a> – DirectionalLight, PointLight</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestLightRadius.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestLightRadius.java" rel="nofollow">jme3/src/test/jme3test/light/TestLightRadius.java</a> – DirectionalLight, PointLight</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestManyLights.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestManyLights.java" rel="nofollow">jme3/src/test/jme3test/light/TestManyLights.java</a> – .j3o scene</div>
</li>
<li class="level1"><div class="li"> More details: <a href="/jme3/advanced/light_and_shadow.html" class="wikilink1" title="jme3:advanced:light_and_shadow">Light and Shadow</a></div>
</li>
</ul>

<p>
<a href="/resources/jme3-advanced-shadow.png" class="media" title="jme3:advanced:shadow.png"><img src="/resources/jme3-advanced-shadow.png" class="mediaright" alt="" width="150" height="100" /></a><a href="/resources/jme3-advanced-light-sources.png" class="media" title="jme3:advanced:light-sources.png"><img src="/resources/jme3-advanced-light-sources.png" class="mediaright" alt="" width="150" height="100" /></a>
</p>

</div>
<!-- EDIT14 SECTION "Light" [4991-5735] -->
<h3 class="sectionedit15" id="shadow">Shadow</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestShadow.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestShadow.java" rel="nofollow">jme3/src/test/jme3test/light/TestShadow.java</a> – BasicShadowRenderer (SceneProcessor)</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestPssmShadow.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestPssmShadow.java" rel="nofollow">jme3/src/test/jme3test/light/TestPssmShadow.java</a> – PssmShadowRenderer (SceneProcessor), also known as Parallel-Split Shadow Mapping (PSSM).</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestSSAO.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestSSAO.java" rel="nofollow">jme3/src/test/jme3test/post/TestSSAO.java</a>, <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestSSAO2.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestSSAO2.java" rel="nofollow">jme3/src/test/jme3test/post/TestSSAO2.java</a> – SSAOFilter, also known as Screen-Space Ambient Occlusion shadows (SSOA).</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestTransparentSSAO.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestTransparentSSAO.java" rel="nofollow">jme3/src/test/jme3test/post/TestTransparentSSAO.java</a> – SSAOFilter, also known as Screen-Space Ambient Occlusion shadows (SSOA), plus transparancy</div>
</li>
<li class="level1"><div class="li"> More details: <a href="/jme3/advanced/light_and_shadow.html" class="wikilink1" title="jme3:advanced:light_and_shadow">Light and Shadow</a></div>
</li>
</ul>

</div>
<!-- EDIT15 SECTION "Shadow" [5736-6917] -->
<h2 class="sectionedit16" id="specialglass_metal_dissolve_toon">Special: Glass, Metal, Dissolve, Toon</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-toon-dino.png" class="media" title="jme3:advanced:toon-dino.png"><img src="/resources/jme3-advanced-toon-dino.png" class="mediaright" alt="" width="150" height="100" /></a>
</p>

</div>
<!-- EDIT16 SECTION "Special: Glass, Metal, Dissolve, Toon" [6918-7010] -->
<h3 class="sectionedit17" id="toon_effect">Toon Effect</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestCartoonEdge.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestCartoonEdge.java" rel="nofollow">jme3/src/test/jme3test/post/TestCartoonEdge.java</a> – CartoonEdgeFilter</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestTransparentCartoonEdge.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestTransparentCartoonEdge.java" rel="nofollow">jme3/src/test/jme3test/post/TestTransparentCartoonEdge.java</a> – CartoonEdgeFilter</div>
</li>
</ul>

</div>
<!-- EDIT17 SECTION "Toon Effect" [7011-7431] -->
<h3 class="sectionedit18" id="fade_in_fade_out">Fade in / Fade out</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/fade.html" class="wikilink1" title="jme3:advanced:fade">Fade</a> – FadeFilter</div>
</li>
</ul>

</div>
<!-- EDIT18 SECTION "Fade in / Fade out" [7432-7503] -->
<h3 class="sectionedit19" id="user_contributed">User Contributed</h3>
<div class="level3">

<p>
<a href="/resources/jme3-advanced-shaderblow_light1.jpg" class="media" title="jme3:advanced:shaderblow_light1.jpg"><img src="/resources/jme3-advanced-shaderblow_light1.jpg" class="mediaright" title="shaderblow_light1.jpg" alt="shaderblow_light1.jpg" width="78" height="150" /></a><a href="/resources/jme3-advanced-shaderblow_glass.jpg" class="media" title="jme3:advanced:shaderblow_glass.jpg"><img src="/resources/jme3-advanced-shaderblow_glass.jpg" class="mediaright" title="shaderblow_glass.jpg" alt="shaderblow_glass.jpg" width="80" height="150" /></a><a href="/resources/jme3-advanced-shaderblow_matcap.jpg" class="media" title="jme3:advanced:shaderblow_matcap.jpg"><img src="/resources/jme3-advanced-shaderblow_matcap.jpg" class="mediaright" title="shaderblow_matcap.jpg" alt="shaderblow_matcap.jpg" width="150" height="150" /></a><a href="/resources/jme3-advanced-shaderblow_light2.jpg" class="media" title="jme3:advanced:shaderblow_light2.jpg"><img src="/resources/jme3-advanced-shaderblow_light2.jpg" class="mediaright" title="shaderblow_light2.jpg" alt="shaderblow_light2.jpg" width="66" height="150" /></a>
</p>

<p>
<a href="/sdk/plugin/shaderblow.html" class="wikilink1" title="sdk:plugin:shaderblow">ShaderBlow - GLSL Shader Library</a>
</p>
<ul>
<li class="level1"><div class="li"> LightBlow Shader – blend material texture maps</div>
</li>
<li class="level1"><div class="li"> FakeParticleBlow Shader – jet, fire effect</div>
</li>
<li class="level1"><div class="li"> ToonBlow Shader – Toon Shading, toon edges </div>
</li>
<li class="level1"><div class="li"> Dissolve Shader – Scifi teleportation/dissolve effect</div>
</li>
<li class="level1"><div class="li"> MatCap Shader – Gold, metals, glass, toons…!</div>
</li>
<li class="level1"><div class="li"> Glass Shader – Glass</div>
</li>
<li class="level1"><div class="li"> Force Shield Shader – Scifi impact-on-force-field effect</div>
</li>
<li class="level1"><div class="li"> SimpleSprite Shader – Animated textures</div>
</li>
<li class="level1"><div class="li"> SimpleSpriteParticle Shader – Sprite library</div>
</li>
<li class="level1"><div class="li"> MovingTexture Shader – Animated cloud/mist texture</div>
</li>
<li class="level1"><div class="li"> SoftParticles Shader – Fire, clouds, smoke etc</div>
</li>
<li class="level1"><div class="li"> Displace Shader – Deformation effect: Ripple, wave, pulse, swell!</div>
</li>
</ul>

<p>
Thanks for your awesome contributions! Keep them coming!
</p>

</div>
<!-- EDIT19 SECTION "User Contributed" [7504-8465] -->
<h2 class="sectionedit20" id="particle_emittersexplosions_fire_smoke">Particle Emitters: Explosions, Fire, Smoke</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-explosion-5.png" class="media" title="jme3:advanced:explosion-5.png"><img src="/resources/jme3-advanced-explosion-5.png" class="mediaright" alt="" width="150" height="100" /></a><a href="/resources/jme3-advanced-particle.png" class="media" title="jme3:advanced:particle.png"><img src="/resources/jme3-advanced-particle.png" class="mediaright" alt="" width="150" height="100" /></a>
<a href="/jme3/advanced/particle_emitters.html" class="wikilink1" title="jme3:advanced:particle_emitters">Particle emitter effects</a> are highly configurable and can have any texture. They can simulate smoke, dust, leaves, meteors, snowflakes, mosquitos, fire, explosions, clusters, embers, sparks…
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/effect/TestExplosionEffect.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/effect/TestExplosionEffect.java" rel="nofollow">jme3/src/test/jme3test/effect/TestExplosionEffect.java</a> – debris, flame, flash, shockwave, smoke, sparks</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/effect/TestPointSprite.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/effect/TestPointSprite.java" rel="nofollow">jme3/src/test/jme3test/effect/TestPointSprite.java</a> – cluster of points </div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/effect/TestMovingParticle.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/effect/TestMovingParticle.java" rel="nofollow">jme3/src/test/jme3test/effect/TestMovingParticle.java</a> – dust, smoke</div>
</li>
</ul>
<hr />

</div>
<!-- EDIT20 SECTION "Particle Emitters: Explosions, Fire, Smoke" [8466-9440] -->
<h3 class="sectionedit21" id="creating_your_own_filters">Creating your own Filters</h3>
<div class="level3">

<p>
Here is an extract taken from @nehon in the forum thread (<a href="http://hub.jmonkeyengine.org/forum/topic/how-exactly-do-filters-work/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/how-exactly-do-filters-work/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/how-exactly-do-filters-work/</a>)
</p>

<p>
The methods are called in this order (pretty much the same flow as processors):
- initFilter() is called once when the FilterPostPorcessor is initialized or when the filter is added to the processor and this one as already been initialized.
</p>

<p>
for each frame the methods are called in that sequence :
- preFrame() occurs before anything happens
- postQueue() occcurs once the queues have been populated (there is one queue per bucket and 2 additional queues for the shadows, casters and recievers). Note that geometries in the queues are the one in the view frustum.
- postFrame occurs once the main frame has been rendered (the back buffer)
</p>

<p>
Those methods are optional in a filter, they are only there if you want to hook in the rendering process.
</p>

<p>
The material variable is here for convenience. You have a getMaterial method that returns the material that’s gonna be used to render the full screen quad. It just happened that in every implementation I had a material attribute in all my sub-classes, so I just put it back in the abstract class. Most of the time getMaterial returns this attribute.
</p>

<p>
Forced-technique can be any technique really, they are more related with the material system than to the filters but anyway. When you use a forced technique the renderer tries to select it on the material of each geometry, if the technique does not exists for the material the geometry is not rendered.
You assume well about the SSAO filer, the normal of the scene are rendered to a texture in a pre pass.
</p>

<p>
Passes : these are filters in filters in a way. First they are a convenient way to initialize a FrameBuffer and the associated textures it needs, then you can use them for what ever you want.
For example, a Pass can be (as in the SSAO filter) an extra render of the scene with a forced technique, and you have to handle the render yourself in the postQueue method.
It can be a post pass to do after the main filter has been rendered to screen (for example an additional blur pass used in SSAO again). You have a list of passes called postRenderPass in the Filter abstract class. If you add a pass to this list, it’ll be automatically rendered by the FilterPostProcessor during the filter chain.
</p>

<p>
The bloom Filter does an intensive use of passes.
</p>

<p>
Filters in a nutshell.
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/particle_emitters.html" class="wikilink1" title="jme3:advanced:particle_emitters">Particle Emitters</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/bloom_and_glow.html" class="wikilink1" title="jme3:advanced:bloom_and_glow">Bloom and Glow</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.smashingmagazine.com/2008/08/07/50-photoshop-tutorials-for-sky-and-space-effects/" class="urlextern" title="http://www.smashingmagazine.com/2008/08/07/50-photoshop-tutorials-for-sky-and-space-effects/" rel="nofollow">Photoshop Tutorial for Sky and space effects (article)</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/effect.html" class="wikilink1" title="tag:effect" rel="tag">effect</a>,
	<a href="/tag/light.html" class="wikilink1" title="tag:light" rel="tag">light</a>,
	<a href="/tag/water.html" class="wikilink1" title="tag:water" rel="tag">water</a>
</span></div>

</div>
<!-- EDIT21 SECTION "Creating your own Filters" [9441-] -->
