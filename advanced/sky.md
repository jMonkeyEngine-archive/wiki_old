---
title: How to add a Sky to your Scene
---
<h1 class="sectionedit1" id="how_to_add_a_sky_to_your_scene">How to add a Sky to your Scene</h1>
<div class="level1">

<p>
<br />

</p>

<p>
Here is an example for how you add a static horizon (a background landscape and a sky) to a scene.
Having a discernable horizon with a suitable landscape (or space, or ocean, or whatever) in the background makes scenes look more realistic than just a single-colored “sky” background.
</p>

</div>
<!-- EDIT1 SECTION "How to add a Sky to your Scene" [1-335] -->
<h2 class="sectionedit2" id="adding_the_sky">Adding the Sky</h2>
<div class="level2">

<p>
Adding a sky is extremely easy using the <code>com.jme3.util.SkyFactory</code>.
</p>
<pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>SkyFactory.<span class="me1">createSky</span><span class="br0">(</span>
            assetManager, <span class="st0">"Textures/Sky/Bright/BrightSky.dds"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To add a sky you need to supply:
</p>
<ol>
<li class="level1"><div class="li"> The assetManager object to use</div>
</li>
<li class="level1"><div class="li"> A cube or sphere map texture of the sky</div>
</li>
<li class="level1"><div class="li"> Set the boolean to true if you are using a sphere map texture. For a cube map, use false. <br />
Tip: Cube map is the default. You would know if you had created a sphere map.</div>
</li>
</ol>

<p>
Internally, the SkyFactory calls the following methods:
</p>
<ol>
<li class="level1"><div class="li"> <code>sky.setQueueBucket(Bucket.Sky);</code> makes certain the sky is rendered in the right order, behind everything else.</div>
</li>
<li class="level1"><div class="li"> <code>sky.setCullHint(Spatial.CullHint.Never);</code> makes certain that the sky is never culled.</div>
</li>
<li class="level1"><div class="li"> The SkyFactory uses the internal jME3 material definition <code>Sky.j3md</code>. This Material definition works with sphere and cube maps. </div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Adding the Sky" [336-1262] -->
<h2 class="sectionedit3" id="creating_the_textures">Creating the Textures</h2>
<div class="level2">

<p>
As the sky texture we use the sample BrightSky.dds file from jme3test-test-data. 
</p>

<p>
How to create a sky textures?
</p>
<ul>
<li class="level1"><div class="li"> There are many tools out there that generate cube and sphere maps. <br />
Examples for landscape texture generators are Terragen or Bryce.</div>
</li>
<li class="level1"><div class="li"> The actual texture size does not matter, as long as you add the Sky Geometry to the Sky bucket: Everything in the sky bucket will always be infinitely far away behind everything else, and never intersect with your scene. <br />
Of course the higher the resolution, the better it will look. On the other hand, if the graphic is too big, it will slow the game down. </div>
</li>
<li class="level1"><div class="li"> A box or sphere map is the simplest solution. But you can use any Node as sky, even complex sets of geometries and quads with animated clouds, blinking stars, city skylines, etc.</div>
</li>
<li class="level1"><div class="li"> JME3 supports cube maps in PNG, JPG, or (compressed) DDS format.</div>
</li>
</ul>

<p>
Box or Sphere?
</p>
<ul>
<li class="level1"><div class="li"> If you have access to cube map textures, then use a SkyBox</div>
<ul>
<li class="level2"><div class="li"> <a href="http://1.bp.blogspot.com/_uVsWqMqIGQU/SN0IZEE117I/AAAAAAAAAPs/4lfHx1Erdqg/s1600/skybox" class="urlextern" title="http://1.bp.blogspot.com/_uVsWqMqIGQU/SN0IZEE117I/AAAAAAAAAPs/4lfHx1Erdqg/s1600/skybox" rel="nofollow">SkyBox examples</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> If you have access to sphere map textures – specially projected sky images that fit inside a sphere – then you use a SkySphere or SkyDome. </div>
<ul>
<li class="level2"><div class="li"> <a href="http://wiki.delphigl.com/index.php/Datei:Skysphere.jpg" class="urlextern" title="http://wiki.delphigl.com/index.php/Datei:Skysphere.jpg" rel="nofollow">SkySphere example</a></div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Creating the Textures" [1263-] -->
