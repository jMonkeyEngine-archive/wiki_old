---
title: MMORPG Adventure
---
<h2 class="sectionedit1" id="mmorpg_adventure">MMORPG Adventure</h2>
<div class="level2">

</div>
<!-- EDIT1 SECTION "MMORPG Adventure" [1-29] -->
<h2 class="sectionedit2" id="code_nameancient_monkey_world_amw">CODE NAME : ANCIENT MONKEY WORLD (AMW)</h2>
<div class="level2">

<p>
<strong>Hi, monkeys</strong>
</p>

<p>
After a long project, I have time to sit down a write something about MMORPG and my adventure in making one (if it’s not a forbidden word). :p
</p>

<p>
</p><p></p><div class="notewarning">A MMORPG Project is <strong>not easy nor appropriate</strong> for beginner. <br />

Such projects need a lot of skills, knowledge, passions and efforts to accomplish… <br />

This tutorial just 've written down as the process of one no warranty attempt start by forum members : @atomix and … () 
</div>


<p>
The project will be a community project, that mean Open-source and non-profit, code name : 
<strong>Ancient Monkey World.</strong>
<a href="/resources/fetch.php" class="media" title="http://digital-art-gallery.com/oid/66/1356x1600_12073_Monkey_King_2d_fantasy_character_monkey_king_picture_image_digital_art.jpg"><img src="/resources/fetch.php" class="mediaright" title="digital-art-gallery.com_oid_66_1356x1600_12073_monkey_king_2d_fantasy_character_monkey_king_picture_image_digital_art.jpg" alt="digital-art-gallery.com_oid_66_1356x1600_12073_monkey_king_2d_fantasy_character_monkey_king_picture_image_digital_art.jpg" width="300" /></a>
</p>

</div>
<!-- EDIT2 SECTION "CODE NAME : ANCIENT MONKEY WORLD (AMW)" [30-797] -->
<h3 class="sectionedit3" id="quick_start_for_developers">Quick start for Developers</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Forum: <a href="http://hub.jmonkeyengine.org/forum/topic/mmorpg-adventure/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/mmorpg-adventure/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/mmorpg-adventure/</a></div>
</li>
<li class="level1"><div class="li"> Wiki: <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:atomixtuts:mmorpg" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:atomixtuts:mmorpg" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:atomixtuts:mmorpg</a> and <a href="http://code.google.com/p/ancient-monkey-world/w/list" class="urlextern" title="http://code.google.com/p/ancient-monkey-world/w/list" rel="nofollow">http://code.google.com/p/ancient-monkey-world/w/list</a></div>
</li>
<li class="level1"><div class="li"> Sourcecode: <a href="http://code.google.com/p/ancient-monkey-world/" class="urlextern" title="http://code.google.com/p/ancient-monkey-world/" rel="nofollow">http://code.google.com/p/ancient-monkey-world/</a></div>
</li>
<li class="level1"><div class="li"> Plan: <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:atomixtuts:mmorpg#process" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:atomixtuts:mmorpg#process" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:atomixtuts:mmorpg#process</a></div>
</li>
<li class="level1"><div class="li"> Issues: <a href="https://code.google.com/p/ancient-monkey-world/issues/list" class="urlextern" title="https://code.google.com/p/ancient-monkey-world/issues/list" rel="nofollow">https://code.google.com/p/ancient-monkey-world/issues/list</a></div>
</li>
<li class="level1"><div class="li"> Setup: </div>
</li>
<li class="level1"><div class="li"> Tools: <a href="/doku.php/jme3:atomixtuts:mmorpg_tools" class="wikilink2" title="jme3:atomixtuts:mmorpg_tools" rel="nofollow"> Tools used</a> <a href="/jme3/atomixtuts/mmorpg/researches/toolset.html" class="wikilink1" title="jme3:atomixtuts:mmorpg:researches:toolset">Research about toolset</a></div>
</li>
<li class="level1"><div class="li"> Game documents: </div>
</li>
<li class="level1"><div class="li"> Art &amp; Assets: </div>
</li>
<li class="level1"><div class="li"> License: BSD </div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Quick start for Developers" [798-1450] -->
<h3 class="sectionedit4" id="quick_start_for_viewers">Quick start for Viewers</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/atomixtuts/mmorpg/phase0.html" class="wikilink1" title="jme3:atomixtuts:mmorpg:phase0"> Phase 0 - JME 3D in 2D RPG gameplay</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/atomixtuts/mmorpg/phase1.html" class="wikilink1" title="jme3:atomixtuts:mmorpg:phase1"> Phase 1 - Physics and network: faster than the bullet</a></div>
</li>
<li class="level1"><div class="li"> <a href="/doku.php/jme3:atomixtuts:mmorpg:phase2#detail" class="wikilink2" title="jme3:atomixtuts:mmorpg:phase2" rel="nofollow"> Phase 2 - Quests and Tools</a></div>
</li>
<li class="level1"><div class="li"> <a href="/doku.php/jme3:atomixtuts:mmorpg:phase3#detail" class="wikilink2" title="jme3:atomixtuts:mmorpg:phase3" rel="nofollow"> Phase 3 - Deploy to the Cloud and PLAY</a></div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Quick start for Viewers" [1451-1825] -->
<h3 class="sectionedit5" id="prelude">Prelude</h3>
<div class="level3">

<p>
I cant count how many times people saying that you can not build a MMORPG with just two hands and a computer… That mean no chance a one man army can even write that kind of game, or it going to be a failure. I’m not a fearless programmer nor a naive kid try to impress. I just think I can!
</p>

<p>
I was from a Database center solution then come to Game industry in a strangest kind of accident :p As I was a pure Java programmer than become a fulltime designer. That’s kind of weird but teach me one thing “You can do extraordinary thing with the right tool”… not mentioned efford, time, knowledge, exprerience and passion…
</p>

<p>
The right tools <strong>weapon</strong> I choose is JMonkeyEngine and other opensources project to start to learn.
</p>

<p>
So did I tell you we can make a MMORPG with just an idea and a few thousand hours of working? Indeed. Here is the story:
</p>

</div>

<h4 id="your_idea">0) Your idea:</h4>
<div class="level4">

<p>
Let’s say you have a good idea of a Game… an imagination world that people interact and fight, meet, share… you have a story to tell, and want to draw some impressive scenery or beatiful characters. Spend like a few years for the ideas, may be research and play a lot of games, use papers, talk with friends, travel around the world… Until you have concentrade enough for only one good idea.
</p>

</div>

<h4 id="your_skills">1) Your skills:</h4>
<div class="level4">

<p>
Question: I can draw, can compose music, video, can code, can sing, can write script, can do Java stuff… Is that enough?
Answer: Ummh, NO!
MMORPG is a freaking black-hole of knowledges and experiences requirement. No estimatable amount of knowledge consider enough.
But then I tell you is ENOUGH. At least you can do Java stuff and can draw, you can. The other you will learn when you are on the journey.
</p>
<ul>
<li class="level1"><div class="li"> + Programming: For the start, you need to “know” Java, the more the better. If you just write your first “Hello world” program 3 months ago. You are too hurry for a big challenge. Let make it at least 3 year exprience. I have 13 and consider people with much more expriences still facing problems of course. The years does not matter!</div>
</li>
<li class="level1"><div class="li"> + Assets: May be you should know how to draw and 3d stuff, the more the better. I recommend if you are at least 1 year with 3D modelling and animating, and should play around with tools. First is Concept. Then other things come quick : Sound, Sprite,…</div>
</li>
<li class="level1"><div class="li"> + Researching skill: This is very important if you are a one man army or indie team. You have to do research, brain-storming or ask people every time. So try to be active to get knowledge.</div>
</li>
</ul>

</div>

<h4 id="your_workflow">2) Your workflow:</h4>
<div class="level4">

<p>
try Extreme programing: <a href="http://en.wikipedia.org/wiki/Extreme_programming" class="urlextern" title="http://en.wikipedia.org/wiki/Extreme_programming" rel="nofollow">http://en.wikipedia.org/wiki/Extreme_programming</a>
</p>

<p>
If you never in a professinal workflow before, try to do it simplier as your only have limited man power. Most valuable advice if you’re an artist do programming: Do it like Zen :p
</p>
<ul>
<li class="level1"><div class="li"> - Smart and active: Research first, try to call out for help if need! Opensource are the key.</div>
</li>
<li class="level1"><div class="li"> - Flexible but manageable: Try to use SVN.</div>
</li>
<li class="level1"><div class="li"> - Shoot with both hands: Do both assets and programming can cause a mesh, do one at a time. After finish review, get approved by yourself or the leader. Continue developing.</div>
</li>
<li class="level1"><div class="li"> - Pirate spirit: Use place holder as much as your can. Skip concept, may use existed assets. There are plenty of free assets.</div>
</li>
<li class="level1"><div class="li"> - Avoid premature optimization: If still concerning about design, make it work first.</div>
</li>
<li class="level1"><div class="li"> … [more to come]</div>
</li>
</ul>

</div>

<h4 id="your_tools">3) Your tools:</h4>
<div class="level4">

<p>
Of course this is big task, Your tools are various from DDC to Image/sound editor… But let’s name a few with zero cost! (mean open-source or free)
</p>
<ul>
<li class="level1"><div class="li"> - JME SDK and its plugins (Programming, database tools… a God-like tool for smart monkey)</div>
</li>
<li class="level1"><div class="li"> - GIMP (2d: concept, texture…)</div>
</li>
<li class="level1"><div class="li"> - Blender (3d)… and there are a lot of good 3d tools. Blender are the best integrated tool to JME</div>
</li>
<li class="level1"><div class="li"> - [Other assets tool like sound editors, sprite… come later]</div>
</li>
</ul>

</div>

<h4 id="your_framework">4) Your framework:</h4>
<div class="level4">

<p>
This is the most important thing that can make your dream possible. So let me speak a bit slowly:
I spend years for researching in this area (MMORPG), I came across WorldForge, Darkstar,… write my own Network engine and related DB stuff using Hypertable, ORM… (bad mislead time)
</p><p></p><div class="notetip">More about MMORPG Architecture and framework Researches: <a href="/jme3/atomixtuts/mmorpg/researches.html" class="wikilink1" title="jme3:atomixtuts:mmorpg:researches">researches</a>
</div>
And finally I found a nice, free but powerful framework: The Threerings project <a href="http://www.threerings.net/code/" class="urlextern" title="http://www.threerings.net/code/" rel="nofollow">http://www.threerings.net/code/</a> 2 year ago.


<p>
It taken time to research and admit that they do it nicely and scalable (i’m not going to blow it up). If you think you are better than me in reviewing go ahead, i also need valuabe comperations of framework at the moment.
</p>

<p>
So what I tell you that amount of tool are pretty enough for thousand players game. I’m not going to do Three rings advertisment, for short, it’s your chance to build a MMORPG.
</p>

<p>
What you will see at first that the OOO even support 3D stuff, as some of their developer also contribute in JME version2, then write their own engine. It’s quite bad compare to JME at the moment. So maybe you want to use JME3 to do graphics stuff and other tools for Network. Deploying and DB. AI stuff are often quite difficult to write your own but in the end, I will offer you a choice.
</p>

<p>
</p><p></p><div class="noteimportant">But is it real you can make a MMORPG game with just that?
Of course not. It will take more than thousands of hours to code and to draw, do experiments, fix bugs… This is just advice point out a good way before start your own journey.
</div>


<p>
People may come up with different levels of knowledge and experience. So here and there, they may want to replace an open-source project by their own library. I also write almost every modules of the architure, but for myself I can not provide enough efforts for an opensource project maintaining. I just can keep bad code, release a few good one and write down articles.
</p>

<p>
For people who are exciting of community project as MMORPG, may be this time you can gather up. I’m not guaranty that I’m enough of abitily to make it to the end, but at least we have a working base to start with. 
</p>

<p>
</p><p></p><div class="noteimportant">
Anyone interest can PM me as @atomix in the forum?
</div>


</div>
<!-- EDIT5 SECTION "Prelude" [1826-7953] -->
<h2 class="sectionedit6" id="the_adventure_begin">THE ADVENTURE BEGIN</h2>
<div class="level2">

</div>
<!-- EDIT6 SECTION "THE ADVENTURE BEGIN" [7954-7984] -->
<h3 class="sectionedit7" id="the_idea">The idea</h3>
<div class="level3">

<p>
In Oriental culture, we all love the legend of Monkey king who traveled to the West and become a Buddha.
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Sun_Wukong" class="urlextern" title="http://en.wikipedia.org/wiki/Sun_Wukong" rel="nofollow">http://en.wikipedia.org/wiki/Sun_Wukong</a>
</p>

<p>
<a href="https://www.google.com/search?q=Monkey+King" class="urlextern" title="https://www.google.com/search?q=Monkey+King" rel="nofollow">https://www.google.com/search?q=Monkey+King</a>
</p>

<p>
( Songoku in Japanese )
</p>

<p>
I compose the idea with wild jungle scenes in fictional oriental - western mixed scenery and theme, and adventures along the jouney.
<a href="/resources/fetch.php" class="media" title="http://fc09.deviantart.net/fs70/i/2011/004/d/5/monkey_king_by_saryth-d36e92m.jpg"><img src="/resources/fetch.php" class="mediacenter" title="fc09.deviantart.net_fs70_i_2011_004_d_5_monkey_king_by_saryth-d36e92m.jpg" alt="fc09.deviantart.net_fs70_i_2011_004_d_5_monkey_king_by_saryth-d36e92m.jpg" width="400" /></a>
</p><p></p><div class="notetip">More about ideas and Game Design [googlecode] and [googledocs] <span class="curid"><a href="/jme3/atomixtuts/mmorpg.html" class="wikilink1" title="jme3:atomixtuts:mmorpg">mmorpg</a></span>
</div>


</div>
<!-- EDIT7 SECTION "The idea" [7985-8553] -->
<h3 class="sectionedit8" id="mind_map">Mind map</h3>
<div class="level3">

<p>
This is the sketch mindmap of the game. 
</p>

<p>
<iframe title="" src="http://text2mindmap.com/JdE5xP" style="width:100%; height:600px"></iframe>
</p>

</div>
<!-- EDIT8 SECTION "Mind map" [8554-8664] -->
<h3 class="sectionedit9" id="game_design">Game design</h3>
<div class="level3">

</div>
<!-- EDIT9 SECTION "Game design" [8665-8687] -->
<h3 class="sectionedit10" id="mmo_game_architecture_researches">MMO Game Architecture Researches</h3>
<div class="level3">

</div>

<h4 id="overal_mmo_game_architecture">Overal MMO Game Architecture</h4>
<div class="level4">

<p>
In Phase 0 of the development process I intend to use Marauroa and some code from Arriane because the ease of use and clear design! 
In <strong>Marauroa</strong> engine they have an excellent short and precise overview MMO game architecture which I will cite below, keep in my the detail implementation like DB or even programming language are optional:
</p>

<p>
<em>Marauroa is based on very simple principles:</em>
</p>
<ul>
<li class="level1"><div class="li"> Clients communicate with the server, and vice-versa, using a TCP portable network protocol with reliability in mind to allow a stabler experience when online game lag occurs.</div>
</li>
<li class="level1"><div class="li"> To play a game every player needs an account on the server that is identified by an username and a password.</div>
</li>
<li class="level1"><div class="li"> Players use their account to login into the server and then choose a 'player' stored under their account to play with. The server then checks the login information using the MySQL backend and loads the player into the game using the persistence engine.</div>
</li>
<li class="level1"><div class="li"> Players send actions to the server. The action system is totally open and has nothing hard-coded so you can edit it totally to your game style. The server sends at regular intervals, called turns, a perception to each player to inform them about the state of the game and any relevant state modifications. Marauroa's perception system is based on the Delta^2 ideology: simply send what has changed.</div>
</li>
<li class="level1"><div class="li"> The server executes some code each turn in order to move the game status on. Using this hook it is simple to code triggers, timeouts, conditions and whatever kind of behavior you need.</div>
</li>
<li class="level1"><div class="li"> The server transparently and automatically stores players and game status modifications on the persistence engine, and also information decided by the game developer using their game definition scripts.</div>
</li>
<li class="level1"><div class="li"> Game rules can be coded in Java to allow simple and rapid development and without having to know anything about Marauroa's internals. Python scripts for the game rules could be supported with a little work.</div>
</li>
<li class="level1"><div class="li"> The server generates statistics of usage which are stored in a MySQL or H2 database (so you can later generate fancy statistics from them). Or in case you don't require them, they can be disabled to save CPU cycles and disk space. Marauroa features a modular structure that means modules can be changed and disabled without affecting the operation of other modules.</div>
</li>
<li class="level1"><div class="li"> Both the server and clients are fully and wisely documented, with documentation about specification and design and not just <abbr title="Application Programming Interface">API</abbr> documentation.</div>
</li>
</ul>

<p>
Review the full description here
</p><p></p><div class="notetip"><a href="http://arianne.sourceforge.net/engine/marauroa.html" class="urlextern" title="http://arianne.sourceforge.net/engine/marauroa.html" rel="nofollow">http://arianne.sourceforge.net/engine/marauroa.html</a>
</div>


<p>
As said, the architecture and the components of a MMORPG game will be kept but part by part will be swaped or replaced as the process go. Why? Because there are better solutions new technologies nowaday. Now let take a look at the three things call the “Triangle of Bedmudas” in game design. 
</p>

</div>

<h4 id="entity_system">Entity system</h4>
<div class="level4">

<p>
Yeah, this is not really new. In fact, the Entity system wave was from 2006-2007, as
<a href="http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/" class="urlextern" title="http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/" rel="nofollow">http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/</a>
and almost become a standard solution in MMO world.
</p>

<p>
The idea of Entity System are descripted better with details here:
<a href="/jme3/contributions/entitysystem/introduction.html" class="wikilink1" title="jme3:contributions:entitysystem:introduction"> Entity system Introduction</a>
</p>

<p>
So, as you see, JME community already offer 2-3 Entity System solutions. As the guys discuss in the forum, the code base of the ES should be kept rather small and compact because it's going to be involve in every game cycle. The first thing should be revolved and change from Marauroa code base is the Entity System intergration which also with be the base of other additons in the future.
</p>

</div>

<h4 id="event_system">Event system</h4>
<div class="level4">

<p>
What's the hurry for a game event system?
Yeah, event system here is not just the event (message) broadcasting. Because game technologies involve more and more parallelism, especially to be corporate with networking, the event system should also be considered again. 
</p>

<p>
Event system should encourage decoupeling and give the developer more strength and controls. Also ease of use, ightweight, non blocking, non replicating…etc
</p>

<p>
I'm not going to the details here but you can read more about it in the researches.
</p>

</div>

<h4 id="network_system">Network system</h4>
<div class="level4">

<p>
This problem can be considered a challange in design. No one can say it easy or they not write it and test it yet. C
</p>

<p>
orporate with entity, event and networking make a “Death point” for every design. For big MMO game (and other kind of massive real time system) in 4-5 years ago, they strugge to make those 3 work together, by trying to reduce the network cost, multi thread the server, and do C++ tricks in memory, pointer…etc . Yeah, we will have to do them same to be optimized …
</p>

<p>
</p><p></p><div class="notetip">For further reading: GOTO <a href="/jme3/atomixtuts/mmorpg/researches.html" class="wikilink1" title="jme3:atomixtuts:mmorpg:researches">researches</a>
</div>


</div>

<h4 id="the_chosen_one">The chosen one</h4>
<div class="level4">
<blockquote><div class="no">
But can we come up with better overal design first?<br />
Hopefully, yes, this time!</div></blockquote>

<p>
So the asynchronized server, network and event system are widely use nowadays. The are dozen of open source project intended to solve the enterprise problems at once. 
</p>
<pre class="code"> Node.js is a good example, the idea is simple but the implementation are truely epic. They've done it beautifully and we (java devs) should have the same thing or get used to it in the mean time.
 The runner up but in the Java world is the Three rings projects, well done and save developer from the hard parts.</pre>

<p>
But till the time of writing, almost no one get it straight into game developing or not into 3D (like Three rings). I considered those general systems can not sastify the needs for <strong>enterprise game developing</strong>! They always try to keep it relatively small because of affair / obsesses it will become un-optimized. But also because of that, they don't solve the 3 main problems at once, which lead to the un sastification i mentioned.
</p>

<p>
In the researches you will find an article tell extractly how I use, modify, leverage and optimize Three rings and the existed opensource projects to let them work seamlessly together, without worry about the over engineering!
</p>

</div>
<!-- EDIT10 SECTION "MMO Game Architecture Researches" [8688-14814] -->
<h3 class="sectionedit11" id="amw_architecture">AMW Architecture</h3>
<div class="level3">

</div>
<!-- EDIT11 SECTION "AMW Architecture" [14815-14842] -->
<h2 class="sectionedit12" id="process">PROCESS</h2>
<div class="level2">

</div>
<!-- EDIT12 SECTION "PROCESS" [14843-14862] -->
<h3 class="sectionedit13" id="phase_zero">Phase Zero</h3>
<div class="level3">

<p>
<strong>Start:</strong> July 1st - August 1st 
</p>

<p>
<strong>Main task:</strong> Setup and Port  MORPG engine Arriane from 2D to 3D. Try and review. 
</p>

<p>
<a href="/jme3/atomixtuts/mmorpg/phase0.html" class="wikilink1" title="jme3:atomixtuts:mmorpg:phase0">phase0</a>
</p>

</div>
<!-- EDIT13 SECTION "Phase Zero" [14863-15036] -->
<h3 class="sectionedit14" id="phase_1">Phase 1</h3>
<div class="level3">

<p>
<strong>Start:</strong> August 1st - September 1st 
</p>

<p>
<strong>Main task:</strong> Unknown
</p>

<p>
<a href="/jme3/atomixtuts/mmorpg/phase1.html" class="wikilink1" title="jme3:atomixtuts:mmorpg:phase1">phase1</a>
</p>

</div>
<!-- EDIT14 SECTION "Phase 1" [15037-15150] -->
<h3 class="sectionedit15" id="phase_2">Phase 2</h3>
<div class="level3">

<p>
<strong>Start:</strong> September 1st - Oct 1st 
</p>

<p>
<strong>Main task:</strong> Unknown
</p>

<p>
<a href="/doku.php/jme3:atomixtuts:mmorpg:phase2" class="wikilink2" title="jme3:atomixtuts:mmorpg:phase2" rel="nofollow">phase2</a>
</p>

</div>
<!-- EDIT15 SECTION "Phase 2" [15151-15262] -->
<h3 class="sectionedit16" id="phase_3">Phase 3</h3>
<div class="level3">

<p>
<strong>Start:</strong> Oct 1st - Nov 1st 
</p>

<p>
<strong>Main task:</strong> Unknown
</p>

<p>
<a href="/doku.php/jme3:atomixtuts:mmorpg:phase3" class="wikilink2" title="jme3:atomixtuts:mmorpg:phase3" rel="nofollow">phase3</a>
</p>

</div>
<!-- EDIT16 SECTION "Phase 3" [15263-] -->
