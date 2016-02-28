---
title: jMonkeyEngine 3 Tutorial (12) - Hello Effects
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_12_-_hello_effects">jMonkeyEngine 3 Tutorial (12) - Hello Effects</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_audio.html" class="wikilink1" title="jme3:beginner:hello_audio">Hello Audio</a>,
Next: <a href="/jme3/beginner/hello_physics.html" class="wikilink1" title="jme3:beginner:hello_physics">Hello Physics</a>
</p>

<p>
<a href="/resources/jme3-beginner-beginner-effect-fire.png" class="media" title="jme3:beginner:beginner-effect-fire.png"><img src="/resources/jme3-beginner-beginner-effect-fire.png" class="mediaright" alt="" width="150" height="165" /></a>
</p>

<p>
When you see one of the following in a game, then a particle system is likely behind it:
</p>
<ul>
<li class="level1"><div class="li"> Fire, flames, sparks;</div>
</li>
<li class="level1"><div class="li"> Rain, snow, waterfalls, leaves;</div>
</li>
<li class="level1"><div class="li"> Explosions, debris, shockwaves;</div>
</li>
<li class="level1"><div class="li"> Dust, fog, clouds, smoke;</div>
</li>
<li class="level1"><div class="li"> Insects swarms, meteor showers;</div>
</li>
<li class="level1"><div class="li"> Magic spells.</div>
</li>
</ul>

<p>
These scene elements cannot be modeled by meshes. In very simple terms:
</p>
<ul>
<li class="level1"><div class="li"> The difference between an explosion and a dust cloud is the speed of the particle effect. </div>
</li>
<li class="level1"><div class="li"> The difference between flames and a waterfall is the direction and the color of the particle effect. </div>
</li>
</ul>

<p>
Particle effects can be animated (e.g. sparks, drops) and static (strands of grass, hair). Non-particle effects include bloom/glow, and motion blur/afterimage. In this tutorial you learn how to make animated particles (com.jme3.effect). 
</p>

<p>
</p><p></p><div class="notetip">To use the example assets in a new jMonkeyEngine SDK project, right-click your project, select “Properties”, go to “Libraries”, press “Add Library” and add the “jme3-test-data” library.
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (12) - Hello Effects" [1-1141] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.effect.ParticleEmitter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.effect.ParticleMesh</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 11 - how to create fire, water, and explosion effects. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloEffects <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloEffects app <span class="sy0">=</span> <span class="kw1">new</span> HelloEffects<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
    ParticleEmitter fire <span class="sy0">=</span> 
            <span class="kw1">new</span> ParticleEmitter<span class="br0">(</span><span class="st0">"Emitter"</span>, ParticleMesh.<span class="me1">Type</span>.<span class="me1">Triangle</span>, <span class="nu0">30</span><span class="br0">)</span><span class="sy0">;</span>
    Material mat_red <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
            <span class="st0">"Common/MatDefs/Misc/Particle.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat_red.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Texture"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Effects/Explosion/flame.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setMaterial</span><span class="br0">(</span>mat_red<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setImagesX</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> 
    fire.<span class="me1">setImagesY</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 2x2 texture animation</span>
    fire.<span class="me1">setEndColor</span><span class="br0">(</span>  <span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f, 0f, 0f, 1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// red</span>
    fire.<span class="me1">setStartColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f, 1f, 0f, 0.5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// yellow</span>
    fire.<span class="me1">getParticleInfluencer</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setInitialVelocity</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">2</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setStartSize</span><span class="br0">(</span>1.5f<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setEndSize</span><span class="br0">(</span>0.1f<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setGravity</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setLowLife</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setHighLife</span><span class="br0">(</span>3f<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">getParticleInfluencer</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setVelocityVariation</span><span class="br0">(</span>0.3f<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>fire<span class="br0">)</span><span class="sy0">;</span>
 
    ParticleEmitter debris <span class="sy0">=</span> 
            <span class="kw1">new</span> ParticleEmitter<span class="br0">(</span><span class="st0">"Debris"</span>, ParticleMesh.<span class="me1">Type</span>.<span class="me1">Triangle</span>, <span class="nu0">10</span><span class="br0">)</span><span class="sy0">;</span>
    Material debris_mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
            <span class="st0">"Common/MatDefs/Misc/Particle.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    debris_mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Texture"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Effects/Explosion/Debris.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">setMaterial</span><span class="br0">(</span>debris_mat<span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">setImagesX</span><span class="br0">(</span><span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span> 
    debris.<span class="me1">setImagesY</span><span class="br0">(</span><span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 3x3 texture animation</span>
    debris.<span class="me1">setRotateSpeed</span><span class="br0">(</span><span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">setSelectRandomImage</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">getParticleInfluencer</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setInitialVelocity</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">4</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">setStartColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">setGravity</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">6</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">getParticleInfluencer</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setVelocityVariation</span><span class="br0">(</span>.60f<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>debris<span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">emitAllParticles</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
You should see an explosion that sends debris flying, and a fire.
<a href="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/effect" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/effect" rel="nofollow">More example code is here.</a>
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [1142-3549] -->
<h3 class="sectionedit3" id="texture_animation_and_variation">Texture Animation and Variation</h3>
<div class="level3">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/Debris.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="96" height="96" /></a>
</p>

<p>
Start by choosing a material texture for your effect. If you provide the emitter with a set of textures (see image), it can use them either for variation (random order), or as animation steps (fixed order). 
</p>

<p>
Setting emitter textures works just as you have already learned in previous chapters. This time you base the material on the <code>Particle.j3md</code> material definition. Let's have a closer look at the material for the Debris effect. 
</p>
<pre class="code java">    ParticleEmitter debris <span class="sy0">=</span> 
            <span class="kw1">new</span> ParticleEmitter<span class="br0">(</span><span class="st0">"Debris"</span>, ParticleMesh.<span class="me1">Type</span>.<span class="me1">Triangle</span>, <span class="nu0">10</span><span class="br0">)</span><span class="sy0">;</span>
    Material debris_mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
            <span class="st0">"Common/MatDefs/Misc/Particle.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    debris_mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Texture"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Effects/Explosion/Debris.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">setMaterial</span><span class="br0">(</span>debris_mat<span class="br0">)</span><span class="sy0">;</span>
    debris.<span class="me1">setImagesX</span><span class="br0">(</span><span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span> 
    debris.<span class="me1">setImagesY</span><span class="br0">(</span><span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 3x3 texture animation</span>
    debris.<span class="me1">setSelectRandomImage</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        ...</pre>
<ol>
<li class="level1"><div class="li"> Create a material and load the texture.</div>
</li>
<li class="level1"><div class="li"> Tell the Emitter into how many animation steps (x*y) the texture is divided. <br />
The debris texture has 3×3 frames.</div>
</li>
<li class="level1"><div class="li"> Optionally, tell the Emitter whether the animation steps are to be at random, or in order. <br />
For the debris, the frames play at random.</div>
</li>
</ol>

<p>
As you see in the debris example, texture animations improve effects because each “flame” or “piece of debris” now looks different. Also think of electric or magic effects, where you can create very interesting animations by using an ordered morphing series of lightning bolts; or flying leaves or snow flakes, for instance.
</p>

<p>
The fire material is created the same way, just using “Effects/Explosion/flame.png” texture, which has with 2×2 ordered animation steps.
</p>

</div>
<!-- EDIT3 SECTION "Texture Animation and Variation" [3550-5408] -->
<h3 class="sectionedit4" id="default_particle_textures">Default Particle Textures</h3>
<div class="level3">

<p>
The following particle textures included in <code>test-data.jar</code>. You can copy and use them in your own effects.
</p>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Texture Path                     </th><th class="col1"> Dimension </th><th class="col2"> Preview </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> Effects/Explosion/Debris.png     </td><td class="col1 leftalign"> 3*3  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/Debris.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> Effects/Explosion/flame.png      </td><td class="col1 leftalign"> 2*2  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/flame.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> Effects/Explosion/shockwave.png  </td><td class="col1 leftalign"> 1*1  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/shockwave.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Effects/Explosion/smoketrail.png </td><td class="col1 leftalign"> 1*3  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/smoketrail.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> Effects/Smoke/Smoke.png          </td><td class="col1"> 1*15 </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Smoke/Smoke.png"><img src="/resources/fetch.php" class="media" alt="" width="96" height="32" /></a> </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [5557-6356] -->
<p>
Copy them into your <code>assets/Effects</code> directory to use them.
</p>

</div>
<!-- EDIT4 SECTION "Default Particle Textures" [5409-6420] -->
<h2 class="sectionedit6" id="creating_custom_textures">Creating Custom Textures</h2>
<div class="level2">

<p>
For your game, you will likely create custom particle textures. Look at the fire example again.
</p>
<pre class="code java">    ParticleEmitter fire <span class="sy0">=</span> 
            <span class="kw1">new</span> ParticleEmitter<span class="br0">(</span><span class="st0">"Emitter"</span>, ParticleMesh.<span class="me1">Type</span>.<span class="me1">Triangle</span>, <span class="nu0">30</span><span class="br0">)</span><span class="sy0">;</span>
    Material mat_red <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
            <span class="st0">"Common/MatDefs/Misc/Particle.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat_red.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Texture"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>
            <span class="st0">"Effects/Explosion/flame.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setMaterial</span><span class="br0">(</span>mat_red<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setImagesX</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> 
    fire.<span class="me1">setImagesY</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 2x2 texture animation</span>
    fire.<span class="me1">setEndColor</span><span class="br0">(</span>  <span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f, 0f, 0f, 1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// red</span>
    fire.<span class="me1">setStartColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f, 1f, 0f, 0.5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// yellow</span>
 </pre>

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/flame.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="96" height="96" /></a>
</p>

<p>
Compare the texture with the resulting effect.
</p>
<ul>
<li class="level1"><div class="li"> Black parts of the image become fully transparent. </div>
</li>
<li class="level1"><div class="li"> White/gray parts of the image are translucent and get colorized.</div>
</li>
<li class="level1"><div class="li"> You set the color using <code>setStartColor()</code> and <code>setEndColor()</code>. <br />
For fire, is's a gradient from yellow to red. </div>
</li>
<li class="level1"><div class="li"> By default, the animation is played in order and loops.</div>
</li>
</ul>

<p>
Create a grayscale texture in a graphic editor, and save it to your <code>assets/Effects</code> directory. If you split up one image file into x*y animation steps, make sure each square is of equal size–just as you see in the examples here. 
</p>

</div>
<!-- EDIT6 SECTION "Creating Custom Textures" [6421-7818] -->
<h3 class="sectionedit7" id="emitter_parameters">Emitter Parameters</h3>
<div class="level3">

<p>
A particle system is always centered around an emitter. 
</p>

<p>
Use the <code>setShape()</code> method to change the EmitterShape:
</p>
<ul>
<li class="level1"><div class="li"> EmitterPointShape(Vector3f.ZERO) –  particles emit from a point (default)</div>
</li>
<li class="level1"><div class="li"> EmitterSphereShape(Vector3f.ZERO,2f) – particles emit from a sphere-sized area</div>
</li>
<li class="level1"><div class="li"> EmitterBoxShape(new Vector3f(-1f,-1f,-1f),new Vector3f(1f,1f,1f)) – particles emit from a box-sized area</div>
</li>
</ul>

<p>
Example: 
</p>
<pre class="code java">emitter.<span class="me1">setShape</span><span class="br0">(</span><span class="kw1">new</span> EmitterPointShape<span class="br0">(</span>Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You create different effects by changing the emitter parameters: 
</p>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Parameter           </th><th class="col1"> Method </th><th class="col2"> Default </th><th class="col3"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> number              </td><td class="col1"> <code>setNumParticles()</code> </td><td class="col2"> N/A </td><td class="col3"> The maximum number of particles visible at the same time. Value is specified by user in constructor. This influences the density and length of the “trail”. </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> velocity            </td><td class="col1 leftalign"> <code>getParticleInfluencer(). setInitialVelocity()</code>  </td><td class="col2"> Vector3f.ZERO </td><td class="col3"> Specify a vector how fast particles move and in which start direction. </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> direction           </td><td class="col1"> <code>getParticleInfluencer(). setVelocityVariation()</code> <br />
<code>setFacingVelocity()</code> <br />
<code>setRandomAngle()</code> <br />
<code>setFaceNormal()</code> <br />
<code>setRotateSpeed()</code> </td><td class="col2"> 0.2f <br />
false <br />
false <br />
Vector3f.NAN <br />
0.0f </td><td class="col3"> Optional accessors that control in which direction particles face while flying. </td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> lifetime            </td><td class="col1"> <code>setLowLife()</code> <br />
<code>setHighLife()</code> </td><td class="col2 leftalign"> 3f  <br />
7f  </td><td class="col3"> Minimum and maximum time period before particles fade. </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> emission rate       </td><td class="col1"> <code>setParticlesPerSec()</code> </td><td class="col2"> 20 </td><td class="col3"> How many new particles are emitted per second. </td>
	</tr>
	<tr class="row6">
		<td class="col0 leftalign"> color               </td><td class="col1"> <code>setStartColor()</code> <br />
<code>setEndColor()</code> </td><td class="col2"> gray </td><td class="col3"> Set to the same colors, or to two different colors for a gradient effect. </td>
	</tr>
	<tr class="row7">
		<td class="col0 leftalign"> size                </td><td class="col1"> <code>setStartSize()</code> <br />
<code>setEndSize()</code> </td><td class="col2"> 0.2f <br />
2f </td><td class="col3"> Set to two different values for shrink/grow effect, or to same size for constant effect. </td>
	</tr>
	<tr class="row8">
		<td class="col0 leftalign"> gravity             </td><td class="col1"> <code>setGravity()</code> </td><td class="col2"> 0,1,0 </td><td class="col3"> Whether particles fall down (positive) or fly up (negative). Set to 0f for a zero-g effect where particles keep flying. </td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [8389-9861] -->
<p>
You can find details about <a href="/jme3/advanced/particle_emitters.html" class="wikilink1" title="jme3:advanced:particle_emitters">effect parameters</a> here.
Add and modify one parameter at a time, and try different values until you get the effect you want. 
</p>

<p>
</p><p></p><div class="notetip"><strong>Tip:</strong> Use the SceneComposer in the jMonkeyEngine SDK to create effects more easily. Create an empty scene and add an emitter object to it. Change the emitter properties and watch the outcome live. You can save created effects as .j3o file and load them like scenes or models.
</div>


</div>
<!-- EDIT7 SECTION "Emitter Parameters" [7819-10370] -->
<h2 class="sectionedit9" id="exercise">Exercise</h2>
<div class="level2">

<p>
Can you “invert” the fire effect into a small waterfall? Here some tips:
</p>
<ul>
<li class="level1"><div class="li"> Change the Red and Yellow color to Cyan and Blue</div>
</li>
<li class="level1"><div class="li"> Invert the velocity vector (direction) by using a negative number</div>
</li>
<li class="level1"><div class="li"> Swap start and end size</div>
</li>
<li class="level1"><div class="li"> Activate gravity by setting it to 0,1,0</div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Exercise" [10371-10661] -->
<h2 class="sectionedit10" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned that many different effects can be created by changing the parameters and textures of one general emitter object.
</p>

<p>
Now you move on to another exciting chapter – the simulation of <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_physics" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:beginner:hello_physics" rel="nofollow">physical objects</a>. Let's shoot some cannon balls at a brick wall!
</p>
<hr />
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/transparency.html" class="wikilink1" title="tag:transparency" rel="tag">transparency</a>,
	<a href="/tag/effect.html" class="wikilink1" title="tag:effect" rel="tag">effect</a>
</span></div>

</div>
<!-- EDIT10 SECTION "Conclusion" [10662-] -->
