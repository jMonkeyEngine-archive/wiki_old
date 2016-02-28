---
title: SpiderMonkey: Multi-Player Networking
---
<h1 class="sectionedit1" id="spidermonkeymulti-player_networking">SpiderMonkey: Multi-Player Networking</h1>
<div class="level1">

<p>
This document introduces you to the SpiderMonkey networking <abbr title="Application Programming Interface">API</abbr>. You use this <abbr title="Application Programming Interface">API</abbr> when you develop games where several players compete with one another in real time. A multi-player game is made up of several clients connecting to a server:
</p>
<ul>
<li class="level1"><div class="li"> The central server (one headless SimpleApplication) coordinates the game in the background.</div>
</li>
<li class="level1"><div class="li"> Each player runs a game client (a standard SimpleApplication) and connects to the central server.</div>
</li>
</ul>

<p>
Each Client keeps the Server informed about its player's moves and actions. The Server centrally maintains the game state and broadcasts the state info back to all connected clients. This network synchronization allows all clients to share the same game world. Each client then displays the game state to one player from this player's perspective.
</p>

</div>
<!-- EDIT1 SECTION "SpiderMonkey: Multi-Player Networking" [1-841] -->
<h2 class="sectionedit2" id="spidermonkey_api_overview">SpiderMonkey API Overview</h2>
<div class="level2">

<p>
The SpiderMonkey <abbr title="Application Programming Interface">API</abbr> is a set of interfaces and helper classes in the 'com.jme3.network' package.  For most users, this package and the 'message' package is all they need to worry about.  (The 'base' and 'kernel' packages only come into play when implementing custom network transports or alternate client/server protocols, which is now possible).
</p>

<p>
The SpiderMonkey <abbr title="Application Programming Interface">API</abbr> assists you in creating a Server, Clients, and Messages. Once a Server instance is created and started, the Server accepts remote connections from Clients, and you can send and receive Messages. Client objects represent the client-side of the client-server connection.  Within the Server, these Client objects are referred to as HostedConnections. HostedConnections can hold application-defined client-specific session attributes that the server-side listeners and services can use to track player information, etc.
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Seen from the Client </th><th class="col1"> </th><th class="col2"> Seen from the Server </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> com.jme3.network.Client </td><td class="col1"> == </td><td class="col2"> com.jme3.network.HostedConnection </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [1767-1885] -->
<p>
You can register several types of listeners to be notified of changes.
</p>
<ul>
<li class="level1"><div class="li"> MessageListeners on both the Client and the Server are notified when new messages arrive.  You can use MessageListeners to be notified about only specific types of messages.</div>
</li>
<li class="level1"><div class="li"> ClientStateListeners inform the Client of changes in its connection state, e.g. when the client gets kicked from the server.</div>
</li>
<li class="level1"><div class="li"> ConnectionListeners inform the Server about HostedConnection arrivals and removals, e.g. if a client joins or quits.</div>
</li>
<li class="level1"><div class="li"> ErrorListeners inform the Client about network exceptions that have happened, e.g. if the server crashes, the client throws a ConnectorException, this can be picked up so that the application can do something about it.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "SpiderMonkey API Overview" [842-2609] -->
<h2 class="sectionedit4" id="client_and_server">Client and Server</h2>
<div class="level2">

</div>
<!-- EDIT4 SECTION "Client and Server" [2610-2640] -->
<h3 class="sectionedit5" id="creating_a_server">Creating a Server</h3>
<div class="level3">

<p>
The game server is a “headless” com.jme3.app.SimpleApplication:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> ServerMain <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    ServerMain app <span class="sy0">=</span> <span class="kw1">new</span> ServerMain<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span>JmeContext.<span class="me1">Type</span>.<span class="me1">Headless</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// headless type for servers!</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
</p><p></p><div class="notetip">A <code>Headless</code> SimpleApplication executes the simpleInitApp() method and runs the update loop normally. But the application does not open a window, and it does not listen to user input. This is the typical behavior for a server application.
</div>


<p>
Create a com.jme3.network.Server in the <code>simpleInitApp()</code> method and specify a communication port, for example 6143.
</p>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    ...
    <span class="me1">Server</span> myServer <span class="sy0">=</span> Network.<span class="me1">createServer</span><span class="br0">(</span><span class="nu0">6143</span><span class="br0">)</span><span class="sy0">;</span>
    myServer.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    ...
  <span class="br0">}</span></pre>

<p>
When you run this app on a host, the server is ready to accept clients. Let's create a client next.
</p>

</div>
<!-- EDIT5 SECTION "Creating a Server" [2641-3591] -->
<h3 class="sectionedit6" id="creating_a_client">Creating a Client</h3>
<div class="level3">

<p>
A game client is a standard com.jme3.app.SimpleApplication.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> ClientMain <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    ClientMain app <span class="sy0">=</span> <span class="kw1">new</span> ClientMain<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span>JmeContext.<span class="me1">Type</span>.<span class="me1">Display</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// standard display type</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
</p><p></p><div class="notetip">A standard SimpleApplication in <code>Display</code> mode executes the simpleInitApp() method, runs the update loop, opens a window for the rendered video output, and listens to user input. This is the typical behavior for a client application.
</div>


<p>
Create a com.jme3.network.Client in the <code>simpleInitApp()</code> method and specify the servers IP address, and the same communication port as for the server, here 6143.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
   ...
   <span class="me1">Client</span> myClient <span class="sy0">=</span> Network.<span class="me1">connectToServer</span><span class="br0">(</span><span class="st0">"localhost"</span>, <span class="nu0">6143</span><span class="br0">)</span><span class="sy0">;</span>
   myClient.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
   ...</pre>

<p>
The server address can be in the format “localhost” or “127.0.0.1” (for local testing), or an IP address of a remote host in the format “123.456.78.9”. In this example, we assume the server is running on the localhost.
</p>

<p>
When you run this client, it connects to the server.
</p>

</div>
<!-- EDIT6 SECTION "Creating a Client" [3592-4757] -->
<h3 class="sectionedit7" id="getting_info_about_a_client">Getting Info About a Client</h3>
<div class="level3">

<p>
The server refers to a connected client as com.jme3.network.HostedConnection objects. The server can get info about clients as follows:
</p>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Accessor</th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">myServer.getConnections()</td><td class="col1">Server gets a collection of all connected HostedConnection objects (all connected clients).</td>
	</tr>
	<tr class="row2">
		<td class="col0">myServer.getConnections().size()</td><td class="col1">Server gets the number of all connected HostedConnection objects (number of clients).</td>
	</tr>
	<tr class="row3">
		<td class="col0">myServer.getConnection(0)</td><td class="col1">Server gets the first (0), second (1), etc, connected HostedConnection object (one client).</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [4934-5313] -->
<p>
Your game can define its own game data based on whatever criteria you want, typically these include player ID and state. If the server needs to look up player/client-specific information, you can store this information directly on the HostedConnection object. The following examples read and write a custom Java object <code>MyState</code> in the HostedConnection object <code>conn</code>:
</p>
<div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Accessor</th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> conn.setAttribute(“MyState”, new MyState()); </td><td class="col1"> Server can change an attribute of the HostedConnection. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> MyState state = conn.getAttribute(“MyState”)</td><td class="col1"> Server can read an attribute of the HostedConnection. </td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [5688-5917] -->
</div>
<!-- EDIT7 SECTION "Getting Info About a Client" [4758-5918] -->
<h2 class="sectionedit10" id="messaging">Messaging</h2>
<div class="level2">

</div>
<!-- EDIT10 SECTION "Messaging" [5919-5941] -->
<h3 class="sectionedit11" id="creating_message_types">Creating Message Types</h3>
<div class="level3">

<p>
Each message represents data that you want to transmit between client and server. Common message examples include transformation updates or game actions. For each message type, create a message class that extends com.jme3.network.AbstractMessage. Use the @Serializable annotation from com.jme3.network.serializing.Serializable and create an empty default constructor. Custom constructors, fields, and methods are up to you and depend on the message data that you want to transmit.
</p>
<pre class="code java">@<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+serializable"><span class="kw3">Serializable</span></a>
<span class="kw1">public</span> <span class="kw1">class</span> HelloMessage <span class="kw1">extends</span> AbstractMessage <span class="br0">{</span>
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> hello<span class="sy0">;</span>       <span class="co1">// custom message data</span>
  <span class="kw1">public</span> HelloMessage<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">}</span>    <span class="co1">// empty constructor</span>
  <span class="kw1">public</span> HelloMessage<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> s<span class="br0">)</span> <span class="br0">{</span> hello <span class="sy0">=</span> s<span class="sy0">;</span> <span class="br0">}</span> <span class="co1">// custom constructor</span>
<span class="br0">}</span></pre>

<p>
You must register each message type to the com.jme3.network.serializing.Serializer, in both server and client!
</p>
<pre class="code java">Serializer.<span class="me1">registerClass</span><span class="br0">(</span>HelloMessage.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT11 SECTION "Creating Message Types" [5942-6894] -->
<h3 class="sectionedit12" id="responding_to_messages">Responding to Messages</h3>
<div class="level3">

<p>
After a Message was received, a Listener responds to it. The listener can access fields of the message, and send messages back, start new threads, etc. There are two listeners, one on the server, one on the client. For each message type, you implement the responses in either Listeners’ <code>messageReceived()</code> method.
</p>

</div>

<h4 id="clientlistenerjava">ClientListener.java</h4>
<div class="level4">

<p>
Create one ClientListener.java and make it extend <code>com.jme3.network.MessageListener</code>.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> ClientListener <span class="kw1">implements</span> MessageListener<span class="sy0">&lt;</span>Client<span class="sy0">&gt;</span> <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw4">void</span> messageReceived<span class="br0">(</span>Client source, Message message<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>message <span class="kw1">instanceof</span> HelloMessage<span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// do something with the message</span>
      HelloMessage helloMessage <span class="sy0">=</span> <span class="br0">(</span>HelloMessage<span class="br0">)</span> message<span class="sy0">;</span>
      <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Client #"</span><span class="sy0">+</span>source.<span class="me1">getId</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">+</span><span class="st0">" received: '"</span><span class="sy0">+</span>helloMessage.<span class="me1">getSomething</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">+</span><span class="st0">"'"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="co1">// else...</span>
  <span class="br0">}</span></pre>

<p>
For each message type, register a client listener to the client.
</p>
<pre class="code java">myClient.<span class="me1">addMessageListener</span><span class="br0">(</span><span class="kw1">new</span> ClientListener<span class="br0">(</span><span class="br0">)</span>, HelloMessage.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>

<h4 id="serverlistenerjava">ServerListener.java</h4>
<div class="level4">

<p>
Create one ServerListener.java and make it extend <code>com.jme3.network.MessageListener</code>.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> ServerListener <span class="kw1">implements</span> MessageListener<span class="sy0">&lt;</span>HostedConnection<span class="sy0">&gt;</span> <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw4">void</span> messageReceived<span class="br0">(</span>HostedConnection source, Message message<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>message <span class="kw1">instanceof</span> HelloMessage<span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// do something with the message</span>
      HelloMessage helloMessage <span class="sy0">=</span> <span class="br0">(</span>HelloMessage<span class="br0">)</span> message<span class="sy0">;</span>
      <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Server received '"</span> <span class="sy0">+</span>helloMessage.<span class="me1">getSomething</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span><span class="st0">"' from client #"</span><span class="sy0">+</span>source.<span class="me1">getId</span><span class="br0">(</span><span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span> <span class="co1">// else....</span>
  <span class="br0">}</span></pre>

<p>
For each message type, register a server listener to the server:
</p>
<pre class="code java">myServer.<span class="me1">addMessageListener</span><span class="br0">(</span><span class="kw1">new</span> ServerListener<span class="br0">(</span><span class="br0">)</span>, HelloMessage.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT12 SECTION "Responding to Messages" [6895-8639] -->
<h3 class="sectionedit13" id="creating_and_sending_messages">Creating and Sending Messages</h3>
<div class="level3">

<p>
Let's create a new message of type HelloMessage:
</p>
<pre class="code java">Message message <span class="sy0">=</span> <span class="kw1">new</span> HelloMessage<span class="br0">(</span><span class="st0">"Hello World!"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now the client can send this message to the server:
</p>
<pre class="code java">myClient.<span class="me1">send</span><span class="br0">(</span>message<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Or the server can broadcast this message to all HostedConnection (clients):
</p>
<pre class="code java">Message message <span class="sy0">=</span> <span class="kw1">new</span> HelloMessage<span class="br0">(</span><span class="st0">"Welcome!"</span><span class="br0">)</span><span class="sy0">;</span>
myServer.<span class="me1">broadcast</span><span class="br0">(</span>message<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Or the server can send the message to a specific subset of clients (e.g. to HostedConnection conn1, conn2, and conn3): 
</p>
<pre class="code java">myServer.<span class="me1">broadcast</span><span class="br0">(</span> Filters.<span class="me1">in</span><span class="br0">(</span> conn1, conn2, conn3 <span class="br0">)</span>, message <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Or the server can send the message to all but a few selected clients (e.g. to all HostedConnections but conn4):
</p>
<pre class="code java">myServer.<span class="me1">broadcast</span><span class="br0">(</span> Filters.<span class="me1">notEqualTo</span><span class="br0">(</span> conn4 <span class="br0">)</span>, message <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The last two broadcasting methods use com.jme3.network.Filters to select a subset of recipients. If you know the exact list of recipients, always send the messages directly to them using the Filters; avoid flooding the network with unnecessary broadcasts to all.
</p>

</div>
<!-- EDIT13 SECTION "Creating and Sending Messages" [8640-9729] -->
<h2 class="sectionedit14" id="identification_and_rejection">Identification and Rejection</h2>
<div class="level2">

<p>
The ID of the Client and HostedConnection are the same at both ends of a connection. The ID is given out authoritatively by the Server.
</p>
<pre class="code java">... <span class="me1">myClient</span>.<span class="me1">getId</span><span class="br0">(</span><span class="br0">)</span> ...</pre>

<p>
A server has a game version and game name property. Each client expects to communicate with a server with a certain game name and version. Test first whether the game name matches, and then whether game version matches, before sending any messages! If they do not match, SpiderMoney will reject it for you, you have no choice in the mater. This is so the client and server can avoid miscommunication.
</p>

<p>
</p><p></p><div class="notetip">Typically, your networked game defines its own attributes (such as player ID) based on whatever criteria you want. If you want to look up player/client-specific information beyond the game version, you can set this information directly on the Client/HostedConnection object (see Getting Info About a Client).
</div>


</div>
<!-- EDIT14 SECTION "Identification and Rejection" [9730-10680] -->
<h2 class="sectionedit15" id="closing_clients_and_server_cleanly">Closing Clients and Server Cleanly</h2>
<div class="level2">

</div>
<!-- EDIT15 SECTION "Closing Clients and Server Cleanly" [10681-10727] -->
<h3 class="sectionedit16" id="closing_a_client">Closing a Client</h3>
<div class="level3">

<p>
You must override the client's destroy() method to close the connection cleanly when the player quits the client:
</p>
<pre class="code java">  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> destroy<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
      ... <span class="co1">// custom code</span>
      myClient.<span class="me1">close</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">super</span>.<span class="me1">destroy</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT16 SECTION "Closing a Client" [10728-11003] -->
<h3 class="sectionedit17" id="closing_a_server">Closing a Server</h3>
<div class="level3">

<p>
You must override the server's destroy() method to close the connection when the server quits:
</p>
<pre class="code java">  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> destroy<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
      ... <span class="co1">// custom code</span>
      myServer.<span class="me1">close</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">super</span>.<span class="me1">destroy</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

</div>
<!-- EDIT17 SECTION "Closing a Server" [11004-11260] -->
<h3 class="sectionedit18" id="kicking_a_client">Kicking a Client</h3>
<div class="level3">

<p>
The server can kick a HostedConnection to make it disconnect. You should provide a String with further info (an explanation to the user what happened, e.g. “Shutting down for maintenance”) for the server to send along. This info message can be used (displayed to the user) by a ClientStateListener. (See below)
</p>
<pre class="code java">conn.<span class="me1">close</span><span class="br0">(</span><span class="st0">"We kick cheaters."</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT18 SECTION "Kicking a Client" [11261-11651] -->
<h2 class="sectionedit19" id="listening_to_connection_notification">Listening to Connection Notification</h2>
<div class="level2">

<p>
The server and clients are notified about connection changes.
</p>

</div>
<!-- EDIT19 SECTION "Listening to Connection Notification" [11652-11763] -->
<h3 class="sectionedit20" id="clientstatelistener">ClientStateListener</h3>
<div class="level3">

<p>
The com.jme3.network.ClientStateListener notifies the Client when the Client has fully connected to the server (including any internal handshaking), and when the Client is kicked (disconnected) from the server.
</p>

<p>
</p><p></p><div class="notetip">The ClientStateListener when it receives a network exception applies the default close action. This just stops the client and you'll have to build around it so your application knows what to do. If you need more control when a network exception happens and the client closes, you may want to investigate in a ErrorListener.
</div>

<div class="table sectionedit21"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> ClientStateListener interface method </th><th class="col1"> Purpose </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> public void clientConnected(Client c){} </td><td class="col1"> Implement here what happens as soon as this client has fully connected to the server. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> public void clientDisconnected(Client c, DisconnectInfo info){} </td><td class="col1"> Implement here what happens after the server kicks this client. For example, display the DisconnectInfo to the user. </td>
	</tr>
</table></div>
<!-- EDIT21 TABLE [12348-12717] -->
<p>
First implement the ClientStateListener interface in the Client class. Then register it to myClient in MyGameClient's simpleInitApp() method:
</p>
<pre class="code java">myClient.<span class="me1">addClientStateListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT20 SECTION "ClientStateListener" [11764-12918] -->
<h3 class="sectionedit22" id="connectionlistener">ConnectionListener</h3>
<div class="level3">

<p>
The com.jme3.network.ConnectionListener notifies the Server whenever new HostedConnections (clients) come and go.  The listener notifies the server after the Client connection is fully established (including any internal handshaking).
</p>
<div class="table sectionedit23"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> ConnectionListener interface method </th><th class="col1"> Purpose </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> public void connectionAdded(Server s, HostedConnection c){} </td><td class="col1"> Implemenent here what happens after a new HostedConnection has joined the Server. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> public void connectionRemoved(Server s, HostedConnection c){} </td><td class="col1"> Implement here what happens after a HostedConnection has left. E.g. a player has quit the game and the server removes his character. </td>
	</tr>
</table></div>
<!-- EDIT23 TABLE [13184-13582] -->
<p>
First implement the ConnectionListener interface in the Server class. Then register it to myServer in MyGameServer's simpleInitApp() method. 
</p>
<pre class="code java">myServer.<span class="me1">addConnectionListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT22 SECTION "ConnectionListener" [12919-13782] -->
<h3 class="sectionedit24" id="errorlistener">ErrorListener</h3>
<div class="level3">

<p>
The com.jme3.network.ErrorListener is a listener for when network exception happens. This listener is built so that you can override the default actions when a network exception happens.
</p>

<p>
</p><p></p><div class="noteimportant">If you intend on using the default network mechanics, <strong>don't</strong> use this!
If you do override this, make sure you add a mechanic that can close the client otherwise your client will get stuck open and cause errors.
</div>

<div class="table sectionedit25"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> ErrorListener interface method </th><th class="col1"> Purpose </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> public void handleError(Client c, Throwable t){} </td><td class="col1"> Implemenent here what happens after a exception affects the network . </td>
	</tr>
</table></div>
<!-- EDIT25 TABLE [14233-14402] -->
<p>
</p><p></p><div class="notetip">This interface was built for the client and server, but the code has never been put on the server to handle this listener.
</div>


<p>
First implement the ErrorListener interface in the client class. Then you need to register it to myClient in MyGameClients's simpleInitApp() method.
</p>
<pre class="code java">myClient.<span class="me1">addErrorListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
In the class that implements the ErrorListener, a method would of been added call handleError(Client s, Throwable t). Inside this method to get you started, you going to want to listen for an error. To do this you're going to want a bit of code like this.
</p>
<pre class="code java"><span class="kw1">if</span><span class="br0">(</span>t <span class="kw1">instanceof</span> exception<span class="br0">)</span> <span class="br0">{</span>
     <span class="co1">//Add your own code here</span>
<span class="br0">}</span></pre>

<p>
Replace <strong>exception</strong> part in the <strong>if</strong> statement for the type of exception that you would like it to handle.
</p>

</div>
<!-- EDIT24 SECTION "ErrorListener" [13783-15194] -->
<h2 class="sectionedit26" id="udp_versus_tcp">UDP versus TCP</h2>
<div class="level2">

<p>
SpiderMonkey supports both UDP (unreliable, fast) and TCP (reliable, slow) transport of messages.
</p>
<pre class="code java">message1.<span class="me1">setReliable</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// TCP</span>
message2.<span class="me1">setReliable</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// UDP</span></pre>
<ul>
<li class="level1"><div class="li"> Choose reliable and slow transport for messages, if you want to make certain the message is delivered (resent) when lost, and if the order of a series of messages is relevant. E.g. game actions such as “1. wield weapon, 2. attack, 3. dodge”.</div>
</li>
<li class="level1"><div class="li"> Choose unreliable and fast transport for messages if the next message makes any previously delayed or lost message obsolete and synchronizes the state again. E.g. a series of new locations while walking.</div>
</li>
</ul>

</div>
<!-- EDIT26 SECTION "UDP versus TCP" [15195-15865] -->
<h2 class="sectionedit27" id="importantuse_multi-threading">Important: Use Multi-Threading</h2>
<div class="level2">

<p>
</p><p></p><div class="noteimportant"><strong>You cannot modify the scenegraph directly from the network thread.</strong> A common example for such a modification is when you synchronize the player's position in the scene. You have to use Java Multithreading.
</div>


<p>
Multithreading means that you create a Callable. A Callable is a Java class representing any (possibly time-intensive) self-contained task that has an impact on the scene graph (such as positioning the player). You enqueue the Callable in the Executor of the client's OpenGL thread. The Callable ensures to executes the modification in sync with the update loop.
</p>
<pre class="code java">app.<span class="me1">enqueue</span><span class="br0">(</span>callable<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Learn more about using <a href="/jme3/advanced/multithreading.html" class="wikilink1" title="jme3:advanced:multithreading">multithreading</a> in jME3 here.
</p>

<p>
For general advice, see the articles <a href="https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking" class="urlextern" title="https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking" rel="nofollow">MultiPlayer Networking</a> and <a href="https://developer.valvesoftware.com/wiki/Latency_Compensating_Methods_in_Client/Server_In-game_Protocol_Design_and_Optimization" class="urlextern" title="https://developer.valvesoftware.com/wiki/Latency_Compensating_Methods_in_Client/Server_In-game_Protocol_Design_and_Optimization" rel="nofollow">Latency Compensating Methods in Client/Server In-game Protocol Design and Optimization</a> by the Valve Developer Community.
</p>

</div>
<!-- EDIT27 SECTION "Important: Use Multi-Threading" [15866-17012] -->
<h2 class="sectionedit28" id="troubleshooting">Troubleshooting</h2>
<div class="level2">

<p>
If you have set up a server in your home network, and the game clients cannot reach the server from the outside, it's time to learn about <a href="http://portforward.com/" class="urlextern" title="http://portforward.com/" rel="nofollow">port forwarding</a>.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/network.html" class="wikilink1" title="tag:network" rel="tag">network</a>,
	<a href="/tag/spidermonkey.html" class="wikilink1" title="tag:spidermonkey" rel="tag">spidermonkey</a>
</span></div>

</div>
<!-- EDIT28 SECTION "Troubleshooting" [17013-] -->
