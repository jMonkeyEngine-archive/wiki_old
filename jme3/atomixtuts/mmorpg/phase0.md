---
title: Phase 0
---
<h2 class="sectionedit1" id="phase_0">Phase 0</h2>
<div class="level2">

<p>
<strong>Start:</strong> July 1st - August 1st 
<strong>Tasks:</strong>
</p>
<ol>
<li class="level1"><div class="li"> Search for free and open assets</div>
</li>
<li class="level1"><div class="li"> Setup MORPG engine Arriane </div>
<ol>
<li class="level2"><div class="li"> Port from 2D to 3D</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Try and review. </div>
</li>
</ol>

<p>
<strong>Features:</strong>
<strong>Bugs:</strong>
</p>

<p>
Google code Issues tracker: 
</p>

</div>
<!-- EDIT1 SECTION "Phase 0" [1-234] -->
<h2 class="sectionedit2" id="detail">Detail</h2>
<div class="level2">

</div>
<!-- EDIT2 SECTION "Detail" [235-251] -->
<h3 class="sectionedit3" id="arianne">Arianne</h3>
<div class="level3">

<p>
<a href="/resources/fetch.php" class="media" title="http://stendhalgame.org/wiki/images/3/34/Stendhal_0_65_fuzzy.png"><img src="/resources/fetch.php" class="mediacenter" alt="" /></a>
Another framework which is much small scale than Three rings is Arianne. 
<a href="http://sourceforge.net/projects/arianne/" class="urlextern" title="http://sourceforge.net/projects/arianne/" rel="nofollow">http://sourceforge.net/projects/arianne/</a>
</p>

<p>
In the phase Zero, I decided to use Arianne instead of Three rings. Why?
</p>

<p>
As I'm working in a game company, I've learnt by heart the importance of Game Design document and Workflow. And I also have fews failure attempts in the past as hobbist game developer with small team try to make BIG thing due to lack of these.
</p>

</div>

<h4 id="so_why_arianne">So Why Arianne?</h4>
<div class="level4">

<p>
Because it's Open source, simple, have enough features, easy to deploy, test, and most important very well documented compare to Three rings.
</p>

</div>

<h4 id="features">Features</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> </div>
</li>
<li class="level1"><div class="li">     Stendhal - MORPG featuring hundreds of NPCs and quests</div>
</li>
<li class="level1"><div class="li">     Stendhal - Huge and beautiful world to explore</div>
</li>
<li class="level1"><div class="li">     Stendhal - Statistics website and Hall of Fame</div>
</li>
<li class="level1"><div class="li">     Marauroa - Game server handling client-server communication</div>
</li>
<li class="level1"><div class="li">     Marauroa - Database persistence with asychronous access</div>
</li>
<li class="level1"><div class="li">     Marauroa - Flexibility of game rules. Apply to drawing boards, card games, PacMan …</div>
</li>
<li class="level1"><div class="li">     Keep It Simple approach</div>
</li>
<li class="level1"><div class="li">     Release early, release often</div>
</li>
<li class="level1"><div class="li">     Automatic client updates</div>
</li>
<li class="level1"><div class="li">     Detailed tutorials to extend Stendhal or get started with Marauroa</div>
</li>
<li class="level1"><div class="li">     Supportive development team in <abbr title="Internet Relay Chat">IRC</abbr></div>
</li>
</ul>

<p>
It's wiki with a lot of tutorials of making Quest and NPC, scripting:
<a href="http://stendhalgame.org/wiki/" class="urlextern" title="http://stendhalgame.org/wiki/" rel="nofollow">http://stendhalgame.org/wiki/</a>
</p>

</div>
<!-- EDIT3 SECTION "Arianne" [252-1680] -->
<h3 class="sectionedit4" id="marauroa_and_stendhal_base_architecture">Marauroa and Stendhal base architecture</h3>
<div class="level3">

<p>
<a href="https://stendhalgame.org/wiki/Marauroa_Core_API" class="urlextern" title="https://stendhalgame.org/wiki/Marauroa_Core_API" rel="nofollow">https://stendhalgame.org/wiki/Marauroa_Core_API</a>
</p>

<p>
<a href="https://stendhalgame.org/wiki/RolePlayingDesign" class="urlextern" title="https://stendhalgame.org/wiki/RolePlayingDesign" rel="nofollow">https://stendhalgame.org/wiki/RolePlayingDesign</a>
</p>

<p>
<a href="https://stendhalgame.org/wiki/NetworkDesign" class="urlextern" title="https://stendhalgame.org/wiki/NetworkDesign" rel="nofollow">https://stendhalgame.org/wiki/NetworkDesign</a>
</p>

<p>
<a href="https://stendhalgame.org/wiki/HowToWriteAdventureGamesUsingArianne#Multiplayer_fun" class="urlextern" title="https://stendhalgame.org/wiki/HowToWriteAdventureGamesUsingArianne#Multiplayer_fun" rel="nofollow">https://stendhalgame.org/wiki/HowToWriteAdventureGamesUsingArianne#Multiplayer_fun</a>
</p>

<p>
</p><p></p><div class="noteimportant">Copy from Stendhal wiki
</div>


</div>

<h4 id="main_entities">Main entities</h4>
<div class="level4">

<p>
The main entities you should know about are:
</p>
<ul>
<li class="level1"><div class="li"> Attributes</div>
</li>
<li class="level1"><div class="li"> RPAction</div>
</li>
<li class="level1"><div class="li"> RPObject</div>
</li>
<li class="level1"><div class="li"> RPSlot</div>
</li>
<li class="level1"><div class="li"> RPClass</div>
</li>
<li class="level1"><div class="li"> IRPZone interface</div>
</li>
<li class="level1"><div class="li"> IRPRuleProcessor interface</div>
</li>
<li class="level1"><div class="li"> RPWorld </div>
</li>
</ul>

</div>

<h4 id="role_playing_design">Role Playing Design</h4>
<div class="level4">

<p>
is the determining factor on how easy is to create a new game for Arianne. We had to choose easing the creation of turn time limited based games. Arianne will work better with this kind of games (also known as realtime games).
</p>

<p>
 Role Playing Design tries to be generic and game agnostic (independant of the game being made). The very basic idea behind RPManager is:
</p>
<pre class="code">forever
  {
  Execute Actions
  Send Perceptions
  Wait for next turn
  }</pre>

<p>
To achieve this we use several classes:
</p>

<p>
<strong>RPManager</strong> is coded in Marauroa and doesn't need to be modified.
</p>

<p>
<strong>IRPRuleProcessor</strong> is the interface that you need to modify in order to personalize the actions that your game will execute.
</p>

<p>
<strong>RPWorld</strong> is the class that you need to extend inorder to implement the onInit and onFinish methods which personalize what happens when you initialise the server and what happens when you close the server.
</p>

<p>
<strong>IRPZone</strong> is an interface that you could implement if you wanted to achive the highest personalization possible of the engine, however, I would use MarauroaRPZone instead as that uses our great <strong>Delta2</strong> feature. 
</p>

</div>

<h4 id="actions">Actions</h4>
<div class="level4">

<p>
To express the willingness of a client to do something it must send the server a MessageC2SAction message.
</p>

<p>
An action is composed of several attributes. (an attribute is similar to a variable in that it has a name and contains a value).
</p>

<p>
There are optional and mandatory attributes. If a mandatory attribute is not found, the message is skipped by the RPServerManager.
</p>

<p>
Mandatory Action Attributes are action_id and type.
</p>

<p>
The action_id is used to identify the action when a resulting response comes in a perception
</p>

</div>

<h4 id="perceptions">Perceptions</h4>
<div class="level4">

<p>
The basic structure for sending world updates to clients is called perceptions.
</p>

<p>
There are two types of perception:
</p>
<pre class="code">  Sync perceptions: these are used to synchronize clients with the server world representation. This is the only valid way of knowing world's status.
  Delta perception: this is used to send only the changes to the world since the last perception. </pre>

<p>
Our actual Perception system is called Delta2. It is heavily attached to the Marauroa core, so I recommend you to use it :)
How Perceptions and Actions work
</p>

<p>
Actions are sent from the client to the server in order to make the character perform an action. In order for the client to know the result of the action the Server needs to send a reply to the client. How will this be done?
</p>

<p>
In a first attempt, we send clients back an action that was the result of their action. However, this made the code really hard because we had to update two different things, perceptions and actions. Instead the solution appears intuitively: Why not join action reply and perceptions.
</p>

<p>
So the action reply is stored inside each object (that executed the action ) with a set of attributes that determine the action return status and the attributes. This way of doing replies makes it a bit harder on RPManager but it simplifies the creation of new clients a lot.
</p>

<p>
See Actions reply in the Objects documentation to know exactly what is returned. However, keep in mind that the return result depends of each particular game.
Delta2 perception Algorithm
</p>

<p>
The idea behind the DPA is to avoid sending ALL the objects to a client each time, but only those that have been modified.
</p>

<p>
Imagine that we have 1000 objects, and only O1 and O505 are active objects that are modified each turn.
</p>

<p>
The Traditional method:
</p>
<ul>
<li class="level1"><div class="li"> - Get objects that our player should see ( 1000 objects )</div>
</li>
<li class="level1"><div class="li"> - Send them to player ( 1000 objects )</div>
</li>
<li class="level1"><div class="li"> - Next turn</div>
</li>
<li class="level1"><div class="li"> - Get objects that our player should see ( 1000 objects )</div>
</li>
<li class="level1"><div class="li"> - Send them to player</div>
</li>
<li class="level1"><div class="li"> - Next turn</div>
</li>
</ul>

<p>
…
</p>

<p>
I hope you see the problem… we are sending objects that haven't changed each turn.
</p>

<p>
The delta perception algorithm:
</p>
<ul>
<li class="level1"><div class="li"> Get objects that our player should see ( 1000 objects )</div>
</li>
<li class="level1"><div class="li"> Reduce the list to the modified ones ( 1000 objects )</div>
</li>
<li class="level1"><div class="li"> Store also the objects that are not longer visible ( 0 objects )</div>
</li>
<li class="level1"><div class="li"> Send them to player ( 1000 objects )</div>
</li>
<li class="level1"><div class="li"> Next turn</div>
</li>
<li class="level1"><div class="li"> Get objects that our player should see ( 1000 objects )</div>
</li>
<li class="level1"><div class="li"> Reduce the list to the modified ones ( 2 objects )</div>
</li>
<li class="level1"><div class="li"> Store also the objects that are not longer visible ( 0 objects )</div>
</li>
<li class="level1"><div class="li"> Send them to player ( 2 objects )</div>
</li>
<li class="level1"><div class="li"> Next turn</div>
</li>
<li class="level1"><div class="li"> …</div>
</li>
</ul>

<p>
The next step of the delta perception algorithm is pretty clear: delta2 The idea is to send only what changes of the objects that changed. This way we save even more bandwidth, making perceptions around 20% of the original delta perception size.
</p>

<p>
The delta2 algorithm is based on four containers:
</p>
<ul>
<li class="level1"><div class="li">     List of added objects</div>
</li>
<li class="level1"><div class="li">     List of modified added attributes of objects</div>
</li>
<li class="level1"><div class="li">     List of modified deleted attributes of objects</div>
</li>
<li class="level1"><div class="li">     List of deleted objects </div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Marauroa and Stendhal base architecture" [1681-6968] -->
<h3 class="sectionedit5" id="plan">Plan</h3>
<div class="level3">

<p>
My initial plan for the phase Zero is to create a port to 3d version of the existed game Stendhal with free 3d models and 3d gameplay. Then I let the team go in, try and discuss, learn, design as much as possible before we going futher.
</p>

</div>

<h4 id="assets">Assets</h4>
<div class="level4">

<p>
In the first attempt, 3d enviroment and models will use open art website such as: 
Blendswap <a href="http://blendswap.com" class="urlextern" title="http://blendswap.com" rel="nofollow">http://blendswap.com</a>
OpengameArt <a href="http://opengameart.com" class="urlextern" title="http://opengameart.com" rel="nofollow">http://opengameart.com</a>
</p>

<p>
and other resources to quick made up a workable game (client and server) to test and enjoy.
</p>

</div>

<h4 id="from_arianne_to_jme3">From Arianne to jME3</h4>
<div class="level4">

<p>
The reusable:
</p>
<ul>
<li class="level1"><div class="li">     Network: Good for small scale game</div>
</li>
<li class="level1"><div class="li">     DB: MySQL or integrated H2</div>
</li>
<li class="level1"><div class="li">     Almost gameplay: Enities definition, Quest, Scripting</div>
</li>
<li class="level1"><div class="li">     They also have a complete website for the game with tutorials, wiki </div>
</li>
</ul>

<p>
The different between a 2d and 3d, Arianne an jME3 engine:
</p>
<ul>
<li class="level1"><div class="li"> </div>
</li>
<li class="level1"><div class="li">     Replace the Arianne game loop with jME3 states and update loop.</div>
</li>
<li class="level1"><div class="li">     Delete the Render task of the game view JPanel</div>
</li>
<li class="level1"><div class="li">     Terrain : I have my own tiled Terrain implement in jME3 for almost top-down game.</div>
</li>
<li class="level1"><div class="li">     Characters: Use 3D Models of Open Art resource</div>
</li>
<li class="level1"><div class="li">     <abbr title="Graphical User Interface">GUI</abbr> : Use pure swing gui (port to Nifty later)</div>
</li>
<li class="level1"><div class="li">     2d to 3d Gameplay: Map entities, trigger</div>
</li>
<li class="level1"><div class="li">     2d to 3d Picking : I use a simple translation </div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Plan" [6969-8235] -->
<h2 class="sectionedit6" id="concepts">Concepts</h2>
<div class="level2">

<p>
Pictures
</p>

<p>
Videos
</p>

</div>
<!-- EDIT6 SECTION "Concepts" [8236-8274] -->
<h2 class="sectionedit7" id="assets1">Assets</h2>
<div class="level2">

</div>
<!-- EDIT7 SECTION "Assets" [8275-8293] -->
<h3 class="sectionedit8" id="d">3D</h3>
<div class="level3">

</div>
<!-- EDIT8 SECTION "3D" [8294-8308] -->
<h3 class="sectionedit9" id="textures">Textures</h3>
<div class="level3">

</div>
<!-- EDIT9 SECTION "Textures" [8309-8329] -->
<h3 class="sectionedit10" id="animations">Animations</h3>
<div class="level3">

</div>
<!-- EDIT10 SECTION "Animations" [8330-8353] -->
<h2 class="sectionedit11" id="programming">Programming</h2>
<div class="level2">

</div>
<!-- EDIT11 SECTION "Programming" [8354-8379] -->
<h2 class="sectionedit12" id="use_of_tools">Use of tools</h2>
<div class="level2">

</div>
<!-- EDIT12 SECTION "Use of tools" [8380-8406] -->
<h3 class="sectionedit13" id="something_to_try">Something to try</h3>
<div class="level3">

</div>

<h4 id="citygen_dungeon_maker">CityGen dungeon maker</h4>
<div class="level4">

</div>
<!-- EDIT13 SECTION "Something to try" [8407-] -->
