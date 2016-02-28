---
title: RTS gameplay
---
<h2 class="sectionedit1" id="rts_gameplay">RTS gameplay</h2>
<div class="level2">

<p>
</p><p></p><div class="noteimportant">To verify and unite the ideas, terms in this page I'd recommend you to read wikipedia to make sure if the term are corrected and common.
</div>


<p>
Wiki: <a href="http://en.wikipedia.org/wiki/Real-time_strategy" class="urlextern" title="http://en.wikipedia.org/wiki/Real-time_strategy" rel="nofollow">http://en.wikipedia.org/wiki/Real-time_strategy</a>
</p>

<p>
Mindmap: 
</p>

<p>
Slide: 
You can view full Gameplay Design document in Googledoc ( with more images, less text)
</p>

</div>
<!-- EDIT1 SECTION "RTS gameplay" [1-347] -->
<h3 class="sectionedit2" id="gameplaycore_and_additional_elements">Gameplay: Core and additional elements</h3>
<div class="level3">

<p>
</p><p></p><div class="notetip">This will be revive in design phase
</div>
Gameplay element will lead to requirements in AI and other components. Here we look around to review others famous game within RTS genre. The most obvious feature can have recognize a RTS game is number of units and its tech tree.


</div>

<h4 id="battle">Battle</h4>
<div class="level4">

<p>
Battle are most obvious activities of wars and also the distinc of RTS with civilazation game genre which have slow peace and mainly in Economic. War between planets and universe races like in StarCraft or between Countries like in Age of Empires. Battle in each game have its own “style” and “form”, mainly cause by the theme of the game, the skills of each units, number of them and the enviroments. 
</p>

<p>
Also we can see this gameplay element will require AI, network system to tightly corporate.
</p>

</div>

<h4 id="economic">Economic</h4>
<div class="level4">

<p>
Economic in RTS can be seen as “build order”, “tech tree” or “resource locating” problem, because almost every game have economic just as secondary gameplay to support battle. 
</p>

</div>

<h4 id="fog_of_war_-_reconnaissance">Fog of war - Reconnaissance</h4>
<div class="level4">

<p>
The lack of full view of the world also need to differences between RTS and board game (chess etc).. as Player don't have full awareness of opponents. Also in some games, player have to go explore or build houses to expand their map.
</p>

</div>

<h4 id="history_and_agriculture">History and agriculture</h4>
<div class="level4">

<p>
Each race or country have its own history and agriculture which will affect assets and can cause different tech tree of course.
</p>
<hr />

</div>
<!-- EDIT2 SECTION "Gameplay: Core and additional elements" [348-1816] -->
<h3 class="sectionedit3" id="rts_core">RTS Core</h3>
<div class="level3">

</div>

<h5 id="player">Player</h5>
<div class="level5">

<p>
Every player have an Account that they can use to log in to lobby and find Game and invite other Players to join a hosted Match
</p>

</div>

<h5 id="match">Match</h5>
<div class="level5">

<p>
A Match have 2-8 Players who have their Team and Races. Team have Color as visual indentification. A Match have specific settings, configuration and most important a choosed Level and Type of GamePlay (Campain, FlagRush, Defeat,…)
</p>

</div>

<h5 id="race">Race</h5>
<div class="level5">

<p>
We have 3 Races : Human, Mech (as Protos), Bug (as Zerg). Their have different Skills, Attributes and TechTree which form different way of playing.
</p>

</div>

<h5 id="game">Game</h5>
<div class="level5">

<p>
A Game start with basic pieces: Players attented, a Level(Map), a GameplayType and Goal. 
</p>

</div>

<h5 id="level_map">Level (Map)</h5>
<div class="level5">

<p>
A Level is a world with a map with Enviroment, Terrain, Items, specific Entities, Routines, Activities..
</p>

</div>

<h5 id="techtree">Techtree</h5>
<div class="level5">

<p>
It's a possible sequences of actions can take to revolve the game. Essentially it form a tree with hierarchy or pre-dependency.
</p>

<p>
Read more
<a href="http://en.wikipedia.org/wiki/Technology_tree" class="urlextern" title="http://en.wikipedia.org/wiki/Technology_tree" rel="nofollow">http://en.wikipedia.org/wiki/Technology_tree</a>
</p>
<hr />

</div>
<!-- EDIT3 SECTION "RTS Core" [1817-2801] -->
<h3 class="sectionedit4" id="actions_routines">Actions &amp; routines</h3>
<div class="level3">

</div>

<h5 id="game_routines">Game routines</h5>
<div class="level5">

<p>
In the Game, various of GameActions are taken by Players to envolve the game. Beside of that the Level also offer specific Rountines.
</p>

<p>
The Map first cover with Fog of War than be revealed and expand as the Unit moving around ( common in RTS game).
</p>

<p>
The main gameplay elements - most 2 things, actions you always do in an RTS game is:
</p>
<ul>
<li class="level1"><div class="li"> Build construction</div>
</li>
<li class="level1"><div class="li"> Control units to fight against opponents</div>
</li>
</ul>

</div>

<h5 id="build">Build</h5>
<div class="level5">

<p>
Building is built with a specific cost, after finish its provide its functions like: Procedure troops, Upgrade skill-weapon, etc…
</p>

<p>
In general speaking, it provides more GameActions, then in turn expand the TechTree.
</p>

</div>

<h5 id="fight">Fight</h5>
<div class="level5">

<p>
Fights happend when you attack your Enemies targets: Unit and Building. The results are:
</p>
<ul>
<li class="level1"><div class="li"> Your units get damaged , get killed or kill others. </div>
</li>
<li class="level1"><div class="li"> Building get damaged or destroyed.</div>
</li>
</ul>

<p>
More aspects of a fight should be concern is range, type of an Attack, abilities to defend againts each Attack. About visual aspects, different skills appear as different effects.
</p>

<p>
By default the fight routine are controled by the AI.
</p>

</div>

<h5 id="rewards">Rewards</h5>
<div class="level5">

<p>
Fight also resulted in points, golds… rewarded to your result/property . As in normal RTS game, like starcraft2, no more bonus if you kill several target at once. but in DotA like game genre, you got bonus if combos happen. So our reward stragegy should be flexible enough to deal with the changable gameplay.
</p>

</div>

<h5 id="declare_win-lose">Declare Win-Lose</h5>
<div class="level5">

<p>
The final conclusion of the game (gameover) is reached as one Team complete the Goal - specific by the GameType, in our game we implemented a few gameplay type as describled below:
</p>
<hr />

</div>
<!-- EDIT4 SECTION "Actions & routines" [2802-4447] -->
<h3 class="sectionedit5" id="gameplaytype_-_objectives_goals">GameplayType - Objectives &amp; Goals</h3>
<div class="level3">

</div>

<h5 id="defeat_enemies">Defeat enemies</h5>
<div class="level5">

<p>
By default, a game normally ended when a team defeat all it enemies, as they killed and destroyed all/every or almost opponents units/constructions. Or in some games, win-lose declared as the MainHouse is destroyed.
</p>

</div>

<h5 id="flagrush">FlagRush</h5>
<div class="level5">

<p>
An intesting gameplay, as the motivation of the game is to capture something call a flag. Every team of players try to take control of an item, area in particular.
</p>

<p>
Win-lose usually declared as one complete a routine take the flag from imdependent platform or opponents home.
</p>

</div>

<h5 id="campains">Campains</h5>
<div class="level5">

<p>
Usually a scripted goal means a specifics special, story based goal with specific routines and items in the Map. Teams or players try to reach the goal as in intruction as fast as possible to declare win.
</p>

</div>

<h5 id="dota_like_rpg">DotA like (RPG)</h5>
<div class="level5">

<p>
The rising gameplay recently ( ehr, not really :p ) …
</p>
<hr />

</div>

<h4 id="gameobject_entites">Gameobject &amp; Entites</h4>
<div class="level4">

</div>

<h5 id="unit">Unit</h5>
<div class="level5">
<hr />

</div>
<!-- EDIT5 SECTION "GameplayType - Objectives & Goals" [4448-5362] -->
<h3 class="sectionedit6" id="devices_inputs_controls">Devices &amp; Inputs &amp; Controls</h3>
<div class="level3">

</div>

<h5 id="pc">PC</h5>
<div class="level5">

</div>

<h5 id="mouse_keyboards">Mouse &amp; Keyboards</h5>
<div class="level5">

</div>

<h5 id="move_build_mirco">Move , build, mirco</h5>
<div class="level5">
<hr />

</div>
<!-- EDIT6 SECTION "Devices & Inputs & Controls" [5363-5462] -->
<h3 class="sectionedit7" id="more_gameplay_aspects">More Gameplay aspects</h3>
<div class="level3">

</div>

<h5 id="economy">Economy</h5>
<div class="level5">

<p>
In Age of Empire (few others), when you just focus in expanding your empire without fighting and the game said that you reach a limit, where you can not expand your economic base futher. Consider this point, you will see the different between RTS game and the game genre just focus in building things in long term like civilazation and city tycoons.
</p>

<p>
So the things you want to concern in our gameplay is the way to watch, aware and manage the status of economy of every players.
</p>

<p>
Beside of that, the players can trade or exchange things in between team, allies. That's an interesting point of gameplay, open possiblites but also technical problems come later, so it's worth to be carefully concerned, designed.
</p>

</div>

<h5 id="balance">Balance</h5>
<div class="level5">

<p>
What if a race have dominance, advantages that superior to others. How can we balance between the race without annoying players by too much restrictions. This point should be considered carefully, even worth researchings. I will also offer some paper in this topic but to help you get an overview, the solutions lying in flowing categories:
</p>
<ul>
<li class="level1"><div class="li"> Unit attributes</div>
</li>
<li class="level2"><div class="li"> Techtrees, aka sequences of action can be taken</div>
</li>
<li class="level2"><div class="li"> Speed/cost of evolving : speed/cost of each actions, speed/cost of upgrading…</div>
</li>
<li class="level2"><div class="li"> The Map!</div>
</li>
<li class="level2"><div class="li"> Specity contrainsts of each race nature/culture</div>
</li>
</ul>

</div>

<h5 id="cheating">Cheating</h5>
<div class="level5">

<p>
People always try to find way to cheat around. And if you don't take care of your AI, it can also be consider treated. The implementation such central system (server) and communication protocol should also be well designed to reduce or prevent cheating as much as possible.
</p>

</div>

<h5 id="modding">Modding</h5>
<div class="level5">

<p>
Starcraft, Warcraft, AOE come with its editor helps modder make their map and game, which is open a whole new world of gaming as we've seen today. This can also be consider of a sub gameplay as player customize their game and publish it.
</p>

</div>
<!-- EDIT7 SECTION "More Gameplay aspects" [5463-] -->
