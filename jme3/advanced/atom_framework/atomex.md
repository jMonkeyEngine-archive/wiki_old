---
title: Atom Ex framework Introduction
---
<h2 class="sectionedit1" id="atom_ex_framework_introduction">Atom Ex framework Introduction</h2>
<div class="level2">

<p>
<strong>Hi Monkeys,</strong>
<strong>Atom Ex</strong> framework helps you biggest steps to make your applications scale to web and distributed computing!
</p>

<p>
</p><p></p><div class="notetip">
It's one of my long-term research, result of more than 6 years of research and 2 years of studying and coding
</div>


</div>
<!-- EDIT1 SECTION "Atom Ex framework Introduction" [1-299] -->
<h3 class="sectionedit2" id="idea_buzz">Idea &amp; Buzz</h3>
<div class="level3">

<p>
<strong>Bigger, more powerful with ease</strong>
</p>
<blockquote><div class="no">
From Data Central and Web's battle field, end up in game developing, I've dreamt about games and applications that scale its self in a snap. At first, something like a render-farm to accelerate 3D rendering pipeline or baking lightmap, massive level entities computing to save 3D artist lives, then may be something like 3D collaborative editing enviroment…</div></blockquote>

<p>
Initial Ideas:
</p>
<ul>
<li class="level1"><div class="li"> Get to the cloud with ease, Spring-like but not just Spring</div>
</li>
<li class="level1"><div class="li"> Framework for games and apps(3D) </div>
</li>
<li class="level1"><div class="li"> Nextgen techs</div>
</li>
</ul>

<p>
But technically, is something like this possible at all????
</p>

<p>
<strong>Yes</strong>, with helps of creative design of tools and frameworks, workflows and lastest technologies!!!
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Model-driven_architecture" class="urlextern" title="http://en.wikipedia.org/wiki/Model-driven_architecture" rel="nofollow">http://en.wikipedia.org/wiki/Model-driven_architecture</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Data-driven_architecture" class="urlextern" title="http://en.wikipedia.org/wiki/Data-driven_architecture" rel="nofollow">http://en.wikipedia.org/wiki/Data-driven_architecture</a>
</p>
<ol>
<li class="level1"><div class="li"> The first thing that most important to make this idea possible: <strong>Everything are data</strong>, including source code. </div>
</li>
<li class="level1"><div class="li"> How can it be? Yes, it can if source code are very <strong>generative</strong> , means it can be generated in this way or others. In fact, <strong>generative</strong> is also a key. </div>
</li>
<li class="level1"><div class="li"> Every aspect of this software development framework involving different kinds of auto-generating. Once again, <strong>automatic</strong> instead of manual is a key</div>
</li>
<li class="level1"><div class="li"> Keep in mind <strong>this is not magic but the lastest technologies</strong> , means it's new, and some people also can not believe it real :p That's easy to understand. </div>
</li>
</ol>

<p>
In fact, current implementation of AtomEx only cover a very small part of the automatic distributed game development but its potential is large. 
</p>
<blockquote><div class="no">
As examples for distributed computing, I made a 3d rendering farm and a lightmap baker for demostration that show well the power of its theory and also helpful but not show much the automatic aspect. <blockquote><div class="no">
In constrast, the example 1000MMORPG show only 1000 LOC (lines of code) of Groovy without the AtomEx's code base can make an full-scale MMORPG with Networking, Multi-nodes Database, servers, monitors, clients, SDKs , much more… which show the power of automatic code generation and model centric architecture. </div></blockquote>
</div></blockquote>

<p>
</p><p></p><div class="notetip">Go try JMERenderFarmLite <a href="http://github.com/sgmedia/jme-renderfarm-lite" class="urlextern" title="http://github.com/sgmedia/jme-renderfarm-lite" rel="nofollow">http://github.com/sgmedia/jme-renderfarm-lite</a> and 1000MMORPG <a href="http://github.com/sgmedia/jme-1000loc-mmorpg" class="urlextern" title="http://github.com/sgmedia/jme-1000loc-mmorpg" rel="nofollow">http://github.com/sgmedia/jme-1000loc-mmorpg</a> on github
</div>


<p>
The most attractive and impressive part is this is not a “config hell” framework, somehow Spring-like mechaism, but Convention over configuration…
</p>

<p>
[to be continued]
</p>

</div>
<!-- EDIT2 SECTION "Idea & Buzz" [300-2730] -->
<h3 class="sectionedit3" id="features">Features</h3>
<div class="level3">

</div>
<!-- EDIT3 SECTION "Features" [2731-2750] -->
<h3 class="sectionedit4" id="architecture_and_components">Architecture and components</h3>
<div class="level3">

<p>
Here are its architecture and components.
Atom Ex Core highlights:
</p>
<ul>
<li class="level1"><div class="li"> Beans: Java at its finesse</div>
</li>
<li class="level1"><div class="li"> Generative | Automative as its insistent characteristic</div>
</li>
<li class="level1"><div class="li"> Dependency | Component injection: For modular enterprise software</div>
</li>
<li class="level1"><div class="li"> Utilize the best open-source projects on earths</div>
</li>
<li class="level1"><div class="li"> Meta widget: for a flexible presentation solution</div>
</li>
<li class="level1"><div class="li"> Polymorphing via interfacing software architecture.</div>
</li>
<li class="level1"><div class="li"> Event base, messaging non block </div>
</li>
<li class="level1"><div class="li"> Paralel ,utilize even GPU</div>
</li>
</ul>

<p>
Atom DB : Generate all DAO, configs for persitent. One code, run anywhere.
</p>
<ul>
<li class="level1"><div class="li"> Bridge to ORMs : Cayneene , Hibernate</div>
</li>
<li class="level1"><div class="li"> Bridge to NoSQL : Casabranda , Neo4j</div>
</li>
<li class="level1"><div class="li"> Leverage all with “useful” EJB3,Spring ideas and model driven architecture</div>
</li>
</ul>

<p>
Atom WebScale : play with only the best in Web world, generate game's website front|admin in few clicks
</p>
<ul>
<li class="level1"><div class="li"> Bridge to Wicket</div>
</li>
<li class="level1"><div class="li"> Bridge to Grails</div>
</li>
<li class="level1"><div class="li"> Bridge to Play</div>
</li>
<li class="level1"><div class="li"> Bridge to SpringMVC</div>
</li>
<li class="level1"><div class="li"> Experiment with HTML5 and JavaScript almighty: Node.js , lot more… <a href="#webscale" title="jme3:advanced:atom_framework:atomex ↵" class="wikilink1">WebScale</a></div>
</li>
</ul>

<p>
Atom Cloud : Modulize the game | application project and deploy structure
</p>
<ul>
<li class="level1"><div class="li"> Bridge to Osgi</div>
</li>
<li class="level1"><div class="li"> Ultimate Maven Gradle automatic deployment</div>
</li>
<li class="level1"><div class="li"> Toward Collabrative enviroment</div>
</li>
</ul>

<p>
Atom Storm : Distributed computing at its finesse
</p>
<ul>
<li class="level1"><div class="li"> Storm: as its best corporator</div>
</li>
<li class="level1"><div class="li"> Hadoop and folks as the runner-up</div>
</li>
<li class="level1"><div class="li"> Come with ready to use tools help 3D rendering and game creating pipeline</div>
</li>
</ul>

<p>
Atom Universal : Bring it all to common open infrastructure
</p>
<ul>
<li class="level1"><div class="li"> Full distributed packages of the Atom framework online</div>
</li>
<li class="level1"><div class="li"> Dynamic flexiable linkage that can suite almost teamwork game developing projects</div>
</li>
<li class="level1"><div class="li"> Simple but powerful Pipeline | Workflow designer</div>
</li>
<li class="level1"><div class="li"> A lot of examples , architype , free stuffs</div>
</li>
<li class="level1"><div class="li"> Code link to OpenShift, Heroku, GoogleAppEngine, AppFrog,… via Git, SVN , Mecury</div>
</li>
<li class="level1"><div class="li"> Utilites to use standard deploy solutions …</div>
</li>
</ul>

<p>
Atom Star Dust:
</p>
<ul>
<li class="level1"><div class="li"> Smallscale version of those mentioned components, toward mobile devices and web-base, HTML5 games for ex.</div>
</li>
<li class="level1"><div class="li"> Every where, small tiny, fastest, embed inside others, stick together well. </div>
</li>
<li class="level1"><div class="li"> This is specific component of Atom framework really show up as “Atom”</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Architecture and components" [2751-4862] -->
<h3 class="sectionedit5" id="vision">Vision</h3>
<div class="level3">

<p>
Without trying to bloat, this is a most attractive point of the whole framework - Atom. 
</p>

<p>
You have open computing power, open infrastructure, open storage and everything under your hand and work as you wish!
</p>

<p>
Toward “cloud” for game development and gaming, even better than that! 
</p>

<p>
Metaphorically, it's the sweestest result you can milk from the open source cows :p (Sorry if the idiom offense anyone) 
</p>

<p>
Yeah, money somehow..? But Open spirit in its heart! 
</p>

</div>
<!-- EDIT5 SECTION "Vision" [4863-5339] -->
<h3 class="sectionedit6" id="other_open-source_dependencies">Other open-source dependencies</h3>
<div class="level3">

<p>
</p><p></p><div class="notewarning">Hundred of opensource projects…Nail it
</div>


<p>
<a href="/jme3/atomixtuts.html" class="wikilink1" title="jme3:atomixtuts"> Atomix Series of game making</a>
</p>

<p>
GOTO <a href="/jme3/advanced/atom_framework.html" class="wikilink1" title="jme3:advanced:atom_framework">This Part of Atom framework </a>
</p>

</div>
<!-- EDIT6 SECTION "Other open-source dependencies" [5340-] -->
