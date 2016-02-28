---
title: How can I structure my code?
---
<h3 class="sectionedit1" id="how_can_i_structure_my_code">How can I structure my code?</h3>
<div class="level3">

</div>

<h4 id="the_question">The question</h4>
<div class="level4">
<pre class="code">How can I structure my code?</pre>

<p>
<a href="http://hub.jmonkeyengine.org/forum/topic/how-to-structure-the-game-code/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/how-to-structure-the-game-code/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/how-to-structure-the-game-code/</a>
</p>

</div>

<h4 id="the_pattern">The pattern</h4>
<div class="level4">

<p>
Read the explain about some design patterns in Design <a href="/jme3/advanced/atom_framework/design.html" class="wikilink1" title="jme3:advanced:atom_framework:design">design</a>
</p>

<p>
This queston evolve several patterns like Singleton, Manager, Factory and related directly to the Central idiom of Atom's framework!
</p>

</div>

<h4 id="the_central">The central</h4>
<div class="level4">

<p>
Now talking about the long “getManager().getSubManager().getItsManagedObject().doSomeThing()”
Consider asking your self this when you code:
</p>
<ol>
<li class="level1"><div class="li"> Can singleton help?</div>
</li>
<li class="level1"><div class="li"> Can hierarchy actually help?</div>
</li>
<li class="level1"><div class="li"> How secure is your application, is it a game or anything else?</div>
</li>
<li class="level1"><div class="li"> How perfomance sensitive your game is?</div>
</li>
</ol>

<p>
For this particular example, related to “Law of Demeter” that @zanval88 mentioned is about “communicating range scope” and “hiding information”, appear as “encapsulation” and “reference” in Java.
</p>
<ol>
<li class="level1"><div class="li"> If all your Manager classes is public, and referenced every where chances that they can be Singleton (read more about singleton for its downside).</div>
</li>
<li class="level1"><div class="li"> If not, you should nest your Manager and its ManagedObject it arbitrary order and way. Consider this for a game, it’s almost always not necessary!</div>
<ol>
<li class="level2"><div class="li"> When you have your Managers and Object form a “tree” and obey a “cycle” or “protocol” or “common pattern”, may be contract them with an Interface or force them to extend the same base. [I DID this in my Atom framework!]</div>
</li>
<li class="level2"><div class="li"> Actually while a lower (near the core) Manager are more powerful and can capture the whole process, the higher level Manager (extended Manager or sub manager) know better about detail and specific aspects. The split should be carefully thought first to avoid un necessary burden of too much Managers. Personally, I usually think about an interesting example about a society with many cops and few citizens to imagine about this balance.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> For part of the game, when security are most important but not the performance, or for external services. Long indirect call is the most appropriate method, because of the availability (something should be injected, lazy loaded…) and security (some protol given, real info is hidden from our view,…etc). Without a check of availability, chance that you have NPE all the time!</div>
</li>
<li class="level1"><div class="li"> For part of the game that need performance. I said “a big deal of performance” you should try “singleton” for final class (and bare with its other issuses) or bet in some other flatten type of reference (little bit worse performance – one level of indirect) should also be concerned:</div>
<ol>
<li class="level2"><div class="li"> array or list with an index. map via Class(Type) apear as Template in java … </div>
<ol>
<li class="level3"><div class="li"> ex: StateManager.getState(ClassName.class).doSomething(); </div>
</li>
<li class="level3"><div class="li"> or even more abstract somekind of Central.get(“StateManager”).do(“ItsFunctionName”)!!! I do this in groovy and for Java 8 dynamic invoking</div>
</li>
</ol>
</li>
<li class="level2"><div class="li"> evolve your hierarchy with EntitySystem paradigm</div>
</li>
</ol>
</li>
</ol>

</div>

<h4 id="the_structure">The structure</h4>
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
