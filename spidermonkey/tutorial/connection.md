---
title: Connecting
---
<h1 class="sectionedit1" id="connecting">Connecting</h1>
<div class="level1">

<p>
</p><p></p><div class="notewarning">This article covers a deprecated <abbr title="Application Programming Interface">API</abbr>! See <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">networking</a> for current documentation.
</div>


<p>
This very first tutorial is going to teach you how to open a server and a client, and connect them to eachother. I'll also discuss how connection registration works. Since this is a very simple process in SpiderMonkey, this tutorial will be quite short.
</p>

</div>
<!-- EDIT1 SECTION "Connecting" [1-399] -->
<h3 class="sectionedit2" id="simple_connections">Simple connections</h3>
<div class="level3">

<p>
Creating a server is as simple as doing this:
</p>
<pre class="code java">Server myServer <span class="sy0">=</span> <span class="kw1">new</span> Server<span class="br0">(</span><span class="nu0">4040</span>, <span class="nu0">5050</span><span class="br0">)</span><span class="sy0">;</span>
myServer.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This initializes and starts a server on TCP port 4040 and UDP port 5050. Now it's time to connect a client:
</p>
<pre class="code java">Client client <span class="sy0">=</span> <span class="kw1">new</span> Client<span class="br0">(</span><span class="st0">"localhost"</span>, <span class="nu0">4040</span>, <span class="nu0">5050</span><span class="br0">)</span><span class="sy0">;</span>
client.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This initializes and starts a client, and it will immediately connect to localhost, TCP port 4040, and UDP port 5050. In the log, you'll get to see this:
</p>
<pre class="code">Sep 16, 2010 11:52:16 AM com.jme3.network.connection.TCPConnection bind
INFO: [Server#1][TCP] Bound to 0.0.0.0/0.0.0.0:4040
Sep 16, 2010 11:52:16 AM com.jme3.network.connection.UDPConnection bind
INFO: [Server#1][UDP] Bound to 0.0.0.0/0.0.0.0:5050
Sep 16, 2010 11:52:16 AM com.jme3.network.connection.Server start
INFO: [Server#1][???] Started server.
Sep 16, 2010 11:52:16 AM com.jme3.network.connection.TCPConnection connect
INFO: [Client#1][TCP] Connecting to localhost/127.0.0.1:4040
Sep 16, 2010 11:52:16 AM com.jme3.network.connection.UDPConnection connect
INFO: [Client#1][UDP] Set target to localhost/127.0.0.1:5050
Sep 16, 2010 11:52:16 AM com.jme3.network.connection.TCPConnection accept
INFO: [Server#1][TCP] A client connected with address /127.0.0.1
Sep 16, 2010 11:52:16 AM com.jme3.network.connection.TCPConnection connect
INFO: [Client#1][TCP] Connection succeeded.</pre>

<p>
As you can see, this is a combined log of the client and server. Even though it looks like only a connection has been made, the Client registration has already happened at this point as well. Client registration is necessary so you can call TCP and UDP methods on only one Client instance on the server. You don't have to worry about client registration, since SpiderMonkey does this automatically on connection.
</p>

</div>
<!-- EDIT2 SECTION "Simple connections" [400-2217] -->
<h3 class="sectionedit3" id="connector_filters">Connector filters</h3>
<div class="level3">

<p>
You can also filter connections (or connectors as I call them) in SpiderMonkey. You can do this by implementing the ConnectorFilter interface:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyConnectorFilter <span class="kw1">implements</span> ConnectorFilter <span class="br0">{</span>
   <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> filterConnector<span class="br0">(</span>InetSocketAddress address<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>address.<span class="me1">isLoopbackAddress</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="kw1">return</span> <span class="st0">"I don't like locals!"</span><span class="sy0">;</span>
      <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
   <span class="br0">}</span>  
<span class="br0">}</span></pre>

<p>
Return null for no filtering, or a String with the reason if you want to filter this person.
</p>

</div>
<!-- EDIT3 SECTION "Connector filters" [2218-2721] -->
<h3 class="sectionedit4" id="discover_hosts">Discover hosts</h3>
<div class="level3">

<p>
SpiderMonkey Clients are also able to discover hosts running in the <abbr title="Local Area Network">LAN</abbr>. This is also a very simple process, and can be done as follows:
</p>
<pre class="code java">Client client <span class="sy0">=</span> <span class="kw1">new</span> Client<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
List<span class="sy0">&lt;</span>InetAddress<span class="sy0">&gt;</span> foundHosts <span class="sy0">=</span> client.<span class="me1">discoverHosts</span><span class="br0">(</span><span class="nu0">5050</span>, <span class="nu0">5000</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This starts the host discovery on port 5050, and listens for servers for 5 seconds. Typically, servers respond pretty fast so a few seconds should be enough. To do something with these hosts it's as simple as doing:
</p>
<pre class="code java"><span class="kw1">for</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+inetaddress"><span class="kw3">InetAddress</span></a> host <span class="sy0">:</span> foundHosts<span class="br0">)</span> <span class="br0">{</span>
    client.<span class="me1">connect</span><span class="br0">(</span>host.<span class="me1">getCanonicalHostName</span><span class="br0">(</span><span class="br0">)</span>, <span class="nu0">4040</span>, <span class="nu0">5050</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
client.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Do note that this would connect to every host found, so this does not work properly, but the idea is that you can configure it the way you want it. Don't forget to start() the client.
</p>

<p>
This concludes the first tutorial. In the next tutorial, it's time to send and listen for messages!
</p>

</div>
<!-- EDIT4 SECTION "Discover hosts" [2722-] -->
