---
title: Bloom and Glow
---
<h1 class="sectionedit1" id="bloom_and_glow">Bloom and Glow</h1>
<div class="level1">

<p>
Bloom is a popular shader effect in 3D games industry. It usually consist in displaying a glowing halo around light sources or bright areas of a scene.
In practice, the bright areas are extracted from the rendered scene, blurred and finally added up to the render.
</p>

<p>
Those images gives an idea of what bloom does. The left image has no bloom effect, the right image does. <br />

<a href="/resources/jme3-advanced-nobloomsky.png" class="media" title="jme3:advanced:nobloomsky.png"><img src="/resources/jme3-advanced-nobloomsky.png" class="media" title="No bloom" alt="No bloom" /></a><a href="/resources/jme3-advanced-blomsky.png" class="media" title="jme3:advanced:blomsky.png"><img src="/resources/jme3-advanced-blomsky.png" class="media" title="Bloom" alt="Bloom" /></a>
</p>

</div>
<!-- EDIT1 SECTION "Bloom and Glow" [1-484] -->
<h1 class="sectionedit2" id="bloom_usage">Bloom Usage</h1>
<div class="level1">
<ol>
<li class="level1"><div class="li"> Create a FilterPostProcessor</div>
</li>
<li class="level1"><div class="li"> Create a BloomFilter</div>
</li>
<li class="level1"><div class="li"> Add the filter to the processor</div>
</li>
<li class="level1"><div class="li"> Add the processor to the viewPort</div>
</li>
</ol>
<pre class="code java"> FilterPostProcessor fpp<span class="sy0">=</span><span class="kw1">new</span> FilterPostProcessor<span class="br0">(</span>assetManager<span class="br0">)</span><span class="sy0">;</span>
 BloomFilter bloom<span class="sy0">=</span><span class="kw1">new</span> BloomFilter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 fpp.<span class="me1">addFilter</span><span class="br0">(</span>bloom<span class="br0">)</span><span class="sy0">;</span>
 viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>fpp<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Here are the parameters that you can tweak :
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Parameter           </th><th class="col1 leftalign"> Method                </th><th class="col2"> Default </th><th class="col3"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> blur scale              </td><td class="col1"> <code>setBlurScale(float)</code> </td><td class="col2 leftalign">1.5f  </td><td class="col3"> the scale of the bloom effect, but be careful, high values does artifacts </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> exposure Power              </td><td class="col1"> <code>setExposurePower(float)</code> </td><td class="col2 leftalign">5.0f  </td><td class="col3"> the glowing channel color is raised to the value power </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> exposure cut-off              </td><td class="col1"> <code>setExposureCutOff(float)</code> </td><td class="col2 leftalign">0.0f  </td><td class="col3"> the threshold of color to bloom during extraction </td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> bloom intensity              </td><td class="col1"> <code>setBloomIntensity(float)</code> </td><td class="col2 leftalign">2.0f  </td><td class="col3"> the resulting bloom value is multiplied by this intensity </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [864-1454] -->
<p>
You'll probably need to adjust those parameters depending on your scene.
</p>

</div>
<!-- EDIT2 SECTION "Bloom Usage" [485-1529] -->
<h1 class="sectionedit4" id="bloom_with_a_glow_map">Bloom with a glow map</h1>
<div class="level1">

<p>
Sometimes, you want to have more control over what glows and does not glow. 
The bloom filter supports a glow map or a glow color.
</p>

</div>

<h5 id="creating_a_glow-map">Creating a glow-map</h5>
<div class="level5">

<p>
Let's take the hover tank example bundled with JME3 test data.<br />

Here you can see the diffuse map of the tank, and the associated glow map that only contains the parts of the texture that will glow and their glowing color: <br />

<a href="/resources/jme3-advanced-tank_diffuse_ss.png" class="media" title="jme3:advanced:tank_diffuse_ss.png"><img src="/resources/jme3-advanced-tank_diffuse_ss.png" class="media" title="Tank diffuse map" alt="Tank diffuse map" /></a>
<a href="/resources/jme3-advanced-tank_glow_map_ss.png" class="media" title="jme3:advanced:tank_glow_map_ss.png"><img src="/resources/jme3-advanced-tank_glow_map_ss.png" class="media" title="Tank glow map" alt="Tank glow map" /></a>
</p>

<p>
Glow maps work with Lighting.j3md, Particles.j3md and SolidColor.j3md material definitions.
The tank material looks like this : 
</p>
<pre class="code">Material My Material : Common/MatDefs/Light/Lighting.j3md {
     MaterialParameters {
        SpecularMap : Models/HoverTank/tank_specular.png
        Shininess : 8
        NormalMap : Models/HoverTank/tank_normals.png
        DiffuseMap : Models/HoverTank/tank_diffuse.png
        GlowMap : Models/HoverTank/tank_glow_map_highres.png
        UseMaterialColors : true
        Ambient  : 0.0 0.0 0.0 1.0
        Diffuse  : 1.0 1.0 1.0 1.0
        Specular : 1.0 1.0 1.0 1.0
     }
}</pre>

<p>
The glow map is defined here : <strong>GlowMap : Models/HoverTank/tank_glow_map_highres.png</strong>
</p>

</div>

<h5 id="usage">Usage</h5>
<div class="level5">
<ol>
<li class="level1"><div class="li"> Create a FilterPostProcessor</div>
</li>
<li class="level1"><div class="li"> Create a BloomFilter with the GlowMode.Objects parameter</div>
</li>
<li class="level1"><div class="li"> Add the filter to the processor</div>
</li>
<li class="level1"><div class="li"> Add the processor to the viewPort</div>
</li>
</ol>
<pre class="code">  FilterPostProcessor fpp=new FilterPostProcessor(assetManager);
  BloomFilter bf=new BloomFilter(BloomFilter.GlowMode.Objects);
  fpp.addFilter(bf);
  viewPort.addProcessor(fpp);</pre>

<p>
Here is the result : <br />

<a href="/resources/jme3-advanced-tanlglow1.png" class="media" title="jme3:advanced:tanlglow1.png"><img src="/resources/jme3-advanced-tanlglow1.png" class="media" title="Glowing hover tank" alt="Glowing hover tank" /></a>
</p>

</div>
<!-- EDIT4 SECTION "Bloom with a glow map" [1530-3231] -->
<h1 class="sectionedit5" id="bloom_with_a_glow_color">Bloom with a glow color</h1>
<div class="level1">

<p>
Sometimes you need an entire object to glow, not just parts of it.
In this case you'll need to use the glow color parameter.
</p>

</div>

<h5 id="usage1">Usage</h5>
<div class="level5">
<ol>
<li class="level1"><div class="li"> Create a material for your object and set the GlowColor parameter</div>
</li>
<li class="level1"><div class="li"> Create a FilterPostProcessor</div>
</li>
<li class="level1"><div class="li"> Create a BloomFilter with the GlowMode.Objects parameter</div>
</li>
<li class="level1"><div class="li"> Add the filter to the processor</div>
</li>
<li class="level1"><div class="li"> Add the processor to the viewPort</div>
</li>
</ol>
<pre class="code">    Material mat = new Material(getAssetManager(), "Common/MatDefs/Misc/SolidColor.j3md");
    mat.setColor("Color", ColorRGBA.Green);
    mat.setColor("GlowColor", ColorRGBA.Green);
    fpp=new FilterPostProcessor(assetManager);
    bloom= new BloomFilter(BloomFilter.GlowMode.Objects);        
    fpp.addFilter(bloom);
    viewPort.addProcessor(fpp);</pre>

<p>
Here is the result on Oto's plasma ball (before and after) : <br />

<a href="/resources/jme3-advanced-otonobloom.png" class="media" title="jme3:advanced:otonobloom.png"><img src="/resources/jme3-advanced-otonobloom.png" class="medialeft" title="Oto&apos;s plasma ball is just a big pea" alt="Oto&apos;s plasma ball is just a big pea" width="400" /></a>
<a href="/resources/jme3-advanced-otoglow.png" class="media" title="jme3:advanced:otoglow.png"><img src="/resources/jme3-advanced-otoglow.png" class="medialeft" title="Oto&apos;s plasma ball radiates incredible power!!!" alt="Oto&apos;s plasma ball radiates incredible power!!!" width="400" /></a>
</p>

</div>
<!-- EDIT5 SECTION "Bloom with a glow color" [3232-4239] -->
<h1 class="sectionedit6" id="hints_and_tricks">Hints and tricks</h1>
<div class="level1">

</div>

<h5 id="increasing_the_blur_range_and_reducing_fps_cost">Increasing the blur range and reducing fps cost</h5>
<div class="level5">

<p>
The glow render is sampled on a texture that has the same dimensions as the viewport.
You can reduce the size of the bloom sampling just by using the setDownSamplingFactor method like this : <br />

</p>
<pre class="code java"> BloomFilter bloom<span class="sy0">=</span><span class="kw1">new</span> BloomFilter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 bloom.<span class="me1">setDownSamplingFactor</span><span class="br0">(</span>2.0f<span class="br0">)</span><span class="sy0">;</span> </pre>

<p>
In this example the sampling size is divided by 4 (width/2,height/2), resulting in less work to blur the scene.
The resulting texture is then up sampled to the screen size using hardware bilinear filtering. this results in a wider blur range.
</p>

</div>

<h5 id="using_classic_bloom_combined_with_a_glow_map">Using classic bloom combined with a glow map</h5>
<div class="level5">

<p>
let's say you want a global bloom on your scene, but you have also a glowing object on it.
You can use only one bloom filter for both effects like that
</p>
<pre class="code java">BloomFilter bloom<span class="sy0">=</span><span class="kw1">new</span> BloomFilter<span class="br0">(</span>BloomFilter.<span class="me1">GlowMode</span>.<span class="me1">SceneAndObjects</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
However, note that both effects will share the same values of attribute, and sometimes, it won't be what you need.
</p>

</div>

<h5 id="making_your_home_brewed_material_definition_support_glow">Making your home brewed material definition support Glow</h5>
<div class="level5">

<p>
Let's say you have made a custom material on your own, and that you want it to support glow maps and glow color.
In your material definition you need to add those lines in the MaterialParameters section :
</p>
<pre class="code"> MaterialParameters {
        
        ....

        // Texture of the glowing parts of the material
        Texture2D GlowMap
        // The glow color of the object
        Color GlowColor
    }</pre>

<p>
Then add the following technique : 
</p>
<pre class="code">    Technique Glow {

        LightMode SinglePass

        VertexShader GLSL100:   Common/MatDefs/Misc/SimpleTextured.vert
        FragmentShader GLSL100: Common/MatDefs/Light/Glow.frag

        WorldParameters {
            WorldViewProjectionMatrix
        }

        Defines {
            HAS_GLOWMAP : GlowMap
            HAS_GLOWCOLOR : GlowColor
        }
    }</pre>

<p>
Then you can use this material with the BloomFilter
</p>

</div>

<h5 id="make_a_glowing_object_stop_to_glow">Make a glowing object stop to glow</h5>
<div class="level5">

<p>
If you are using a glow map, remove the texture from the material.
</p>
<pre class="code">material.clearTextureParam("GlowMap");</pre>

<p>
If you are using a glow color, set it to black
</p>
<pre class="code">material.setColor("GlowColor",ColorRGBA.Black);</pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/effect.html" class="wikilink1" title="tag:effect" rel="tag">effect</a>,
	<a href="/tag/light.html" class="wikilink1" title="tag:light" rel="tag">light</a>
</span></div>

</div>
<!-- EDIT6 SECTION "Hints and tricks" [4240-] -->
