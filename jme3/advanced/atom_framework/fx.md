---
title: FX
---
<h2 class="sectionedit1" id="fx">FX</h2>
<div class="level2">

<p>
Stand for Effects.
</p>

<p>
Also stand for dynamic value functions f(x). 
</p>

<p>
Inspired by 
</p>

<p>
<a href="http://nodebox.net/node/" class="urlextern" title="http://nodebox.net/node/" rel="nofollow">http://nodebox.net/node/</a>
</p>

<p>
<a href="http://udk.com" class="urlextern" title="http://udk.com" rel="nofollow">http://udk.com</a>
</p>

</div>
<!-- EDIT1 SECTION "FX" [1-137] -->
<h3 class="sectionedit2" id="what_s_about_the_f_x">What's about the f(x) ?</h3>
<div class="level3">

<p>
For various effects the game may require. Need customable, extensible way to declare input-process-ouput:
</p>
<ol>
<li class="level1"><div class="li"> dynamic generic Data, which can be procedure by various sources, signals, services</div>
</li>
<li class="level1"><div class="li"> dynamic generic declaration of operations</div>
</li>
<li class="level1"><div class="li"> dynamic generic declaration of output order</div>
</li>
</ol>

<p>
Last but not least, it should be resuable, generative and composable.
</p>

</div>

<h4 id="in_java">In Java?</h4>
<div class="level4">

<p>
About the implementation, such as language should be under considered!
</p>

<p>
These all requirements fit to an DSL, functional and lazy like groovy scenario, but what about java - a traditional grown as imperative language? It's like we going to implement all its core language elements for god-sake… Umh, not like that. With the help of Guava, we do it properly acceptable and scalable! But read it carefully first or mislead later!!!
</p>

<p>
<a href="http://code.google.com/p/guava-libraries/wiki/FunctionalExplained" class="urlextern" title="http://code.google.com/p/guava-libraries/wiki/FunctionalExplained" rel="nofollow">http://code.google.com/p/guava-libraries/wiki/FunctionalExplained</a>
</p><p></p><div class="noteimportant">This framework's feature goes in two branches: in Java 1.5+ with Guava and in Groovy2+ , the difference will be distinguish later!
</div>


</div>

<h4 id="focus_in_effects">Focus in effects</h4>
<div class="level4">

<p>
</p><p></p><div class="noteimportant">The abstract concept and even implementation of the Fx framework make it look similar or even exactly like Codegen - the Atom's code generation framework. Because they both lend them selfs from same underlying concepts. But remember Fx is for effects and not focus in the code side. It was born to help people like artist to survive their career without reading more programmin books!!
</div>


<p>
Of course we not going to do a whole language enhancement here but use a functional ultilities to get start up quick and go straight to the “real-time effects” part later. But remember the base concepts of it, which really to be extend and custom for your own needs. 
</p>

<p>
Now Let's see how does it work?
</p>

</div>
<!-- EDIT2 SECTION "What's about the f(x) ?" [138-1937] -->
<h3 class="sectionedit3" id="interface_abstract">Interface &amp; Abstract</h3>
<div class="level3">

<p>
We need dynamic Data, which can be procedure through various sources, signals, services… let call the abstract which provide the data IValueProvider:
</p>

<p>
interface IValueProvider &lt;x,y&gt;{
y   value(x) return new y
}
</p>

<p>
Function &lt;x,y&gt; is the default implementation
</p>

<p>
Function &lt;x,y&gt;{
}
</p>

</div>
<!-- EDIT3 SECTION "Interface & Abstract" [1938-2247] -->
<h3 class="sectionedit4" id="input">Input</h3>
<div class="level3">

<p>
So what can be the input?
</p>

<p>
Single&lt;Value&gt; or any primitive
</p>

<p>
List&lt;Value&gt; . String
</p>

<p>
more
</p>

</div>
<!-- EDIT4 SECTION "Input" [2248-2350] -->
<h3 class="sectionedit5" id="time_factor_real_time_application">Time factor &amp; Real time application</h3>
<div class="level3">

<p>
An important factor of a real time system is … time, indeed. Imagine a physic world functioning with f(t) is the primitive law. Our effects system also. Almost every effects envolve time and almost modify or procedure several positions values. It's a very common case in this scenario.
</p>

<p>
In fact almost of the F(x) features are actually f(t) which t is the time provided by the system via update cycle. 
</p>

<p>
Now consider this very simple physic xample :
</p>

<p>
S = V.t 
</p>

<p>
pos = startPos + S 
</p>

<p>
→ pos = startPos + V.t
</p>

<p>
We have:
</p>
<ol>
<li class="level1"><div class="li"> startPos is a Vector3f (can be localTranslation of a jme3's Spatial!). </div>
</li>
<li class="level1"><div class="li"> a parameter vector V, basicly stand for the Speed</div>
</li>
<li class="level1"><div class="li"> t is time provided by system</div>
</li>
<li class="level1"><div class="li"> plus and multiply is numberical operations</div>
</li>
</ol>

<p>
→ We can compute the new pos which we can use as a slide of a ball!
</p>

<p>
In this simplest example, we should reads a mathematic equations as a “procedural process” in our fx system with time as an essential key. Which later will help us build up extraordary complex effect!
</p>

</div>

<h4 id="animations_concepts">Animations concepts</h4>
<div class="level4">

<p>
Here we will revised some animation concept. Kinematic and functionals.
</p>

</div>

<h5 id="timeline">Timeline</h5>
<div class="level5">

</div>

<h5 id="keyframe">Keyframe</h5>
<div class="level5">

</div>

<h5 id="sequence">Sequence</h5>
<div class="level5">

</div>

<h5 id="track">Track</h5>
<div class="level5">

</div>
<!-- EDIT5 SECTION "Time factor & Real time application" [2351-3551] -->
<h3 class="sectionedit6" id="operations">Operations</h3>
<div class="level3">

</div>

<h4 id="single_operation">Single operation</h4>
<div class="level4">

</div>

<h5 id="math">Math</h5>
<div class="level5">

</div>

<h5 id="add_remove">Add remove</h5>
<div class="level5">

</div>

<h4 id="list_operation">List operation</h4>
<div class="level4">

</div>

<h5 id="add_remove1">Add remove</h5>
<div class="level5">

</div>

<h5 id="transfrom">Transfrom</h5>
<div class="level5">

</div>

<h5 id="indexing">Indexing</h5>
<div class="level5">

</div>

<h4 id="d_geometric_operation">3D Geometric operation</h4>
<div class="level4">

</div>

<h5 id="curve__interpolator">Curve . Interpolator</h5>
<div class="level5">

<p>
IValueProvider
</p>

</div>

<h5 id="layout">Layout</h5>
<div class="level5">

</div>

<h5 id="shape_and_formation">Shape and formation</h5>
<div class="level5">

</div>

<h5 id="steering">Steering</h5>
<div class="level5">

</div>
<!-- EDIT6 SECTION "Operations" [3552-3822] -->
<h2 class="sectionedit7" id="effects">Effects</h2>
<div class="level2">

<p>
</p><p></p><div class="noteclassic">Ideas from Adobe After effect ,3DSMax, Cinema4D, Processing, Blender…!
</div>


</div>
<!-- EDIT7 SECTION "Effects" [3823-3928] -->
<h3 class="sectionedit8" id="text_effects">Text Effects</h3>
<div class="level3">

<p>
One of the most under rated part in almost every 3d game engine I come across is the *Text effect*. We *DO* need Text effect but it didn't have any native support. I've started by doing a lot of After effect's text effects and plugin, then trying in 3DSMax, Cinema4D, later in Processing… but I can not find one that make me feel easy to use and powerful. From some ideas borrow from those applications, I try to implement some in this framework.
</p>

</div>
<!-- EDIT8 SECTION "Text Effects" [3929-4401] -->
<h3 class="sectionedit9" id="particle_effects">Particle Effects</h3>
<div class="level3">

</div>
<!-- EDIT9 SECTION "Particle Effects" [4402-4428] -->
<h3 class="sectionedit10" id="cinematic_effects">Cinematic Effects</h3>
<div class="level3">

</div>
<!-- EDIT10 SECTION "Cinematic Effects" [4429-4456] -->
<h3 class="sectionedit11" id="color_texture_effects">Color &amp; Texture Effects</h3>
<div class="level3">

</div>
<!-- EDIT11 SECTION "Color & Texture Effects" [4457-4490] -->
<h3 class="sectionedit12" id="mesh_spatials_effects">Mesh &amp; Spatials Effects</h3>
<div class="level3">

</div>
<!-- EDIT12 SECTION "Mesh & Spatials Effects" [4491-4524] -->
<h3 class="sectionedit13" id="animation_effects">Animation Effects</h3>
<div class="level3">

</div>
<!-- EDIT13 SECTION "Animation Effects" [4525-4552] -->
<h3 class="sectionedit14" id="scripted_effects">Scripted Effects</h3>
<div class="level3">

</div>
<!-- EDIT14 SECTION "Scripted Effects" [4553-] -->
