---
title: Read Graphic Card Capabilites
---
<h1 class="sectionedit1" id="read_graphic_card_capabilites">Read Graphic Card Capabilites</h1>
<div class="level1">

<p>
When different people test your new game, you may get feedback that the game doesn't run on their hardware, or that some details don't look as expected. You need to detect which fetaures the user's hardware supports, and offer a replacement for non-supported features on olde hardware (or deactivate them automatically).
</p>

<p>
You can read (and print) the capabilities of the user's graphic card using the <code>com.jme3.renderer.Caps</code> class:
</p>
<pre class="code java">Collection<span class="sy0">&lt;</span>Caps<span class="sy0">&gt;</span> caps <span class="sy0">=</span> renderer.<span class="me1">getCaps</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
Logger.<span class="me1">getLogger</span><span class="br0">(</span>HelloWorld.<span class="kw1">class</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">log</span><span class="br0">(</span>Level.<span class="me1">INFO</span>, “Caps<span class="sy0">:</span> <span class="br0">{</span><span class="nu0">0</span><span class="br0">}</span>”, caps.<span class="me1">toString</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Note:</strong> Replace <code>HelloWorld</code> by the name of the class where you are using this line.
</p>

</div>
<!-- EDIT1 SECTION "Read Graphic Card Capabilites" [1-731] -->
<h2 class="sectionedit2" id="examples">Examples</h2>
<div class="level2">

<p>
A newer graphic card has modern capabilities, for example OpenGL 2.1 and NonPowerOfTwoTextures: 
</p>
<pre class="code">INFO: Running on jMonkeyEngine 3.0.0 
INFO: Using LWJGL 2.8.2
INFO: Selected display mode: 1280 x 720 x 0 @0Hz
INFO: Adapter: null
INFO: Driver Version: null
INFO: Vendor: ATI Technologies Inc.
INFO: OpenGL Version: 2.1 ATI-7.14.5
INFO: Renderer: AMD Radeon HD 6770M OpenGL Engine
INFO: GLSL Ver: 1.20
INFO: Timer resolution: 1.000 ticks per second
INFO: Capabilities: [FrameBuffer, FrameBufferMRT, FrameBufferMultisample, 
OpenGL20, OpenGL21, ARBprogram, GLSL100, GLSL110, GLSL120, 
VertexTextureFetch, TextureArray, FloatTexture, 
FloatColorBuffer, FloatDepthBuffer, PackedFloatTexture, SharedExponentTexture, PackedFloatColorBuffer, 
TextureCompressionLATC, NonPowerOfTwoTextures, MeshInstancing]</pre>

<p>
Here is an example of the capabilities of an semi-old graphic card that only supports OpenGL 2.0. If you use OpenGL 2.1 features you need to decide whether to branch to a low-quality replacement of the unsupported features (if you still want to support this card); or whether the game will not start at all and displays an error message explaining the user what capabilities his hardware is missing to be able to play the game.
</p>
<pre class="code">INFO: Running on jMonkey Engine 3 
INFO: Using LWJGL 2.7.1
INFO: Selected display mode: 1024 x 768 x 0 @0Hz
INFO: Adapter: null
INFO: Driver Version: null
INFO: Vendor: ATI Technologies Inc.
INFO: OpenGL Version: 2.0 ATI-1.6.36
INFO: Renderer: ATI Radeon X1600 OpenGL Engine
INFO: GLSL Ver: 1.20
INFO: Timer resolution: 1.000 ticks per second
INFO: Capabilities: [FrameBuffer, FrameBufferMRT, FrameBufferMultisample,
OpenGL20, ARBprogram, GLSL100, GLSL110, GLSL120, 
VertexTextureFetch, FloatTexture, 
TextureCompressionLATC, NonPowerOfTwoTextures]</pre>

<p>
This next example is lacking <code>NonPowerOfTwoTextures</code>, this tells you that this user's graphic card cannot handle textures with sizes that are not square powers of two (such as “128×128”).
</p>
<pre class="code">INFO: Capabilities: [FrameBuffer, FrameBufferMRT, FrameBufferMultisample, 
OpenGL20, ARBprogram, GLSL100, GLSL110, GLSL120, 
VertexTextureFetch, FloatTexture, TextureCompressionLATC]</pre>

</div>
<!-- EDIT2 SECTION "Examples" [732-] -->
