---
title: Open Game Finder
---
<h1 class="sectionedit1" id="open_game_finder">Open Game Finder</h1>
<div class="level1">

<p>
The Open Game Finder (OGF) by Mark Schrijver can be plugged into any Java game. OGF enables you to find other people playing the same multiplayer game, and join them.
</p>
<ul>
<li class="level1"><div class="li"> Homepage: <a href="http://code.google.com/p/open-game-finder/" class="urlextern" title="http://code.google.com/p/open-game-finder/" rel="nofollow">http://code.google.com/p/open-game-finder/</a></div>
</li>
<li class="level1"><div class="li"> Documentation: <a href="http://code.google.com/p/open-game-finder/w/list" class="urlextern" title="http://code.google.com/p/open-game-finder/w/list" rel="nofollow">http://code.google.com/p/open-game-finder/w/list</a></div>
</li>
</ul>

<p>
Both on the client and the server side of OGF is written purely in Java. OGF has a pluggable architecture and comes with a full set of plugins to get the job done. You can add your own plugins, or replace existing plugins to make them more in line with your game. OGF uses NiftyGUI as the main <abbr title="Graphical User Interface">GUI</abbr> plugin.
</p>

</div>
<!-- EDIT1 SECTION "Open Game Finder" [1-629] -->
<h2 class="sectionedit2" id="installation">Installation</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Go to <a href="http://code.google.com/p/open-game-finder/downloads/list" class="urlextern" title="http://code.google.com/p/open-game-finder/downloads/list" rel="nofollow">http://code.google.com/p/open-game-finder/downloads/list</a></div>
</li>
<li class="level1"><div class="li"> Download Client-1.0-bin.zip and Server-1.0-bin.zip</div>
</li>
<li class="level1"><div class="li"> Unzip the two files to, for example, your jMonkeyProjects directory.</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Installation" [630-849] -->
<h2 class="sectionedit3" id="setting_up_the_database">Setting up the Database</h2>
<div class="level2">

<p>
The OGF server uses an embedded Apache Derby database. You have to install the database, this means creating the data files and adding the tables. You can do this straight from the command line by running a script file.
</p>
<ul>
<li class="level1"><div class="li"> On Windows, use installServer.bat to create a new database from scratch. On Mac <abbr title="Operating System">OS</abbr> or Linux, run <code>java -jar lib/Server-0.1.jar install</code> in the Terminal.</div>
</li>
<li class="level1"><div class="li"> On Windows, use updateServer.bat to update the difference between the current state of the database and the way it should be. On Mac <abbr title="Operating System">OS</abbr> and Linux, run <code>java -jar lib/Server-0.1.jar update</code> in the Terminal. <br />
<strong>This new feature is currently untested.</strong></div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Setting up the Database" [850-1523] -->
<h2 class="sectionedit4" id="running_the_server">Running the server</h2>
<div class="level2">

<p>
Change into the OGF-Server directory and run the server:
</p>
<ul>
<li class="level1"><div class="li"> On Windows: Run startServer.bat</div>
</li>
<li class="level1"><div class="li"> On Linux and MacOS X: Run <code>java -jar lib/Server-1.0.jar</code> in the Terminal.</div>
</li>
</ul>

<p>
The server is now running and ready to accept connections. <br />

<strong>Note:</strong> In the alpha release, the server runs on localhost. In the final release, you will be able to configure the host!
</p>

</div>
<!-- EDIT4 SECTION "Running the server" [1524-1913] -->
<h2 class="sectionedit5" id="running_the_client">Running the client</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Change into the OGF-Client directory and run the client:</div>
<ul>
<li class="level2"><div class="li"> On Windows: Run startClient.bat</div>
</li>
<li class="level2"><div class="li"> On Linux and MacOS X: Run <code>java -jar lib/Client-1.0.jar</code> in the Terminal.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> If a Display Settings window appears, you can keep the defaults and click OK.</div>
</li>
</ol>

<p>
A client is now running, connects to the server, and displays a registration/login window.
<a href="/resources/jme3-advanced-open-game-finder-1.png" class="media" title="jme3:advanced:open-game-finder-1.png"><img src="/resources/jme3-advanced-open-game-finder-1.png" class="mediacenter" alt="" /></a>
<strong>Note:</strong> You can run several clients on localhost for testing.
</p>

</div>
<!-- EDIT5 SECTION "Running the client" [1914-2406] -->
<h3 class="sectionedit6" id="client1_registration">Client: 1. Registration</h3>
<div class="level3">

<p>
If clients use OGF for the first time, they need to register.
On the main screen of the client:
</p>
<ol>
<li class="level1"><div class="li"> Click Register</div>
</li>
<li class="level1"><div class="li"> Choose a user name and password (repeat the password).</div>
</li>
<li class="level1"><div class="li"> Select an Avatar image.</div>
</li>
<li class="level1"><div class="li"> Click register to complete the registration.</div>
</li>
</ol>

<p>
The client registers the account and opens the chat window directly.
</p>

</div>
<!-- EDIT6 SECTION "Client: 1. Registration" [2407-2760] -->
<h3 class="sectionedit7" id="client2_login">Client: 2. Login</h3>
<div class="level3">

<p>
If returning clients are already registered to an OGF server, they can log in.
On the main screen of the client:
</p>
<ol>
<li class="level1"><div class="li"> Enter a user name and password that you previously registered.</div>
</li>
<li class="level1"><div class="li"> Click Login</div>
</li>
</ol>

<p>
The client logs you in and opens the chat window.
</p>

</div>
<!-- EDIT7 SECTION "Client: 2. Login" [2761-3033] -->
<h3 class="sectionedit8" id="client3_chat">Client: 3. Chat</h3>
<div class="level3">

<p>
The chat window shows a list of all users logged in to the server. Logged-in users can send public messages, and can receive public messages from others.
</p>

</div>
<!-- EDIT8 SECTION "Client: 3. Chat" [3034-3213] -->
<h2 class="sectionedit9" id="connecting_to_a_game">Connecting to a Game</h2>
<div class="level2">

<p>
Q: I want to gather players using the OGF client to connect to the game server. How do I start my multiplayer game? <br />

A: The following sample code demos the typical use case: <a href="http://code.google.com/p/open-game-finder/source/browse/OGF/TRUNK/Client/src/main/java/com/ractoc/opengamefinder/client/OGFClientStartup.java" class="urlextern" title="http://code.google.com/p/open-game-finder/source/browse/OGF/TRUNK/Client/src/main/java/com/ractoc/opengamefinder/client/OGFClientStartup.java" rel="nofollow">OGFClientStartup.java</a>
<br />

In a JME3 Application's init method:
</p>
<ol>
<li class="level1"><div class="li"> Create a com.ractoc.opengamefinder.client.GUIContainer object.</div>
</li>
<li class="level1"><div class="li"> Create a game instance using the GUIContainer (via a ClientFactory).</div>
</li>
<li class="level1"><div class="li"> Check the com.ractoc.pffj.api.BasePluginMessageResult for success or failure.</div>
</li>
</ol>

<p>
After this, continue writing your JME3 init method.
</p>

</div>
<!-- EDIT9 SECTION "Connecting to a Game" [3214-3904] -->
<h2 class="sectionedit10" id="configuration">Configuration</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> Q: How can I offer more avatars to choose from? <br />
A: Save the image files in the path <code>jMonkeyProjects/OGF-Client-1.0-bin/OGF/resources/avatars/</code></div>
</li>
<li class="level1"><div class="li"> Q: How do I configure servers addresses? <br />
A: TBD</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/network.html" class="wikilink1" title="tag:network" rel="tag">network</a>
</span></div>

</div>
<!-- EDIT10 SECTION "Configuration" [3905-] -->
