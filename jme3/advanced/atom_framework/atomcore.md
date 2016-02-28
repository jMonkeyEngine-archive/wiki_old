---
title: AtomCore Introduction
---
<h2 class="sectionedit1" id="atomcore_introduction">AtomCore Introduction</h2>
<div class="level2">

<p>
AtomCore is the main component of Atom framework.
</p>

<p>
This is the detailed documentation of AtomCore module architecture, design decisions, implementations and real usecases, examples, resources.
</p>

<p>
Source: <a href="https://code.google.com/p/atom-game-framework/source/browse/AtomCore/" class="urlextern" title="https://code.google.com/p/atom-game-framework/source/browse/AtomCore/" rel="nofollow">https://code.google.com/p/atom-game-framework/source/browse/AtomCore/</a>
</p>

<p>
Javadoc: 
</p>

<p>
Issues:
</p>

<p>
Quick links: <em>Read if you know ready know the basic</em>
</p>

<p>
<a href="/jme3/advanced/atom_framework/atomcore/cycle.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore:cycle">AtomCore Cycle</a>
</p>

<p>
<a href="/jme3/advanced/atom_framework/design/patterns.html" class="wikilink1" title="jme3:advanced:atom_framework:design:patterns">AtomCore patterns</a>
</p>

<p>
<a href="/jme3/advanced/atom_framework/atomcore/algorithms.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore:algorithms">AtomCore algorithms</a>
</p>

</div>
<!-- EDIT1 SECTION "AtomCore Introduction" [1-587] -->
<h2 class="sectionedit2" id="architecture_design">Architecture Design</h2>
<div class="level2">

<p>
Atom philosophy is “Minimal”, “Only one”.
</p>

<p>
As a software modeler, you always need more than one thing to decribe your solutions. Atom try to compact them into mimimal sets and if possible, only one piece of consistent but flexible design.
</p>

<p>
As a developer, you may find it easy to adapt and extend the framework to suite your games and purpose.
</p>

<p>
Now talk about the most primitive “Core” design of the framework is a “Relationship” between the “Core” and the “Container”. This also the most important concept of philosophy of the universe, sciences and of course programming.
</p>

<p>
AtomCore leverages Java programming with concepts and ultilities for various pairs of Core-Container (common in game development) such as: Actor &amp; Stage, Player &amp; League, Task &amp; Manager, Worker &amp; Thread, Entity &amp; Context, UI &amp; Layout, Stream &amp; Pipeline, Pipeline &amp; Topology…
</p>

<p>
Beside of those common basis pairs, collections, graphs and other datastructure, executions, pattern and behaviours are also supported!
</p>

<p>
The details of those techniques will be listed below.
</p>

</div>
<!-- EDIT2 SECTION "Architecture Design" [588-1663] -->
<h3 class="sectionedit3" id="the_core_features">The core features:</h3>
<div class="level3">

<p>
Features of AtomCore
</p>
<ul>
<li class="level1"><div class="li"> Cross game-genre elements: stage, cycle, entity, logic, trigger, event, config;</div>
</li>
<li class="level1"><div class="li"> Managers and management: Advanced assets manager, IOC, AOP, dependecy injection, factory, scripting, basic DB..;</div>
</li>
<li class="level1"><div class="li"> Common case: Common state, common scenerio, common UIs…</div>
</li>
</ul>

<p>
Below you will read about how each feature is implemented in AtomCore.
</p>

</div>

<h4 id="cross_game-genre_elements">Cross game-genre elements</h4>
<div class="level4">

<p>
From an abstraction level, a Game- a special kind of software (almost always):
</p>
<ul>
<li class="level1"><div class="li"> composed by Entities, and their Stage; </div>
</li>
<li class="level1"><div class="li"> where Actions happen in a Cycle, procedure Events;</div>
</li>
</ul>

<p>
A little bit more detailed, Gameplay is the way player play the Game, has:
</p>
<ul>
<li class="level1"><div class="li"> Logic:</div>
<ul>
<li class="level2"><div class="li"> Trigger: in which Conditions, active some appropriate Action, as primitive brick.</div>
</li>
<li class="level2"><div class="li"> Rule: the laws, restrictions form the game rule which player, entities obey.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Routines: Situations/ Events/ Actions that happen in the game Cycle.</div>
<ul>
<li class="level2"><div class="li"> Story/Cinematic mode: When player just watch the game like a movie.</div>
</li>
<li class="level2"><div class="li"> Interactive mode: When player interact with the game world</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Control: The way player handle their entities</div>
</li>
<li class="level1"><div class="li"> League: </div>
<ul>
<li class="level2"><div class="li"> Player, Matchs, Groups and their infos &amp; activities</div>
</li>
<li class="level2"><div class="li"> Single: Infos, score, rewards stick to an individual </div>
</li>
<li class="level2"><div class="li"> Multi: The way players join, left, make friend and interactive and play together…</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Status: Way to pause/continue , save/load current game</div>
</li>
</ul>

<p>
The game “software” should be published in specific enviroment called Context, it then has:
</p>
<ul>
<li class="level1"><div class="li"> Configurations : appropriate settings for specific enviroment, device.</div>
</li>
<li class="level1"><div class="li"> Data : appropriate size and format</div>
</li>
</ul>

</div>

<h5 id="around_bean">Around Bean</h5>
<div class="level5">

<p>
</p><p></p><div class="noteclassic">This is so important to mention that every techs Atom framework are around Bean/ POJO technologies. 
</div>


<p>
In <a href="/jme3/advanced/atom_framework/atomcore/beans.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore:beans">AtomCore Bean</a> are leverage in a few ways:
</p>
<ul>
<li class="level1"><div class="li"> Modeling</div>
</li>
<li class="level1"><div class="li"> Generating</div>
</li>
<li class="level1"><div class="li"> Binding</div>
</li>
<li class="level1"><div class="li"> Mapping / Morphing</div>
</li>
<li class="level1"><div class="li"> Instropecting</div>
</li>
<li class="level1"><div class="li"> Managed</div>
</li>
</ul>

</div>

<h5 id="attend_cycle">Attend Cycle</h5>
<div class="level5">

<p>
In JME3 we almost see the things work like this, the “almighty” Cycle:
</p>

<p>
<a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:update_loop" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:update_loop" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:update_loop</a>
</p>
<ol>
<li class="level1"><div class="li"> Input listeners respond to mouse clicks and keyboard presses – Input handling</div>
</li>
<li class="level1"><div class="li"> Update game state:</div>
<ol>
<li class="level2"><div class="li"> Update overall game state – Execute Application States</div>
<ol>
<li class="level3"><div class="li"> User code update – Execute simpleUpdate() method</div>
</li>
<li class="level3"><div class="li"> Logical update of entities – Execute Custom Controls</div>
</li>
</ol>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Render audio and video</div>
<ol>
<li class="level2"><div class="li"> Application States rendering.</div>
</li>
<li class="level2"><div class="li"> Scene rendering.</div>
</li>
<li class="level2"><div class="li"> User code rendering – Execute simpleRender() method.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Repeat loop.</div>
</li>
</ol>

<p>
The reason this cycle exists is because of JME3 application tied strictly with monotholic processing method, and the main convict is OpenGL.
</p>

<p>
In Atom, is not actually the case!! Atom try to connect various parts of facilities in networks and try to run as independent-parallel as it can. Cycle defined as a pre-ordered routine is not suiable with the work of parallel processing and enterprise… That's why a sotiphicated customable-expandable “cycle” is the heart to Atom framework which made it a solid replacement of “old” JME3 cycle. 
</p>

<p>
Read more details in AtomCore's Cycle.
</p>

<p>
<span class="curid"><a href="/jme3/advanced/atom_framework/atomcore.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore">atomcore</a></span>
</p>

</div>

<h5 id="as_core_of_a_whole_enterprise">As core of a whole Enterprise</h5>
<div class="level5">

<p>
As a long term follower of Spring (one of Atom inspiration) : 
<a href="http://spring.io/" class="urlextern" title="http://spring.io/" rel="nofollow">http://spring.io/</a>  …
<a href="http://en.wikipedia.org/wiki/Spring_framework" class="urlextern" title="http://en.wikipedia.org/wiki/Spring_framework" rel="nofollow">http://en.wikipedia.org/wiki/Spring_framework</a>
</p>

<p>
I learnt few things,eventually Spring is for Enterprise, so most of its features is accessed through AtomEx, but AtomCore will have some of its goods to be integrated later.
</p>

<p>
<a href="/jme3/advanced/atom_framework/atomex.html" class="wikilink1" title="jme3:advanced:atom_framework:atomex">atomex</a>
</p>

</div>
<!-- EDIT3 SECTION "The core features:" [1664-5213] -->
<h3 class="sectionedit4" id="atomcore_concepts">AtomCore concepts</h3>
<div class="level3">
<pre class="code"> From the cross-genre games elements mentioned above, AtomCore introduce some concepts which latter implemented in classes in appropriate packages.</pre>

</div>

<h5 id="entity">Entity</h5>
<div class="level5">

</div>

<h5 id="managers">Managers</h5>
<div class="level5">

<p>
AtomCore introduce the concepts of Manager (then Helper, Worker, Actor later). What are they?
</p>

<p>
Managers are useful objects (usually Singleton) to manage aspects of a game, such as Rendering,  Sounds, World, Assets, Networks, Effects, etc…
</p>

<p>
Managers are born to help developer manage/ monitor/ manipulate every conner/ moment/ objects in the game code base and run-time activites.
</p>

<p>
Manager is the concept of who have responsibities and power over others (as its children or employee in the real world), essentially it is a list of its children, and have basic opertions like add,remove to manage that list… You can also think about it as the Control of the MVC paradigm where it is the mediator between Model and View. In JME3, you see Manager every where such as AssetManager, StateManager as the wraper of underlying functions. So, event mixed up quite a lot concepts at once, Manager in Scripting is extremely useful and fullfill the missing piece of the picture we are painting for a while here.
</p>

<p>
To clean the mist of confusion about mixed of concepts a little bit, there are some practical wisdoms about Manager implementation:
</p>
<pre class="code">  Manager acts globally, handy: usually a Singleton, or really easy to reference in script
  Manager wrap underlying details in intuitive way
  Manager share common informations
  Manager executions are frequently : like in an default update cycle
  Manager have power over its children : its handle it children; in almost scenarios child has left its Manager's list come hollow (as null)</pre>

<p>
Entity related - Managers can be considered as the other piece in constrast with Entity, as it manage entity existing and activities. 
</p>

<p>
Also note that Managers normally form a Tree, with Hierarchy or dependency as commonly seen in OOP.
</p>

<p>
But, the Manager-Entity system is not forced to be in relationship with each other! If work as a flat array, the Manager system can be transform to a Component process as seen in COP. This open a door to integrated deeply with Component base solutions as describled below.
</p>

</div>

<h5 id="actor">Actor</h5>
<div class="level5">

</div>

<h5 id="task_worker">Task &amp; Worker</h5>
<div class="level5">

</div>

<h5 id="helper">Helper</h5>
<div class="level5">

</div>

<h5 id="component_base_solution">Component base solution</h5>
<div class="level5">

<p>
</p><p></p><div class="noteimportant">We (forum members) and game devs all over the world also have controversial conversations, debates and judgments about it. But I have to admit its an undeniable trend game maker all head into in the next decade as the revolution of GPU, CPU employ data oriented approach and batch processing a lot.
</div>


<p>
You can read about Component base solutions and architecture here:
</p>

<p>
In AtomCore I sketch some interface of ES in which not care much about the implementation of the ES (pure data, smart bean, DB backed what ever…), open possiblities to intergrated ES libs in Atom framework.
</p>

</div>

<h4 id="common_implementations">Common implementations</h4>
<div class="level4">
<pre class="code">  Of course a framewok is almost meaningless if it just contain psuedo code or interfaces without inplementation. I also implemented some common and useful piecies of code which ready to use :p. </pre>

</div>

<h5 id="common_cycle">Common Cycle</h5>
<div class="level5">

<p>
The first thing should be mentioned, as essentital to the framework is root of the game activities: the Cycle - Ordered activities that repeat over and over!
</p>

<p>
My basic form of game Cycle aka CommonCycle crafted to work well with AppState concept of JME3 and other existed Managers (StateManager, AssetManager, InputManager..).
</p>

<p>
The Cycle consist 6 basis methods:
</p>
<ol>
<li class="level1"><div class="li"> init : Lazy init and be injected with its dependencies declaretion</div>
</li>
<li class="level1"><div class="li"> load : Load assets or underlying data (later than its dependencies) </div>
</li>
<li class="level1"><div class="li"> config : reconfig if need, even in update</div>
</li>
<li class="level1"><div class="li"> start : trigger start a working routine of the object</div>
</li>
<li class="level1"><div class="li"> update</div>
</li>
<li class="level1"><div class="li"> end</div>
</li>
</ol>

<p>
why 6? Why cycle? The customizable version of cycle? Introduce new cycles, queues and stuffs. read <a href="/jme3/advanced/atom_framework/atomcore/cycle.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore:cycle">cycle</a>
</p>

</div>

<h4 id="common_scenarios">Common scenarios</h4>
<div class="level4">

<p>
Common scenarios that almost every game have, help you to startup easily. That mean the code is there in the library, you can also overide because its very extensible!
</p>
<ul>
<li class="level1"><div class="li"> Manage entities: add/remove/select </div>
</li>
<li class="level1"><div class="li"> Composable logic: with condition, trigger</div>
</li>
<li class="level1"><div class="li"> Event messaging system (network ready): as inner / outter communicate media with eventbus and non blocking network</div>
</li>
<li class="level1"><div class="li"> Provide user functions and controls: As State, Control, Actors</div>
</li>
<li class="level1"><div class="li"> Game status persistent: Save/ Load/ Replay</div>
</li>
<li class="level1"><div class="li"> Routines: Interactive / non interactive as Cycle change to InteractiveMode or CinematicMode. Handle Tasks, Actions in good concurent way (multi threading, actor..).</div>
</li>
<li class="level1"><div class="li"> Easy UI making: as common ui below</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "AtomCore concepts" [5214-9887] -->
<h2 class="sectionedit5" id="common_scenarios_detailed">Common scenarios Detailed</h2>
<div class="level2">

</div>
<!-- EDIT5 SECTION "Common scenarios Detailed" [9888-9924] -->
<h3 class="sectionedit6" id="game_related">Game related</h3>
<div class="level3">

</div>

<h4 id="managed_entities">Managed entities</h4>
<div class="level4">

<p>
The AtomCore offer (but not forced) you a way to manage “your entities (game objects) embeded to a scenegraph” . This is the distinct point that made AtomCore entity difference with “other” entity framework (component entity, pure data, …)
</p>

<p>
Detail:
</p>

</div>

<h4 id="composable_logic">Composable logic</h4>
<div class="level4">

<p>
In AtomCore version 0.1, i've implementated my own Conditional checking and composing classes and functions to build up a composable logic system. That means compose a logic phrase out of 2 boolean values: true and false!
</p>

<p>
This system later can be use as piece in Gameplay composing, piece of Decision tree, as Guard in Finite State Machine, as condition in selecting…
</p>

<p>
In AtomCore 0.2, I made a change, consider big affect to the whole AtomCore I adapted to Guava's Function and Predicate. What's so intereting about Java's functional flavours? It provides more ways to compose logic, also more consise, readable, resuable if done right… Read more about Predicate:
<a href="http://code.google.com/p/guava-libraries/wiki/FunctionalExplained#Predicates" class="urlextern" title="http://code.google.com/p/guava-libraries/wiki/FunctionalExplained#Predicates" rel="nofollow">http://code.google.com/p/guava-libraries/wiki/FunctionalExplained#Predicates</a>
<a href="http://java.dzone.com/articles/google-guavas-predicates" class="urlextern" title="http://java.dzone.com/articles/google-guavas-predicates" rel="nofollow">http://java.dzone.com/articles/google-guavas-predicates</a>
</p>

<p>
Detail:
</p>

</div>

<h4 id="event_message_system">Event message system</h4>
<div class="level4">

<p>
With eventbus 
</p>

<p>
non blocking network
</p>

</div>

<h4 id="common_state">Common state</h4>
<div class="level4">

<p>
In turn, along with this pre defined cycle, some common states which ready to use
</p>
<ul>
<li class="level1"><div class="li"> LoadState : load / watch</div>
</li>
<li class="level1"><div class="li"> MenuState : select / option / ingame / exit</div>
</li>
<li class="level1"><div class="li"> InGameState : pause/ stop </div>
</li>
</ul>

</div>

<h4 id="common_routines">Common Routines</h4>
<div class="level4">

<p>
Handle Tasks, Actions in good concurent way (multi threading, actor..).
</p>

</div>

<h5 id="common_controls">Common Controls</h5>
<div class="level5">

<p>
EntityControl 
</p>

<p>
SpatialEditorControl 
</p>

<p>
AtomCharacterControl
</p>

<p>
AtomAnimationControl
</p>

<p>
IKControl
</p>

</div>

<h4 id="common_actors">Common Actors</h4>
<div class="level4">

</div>

<h4 id="game_status_persistent">Game status persistent</h4>
<div class="level4">

</div>

<h5 id="save">Save</h5>
<div class="level5">

</div>

<h5 id="load">Load</h5>
<div class="level5">

</div>

<h5 id="replay">Replay</h5>
<div class="level5">

</div>

<h4 id="common_uis">Common UIs</h4>
<div class="level4">

<p>
Provide a easy way to make <abbr title="Graphical User Interface">GUI</abbr> out of XML, bean, text, script… as seen in MetaWidget. Binding means input and data transaction ready.
</p>

<p>
Some common game UI as FlashScreen, MainMenu, Options, Lobby, Credit…
</p>

<p>
Advanced UI operation is on AtomGUI
</p>

</div>
<!-- EDIT6 SECTION "Game related" [9925-11881] -->
<h3 class="sectionedit7" id="application_related">Application related</h3>
<div class="level3">

</div>

<h4 id="common_configs">Common Configs</h4>
<div class="level4">

</div>

<h4 id="common_services">Common Services</h4>
<div class="level4">

</div>
<!-- EDIT7 SECTION "Application related" [11882-11952] -->
<h3 class="sectionedit8" id="packages">Packages</h3>
<div class="level3">

</div>

<h4 id="sgatomcore">sg.atom.core</h4>
<div class="level4">

<p>
Core elements of the framework.
</p>
<ul>
<li class="level1"><div class="li"> annotations 	Annotations to setting up elements in java code. [Same in every packages!]</div>
</li>
<li class="level1"><div class="li"> assets 			Facilities to import / export assets from JME3 pipeline</div>
</li>
<li class="level1"><div class="li"> bean			Facilities to use Java bean in Atom context with mapping and binding.</div>
</li>
<li class="level1"><div class="li"> config			Facilities to use Configs in Atom, with the help of Common Configuration</div>
</li>
<li class="level1"><div class="li"> context			Bridge concepts help to bring entities from one enviroment to others crossed platforms.</div>
</li>
<li class="level1"><div class="li"> execution		Facilities for execution, with help of Common lang and Guava</div>
</li>
<li class="level1"><div class="li"> lifecycle		Concepts for game (and real time application) cycle</div>
</li>
<li class="level1"><div class="li"> monitor			Facilities to monitor your game and application</div>
</li>
<li class="level1"><div class="li"> timing			Concepts &amp; Facilities for real time application</div>
</li>
</ul>

</div>

<h4 id="sgatomentity">sg.atom.entity</h4>
<div class="level4">

<p>
Concepts and Facilities to build up Game object. [Beta]
</p>

</div>

<h4 id="sgatomfx">sg.atom.fx</h4>
<div class="level4">

<p>
Concepts and Facilities to create and manage animations and effects.
</p>
<ul>
<li class="level1"><div class="li"> anim			Concepts for animation</div>
</li>
<li class="level1"><div class="li"> automatic 		Automatic driven for animation</div>
</li>
<li class="level1"><div class="li"> constraint		Other way to declare relationship between entities and activities</div>
</li>
<li class="level1"><div class="li"> filters			Additions to JME3 filters</div>
</li>
<li class="level1"><div class="li"> functional		Functional flavours for effects</div>
</li>
<li class="level1"><div class="li"> particles 		Concepts to build bigger system from smaller part [Atom concepts]</div>
</li>
<li class="level1"><div class="li"> sprite			Concepts for cross dimensional elements</div>
</li>
<li class="level1"><div class="li"> timeline		Enhance of timming framework</div>
</li>
<li class="level1"><div class="li"> transition		Transition between stateful objects </div>
</li>
<li class="level1"><div class="li"> tween			Object interpolations.</div>
</li>
</ul>

</div>

<h4 id="sgatomgameplay">sg.atom.gameplay</h4>
<div class="level4">

<p>
Concepts and facilities for games (cross-genre)
</p>
<ul>
<li class="level1"><div class="li"> action			Concepts and interfaces for action in games</div>
</li>
<li class="level1"><div class="li"> controls		Additional to JME3 character controls</div>
</li>
<li class="level1"><div class="li"> league			Leagues  group and tournament of players</div>
</li>
<li class="level1"><div class="li"> managers		Manager of leagues  group and tournament of players</div>
</li>
<li class="level1"><div class="li"> player			Player and their data</div>
</li>
<li class="level1"><div class="li"> replay			To record the game activities</div>
</li>
<li class="level1"><div class="li"> score			To recored the game results</div>
</li>
</ul>

</div>

<h4 id="sgatomlogic">sg.atom.logic</h4>
<div class="level4">

<p>
Basic block for building game from a programming language via formal system.
</p>

</div>

<h4 id="sgatomnet">sg.atom.net</h4>
<div class="level4">

<p>
Concepts and interfaces for connectivity and communication via networks
</p>

</div>

<h4 id="sgatomstage">sg.atom.stage</h4>
<div class="level4">

<p>
Concepts and facilities for cinematography like games
</p>
<ul>
<li class="level1"><div class="li"> actor			Bridge from entities to actor framework	</div>
</li>
<li class="level1"><div class="li"> cine			Sostiphicate cinematic framework for complex video games</div>
</li>
<li class="level1"><div class="li"> helpers			“Inplace” controls which know about Stage. Bridge from JME3 Controls concepts</div>
</li>
<li class="level1"><div class="li"> input			Sostiphicate high level input system use for develop and test game</div>
</li>
<li class="level1"><div class="li"> select			Facilities for selecting (from input) an on screen spatial or entities</div>
</li>
<li class="level1"><div class="li"> sound			Additional facilities to JME3 sound system</div>
</li>
<li class="level1"><div class="li"> sync			Additional facilities to syncing between multi thread progress</div>
</li>
</ul>

</div>

<h4 id="sgatomstate">sg.atom.state</h4>
<div class="level4">

<p>
Additional for JME3 app state (bridge between to systems) and some common states for a common games
</p>

</div>

<h4 id="sgatomui">sg.atom.ui</h4>
<div class="level4">

<p>
General <abbr title="Graphical User Interface">GUI</abbr> for user interaction and styling in hierachy (non-strict) elements
</p>

</div>

<h4 id="sgatomutils">sg.atom.utils</h4>
<div class="level4">

<p>
Collections of userful utilities and datastructures, algorimths here and there. 
</p>

<p>
</p><p></p><div class="notewarning">Note: This package contains a lot of stuff borrowed from libraries and should be clean up. Do not rely too much in this library!
</div>


</div>

<h4 id="sgatomworld">sg.atom.world</h4>
<div class="level4">

<p>
Concepts and interfaces to build and manage the game world and enviroment
</p>
<ul>
<li class="level1"><div class="li"> gen				Generate the world from data</div>
</li>
<li class="level1"><div class="li"> geometry		Maths for geometries</div>
</li>
<li class="level1"><div class="li"> lod				Level of detail framework provides a lot of methods to optimize scene and geometry. </div>
</li>
<li class="level1"><div class="li"> material		Additional to JME3 material system</div>
</li>
<li class="level1"><div class="li"> physics			Additional to JME3 physic system</div>
</li>
<li class="level1"><div class="li"> rendering		Additional to JME3 render system</div>
</li>
<li class="level1"><div class="li"> terrain			Additional to JME3 terrain system</div>
</li>
<li class="level1"><div class="li"> visibility		Additional to JME3 cull and partition system</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Packages" [11953-15596] -->
<h2 class="sectionedit9" id="documentation">Documentation</h2>
<div class="level2">

</div>
<!-- EDIT9 SECTION "Documentation" [15597-15623] -->
<h2 class="sectionedit10" id="troubleshooting_gotchas_best_practices">Troubleshooting, gotchas &amp; Best practices</h2>
<div class="level2">

</div>
<!-- EDIT10 SECTION "Troubleshooting, gotchas & Best practices" [15624-15678] -->
<h2 class="sectionedit11" id="contributions">Contributions</h2>
<div class="level2">

</div>
<!-- EDIT11 SECTION "Contributions" [15679-] -->
