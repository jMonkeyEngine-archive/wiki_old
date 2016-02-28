---
title: jMonkeyEngine 3 Tutorial (11) - Hello Audio
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_11_-_hello_audio">jMonkeyEngine 3 Tutorial (11) - Hello Audio</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">Hello Terrain</a>, Next: <a href="/jme3/beginner/hello_effects.html" class="wikilink1" title="jme3:beginner:hello_effects">Hello Effects</a>
</p>

<p>
This tutorial explains how to add 3D sound to a game, and how to make sounds play together with events, such as clicking. You learn how to use an Audio Listener and Audio Nodes. You also make use of an Action Listener and a MouseButtonTrigger from the previous <a href="/jme3/beginner/hello_input_system.html" class="wikilink1" title="jme3:beginner:hello_input_system">Hello Input</a> tutorial to make a mouse click trigger a gun shot sound.
</p>

<p>
</p><p></p><div class="notetip">To use the example assets in a new jMonkeyEngine SDK project, right-click your project, select “Properties”, go to “Libraries”, press “Add Library” and add the “jme3-test-data” library.
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (11) - Hello Audio" [1-683] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.audio.AudioNode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.MouseInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.MouseButtonTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 11 - playing 3D audio. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloAudio <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
  <span class="kw1">private</span> AudioNode audio_gun<span class="sy0">;</span>
  <span class="kw1">private</span> AudioNode audio_nature<span class="sy0">;</span>
  <span class="kw1">private</span> Geometry player<span class="sy0">;</span>
 
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    HelloAudio app <span class="sy0">=</span> <span class="kw1">new</span> HelloAudio<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span><span class="nu0">40</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** just a blue box floating in space */</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box1 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    player <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Player"</span>, box1<span class="br0">)</span><span class="sy0">;</span>
    Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,<span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
    player.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** custom init methods, see below */</span>
    initKeys<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    initAudio<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** We create two audio nodes. */</span>
  <span class="kw1">private</span> <span class="kw4">void</span> initAudio<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="coMULTI">/* gun shot sound is to be triggered by a mouse click. */</span>
    audio_gun <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/Effects/Gun.wav"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    audio_gun.<span class="me1">setPositional</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    audio_gun.<span class="me1">setLooping</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    audio_gun.<span class="me1">setVolume</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>audio_gun<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="coMULTI">/* nature sound - keeps playing in a loop. */</span>
    audio_nature <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/Environment/Ocean Waves.ogg"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    audio_nature.<span class="me1">setLooping</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// activate continuous playing</span>
    audio_nature.<span class="me1">setPositional</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>   
    audio_nature.<span class="me1">setVolume</span><span class="br0">(</span><span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>audio_nature<span class="br0">)</span><span class="sy0">;</span>
    audio_nature.<span class="me1">play</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// play continuously!</span>
  <span class="br0">}</span>
 
  <span class="co3">/** Declaring "Shoot" action, mapping it to a trigger (mouse left click). */</span>
  <span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Shoot"</span>, <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Shoot"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/** Defining the "Shoot" action: Play a gun sound. */</span>
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Shoot"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        audio_gun.<span class="me1">playInstance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// play each instance once!</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span>
 
  <span class="co3">/** Move the listener with the a camera - for 3D audio. */</span>
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    listener.<span class="me1">setLocation</span><span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    listener.<span class="me1">setRotation</span><span class="br0">(</span>cam.<span class="me1">getRotation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
When you run the sample, you should see a blue cube. You should hear a nature-like ambient sound. When you click, you hear a loud shot.
</p>

</div>
<!-- EDIT2 SECTION "Sample Code" [684-3501] -->
<h2 class="sectionedit3" id="understanding_the_code_sample">Understanding the Code Sample</h2>
<div class="level2">

<p>
In the <code>initSimpleApp()</code> method, you create a simple blue cube geometry called <code>player</code> and attach it to the scene – this is just arbitrary sample content, so you see something when running the audio sample.
</p>

<p>
Let's have a closer look at <code>initAudio()</code> to learn how to use <code>AudioNode</code>s.
</p>

</div>
<!-- EDIT3 SECTION "Understanding the Code Sample" [3502-3839] -->
<h2 class="sectionedit4" id="audionodes">AudioNodes</h2>
<div class="level2">

<p>
Adding sound to your game is quite simple: Save your audio files into your <code>assets/Sound</code> directory. JME3 supports both Ogg Vorbis (.ogg) and Wave (.wav) file formats.
</p>

<p>
For each sound, you create an AudioNode. You can use an AudioNode like any node in the JME scene graph, e.g. attach it to other Nodes. You create one node for a gunshot sound, and one node for a nature sound.
</p>
<pre class="code java">  <span class="kw1">private</span> AudioNode audio_gun<span class="sy0">;</span>
  <span class="kw1">private</span> AudioNode audio_nature<span class="sy0">;</span></pre>

<p>
Look at the custom <code>initAudio()</code> method: Here you initialize the sound objects and set their parameters.
</p>
<pre class="code Java">audio_gun <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/Effects/Gun.wav"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    ...
<span class="me1">audio_nature</span> <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/Environment/Nature.ogg"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
These two lines create new sound nodes from the given audio files in the AssetManager. The <code>false</code> flag means that you want to buffer these sounds before playing. (If you set this flag to true, the sound will be streamed, which makes sense for really long sounds.)
</p>

<p>
You want the gunshot sound to play <em>once</em> (you don't want it to loop). You also specify its volume as gain factor (at 0, sound is muted, at 2, it is twice as loud, etc.).
</p>
<pre class="code java">    audio_gun.<span class="me1">setPositional</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    audio_gun.<span class="me1">setLooping</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    audio_gun.<span class="me1">setVolume</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>audio_gun<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="noteimportant">Note that setPositional(false) is pretty important when you use stereo sounds. Positional sounds must always be mono audio files, otherwise the engine will remind it to you with a crash.
</div>


<p>
The nature sound is different: You want it to loop <em>continuously</em> as background sound. This is why you set looping to true, and immediately call the play() method on the node. You also choose to set its volume to 3.
</p>
<pre class="code java">    audio_nature.<span class="me1">setLooping</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// activate continuous playing</span>
    ...
    <span class="me1">audio_nature</span>.<span class="me1">setVolume</span><span class="br0">(</span><span class="nu0">3</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>audio_nature<span class="br0">)</span><span class="sy0">;</span>
    audio_nature.<span class="me1">play</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// play continuously!</span>
  <span class="br0">}</span></pre>

<p>
Here you make audio_nature a positional sound that comes from a certain place. For that you give the node an explicit translation, in this example, you choose Vector3f.ZERO (which stands for the coordinates <code>0.0f,0.0f,0.0f</code>, the center of the scene.) Since jME supports 3D audio, you are now able to hear this sound coming from this particular location. Making the sound positional is optional. If you don't use these lines, the ambient sound comes from every direction.
</p>
<pre class="code java">    ...
    <span class="me1">audio_nature</span>.<span class="me1">setPositional</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
    audio_nature.<span class="me1">setLocalTranslation</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    ...</pre>

<p>
<strong>Tip:</strong> Attach AudioNodes into the scene graph like all nodes, to make certain moving nodes stay up-to-date. If you don't attach them, they are still audible and you don't get an error message but 3D sound will not work as expected. AudioNodes can be attached directly to the root node or they can be attached inside a node that is moving through the scene and both the AudioNode and the 3d position of the sound it is generating will move accordingly.
</p>

<p>
<strong>Tip:</strong> playInstance always plays the sound from the position of the AudioNode so multiple gunshots from one gun (for example) can be generated this way, however if multiple guns are firing at once then an AudioNode is needed for each one.
</p>

</div>
<!-- EDIT4 SECTION "AudioNodes" [3840-7174] -->
<h2 class="sectionedit5" id="triggering_sound">Triggering Sound</h2>
<div class="level2">

<p>
Let's have a closer look at <code>initKeys()</code>: As you learned in previous tutorials, you use the <code>inputManager</code> to respond to user input. Here you add a mapping for a left mouse button click, and name this new action <code>Shoot</code>.
</p>
<pre class="code java">  <span class="co3">/** Declaring "Shoot" action, mapping it to a trigger (mouse left click). */</span>
  <span class="kw1">private</span> <span class="kw4">void</span> initKeys<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Shoot"</span>, <span class="kw1">new</span> MouseButtonTrigger<span class="br0">(</span>MouseInput.<span class="me1">BUTTON_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Shoot"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

<p>
Setting up the ActionListener should also be familiar from previous tutorials. You declare that, when the trigger (the mouse button) is pressed and released, you want to play a gun sound.
</p>
<pre class="code java">  <span class="co3">/** Defining the "Shoot" action: Play a gun sound. */</span>
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Shoot"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        audio_gun.<span class="me1">playInstance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// play each instance once!</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

<p>
Since you want to be able to shoot fast repeatedly, so you do not want to wait for the previous gunshot sound to end before the next one can start. This is why you play this sound using the <code>playInstance()</code> method. This means that every click starts a new instance of the sound, so two instances can overlap. You set this sound not to loop, so each instance only plays once. As you would expect it of a gunshot.
</p>

</div>
<!-- EDIT5 SECTION "Triggering Sound" [7175-8664] -->
<h2 class="sectionedit6" id="ambient_or_situational">Ambient or Situational?</h2>
<div class="level2">

<p>
The two sounds are two different use cases:
</p>
<ul>
<li class="level1"><div class="li"> A gunshot is situational. You want to play it only once, right when it is triggered.</div>
<ul>
<li class="level2"><div class="li"> This is why you <code>setLooping(false)</code>.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> The nature sound is an ambient, background noise. You want it to start playing from the start, as long as the game runs.</div>
<ul>
<li class="level2"><div class="li"> This is why you <code>setLooping(true)</code>.</div>
</li>
</ul>
</li>
</ul>

<p>
Now every sound knows whether it should loop or not. 
</p>

<p>
Apart from the looping boolean, another difference is where <code>play().playInstance()</code> is called on those nodes:
</p>
<ul>
<li class="level1"><div class="li"> You start playing the background nature sound right after you have created it, in the initAudio() method.<pre class="code java">    audio_nature.<span class="me1">play</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// play continuously!</span></pre>
</div>
</li>
<li class="level1"><div class="li"> The gunshot sound, however, is triggered situationally, once, only as part of the <code>Shoot</code> input action that you defined in the ActionListener.<pre class="code java">  <span class="co3">/** Defining the "Shoot" action: Play a gun sound. */</span>
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Shoot"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span>
        audio_gun.<span class="me1">playInstance</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// play each instance once!</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Ambient or Situational?" [8665-9895] -->
<h2 class="sectionedit7" id="buffered_or_streaming">Buffered or Streaming?</h2>
<div class="level2">

<p>
The Boolean in the AudioNode constructor defines whether the audio is buffered (false) or streamed (true). For example:
</p>
<pre class="code java">audio_gunshot <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/Effects/Gun.wav"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// buffered</span>
...
<span class="me1">audio_nature</span> <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/Environment/Nature.ogg"</span>, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// streamed </span></pre>

<p>
Typically, you stream long sounds, and buffer short sounds.
</p>

<p>
Note that streamed sounds can not loop (i.e. setLooping will not work as you expect). Check the getStatus on the node and if it has stopped recreate the node.
</p>

</div>
<!-- EDIT7 SECTION "Buffered or Streaming?" [9896-10478] -->
<h2 class="sectionedit8" id="play_or_playinstance">Play() or PlayInstance()?</h2>
<div class="level2">
<div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">audio.play()</th><th class="col1">audio.playInstance()</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Plays buffered sounds.</td><td class="col1">Plays buffered sounds. </td>
	</tr>
	<tr class="row2">
		<td class="col0">Plays streamed sounds.</td><td class="col1">Cannot play streamed sounds.</td>
	</tr>
	<tr class="row3">
		<td class="col0">The same sound cannot play twice at the same time.</td><td class="col1">The same sounds can play multiple times and overlap.</td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [10518-10762] -->
</div>
<!-- EDIT8 SECTION "Play() or PlayInstance()?" [10479-10763] -->
<h2 class="sectionedit10" id="your_ear_in_the_scene">Your Ear in the Scene</h2>
<div class="level2">

<p>
To create a 3D audio effect, JME3 needs to know the position of the sound source, and the position of the ears of the player. The ears are represented by an 3D Audio Listener object. The <code>listener</code> object is a default object in a SimpleApplication.
</p>

<p>
In order to make the most of the 3D audio effect, you must use the <code>simpleUpdate()</code> method to move and rotate the listener (the player's ears) together with the camera (the player's eyes).
</p>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    listener.<span class="me1">setLocation</span><span class="br0">(</span>cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    listener.<span class="me1">setRotation</span><span class="br0">(</span>cam.<span class="me1">getRotation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

<p>
If you don't do that, the results of 3D audio will be quite random.
</p>

</div>
<!-- EDIT10 SECTION "Your Ear in the Scene" [10764-11466] -->
<h2 class="sectionedit11" id="global_directional_positional">Global, Directional, Positional?</h2>
<div class="level2">

<p>
In this example, you defined the nature sound as coming from a certain position, but not the gunshot sound. This means your gunshot is global and can be heard everywhere with the same volume. JME3 also supports directional sounds which you can only hear from a certain direction. 
</p>

<p>
It makes equal sense to make the gunshot positional, and let the ambient sound come from every direction. How do you decide which type of 3D sound to use from case to case?
</p>
<ul>
<li class="level1"><div class="li"> In a game with moving enemies you may want to make the gun shot or footsteps positional sounds. In these cases you must move the AudioNode to the location of the enemy before <code>playInstance()</code>ing it. This way a player with stereo speakers hears from which direction the enemy is coming.</div>
</li>
<li class="level1"><div class="li"> Similarly, you may have game levels where you want one background sound to play globally. In this case, you would make the AudioNode neither positional nor directional (set both to false).</div>
</li>
<li class="level1"><div class="li"> If you want sound to be “absorbed by the walls” and only broadcast in one direction, you would make this AudioNode directional. This tutorial does not discuss directional sounds, you can read about <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">Advanced Audio</a> here.</div>
</li>
</ul>

<p>
In short, you must choose in every situation whether it makes sense for a sound to be global, directional, or positional.
</p>

</div>
<!-- EDIT11 SECTION "Global, Directional, Positional?" [11467-12823] -->
<h2 class="sectionedit12" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You now know how to add the two most common types of sound to your game: Global sounds and positional sounds. You can play sounds in two ways: Either continuously in a loop, or situationally just once. You know the difference between buffering short sounds and streaming long sounds. You know the difference between playing overlapping sound instances, and playing unique sounds that cannot overlap with themselves. You also learned to use sound files that are in either .ogg or .wav format.
</p>

<p>
<strong>Tip:</strong> JME's Audio implementation also supports more advanced effects such as reverberation and Doppler effect. Use these “pro” features to make audio sound different depending on whether it's in the hallway, in a cave, outdoors, or in a carpeted room. Find out more about environmental effects from the sample code included in the jme3test directory and from the advanced <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">Audio</a> docs.
</p>

<p>
Want some fire and explosions to go with your sounds? Read on to learn more about <a href="/jme3/beginner/hello_effects.html" class="wikilink1" title="jme3:beginner:hello_effects">effects</a>.
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li">  <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">Audio</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/sound.html" class="wikilink1" title="tag:sound" rel="tag">sound</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>
</span></div>

</div>
<!-- EDIT12 SECTION "Conclusion" [12824-] -->
