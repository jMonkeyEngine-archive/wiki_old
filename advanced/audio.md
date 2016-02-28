---
title: Audio in jME3
---
<h1 class="sectionedit1" id="audio_in_jme3">Audio in jME3</h1>
<div class="level1">

<p>
Place audio files in the <code>assets/Sound/</code> directory of your project. jME3 supports Ogg Vorbis audio compression (.ogg) and uncompressed PCM Wave (.wav) formats. You can use for example <a href="http://audacity.sourceforge.net/" class="urlextern" title="http://audacity.sourceforge.net/" rel="nofollow">Audacity</a> to convert from other formats.
</p>

</div>
<!-- EDIT1 SECTION "Audio in jME3" [1-293] -->
<h2 class="sectionedit2" id="audio_terminology">Audio Terminology</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <strong>Streaming:</strong> There are two ways to load audio data: Short audio files are to be stored entirely in memory (prebuffered), while long audio files, such as music, are streamed from the hard drive as it is played.</div>
</li>
<li class="level1"><div class="li"> <strong>Looping:</strong> You can play a sound either once and then stop, or repeatedly (continuously) in a loop. <br />
You cannot loop streamed sounds.</div>
</li>
<li class="level1"><div class="li"> <strong>Instance:</strong> If you play the same audio twice, the playing is queued up and jME plays one after the other. If you play instances of sounds, several instances of the same sound can play at the same time.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Audio Terminology" [294-891] -->
<h2 class="sectionedit3" id="creating_audio_nodesstreamed_or_buffered">Creating Audio Nodes: Streamed or Buffered</h2>
<div class="level2">

<p>
The main jME audio class to look at is <code>com.jme3.audio.AudioNode</code>. When creating a new audio node you need to declare whether how you want to load this sound:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Buffered:</strong> By default, a new audio node is buffered. This means jME3 loads the whole file into memory before playing. Use this for short sounds. You create a buffered sound  by setting the boolean to false, or using no boolean at all: <pre class="code java">AudioNode boom <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/boom.wav"</span><span class="br0">)</span><span class="sy0">;</span>
AudioNode boom <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/boom.wav"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> <strong>Streamed:</strong> If it is a long file such as music or a dialog, you stream the audio. Streaming means, you load and play in parallel until the sound is done. You cannot loop streams. You create a streamed sound by setting the boolean to true:<pre class="code java">AudioNode music <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/music.wav"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Creating Audio Nodes: Streamed or Buffered" [892-1839] -->
<h2 class="sectionedit4" id="getting_audionode_properties">Getting AudioNode Properties</h2>
<div class="level2">
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AudioNode Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getStatus()</td><td class="col1">Returns either AudioSource.Status.Playing, AudioSource.Status.Stopped, or AudioSource.Status.Paused. </td>
	</tr>
	<tr class="row2">
		<td class="col0">getVolume()</td><td class="col1">Returns the volume. </td>
	</tr>
	<tr class="row3">
		<td class="col0">getPitch()</td><td class="col1">Returns the pitch. </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [1882-2090] -->
<p>
Note: There are other obvious getters to poll the status of all corresponding setters listed here.
</p>

</div>
<!-- EDIT4 SECTION "Getting AudioNode Properties" [1840-2192] -->
<h2 class="sectionedit6" id="setting_audionode_properties">Setting AudioNode Properties</h2>
<div class="level2">
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AudioNode Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setTimeOffset(0.5f)</td><td class="col1">Play the sound starting at a 0.5 second offset from the beginning. Default is 0.</td>
	</tr>
	<tr class="row2">
		<td class="col0">setPitch(1)</td><td class="col1">Makes the sound play in a higher or lower pitch. Default is 1. 2 is twice as high, .5f is half as high. </td>
	</tr>
	<tr class="row3">
		<td class="col0">setVolume(1)</td><td class="col1">Sets the volume gain. 1 is the default volume, 2 is twice as loud, etc. 0 is silent/mute. </td>
	</tr>
	<tr class="row4">
		<td class="col0">setRefDistance(50f)</td><td class="col1">The reference distance controls how far a sound can still be heard at 50% of its original volume (<em>this is assuming an exponential fall-off!</em>). A sound with a high RefDist can be heard loud over wide distances; a sound with a low refDist can only be heard when the listener is close by. Default is 10 world units.</td>
	</tr>
	<tr class="row5">
		<td class="col0">setMaxDistance(100f)</td><td class="col1"> The 'maximum attenuation distance' specifies how far from the source the sound stops growing more quiet (sounds in nature don't do that). Set this to a smaller value to keep the sound loud even at a distance; set this to higher value to let the sound fade out quickly. Default is 20 world units.</td>
	</tr>
	<tr class="row6">
		<td class="col0">setLooping(false)</td><td class="col1">Configures the sound so that, if it is played, it plays once and stops. No looping is the default.</td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [2235-3364] -->
</div>
<!-- EDIT6 SECTION "Setting AudioNode Properties" [2193-3365] -->
<h3 class="sectionedit8" id="looping_ambient_sounds">Looping &amp; Ambient Sounds</h3>
<div class="level3">
<div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AudioNode Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setPositional(false) <br />
setDirectional(false)</td><td class="col1">All 3D effects switched off. This sound is global and plays in headspace (it appears to come from everywhere). Good for environmental ambient sounds and background music.</td>
	</tr>
	<tr class="row2">
		<td class="col0">setLooping(true)</td><td class="col1">Configures the sound to be a loop: After the sound plays, it repeats from the beginning, until you call stop() or pause(). Good for music and ambient background noises. <br />
<strong>Looping does not work on streamed sounds.</strong> </td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [3402-3883] -->
</div>
<!-- EDIT8 SECTION "Looping & Ambient Sounds" [3366-3884] -->
<h3 class="sectionedit10" id="positional_3d_sounds">Positional 3D Sounds</h3>
<div class="level3">
<div class="table sectionedit11"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AudioNode Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setPositional(true) <br />
setLocalTranslation(…)</td><td class="col1">Activates 3D audio: The sound appears to come from a certain position, where it is loudest. Position the AudioNode in the 3D scene, or move it with mobile players or NPCs.</td>
	</tr>
	<tr class="row2">
		<td class="col0">setReverbEnabled(true)</td><td class="col1">Reverb is a 3D echo effect that only makes sense with positional AudioNodes. Use Audio Environments to make scenes sound as if they were “outdoors”, or “indoors” in a large or small room, etc. The reverb effect is defined by the <code>com.jme3.audio.Environment</code> that the <code>audioRenderer</code> is in. See “Setting Audio Environment Properties” below. </td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [3917-4533] -->
<p>
</p><p></p><div class="noteimportant">Positional 3D sounds require an <code>AudioListener</code> object in the scene (representing the player's ears).
</div>


</div>
<!-- EDIT10 SECTION "Positional 3D Sounds" [3885-4662] -->
<h3 class="sectionedit12" id="directional_3d_sounds">Directional 3D Sounds</h3>
<div class="level3">
<div class="table sectionedit13"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AudioNode Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setDirectional(true) <br />
setDirection(…) </td><td class="col1">Activates 3D audio: This sound can only be heard from a certain direction. Specify the direction and angle in the 3D scene if you have setDirectional() true. Use this to restrict noises that should not be heard, for example, through a wall.</td>
	</tr>
	<tr class="row2">
		<td class="col0">setInnerAngle() <br />
setOuterAngle()</td><td class="col1">Set the angle in degrees for the directional audio. The angle is relative to the direction. Note: By default, both angles are 360° and the sound can be heard from all directions!</td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [4696-5223] -->
<p>
</p><p></p><div class="noteimportant">Directional 3D sounds require an AudioListener object in the scene (representing the player's ears). 
</div>


</div>
<!-- EDIT12 SECTION "Directional 3D Sounds" [4663-5350] -->
<h2 class="sectionedit14" id="play_pause_stop">Play, Pause, Stop</h2>
<div class="level2">

<p>
You play, pause, and stop a node called myAudioNode by using the respective of the following three methods:
</p>
<pre class="code java">myAudioNode.<span class="me1">play</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">myAudioNode.<span class="me1">pause</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">myAudioNode.<span class="me1">stop</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Note:</strong> Whether an Audio Node plays continuously or only once, depends on the Loop properties you have set above!
</p>

<p>
You can also start playing instances of an AudioNode. Use the <code>playInstance()</code> method if you need to play the same AudioNode multiple times, possibly simulatenously. Note that changes to the parameters of the original AudioNode do not affect the instances that are already playing!
</p>
<pre class="code java">myAudioNode.<span class="me1">playInstance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT14 SECTION "Play, Pause, Stop" [5351-6055] -->
<h2 class="sectionedit15" id="the_audio_listener">The Audio Listener</h2>
<div class="level2">

<p>
The default AudioListener object <code>listener</code> in <code>SimpleApplication</code> is the user's ear in the scene. If you use 3D audio (positional or directional sounds), you must move the AudioListener with the player: For example, for a first-person player, you move the listener with the camera. For a third-person player, you move the listener with the player avatar Geometry.
</p>
<pre class="code java">  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// first-person: keep the audio listener moving with the camera</span>
    listener.<span class="me1">setLocation</span><span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    listener.<span class="me1">setRotation</span><span class="br0">(</span>cam.<span class="me1">getRotation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT15 SECTION "The Audio Listener" [6056-6692] -->
<h2 class="sectionedit16" id="setting_audio_environment_properties">Setting Audio Environment Properties</h2>
<div class="level2">

<p>
Optionally, You can choose from the following environmental presets from <code>com.jme3.audio.Environment</code>. This presets influence subtle echo effects (reverb) that evoke associations of different environments in your users. That is, it makes you scene sound “indoors” or “outdoors” etc. You use Audio Environments together with <code>setReverbEnabled(true)</code> on positional AudioNodes (see above).
</p>
<div class="table sectionedit17"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Environment</th><th class="col1">density</th><th class="col2">diffusion</th><th class="col3">gain</th><th class="col4">gainHf</th><th class="col5">decayTime</th><th class="col6">decayHf</th><th class="col7">reflGain</th><th class="col8">reflDelay</th><th class="col9">lateGain</th><th class="col10">lateDelay</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign">Garage      </td><td class="col1">1.00f</td><td class="col2">1.0f</td><td class="col3">1.0f</td><td class="col4">1.00f</td><td class="col5">0.90f</td><td class="col6">0.5f</td><td class="col7">0.751f</td><td class="col8">0.0039f</td><td class="col9">0.661f</td><td class="col10">0.0137f</td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign">Dungeon     </td><td class="col1">0.75f</td><td class="col2">1.0f</td><td class="col3">1.0f</td><td class="col4">0.75f</td><td class="col5">1.60f</td><td class="col6">1.0f</td><td class="col7">0.950f</td><td class="col8">0.0026f</td><td class="col9">0.930f</td><td class="col10">0.0103f</td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign">Cavern      </td><td class="col1">0.50f</td><td class="col2">1.0f</td><td class="col3">1.0f</td><td class="col4">0.50f</td><td class="col5">2.25f</td><td class="col6">1.0f</td><td class="col7">0.908f</td><td class="col8">0.0103f</td><td class="col9">0.930f</td><td class="col10">0.0410f</td>
	</tr>
	<tr class="row4">
		<td class="col0">AcousticLab </td><td class="col1">0.50f</td><td class="col2">1.0f</td><td class="col3">1.0f</td><td class="col4">1.00f</td><td class="col5">0.28f</td><td class="col6">1.0f</td><td class="col7">0.870f</td><td class="col8">0.0020f</td><td class="col9">0.810f</td><td class="col10">0.0080f</td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign">Closet      </td><td class="col1">1.00f</td><td class="col2">1.0f</td><td class="col3">1.0f</td><td class="col4">1.00f</td><td class="col5">0.15f</td><td class="col6">1.0f</td><td class="col7">0.600f</td><td class="col8">0.0025f</td><td class="col9">0.500f</td><td class="col10">0.0006f</td>
	</tr>
</table></div>
<!-- EDIT17 TABLE [7135-7624] --><ol>
<li class="level1"><div class="li"> Activate a Environment preset</div>
<ul>
<li class="level2"><div class="li"> Either use a default, e.g. make you scene sounds like a dungeon environment: <pre class="code java">audioRenderer.<span class="me1">setEnvironment</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+environment"><span class="kw3">Environment</span></a><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+environment"><span class="kw3">Environment</span></a>.<span class="me1">Dungeon</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level2"><div class="li"> Or activate <a href="/jme3/advanced/audio_environment_presets.html" class="wikilink1" title="jme3:advanced:audio_environment_presets">custom environment settings</a> in the Environment constructor:<pre class="code java">audioRenderer.<span class="me1">setEnvironment</span><span class="br0">(</span>
        <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+environment"><span class="kw3">Environment</span></a><span class="br0">(</span> density, diffusion, gain, gainHf, decayTime, decayHf,
                reflGain, reflDelay, lateGain, lateDelay <span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Activate 3D audio for certain sounds: <pre class="code java">footstepsAudio.<span class="me1">setPositional</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
footstepsAudio.<span class="me1">setReverbEnabled</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
</p><p></p><div class="notetip">A sound engineer can create a custom <code>com.​jme3.​audio.Environment</code> object and specify custom environment values such as density, diffusion, gain, decay, delay… You can find many <a href="/jme3/advanced/audio_environment_presets.html" class="wikilink1" title="jme3:advanced:audio_environment_presets">examples of custom audio environment presets</a> here.
</div>


<p>
Advanced users find more info about OpenAL and its features here: <a href="http://web.archive.org/web/20130327063429/http://connect.creativelabs.com/openal/Documentation/OpenAL_Programmers_Guide.pdf" class="urlextern" title="http://web.archive.org/web/20130327063429/http://connect.creativelabs.com/openal/Documentation/OpenAL_Programmers_Guide.pdf" rel="nofollow">OpenAL 1.1 Specification</a>. 
</p>

<p>
</p><p></p><div class="noteimportant">It depends on the hardware whether audio effects are supported (if not, you get the message <code>OpenAL EFX not available! Audio effects won't work.</code>)
</div>

<div class="tags"><span>
	<a href="/tag/sound.html" class="wikilink1" title="tag:sound" rel="tag">sound</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/environment.html" class="wikilink1" title="tag:environment" rel="tag">environment</a>
</span></div>

</div>
<!-- EDIT16 SECTION "Setting Audio Environment Properties" [6693-] -->
