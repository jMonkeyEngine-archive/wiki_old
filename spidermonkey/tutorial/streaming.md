---
title: Streaming service
---
<h1 class="sectionedit1" id="streaming_service">Streaming service</h1>
<div class="level1">

<p>
</p><p></p><div class="notewarning">This article covers a deprecated <abbr title="Application Programming Interface">API</abbr>! See <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">networking</a> for current documentation.
</div>


<p>
The streaming service is meant for situations where you want to transfer files, or other types of data to clients. In this tutorial we'll discuss how it works, and how to use it.
</p>

<p>
Let's start off with how it works; streaming service uses messages to transfer data. This is done so it doesn't block other messages from being sent, while transferring. First a message is sent the describes the stream. The peer can now choose whether to accept or reject the stream. When the peer accepts, the data will be sent. You have to handle this data yourself. At the end of the stream you get the same message as when the stream was offered, to indicate the end of the stream.
</p>

<p>
Let's transfer a file to a client:
</p>
<pre class="code java">StreamingService sService <span class="sy0">=</span> client.<span class="me1">getService</span><span class="br0">(</span>StreamingService.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
sService.<span class="me1">addStreamListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
 
sService <span class="sy0">=</span> server.<span class="me1">getService</span><span class="br0">(</span>StreamingService.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
Client receiver <span class="sy0">=</span> server.<span class="me1">getConnectors</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">get</span><span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// Note that you can't use 'client' here, since it's not a connector.</span>
sService.<span class="me1">offerStream</span><span class="br0">(</span>receiver, <span class="kw1">new</span> StreamMessage<span class="br0">(</span><span class="br0">)</span>, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+fileinputstream"><span class="kw3">FileInputStream</span></a><span class="br0">(</span><span class="st0">"test.txt"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// StreamMessage used here as start and end message, but can be anything to describe the stream on the other end.</span></pre>

<p>
As you can see, this system uses the Service system. First, we get the client's StreamingService, and register ourselves as a listener. Then we get the server's version of the StreamingService, from which you can stream things. Then we get a connector client (the first one), and send the file via an InputStream.
</p>

<p>
Now to receive this stuff is simple;
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">boolean</span> streamOffered<span class="br0">(</span>StreamMessage message<span class="br0">)</span> <span class="br0">{</span>
   <span class="co1">// Here you'd normally check the message what this stream is all about, and </span>
   <span class="co1">// base your acception criteria on that.</span>
   fileStream <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+fileoutputstream"><span class="kw3">FileOutputStream</span></a><span class="br0">(</span><span class="st0">"test.txt"</span><span class="br0">)</span><span class="sy0">;</span>
   <span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span> <span class="co1">// Sure, we'll just accept this message.</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> streamDataReceived<span class="br0">(</span>StreamDataMessage message<span class="br0">)</span> <span class="br0">{</span>
   fileStream.<span class="me1">write</span><span class="br0">(</span>message.<span class="me1">getData</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> streamCompleted<span class="br0">(</span>StreamMessage message<span class="br0">)</span> <span class="br0">{</span>
   fileStream.<span class="me1">flush</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
   fileStream.<span class="me1">close</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
That was all; simple right?
</p>

</div>
