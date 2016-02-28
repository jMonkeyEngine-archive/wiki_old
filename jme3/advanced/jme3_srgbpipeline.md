---
title: Gamma Correction or sRGB pipline
---
<h1 class="sectionedit1" id="gamma_correction_or_srgb_pipline">Gamma Correction or sRGB pipline</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Gamma Correction or sRGB pipline" [1-48] -->
<h2 class="sectionedit2" id="overview">Overview</h2>
<div class="level2">

<p>
Here is a quick overview of what lies under the “Gamma Correction” term. <br />

More in depth rundowns on the matter can be found here : <a href="http://http.developer.nvidia.com/GPUGems3/gpugems3_ch24.html" class="urlextern" title="http://http.developer.nvidia.com/GPUGems3/gpugems3_ch24.html" rel="nofollow">http://http.developer.nvidia.com/GPUGems3/gpugems3_ch24.html</a> and here <a href="http://www.arcsynthesis.org/gltut/Texturing/Tutorial%2016.html" class="urlextern" title="http://www.arcsynthesis.org/gltut/Texturing/Tutorial%2016.html" rel="nofollow">http://www.arcsynthesis.org/gltut/Texturing/Tutorial%2016.html</a>
</p>

<p>
We consider color values to be linear when computing lighting. What does that means? That means that we assume that the color 0.5,0.5,0.5 is half way between black and white.<br />

The problem is that it’s not the case, or at least not when you look at the color through a monitor.<br />

CRT monitors had physical limitations that prevented them to have a linear way of representing colors. that means that 0.5,0.5,0.5 through a monitor is not half way between black and white (it’s darker). Note that black and white remains the same though.<br />

<br />

If we do not take that into account, the rendered images are overly darken and feels dull.<br />

<br />

LCD monitors still mimic this physical limitation (I guess for backward compatibility).<br />

<br />

<strong>Output correct colors</strong><br />

Gamma Correction is the technique that tends to correct the issue. Gamma is an power factor applied to the color by the monitor when lighting a pixel on screen (or at least a simplification of the function applied). So when we output the color, we have to apply the inverse power of this factor to nullify the effect : finalColor = pow(computedColor, 1/gamma);<br />

</p>

<p>
<strong>Knowing what colors we have as input</strong><br />

The other aspect of gamma correction is the colors we get as input in the rendering process that are stored in textures or in ColorRGBA material params. Almost all image editors are storing color data in images already gamma corrected (so that colors are correct when you display the picture in a viewer of in a browser). Also most hand picked colors (in a color picker) can be assumed as gamma corrected as you most probably chose this color through a monitor display.
Such images or color are said to be in sRGB color space, meaning “standard RGB” (which is not the standard one would guess).
That means that textures and colors that we use as input in our shaders are not in a linear space. The issue is that we need them in linear space when we compute the lighting, else the lighting is wrong.
To avoid this we need to apply some gamma correction to the colors : (pow(color, gamma);
This only apply to textures that will render colors on screen (basically diffuse map, specular, light maps). Normal maps, height maps don’t need the correction.
</p>

<p>
this is the kind of difference you can have :<br />

left is non corrected output, right is gamma corrected output.<br />

<a href="/resources/fetch.php" class="media" title="http://i.imgur.com/uNL7vw8.png"><img src="/resources/fetch.php" class="media" alt="" /></a>
<br />

</p>

</div>
<!-- EDIT2 SECTION "Overview" [49-2711] -->
<h3 class="sectionedit3" id="implementation">Implementation</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> To handle proper gamma corrected ouput colors, Opengl expose an ARB extension that allows you to output a color in linear space and have the GPU automatically correct it : <a href="https://www.opengl.org/registry/specs/ARB/framebuffer_sRGB.txt" class="urlextern" title="https://www.opengl.org/registry/specs/ARB/framebuffer_sRGB.txt" rel="nofollow">https://www.opengl.org/registry/specs/ARB/framebuffer_sRGB.txt</a></div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> To handle the input, instead of classic RGBA8 image format, one can use SRGB8_ALPHA8_EXT which is basically RGBA in sRGB. Using this you specify the GPU that the texture is in sRGB space and when fetching  a color from it, the GPU will linearize the color value for you (for free). There are sRGB equivalent to all 8 bits formats (even compressed format like DXT).<br />
</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> But all textures don't need this. For example, normal maps, height maps colors are most probably generated and not hand picked by an artist looking through a monitor. The implementation needs to account for it and expose a way to exclude some textures from the sRGB pipeline.</div>
</li>
</ul>

<p>
Gamma Correction in jME 3.0 is based on those three statements.
</p><p></p><div class="noteimportant">Note that Gamma Correction is only available on desktop with LWJGL or JOGL renderer. They are not yet supported on Android or iOS renderers
</div>


</div>

<h4 id="turning_gamma_correction_on_off">Turning Gamma Correction on/off</h4>
<div class="level4">

<p>
You can turn Gamma Correction on and off using the AppSettings. There is a method setGammaCorrection(boolean) that changes the setting.
use this in the main() method of your application : 
</p>
<pre class="code java">AppSettings settings <span class="sy0">=</span> <span class="kw1">new</span> AppSettings<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
settings.<span class="me1">setGammaCorrection</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
app.<span class="me1">setSettings</span><span class="br0">(</span>settings<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This setting is also exposed in the Settings dialog displayed when you launch a jME application.<br />

<a href="/resources/fetch.php" class="media" title="http://i.imgur.com/Lya1ldH.png"><img src="/resources/fetch.php" class="media" alt="" width="400" /></a>
</p>

<p>
</p><p></p><div class="noteimportant">This is a short hand to enable both linearization of input textures and Gamma correction of the rendered output on screen.<strong> But both can be enabled separately</strong>.

</div>


</div>

<h5 id="enabling_output_gamma_correction">Enabling output Gamma Correction</h5>
<div class="level5">

<p>
You can enable or disable the Gamma correction of the rendered output by using 
</p>
<pre class="code java">renderer.<span class="me1">setMainFrameBufferSrgb</span><span class="br0">(</span><span class="kw4">boolean</span> srgb<span class="br0">)</span></pre>

<p>
This will be ignored if the hardware doesn't have the GL_ARB_framebuffer_sRGB or the GL_EXT_texture_sRGB.
This can be toggled at run time.
</p>

<p>
This uses Opengl hardware gamma correction that uses an approximated Gamma value of 2.2 and uses the following formula : color = pow(color,1/gamma)<br />

Not that this will not yield exact results, as the real gamma can vary depending on the monitor. <br />

If this is a problem, please refer to the “handling gamma correction in a post process” section.
</p>

</div>

<h5 id="enabling_texture_linearization">Enabling texture linearization</h5>
<div class="level5">

<p>
You can enable or disable texture linearization by using
</p>
<pre class="code java">renderer.<span class="me1">setLinearizeSrgbImages</span><span class="br0">(</span><span class="kw4">boolean</span> linearize<span class="br0">)</span></pre>

<p>
This will be ignored if the hardware doesn't have the GL_ARB_framebuffer_sRGB or the GL_EXT_texture_sRGB.
</p><p></p><div class="noteimportant">Toggling this setting at runtime will produce unexpected behavior for now. A change in this setting would need a proper reload of the context to work.
</div>


<p>
All images marked as in sRGB color space will be uploaded to the GPU using a sRGB image format.
Opengl hardware texture linearization also uses an approximated Gamma value of 2.2 and linearize the fetched texel color using the following formula : color = pow(color, gamma)<br />

As with output gamma correction this will not give exact result, but the error is less important since most image editor uses the same approximation to correct images and save them in sRGB color space.
</p>

<p>
Not all image format have their sRGB equivalent, and only 8bit formats.
Here is an exhaustive list of the supported format and there equivalent :
</p>
<ul>
<li class="level1"><div class="li"> RGB8 : GL_SRGB8           </div>
</li>
<li class="level1"><div class="li"> RGBA8 : GL_SRGB8_ALPHA8</div>
</li>
<li class="level1"><div class="li"> BGR8 : GL_SRGB8  </div>
</li>
<li class="level1"><div class="li"> ABGR8 : GL_SRGB8_ALPHA8</div>
</li>
<li class="level1"><div class="li"> Luminance8 : GL_SLUMINANCE8</div>
</li>
<li class="level1"><div class="li"> Luminance8Alpha8 : GL_SLUMINANCE8_ALPHA8</div>
</li>
<li class="level1"><div class="li"> DXT1 : GL_COMPRESSED_SRGB_S3TC_DXT1</div>
</li>
<li class="level1"><div class="li"> DXT1A : GL_COMPRESSED_SRGB_ALPHA_S3TC_DXT1</div>
</li>
<li class="level1"><div class="li"> DXT3 : GL_COMPRESSED_SRGB_ALPHA_S3TC_DXT3</div>
</li>
<li class="level1"><div class="li"> DXT5 : GL_COMPRESSED_SRGB_ALPHA_S3TC_DXT5  </div>
</li>
</ul>

<p>
</p><p></p><div class="noteimportant">Conventionally only the rgb channels are gamma corrected, as the alpha channel does not a represent a color value
</div>


</div>

<h4 id="excluding_images_from_the_srgb_pipeline">Excluding images from the sRGB pipeline</h4>
<div class="level4">

<p>
</p><p></p><div class="noteimportant">Only loaded images will be marked as in sRGB color space, when using assetManager.loadTexture or loadAsset.<br />

The color space of an image created by code will have to be specified in the constructor or will be assumed as Linear if not specified. 
</div>


<p>
Not all images need to be linearized. Some images don't represent color information that will be displayed on screen, but more different sort of data packed in a texture.<br />

The best example is a Normal map that will contains normal vectors for each pixel. Height maps will contain elevation values. These textures must not be linearized.
</p>

<p>
There is no way to determine the real color space of an image when loading it, so we must deduce the color space from the usage it's loaded for.
The usage is dictated by the material, those textures are used for, and by the material parameter they are assigned to.
One can now specify in a material definition file (j3md) if a texture parameter must be assumed as in linear color space, and thus, must not be linearized, by using the keyword -LINEAR next to the parameter (case does not matter).
</p>

<p>
For example here is how the NormalMap parameter is declared in the lighting material definition.
</p>
<pre class="code"> // Normal map
 Texture2D NormalMap -LINEAR</pre>

<p>
When a texture is assigned to this material param by using material.setTexture(“NormalMap”, myNormalTexture), the color space of this texture's image will be forced to linear. 
So if you make your own material and want to use Gamma Correction, make sure you properly mark your textures as in the proper color space.
</p>

<p>
This can sound complicated, but you just have to answer this question :  Does my image represent color data? if the answer is no, then you have to set the -Linear flag.
</p>

</div>

<h4 id="colorrgba_as_srgb">ColorRGBA as sRGB</h4>
<div class="level4">

<p>
</p><p></p><div class="noteimportant">The r, g, b attributes of a ColorRGBA object are <strong>ALWAYS</strong> assumed in Linear color space.

</div>


<p>
If you want to set a color that you hand picked in a color picker, you should use the setAsSRGB method of ColorRGBA. This will convert the given values to linear color space by using the same formula as before : color = pow (color, gamma) where gamma = 2.2;
</p>

<p>
If you want to retrieve those values from a ColorRGBA, you can call the getAsSRGB method. The values will be converted back to sRGB color Space.<br />

Note that the return type of that method is a Vector4f and not a ColorRGBA, because as stated before, all ColorRGBA objects r,g,b attributes are assumed in Linear color space.
</p>

</div>

<h4 id="handling_rendered_output_gamma_correction_with_a_post_process_filter">Handling rendered output Gamma Correction with a post process filter</h4>
<div class="level4">

<p>
As stated before, the hardware gamma correction uses and approximated gamma value of 2.2.
Some may not be satisfied with that approximations and may want to pick a more appropriate gamma value.
You can see in some games some Gamma calibration screens, that are here to help the player pick a correct gamma value for the monitor he's using.
</p>

<p>
For this particular case, you can do as follow :
</p>
<ol>
<li class="level1"><div class="li"> Enable Gamma Correction global app setting.</div>
</li>
<li class="level1"><div class="li"> Disable rendered output correction : renderer.setMainFrameBufferSrgb(false); (for example in the simpleInit method of your SimpleApplication).</div>
</li>
<li class="level1"><div class="li"> Use the GammaCorrectionFilter in a FilterPostProcessor, and set the proper gamma value on it (default is 2.2).</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Implementation" [2712-10098] -->
<h3 class="sectionedit4" id="should_you_use_this">Should you use this?</h3>
<div class="level3">

<p>
Yes. Mostly because it's the only way to have proper lighting.
If you're starting a new project it's a no brainer…use it, period. And don't allow the player to turn it off.
</p>

<p>
Now if you already spent time to adjust lighting in your scenes, without gamma correction, turning it on will make everything too bright, and you'll have to adjust all your lighting and colors again.
That's why we kept a way to turn it off, for backward compatibility.
</p>

</div>
<!-- EDIT4 SECTION "Should you use this?" [10099-] -->
