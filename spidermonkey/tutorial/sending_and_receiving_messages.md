---
title: Sending and receiving messages
---
<h1 class="sectionedit1" id="sending_and_receiving_messages">Sending and receiving messages</h1>
<div class="level1">

<p>
</p><p></p><div class="notewarning">This article covers a deprecated <abbr title="Application Programming Interface">API</abbr>! See <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">networking</a> for current documentation.
</div>
In this tutorial I'm going to cover sending and receiving messages. I'll also explain how to write your own messages. This tutorial assumes you already have a working server-client connection.


<p>
Let's start by creating our own message. Later on we'll send this across the network.
</p>
<pre class="code java">@<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+serializable"><span class="kw3">Serializable</span></a><span class="br0">(</span><span class="br0">)</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloMessage <span class="kw1">extends</span> Message <span class="br0">{</span>
   <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> hello <span class="sy0">=</span> <span class="st0">"Hello!"</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
This is probably the smallest and simplest message you'll find. This is simply the process of creating a class, extending Message, and adding your fields to it. Also you need the @Serializable annotation, but we'll get to that later. Even though you don't <strong>have to</strong> extend Message, you generally should since then SpiderMonkey can add client and connection information on receiving. You can also send separate data, but we'll not go into that here - you should just send Messages.
</p>

<p>
Now let's send this message across the network. We'll send it from the client to the server.
</p>
<pre class="code java">Serializer.<span class="me1">registerClass</span><span class="br0">(</span>HelloMessage.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
server.<span class="me1">addMessageListener</span><span class="br0">(</span><span class="kw1">this</span>, HelloMessage.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
client.<span class="me1">addMessageListener</span><span class="br0">(</span><span class="kw1">this</span>, HelloMessage.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
client.<span class="me1">send</span><span class="br0">(</span><span class="kw1">new</span> HelloMessage<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> </pre>

<p>
First we've registered the class to the Serializer. This needs to happen on both the client and server, I'll explain why in the next tutorial. Then we add the message listeners for both the server and client, this makes sure we're notified when messages are received. Then we send the message. The message is by default reliable, and so it will be sent over TCP. Now we'll handle it on the server:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> messageReceived<span class="br0">(</span>Message message<span class="br0">)</span> <span class="br0">{</span>
   <span class="co1">// This message is of type HelloMessage, so we don't have to check.</span>
   HelloMessage helloMessage <span class="sy0">=</span> <span class="br0">(</span>HelloMessage<span class="br0">)</span>message<span class="sy0">;</span>
   <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>helloMessage.<span class="me1">hello</span><span class="br0">)</span><span class="sy0">;</span>
   helloMessage.<span class="me1">hello</span> <span class="sy0">=</span> <span class="st0">"Hi!"</span><span class="sy0">;</span>
   message.<span class="me1">getClient</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">send</span><span class="br0">(</span>helloMessage<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
This simply receives the message, and changes the Hello! to Hi! and sends it back to the client. The client, can of course handle this message however it wants to.
</p>

</div>
<!-- EDIT1 SECTION "Sending and receiving messages" [1-2217] -->
<h3 class="sectionedit2" id="serializable_annotation">Serializable annotation</h3>
<div class="level3">

<p>
The Serializable annotation is used to determine which serializer you want to use for your message, and which ID you want to register to it. If you specify no ID and no serializer, a ID will be assigned, and the default serializer will be used. The problem with specifying no ID is that you have to have the same order of registration on both the client and server, otherwise serializing will go wrong. It's therefore advisable that you use the id field, if you want to register classes in a different order.
</p>

<p>
The default serializer is, of course, FieldSerializer, which'll do just fine for just about any message you can throw at it. However, if you wish to serialize your message yourself, all you must do is write your own serializer, and then pass the class to the serializer field in the annotation. For example, this Serializable annotation sets ID to four, and serializer to CustomSerializer (which doesn't exist, mind you).
</p>
<pre class="code java">@<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+serializable"><span class="kw3">Serializable</span></a><span class="br0">(</span>id<span class="sy0">=</span><span class="nu0">4</span>, serializer<span class="sy0">=</span>CustomSerializer.<span class="kw1">class</span><span class="br0">)</span></pre>

<p>
That was it! The next tutorial explains how the Serializer system works, and how you can register your own serializers!
</p>

</div>
<!-- EDIT2 SECTION "Serializable annotation" [2218-] -->
