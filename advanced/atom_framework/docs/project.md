---
title: The structure
---
<h3 class="sectionedit1" id="the_structure">The structure</h3>
<div class="level3">

</div>

<h4 id="videogame_structure">Videogame structure</h4>
<div class="level4">

<p>
I have a strong conceptual POV about video game, which affected by cinematography a lot. Because English is not my native language I can misunderstood the real meaning of the noun but I’ve tried to find the right words in decade.
</p>

<p>
This one is mine, maybe only me but noone else :p :
</p>

<p>
So consider this 5 level of separation:
</p>
<ol>
<li class="level1"><div class="li"> Main : The main entry, have everything only relate to this single game, single application. Also game specific Configs should be here</div>
</li>
<li class="level1"><div class="li"> Core : The shared part can be used in almost every application share the same base</div>
</li>
<li class="level1"><div class="li"> Stage : The ‘Stage’ is the base of entities, activites and events… It’s not nessesary care about the gameplay but the World, Camera, Light and Effects, Cinematic. Stage contain most of the underlying logic, and the actors.</div>
</li>
<li class="level1"><div class="li"> GamePlay: The part care about the routine of the game, the player, characters, stories, items, gameactions, techtree… it’s make the game look more like a game than an normal software or a movie. Gameplay contain most of the interactive part.</div>
</li>
<li class="level1"><div class="li"> State : Even your game routine can be modeled by something else not States, I introduced State to be more friendly with JME3′s AppState concept. I ultilized it and leveraged it, and you should also.</div>
</li>
</ol>

<p>
Others optional:
</p>
<ol>
<li class="level1"><div class="li"> *Network : For network game, blending between state, sub-routine and arbitrary events is difficult and may require other kind of paradigm, that’s why is not in Stage, but elsewhere outside.</div>
</li>
<li class="level1"><div class="li"> *Services: If your game use external services such as Web or IAP or something like that.</div>
</li>
<li class="level1"><div class="li"> *UI: UI stand for user interface, almost everygame have user interfaces but not all, so it’s also optional</div>
</li>
<li class="level1"><div class="li"> *Script: For scripting, in my application, I embed Groovy everywhere, but I also preseved a place to hold “tranditional” run-time script that only be awared and executed when the game is already running.</div>
</li>
<li class="level1"><div class="li"> *Model: If you are in a company or from a strong “standard lized” Java workflow, it’s nearly you’ll come up with some Bean like this, but it’s kind of for normal software not a game.</div>
</li>
<li class="level1"><div class="li"> *Generated: Also if you have to embed some XML or some generated sources</div>
</li>
<li class="level1"><div class="li"> *DB: Of course Database and persistent solution can be here( if not better be in the Service section)</div>
</li>
</ol>

<p>
…
</p>

</div>

<h4 id="project_source_structure">Project source structure</h4>
<div class="level4">

<p>
The directory :
 * src
</p>
<ul>
<li class="level1"><div class="li">my.game.name</div>
<ul>
<li class="level2"><div class="li">main</div>
</li>
<li class="level2"><div class="li">core</div>
</li>
<li class="level2"><div class="li">state</div>
</li>
<li class="level2"><div class="li">gameplay</div>
</li>
<li class="level2"><div class="li">(*)network</div>
</li>
<li class="level2"><div class="li">(*)services</div>
</li>
<li class="level2"><div class="li">(*)ui</div>
</li>
<li class="level2"><div class="li">(*)others</div>
</li>
</ul>
</li>
</ul>

<p>
More detailed, You can find a better example here in my game examples:
<a href="/jme3/atomixtuts.html" class="wikilink1" title="jme3:atomixtuts">atomixtuts</a>
</p>

</div>
