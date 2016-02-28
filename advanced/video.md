---
title: Video
---
<h1 class="sectionedit1" id="video">Video</h1>
<div class="level1">

<p>
Relevant forum topics:
</p>

<p>
<a href="http://hub.jmonkeyengine.org/t/ive-made-a-movieappstate-so-you-dont-have-to/31673" class="urlextern" title="http://hub.jmonkeyengine.org/t/ive-made-a-movieappstate-so-you-dont-have-to/31673" rel="nofollow">http://hub.jmonkeyengine.org/t/ive-made-a-movieappstate-so-you-dont-have-to/31673</a>
</p>

<p>
<a href="http://hub.jmonkeyengine.org/t/news-about-playing-videos-on-jme/30084/5" class="urlextern" title="http://hub.jmonkeyengine.org/t/news-about-playing-videos-on-jme/30084/5" rel="nofollow">http://hub.jmonkeyengine.org/t/news-about-playing-videos-on-jme/30084/5</a>
</p>

<p>
<a href="http://www.java-gaming.org/topics/java-media-player/27100/view.html" class="urlextern" title="http://www.java-gaming.org/topics/java-media-player/27100/view.html" rel="nofollow">YUNPM - a Java Media Player</a> (java-gaming.org)
</p>

<p>
<a href="http://www.java-gaming.org/topics/gstlwjgl-yet-another-media-player/27146/view.html" class="urlextern" title="http://www.java-gaming.org/topics/gstlwjgl-yet-another-media-player/27146/view.html" rel="nofollow">GstLWJGL</a> (java-gaming.org)
</p>

<p>
<a href="http://jogamp.org/deployment/jogamp-next/javadoc/jogl/javadoc/com/jogamp/opengl/util/av/package-summary.html" class="urlextern" title="http://jogamp.org/deployment/jogamp-next/javadoc/jogl/javadoc/com/jogamp/opengl/util/av/package-summary.html" rel="nofollow">GL Media Player</a> (jogamp.org)
</p>

<p>
<a href="http://www.xuggle.com/xuggler" class="urlextern" title="http://www.xuggle.com/xuggler" rel="nofollow">Xuggler</a>
</p>

<p>
</p><p></p><div class="notewarning">This <abbr title="Application Programming Interface">API</abbr> is deprecated.
</div>


<p>
jMonkeyEngine supports Jheora Ogg video (<code>com.jme3.video</code>).
</p>

<p>
Full code sample here: <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/jheora/com/jme3/video/TestVideoPlayer.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/jheora/com/jme3/video/TestVideoPlayer.java" rel="nofollow">TestVideoPlayer.java</a>
</p>

<p>
You create either a file inputstream to load the video from your hard drive:
</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+fileinputstream"><span class="kw3">FileInputStream</span></a>  fis <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+fileinputstream"><span class="kw3">FileInputStream</span></a><span class="br0">(</span><span class="st0">"E:<span class="es0">\\</span>my_bunny.ogg"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Or you stream the video live from a web location:
</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+inputstream"><span class="kw3">InputStream</span></a> fis <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+url"><span class="kw3">URL</span></a><span class="br0">(</span><span class="st0">"http://server/my_video.ogg"</span><span class="br0">)</span>.<span class="me1">openStream</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Setting the queued frames to a value value higher than 5 (<code>videoQueue = new VQueue(5);</code>) will make web streamed playback smoother at the cost of memory.
Here is an example of video streaming in context:
</p>
<pre class="code java">    <span class="kw1">private</span> <span class="kw4">void</span> createVideo<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+inputstream"><span class="kw3">InputStream</span></a> fis <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+url"><span class="kw3">URL</span></a><span class="br0">(</span><span class="st0">"http://mirrorblender.top-ix.org/peach/"</span><span class="sy0">+</span>
            <span class="st0">"bigbuckbunny_movies/big_buck_bunny_480p_stereo.ogg"</span><span class="br0">)</span>.<span class="me1">openStream</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            videoQueue <span class="sy0">=</span> <span class="kw1">new</span> VQueue<span class="br0">(</span><span class="nu0">5</span><span class="br0">)</span><span class="sy0">;</span>               <span class="co1">// streaming quality vs memory</span>
            decoder <span class="sy0">=</span> <span class="kw1">new</span> AVThread<span class="br0">(</span>fis, videoQueue<span class="br0">)</span><span class="sy0">;</span>
            videoThread <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+thread"><span class="kw3">Thread</span></a><span class="br0">(</span>decoder, <span class="st0">"Jheora Video Decoder"</span><span class="br0">)</span><span class="sy0">;</span>
            videoThread.<span class="me1">setDaemon</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
            videoThread.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            masterClock <span class="sy0">=</span> decoder.<span class="me1">getMasterClock</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> ex<span class="br0">)</span> <span class="br0">{</span>
            ex.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span></pre>

<p>
Use the simpleUpdate() method to play the audio:
</p>
<pre class="code java">    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>source <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>decoder.<span class="me1">getAudioStream</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
                source <span class="sy0">=</span> <span class="kw1">new</span> AudioNode<span class="br0">(</span>decoder.<span class="me1">getAudioStream</span><span class="br0">(</span><span class="br0">)</span>, <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
                source.<span class="me1">setPositional</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
                source.<span class="me1">setReverbEnabled</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
                audioRenderer.<span class="me1">playSource</span><span class="br0">(</span>source<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span><span class="kw1">else</span><span class="br0">{</span>
                <span class="co1">// uncomment this statement to be able to play videos</span>
                <span class="co1">// without audio.</span>
                <span class="kw1">return</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
 
        <span class="kw1">if</span> <span class="br0">(</span>waitTime <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span><span class="br0">{</span>
            waitTime <span class="sy0">-=</span> tpf<span class="sy0">;</span>
            <span class="kw1">if</span> <span class="br0">(</span>waitTime <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span>
                <span class="kw1">return</span><span class="sy0">;</span>
            <span class="kw1">else</span><span class="br0">{</span>
                waitTime <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
                drawFrame<span class="br0">(</span>frameToDraw<span class="br0">)</span><span class="sy0">;</span>
                frameToDraw <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span><span class="kw1">else</span><span class="br0">{</span>
            VFrame frame<span class="sy0">;</span>
            <span class="kw1">try</span> <span class="br0">{</span>
                frame <span class="sy0">=</span> videoQueue.<span class="me1">take</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+interruptedexception"><span class="kw3">InterruptedException</span></a> ex<span class="br0">)</span><span class="br0">{</span>
                stop<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="kw1">return</span><span class="sy0">;</span>
            <span class="br0">}</span>
            <span class="kw1">if</span> <span class="br0">(</span>frame.<span class="me1">getTime</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&lt;</span> lastFrameTime<span class="br0">)</span><span class="br0">{</span>
                videoQueue.<span class="me1">returnFrame</span><span class="br0">(</span>frame<span class="br0">)</span><span class="sy0">;</span>
                <span class="kw1">return</span><span class="sy0">;</span>
            <span class="br0">}</span>
 
            <span class="kw1">if</span> <span class="br0">(</span>frame.<span class="me1">getTime</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">==</span> <span class="sy0">-</span><span class="nu0">2</span><span class="br0">)</span><span class="br0">{</span>
                <span class="co1">// end of stream</span>
                <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"End of stream"</span><span class="br0">)</span><span class="sy0">;</span>
                stop<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="kw1">return</span><span class="sy0">;</span>
            <span class="br0">}</span>
 
            <span class="kw4">long</span> AV_SYNC_THRESHOLD <span class="sy0">=</span> <span class="nu0">1</span> <span class="sy0">*</span> Clock.<span class="me1">MILLIS_TO_NANOS</span><span class="sy0">;</span>
 
            <span class="kw4">long</span> delay <span class="sy0">=</span> frame.<span class="me1">getTime</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">-</span> lastFrameTime<span class="sy0">;</span>
            <span class="kw4">long</span> diff <span class="sy0">=</span> frame.<span class="me1">getTime</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">-</span> masterClock.<span class="me1">getTime</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw4">long</span> syncThresh <span class="sy0">=</span> delay <span class="sy0">&gt;</span> AV_SYNC_THRESHOLD <span class="sy0">?</span> delay <span class="sy0">:</span> AV_SYNC_THRESHOLD<span class="sy0">;</span>
 
            <span class="co1">// if difference is more than 1 second, synchronize.</span>
            <span class="kw1">if</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+math"><span class="kw3">Math</span></a>.<span class="me1">abs</span><span class="br0">(</span>diff<span class="br0">)</span> <span class="sy0">&lt;</span> Clock.<span class="me1">SECONDS_TO_NANOS</span><span class="br0">)</span><span class="br0">{</span>
                <span class="kw1">if</span><span class="br0">(</span>diff <span class="sy0">&lt;=</span> <span class="sy0">-</span>syncThresh<span class="br0">)</span> <span class="br0">{</span>
                  delay <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
                <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span><span class="br0">(</span>diff <span class="sy0">&gt;=</span> syncThresh<span class="br0">)</span> <span class="br0">{</span>
                  delay <span class="sy0">=</span> <span class="nu0">2</span> <span class="sy0">*</span> delay<span class="sy0">;</span>
                <span class="br0">}</span>
            <span class="br0">}</span>
 
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"M: "</span><span class="sy0">+</span>decoder.<span class="me1">getSystemClock</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getTimeSeconds</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">+</span>
                               <span class="st0">", V: "</span><span class="sy0">+</span>decoder.<span class="me1">getVideoClock</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getTimeSeconds</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">+</span>
                               <span class="st0">", A: "</span><span class="sy0">+</span>decoder.<span class="me1">getAudioClock</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getTimeSeconds</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="kw1">if</span> <span class="br0">(</span>delay <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span><span class="br0">{</span>
                waitNanos<span class="br0">(</span>delay<span class="br0">)</span><span class="sy0">;</span>
                drawFrame<span class="br0">(</span>frame<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span><span class="kw1">else</span><span class="br0">{</span>
                videoQueue.<span class="me1">returnFrame</span><span class="br0">(</span>frame<span class="br0">)</span><span class="sy0">;</span>
                lastFrameTime <span class="sy0">=</span> frame.<span class="me1">getTime</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span></pre>

<p>
Helper Methods:
</p>
<pre class="code java">    <span class="kw1">private</span> <span class="kw4">void</span> drawFrame<span class="br0">(</span>VFrame frame<span class="br0">)</span><span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+image"><span class="kw3">Image</span></a> image <span class="sy0">=</span> frame.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        frame.<span class="me1">setImage</span><span class="br0">(</span>image<span class="br0">)</span><span class="sy0">;</span>
        picture.<span class="me1">setTexture</span><span class="br0">(</span>assetManager, frame, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// note: this forces renderer to upload frame immediately,</span>
        <span class="co1">// since it is going to be returned to the video queue pool</span>
        <span class="co1">// it could be used again.</span>
        renderer.<span class="me1">setTexture</span><span class="br0">(</span><span class="nu0">0</span>, frame<span class="br0">)</span><span class="sy0">;</span>
        videoQueue.<span class="me1">returnFrame</span><span class="br0">(</span>frame<span class="br0">)</span><span class="sy0">;</span>
        lastFrameTime <span class="sy0">=</span> frame.<span class="me1">getTime</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span></pre>
<pre class="code java">    <span class="kw1">private</span> <span class="kw4">void</span> waitNanos<span class="br0">(</span><span class="kw4">long</span> time<span class="br0">)</span><span class="br0">{</span>
        <span class="kw4">long</span> millis <span class="sy0">=</span> <span class="br0">(</span><span class="kw4">long</span><span class="br0">)</span> <span class="br0">(</span>time <span class="sy0">/</span> Clock.<span class="me1">MILLIS_TO_NANOS</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw4">int</span> nanos   <span class="sy0">=</span> <span class="br0">(</span><span class="kw4">int</span><span class="br0">)</span> <span class="br0">(</span>time <span class="sy0">-</span> <span class="br0">(</span>millis <span class="sy0">*</span> Clock.<span class="me1">MILLIS_TO_NANOS</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="kw1">try</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+thread"><span class="kw3">Thread</span></a>.<span class="me1">sleep</span><span class="br0">(</span>millis, nanos<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span><span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+interruptedexception"><span class="kw3">InterruptedException</span></a> ex<span class="br0">)</span><span class="br0">{</span>
            stop<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span></pre>

</div>
