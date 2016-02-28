---
title: Capture Audio/Video to a File
---
<h1 class="sectionedit1" id="capture_audio_video_to_a_file">Capture Audio/Video to a File</h1>
<div class="level1">

<p>
So you've made your cool new JMonkeyEngine3 game and you want to
create a demo video to show off your hard work. Or maybe you want to
make a cutscene for your game using the physics and characters in the
game itself.  Screen capturing is the most straightforward way to do
this, but it can slow down your game and produce low-quality video and
audio as a result. A better way is to record video and audio directly
from the game while it is running using VideoRecorderAppState.
</p>

<p>
</p><p></p><div class="notetip">Combine this method with jMonkeyEngine's 
<a href="/jme3/advanced/cinematics.html" class="wikilink1" title="jme3:advanced:cinematics">Cinematics</a>
feature to record high-quality game trailers!
</div>


</div>
<!-- EDIT1 SECTION "Capture Audio/Video to a File" [1-658] -->
<h2 class="sectionedit2" id="simple_way">Simple Way</h2>
<div class="level2">

<p>
First off, if all you need is to record video at 30fps with no sound, then look
no further than jMonkeyEngine 3's built in <code>VideoRecorderAppState</code>
class.
</p>

<p>
Add the following code to your <code>simpleInitApp()</code> method. 
</p>
<pre class="code java">stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">new</span> VideoRecorderAppState<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//start recording</span></pre>

<p>
The game will run slow, but the recording will be in high-quality and
normal speed. Recording starts when the state is
attached, and ends when the application quits or the state is detached.
</p>

<p>
The video files will be stored in your <strong>user home directory</strong>. 
If you want to save to another path, specify a File object in the
VideoRecorderAppState constructor. 
</p>

<p>
That's all!
</p>

</div>
<!-- EDIT2 SECTION "Simple Way" [659-1362] -->
<h2 class="sectionedit3" id="advanced_way">Advanced Way</h2>
<div class="level2">

<p>
</p><p></p><div class="noteclassic">This way of A/V recording is still in development.  
It works for all of jMonkeyEngine's test cases. 
If you experience any problems or
if something isn't clear, please <a href="http://jmonkeyengine.org/members/bortreb/" class="urlextern" title="http://jmonkeyengine.org/members/bortreb/" rel="nofollow">let me know</a>. – bortreb
</div>


<p>
If you want to record audio as well, record at different framerates,
or record from multiple viewpoints at once, then there's a full
solution for doing this already made for you here:
</p>

<p>
<a href="http://www.aurellem.com/releases/jmeCapture-latest.zip" class="urlextern" title="http://www.aurellem.com/releases/jmeCapture-latest.zip" rel="nofollow">http://www.aurellem.com/releases/jmeCapture-latest.zip</a>
</p>

<p>
<a href="http://www.aurellem.com/releases/jmeCapture-latest.tar.bz2" class="urlextern" title="http://www.aurellem.com/releases/jmeCapture-latest.tar.bz2" rel="nofollow">http://www.aurellem.com/releases/jmeCapture-latest.tar.bz2</a>
</p>

<p>
Download the archive in your preferred format, extract,
add the jars to your project, and you are ready to go.
</p>

<p>
The javadoc is here:
<a href="http://www.aurellem.com/jmeCapture/docs/" class="urlextern" title="http://www.aurellem.com/jmeCapture/docs/" rel="nofollow">http://www.aurellem.com/jmeCapture/docs/</a>
</p>

<p>
To capture video and audio you use the
<code>com.aurellem.capture.Capture</code> class, which has two methods,
<code>captureAudio()</code> and <code>captureVideo()</code>, and the
<code>com.aurellem.capture.IsoTimer</code> class, which sets the audio and
video framerate.
</p>

<p>
The steps are:
</p>
<pre class="code java">yourApp.<span class="me1">setTimer</span><span class="br0">(</span><span class="kw1">new</span> IsoTimer<span class="br0">(</span>desiredFramesPerSecond<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This causes jMonkeyEngine to take as much time as it needs to fully
calculate every frame of the video and audio.  You will see your game
speed up and slow down depending on how computationally demanding your
game is, but the final recorded audio and video will be perfectly
sychronized and will run at exactly the fps which you specified.
</p>
<pre class="code java">captureVideo<span class="br0">(</span>yourApp, targetVideoFile<span class="br0">)</span><span class="sy0">;</span>
captureAudio<span class="br0">(</span>yourApp, targetAudioFile<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
These will cause the app to record audio and video when it is run.
Audio and video will stop being recorded when the app stops. Your
audio will be recorded as a 44,100 Hz linear PCM wav file, while the
video will be recorded according to the following rules:
</p>

<p>
1.) (Preferred) If you supply an empty directory as the file, then
the video will be saved as a sequence of .png files, one file per
frame.  The files start at 0000000.png and increment from there.
You can then combine the frames into your preferred
container/codec. If the directory is not empty, then writing
video frames to it will fail, and nothing will be written.
</p>

<p>
2.) If the filename ends in “.avi” then the frames will be encoded as
a RAW stream inside an AVI 1.0 container.  The resulting file
will be quite large and you will probably want to re-encode it to
your preferred container/codec format.  Be advised that some
video payers cannot process AVI with a RAW stream, and that AVI
1.0 files generated by this method that exceed 2.0GB are invalid
according to the AVI 1.0 <abbr title="specification">spec</abbr> (but many programs can still deal
with them.)  Thanks to 
<a href="http://www.randelshofer.ch/blog/2008/08/writing-avi-videos-in-pure-java/" class="urlextern" title="http://www.randelshofer.ch/blog/2008/08/writing-avi-videos-in-pure-java/" rel="nofollow">Werner Randelshofer</a>
for his excellent work which made the AVI file writer option possible.
</p>

<p>
3.) Any non-directory file ending in anything other than “.avi” will
be processed through Xuggle.  Xuggle provides the option to use
many codecs/containers, but you will have to install it on your
system yourself in order to use this option. Please visit
<a href="http://www.xuggle.com/" class="urlextern" title="http://www.xuggle.com/" rel="nofollow">http://www.xuggle.com/</a> to learn how to do this.
</p>

<p>
Note that you will not hear any sound if you choose to record sound to
a file.
</p>

</div>
<!-- EDIT3 SECTION "Advanced Way" [1363-4555] -->
<h3 class="sectionedit4" id="basic_example">Basic Example</h3>
<div class="level3">

<p>
Here is a complete example showing how to capture both audio and video
from one of jMonkeyEngine3's advanced demo applications.
</p>
<pre class="code java"><span class="kw1">import</span> <span class="co2">java.io.File</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.io.IOException</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">jme3test.water.TestPostWater</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.Capture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.IsoTimer</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
 
 
<span class="co3">/**
 * Demonstrates how to use basic Audio/Video capture with a
 * jMonkeyEngine application. You can use these techniques to make
 * high quality cutscenes or demo videos, even on very slow laptops.
 * 
 * @author Robert McIntyre
 */</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> Basic <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> ignore<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a><span class="br0">{</span>
	<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> video <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a>.<span class="me1">createTempFile</span><span class="br0">(</span><span class="st0">"JME-water-video"</span>, <span class="st0">".avi"</span><span class="br0">)</span><span class="sy0">;</span>
	<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> audio <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a>.<span class="me1">createTempFile</span><span class="br0">(</span><span class="st0">"JME-water-audio"</span>, <span class="st0">".wav"</span><span class="br0">)</span><span class="sy0">;</span>
 
	SimpleApplication app <span class="sy0">=</span> <span class="kw1">new</span> TestPostWater<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	app.<span class="me1">setTimer</span><span class="br0">(</span><span class="kw1">new</span> IsoTimer<span class="br0">(</span><span class="nu0">60</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	app.<span class="me1">setShowSettings</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
 
	Capture.<span class="me1">captureVideo</span><span class="br0">(</span>app, video<span class="br0">)</span><span class="sy0">;</span>
	Capture.<span class="me1">captureAudio</span><span class="br0">(</span>app, audio<span class="br0">)</span><span class="sy0">;</span>
 
	app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
	<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>video.<span class="me1">getCanonicalPath</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>audio.<span class="me1">getCanonicalPath</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "Basic Example" [4556-5688] -->
<h3 class="sectionedit5" id="how_it_works">How it works</h3>
<div class="level3">

<p>
A standard JME3 application that extends <code>SimpleApplication</code> or
<code>Application</code> tries as hard as it can to keep in sync with
<em>user-time</em>.  If a ball is rolling at 1 game-mile per game-hour in the
game, and you wait for one user-hour as measured by the clock on your
wall, then the ball should have traveled exactly one game-mile. In
order to keep sync with the real world, the game throttles its physics
engine and graphics display.  If the computations involved in running
the game are too intense, then the game will first skip frames, then
sacrifice physics accuracy.  If there are particuraly demanding
computations, then you may only get 1 fps, and the ball may tunnel
through the floor or obstacles due to inaccurate physics simulation,
but after the end of one user-hour, that ball will have traveled one
game-mile.
</p>

<p>
When we're recording video, we don't care if the game-time syncs with
user-time, but instead whether the time in the recorded video
(video-time) syncs with user-time. To continue the analogy, if we
recorded the ball rolling at 1 game-mile per game-hour and watched the
video later, we would want to see 30 fps video of the ball rolling at
1 video-mile per <em>user-hour</em>. It doesn't matter how much user-time it
took to simulate that hour of game-time to make the high-quality
recording.
</p>

<p>
The IsoTimer ignores real-time and always reports that the same amount
of time has passed every time it is called. That way, one can put code
to write each video/audio frame to a file without worrying about that
code itself slowing down the game to the point where the recording
would be useless.
</p>

</div>
<!-- EDIT5 SECTION "How it works" [5689-7327] -->
<h3 class="sectionedit6" id="advanced_example">Advanced Example</h3>
<div class="level3">

<p>
The package from aurellem.com was made for AI research and can do more
than just record a single stream of audio and video. You can use it
to:
</p>

<p>
1.) Create multiple independent listeners that each hear the world
from their own perspective.
</p>

<p>
2.) Process the sound data in any way you wish.
</p>

<p>
3.) Do the same for visual data.
</p>

<p>
Here is a more advanced example, which can also be found along with
other examples in the jmeCapture.jar file included in the
distribution.
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">com.aurellem.capture.examples</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">java.io.File</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.io.IOException</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.lang.reflect.Field</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.nio.ByteBuffer</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">javax.sound.sampled.AudioFormat</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">org.tritonus.share.sampled.FloatSampleTools</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.AurellemSystemDelegate</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.Capture</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.IsoTimer</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.audio.CompositeSoundProcessor</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.audio.MultiListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.audio.SoundProcessor</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.aurellem.capture.audio.WaveFileWriter</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.audio.AudioNode</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.audio.Listener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.cinematic.MotionPath</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.cinematic.events.AbstractCinematicEvent</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.cinematic.events.MotionTrack</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.FastMath</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Quaternion</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Sphere</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.system.AppSettings</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.system.JmeSystem</span><span class="sy0">;</span>
 
<span class="co3">/**
 * 
 * Demonstrates advanced use of the audio capture and recording
 * features.  Multiple perspectives of the same scene are
 * simultaneously rendered to different sound files.
 * 
 * A key limitation of the way multiple listeners are implemented is
 * that only 3D positioning effects are realized for listeners other
 * than the main LWJGL listener.  This means that audio effects such
 * as environment settings will *not* be heard on any auxiliary
 * listeners, though sound attenuation will work correctly.
 * 
 * Multiple listeners as realized here might be used to make AI
 * entities that can each hear the world from their own perspective.
 * 
 * @author Robert McIntyre
 */</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> Advanced <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
	<span class="co3">/**
	 * You will see three grey cubes, a blue sphere, and a path which
	 * circles each cube.  The blue sphere is generating a constant
	 * monotone sound as it moves along the track.  Each cube is
	 * listening for sound; when a cube hears sound whose intensity is
	 * greater than a certain threshold, it changes its color from
	 * grey to green.
	 * 
	 *  Each cube is also saving whatever it hears to a file.  The
	 *  scene from the perspective of the viewer is also saved to a
	 *  video file.  When you listen to each of the sound files
	 *  alongside the video, the sound will get louder when the sphere
	 *  approaches the cube that generated that sound file.  This
	 *  shows that each listener is hearing the world from its own
	 *  perspective.
	 * 
	 */</span>
	<span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
		Advanced app <span class="sy0">=</span> <span class="kw1">new</span> Advanced<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		AppSettings settings <span class="sy0">=</span> <span class="kw1">new</span> AppSettings<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
		settings.<span class="me1">setAudioRenderer</span><span class="br0">(</span>AurellemSystemDelegate.<span class="me1">SEND</span><span class="br0">)</span><span class="sy0">;</span>
		JmeSystem.<span class="me1">setSystemDelegate</span><span class="br0">(</span><span class="kw1">new</span> AurellemSystemDelegate<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		app.<span class="me1">setSettings</span><span class="br0">(</span>settings<span class="br0">)</span><span class="sy0">;</span>
		app.<span class="me1">setShowSettings</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
		app.<span class="me1">setPauseOnLostFocus</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
 
 
		<span class="kw1">try</span> <span class="br0">{</span>
			Capture.<span class="me1">captureVideo</span><span class="br0">(</span>app, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a>.<span class="me1">createTempFile</span><span class="br0">(</span><span class="st0">"advanced"</span>,<span class="st0">".avi"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
			Capture.<span class="me1">captureAudio</span><span class="br0">(</span>app, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a>.<span class="me1">createTempFile</span><span class="br0">(</span><span class="st0">"advanced"</span>, <span class="st0">".wav"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="br0">}</span>
		<span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> e<span class="br0">)</span> <span class="br0">{</span>e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span>
 
		app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
 
 
	<span class="kw1">private</span> Geometry bell<span class="sy0">;</span>
	<span class="kw1">private</span> Geometry ear1<span class="sy0">;</span>
	<span class="kw1">private</span> Geometry ear2<span class="sy0">;</span>
	<span class="kw1">private</span> Geometry ear3<span class="sy0">;</span>
	<span class="kw1">private</span> AudioNode music<span class="sy0">;</span>
	<span class="kw1">private</span> MotionTrack motionControl<span class="sy0">;</span>
	<span class="kw1">private</span> IsoTimer motionTimer <span class="sy0">=</span> <span class="kw1">new</span> IsoTimer<span class="br0">(</span><span class="nu0">60</span><span class="br0">)</span><span class="sy0">;</span>
 
	<span class="kw1">private</span> Geometry makeEar<span class="br0">(</span>Node root, Vector3f position<span class="br0">)</span><span class="br0">{</span>
		Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
		Geometry ear <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"ear"</span>, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>1.0f, 1.0f, 1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		ear.<span class="me1">setLocalTranslation</span><span class="br0">(</span>position<span class="br0">)</span><span class="sy0">;</span>
		mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
		ear.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
		root.<span class="me1">attachChild</span><span class="br0">(</span>ear<span class="br0">)</span><span class="sy0">;</span>
		<span class="kw1">return</span> ear<span class="sy0">;</span>
	<span class="br0">}</span> 
 
	<span class="kw1">private</span> Vector3f<span class="br0">[</span><span class="br0">]</span> path <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">[</span><span class="br0">]</span><span class="br0">{</span>
			<span class="co1">// loop 1</span>
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">10</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">2</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">14</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">6</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">26</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">6</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">14</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">6</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">26</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">6</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">20</span><span class="br0">)</span>,
			<span class="co1">// loop 2</span>
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">5</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">5</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">7</span>, <span class="nu0">0</span>, 1.5f<span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">14</span>, <span class="nu0">0</span>, <span class="nu0">2</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">20</span>, <span class="nu0">0</span>, <span class="nu0">6</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">26</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">20</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">6</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">14</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">20</span>, <span class="nu0">0</span>, <span class="nu0">6</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">26</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">20</span>, <span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">6</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">14</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>,
			<span class="co1">// loop 3</span>
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">8</span>, <span class="nu0">0</span>, 7.5f<span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">7</span>, <span class="nu0">0</span>, 10.5f<span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">6</span>, <span class="nu0">0</span>, <span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">26</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">6</span>, <span class="nu0">0</span>, <span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">14</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">6</span>, <span class="nu0">0</span>, <span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">26</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">6</span>, <span class="nu0">0</span>, <span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">14</span><span class="br0">)</span>,
			<span class="co1">// begin ellipse</span>
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">16</span>, <span class="nu0">5</span>, <span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">26</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">16</span>, <span class="sy0">-</span><span class="nu0">10</span>, <span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">14</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">16</span>, <span class="nu0">20</span>, <span class="nu0">20</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">26</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">10</span>, <span class="sy0">-</span><span class="nu0">25</span>, <span class="nu0">10</span><span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">10</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span>,
			<span class="co1">// come at me!</span>
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>28.00242f, 48.005623f, <span class="sy0">-</span>34.648228f<span class="br0">)</span>,
			<span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span> , <span class="sy0">-</span><span class="nu0">20</span><span class="br0">)</span>,
	<span class="br0">}</span><span class="sy0">;</span>
 
	<span class="kw1">private</span> <span class="kw4">void</span> createScene<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
		Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
		bell <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span> <span class="st0">"sound-emitter"</span> , <span class="kw1">new</span> Sphere<span class="br0">(</span><span class="nu0">15</span>,<span class="nu0">15</span>,<span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
		bell.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
		rootNode.<span class="me1">attachChild</span><span class="br0">(</span>bell<span class="br0">)</span><span class="sy0">;</span>
 
		ear1 <span class="sy0">=</span> makeEar<span class="br0">(</span>rootNode, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span> ,<span class="sy0">-</span><span class="nu0">20</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		ear2 <span class="sy0">=</span> makeEar<span class="br0">(</span>rootNode, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span> ,<span class="nu0">20</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		ear3 <span class="sy0">=</span> makeEar<span class="br0">(</span>rootNode, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">20</span>, <span class="nu0">0</span> ,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
		MotionPath track <span class="sy0">=</span> <span class="kw1">new</span> MotionPath<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
		<span class="kw1">for</span> <span class="br0">(</span>Vector3f v <span class="sy0">:</span> path<span class="br0">)</span><span class="br0">{</span>
			track.<span class="me1">addWayPoint</span><span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
		<span class="br0">}</span>
		track.<span class="me1">setCurveTension</span><span class="br0">(</span>0.80f<span class="br0">)</span><span class="sy0">;</span>
 
		motionControl <span class="sy0">=</span> <span class="kw1">new</span> MotionTrack<span class="br0">(</span>bell,track<span class="br0">)</span><span class="sy0">;</span>
		<span class="co1">// for now, use reflection to change the timer... </span>
		<span class="co1">// motionControl.setTimer(new IsoTimer(60));</span>
 
		<span class="kw1">try</span> <span class="br0">{</span>
			<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+field"><span class="kw3">Field</span></a> timerField<span class="sy0">;</span>
			timerField <span class="sy0">=</span> AbstractCinematicEvent.<span class="kw1">class</span>.<span class="me1">getDeclaredField</span><span class="br0">(</span><span class="st0">"timer"</span><span class="br0">)</span><span class="sy0">;</span>
			timerField.<span class="me1">setAccessible</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
			<span class="kw1">try</span> <span class="br0">{</span>timerField.<span class="me1">set</span><span class="br0">(</span>motionControl, motionTimer<span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span> 
			<span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+illegalargumentexception"><span class="kw3">IllegalArgumentException</span></a> e<span class="br0">)</span> <span class="br0">{</span>e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span> 
			<span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+illegalaccessexception"><span class="kw3">IllegalAccessException</span></a> e<span class="br0">)</span> <span class="br0">{</span>e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span>
		<span class="br0">}</span> 
		<span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+securityexception"><span class="kw3">SecurityException</span></a> e<span class="br0">)</span> <span class="br0">{</span>e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span> 
		<span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+nosuchfieldexception"><span class="kw3">NoSuchFieldException</span></a> e<span class="br0">)</span> <span class="br0">{</span>e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span>
 
 
		motionControl.<span class="me1">setDirectionType</span><span class="br0">(</span>MotionTrack.<span class="me1">Direction</span>.<span class="me1">PathAndRotation</span><span class="br0">)</span><span class="sy0">;</span>
		motionControl.<span class="me1">setRotation</span><span class="br0">(</span><span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleNormalAxis</span><span class="br0">(</span><span class="sy0">-</span>FastMath.<span class="me1">HALF_PI</span>, Vector3f.<span class="me1">UNIT_Y</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		motionControl.<span class="me1">setInitialDuration</span><span class="br0">(</span>20f<span class="br0">)</span><span class="sy0">;</span>
		motionControl.<span class="me1">setSpeed</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
 
		track.<span class="me1">enableDebugShape</span><span class="br0">(</span>assetManager, rootNode<span class="br0">)</span><span class="sy0">;</span>
		positionCamera<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
 
 
	<span class="kw1">private</span> <span class="kw4">void</span> positionCamera<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
		<span class="kw1">this</span>.<span class="me1">cam</span>.<span class="me1">setLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>28.00242f, 48.005623f, <span class="sy0">-</span>34.648228f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="kw1">this</span>.<span class="me1">cam</span>.<span class="me1">setRotation</span><span class="br0">(</span><span class="kw1">new</span> Quaternion<span class="br0">(</span>0.3359635f, 0.34280345f, <span class="sy0">-</span>0.13281013f, 0.8671653f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
 
	<span class="kw1">private</span> <span class="kw4">void</span> initAudio<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
		org.<span class="me1">lwjgl</span>.<span class="me1">input</span>.<span class="me1">Mouse</span>.<span class="me1">setGrabbed</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>	
		music <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>assetManager, <span class="st0">"Sound/Effects/Beep.ogg"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
 
		rootNode.<span class="me1">attachChild</span><span class="br0">(</span>music<span class="br0">)</span><span class="sy0">;</span>
		audioRenderer.<span class="me1">playSource</span><span class="br0">(</span>music<span class="br0">)</span><span class="sy0">;</span>
		music.<span class="me1">setPositional</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
		music.<span class="me1">setVolume</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
		music.<span class="me1">setReverbEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
		music.<span class="me1">setDirectional</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
		music.<span class="me1">setMaxDistance</span><span class="br0">(</span>200.0f<span class="br0">)</span><span class="sy0">;</span>
		music.<span class="me1">setRefDistance</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
		<span class="co1">//music.setRolloffFactor(1f);</span>
		music.<span class="me1">setLooping</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
		audioRenderer.<span class="me1">pauseSource</span><span class="br0">(</span>music<span class="br0">)</span><span class="sy0">;</span> 
	<span class="br0">}</span>
 
	<span class="kw1">public</span> <span class="kw1">class</span> Dancer <span class="kw1">implements</span> SoundProcessor <span class="br0">{</span>
		Geometry entity<span class="sy0">;</span>
		<span class="kw4">float</span> scale <span class="sy0">=</span> <span class="nu0">2</span><span class="sy0">;</span>
		<span class="kw1">public</span> Dancer<span class="br0">(</span>Geometry entity<span class="br0">)</span><span class="br0">{</span>
			<span class="kw1">this</span>.<span class="me1">entity</span> <span class="sy0">=</span> entity<span class="sy0">;</span>
		<span class="br0">}</span>
 
		<span class="co3">/**
		 * this method is irrelevant since there is no state to cleanup.
		 */</span>
		<span class="kw1">public</span> <span class="kw4">void</span> cleanup<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">}</span>
 
 
		<span class="co3">/**
		 * Respond to sound!  This is the brain of an AI entity that 
		 * hears its surroundings and reacts to them.
		 */</span>
		<span class="kw1">public</span> <span class="kw4">void</span> process<span class="br0">(</span>ByteBuffer audioSamples, <span class="kw4">int</span> numSamples, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+audioformat"><span class="kw3">AudioFormat</span></a> format<span class="br0">)</span> <span class="br0">{</span>
			audioSamples.<span class="me1">clear</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
			<span class="kw4">byte</span><span class="br0">[</span><span class="br0">]</span> data <span class="sy0">=</span> <span class="kw1">new</span> <span class="kw4">byte</span><span class="br0">[</span>numSamples<span class="br0">]</span><span class="sy0">;</span>
			<span class="kw4">float</span><span class="br0">[</span><span class="br0">]</span> out <span class="sy0">=</span> <span class="kw1">new</span> <span class="kw4">float</span><span class="br0">[</span>numSamples<span class="br0">]</span><span class="sy0">;</span>
			audioSamples.<span class="me1">get</span><span class="br0">(</span>data<span class="br0">)</span><span class="sy0">;</span>
			FloatSampleTools.<span class="me1">byte2floatInterleaved</span><span class="br0">(</span>data, <span class="nu0">0</span>, out, <span class="nu0">0</span>, 
					numSamples<span class="sy0">/</span>format.<span class="me1">getFrameSize</span><span class="br0">(</span><span class="br0">)</span>, format<span class="br0">)</span><span class="sy0">;</span>
 
			<span class="kw4">float</span> max <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+float"><span class="kw3">Float</span></a>.<span class="me1">NEGATIVE_INFINITY</span><span class="sy0">;</span>
			<span class="kw1">for</span> <span class="br0">(</span><span class="kw4">float</span> f <span class="sy0">:</span> out<span class="br0">)</span><span class="br0">{</span><span class="kw1">if</span> <span class="br0">(</span>f <span class="sy0">&gt;</span> max<span class="br0">)</span> max <span class="sy0">=</span> f<span class="sy0">;</span><span class="br0">}</span>
			audioSamples.<span class="me1">clear</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
			<span class="kw1">if</span> <span class="br0">(</span>max <span class="sy0">&gt;</span> <span class="nu0">0.1</span><span class="br0">)</span><span class="br0">{</span>entity.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span>
			<span class="kw1">else</span> <span class="br0">{</span>entity.<span class="me1">getMaterial</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Gray</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span>
		<span class="br0">}</span>
	<span class="br0">}</span>
 
	<span class="kw1">private</span> <span class="kw4">void</span> prepareEar<span class="br0">(</span>Geometry ear, <span class="kw4">int</span> n<span class="br0">)</span><span class="br0">{</span>
		<span class="kw1">if</span> <span class="br0">(</span><span class="kw1">this</span>.<span class="me1">audioRenderer</span> <span class="kw1">instanceof</span> MultiListener<span class="br0">)</span><span class="br0">{</span>
			MultiListener rf <span class="sy0">=</span> <span class="br0">(</span>MultiListener<span class="br0">)</span><span class="kw1">this</span>.<span class="me1">audioRenderer</span><span class="sy0">;</span>
 
			Listener auxListener <span class="sy0">=</span> <span class="kw1">new</span> Listener<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
			auxListener.<span class="me1">setLocation</span><span class="br0">(</span>ear.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
			rf.<span class="me1">addListener</span><span class="br0">(</span>auxListener<span class="br0">)</span><span class="sy0">;</span>
			WaveFileWriter aux <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
 
			<span class="kw1">try</span> <span class="br0">{</span>aux <span class="sy0">=</span> <span class="kw1">new</span> WaveFileWriter<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a>.<span class="me1">createTempFile</span><span class="br0">(</span><span class="st0">"advanced-audio-"</span> <span class="sy0">+</span> n, <span class="st0">".wav"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span> 
			<span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> e<span class="br0">)</span> <span class="br0">{</span>e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span><span class="br0">}</span>
 
			rf.<span class="me1">registerSoundProcessor</span><span class="br0">(</span>auxListener, 
					<span class="kw1">new</span> CompositeSoundProcessor<span class="br0">(</span><span class="kw1">new</span> Dancer<span class="br0">(</span>ear<span class="br0">)</span>, aux<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
		<span class="br0">}</span>   
	<span class="br0">}</span>
 
 
	<span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
		<span class="kw1">this</span>.<span class="me1">setTimer</span><span class="br0">(</span><span class="kw1">new</span> IsoTimer<span class="br0">(</span><span class="nu0">60</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
		initAudio<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
		createScene<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
		prepareEar<span class="br0">(</span>ear1, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
		prepareEar<span class="br0">(</span>ear2, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
		prepareEar<span class="br0">(</span>ear3, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
 
		motionControl.<span class="me1">play</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
	<span class="br0">}</span>
 
	<span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
		motionTimer.<span class="me1">update</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="kw1">if</span> <span class="br0">(</span>music.<span class="me1">getStatus</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">!=</span> AudioSource.<span class="me1">Status</span>.<span class="me1">Playing</span><span class="br0">)</span><span class="br0">{</span>
			music.<span class="me1">play</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		<span class="br0">}</span>
		Vector3f loc <span class="sy0">=</span> cam.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		Quaternion rot <span class="sy0">=</span> cam.<span class="me1">getRotation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
		listener.<span class="me1">setLocation</span><span class="br0">(</span>loc<span class="br0">)</span><span class="sy0">;</span>
		listener.<span class="me1">setRotation</span><span class="br0">(</span>rot<span class="br0">)</span><span class="sy0">;</span>
		music.<span class="me1">setLocalTranslation</span><span class="br0">(</span>bell.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
	<span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
<a href="/lib/exe/fetch.php?tok=b1b225&amp;media=http%3A%2F%2Fwww.youtube.com%2Fv%2FoCEfK0yhDrY%3F.swf" class="media mediafile mf_swf" title="http://www.youtube.com/v/oCEfK0yhDrY?.swf">oCEfK0yhDrY?.swf</a>
</p>

</div>
<!-- EDIT6 SECTION "Advanced Example" [7328-17233] -->
<h3 class="sectionedit7" id="using_advanced_features_to_record_from_more_than_one_perspective_at_once">Using Advanced features to Record from more than one perspective at once</h3>
<div class="level3">

<p>
<a href="/lib/exe/fetch.php?tok=8afd69&amp;media=http%3A%2F%2Fwww.youtube.com%2Fv%2FWIJt9aRGusc%3F.swf" class="media mediafile mf_swf" title="http://www.youtube.com/v/WIJt9aRGusc?.swf">WIJt9aRGusc?.swf</a>
</p>

</div>
<!-- EDIT7 SECTION "Using Advanced features to Record from more than one perspective at once" [17234-17375] -->
<h2 class="sectionedit8" id="more_information">More Information</h2>
<div class="level2">

<p>
This is the old page showing the first version of this idea
<a href="http://aurellem.org/cortex/html/capture-video.html" class="urlextern" title="http://aurellem.org/cortex/html/capture-video.html" rel="nofollow">http://aurellem.org/cortex/html/capture-video.html</a>
</p>

<p>
All source code can be found here:
</p>

<p>
<a href="http://hg.bortreb.com/audio-send" class="urlextern" title="http://hg.bortreb.com/audio-send" rel="nofollow">http://hg.bortreb.com/audio-send</a>
</p>

<p>
<a href="http://hg.bortreb.com/jmeCapture" class="urlextern" title="http://hg.bortreb.com/jmeCapture" rel="nofollow">http://hg.bortreb.com/jmeCapture</a>
</p>

<p>
More information on the modifications to OpenAL to support multiple
listeners can be found here.
</p>

<p>
<a href="http://aurellem.org/audio-send/html/ear.html" class="urlextern" title="http://aurellem.org/audio-send/html/ear.html" rel="nofollow">http://aurellem.org/audio-send/html/ear.html</a>
</p>

</div>
<!-- EDIT8 SECTION "More Information" [17376-] -->
