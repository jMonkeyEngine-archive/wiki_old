---
title: The grass system
---
<h1 class="sectionedit1" id="the_grass_system">The grass system</h1>
<div class="level1">

<p>
Here you will learn how to use the grass system. The test project available on the project page contains enough well-commented examples to get you going, but there are some more information available here.
</p>

</div>
<!-- EDIT1 SECTION "The grass system" [1-239] -->
<h2 class="sectionedit2" id="simplegrasstestjava">SimpleGrassTest.java</h2>
<div class="level2">

<p>
The demo project contains an example named SimpleGrassTest.java. That class has a method named setupForester().
It is well commented, and can be used as a primer on how to set up a simple grass system. The basic approach is this:
</p>

<p>
1) Create a Forester object, and initialize it.
</p>

<p>
2) Use it to create a grass-loader.
</p>

<p>
3) Use the grassloader to create a map-provider. The map-provider is used to feed the grass-loader with densitymaps.
</p>

<p>
4) Use the grassloader to create one grass-layer for each type of grass. Each type of grass has its own grasslayer object which contains the material settings, the actual grass texture, and lots of other settings. Each layer also has their own instance of the planting algorithm, so that each type of grass can be planted in it's own way.
</p>

<p>
5) Tweak everything until you're happy with the way it looks/runs.
</p>

<p>
6) Make sure you call forester.update() each frame.
</p>

</div>
<!-- EDIT2 SECTION "SimpleGrassTest.java" [240-1169] -->
<h2 class="sectionedit3" id="rendering_vegetation_basic">Rendering vegetation (Basic)</h2>
<div class="level2">

<p>
Here is some basic information and tips here on how to make a vegetation system more efficient and/or better looking. There are also links to more in-depth jME tutorials on each subject, where there are any.
</p>

</div>
<!-- EDIT3 SECTION "Rendering vegetation (Basic)" [1170-1420] -->
<h3 class="sectionedit4" id="alpha_textures">Alpha textures</h3>
<div class="level3">

<p>
Grass and foliage often use alpha textures. Alpha textures are partially (or fully) transparent. A standard alpha texture contains the RGB channels, but also an additional alpha channel where the transparency values are stored.
</p>

<p>
There is a tutorial on how to work with alpha textures and transparency here: <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_material" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_material" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_material</a>
</p>

</div>
<!-- EDIT4 SECTION "Alpha textures" [1421-1826] -->
<h3 class="sectionedit5" id="coloring_depth">Coloring &amp; Depth</h3>
<div class="level3">

<p>
Materials have something called additional renderstate options. They can be found in the material editor. When rendering grass, you usually want to look at these settings:
</p>

<p>
<strong>FaceCull:</strong> When using fixed quads it should be set to “Off”. This means both sides of the quads will be rendered. When using billboarded grass, you can cull the back side, because it never faces the camera.
</p>

<p>
<strong>Blending mode:</strong> With grass you'd normally be using <strong>Alpha</strong>. The <strong>AlphaTestFallof</strong> parameter should also be set, but the value to use depends a lot on the texture. It may be worth trying a few different values.
</p>

<p>
<strong>DepthWrite/DepthCheck:</strong> Both of those should normally be checked.
</p>

<p>
<strong>ColorWrite:</strong> This should always be on.
</p>

</div>
<!-- EDIT5 SECTION "Coloring & Depth" [1827-2569] -->
<h3 class="sectionedit6" id="alpha_to_coverage">Alpha to coverage</h3>
<div class="level3">

<p>
Alpha to coverage (AtoC) is a method used to smooth out the edges of grass and such. It is an alternative to regular alpha blending. In jME you enable it through the rendermanager, or renderer:
</p>
<pre class="code java">renderer.<span class="me1">setAlphaToCoverage</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
There's an example in the Forester test project that shows how you enable it, and how you use it in Forester.
</p>

<p>
Alpha to coverage works through multi-sampling, and you have to use 4xMSAA in order for it to work. It is a fairly new technique and may not be supported on older graphics-cards. It is also implemented differently by different vendors, and while some cards “technically support it”, it may not work as intended. This means it's always a good idea to provide an alternative to AtoC in your apps/games.
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Alpha_to_coverage" class="urlextern" title="http://en.wikipedia.org/wiki/Alpha_to_coverage" rel="nofollow">http://en.wikipedia.org/wiki/Alpha_to_coverage</a>
</p>

</div>
<!-- EDIT6 SECTION "Alpha to coverage" [2570-] -->
