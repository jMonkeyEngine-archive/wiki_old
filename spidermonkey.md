---
title: SpiderMonkey (Deprecated!)
---
<h1 class="sectionedit1" id="spidermonkey_deprecated">SpiderMonkey (Deprecated!)</h1>
<div class="level1">

<p>
</p><p></p><div class="notewarning">This article covers a deprecated <abbr title="Application Programming Interface">API</abbr>! See <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">networking</a> for current documentation. See <a href="/spidermonkey/migration.html" class="wikilink1" title="spidermonkey:migration">migration</a> for migration instructions.
</div>
SpiderMonkey is a high performance Java networking engine, aiming to provide game developers a stable and efficient networking system. It's also perfectly capable of doing anything other than game networking. SpiderMonkey is part of jME3 and can be found in the src/networking directory.
<strong>Author:</strong> Lars 'Levia' Wesselius<br />

<strong>License:</strong> <a href="http://www.opensource.org/licenses/bsd-license.php" class="urlextern" title="http://www.opensource.org/licenses/bsd-license.php" rel="nofollow">New BSD license</a><br />

<strong>Blog:</strong> <a href="http://codeninja.me/tag/spidermonkey/" class="urlextern" title="http://codeninja.me/tag/spidermonkey/" rel="nofollow">http://codeninja.me/tag/spidermonkey/</a><br />

<strong>Forum:</strong> <a href="http://jmonkeyengine.org/groups/spidermonkey/forum/" class="urlextern" title="http://jmonkeyengine.org/groups/spidermonkey/forum/" rel="nofollow">http://jmonkeyengine.org/groups/spidermonkey/forum/</a><br />

A tutorial trail can be found below, and below that all different aspects of SpiderMonkey are explained. These tutorials are to be updated upon SVN HEAD, so if new features are added in SVN, you should tutorials arriving of them soon.


</div>
<!-- EDIT1 SECTION "SpiderMonkey (Deprecated!)" [1-989] -->
<h3 class="sectionedit2" id="tutorial_trail">Tutorial trail</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> <a href="/spidermonkey/tutorial/connection.html" class="wikilink1" title="spidermonkey:tutorial:connection">Connections</a></div>
</li>
<li class="level1"><div class="li"> <a href="/spidermonkey/tutorial/sending_and_receiving_messages.html" class="wikilink1" title="spidermonkey:tutorial:sending_and_receiving_messages">Sending and receiving messages</a></div>
</li>
<li class="level1"><div class="li"> <a href="/spidermonkey/tutorial/serializing.html" class="wikilink1" title="spidermonkey:tutorial:serializing">Serialization</a></div>
</li>
<li class="level1"><div class="li"> <a href="/spidermonkey/tutorial/compression.html" class="wikilink1" title="spidermonkey:tutorial:compression">Compression</a></div>
</li>
<li class="level1"><div class="li"> <a href="/spidermonkey/tutorial/services.html" class="wikilink1" title="spidermonkey:tutorial:services">Services</a></div>
</li>
<li class="level1"><div class="li"> <a href="/spidermonkey/tutorial/streaming.html" class="wikilink1" title="spidermonkey:tutorial:streaming">Streaming</a></div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Tutorial trail" [990-1365] -->
<h2 class="sectionedit3" id="explanation_of_spidermonkey_s_inner_workings">Explanation of SpiderMonkey's inner workings</h2>
<div class="level2">

</div>
<!-- EDIT3 SECTION "Explanation of SpiderMonkey's inner workings" [1366-1420] -->
<h3 class="sectionedit4" id="connection_protocols">Connection protocols</h3>
<div class="level3">

<p>
SpiderMonkey supports both TCP and UDP, and is also extendable to provide others. Possible future protocols may be RUDP, UDP Lite, and SCTP. SCTP will be added in Java 7, and will therefore probably added to SpiderMonkey after it's released. Please note that the language level of SpiderMonkey is 1.5, so it will definitely not be part of the standard <abbr title="Application Programming Interface">API</abbr> for a few years.
</p>

</div>
<!-- EDIT4 SECTION "Connection protocols" [1421-1822] -->
<h3 class="sectionedit5" id="clients">Clients</h3>
<div class="level3">

<p>
SpiderMonkey creates two connections by default. A TCP connection for a reliable connection, and an UDP 'connection' <sup><a href="#fn__1" id="fnt__1" class="fn_top">1)</a></sup> for fast message handling. A problem arises here: these two connections mean that even though there are two connections, there's only one client to represent both the connections. In SpiderMonkey you don't have to worry about that. The server has a client manager which deals with this problem. Upon connecting, clients have to send a ClientRegistration message to link their TCP and UDP connections together. Upon receiving those two messages, server combines the clients into one, and provides this client to you. This means you can call both TCP and UDP methods on the client. If you still want to receive the 'local' client of a connection, you can do so by calling the appropriate messages in the Server class.
</p>

</div>
<!-- EDIT5 SECTION "Clients" [1823-2697] -->
<h3 class="sectionedit6" id="serializing">Serializing</h3>
<div class="level3">

<p>
Serializing is an aspect that received a lot of attention. I wanted it to be simple for people to register their own messages, but also be able to register serializers for their own object types. The system works by registering classes to serializers. Generally, a serializer does not exist without a class it can serialize - simply because it doesn't have to: Why have a serializer when there's nothing to serialize. A lot of work has been put into making it as efficient as possible. What can be left out, is left out, and what can optimized, is optimized.
</p>

</div>

<h5 id="field_serializer">Field serializer</h5>
<div class="level5">

<p>
The default serializer requires some explanation. This serializer serializes all classes that have no (registered) serializer. The field serializer works by saving all fields internally, so it can access them on serialization faster. The fields are taken, and their types are checked. They are put through a serializer again (which serializer depends, of course, on the data type). Then they are ready to be written to the buffer. As you can tell, this is quite a simple serializer, and should be used if your message don't require extra attention. See <a href="/spidermonkey/tutorial/serializing.html" class="wikilink1" title="spidermonkey:tutorial:serializing">this tutorial</a> if you want to know how to register your own messages or serializers.
</p>

</div>
<!-- EDIT6 SECTION "Serializing" [2698-3972] -->
<h3 class="sectionedit7" id="service_system">Service system</h3>
<div class="level3">

<p>
The service system is in fact a tiny system. It's meant to solve a small, but annoying problem. Imagine you have SpiderMonkey as your networking library, and other people have made extra's for it. Excellent, of course, but they may all require different initialization! Perhaps you have to instantiate one yourself by using new, or maybe another works by calling a factory method; the service system exists to avoid that problem. All extras should use this system. Please see <a href="/spidermonkey/tutorial/services.html" class="wikilink1" title="spidermonkey:tutorial:services">the service tutorial</a> on how to use this system.
</p>

</div>
<!-- EDIT7 SECTION "Service system" [3973-4554] -->
<h3 class="sectionedit8" id="compression">Compression</h3>
<div class="level3">

<p>
By default SpiderMonkey supports compressing messages. It's been made to where you have complete freedom over what messages you wish to compress. See <a href="/spidermonkey/tutorial/compression.html" class="wikilink1" title="spidermonkey:tutorial:compression">this tutorial</a> on how to use these special messages.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/network.html" class="wikilink1" title="tag:network" rel="tag">network</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Compression" [4555-] --><div class="footnotes">
<div class="fn"><sup><a href="#fnt__1" id="fn__1" class="fn_bot">1)</a></sup> 
UDP is connectionless</div>
</div>
