---
title: Serialization system
---
<h1 class="sectionedit1" id="serialization_system">Serialization system</h1>
<div class="level1">

<p>
</p><p></p><div class="notewarning">This article covers a deprecated <abbr title="Application Programming Interface">API</abbr>! See <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">networking</a> for current documentation.
</div>
In this lesson you'll learn about a pretty advanced system of SpiderMonkey. Why so early, you may ask; it's because it is an important aspect of SpiderMonkey, that you need to understand to effectively network your games.


<p>
Let's start with a general explanation of how the serialization system works. SpiderMonkey's Serializer class is the entry point for everything serializing. Serializing is the act of translating an object into bytes, so it can be transferred over the network. SpiderMonkey does this by having Serializer classes (they extend Serializer itself), and having some static methods available in the Serializer class. A serializer does not exist without a class it can serialize - this means that Serializers need to be registered with a class. For example, the String type is registered to the StringSerializer class. Without the String type being registered, there'd be no instance of StringSerializer. So! Let's get down to business!
</p>

</div>
<!-- EDIT1 SECTION "Serialization system" [1-1106] -->
<h3 class="sectionedit2" id="writing_your_own_serializer">Writing your own serializer</h3>
<div class="level3">

<p>
There is going to be a situation where you need to serialize something yourself, whether you like it or not. We're going through how you're going to do, by writing a entirely new Serializer - please note that this Serializer is not necessary in SpiderMonkey, since SpiderMonkey can serialize Serializable, and InetAddress4 implements Serializable (though it does save a LOT of bytes by doing it yourself). The field that makes an InetAddress4 an InetAddress4 is the IP address, so that's what we're going to serialize. Let's start by going through the basics of extending the Serializer class:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> Inet4AddressSerializer <span class="kw1">extends</span> Serializer <span class="br0">{</span>
   <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+inetaddress"><span class="kw3">InetAddress</span></a> readObject<span class="br0">(</span>ByteBuffer data, <span class="kw1">Class</span> c<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a>
      <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
   <span class="br0">}</span>
 
   <span class="kw1">public</span> <span class="kw4">void</span> writeObject<span class="br0">(</span>ByteBuffer buffer, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> object<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
      <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+inetaddress"><span class="kw3">InetAddress</span></a> address <span class="sy0">=</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+inetaddress"><span class="kw3">InetAddress</span></a><span class="br0">)</span>object<span class="sy0">;</span>
   <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
As you can see, you have to extend Serializer and implement the methods T readObject(ByteBuffer, Class) and writeObject(ByteBuffer, Object). These are the methods that actually do the job. Obviously, writeObject is used when sending, and readObject is used when reading. The next part is just Java coding - you just kind of have to know the <abbr title="Application Programming Interface">API</abbr> of those objects you're serializing to convert into bytes. This one's really simple though ;)
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> Inet4AddressSerializer <span class="kw1">extends</span> Serializer <span class="br0">{</span>
   @Override
   <span class="kw1">public</span> <span class="sy0">&lt;</span>T<span class="sy0">&gt;</span> T readObject<span class="br0">(</span>ByteBuffer data, Class<span class="sy0">&lt;</span>T<span class="sy0">&gt;</span> c<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
       <span class="kw4">byte</span><span class="br0">[</span><span class="br0">]</span> address <span class="sy0">=</span> <span class="kw1">new</span> <span class="kw4">byte</span><span class="br0">[</span><span class="nu0">4</span><span class="br0">]</span><span class="sy0">;</span>
       data.<span class="me1">get</span><span class="br0">(</span>address<span class="br0">)</span><span class="sy0">;</span>
       <span class="kw1">return</span> <span class="br0">(</span>T<span class="br0">)</span>Inet4Address.<span class="me1">getByAddress</span><span class="br0">(</span>address<span class="br0">)</span><span class="sy0">;</span>
   <span class="br0">}</span>
 
   @Override
   <span class="kw1">public</span> <span class="kw4">void</span> writeObject<span class="br0">(</span>ByteBuffer buffer, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> object<span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
       Inet4Address address <span class="sy0">=</span> <span class="br0">(</span>Inet4Address<span class="br0">)</span>object<span class="sy0">;</span>
       buffer.<span class="me1">put</span><span class="br0">(</span>address.<span class="me1">getAddress</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
   <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
So now you've got this serializer, and you don't know what to do with it. Well, you need to register it to a class, and what other class would you want to register it to, than Inet4Address?
</p>
<pre class="code">Serializer.registerClass(Inet4Address.class, new Inet4AddressSerializer());</pre>

<p>
And now you can use the Inet4Address anywhere in a Message! Now we'll test this Serializer, and see if we can get the IP on the other side:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> AddressMessage <span class="kw1">extends</span> Message <span class="br0">{</span>
  <span class="kw1">public</span> Inet4Address addr<span class="sy0">;</span>
  <span class="kw1">public</span> AddressMessage<span class="br0">(</span>Inet4Address addr<span class="br0">)</span> <span class="br0">{</span> <span class="kw1">this</span>.<span class="me1">addr</span> <span class="sy0">=</span> addr<span class="sy0">;</span> <span class="br0">}</span>
<span class="br0">}</span>
...
<span class="me1">client</span>.<span class="me1">send</span><span class="br0">(</span><span class="kw1">new</span> AddressMessage<span class="br0">(</span>Inet4Address.<span class="me1">getByName</span><span class="br0">(</span><span class="st0">"google.com"</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Results in a message being received, which prints out as:
</p>
<pre class="code">/66.102.13.106</pre>

<p>
And there you go, that's the end of this tutorial!
</p>

<p>
Next tutorial you'll learn about a simple, but powerful feature - compression.
</p>

</div>
<!-- EDIT2 SECTION "Writing your own serializer" [1107-] -->
