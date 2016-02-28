---
title: AtomAI
---
<h2 class="sectionedit1" id="atomai">AtomAI</h2>
<div class="level2">

<p>
Hi,
</p>

<p>
This is the wiki for Atom AI framework.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://blogs.ifsworld.com/wp-content/uploads/2012/11/AI-lowres.jpg"><img src="/resources/fetch.php" class="mediaright" title="blogs.ifsworld.com_wp-content_uploads_2012_11_ai-lowres.jpg" alt="blogs.ifsworld.com_wp-content_uploads_2012_11_ai-lowres.jpg" width="200" /></a>
</p>

</div>
<!-- EDIT1 SECTION "AtomAI" [1-140] -->
<h3 class="sectionedit2" id="questions_and_answers">Questions and Answers</h3>
<div class="level3">

<p>
<strong>Question:</strong> What's the h#$ll is AI or why should I bother in this thingy anyway <img src="/lib/images/smileys/icon_question.gif" class="icon" alt=":?:" />
</p>

<p>
<strong>Answer:</strong> It's big, over-complicated and also attractive subject in Game developing.. <img src="/lib/images/smileys/icon_exclaim.gif" class="icon" alt=":!:" /> <img src="/lib/images/smileys/icon_cool.gif" class="icon" alt="8-)" />
</p>

<p>
<strong>Question:</strong> What can be use in my game?
</p>

<p>
<strong>Answer:</strong> Everything… You can use this lib to:
</p>
<ul>
<li class="level1"><div class="li">  solve the common path finding, </div>
</li>
<li class="level1"><div class="li"> let your creature know how to think and learn, </div>
</li>
<li class="level1"><div class="li"> direct your vehicle the way to move, </div>
</li>
<li class="level1"><div class="li"> your camera to interact with the screen, </div>
</li>
<li class="level1"><div class="li"> teach your characters to walk/ talk/ shoot/ trading… </div>
</li>
<li class="level1"><div class="li"> You can also use it in various type of simulations and </div>
</li>
<li class="level1"><div class="li"> even try to solve a mathematic problem.</div>
</li>
</ul>

<p>
<strong>Question:</strong> Sound wonderful…? But wait… It should be soooooooo freaking big and heavy, is it <strong>real-time</strong> shit?
</p>

<p>
<strong>Answer:</strong> Yes, partly… Some parts are real heavy for real time computing. They just can be used in non real time application or few kind of games. Others apx 60% are designed well enough to run in real time, and also provided with JME examples. It also comes with architectures/ functions that can config, optimize, balance, cache, and batch it selfs for real-time applications…
</p>

<p>
<strong>Question:</strong> Eh… Universal solution can not be true…
</p>

<p>
<strong>Answer:</strong> Let's me explain. Consider this a warper of every good open-source java AI libraries you can name out and hook in to JME architecure (AppState, Sptial, Entity, Control, Update cycle…etc). Under the hood, I use Guice| OSGi |Felix to dynamicly link/bind them, when you need it. The full explaination you will find below.
</p>

<p>
<strong>Question:</strong> Nice, I want to try it?
</p>

<p>
<strong>Answer:</strong> Everything is here at once, sir/ madam !
More questions ? Not convinced yet? Go to <a href="#faq" title="jme3:advanced:atom_framework:ai ↵" class="wikilink1">FAQ</a>
</p>

</div>
<!-- EDIT2 SECTION "Questions and Answers" [141-1843] -->
<h3 class="sectionedit3" id="introducing_atom_ai_framework">Introducing Atom AI framework</h3>
<div class="level3">

<p>
This Atom AI framework are more or less a “framework” to bring AI to jME3 game (also means real-time application)!
</p>

<p>
</p><p></p><div class="notetip">Here is my picked list of <a href="/doku.php/jme3:advanced:atom_framework:ai:researches" class="wikilink2" title="jme3:advanced:atom_framework:ai:researches" rel="nofollow">researches</a> and articles you can read in AI field (game and none-game) 
</div>


</div>
<!-- EDIT3 SECTION "Introducing Atom AI framework" [1844-2162] -->
<h3 class="sectionedit4" id="idea_buzz">Idea &amp; Buzz</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> It contains warpers for various java AI libraries build on top of light-weight, configable module architecture and provide the way to hook seamlessly to jME3 games. </div>
</li>
<li class="level1"><div class="li"> It's also come up with a lot of working examples in several game genre (RTS, RPG, FPS, Sport,…). </div>
</li>
<li class="level1"><div class="li"> 40% of components, AI algorimth are rewritten by the author (@atomix) to be light-weight and usable in real-time application.</div>
</li>
<li class="level1"><div class="li"> Tend to be used in production application and games and suppose to support broadest cases it can.</div>
</li>
<li class="level1"><div class="li"> Users can use the pieces to build up their own AI part of their games and apps</div>
</li>
<li class="level1"><div class="li"> Pushed to future java techs: dependencies injection, parallel as its core…</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Idea & Buzz" [2163-2858] -->
<h3 class="sectionedit5" id="features">Features</h3>
<div class="level3">

<p>
(T) means additional Tools are supported
</p>

<p>
(C) means with examples cases
</p>

<p>
(E) means use| depend on external libs 
</p>

<p>
</p><p></p><div class="noteimportant">Note that: despite of the fact, the lib has a lot of dependencies, the author always try have simple fallback - homegrown implemention.  Of course, support a fewer use cases, mainly for specific game genres, but it's better than nothing, that's the bright side 
</div>


<p>
</p><p></p><div class="noteimportant">Read alternatives and searches if you want to go further than Atom!
</div>


</div>

<h4 id="framework">Framework</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> Modulize (E)</div>
</li>
<li class="level1"><div class="li"> Dependency free (E)</div>
</li>
<li class="level1"><div class="li"> Configable , balancable , profilable , level of detail (T)</div>
</li>
<li class="level1"><div class="li"> Paralel (E)</div>
</li>
</ul>

</div>

<h4 id="data_structure">Data Structure</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> State (T)</div>
</li>
<li class="level1"><div class="li"> Tree (T)</div>
</li>
<li class="level1"><div class="li"> Graph (T)(E)</div>
</li>
<li class="level1"><div class="li"> Geometric (T)(E)</div>
</li>
</ul>

</div>

<h4 id="general_algorimth_and_support_techs">General algorimth and Support techs</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> Optimizing problem(E)</div>
</li>
<li class="level1"><div class="li"> Constraint programming(E)</div>
</li>
<li class="level1"><div class="li"> Fuzzy logic(E)</div>
</li>
<li class="level1"><div class="li"> Probability</div>
</li>
<li class="level1"><div class="li"> Genetic (T)(E)</div>
</li>
<li class="level1"><div class="li"> Neutral network (T)(E)</div>
</li>
<li class="level1"><div class="li"> Rule base (T)(E)</div>
</li>
<li class="level1"><div class="li"> Scripting (T)</div>
</li>
</ul>

</div>

<h4 id="general_ai_techs">General AI Techs</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> Movement</div>
<ul>
<li class="level2"><div class="li"> Kinematic</div>
</li>
<li class="level2"><div class="li"> Physics embed</div>
</li>
<li class="level2"><div class="li"> Steering</div>
<ul>
<li class="level3"><div class="li"> Boid</div>
</li>
<li class="level3"><div class="li"> Swarm</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> Formation</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> FSM , HFSM , FFSM for AI (T)</div>
</li>
<li class="level1"><div class="li"> Searching</div>
<ul>
<li class="level2"><div class="li"> Path finding </div>
<ul>
<li class="level3"><div class="li"> algorimth: A Star, theta Star </div>
</li>
<li class="level3"><div class="li"> space: Grid, Hex, Tris, Polys, 3D Block, 3D Terrain, NavMesh, points cloud/, graphs… [more]</div>
</li>
<li class="level3"><div class="li"> generate methods: navmesh gen,jump points, choke points, viewset points, … [more]</div>
</li>
<li class="level3"><div class="li"> re-touch methods: smooth, reduce, prunning, time-wise, cahing, progessive</div>
</li>
<li class="level3"><div class="li"> highly extensible, hookable, configableready to use as corporated with lower and higher techs</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> General path finding</div>
<ul>
<li class="level3"><div class="li"> Iterative deepending</div>
</li>
<li class="level3"><div class="li"> Some academic stuffs …</div>
</li>
</ul>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Reasoning</div>
<ul>
<li class="level2"><div class="li"> Decision Tree </div>
</li>
<li class="level2"><div class="li"> Minimax</div>
</li>
<li class="level2"><div class="li"> Some academic stuffs …</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Planning</div>
<ul>
<li class="level2"><div class="li"> Goal base</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Problem sovling</div>
</li>
<li class="level1"><div class="li"> Learning</div>
</li>
</ul>

</div>

<h4 id="character_ai">Character AI</h4>
<div class="level4">

</div>

<h5 id="human">Human</h5>
<div class="level5">
<ul>
<li class="level1"><div class="li"> Chatbot  (T)(E)(C)</div>
</li>
<li class="level1"><div class="li"> Dialoge (T)(C)</div>
</li>
<li class="level1"><div class="li"> Emotion (T)(C)</div>
</li>
<li class="level1"><div class="li"> Facial (T)(C)</div>
</li>
<li class="level1"><div class="li"> Voice (T)(E)</div>
</li>
<li class="level1"><div class="li"> Gesture (T)(E)</div>
</li>
<li class="level1"><div class="li"> CommonSense (C)</div>
</li>
<li class="level1"><div class="li"> Common Human AI usecases (C)</div>
</li>
</ul>

</div>

<h5 id="animal">Animal</h5>
<div class="level5">

</div>
<!-- EDIT5 SECTION "Features" [2859-4873] -->
<h3 class="sectionedit6" id="architecture_and_components">Architecture and components</h3>
<div class="level3">

<p>
Here are its <a href="/doku.php/jme3:advanced:atom_framework:ai:architecture:architecture" class="wikilink2" title="jme3:advanced:atom_framework:ai:architecture:architecture" rel="nofollow">Architecture</a> and <a href="/doku.php/jme3:advanced:atom_framework:ai:components:components" class="wikilink2" title="jme3:advanced:atom_framework:ai:components:components" rel="nofollow">Components</a>.
</p>

<p>
<iframe title="600px,600px" src="http://bubbl.us/view/1860d6/2fd76d/15vmlQSf.3GMg/" style="width:98%; height:400px"></iframe>
</p>

</div>
<!-- EDIT6 SECTION "Architecture and components" [4874-5122] -->
<h3 class="sectionedit7" id="vision">Vision</h3>
<div class="level3">

<p>
As the framework grown up, I will bring more unit tests and example cases.
</p>

<p>
Also it should has even better integration with the JME SDK and other Netbean's plugins like (weka, neuphons…). Corporate with Code gen, it's can easily replace Alice, Manson,etc…  as much better 3D non-coding enviroment and one day maybe become the most advanced AI simulation enviroment on earth! 
</p>

</div>
<!-- EDIT7 SECTION "Vision" [5123-5517] -->
<h3 class="sectionedit8" id="faq">FAQ</h3>
<div class="level3">

<p>
<strong>Question</strong>: Why warpers?
</p>

<p>
<strong>Answer</strong>: Not reinventing the wheel, trust in good opensource project, broader use caces, broader user… And last but not least, it's just work!
</p>
<hr />

<p>
<strong>Question</strong>: Why java 1.5+?
</p>

<p>
<strong>Answer</strong> : Consider this lib is a push to java techs and java's game techs. The user are forced to get familiar with the changing world… Yes, AI is a rapid changing subject and we (java game devs) should keep up.
</p>
<hr />

<p>
<strong>Question</strong>: Why f$#kin heavy and not light-weight, real-time, etc???
</p>

<p>
<strong>Answer</strong>: This libs provide some features which just optimized enough to run in “quite” high performance machine. But it also have sotiphicated methods to config it self. Consider this key feature to keep in mind. Get fit!
</p>
<hr />

<p>
<strong>Question</strong>: Big jar?
</p>

<p>
<strong>Answer</strong>: Nope, consider not too big… thanks to Guice, size &lt; 6MBs and can even smaller if you compile it your self and cut the unneccesary things. In some case you want to use <strong>ALL</strong> the features, the whole dependencies will take about <strong>78MB</strong> and <strong>45MB</strong> for the SDK plugins! And Maven should be to used to get every artifacts!
</p>
<hr />

<p>
<strong>Question</strong>: Documentations and javadoc?
</p>

<p>
<strong>Answer</strong> : On its way, the orginal author (me, @atomix) are slow (busy) , volunteers are welcome! Also read all the external wel-documented open source libs <a href="/doku.php/jme3:advanced:atom_framework:ai:libs" class="wikilink2" title="jme3:advanced:atom_framework:ai:libs" rel="nofollow"> Full list here</a> that this lib depend on are quite enough. Cause its idiom is simple.
</p>
<hr />

<p>
<strong>Question</strong>: I have ideas?
</p>

<p>
<strong>Answer</strong> : Tell me , @atomix in the forum.
</p>

</div>
<!-- EDIT8 SECTION "FAQ" [5518-7041] -->
<h3 class="sectionedit9" id="other_open-source_dependencies">Other open-source dependencies</h3>
<div class="level3">

<p>
As said, even if I try to rewriten some parts that most critical for real time game, I cannot against the ideas of including every good functions of other libs. So, I provide good way to communicate between them and the way to link them on demand…
</p>

<p>
Let name the libs can be used:
As category
</p>
<ul>
<li class="level1"><div class="li"> Neutral Network</div>
</li>
<li class="level1"><div class="li"> Machine Learning</div>
</li>
<li class="level1"><div class="li"> Search</div>
</li>
<li class="level1"><div class="li"> Constraint programming</div>
</li>
<li class="level1"><div class="li"> Geometry constraint</div>
</li>
<li class="level1"><div class="li"> Human language processing</div>
<ul>
<li class="level2"><div class="li"> Chatbot</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Other open-source dependencies" [7042-7524] -->
<h2 class="sectionedit10" id="documentation">Documentation</h2>
<div class="level2">

</div>
<!-- EDIT10 SECTION "Documentation" [7525-7550] -->
<h3 class="sectionedit11" id="basic">Basic</h3>
<div class="level3">

</div>
<!-- EDIT11 SECTION "Basic" [7551-7566] -->
<h3 class="sectionedit12" id="examples_usecases">Examples &amp; Usecases</h3>
<div class="level3">

</div>
<!-- EDIT12 SECTION "Examples & Usecases" [7567-7596] -->
<h3 class="sectionedit13" id="api">API</h3>
<div class="level3">

</div>
<!-- EDIT13 SECTION "API" [7597-7610] -->
<h2 class="sectionedit14" id="alternatives">Alternatives</h2>
<div class="level2">

</div>
<!-- EDIT14 SECTION "Alternatives" [7611-7635] -->
<h3 class="sectionedit15" id="open_sources">Open sources</h3>
<div class="level3">

</div>
<!-- EDIT15 SECTION "Open sources" [7636-7658] -->
<h3 class="sectionedit16" id="commercial">Commercial</h3>
<div class="level3">

</div>
<!-- EDIT16 SECTION "Commercial" [7659-7679] -->
<h3 class="sectionedit17" id="toolset">Toolset</h3>
<div class="level3">

</div>
<!-- EDIT17 SECTION "Toolset" [7680-7698] -->
<h2 class="sectionedit18" id="researches">Researches</h2>
<div class="level2">

<p>
Go to <a href="/doku.php/jme3:advanced:atom_framework:researches" class="wikilink2" title="jme3:advanced:atom_framework:researches" rel="nofollow">researches</a>
</p>

</div>
<!-- EDIT18 SECTION "Researches" [7699-] -->
