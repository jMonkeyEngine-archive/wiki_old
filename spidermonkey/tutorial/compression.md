---
title: Compression
---
<h1 class="sectionedit1" id="compression">Compression</h1>
<div class="level1">

<p>
</p><p></p><div class="notewarning">This article covers a deprecated <abbr title="Application Programming Interface">API</abbr>! See <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">networking</a> for current documentation.
</div>
Now this is going to be a real simply tutorial but still I wanted this in a separate article. Why you may ask? Simply because it's a feature that requires some explanation, since it has some caveats that I'll discuss. Also, I'll cover writing your own compression message.


<p>
First off - there are two compression types in SpiderMonkey, they are GZip and Zip. Could've added more, but didn't want to have a dependency for just a compression method. Both are used by wrapping your message in the appropriate compression message:
</p>
<pre class="code java">MyMessage msg <span class="sy0">=</span> <span class="kw1">new</span> MyMessage<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
client.<span class="me1">send</span><span class="br0">(</span><span class="kw1">new</span> GZIPCompressedMessage<span class="br0">(</span>msg<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// or</span>
client.<span class="me1">send</span><span class="br0">(</span><span class="kw1">new</span> ZIPCompressedMessage<span class="br0">(</span>msg<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Really simple, but ZIP requires some explanation. The ZIPCompressedMessage class also has two extra methods; setLevel(int) and getLevel(). These methods are for setting the compression level, where 1 is best compression but slowest, and where 9 is weakest compression but fastest. Please note that 9 is <strong>not</strong> the so called 'store' ZIP method, which simply stores file in the ZIP, instead of compressing it. This 'store' feature is not in SpiderMonkey since otherwise it would not have been called compression.
</p>

</div>
<!-- EDIT1 SECTION "Compression" [1-1331] -->
<h3 class="sectionedit2" id="writing_your_own">Writing your own</h3>
<div class="level3">

<p>
Now of course I'd love to see more compression methods in SpiderMonkey, so I'll discuss how to write your own. Let's just take GZIPCompressedMessage as example, since that one is the most straightforward. What I've done, is I've just created a GZIPCompressedMessage which extends CompressedMessage. It does not contain any extra messages, so the GZIPCompressedMessage class is practically 'empty'. The magic happens at the serializer, which is called the GZIPSerializer (you can read about writing your own serializer <a href="/spidermonkey/tutorial/serializing.html" class="wikilink1" title="spidermonkey:tutorial:serializing">here</a>). Then I just registered the GZIPSerializer to GZIPCompressedMessage and presto - you're done. Don't forget that in the Serializer you need to use writeClassAndObject first and then compress that data, and for read you'd need to use readClassAndObject after you've uncompressed (inflated) the message. For this to be clear, it may be useful to read <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/networking/com/jme3/network/serializing/serializers/GZIPSerializer.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/networking/com/jme3/network/serializing/serializers/GZIPSerializer.java" rel="nofollow">the GZIPSerializer class</a>.
</p>

<p>
That's that! Next tutorial we're going to discuss how to use the Service system.
</p>

</div>
<!-- EDIT2 SECTION "Writing your own" [1332-] -->
