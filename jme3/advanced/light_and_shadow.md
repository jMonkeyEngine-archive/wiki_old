---
title: Light and Shadow
---
<h1 class="sectionedit1" id="light_and_shadow">Light and Shadow</h1>
<div class="level1">

<p>
<a href="/resources/jme3-advanced-shading-ani.gif" class="media" title="jme3:advanced:shading-ani.gif"><img src="/resources/jme3-advanced-shading-ani.gif" class="media" title="Examples of shading and lighting." alt="Examples of shading and lighting." /></a>
</p>

<p>
Light and Shadow are two separate things in 3D engines, although we percieve them together in real life:
</p>
<ul>
<li class="level1"><div class="li"> Lighting means that an object is brighter on the side facing the light direction, and darker on the backside. Computationally, this is relatively easy. </div>
</li>
<li class="level1"><div class="li"> Lighting does not mean that objects cast a shadow on the floor or other objects: Activating shadow processing is an additional step described here. Since casting shadows has an impact on performance, drop shadows and ambient occlusion shading are not activated by default.</div>
</li>
</ul>

<p>
</p><p></p><div class="noteimportant">A light source with a direction or location is required for all Geometries with Lighting.j3md-based Materials. An ambient light is not sufficient. In a scene with no appropriate light sources, Geometries with Lighting.j3md-based Materials do not render. Only Geometries with Unshaded.j3md-based Materials are visible independent of any light sources.
</div>


</div>
<!-- EDIT1 SECTION "Light and Shadow" [1-1017] -->
<h2 class="sectionedit2" id="light_sources_and_colors">Light Sources and Colors</h2>
<div class="level2">

<p>
<a href="/resources/jme3-advanced-light-sources.png" class="media" title="jme3:advanced:light-sources.png"><img src="/resources/jme3-advanced-light-sources.png" class="mediaright" title="A lit scene with multiple light sources" alt="A lit scene with multiple light sources" width="300" height="200" /></a>
</p>

<p>
You can add several types of light sources to a scene using <code>rootNode.addLight(mylight)</code>. 
</p>

<p>
The available light sources in <code>com.​jme3.​light</code> are:
</p>
<ul>
<li class="level1"><div class="li"> SpotLight </div>
</li>
<li class="level1"><div class="li"> PointLight</div>
</li>
<li class="level1"><div class="li"> AmbientLight</div>
</li>
<li class="level1"><div class="li"> DirectionalLight</div>
</li>
</ul>

<p>
You control the color and intensity of each light source. Typically you set the color to white (<code>new ColorRGBA(1.0f,1.0f,1.0f,1.0f)</code> or <code>ColorRGBA.White</code>), which makes all scene elements appear in their natural color. 
</p>

<p>
You can choose to use lights in other colors than white, or darker colors. This influences the scene's atmosphere and will make the scene appear colder (e.g. <code>ColorRGBA.Cyan</code>) or warmer (<code>ColorRGBA.Yellow</code>), brighter (higher values) or darker (lower values).
</p>

<p>
You can get a list of all lights added to a Spatial by calling <code>getWorldLightList()</code> (includes inherited lights) or <code>getLocalLightList()</code> (only directly added lights), and iterating over the result.
</p>

</div>
<!-- EDIT2 SECTION "Light Sources and Colors" [1018-2059] -->
<h3 class="sectionedit3" id="pointlight">PointLight</h3>
<div class="level3">

<p>
<a href="/resources/jme3-advanced-elephant-pointlights.png" class="media" title="jme3:advanced:elephant-pointlights.png"><img src="/resources/jme3-advanced-elephant-pointlights.png" class="mediaright" title="An elephant model illuminated by pointlights" alt="An elephant model illuminated by pointlights" width="300" height="205" /></a>
</p>

<p>
A PointLight has a location and shines from there in all directions as far as its radius reaches. The light intensity decreases with increased distance from the light source. A PointLight can be used to cast shadows along with a PointLightShadowRenderer (see the Casting Shadows section)
</p>

<p>
<strong>Typical example:</strong> Lamp, lightbulb, torch, candle.
</p>
<pre class="code java">PointLight lamp_light <span class="sy0">=</span> <span class="kw1">new</span> PointLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
lamp_light.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">Yellow</span><span class="br0">)</span><span class="sy0">;</span>
lamp_light.<span class="me1">setRadius</span><span class="br0">(</span>4f<span class="br0">)</span><span class="sy0">;</span>
lamp_light.<span class="me1">setPosition</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>lamp_geo.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">addLight</span><span class="br0">(</span>lamp_light<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT3 SECTION "PointLight" [2060-2750] -->
<h3 class="sectionedit4" id="directionallight">DirectionalLight</h3>
<div class="level3">

<p>
<a href="/resources/jme3-advanced-house-directionallight.png" class="media" title="jme3:advanced:house-directionallight.png"><img src="/resources/jme3-advanced-house-directionallight.png" class="mediaright" title="A house model illuminated with a sun-like directional light" alt="A house model illuminated with a sun-like directional light" width="300" height="210" /></a>
</p>

<p>
A DirectionalLight has no position, only a direction. It sends out parallel beams of light and is considered “infinitely” far away. You typically have one directional light per scene. A DirectionalLight can be used together with shadows. 
</p>

<p>
<strong>Typically example:</strong> Sun light.
</p>
<pre class="code java">DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
sun.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>.5f,<span class="sy0">-</span>.5f,<span class="sy0">-</span>.5f<span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "DirectionalLight" [2751-3355] -->
<h3 class="sectionedit5" id="spotlight">SpotLight</h3>
<div class="level3">

<p>
<a href="/resources/jme3-advanced-spotlight.png" class="media" title="jme3:advanced:spotlight.png"><img src="/resources/jme3-advanced-spotlight.png" class="mediaright" title="Spotlight" alt="Spotlight" /></a>
</p>

<p>
A SpotLight sends out a distinct beam or cone of light. A SpotLight has a direction, a position, distance (range) and two angles. The inner angle is the central maximum of the light cone, the outer angle the edge of the light cone. Everything outside the light cone's angles is not affected by the light.
</p>

<p>
<strong>Typical Example:</strong> Flashlight
</p>
<pre class="code java">SpotLight spot <span class="sy0">=</span> <span class="kw1">new</span> SpotLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
spot.<span class="me1">setSpotRange</span><span class="br0">(</span>100f<span class="br0">)</span><span class="sy0">;</span>                           <span class="co1">// distance</span>
spot.<span class="me1">setSpotInnerAngle</span><span class="br0">(</span>15f <span class="sy0">*</span> FastMath.<span class="me1">DEG_TO_RAD</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// inner light cone (central beam)</span>
spot.<span class="me1">setSpotOuterAngle</span><span class="br0">(</span>35f <span class="sy0">*</span> FastMath.<span class="me1">DEG_TO_RAD</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// outer light cone (edge of the light)</span>
spot.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span>.<span class="me1">mult</span><span class="br0">(</span>1.3f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>         <span class="co1">// light color</span>
spot.<span class="me1">setPosition</span><span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>               <span class="co1">// shine from camera loc</span>
spot.<span class="me1">setDirection</span><span class="br0">(</span>cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>             <span class="co1">// shine forward from camera loc</span>
rootNode.<span class="me1">addLight</span><span class="br0">(</span>spot<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
If you want the spotlight to follow the flycam, repeat the setDirection(…) and setPosition(…) calls in the update loop, and kee syncing them with the camera position and direction.
</p>

</div>
<!-- EDIT5 SECTION "SpotLight" [3356-4490] -->
<h3 class="sectionedit6" id="ambientlight">AmbientLight</h3>
<div class="level3">

<p>
An AmbientLight simply influences the brightness and color of the scene globally. It has no direction and no location and shines equally everywhere. An AmbientLight does not cast any shadows, and it lights all sides of Geometries evenly, which makes 3D objects look unnaturally flat; this is why you typically do not use an AmbientLight alone without one of the other lights.  
</p>

<p>
<strong>Typical example:</strong> Regulate overall brightness, tinge the whole scene in a warm or cold color. 
</p>
<pre class="code java">AmbientLight al <span class="sy0">=</span> <span class="kw1">new</span> AmbientLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
al.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span>.<span class="me1">mult</span><span class="br0">(</span>1.3f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">addLight</span><span class="br0">(</span>al<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="notetip">You can increase the brightness of a light source gradually by multiplying the light color to values greater than 1.0f. <br />
Example: <code>mylight.setColor(ColorRGBA.White.mult(1.3f));</code>
</div>


</div>
<!-- EDIT6 SECTION "AmbientLight" [4491-5313] -->
<h2 class="sectionedit7" id="light_follows_spatial">Light Follows Spatial</h2>
<div class="level2">

<p>
You can use a <code>com.jme3.scene.control.LightControl</code> to make a SpotLight or PointLight follow a Spatial. This can be used for a flashlight being carried by a character, or for car headlights, or an aircraft's spotlight, etc.
</p>
<pre class="code java">PointLight myLight <span class="sy0">=</span> <span class="kw1">new</span> PointLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">addLight</span><span class="br0">(</span>myLight<span class="br0">)</span><span class="sy0">;</span>
LightControl lightControl <span class="sy0">=</span> <span class="kw1">new</span> LightControl<span class="br0">(</span>myLight<span class="br0">)</span><span class="sy0">;</span>
spatial.<span class="me1">addControl</span><span class="br0">(</span>lightControl<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// this spatial controls the position of this light.</span></pre>

<p>
Obviously, this does not apply to AmbientLights, which have no position.
</p>

</div>
<!-- EDIT7 SECTION "Light Follows Spatial" [5314-5880] -->
<h2 class="sectionedit8" id="basicshadowrenderer_deprecated">BasicShadowRenderer (deprecated)</h2>
<div class="level2">

<p>
Full code sample
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestShadow.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestShadow.java" rel="nofollow">TestShadow.java</a></div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "BasicShadowRenderer (deprecated)" [5881-6073] -->
<h2 class="sectionedit9" id="casting_shadows">Casting Shadows</h2>
<div class="level2">

<p>
For each type of non-ambient light source, JME3 implements two ways to simulate geometries casting shadows on other geometries:
</p>
<ul>
<li class="level1"><div class="li"> a shadow renderer (which you apply to a viewport) and</div>
</li>
<li class="level1"><div class="li"> a shadow filter (which you can add to a viewport's filter post-processor).</div>
</li>
</ul>
<div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> light source class </th><th class="col1"> shadow renderer class </th><th class="col2"> shadow filter class </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> DirectionalLight </td><td class="col1"> DirectionalLightShadowRenderer </td><td class="col2"> DirectionalLightShadowFilter </td>
	</tr>
	<tr class="row2">
		<td class="col0"> PointLight </td><td class="col1"> PointLightShadowRenderer </td><td class="col2"> PointLightShadowFilter </td>
	</tr>
	<tr class="row3">
		<td class="col0"> SpotLight </td><td class="col1"> SpotLightShadowRenderer </td><td class="col2"> SpotLightShadowFilter </td>
	</tr>
	<tr class="row4">
		<td class="col0"> AmbientLight </td><td class="col1"> (not applicable) </td><td class="col2"> (not applicable) </td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [6369-6708] -->
<p>
You only need one shadow simulation per light source:  if you use shadow rendering, you won't need a shadow filter and vice versa.  Which way is more efficient depends partly on the complexity of your scene. All six shadow simulation classes have similar interfaces, so once you know how to use one, you can easily figure out the rest.
</p>

<p>
Shadow calculations (cast and receive) have a performance impact, so use them sparingly.  With shadow renderers, you can turn off shadow casting and/or shadow receiving for individual geometries, for portions of the scene graph, or for the entire scene:
</p>
<pre class="code java">spatial.<span class="me1">setShadowMode</span><span class="br0">(</span>ShadowMode.<span class="me1">Inherit</span><span class="br0">)</span><span class="sy0">;</span>     <span class="co1">// This is the default setting for new spatials.</span>
rootNode.<span class="me1">setShadowMode</span><span class="br0">(</span>ShadowMode.<span class="me1">Off</span><span class="br0">)</span><span class="sy0">;</span>        <span class="co1">// Disable shadows for the whole scene, except where overridden. </span>
wall.<span class="me1">setShadowMode</span><span class="br0">(</span>ShadowMode.<span class="me1">CastAndReceive</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// The wall can cast shadows and also receive them.</span>
floor.<span class="me1">setShadowMode</span><span class="br0">(</span>ShadowMode.<span class="me1">Receive</span><span class="br0">)</span><span class="sy0">;</span>       <span class="co1">// Any shadows cast by the floor would be hidden by it.</span>
airplane.<span class="me1">setShadowMode</span><span class="br0">(</span>ShadowMode.<span class="me1">Cast</span><span class="br0">)</span><span class="sy0">;</span>       <span class="co1">// There's nothing above the airplane to cast shadows on it.</span>
ghost.<span class="me1">setShadowMode</span><span class="br0">(</span>ShadowMode.<span class="me1">Off</span><span class="br0">)</span><span class="sy0">;</span>           <span class="co1">// The ghost is translucent: it neither casts nor receives shadows.</span></pre>

<p>
Both shadow renderers and shadow filters use shadow modes to determine which objects can cast shadows. However, only the shadow renderers pay attention to shadow modes when determining which objects receive shadows.  With a shadow filter, shadow modes have no effect on which objects receive shadows.
</p>

<p>
Here's a sample application which demonstrates both DirectionalLightShadowRenderer and DirectionalLightShadowFilter:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestDirectionalLightShadow.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestDirectionalLightShadow.java" rel="nofollow">TestDirectionalLightShadow.java</a></div>
</li>
</ul>

<p>
Here is the key code fragment:
</p>
<pre class="code java">        DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        sun.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
        sun.<span class="me1">setDirection</span><span class="br0">(</span>cam.<span class="me1">getDirection</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="coMULTI">/* Drop shadows */</span>
        <span class="kw1">final</span> <span class="kw4">int</span> SHADOWMAP_SIZE<span class="sy0">=</span><span class="nu0">1024</span><span class="sy0">;</span>
        DirectionalLightShadowRenderer dlsr <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLightShadowRenderer<span class="br0">(</span>assetManager, SHADOWMAP_SIZE, <span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span>
        dlsr.<span class="me1">setLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
        viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>dlsr<span class="br0">)</span><span class="sy0">;</span>
 
        DirectionalLightShadowFilter dlsf <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLightShadowFilter<span class="br0">(</span>assetManager, SHADOWMAP_SIZE, <span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span>
        dlsf.<span class="me1">setLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
        dlsf.<span class="me1">setEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        FilterPostProcessor fpp <span class="sy0">=</span> <span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span>
        fpp.<span class="me1">addFilter</span><span class="br0">(</span>dlsf<span class="br0">)</span><span class="sy0">;</span>
        viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>fpp<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Constructor arguments:
 * your AssetManager object
 * size of the rendered shadow maps, in pixels per side (512, 1024, 2048, etc…)
 * the number of shadow maps rendered (more shadow maps = better quality, but slower)
</p>

<p>
Properties you can set:
 * setDirection(Vector3f) – the direction of the light
 * setLambda(0.65f) – to reduce the split size
 * setShadowIntensity(0.7f) – shadow darkness (1=black, 0=invisible)
 * setShadowZextend(float) – distance from camera to which shadows will be computed
</p>

</div>
<!-- EDIT9 SECTION "Casting Shadows" [6074-9825] -->
<h2 class="sectionedit11" id="parallel-split_shadow_map_deprecated">Parallel-Split Shadow Map (deprecated)</h2>
<div class="level2">

<p>
Full sample code
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestPssmShadow.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/light/TestPssmShadow.java" rel="nofollow">TestPssmShadow.java</a></div>
</li>
</ul>

<p>
<a href="/resources/jme3-advanced-shadow.png" class="media" title="jme3:advanced:shadow.png"><img src="/resources/jme3-advanced-shadow.png" class="mediaright" title="A lit scene with PSSM drop shadows" alt="A lit scene with PSSM drop shadows" width="300" height="200" /></a>
</p>
<pre class="code java"><span class="kw1">private</span> PssmShadowRenderer pssmRenderer<span class="sy0">;</span>
...
<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ....
    <span class="me1">pssmRenderer</span> <span class="sy0">=</span> <span class="kw1">new</span> PssmShadowRenderer<span class="br0">(</span>assetManager, <span class="nu0">1024</span>, <span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span>
    pssmRenderer.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>.5f,<span class="sy0">-</span>.5f,<span class="sy0">-</span>.5f<span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// light direction</span>
    viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>pssmRenderer<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT11 SECTION "Parallel-Split Shadow Map (deprecated)" [9826-10415] -->
<h2 class="sectionedit12" id="screen_space_ambient_occlusion">Screen Space Ambient Occlusion</h2>
<div class="level2">

<p>
Full sample code
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestSSAO.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestSSAO.java" rel="nofollow">jme3/src/test/jme3test/post/TestSSAO.java</a> – Screen-Space Ambient Occlusion shadows</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestTransparentSSAO.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/post/TestTransparentSSAO.java" rel="nofollow">jme3/src/test/jme3test/post/TestTransparentSSAO.java</a> – Screen-Space Ambient Occlusion shadows plus transparancy</div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/2010/08/screen-space-ambient-occlusion-for-jmonkeyengine-3-0/" class="urlextern" title="http://hub.jmonkeyengine.org/2010/08/screen-space-ambient-occlusion-for-jmonkeyengine-3-0/" rel="nofollow">Screen Space Ambient Occlusion for jMonkeyEngine (article)</a></div>
</li>
</ul>

<p>
Ambient Occlusion refers to the shadows which nearby objects cast on each other under an ambient lighting. Screen Space Ambient Occlusion (SSAO) approximates how light radiates in real life.
</p>

<p>
In JME3, SSAO is implemented by adding an instance of <code>com.jme3.post.SSAOFilter</code> to a viewport which already simulates shadows using another method such as DirectionalLightShadowRenderer.
</p>
<pre class="code java">FilterPostProcessor fpp <span class="sy0">=</span> <span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span>
SSAOFilter ssaoFilter <span class="sy0">=</span> <span class="kw1">new</span> SSAOFilter<span class="br0">(</span>12.94f, 43.92f, 0.33f, 0.61f<span class="br0">)</span><span class="sy0">;</span>
fpp.<span class="me1">addFilter</span><span class="br0">(</span>ssaoFilter<span class="br0">)</span><span class="sy0">;</span>
viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>fpp<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<a href="/resources/jme3-advanced-shading-textured-ani.gif" class="media" title="jme3:advanced:shading-textured-ani.gif"><img src="/resources/jme3-advanced-shading-textured-ani.gif" class="media" title="Shading with and without Ambient Occlusion" alt="Shading with and without Ambient Occlusion" /></a>
</p>

</div>
<!-- EDIT12 SECTION "Screen Space Ambient Occlusion" [10416-] -->
