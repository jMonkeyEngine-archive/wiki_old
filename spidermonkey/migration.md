---
title: SpiderMonkey: Migrating to the Current API
---
<h1 class="sectionedit1" id="spidermonkeymigrating_to_the_current_api">SpiderMonkey: Migrating to the Current API</h1>
<div class="level1">

<p>
</p><p></p><div class="notewarning">This article covers how to move away from an older, deprecated <abbr title="Application Programming Interface">API</abbr>! If you just start with JME3 networking, see <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">networking</a> for current documentation.
</div>


<p>
This document provides an overview of the new versus  the old SpiderMonkey <abbr title="Application Programming Interface">API</abbr>, and a path for migrating from the old, now deprecated, <abbr title="Application Programming Interface">API</abbr> to the newer version.  Much has changed.
The <a href="/spidermonkey.html" class="wikilink1" title="spidermonkey">original SpiderMonkey</a> implementation was a good concept and a clever implementation but suffered under the weight of rapid patches and some creeping design deficit.  In the end, there were enough small problems, long-term maintenance issues, and limitations that a newer design was warranted.
Some things will be very similar but others have changed very much. Hopefully for the better.
</p>

</div>
<!-- EDIT1 SECTION "SpiderMonkey: Migrating to the Current API" [1-837] -->
<h2 class="sectionedit2" id="overview">Overview</h2>
<div class="level2">

<p>
Most of the new SpiderMonkey <abbr title="Application Programming Interface">API</abbr> now exists as a set of interfaces and helper classes in the 'com.jme3.network' package.  For most users, this package and the 'message' package will be all they need to worry about.  The 'base' and 'kernel' packages only come into play when implementing custom network transports or alternate client/server protocols (<em>which are now possible</em>).
Clients and Servers can be created from the factory methods on the Network helper class.  Once a Server instance is created and started, it can accept remote connections from Clients.  The Client objects represent the client-side of a client→server connection.  Within the Server, these are HostedConnections.  This is a distinct change from the old <abbr title="Application Programming Interface">API</abbr>.
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Client      </th><th class="col1 leftalign">         </th><th class="col2 leftalign"> Server       </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> com.jme3.network.Client </td><td class="col1"> ←→ </td><td class="col2"> com.jme3.network.HostedConnection </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [1595-1706] -->
<p>
HostedConnections can hold application defined client-specific session attributes that the server-side listeners and services can use to track player information, etc..
MessageListeners can be registered with either the Client or the Server to be notified when new messages arrive.  As before, these listeners can be registered to be notified about only specific
types of messages.
ClientStateListeners can be registered with a Client to detect changes in connection state.
ConnectionListeners can be registered with a Server to be notified about HostedConnection arrivals and removals.
</p>

</div>
<!-- EDIT2 SECTION "Overview" [838-2293] -->
<h2 class="sectionedit4" id="what_s_gone">What's Gone?</h2>
<div class="level2">

<p>
All of 'connection', 'events', 'queue', 'service', 'streaming', and 'sync' are now deprecated.  The 'service', 'streaming', and 'sync' packages were too difficult to easily port to the new <abbr title="Application Programming Interface">API</abbr> and would have required additional code review for thread-related issues.  Since the service manager model has _not_ been ported and will likely live on in a different way, it was better to let these go until better solutions evolve.  For example, streaming is probably better done more tightly integrated with the core <abbr title="Application Programming Interface">API</abbr> and as actual java.io streams.
</p>

</div>
<!-- EDIT4 SECTION "What's Gone?" [2294-2866] -->
<h2 class="sectionedit5" id="migration">Migration</h2>
<div class="level2">

</div>
<!-- EDIT5 SECTION "Migration" [2867-2888] -->
<h3 class="sectionedit6" id="package_class_imports">Package/Class Imports</h3>
<div class="level3">

<p>
As a first pass, use the following table for conversion and then see specific class notes.
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Old Class </th><th class="col1"> New Class </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">com.jme3.network.connection.Client </td><td class="col1"> com.jme3.network.Client or com.jme3.network.HostedConnection </td>
	</tr>
	<tr class="row2">
		<td class="col0">com.jme3.network.connection.Server </td><td class="col1"> com.jme3.network.Server </td>
	</tr>
	<tr class="row3">
		<td class="col0">com.jme3.network.event.MessageListener </td><td class="col1"> com.jme3.network.MessageListener </td>
	</tr>
	<tr class="row4">
		<td class="col0">com.jme3.network.event.ConnectionListener </td><td class="col1"> com.jme3.network.ClientStateListener or com.jme3.network.ConnectionListener </td>
	</tr>
	<tr class="row5">
		<td class="col0">com.jme3.network.event.MessageAdapter </td><td class="col1"> no equivalent class, implement MessageListener directly </td>
	</tr>
	<tr class="row6">
		<td class="col0">com.jme3.network.event.ConnectionAdapter </td><td class="col1"> no equivalent class, implement ClientStateListener or ConnectionListener directly </td>
	</tr>
	<tr class="row7">
		<td class="col0">com.jme3.network.message.Message </td><td class="col1"> if used as a reference and not a superclass, com.jme3.network.Message.  The base class stays the same for message subclasses. </td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [3012-3793] -->
<p>
Doing all of those changes will certainly break your build… so now let's fix it.
</p>

</div>
<!-- EDIT6 SECTION "Package/Class Imports" [2889-3876] -->
<h3 class="sectionedit8" id="client_and_messagelistener">Client and MessageListener</h3>
<div class="level3">

<p>
This class is the hardest migration to perform.  Do not get discouraged.
The old version used com.jme3.network.connection.Client for both client side and server side.  So, depending on context, these references will either change to com.jme3.network.Client or com.jme3.network.HostedConnection.  In the case where calling code is not client or server specific, then there is also the common com.jme3.network.MessageConnection interface.
In general, the actual client changes are of one of the following to types:
</p>
<pre class="code java">  Client client <span class="sy0">=</span> <span class="kw1">new</span> Client<span class="br0">(</span> host, port <span class="br0">)</span><span class="sy0">;</span>
  ...<span class="me1">becomes</span>...
  <span class="me1">Client</span> client <span class="sy0">=</span> Network.<span class="me1">connectToServer</span><span class="br0">(</span> host, port <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
In the delayed connection case:
</p>
<pre class="code java">  Client client <span class="sy0">=</span> <span class="kw1">new</span> Client<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  ...
  <span class="me1">client</span>.<span class="me1">connect</span><span class="br0">(</span> host, port <span class="br0">)</span><span class="sy0">;</span>
  ...<span class="me1">becomes</span>...
  <span class="me1">NetworkClient</span> client <span class="sy0">=</span> Network.<span class="me1">createClient</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  ...
  <span class="me1">client</span>.<span class="me1">connectToServer</span><span class="br0">(</span> host, port <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
NetworkClient is a Client.  The rest of your code can just refer to Client.
Those are the easy changes.  The trickier ones are related to the MessageListeners.
</p>

</div>

<h4 id="messagelistener">MessageListener</h4>
<div class="level4">

<p>
By now you've figured out that all of your MessageListeners are broken because the new method signature is different.  The source of a message is no longer stored with the message and is instead provided to the MessageListener.
Depending on whether your MessageListener is being added to the Client or the Server, it will need to refer to either com.jme3.network.Client or com.jme3.network.HostedConnection in its messageReceived(), respectively.  The MessageListener interface is generically typed to help make sure the right listener goes where it's supposed to and so the listener implementations don't have to cast all the time.
</p>
<pre class="code java"><span class="co1">// An example client-specific listener</span>
<span class="kw1">public</span> <span class="kw1">class</span> MyClientListener <span class="kw1">implements</span> MessageListener<span class="sy0">&lt;</span>Client<span class="sy0">&gt;</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> messageReceived<span class="br0">(</span> Client source, Message m <span class="br0">)</span> <span class="br0">{</span>
       ...<span class="kw1">do</span> stuff...
    <span class="br0">}</span>
<span class="br0">}</span>
<span class="co1">// And example server-specific listener</span>
<span class="kw1">public</span> <span class="kw1">class</span> MyServerListener <span class="kw1">implements</span> MessageListener<span class="sy0">&lt;</span>HostedConnection<span class="sy0">&gt;</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> messageReceived<span class="br0">(</span> HostedConnection source, Message m <span class="br0">)</span> <span class="br0">{</span>
        ...<span class="kw1">do</span> stuff...
    <span class="br0">}</span>
<span class="br0">}</span>
<span class="co1">// A client or server listener</span>
<span class="kw1">public</span> <span class="kw1">class</span> MyGenericListener <span class="kw1">implements</span> MessageListener<span class="sy0">&lt;</span>MessageConnection<span class="sy0">&gt;</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> messageReceived<span class="br0">(</span> MessageConnection source, Message m <span class="br0">)</span> <span class="br0">{</span>
        ... <span class="kw1">do</span> limited stuff....
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Your listeners will fall into one of those three categories.
</p><p></p><div class="noteclassic">Several of the old MessageListener's methods have gone away.  The object-based methods didn't fit with the new <abbr title="Application Programming Interface">API</abbr> and messageSent() seemed of little utility.  It could be resurrected if there is demand.
</div>


</div>

<h4 id="client_method_changes">Client method changes</h4>
<div class="level4">

<p>
Some of the methods on the old Client class have changed or been removed.  Here is a basic summary:
</p>
<div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Old Method </th><th class="col1"> New Method </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Client.disconnect() </td><td class="col1"> Client.close() or HostedConnection.close(reason) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Client.kick(reason) </td><td class="col1"> HostedConnection.close(reason) </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Client.getClientID() </td><td class="col1"> Client.getId() or HostedConnection.getId() </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Client.get/setPlayerID() </td><td class="col1"> no equivalent </td>
	</tr>
	<tr class="row5">
		<td class="col0"> Client.get/setLabel() </td><td class="col1"> no equivalent </td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [6684-7000] -->
</div>

<h4 id="no_ioexceptions">No IOExceptions</h4>
<div class="level4">

<p>
After you've done all of that, the compiler will be complaining about the fact that send(), broadcast(), etc. no longer throw IOException.  So remove all of those try/catch blocks.
</p><p></p><div class="noteclassic">The truth is that even in the old <abbr title="Application Programming Interface">API</abbr>, expecting a real IOException from these methods was unreasonable because often times the message was queued and actually sent later by a separate thread.  The new <abbr title="Application Programming Interface">API</abbr> assumes that all underlying transports will operate this way and so forgoes the artificial annoyance or sense of security provided by these 'throws' clauses.  It also simplifies the calling code a great deal.

</div>
Only <abbr title="Application Programming Interface">API</abbr> methods that actually perform direct IO (such as the Network.connectToServer() and NetworkClient.connectToServer() methods) will ever be declared to throw IOException.


</div>
<!-- EDIT8 SECTION "Client and MessageListener" [3877-7811] -->
<h3 class="sectionedit10" id="messagegetclient_and_messagegetconnection">Message.getClient() and Message.getConnection()</h3>
<div class="level3">

<p>
This is important enough to deserve its own sub-heading because your code <strong>will</strong> break if you use these as they now return null.  Any reason for calling them is now provided directly to the MessageListener in the form of the source Client or source HostedConnection.
</p>

</div>
<!-- EDIT10 SECTION "Message.getClient() and Message.getConnection()" [7812-8138] -->
<h3 class="sectionedit11" id="client_id_and_player_id">Client ID and Player ID</h3>
<div class="level3">

<p>
The ID of the Client and HostedConnection are now the same at both ends of a connection and the ID is given out authoritatively by the hosting Server.  This removes some of the inconsistency on when to use the old player ID and when to use the old client ID as the new client ID serves both purposes.  This leaves the game to be able to define its own player ID based on whatever user criteria it wants.
</p><p></p><div class="noteclassic">Many of the reasons for accessing the client ID on the server can now be taken care of using the session attributes on HostedConnection.  It seems like a common use-case for these IDs was to look-up player/client-specific information in a java.util.Map.  This information can now be set directly on the HostedConnection.
</div>


</div>
<!-- EDIT11 SECTION "Client ID and Player ID" [8139-8910] -->
<h3 class="sectionedit12" id="comjme3networkeventconnectionlistener">com.jme3.network.event.ConnectionListener</h3>
<div class="level3">

<p>
Along with the shift from not using the same object at both ends of the client connection was a shift in the interfaces that are notified about those ends.
On the client, there is now com.jme3.network.ClientStateListener which is notified when the client fully connects to the server (including any internal handshaking) and when the client is disconnected.
On the server, com.jme3.network.ConnectionListener will be notified whenever new HostedConnections are added or removed.  This listener isn't notified until the connection is fully setup (including any internal handshaking).
</p>
<div class="table sectionedit13"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Old Method </th><th class="col1"> New Method </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> clientConnected(Client) </td><td class="col1"> connectionAdded(Server,HostedConnection) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> clientDisconnected(Client) </td><td class="col1"> connectionRemoved(Server,HostedConnection) </td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [9546-9720] -->
</div>
<!-- EDIT12 SECTION "com.jme3.network.event.ConnectionListener" [8911-9720] -->
<h2 class="sectionedit14" id="why_am_i_doing_this_again">Why am I doing this again?</h2>
<div class="level2">

<p>
As you've seen above, there are quite a few changes necessary to migrate to the new <abbr title="Application Programming Interface">API</abbr>.  You might be asking yourself if it's worth the trouble.
The bottom line is that the old architecture had threading and stability issues that just couldn't be fixed in any reasonable way.  Some were minor, others kind of severe… and they combined to make trouble.  If you've ever wondered why sometimes your clients connect and then the network connection hangs or stops sending data.  Or if you've ever wondered why UDP/unreliable messages get corrupted or somehow won't deserialize properly then you've run into some of these issues.
Moreover, the lack of thread safety meant that user code sometimes had to do some strange and/or complicated work-arounds.  The goal should be that the <abbr title="Application Programming Interface">API</abbr> should just work like it looks like it will with a minimum of hassle.
The new architecture is built from the ground up for threading stability and for a clean separation between the public <abbr title="Application Programming Interface">API</abbr>, the message passing layer, and the underlying network transport implementations.  You should be able to throw all kinds of stuff at it that would make the old system fall over and it should just hum along.
There will certainly be some growing pains as we work the kinks out of the new system but it is already much more stable in even the most basic of stress tests.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/network.html" class="wikilink1" title="tag:network" rel="tag">network</a>
</span></div>

</div>
<!-- EDIT14 SECTION "Why am I doing this again?" [9721-] -->
