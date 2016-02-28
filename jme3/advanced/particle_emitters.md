---
title: Particle Emmitter Settings
---
<h1 class="sectionedit1" id="particle_emmitter_settings">Particle Emmitter Settings</h1>
<div class="level1">

<p>
You cannot create a 3D model for delicate things like fire, smoke, or explosions. Particle Emitters are quite an efficient solution to create these kinds of effects: The emitter renders a series of flat orthogonal images and manipulates them in a way that creates the illusion of a anything from a delicate smoke cloud to individual flames, etc.
Creating an effect involves some trial and error to get the settings <em>just right</em>, and it's worth exploring the expressiveness of the options described below. 
</p>

<p>
</p><p></p><div class="notetip">Use the <a href="/sdk/scene_explorer.html" class="wikilink1" title="sdk:scene_explorer">Scene Explorer</a> in the <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> to design and preview effects.
</div>


<p>
<a href="/resources/jme3-advanced-explosion-5.png" class="media" title="jme3:advanced:explosion-5.png"><img src="/resources/jme3-advanced-explosion-5.png" class="media" alt="" width="150" height="100" /></a>  <a href="/resources/jme3-advanced-particle.png" class="media" title="jme3:advanced:particle.png"><img src="/resources/jme3-advanced-particle.png" class="media" alt="" width="150" height="100" /></a>  <a href="/resources/jme3-beginner-beginner-effect-fire.png" class="media" title="jme3:beginner:beginner-effect-fire.png"><img src="/resources/jme3-beginner-beginner-effect-fire.png" class="media" alt="" width="150" height="100" /></a> <a href="/resources/jme3-advanced-butterfly-particle-emitter.png" class="media" title="jme3:advanced:butterfly-particle-emitter.png"><img src="/resources/jme3-advanced-butterfly-particle-emitter.png" class="media" alt="" width="150" height="100" /></a>
</p>

</div>
<!-- EDIT1 SECTION "Particle Emmitter Settings" [1-844] -->
<h2 class="sectionedit2" id="create_an_emitter">Create an Emitter</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Create one emitter for each effect: <pre class="code java">ParticleEmitter explosion <span class="sy0">=</span> <span class="kw1">new</span> ParticleEmitter<span class="br0">(</span>
<span class="st0">"My explosion effect"</span>, Type.<span class="me1">Triangle</span>, <span class="nu0">30</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Attach the emitter to the rootNode and position it in the scene: <pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>explosion<span class="br0">)</span><span class="sy0">;</span>
explosion.<span class="me1">setLocalTranslation</span><span class="br0">(</span>bomb.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Trigger the effect by calling <pre class="code java">explosion.<span class="me1">emitAllParticles</span><span class="br0">(</span><span class="br0">)</span></pre>
</div>
</li>
<li class="level1"><div class="li"> End the effect by calling <pre class="code java">explosion.<span class="me1">killAllParticles</span><span class="br0">(</span><span class="br0">)</span></pre>
</div>
</li>
</ol>

<p>
Choose one of the following mesh shapes
</p>
<ul>
<li class="level1"><div class="li"> Type.Triangle</div>
</li>
<li class="level1"><div class="li"> Type.Point</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Create an Emitter" [845-1434] -->
<h2 class="sectionedit3" id="configure_parameters">Configure Parameters</h2>
<div class="level2">

<p>
Not all of these parameters are required for all kinds of effects. If you don't specify one of them, a default value will be used.
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Parameter           </th><th class="col1 leftalign"> Method                </th><th class="col2"> Default </th><th class="col3"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> number              </td><td class="col1"> <code>setNumParticles()</code> </td><td class="col2 leftalign">  </td><td class="col3"> The maximum number of particles visible at the same time. Specified by user in constructor. </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> emission rate       </td><td class="col1"> <code>setParticlesPerSec()</code> </td><td class="col2"> 20 </td><td class="col3"> Density of the effect, how many new particles are emitted per second. <br />
Set to zero to control the start/end of the effect. <br />
Set to a number for a constantly running effect. </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> size                </td><td class="col1"> <code>setStartSize()</code>, <code>setEndSize()</code> </td><td class="col2"> 0.2f, 2f </td><td class="col3"> The radius of the scaled sprite image. Set both to same value for constant size effect. <br />
Set to different values for shrink/grow effect. </td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> color               </td><td class="col1"> <code>setStartColor()</code>, <code>setEndColor()</code> </td><td class="col2"> gray </td><td class="col3"> Controls how the opaque (non-black) parts of the texture are colorized. <br />
Set both to the same color for single-colored effects (e.g. fog, debris). <br />
Set both to different colors for a gradient effect (e.g. fire). </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> direction/velocity  </td><td class="col1"> <code>getParticleInfluencer(). setInitialVelocity(initialVelocity)</code> </td><td class="col2"> Vector3f(0,0,0) </td><td class="col3"> A vector specifying the initial direction and speed of particles. The longer the vector, the faster. </td>
	</tr>
	<tr class="row6">
		<td class="col0 leftalign"> fanning out         </td><td class="col1"> <code>getParticleInfluencer(). setVelocityVariation(variation)</code> </td><td class="col2"> 0.2f </td><td class="col3"> How much the direction (<code>setInitialVelocity()</code>) can vary among particles. Use a value between 1 and 0 to create a directed swarm-like cloud of particles. <br />
1 = Maximum variation, particles emit in random 360° directions (e.g. explosion, butterflies). <br />
0.5f = particles are emitted within 180° of the initial direction. <br />
0 = No variation, particles fly in a straight line in direction of start velocity (e.g. lasergun blasts). </td>
	</tr>
	<tr class="row7">
		<td class="col0"> direction <br />
(pick one)</td><td class="col1"> <code>setFacingVelocity()</code> </td><td class="col2"> false </td><td class="col3"> true = Flying particles pitch in the direction they're flying (e.g. missiles). <br />
false = Particles keep flying rotated the way they started (e.g. debris). </td>
	</tr>
	<tr class="row8">
		<td class="col0"> direction <br />
(pick one)</td><td class="col1"> <code>setFaceNormal()</code> </td><td class="col2"> Vector3f.NAN </td><td class="col3"> Vector3f = Flying particles face in the given direction (e.g. horizontal shockwave faces up = Vector3f.UNIT_Y). <br />
Vector3f.NAN = Flying particles face the camera. </td>
	</tr>
	<tr class="row9">
		<td class="col0 leftalign"> lifetime  </td><td class="col1"> <code>setLowLife()</code>, <code>setHighLife()</code> </td><td class="col2"> 3f, 7f </td><td class="col3"> The time period before a particle fades is set to a random value between minimum and maximum; minimum must be smaller than maximum. A minimum &lt; 1f makes the effect more busy, a higher minimum looks more steady. Use a maximum &lt; 1f for short bursts, and higher maxima for long lasting swarms or smoke. Set maximum and minimum to similar values to create an evenly spaced effect (e.g. fountain), set the to very different values to create a distorted effect (e.g. fire with individual long flames). </td>
	</tr>
	<tr class="row10">
		<td class="col0 leftalign"> spinning          </td><td class="col1"> <code>setRotateSpeed()</code> </td><td class="col2"> 0f </td><td class="col3"> 0 = Flying particles don't spin while flying (e.g. smoke, insects, controlled projectiles). <br />
&gt; 0 = How fast particle spins while flying (e.g. debris, shuriken, missiles out of control). </td>
	</tr>
	<tr class="row11">
		<td class="col0 leftalign"> rotation          </td><td class="col1"> <code>setRandomAngle()</code> </td><td class="col2"> false </td><td class="col3"> true = The particle sprite is rotated at a random angle when it is emitted (e.g. explosion, debris). <br />
false = Particles fly straight like you drew them in the sprite texture (e.g. insects). </td>
	</tr>
	<tr class="row12">
		<td class="col0 leftalign"> gravity           </td><td class="col1"> <code>setGravity()</code> </td><td class="col2"> Vector3f(0.0f,0.1f,0.0f) </td><td class="col3"> Particles fall in the direction of the vector (e.g. debris, sparks). <br />
(0,0,0) = Particles keep flying in start direction (e.g. flames, zero-gravity explosion.) </td>
	</tr>
	<tr class="row13">
		<td class="col0 leftalign"> start area        </td><td class="col1"><code>setShape(new EmitterSphereShape( Vector3f.ZERO, 2f));</code></td><td class="col2">EmitterPointShape()</td><td class="col3">By default, particles are emitted from the emitters location (a point). You can increase the emitter shape to occupy a sphere, so that the start point of new particles can be anywhere inside the sphere, which makes the effect a bit more irregular.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [1599-5373] -->
<p>
Build up you effect by specifying one parameter after the other. If you change several parameters at the same time, it's difficult to tell which of the values caused which outcome.
</p>

</div>
<!-- EDIT3 SECTION "Configure Parameters" [1435-5555] -->
<h2 class="sectionedit5" id="create_an_effect_material">Create an Effect Material</h2>
<div class="level2">

<p>
<a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/flash.png"><img src="/resources/fetch.php" class="mediaright" alt="" width="128" height="128" /></a>
</p>

<p>
Use the common Particle.j3md Material Definition and a texture to specify the shape of the particles. The shape is defined by the texture you provide and can be anything – debris, flames, smoke, mosquitoes, leaves, butterflies… be creative.
</p>
<pre class="code java">    Material flash_mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>
        assetManager, <span class="st0">"Common/MatDefs/Misc/Particle.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    flash_mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Texture"</span>,
        assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Effects/Explosion/flash.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    flash.<span class="me1">setMaterial</span><span class="br0">(</span>flash_mat<span class="br0">)</span><span class="sy0">;</span>
    flash.<span class="me1">setImagesX</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// columns</span>
    flash.<span class="me1">setImagesY</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// rows</span>
    flash.<span class="me1">setSelectRandomImage</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The effect texture can be one image, or contain a sprite animation – a series of slightly different pictures in equally spaced rows and columns. If you choose the sprite animation:
</p>
<ul>
<li class="level1"><div class="li"> Specify the number of rows and columns using setImagesX(2) and setImagesY().</div>
</li>
<li class="level1"><div class="li"> Specify whether you want to play the sprite series in order (animation), or at random (explosion, flame), by setting setSelectRandomImage() true or false.</div>
</li>
</ul>

<p>
<strong>Examples:</strong> Have a look at the following default textures and you will see how you can create your own sprite textures after the same fashion.
</p>

</div>
<!-- EDIT5 SECTION "Create an Effect Material" [5556-6876] -->
<h3 class="sectionedit6" id="default_particle_textures">Default Particle Textures</h3>
<div class="level3">

<p>
The Material is used together with grayscale texture: The black parts will be transparent and the white parts will be opaque (colored).
The following effect textures are available by default from <code>test-data.jar</code>. You can also load your own textures from your assets directory.
</p>
<div class="table sectionedit7"><table class="inline">
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
		<td class="col0 leftalign"> Effects/Explosion/flash.png      </td><td class="col1 leftalign"> 2*2  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/flash.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Effects/Explosion/roundspark.png </td><td class="col1 leftalign"> 1*1  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/roundspark.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> Effects/Explosion/shockwave.png  </td><td class="col1 leftalign"> 1*1  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/shockwave.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row6">
		<td class="col0"> Effects/Explosion/smoketrail.png </td><td class="col1 leftalign"> 1*3  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/smoketrail.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row7">
		<td class="col0 leftalign"> Effects/Explosion/spark.png      </td><td class="col1 leftalign"> 1*1  </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Explosion/spark.png"><img src="/resources/fetch.php" class="media" alt="" width="32" height="32" /></a> </td>
	</tr>
	<tr class="row8">
		<td class="col0 leftalign"> Effects/Smoke/Smoke.png          </td><td class="col1"> 1*15 </td><td class="col2"> <a href="/resources/fetch.php" class="media" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/test-data/Effects/Smoke/Smoke.png"><img src="/resources/fetch.php" class="media" alt="" width="96" height="32" /></a> </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [7192-8437] -->
<p>
<strong>Tip:</strong> Use the <code>setStartColor()</code>/<code>setEndColor()</code> settings described above to colorize the white and gray parts of textures.
</p>

</div>
<!-- EDIT6 SECTION "Default Particle Textures" [6877-8569] -->
<h2 class="sectionedit8" id="usage_example">Usage Example</h2>
<div class="level2">
<pre class="code java">    ParticleEmitter fire <span class="sy0">=</span> <span class="kw1">new</span> ParticleEmitter<span class="br0">(</span><span class="st0">"Emitter"</span>, Type.<span class="me1">Triangle</span>, <span class="nu0">30</span><span class="br0">)</span><span class="sy0">;</span>
    Material mat_red <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Particle.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat_red.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Texture"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Effects/Explosion/flame.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setMaterial</span><span class="br0">(</span>mat_red<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setImagesX</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> fire.<span class="me1">setImagesY</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 2x2 texture animation</span>
    fire.<span class="me1">setEndColor</span><span class="br0">(</span>  <span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f, 0f, 0f, 1f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// red</span>
    fire.<span class="me1">setStartColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f, 1f, 0f, 0.5f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// yellow</span>
        fire.<span class="me1">getParticleInfluencer</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setInitialVelocity</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">2</span>,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setStartSize</span><span class="br0">(</span>1.5f<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setEndSize</span><span class="br0">(</span>0.1f<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setGravity</span><span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setLowLife</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">setHighLife</span><span class="br0">(</span>3f<span class="br0">)</span><span class="sy0">;</span>
    fire.<span class="me1">getParticleInfluencer</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setVelocityVariation</span><span class="br0">(</span>0.3f<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>fire<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Browse the full source code of all <a href="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/effect" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/tree/master/jme3-examples/src/main/java/jme3test/effect" rel="nofollow">effect examples</a> here.
</p>
<hr />

<p>
See also: <a href="/jme3/advanced/effects_overview.html" class="wikilink1" title="jme3:advanced:effects_overview">Effects Overview</a>
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/effect.html" class="wikilink1" title="tag:effect" rel="tag">effect</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Usage Example" [8570-] -->
