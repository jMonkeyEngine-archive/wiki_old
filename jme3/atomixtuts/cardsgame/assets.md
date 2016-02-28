---
title: The Card:
---
<h3 class="sectionedit1" id="the_card">The Card:</h3>
<div class="level3">

<p>
</p><p></p><div class="notetip">In my example,for the Front textures of the cards, I use the orignal Yugioh Card game, but you can make your own if you want!! (prevent copy right issues)
</div>


</div>

<h4 id="the_card_model">The Card Model:</h4>
<div class="level4">

<p>
The card model made of a Box with side faces deleted. The two remain faces has some change in UV, instead of the have exactly the same UV, they share the 50-50% vertical areas. Why? Cause in the shader we will modify the way to calculate UV and use two different diffuse for front face and back face. :p This is very cool thing to learn!
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://farm9.staticflickr.com/8104/8617106224_e0c494dbf6_z.jpg"><img src="/resources/fetch.php" class="media" title="farm9.staticflickr.com_8104_8617106224_e0c494dbf6_z.jpg" alt="farm9.staticflickr.com_8104_8617106224_e0c494dbf6_z.jpg" /></a>
</p>

</div>

<h4 id="the_card_material">The Card material:</h4>
<div class="level4">

<p>
After import from Blender, the importer made a default Lighting material for the model. So basicly we want to change that to our approriate material. 
</p>

<p>
We make it by creating 3 new files: <strong>CardMat.j3md</strong> , <strong>CardMat.j3m</strong>, <strong>SimpleCard.frag</strong> ; and go to the Libraries section, where the TestData package is, copy the 4th file: <strong>ColoredTexture.vert</strong>.
</p>
<pre class="code">  That’s basic how the Material system in JME works. 4 things combine:
  - **CardMat.j3md** is the Material definition (MatDef).
  - **CardMat.j3m** an instance with parameter s like textures, colors..etc
  - **SimpleCard.frag** : the fragment shader which choose by the MatDef
  - **ColoredTexture.vert**: The vertex shader which choose by the MatDef</pre>

<p>
Below show the detail content of the Material file in JMP and explain why for newbie in GLSL:
<a href="/resources/fetch.php" class="media" title="http://farm9.staticflickr.com/8521/8616051519_7c8c32ee1a_c.jpg"><img src="/resources/fetch.php" class="mediacenter" title="farm9.staticflickr.com_8521_8616051519_7c8c32ee1a_c.jpg" alt="farm9.staticflickr.com_8521_8616051519_7c8c32ee1a_c.jpg" /></a>
</p>

</div>

<h4 id="cardmatj3md">CardMat.j3md</h4>
<div class="level4">
<pre class="code glsl">MaterialDef Card <span class="br0">{</span>
 
    MaterialParameters <span class="br0">{</span>
        Texture2D ColorMap
        Texture2D ColorMap2
        Color Color <span class="br0">(</span>Color<span class="br0">)</span>
        Boolean MixGlow
    <span class="br0">}</span>
 
    Technique <span class="br0">{</span>
        VertexShader GLSL100<span class="sy0">:</span>   MatDefs<span class="sy0">/</span>ColoredTextured<span class="sy0">.</span><span class="me1">vert</span>
        FragmentShader GLSL100<span class="sy0">:</span> MatDefs<span class="sy0">/</span>SimpleCard<span class="sy0">.</span><span class="me1">frag</span>
 
        WorldParameters <span class="br0">{</span>
            WorldViewProjectionMatrix
            Time
        <span class="br0">}</span>
 
        Defines <span class="br0">{</span>
            GLOW <span class="sy0">:</span> MixGlow
        <span class="br0">}</span>
    <span class="br0">}</span>
 
<span class="br0">}</span></pre>

</div>

<h4 id="simplecardfrag">SimpleCard.frag</h4>
<div class="level4">
<pre class="code glsl"><span class="kw2">varying</span> <span class="kw3">vec2</span> texCoord<span class="sy0">;</span>
 
<span class="kw2">uniform</span> <span class="kw3">sampler2D</span> m_ColorMap<span class="sy0">;</span>
<span class="kw2">uniform</span> <span class="kw3">sampler2D</span> m_ColorMap2<span class="sy0">;</span>
<span class="kw2">uniform</span> <span class="kw3">vec4</span> m_Color<span class="sy0">;</span>
<span class="kw2">uniform</span> <span class="kw3">bool</span> m_MixGlow<span class="sy0">;</span>
 
<span class="kw2">uniform</span> <span class="kw3">float</span> g_Time<span class="sy0">;</span>
 
<span class="kw3">void</span> main<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw3">vec2</span> uv <span class="sy0">=</span> texCoord<span class="sy0">;</span>
    <span class="kw3">vec4</span> texColor<span class="sy0">;</span>
    <span class="kw3">vec4</span> color<span class="sy0">;</span>
 
    <span class="kw1">if</span> <span class="br0">(</span>uv<span class="sy0">.</span><span class="me1">x</span> <span class="sy0">&gt;</span> <span class="nu0">0.5</span><span class="br0">)</span><span class="br0">{</span>
        uv<span class="sy0">.</span><span class="me1">x</span> <span class="sy0">=</span> <span class="br0">(</span>uv<span class="sy0">.</span><span class="me1">x</span> – <span class="nu0">0.5</span><span class="br0">)</span> <span class="sy0">*</span><span class="nu0">2</span><span class="sy0">;</span>
        texColor <span class="sy0">=</span> <span class="kw5">texture2D</span><span class="br0">(</span>m_ColorMap<span class="sy0">,</span> uv<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        uv<span class="sy0">.</span><span class="me1">x</span> <span class="sy0">=</span> uv<span class="sy0">.</span><span class="me1">x</span> <span class="sy0">*</span><span class="nu0">2</span><span class="sy0">;</span>
        texColor <span class="sy0">=</span> <span class="kw5">texture2D</span><span class="br0">(</span>m_ColorMap2<span class="sy0">,</span> uv<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw3">vec2</span> uvc <span class="sy0">=</span> uv<span class="sy0">;</span>
    uvc<span class="sy0">.</span><span class="me1">x</span> <span class="sy0">=</span> uv<span class="sy0">.</span><span class="me1">x</span> – <span class="nu0">0.5</span><span class="sy0">;</span>
    uvc<span class="sy0">.</span><span class="me1">y</span> <span class="sy0">=</span> uv<span class="sy0">.</span><span class="me1">y</span> – <span class="nu0">0.5</span><span class="sy0">;</span>
    <span class="kw3">vec2</span> borderSize <span class="sy0">=</span> <span class="kw3">vec2</span><span class="br0">(</span><span class="nu0">0.05</span><span class="sy0">,</span><span class="nu0">0.05</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co2">#ifdef GLOW</span>
        <span class="kw1">if</span> <span class="br0">(</span>m_MixGlow <span class="sy0">==</span> <span class="kw4">true</span><span class="br0">)</span><span class="br0">{</span>
                <span class="kw3">float</span> glowV<span class="sy0">=</span><span class="kw5">sqrt</span><span class="br0">(</span><span class="br0">(</span>uvc<span class="sy0">.</span><span class="me1">x</span><span class="br0">)</span><span class="sy0">*</span><span class="br0">(</span>uvc<span class="sy0">.</span><span class="me1">x</span><span class="br0">)</span><span class="sy0">+</span><span class="br0">(</span>uvc<span class="sy0">.</span><span class="me1">y</span><span class="br0">)</span><span class="sy0">*</span><span class="br0">(</span>uvc<span class="sy0">.</span><span class="me1">y</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="kw3">vec4</span> glowC <span class="sy0">=</span> <span class="kw5">mix</span><span class="br0">(</span><span class="kw3">vec4</span><span class="br0">(</span><span class="nu0">0.9</span><span class="sy0">,</span><span class="nu0">0.8</span><span class="sy0">,</span><span class="nu0">0.1</span><span class="sy0">,</span><span class="nu0">1</span><span class="br0">)</span><span class="sy0">,</span><span class="kw3">vec4</span><span class="br0">(</span><span class="nu0">0.4</span><span class="sy0">,</span><span class="nu0">0.7</span><span class="sy0">,</span><span class="nu0">1</span><span class="sy0">,</span><span class="nu0">1</span><span class="br0">)</span><span class="sy0">,</span><span class="kw5">sin</span><span class="br0">(</span>g_Time<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                color <span class="sy0">=</span> <span class="kw5">mix</span><span class="br0">(</span>texColor<span class="sy0">,</span>glowC<span class="sy0">,</span>glowV<span class="br0">)</span><span class="sy0">;</span>
 
                <span class="kw1">if</span> <span class="br0">(</span><span class="br0">(</span>uv<span class="sy0">.</span><span class="me1">x</span> <span class="sy0">&lt;</span>borderSize<span class="sy0">.</span><span class="me1">x</span> <span class="sy0">||</span> <span class="nu0">1</span><span class="sy0">-</span>uv<span class="sy0">.</span><span class="me1">x</span><span class="sy0">&lt;</span>borderSize<span class="sy0">.</span><span class="me1">x</span><span class="br0">)</span><span class="sy0">||</span><span class="br0">(</span>uv<span class="sy0">.</span><span class="me1">y</span> <span class="sy0">&lt;</span>borderSize<span class="sy0">.</span><span class="me1">y</span> <span class="sy0">||</span> <span class="nu0">1</span><span class="sy0">-</span>uv<span class="sy0">.</span><span class="me1">y</span><span class="sy0">&lt;</span>borderSize<span class="sy0">.</span><span class="me1">y</span><span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
                    color<span class="sy0">+=</span> <span class="kw3">vec4</span><span class="br0">(</span><span class="nu0">0.8</span><span class="sy0">,</span><span class="nu0">0.8</span><span class="sy0">,</span><span class="nu0">0.1</span><span class="sy0">,</span><span class="nu0">0.5</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
            color <span class="sy0">=</span> texColor<span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="co2">#else</span>
        color <span class="sy0">=</span> texColor<span class="sy0">;</span>
    <span class="co2">#endif</span>
 
    <span class="kw6">gl_FragColor</span> <span class="sy0">=</span> color<span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
This GLSL code can be obviously explain like this:
</p>
<ul>
<li class="level1"><div class="li"> uv is the coordinate for the diffuse map. In our model, we modified the UV, so if the “x”-horizontal value of vertex coordinates is bigger than 0.5, than mean it in the back( that’s the trick I said), use the ColorMap2 texture.</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> uv2 is the coordinate to put the highlight for the border of the card, the value of highlight controller by the value of “sin(time)” … that means it goes up and down like a wave.</div>
</li>
</ul>

<p>
That’s it! No big deal!
</p>

</div>

<h5 id="note">Note:</h5>
<div class="level5">

<p>
texCoord is a Varying – mean it transfered from Vertex shader
Time is global Attribute – mean it sent to openGL from JME renderer
ColorMap – ColorMap2 are Uniform (s) – mean they are parameters from the user set to the Shader
</p>

</div>
<!-- EDIT1 SECTION "The Card:" [1-3907] -->
<h3 class="sectionedit2" id="the_table">The Table:</h3>
<div class="level3">

<p>
The table of this card game is a design from the orginal game. It divide into two main area:
The ground and sides
The ground divided by two for each opponents
The side divided to some areas, including: Deck block, Magic block, Fusion block…ect
</p>

</div>

<h4 id="table_texture">Table Texture:</h4>
<div class="level4">

<p>
The table represent by a single quad with this texture. I did it in PTS but you can also do the same thing in Gimp or even paint.net (which one you prefered). The source PTS file is in the Project assets if you want to look into.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://farm9.staticflickr.com/8251/8617035018_bf7db17d09_z.jpg"><img src="/resources/fetch.php" class="mediacenter" title="farm9.staticflickr.com_8251_8617035018_bf7db17d09_z.jpg" alt="farm9.staticflickr.com_8251_8617035018_bf7db17d09_z.jpg" /></a>
</p>

</div>
<!-- EDIT2 SECTION "The Table:" [3908-] -->
