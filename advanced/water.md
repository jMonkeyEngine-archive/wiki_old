---
title: Simple Water
---
<h1 class="sectionedit1" id="simple_water">Simple Water</h1>
<div class="level1">

<p>
jMonkeyEngine offers a SimpleWaterProcessor that turns any quad (flat rectangle) into a reflective water surface with waves. You can use this quad for simple limited water surfaces such as water troughs, shallow fountains, puddles, shallow water in channels. The SimpleWaterProcessor has less performance impact on your game than the full featured <a href="/jme3/advanced/post-processor_water.html" class="wikilink1" title="jme3:advanced:post-processor_water">SeaMonkey WaterFilter</a>; the main difference is that the SimpleWaterProcessor does not include under-water effects. 
</p>

<p>
Here is some background info for JME3's basic water implementation:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://www.jmonkeyengine.com/forum/index.php?topic=14740.0" class="urlextern" title="http://www.jmonkeyengine.com/forum/index.php?topic=14740.0" rel="nofollow">http://www.jmonkeyengine.com/forum/index.php?topic=14740.0</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.bonzaisoftware.com/water_tut.html" class="urlextern" title="http://www.bonzaisoftware.com/water_tut.html" rel="nofollow">http://www.bonzaisoftware.com/water_tut.html</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.gametutorials.com/Articles/RealisticWater.pdf" class="urlextern" title="http://www.gametutorials.com/Articles/RealisticWater.pdf" rel="nofollow">http://www.gametutorials.com/Articles/RealisticWater.pdf</a></div>
</li>
</ul>

<p>
<a href="/resources/fetch.php" class="media" title="http://www.jmonkeyengine.com/wp-content/uploads/2010/10/simplewaterdemo.jpg"><img src="/resources/fetch.php" class="mediacenter" title="www.jmonkeyengine.com_wp-content_uploads_2010_10_simplewaterdemo.jpg" alt="www.jmonkeyengine.com_wp-content_uploads_2010_10_simplewaterdemo.jpg" width="277" height="180" /></a>
</p>

</div>
<!-- EDIT1 SECTION "Simple Water" [1-865] -->
<h2 class="sectionedit2" id="simplewaterprocessor">SimpleWaterProcessor</h2>
<div class="level2">

<p>
A JME3 scene with water can use a <code>com.jme3.water.SimpleWaterProcessor</code> (which implements the SceneProcessor interface).
</p>

<p>
To achieve a water effect, JME3 uses shaders and a special material, <code>Common/MatDefs/Water/SimpleWater.j3md</code>. The water surface is a quad, and we use normal map and dU/dV map texturing to simulate the waves. 
</p>
<ol>
<li class="level1"><div class="li"> Every frame, we render to three texture maps:</div>
<ul>
<li class="level2"><div class="li"> For the water surface (reflection), we take a snapshot of the environment, flip it upside down, and clip it to the visible water surface. Note that we do not actually use a “water texture” color map: The “texture” of the water is solely a distorted reflection.</div>
</li>
<li class="level2"><div class="li"> For the “wavy” distortion (refraction), we use the derivative of a normal map, a dU/dV map.</div>
</li>
<li class="level2"><div class="li"> For the fogginess of water (depth) we use a depth map from the terrains z-buffer.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In the shaders, we add all of the texture maps together. </div>
<ul>
<li class="level2"><div class="li"> For the “bumpy” displacement of the waves, we use a normal map and a du/dv map that are shifted against each other over time to create the wave effect.</div>
</li>
<li class="level2"><div class="li"> For the light reflection vectors on the water surface, we use the Fresnel formula, together with normal vectors.</div>
</li>
<li class="level2"><div class="li"> We add specular lighting.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> (For the underwater caustics effect, we use splatted textures. – WIP/TODO)</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "SimpleWaterProcessor" [866-2190] -->
<h2 class="sectionedit3" id="usage">Usage</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-simplewater.png" class="media" title="jme3:advanced:simplewater.png"><img src="/resources/jme3-advanced-simplewater.png" class="mediaright" alt="" width="384" height="288" /></a>
</p>
<ol>
<li class="level1"><div class="li"> Create a <code>mainScene</code> Node</div>
<ol>
<li class="level2"><div class="li"> Attach the <code>mainScene</code> Node to the <code>rootNode</code></div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Load your <code>scene</code> Spatial</div>
<ol>
<li class="level2"><div class="li"> Add a light source to the <code>scene</code> Spatial</div>
</li>
<li class="level2"><div class="li"> Attach the <code>scene</code> Spatial to the <code>mainScene</code> Node</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Load your <a href="/jme3/advanced/sky.html" class="wikilink1" title="jme3:advanced:sky">sky</a> Geometry</div>
<ol>
<li class="level2"><div class="li"> Attach the sky Geometry to the <code>mainScene</code> Node</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Create the SimpleWaterProcessor <code>waterProcessor</code></div>
<ol>
<li class="level2"><div class="li"> Set the processor's ReflectionScene to the <code>mainScene</code> Spatial (!)</div>
</li>
<li class="level2"><div class="li"> Set the processor's Plane to where you want your water surface to be</div>
</li>
<li class="level2"><div class="li"> Set the processor's WaterDepth, DistortionScale, and WaveSpeed</div>
</li>
<li class="level2"><div class="li"> Attach the processor to the <code>viewPort</code></div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Create a Quad <code>quad</code></div>
<ol>
<li class="level2"><div class="li"> Set the quad's TextureCoordinates to specify the size of the waves</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Create a <code>water</code> Geometry from the Quad</div>
<ol>
<li class="level2"><div class="li"> Set the water's translation and rotation (same Y value as Plane above!)</div>
</li>
<li class="level2"><div class="li"> Set the water's material to the processor's output material</div>
</li>
<li class="level2"><div class="li"> Attach the <code>water</code> Geometry to the <code>rootNode</code>. (Not to the mainScene!)</div>
</li>
</ol>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Usage" [2191-3265] -->
<h2 class="sectionedit4" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
The sample code can be found in <code>jme3/src/jme3test/water/TestSimpleWater.java</code> and <code>jme3/src/jme3test/water/TestSceneWater.java</code>.
</p>

<p>
Here is the most important part of the code:
</p>
<pre class="code java"><span class="co1">// we create a water processor</span>
SimpleWaterProcessor waterProcessor <span class="sy0">=</span> <span class="kw1">new</span> SimpleWaterProcessor<span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span>
waterProcessor.<span class="me1">setReflectionScene</span><span class="br0">(</span>mainScene<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// we set the water plane</span>
Vector3f waterLocation<span class="sy0">=</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="sy0">-</span><span class="nu0">6</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
waterProcessor.<span class="me1">setPlane</span><span class="br0">(</span><span class="kw1">new</span> Plane<span class="br0">(</span>Vector3f.<span class="me1">UNIT_Y</span>, waterLocation.<span class="me1">dot</span><span class="br0">(</span>Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>waterProcessor<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// we set wave properties</span>
waterProcessor.<span class="me1">setWaterDepth</span><span class="br0">(</span><span class="nu0">40</span><span class="br0">)</span><span class="sy0">;</span>         <span class="co1">// transparency of water</span>
waterProcessor.<span class="me1">setDistortionScale</span><span class="br0">(</span>0.05f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// strength of waves</span>
waterProcessor.<span class="me1">setWaveSpeed</span><span class="br0">(</span>0.05f<span class="br0">)</span><span class="sy0">;</span>       <span class="co1">// speed of waves</span>
 
<span class="co1">// we define the wave size by setting the size of the texture coordinates</span>
Quad quad <span class="sy0">=</span> <span class="kw1">new</span> Quad<span class="br0">(</span><span class="nu0">400</span>,<span class="nu0">400</span><span class="br0">)</span><span class="sy0">;</span>
quad.<span class="me1">scaleTextureCoordinates</span><span class="br0">(</span><span class="kw1">new</span> Vector2f<span class="br0">(</span>6f,6f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// we create the water geometry from the quad</span>
Geometry water<span class="sy0">=</span><span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"water"</span>, quad<span class="br0">)</span><span class="sy0">;</span>
water.<span class="me1">setLocalRotation</span><span class="br0">(</span><span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span><span class="sy0">-</span>FastMath.<span class="me1">HALF_PI</span>, Vector3f.<span class="me1">UNIT_X</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
water.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="sy0">-</span><span class="nu0">200</span>, <span class="sy0">-</span><span class="nu0">6</span>, <span class="nu0">250</span><span class="br0">)</span><span class="sy0">;</span>
water.<span class="me1">setShadowMode</span><span class="br0">(</span>ShadowMode.<span class="me1">Receive</span><span class="br0">)</span><span class="sy0">;</span>
water.<span class="me1">setMaterial</span><span class="br0">(</span>waterProcessor.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>water<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Sample Code" [3266-4565] -->
<h2 class="sectionedit5" id="settings">Settings</h2>
<div class="level2">

<p>
You can lower the render size to gain higher performance:
</p>
<pre class="code java">waterProcessor.<span class="me1">setRenderSize</span><span class="br0">(</span><span class="nu0">128</span>,<span class="nu0">128</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The deeper the water, the more transparent. (?) 
</p>
<pre class="code java">waterProcessor.<span class="me1">setWaterDepth</span><span class="br0">(</span><span class="nu0">40</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
A higher distortion scale makes bigger waves.
</p>
<pre class="code java">waterProcessor.<span class="me1">setDistortionScale</span><span class="br0">(</span>0.05f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
A lower wave speed makes calmer water.
</p>
<pre class="code java">waterProcessor.<span class="me1">setWaveSpeed</span><span class="br0">(</span>0.05f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
If your scene does not have a lightsource, you can set the light direction for the water:
</p>
<pre class="code java">waterProcessor.<span class="me1">setLightDirection</span><span class="br0">(</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>0.55f, <span class="sy0">-</span>0.82f, 0.15f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Instead of creating a quad and specifying a plane, you can get a default waterplane from the processor:
</p>
<pre class="code java">Geometry waterPlane <span class="sy0">=</span> waterProcessor.<span class="me1">createWaterGeometry</span><span class="br0">(</span><span class="nu0">10</span>, <span class="nu0">10</span><span class="br0">)</span><span class="sy0">;</span>
waterPlane.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="sy0">-</span><span class="nu0">5</span>, <span class="nu0">0</span>, <span class="nu0">5</span><span class="br0">)</span><span class="sy0">;</span>
waterPlane.<span class="me1">setMaterial</span><span class="br0">(</span>waterProcessor.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can offer a switch to set the water Material to a static texture – for users with slow PCs.
</p>

</div>
<!-- EDIT5 SECTION "Settings" [4566-] -->
