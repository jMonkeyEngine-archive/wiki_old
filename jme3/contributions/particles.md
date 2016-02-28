---
title: Next Generation Particle Emitters
---
<h1 class="sectionedit1" id="next_generation_particle_emitters">Next Generation Particle Emitters</h1>
<div class="level1">

<p>
This is a new particle system for jME3 posted for review and comments. This is an opportunity for people to comment on and request changes to the <abbr title="Application Programming Interface">API</abbr> or the internal functionality of the system.
The code for this particle system can be found <a href="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/#svn%2Ftrunk%2FParticleController" class="urlextern" title="https://code.google.com/p/jmonkeyplatform-contributions/source/browse/#svn%2Ftrunk%2FParticleController" rel="nofollow">here</a>
</p>

<p>
Apologies for the slight jitter in some of the videos, the VideoRecorderState seems to be causing some issues which are not present when the application is running normally.
</p>

</div>
<!-- EDIT1 SECTION "Next Generation Particle Emitters" [1-580] -->
<h3 class="sectionedit2" id="credits">Credits</h3>
<div class="level3">

<p>
These particle emitters are inspired by and use some code from t0neg0ds particle emitters as described <a href="http://hub.jmonkeyengine.org/t/influencer-based-particleemitter-candidate-mesh-based-animated-particles/25831" class="urlextern" title="http://hub.jmonkeyengine.org/t/influencer-based-particleemitter-candidate-mesh-based-animated-particles/25831" rel="nofollow">here</a>
</p>

<p>
Those in turn were based on the original jME3 particle system by Kirill Vainer
</p>

</div>
<!-- EDIT2 SECTION "Credits" [581-904] -->
<h3 class="sectionedit3" id="the_big_picture">The Big Picture</h3>
<div class="level3">

<p>
The core of all Particle Emitters is a ParticleController. That is used to manage all of the particles, the behaviour of the particles themselves though is controlled though a number of other classes that are plugged in to the ParticleController to provide the required functionality. You can think of the ParticleController as providing the central hub into which you plug all the modules you need to get the desired behaviour.
</p>

<p>
An easy way to see what you need is to create a new ParticleController and then look at the constructor, you can see what parameters need to be supplied there.
</p>
<div class="table sectionedit4"><table class="inline">
	<tr class="row0">
		<td class="col0"> name </td><td class="col1"> The name to use for the geometry in the scene graph </td>
	</tr>
	<tr class="row1">
		<td class="col0"> mesh </td><td class="col1"> The mesh to use (Usually either PointMesh or QuadMesh) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> maxParticles </td><td class="col1"> The maximum number of particles to allow active at any one time </td>
	</tr>
	<tr class="row3">
		<td class="col0"> lifeMin </td><td class="col1"> The minimum amount of time (in seconds) for which each particle lives </td>
	</tr>
	<tr class="row4">
		<td class="col0"> lifeMax </td><td class="col1"> The maximum amount of time (in seconds) for which each particle lives </td>
	</tr>
	<tr class="row5">
		<td class="col0"> source </td><td class="col1"> The source from which the particles are spawned </td>
	</tr>
	<tr class="row6">
		<td class="col0"> emissionController </td><td class="col1"> The frequency and timing with which particles are spawned. If null then no particles are automatically spawned and they must be triggered manually using emitNextParticle() or emitAllParticles() </td>
	</tr>
	<tr class="row7">
		<td class="col0"> influencers </td><td class="col1"> Zero or more ParticleInfluencers, each of which changes the behaviour of the particles. </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [1523-2288] -->
<p>
By selecting the behaviour you desire for each option you can configure up a virtually infinite array of possible particle emitters.
</p>

<p>
We will now walk through some common examples and possible uses, and then in the end we will document all of the possible choices for these options.
</p>

<p>
For a full reference of the standard options available see the <a href="/jme3/contributions/particles/reference.html" class="wikilink1" title="jme3:contributions:particles:reference">Reference Page</a>.
</p>

</div>
<!-- EDIT3 SECTION "The Big Picture" [905-2695] -->
<h3 class="sectionedit5" id="simple_fire">Simple Fire</h3>
<div class="level3">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HelloParticles1_SimpleFire <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloParticles1_SimpleFire app <span class="sy0">=</span> <span class="kw1">new</span> HelloParticles1_SimpleFire<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// start the game</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
<span class="co1">// Construct a new ParticleController       </span>
        ParticleController pCtrl <span class="sy0">=</span> <span class="kw1">new</span> ParticleController<span class="br0">(</span>
<span class="co1">// The name of the emitter</span>
                <span class="st0">"SimpleFire"</span>, 
<span class="co1">// Use a simple point mesh (the fastest but most limitted mesh type) with the specified</span>
<span class="co1">// image (from jME3-testdata). The image actually contains a 2x2 grid of sprites.</span>
                <span class="kw1">new</span> PointMesh<span class="br0">(</span>assetManager, <span class="st0">"Effects/Explosion/flame.png"</span>, <span class="nu0">2</span>, <span class="nu0">2</span><span class="br0">)</span>,
<span class="co1">// Allow at most 32 particles at any time                </span>
                <span class="nu0">32</span>, 
<span class="co1">// Particles last for at least 2 seconds                </span>
                <span class="nu0">2</span>, 
<span class="co1">// And at most 3 seconds</span>
                <span class="nu0">3</span>,
<span class="co1">// Point sources always generate particles at the location of the source, the particles</span>
<span class="co1">// are given a random velocity between the two given.</span>
                <span class="kw1">new</span> PointSource<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">3</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">3</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">0</span>, <span class="nu0">3</span><span class="br0">)</span><span class="br0">)</span>,
<span class="co1">// Emit particles at regular intervals, 10 particles every second</span>
                <span class="kw1">new</span> RegularEmission<span class="br0">(</span><span class="nu0">10</span><span class="br0">)</span>,
<span class="co1">// ** Influencers start here                </span>
<span class="co1">// Select a random sprite from the 4 available for each particle                </span>
                <span class="kw1">new</span> RandomSpriteInfluencer<span class="br0">(</span><span class="br0">)</span>,
<span class="co1">// Particles start off with a size of 0.5 units, end with a radius of 0.1                </span>
                <span class="kw1">new</span> SizeInfluencer<span class="br0">(</span>0.5f, 0.1f<span class="br0">)</span>,
<span class="co1">// Particles start yellow full opacity and fade towards red with very low opacity</span>
                <span class="kw1">new</span> ColorInfluencer<span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,0.2f,<span class="nu0">1</span><span class="br0">)</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span>,0.1f<span class="br0">)</span><span class="br0">)</span>,
<span class="co1">// No matter what velocity particles started with they will start moving upwards.               </span>
                <span class="kw1">new</span> PreferredDirectionInfluencer<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span>, 0.25f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Finally attach the geometry to the rootNode in order to start the particles running</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Run that and the result should look something like:
</p>

<p>
<a href="/resources/jme3-particles1.jpg" class="media" title="jme3:particles1.jpg"><img src="/resources/jme3-particles1.jpg" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT5 SECTION "Simple Fire" [2696-4855] -->
<h3 class="sectionedit6" id="simple_fire_and_smoke">Simple Fire and Smoke</h3>
<div class="level3">
<pre class="code java">    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
<span class="co1">// Construct a new ParticleController       </span>
        ParticleController pCtrl <span class="sy0">=</span> <span class="kw1">new</span> ParticleController<span class="br0">(</span>
<span class="co1">// The name of the emitter</span>
                <span class="st0">"SimpleFire"</span>, 
<span class="co1">// Use a simple point mesh (the fastest but most limitted mesh type) with the specified</span>
<span class="co1">// image (from jME3-testdata). The image actually contains a 2x2 grid of sprites.</span>
                <span class="kw1">new</span> PointMesh<span class="br0">(</span>assetManager, <span class="st0">"Effects/Explosion/flame.png"</span>, <span class="nu0">2</span>, <span class="nu0">2</span><span class="br0">)</span>,
<span class="co1">// Allow at most 50 particles at any time, the particles are lasting longer this time</span>
<span class="co1">// so we need to allow more on screen at once                </span>
                <span class="nu0">50</span>, 
<span class="co1">// Particles last for at least 4 seconds                </span>
                <span class="nu0">4</span>, 
<span class="co1">// And at most 5 seconds</span>
                <span class="nu0">5</span>,
<span class="co1">// Point sources always generate particles at the location of the source, the particles</span>
<span class="co1">// are given a random velocity between the two given.</span>
                <span class="kw1">new</span> PointSource<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">3</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">3</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">0</span>, <span class="nu0">3</span><span class="br0">)</span><span class="br0">)</span>,
<span class="co1">// Emit particles at regular intervals, 10 particles every second</span>
                <span class="kw1">new</span> RegularEmission<span class="br0">(</span><span class="nu0">10</span><span class="br0">)</span>,
<span class="co1">// ** Influencers start here                </span>
<span class="co1">// Select a random sprite from the 4 available for each particle                </span>
                <span class="kw1">new</span> RandomSpriteInfluencer<span class="br0">(</span><span class="br0">)</span>,
<span class="co1">// Particles start off with a size of 0.5 units, end with a radius of 0.1                </span>
                <span class="kw1">new</span> SizeInfluencer<span class="br0">(</span>0.5f, 0.25f<span class="br0">)</span>,
<span class="co1">// Particles start yellow full opacity and fade towards red with very low opacity</span>
                <span class="kw1">new</span> MultiColorInfluencer<span class="br0">(</span>
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span><span class="nu0">0</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, 0.1f, <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span>,
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span>0.15f, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span>, 0.25f<span class="br0">)</span><span class="br0">)</span>,
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span>0.3f, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f, 1f, 1f, 0.5f<span class="br0">)</span><span class="br0">)</span>,
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span><span class="nu0">1</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f,1f,1f,0f<span class="br0">)</span><span class="br0">)</span>
                <span class="br0">)</span>,
<span class="co1">// No matter what velocity particles started with they will start moving upwards.               </span>
                <span class="kw1">new</span> PreferredDirectionInfluencer<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span>, 0.25f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Finally attach the geometry to the rootNode in order to start the particles running</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span></pre>

<p>
You can see that the only change is to make the particles last a little longer and to change the ColorInfluencer for a MultiColorInfluencer, and yet the results look quite different:
</p>

<p>
<a href="/resources/jme3-particles2.jpg" class="media" title="jme3:particles2.jpg"><img src="/resources/jme3-particles2.jpg" class="media" alt="" /></a>
</p>

<p>
This isn't a very convincing fire yet, but it is very simple to get up and running. One problem with this approach is that particles are done using an alpha-additive material, they can only make things brighter but never darker. That is not ideal for smoke which should be able to make them darker too. We will look at this again later but for now we will move on to some different mesh types.
</p>

</div>
<!-- EDIT6 SECTION "Simple Fire and Smoke" [4856-7723] -->
<h3 class="sectionedit7" id="quad_meshes_and_billboarding">Quad Meshes and Billboarding</h3>
<div class="level3">

<p>
Point Meshes are extremely fast, but they have a number of limitations. The main ones being that the sprites must always be facing towards the screen and that on certain graphics cards the maximum number of pixels a sprite can occupy on the screen is limited.
</p>

<p>
While PointMesh is recommended for basic particles for more advanced options there is the QuadMesh, this constructs each particle using a quad and as a result can allow any size on the screen and any orientation. The following example combines two separate particle emitters to produce a spell-like effect.
</p>

<p>
</p><p></p><div class="noteclassic">
The flame image from before is used for the second emitter, the first emitter uses this image which you can download and use:


<p>
<a href="/resources/jme3-runecircle.png" class="media" title="jme3:runecircle.png"><img src="/resources/jme3-runecircle.png" class="media" alt="" width="256" /></a>

</p></div>

<pre class="code java">    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
<span class="co1">// Construct a new ParticleController to provide the actual spell runes effect     </span>
        ParticleController pCtrl <span class="sy0">=</span> <span class="kw1">new</span> ParticleController<span class="br0">(</span>
<span class="co1">// The name of the emitter</span>
                <span class="st0">"SpellRunes"</span>, 
<span class="co1">// Use a Quad Mesh, this image is available for download on this page. The texture file contains</span>
<span class="co1">// a single image so there are no sprite columns and rows to set up. The BillboardStrategy is how</span>
<span class="co1">// the particles should be oriented, in this case it uses the particle rotation.</span>
                <span class="kw1">new</span> QuadMesh<span class="br0">(</span>QuadMeshBillboardStrategy.<span class="me1">USE_PARTICLE_ROTATION</span>, assetManager, <span class="st0">"Textures/runeCircle.png"</span><span class="br0">)</span>,
<span class="co1">// Allow at most 9 particles at any time</span>
                <span class="nu0">9</span>, 
<span class="co1">// Particles always last for 4 seconds                </span>
                <span class="nu0">4</span>, 
                <span class="nu0">4</span>,
<span class="co1">// We want to generate all particles from the same location with the same velocity.</span>
                <span class="kw1">new</span> PointSource<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, 1f, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, 1f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span>,
<span class="co1">// Emit particles at regular intervals, 4 particles every second</span>
                <span class="kw1">new</span> RegularEmission<span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span>,
<span class="co1">// ** Influencers start here                </span>
<span class="co1">// These particles should be size 3 and stay the same size</span>
                <span class="kw1">new</span> SizeInfluencer<span class="br0">(</span><span class="nu0">3</span>, <span class="nu0">3</span><span class="br0">)</span>,
<span class="co1">// Start the particles at full opacity blue and then fade them out to 0 opacity cyan.                </span>
                <span class="kw1">new</span> ColorInfluencer<span class="br0">(</span>ColorRGBA.<span class="me1">Blue</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span>,
<span class="co1">// Rotate all particles by the same amount. The units are radians-per-second              </span>
                <span class="kw1">new</span> RotationInfluencer<span class="br0">(</span>
                    <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, FastMath.<span class="me1">QUARTER_PI</span>, <span class="nu0">0</span><span class="br0">)</span>,
                    <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, FastMath.<span class="me1">QUARTER_PI</span>, <span class="nu0">0</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Finally attach the geometry to the rootNode in order to start the particles running</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
 
<span class="co1">// Construct a new ParticleController to provide the central glow effect</span>
        pCtrl <span class="sy0">=</span> <span class="kw1">new</span> ParticleController<span class="br0">(</span>
<span class="co1">// The name of the emitter</span>
                <span class="st0">"SpellBase"</span>, 
<span class="co1">// Use a simple point mesh (the fastest but most limitted mesh type) with the specified</span>
<span class="co1">// image (from jME3-testdata). The image actually contains a 2x2 grid of sprites.</span>
                <span class="kw1">new</span> PointMesh<span class="br0">(</span>assetManager, <span class="st0">"Textures/flame.png"</span>, <span class="nu0">2</span>, <span class="nu0">2</span><span class="br0">)</span>,
<span class="co1">// Allow at most 76 particles at any time                </span>
                <span class="nu0">76</span>, 
<span class="co1">// Particles last for at least 5 seconds                </span>
                <span class="nu0">5</span>, 
<span class="co1">// And at most 5 seconds</span>
                <span class="nu0">5</span>,
<span class="co1">// Point sources always generate particles at the location of the source, the particles</span>
<span class="co1">// are given a random velocity between the two given.</span>
                <span class="kw1">new</span> PointSource<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>1f, <span class="nu0">0</span>, <span class="sy0">-</span>1f<span class="br0">)</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span>1f, 0.5f, 1f<span class="br0">)</span><span class="br0">)</span>,
<span class="co1">// Emit particles at regular intervals, 15 particles every second</span>
                <span class="kw1">new</span> RegularEmission<span class="br0">(</span><span class="nu0">15</span><span class="br0">)</span>,
<span class="co1">// ** Influencers start here                </span>
<span class="co1">// Select a random sprite from the 4 available for each particle                </span>
                <span class="kw1">new</span> RandomSpriteInfluencer<span class="br0">(</span><span class="br0">)</span>,
<span class="co1">// Particles start red with some blue and green and fade towards blue zero opacity</span>
<span class="co1">// Because particles are rendered using an additive blend then any area where a lot</span>
<span class="co1">// of particles overlap will end up white.</span>
                <span class="kw1">new</span> ColorInfluencer<span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>,0.25f,0.25f,0.25f<span class="br0">)</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">0</span>,<span class="nu0">1</span>,0f<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Finally attach the geometry to the rootNode in order to start the particles running</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
 
        cam.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">10</span>, <span class="sy0">-</span><span class="nu0">10</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        cam.<span class="me1">lookAt</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span></pre>

<p>
The result should look something like:
<a href="/lib/exe/fetch.php/jme3:contributions:youtube_spjqag99hy" class="media mediafile mf_ wikilink2" title="jme3:contributions:youtube_spjqag99hy">youtube_spjqag99hy</a>
</p>

</div>
<!-- EDIT7 SECTION "Quad Meshes and Billboarding" [7724-12105] -->
<h3 class="sectionedit8" id="using_a_mesh_as_the_particle_source">Using a mesh as the particle source</h3>
<div class="level3">

<p>
There is a model of a monkeys head in the test data that is used in this example, although you can use any other model you like. Just make sure you can find the geometry within the model for the next step.
</p>
<pre class="code java">    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        Node monkey <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/MonkeyHead/MonkeyHead.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>monkey<span class="br0">)</span><span class="sy0">;</span>
 
        DirectionalLight dl <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        dl.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f,<span class="sy0">-</span>0.7f,<span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        dl.<span class="me1">setColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span>0.88f, 0.60f, 0.60f, 1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span>dl<span class="br0">)</span><span class="sy0">;</span>
 
        AmbientLight al <span class="sy0">=</span> <span class="kw1">new</span> AmbientLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        al.<span class="me1">setColor</span><span class="br0">(</span>ColorRGBA.<span class="me1">White</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span>al<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The result should look something like:
</p>

<p>
<a href="/resources/jme3-particles3.jpg" class="media" title="jme3:particles3.jpg"><img src="/resources/jme3-particles3.jpg" class="media" alt="" /></a>
</p>

<p>
Now lets set fire to the monkey! (No monkeys were harmed during the making of this particle system!).
</p>
<pre class="code java"><span class="co1">// Construct a new ParticleController       </span>
        ParticleController pCtrl <span class="sy0">=</span> <span class="kw1">new</span> ParticleController<span class="br0">(</span>
<span class="co1">// The name of the emitter</span>
                <span class="st0">"SimpleFire"</span>, 
<span class="co1">// Use a simple point mesh (the fastest but most limitted mesh type) with the specified</span>
<span class="co1">// image (from jME3-testdata). The image actually contains a 2x2 grid of sprites.</span>
                <span class="kw1">new</span> PointMesh<span class="br0">(</span>assetManager, <span class="st0">"Textures/flame.png"</span>, <span class="nu0">2</span>, <span class="nu0">2</span><span class="br0">)</span>,
<span class="co1">// Allow at most 1200 particles at any time, the particles are lasting longer this time</span>
<span class="co1">// so we need to allow more on screen at once                </span>
                <span class="nu0">1200</span>, 
<span class="co1">// Particles last for at least 4 seconds                </span>
                <span class="nu0">4</span>, 
<span class="co1">// And at most 5 seconds</span>
                <span class="nu0">5</span>,
<span class="co1">// A MeshSource scans a geometry and picks a random point on the surface of that</span>
<span class="co1">// geometry in order to emit the particle from it. The particle has an inital velocity</span>
<span class="co1">// of 1wu/s along the normal of the triangle from which it is emitted.</span>
                <span class="kw1">new</span> MeshSource<span class="br0">(</span>g<span class="br0">)</span>,
<span class="co1">// Emit particles at regular intervals, 10 particles every second</span>
                <span class="kw1">new</span> RegularEmission<span class="br0">(</span><span class="nu0">240</span><span class="br0">)</span>,
<span class="co1">// ** Influencers start here                </span>
<span class="co1">// Select a random sprite from the 4 available for each particle                </span>
                <span class="kw1">new</span> RandomSpriteInfluencer<span class="br0">(</span><span class="br0">)</span>,
<span class="co1">// Particles start off with a size of 0.1 units, end with a size of 0.15                </span>
                <span class="kw1">new</span> SizeInfluencer<span class="br0">(</span>0.1f, 0.15f<span class="br0">)</span>,
<span class="co1">// Particles have a constant speed of 0.25f, this will modify the original speed</span>
<span class="co1">// from the emitter and then allow the GravityInfluencer to change the direction</span>
<span class="co1">// of motion but constrain the speed</span>
                <span class="kw1">new</span> SpeedInfluencer<span class="br0">(</span>0.25f, 0.25f<span class="br0">)</span>,
<span class="co1">// Fade the paticles through a range of colours</span>
                <span class="kw1">new</span> MultiColorInfluencer<span class="br0">(</span>
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span><span class="nu0">0</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, 0.1f, <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span>,
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span>0.25f, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span>, 0.25f<span class="br0">)</span><span class="br0">)</span>,
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span>0.5f, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f, 1f, 1f, 0.25f<span class="br0">)</span><span class="br0">)</span>,
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span><span class="nu0">1</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span>1f,1f,1f,0f<span class="br0">)</span><span class="br0">)</span>
                <span class="br0">)</span>,
<span class="co1">// No matter what velocity particles started with they will start moving upwards.               </span>
                <span class="kw1">new</span> GravityInfluencer<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, 0.5f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Finally attach the geometry to the rootNode in order to start the particles running</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Again this is just a very simple example, much more sophisticated fire effects are possible with the use of the right textures and mixture of emitters and influencers. The result though should look something like this:
</p>

<p>
<a href="/lib/exe/fetch.php/jme3:contributions:youtube_w_zgjhz2au" class="media mediafile mf_ wikilink2" title="jme3:contributions:youtube_w_zgjhz2au">youtube_w_zgjhz2au</a>
</p>

</div>
<!-- EDIT8 SECTION "Using a mesh as the particle source" [12106-15746] -->
<h3 class="sectionedit9" id="meshes_and_weighted_meshes">Meshes and Weighted Meshes</h3>
<div class="level3">

<p>
The previous example uses a MeshSource, this picks a random triangle from the mesh without any regard given to the size of different triangles. This means areas with small triangles are actually more likely to emit particles than areas with large triangles. For most meshes this is not visible, however there is a WeightedMeshSource available if this should be a problem.
</p>

<p>
The WeightedMeshSource scans the mesh and works out a weight for each triangle based on its relative size, so that the result is an even spread of particles even with very large differences in triangle sizes. There are some limitations with this though:
</p>
<ol>
<li class="level1"><div class="li"> The WeightedMeshSource consumes more memory as it needs to remember the weights</div>
</li>
<li class="level1"><div class="li"> The WeightedMeshSource is slower as it needs to do more work to pick a triangle</div>
</li>
<li class="level1"><div class="li"> The WeightedMeshSource does not update automatically if the mesh changes, if triangles are added they will not emit, if triangles are removed it could cause a crash. If triangles change shape then the weights are not updated.</div>
</li>
</ol>

<p>
There is a method available to cause the weights to be recalculated which can be used if changing the mesh, but really if possible a non-weighted MeshSource should be used for dynamic meshes.
</p>

</div>
<!-- EDIT9 SECTION "Meshes and Weighted Meshes" [15747-17004] -->
<h3 class="sectionedit10" id="d_particles_-_templatemesh">3d Particles - TemplateMesh</h3>
<div class="level3">

<p>
The previous mesh examples all use simple 2d quads to display images. There is another mesh type though, the TemplateMesh, which allows fully featured 3d particles to be used.
</p>

<p>
</p><p></p><div class="noteclassic">
There is a rock texture available in the jME3 test data, or you can substitute any other suitable texture. The model for this example is: <a href="http://www.zero-separation.com/particles/FracturedCube.j3o" class="urlextern" title="http://www.zero-separation.com/particles/FracturedCube.j3o" rel="nofollow">FracturedCube.j3o</a>

</div>

<pre class="code java">    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        <span class="co1">// Since we actually use a full lit material for these particles we need</span>
        <span class="co1">// to add a light to the scene in order to see anything.</span>
        DirectionalLight dl <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        dl.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f,<span class="sy0">-</span>0.7f,<span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        dl.<span class="me1">setColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span>0.6f, 0.60f, 0.60f, 1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span>dl<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// A standard lit material is used, this rock texture was taking from the</span>
<span class="co1">// jme3 test data but you can easily substitute your own.</span>
        Material rock <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Light/Lighting.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        rock.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"DiffuseMap"</span>, assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Rock.PNG"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rock.<span class="me1">setFloat</span><span class="br0">(</span><span class="st0">"Shininess"</span>, 100f<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// A PointSource is actually a fully featured Spatial object, in this case</span>
<span class="co1">// we simply adjust its translation, but it can actually be attached to the</span>
<span class="co1">// scene graph and the source will automatically move as the Node to which</span>
<span class="co1">// it is attached is transformed.</span>
        PointSource source <span class="sy0">=</span> <span class="kw1">new</span> PointSource<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">5</span>,<span class="sy0">-</span><span class="nu0">5</span>,<span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">5</span>,<span class="nu0">5</span>,<span class="nu0">5</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        source.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">10</span>, <span class="sy0">-</span><span class="nu0">20</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// A TemplateMesh uses any number of standard meshes to be the template for</span>
<span class="co1">// each 3d particle. This model was generated simply by taking a cube in</span>
<span class="co1">// Blender and running a fracture script on it to generate 20 fragments.</span>
        Node n <span class="sy0">=</span> <span class="br0">(</span>Node<span class="br0">)</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/FracturedCube.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
        Mesh<span class="br0">[</span><span class="br0">]</span> templates <span class="sy0">=</span> <span class="kw1">new</span> Mesh<span class="br0">[</span>n.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="br0">]</span><span class="sy0">;</span>
        <span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
        <span class="kw1">for</span> <span class="br0">(</span>Spatial s<span class="sy0">:</span> n.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            Geometry g <span class="sy0">=</span> <span class="br0">(</span>Geometry<span class="br0">)</span><span class="br0">(</span><span class="br0">(</span>Node<span class="br0">)</span>s<span class="br0">)</span>.<span class="me1">getChild</span><span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
            templates<span class="br0">[</span>i<span class="sy0">++</span><span class="br0">]</span> <span class="sy0">=</span> g.<span class="me1">getMesh</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
 
<span class="co1">// Construct the new particle controller</span>
        ParticleController rockCtrl <span class="sy0">=</span> <span class="kw1">new</span> ParticleController<span class="br0">(</span>
                <span class="st0">"TemplateMesh"</span>, 
<span class="co1">// The TemplateMesh uses the rock material we created previously, the two boolean</span>
<span class="co1">// flags say that we are not interested in vertex colours but we do want the vertex</span>
<span class="co1">// normals. The array of meshes extracted from the model is then passed in to use</span>
<span class="co1">// as models for each particle.</span>
                <span class="kw1">new</span> TemplateMesh<span class="br0">(</span>rock, <span class="kw2">false</span>, <span class="kw2">true</span>, templates<span class="br0">)</span>, 
<span class="co1">// A maximum of 64 particles at once, each lasting for 5 to 5.5 seconds.                </span>
                <span class="nu0">64</span>, 
                <span class="nu0">5</span>, 
                5.5f,
<span class="co1">// Particles are emitted from the source that we created and positioned earlier                </span>
                source, 
<span class="co1">// Emit 8 particles per second                </span>
                <span class="kw1">new</span> RegularEmission<span class="br0">(</span><span class="nu0">8</span><span class="br0">)</span>,
<span class="co1">// The "sprites" in this case are the available templates. The TemplateMesh has</span>
<span class="co1">// one spriteColumn for each template it has been provided, so the standard</span>
<span class="co1">// RandomSpriteInfluencer just causes one to be picked at random each time a</span>
<span class="co1">// particle is emitted.</span>
                <span class="kw1">new</span> RandomSpriteInfluencer<span class="br0">(</span><span class="br0">)</span>,
<span class="co1">// Rocks fall.                </span>
                <span class="kw1">new</span> GravityInfluencer<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">4</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span>,
<span class="co1">// Rocks spin.</span>
                <span class="kw1">new</span> RotationInfluencer<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">2</span>, <span class="sy0">-</span><span class="nu0">2</span>, <span class="sy0">-</span><span class="nu0">2</span><span class="br0">)</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">2</span>, <span class="nu0">2</span>, <span class="nu0">2</span><span class="br0">)</span>, <span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>rockCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>        
    <span class="br0">}</span>        </pre>

<p>
The result should look like:
<a href="/lib/exe/fetch.php/jme3:contributions:youtube_a7y53uf8giw" class="media mediafile mf_ wikilink2" title="jme3:contributions:youtube_a7y53uf8giw">youtube_a7y53uf8giw</a>
</p>

<p>
Any number and mixture of models can be used, although as it is all a single mesh the same material must be used for all of them. It is recommended to keep a similar number of vertices for each of the models but that is not a strict requirement.
</p>

</div>
<!-- EDIT10 SECTION "3d Particles - TemplateMesh" [17005-20916] -->
<h3 class="sectionedit11" id="emitting_particles_from_particles">Emitting Particles from Particles</h3>
<div class="level3">

<p>
To add more dramatic effects sometimes you want to emit particles from particles, this could be done simply by attaching a MeshSource for the second controller to the mesh from the first controller. There are a number of limitations to this approach though, which will be demonstrated now:
</p>

<p>
Adding the following code:
</p>
<pre class="code java"> 
 
        ParticleController pCtrl <span class="sy0">=</span> <span class="kw1">new</span> ParticleController<span class="br0">(</span>
                <span class="st0">"TemplateFlames"</span>, 
                <span class="kw1">new</span> PointMesh<span class="br0">(</span>assetManager, <span class="st0">"Textures/flame.png"</span>, <span class="nu0">2</span>, <span class="nu0">2</span><span class="br0">)</span>,
                <span class="nu0">1300</span>, 
                <span class="nu0">3</span>, 
                <span class="nu0">4</span>, 
                <span class="kw1">new</span> MeshSource<span class="br0">(</span>rockCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>,
                <span class="kw1">new</span> RegularEmission<span class="br0">(</span><span class="nu0">320</span><span class="br0">)</span>, 
                <span class="kw1">new</span> SizeInfluencer<span class="br0">(</span>0.5f, <span class="nu0">2</span><span class="br0">)</span>,
                <span class="kw1">new</span> ColorInfluencer<span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">1</span>,0.1f, 1f<span class="br0">)</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span>,0.05f<span class="br0">)</span><span class="br0">)</span>,
                <span class="kw1">new</span> GravityInfluencer<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, 0.3f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span>,
                <span class="kw1">new</span> RandomImpulseInfluencer<span class="br0">(</span>
                    RandomImpulseInfluencer.<span class="me1">ImpulseApplicationTime</span>.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+initialize"><span class="kw3">INITIALIZE</span></a>, 
                    <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.5f, <span class="sy0">-</span>0.5f, <span class="sy0">-</span>0.5f<span class="br0">)</span>, 
                    <span class="kw1">new</span> Vector3f<span class="br0">(</span>0.5f, 0.5f, 0.5f<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 </pre>

<p>
Results in something that looks like this:
</p>

<p>
<a href="/lib/exe/fetch.php/jme3:contributions:youtube_wgr5rzf9apg" class="media mediafile mf_ wikilink2" title="jme3:contributions:youtube_wgr5rzf9apg">youtube_wgr5rzf9apg</a>
</p>

<p>
You can see that while dramatic the fire is left behind each particle, this is because although it is emitted from the face of the particle at its current position it has no knowledge of how that particle is moving.
</p>

<p>
To allow for this we also offer a different emitter, this allows one ParticleController to act as the source for another. The emitted particles are then able to start with the same velocity and rotation of the particle they are being emitted from and then move onwards from there as appropriate.
</p>

<p>
Leave everything else the same but change the MeshSource into
</p>
<pre class="code java">                <span class="kw1">new</span> ParticleParticleSource<span class="br0">(</span>rockCtrl<span class="br0">)</span>,</pre>

<p>
You can see that this gives much better results:
<a href="/lib/exe/fetch.php/jme3:contributions:youtube_2blbzvm0ezq" class="media mediafile mf_ wikilink2" title="jme3:contributions:youtube_2blbzvm0ezq">youtube_2blbzvm0ezq</a>
</p>

<p>
There is a lot of falling rocks and fire here, but not much in the way of smoke. That could be added using a multi-colour emitter as previously, but the standard particle material is additive. That means it can only make colours brighter, never darker. For smoke it should be able to darken as well as lighten.
</p>

<p>
To add smoke we can add a third emitter after the other two:
</p>
<pre class="code java"><span class="co1">// Construct a new material for the smoke based off the default particle material</span>
        Material smokeMat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>
               assetManager, <span class="st0">"Common/MatDefs/Misc/Particle.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// The Smoke.png texture can be found in the jme3 test data</span>
        smokeMat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"Texture"</span>,
            assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Smoke.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// Set the blend mode to Alpha rather than AlphaAdditive so that dark smoke</span>
<span class="co1">// can darken the scene behind it</span>
        smokeMat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setBlendMode</span><span class="br0">(</span>RenderState.<span class="me1">BlendMode</span>.<span class="me1">Alpha</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// For point sprite meshes this parameter must be set</span>
        smokeMat.<span class="me1">setBoolean</span><span class="br0">(</span><span class="st0">"PointSprite"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Construct the new particle controller</span>
        pCtrl <span class="sy0">=</span> <span class="kw1">new</span> ParticleController<span class="br0">(</span>
                <span class="st0">"TemplateSmoke"</span>, 
<span class="co1">// The Smoke.png texture contains 15 sprites, if you use a different texture adjust</span>
<span class="co1">// these parameters accordingly.</span>
                <span class="kw1">new</span> PointMesh<span class="br0">(</span>smokeMat, <span class="nu0">15</span>, <span class="nu0">1</span><span class="br0">)</span>,
                <span class="nu0">800</span>, 
                <span class="nu0">4</span>, 
                <span class="nu0">5</span>, 
                <span class="kw1">new</span> ParticleParticleSource<span class="br0">(</span>rockCtrl<span class="br0">)</span>, 
                <span class="kw1">new</span> RegularEmission<span class="br0">(</span><span class="nu0">180</span><span class="br0">)</span>, 
                <span class="kw1">new</span> SizeInfluencer<span class="br0">(</span>1f, 2.5f<span class="br0">)</span>,
                <span class="kw1">new</span> MultiColorInfluencer<span class="br0">(</span>
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span><span class="nu0">0</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span>,
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span>0.5f, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span>, 0.5f<span class="br0">)</span><span class="br0">)</span>,
                    <span class="kw1">new</span> MultiColorInfluencer.<span class="me1">Stage</span><span class="br0">(</span><span class="nu0">1</span>, <span class="kw1">new</span> ColorRGBA<span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span>,
                <span class="kw1">new</span> GravityInfluencer<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, 0.75f, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span>,
                <span class="kw1">new</span> RandomImpulseInfluencer<span class="br0">(</span>
                    RandomImpulseInfluencer.<span class="me1">ImpulseApplicationTime</span>.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+initialize"><span class="kw3">INITIALIZE</span></a>, 
                    <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.5f, <span class="sy0">-</span>0.5f, <span class="sy0">-</span>0.5f<span class="br0">)</span>, 
                    <span class="kw1">new</span> Vector3f<span class="br0">(</span>0.5f, 0.5f, 0.5f<span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pCtrl.<span class="me1">getGeometry</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>      </pre>

<p>
The results look something like:
<a href="/lib/exe/fetch.php/jme3:contributions:youtube_01qcbgbvf-c" class="media mediafile mf_ wikilink2" title="jme3:contributions:youtube_01qcbgbvf-c">youtube_01qcbgbvf-c</a>
</p>

<p>
To complete the effect one final line of code adds a skybox (using another texture that can be find in the test data):
</p>
<pre class="code java">        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>SkyFactory.<span class="me1">createSky</span><span class="br0">(</span>assetManager, <span class="st0">"Textures/BrightSky.dds"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now we have the final effect which looks like:
</p>

<p>
<a href="/lib/exe/fetch.php/jme3:contributions:youtube_udewajw4lxu" class="media mediafile mf_ wikilink2" title="jme3:contributions:youtube_udewajw4lxu">youtube_udewajw4lxu</a>
</p>

</div>
<!-- EDIT11 SECTION "Emitting Particles from Particles" [20917-] -->
