---
title: Atom Framework Design
---
<h2 class="sectionedit1" id="atom_framework_design">Atom Framework Design</h2>
<div class="level2">

<p>
This is the repository resulted of the design phase of Atom framework over years.
</p>

</div>
<!-- EDIT1 SECTION "Atom Framework Design" [1-116] -->
<h3 class="sectionedit2" id="motivation">Motivation</h3>
<div class="level3">

<p>
It born to helps JME3 focus in <strong>game/simulation development</strong>, push futher in lastest/future Java technologies toward to enterpise/AAA game dev as its final goal, but compromise/ compatible with existing insfracture of JME3 and OpenGL.
</p>

<p>
Its concept, design and archictecture inspired by AAA game engine and Enterprise Java solution.
</p>

</div>
<!-- EDIT2 SECTION "Motivation" [117-471] -->
<h3 class="sectionedit3" id="overview">Overview</h3>
<div class="level3">

<p>
In this page:
</p>
<ol>
<li class="level1"><div class="li"> Goal of Atom framework - which tend to expand JME3 and Java language to suite more for game dev.</div>
</li>
<li class="level1"><div class="li"> Problems of realtime applications (especially games).</div>
</li>
<li class="level1"><div class="li"> Solutions and those base platforms, frameworks that we going to use to approach those goals.</div>
</li>
<li class="level1"><div class="li"> Remain works and future vision</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Overview" [472-796] -->
<h2 class="sectionedit4" id="design_goals">Design goals</h2>
<div class="level2">

</div>

<h4 id="overal_goals">Overal goals</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> Flexible: Game | simulations centric but not forced!</div>
</li>
<li class="level1"><div class="li"> Modular: Dependency injection along with Component injection</div>
</li>
<li class="level1"><div class="li"> Parallel: Embrace parallel computing</div>
</li>
<li class="level1"><div class="li"> Next gen: Come with Bleeding edge technologies and powers of Java languages</div>
</li>
<li class="level1"><div class="li"> Cloud ready: Scale to web and distributed computing</div>
</li>
<li class="level1"><div class="li"> With ease: <abbr title="Graphical User Interface">GUI</abbr> Tools everywhere, almost zero config need</div>
</li>
<li class="level1"><div class="li"> Cross devices: Can run wide range of devices PC-mobile-TV.. any one that has java!</div>
</li>
</ul>

</div>

<h4 id="additional_sub_goals">Additional sub goals</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> Minimum dependencies and their overlap</div>
</li>
<li class="level1"><div class="li"> Small footprint &amp; Efficient</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Design goals" [797-1390] -->
<h3 class="sectionedit5" id="slides">Slides</h3>
<div class="level3">

<p>
You can view slides and download papers about the design of Atom framework here.
</p>

</div>
<!-- EDIT5 SECTION "Slides" [1391-1488] -->
<h2 class="sectionedit6" id="real_time_applications">Real time applications</h2>
<div class="level2">

<p>
Atom is designed to <strong>MAKE</strong> concurrent, real-time, embedded systems and <strong>GAMES</strong>
</p>

</div>
<!-- EDIT6 SECTION "Real time applications" [1489-1607] -->
<h3 class="sectionedit7" id="atom_vs_ptolemy">Atom VS ptolemy</h3>
<div class="level3">

<p>
As mentioned in the Atom framwork's introduction, Atom is actually inspired by Plotemy project <a href="http://ptolemy.eecs.berkeley.edu/index.htm" class="urlextern" title="http://ptolemy.eecs.berkeley.edu/index.htm" rel="nofollow">http://ptolemy.eecs.berkeley.edu/index.htm</a>
</p>

<p>
 but it actually tend to has various different goals, techniques, mindset and approaches. The comparasion in constrast with Ptolemy will reveal a lot of Atom characteristics.
</p>
<pre class="code"> The Ptolemy project studies modeling, simulation, and design of concurrent, real-time, embedded systems. The focus is on assembly of concurrent components. The key underlying principle in the project is the use of well-defined models of computation that govern the interaction between components.A major problem area being addressed is the use of heterogeneous mixtures of models of computation.</pre>

<p>
<strong>VS</strong>
</p>
<pre class="code"> Atom is designed to **MAKE** concurrent, real-time, embedded systems and **GAMES**. So it focus more in code generation, profile, monitoring; focus more in graphics, physics, **player experience**... etc.   Underlying, it borrow quite a bunch of concepts that built in Ptolemy (not codes!).</pre>

</div>

<h4 id="goals">Goals</h4>
<div class="level4">

<p>
So the two projects' <strong>goals</strong> are quite overlapped but have different focus points and mindset!
</p>
<ul>
<li class="level1"><div class="li"> Atom has no or less concern/ interests about mathematic/ physics correctioness ( so simmulations) but the graphics side and overal behaviors.</div>
</li>
<li class="level1"><div class="li"> Atom has open-source spirit… but not academic!! You can see Plotemy is quite “complicated” and not very popular as it provided for academic first; in constrast, Atom is broadcasted for every one to use and to make games as kids in sandboxes. </div>
</li>
</ul>

</div>

<h4 id="techniques_differencies">Techniques differencies:</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> Atom not “just” depend on well-defined models!</div>
</li>
<li class="level1"><div class="li"> Atom use simplier models, …but sometime simplier is better! </div>
<ul>
<li class="level2"><div class="li"> Simplier Entity model (not abstract out of Java object)</div>
</li>
<li class="level2"><div class="li"> Actor model is not as abstrat also actually from threaded enviroment</div>
</li>
<li class="level2"><div class="li"> No contract in Systems, the study of Systems conections and interactivities are though data-driven analysising only, that's it, a dataflow monitoring system over working system.</div>
</li>
<li class="level2"><div class="li"> Timming: Because of the lack of interests in math/ phycics, time model and precision model is undefined but also from Java platform.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Those above and its core techniques that you can find below, lead Atom to be less independent from Java but also has well embeding characteristics of Java languages and run-time enviroments. So can say Atom is built directly on top of Java with no hesitate!</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Atom VS ptolemy" [1608-4036] -->
<h3 class="sectionedit8" id="atom_vs_jscience">Atom VS JScience</h3>
<div class="level3">

<p>
Atom also depends in Javolution and has some parts from JScience code base but once again the purpose, Atom focus in Games and simulations… Also a lot of techniques Atom is different from one used in JScience.
</p>

<p>
One can also see that Atom fullfill the lack of JScience's experimental Game package. :)
</p>

</div>
<!-- EDIT8 SECTION "Atom VS JScience" [4037-4365] -->
<h3 class="sectionedit9" id="target_devices_platforms">Target Devices &amp; Platforms</h3>
<div class="level3">

</div>

<h4 id="pc">PC</h4>
<div class="level4">

</div>

<h4 id="mobile">Mobile</h4>
<div class="level4">

</div>

<h5 id="android">Android</h5>
<div class="level5">

</div>

<h4 id="web">Web</h4>
<div class="level4">

</div>

<h5 id="html5_and_webgl">HTML5 and WebGL</h5>
<div class="level5">

</div>
<!-- EDIT9 SECTION "Target Devices & Platforms" [4366-4472] -->
<h2 class="sectionedit10" id="problems">Problems</h2>
<div class="level2">

</div>
<!-- EDIT10 SECTION "Problems" [4473-4494] -->
<h2 class="sectionedit11" id="solutions_frameworks_platforms">Solutions &amp; Frameworks &amp; Platforms</h2>
<div class="level2">

<p>
In Java, a lot good opensource projects are already provide solutions for various challanges in software developments. The problem is how to glue those gems together in appropriate way and result in efficient, good quality product - Saving time and efforts.
</p>

<p>
</p><p></p><div class="notewarning">Hundred of opensource projects…
</div>


<p>
For example, AtomCore module depends in these high quality libraries:
</p>
<ul>
<li class="level1"><div class="li"> JME3</div>
</li>
<li class="level1"><div class="li"> Common Java JSR annotations:</div>
</li>
<li class="level1"><div class="li"> Apache commons </div>
<ul>
<li class="level2"><div class="li"> Lang</div>
</li>
<li class="level2"><div class="li"> Configurations</div>
</li>
<li class="level2"><div class="li"> BeanUtils</div>
</li>
<li class="level2"><div class="li"> Collections</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Google's </div>
<ul>
<li class="level2"><div class="li"> Guava:</div>
</li>
<li class="level2"><div class="li"> Guice: Dependency injection</div>
</li>
<li class="level2"><div class="li"> Snappy:</div>
</li>
<li class="level2"><div class="li"> LevelDB</div>
</li>
<li class="level2"><div class="li"> Auto</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> </div>
</li>
</ul>

<p>
Other require pieces are write from sk
</p>

</div>
<!-- EDIT11 SECTION "Solutions & Frameworks & Platforms" [4495-5200] -->
<h2 class="sectionedit12" id="atom_framework_design_course">Atom framework Design course</h2>
<div class="level2">

<p>
This section is dedicated to explain some idioms, patterns, and long term solutions for problems and each design goals, structures.
</p>

</div>
<!-- EDIT12 SECTION "Atom framework Design course" [5201-5372] -->
<h3 class="sectionedit13" id="game_and_real-time_application">Game and real-time application</h3>
<div class="level3">

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
The game “software” should be published in specific enviroment, it then has:
</p>
<ul>
<li class="level1"><div class="li"> Configurations : appropriate settings for specific enviroment, device.</div>
</li>
<li class="level1"><div class="li"> Data : appropriate size and format</div>
</li>
</ul>

</div>

<h4 id="cpu-gpu_interactions">CPU-GPU interactions</h4>
<div class="level4">

</div>

<h4 id="java-native_interactions">Java-Native interactions</h4>
<div class="level4">

</div>

<h4 id="timing">Timing</h4>
<div class="level4">

</div>

<h4 id="cycle">Cycle</h4>
<div class="level4">

</div>
<!-- EDIT13 SECTION "Game and real-time application" [5373-6647] -->
<h3 class="sectionedit14" id="atomcore_architecture">AtomCore Architecture</h3>
<div class="level3">

<p>
The Core is the part that focus in <strong>Game and real-time application</strong>. It declare
</p>

<p>
You can read more about the Core architecture here.
<a href="/jme3/advanced/atom_framework/atomcore.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore">atomcore</a>
</p>

</div>
<!-- EDIT14 SECTION "AtomCore Architecture" [6648-6856] -->
<h3 class="sectionedit15" id="design_patterns_programming_paradigms">Design patterns &amp; Programming paradigms</h3>
<div class="level3">

<p>
Consider research through this trusted resources before we go deeper into Atom architecture and where/why/how it apply each Design patterns:
</p>

<p>
<a href="/jme3/advanced/atom_framework/design/patterns.html" class="wikilink1" title="jme3:advanced:atom_framework:design:patterns">patterns</a>
</p>

</div>
<!-- EDIT15 SECTION "Design patterns & Programming paradigms" [6857-7095] -->
<h3 class="sectionedit16" id="programming_aspects">Programming aspects</h3>
<div class="level3">

</div>

<h4 id="java_but_not_just_java">Java, but not just Java</h4>
<div class="level4">

<p>
The most “Java” things in AtomCore is Bean and Properties. Two pure Java data type which are very useful in Game world. Bean is for game object modeling and Properties for configuration.
</p>

<p>
Of course, other Java technologies are also used but not mentioned because it's not nessesary. But Bean and Properties are the two techs that heavily used!
</p>

<p>
“Good” Java extensions used in AtomCore 0.2+ is:
Guava:
</p>
<ul>
<li class="level1"><div class="li"> Bring Eventbus, network in a snap</div>
</li>
<li class="level1"><div class="li"> Collection, Fluent, functional syntax and flavour to Java.</div>
</li>
<li class="level1"><div class="li"> Guava also support Cache, reflection and more low level operations</div>
</li>
</ul>

<p>
Guice: bring Dependency injection, better unit test, refactoring in a lightweight manner.
</p>

<p>
Groovy is a JVM language and intergrated deeply with AtomCore, most appreal as Scripting language but remember it also can replace Java, or seen as Java. Groovy also offer much more of superb things.
</p>

</div>

<h4 id="code_vs_data">Code vs Data</h4>
<div class="level4">

<p>
For big game, the amount of Data required can be so much. Mean while the complexity of code also rise fast, as the result of data increasing!
</p>

<p>
At some point, we have to find a solution to reduce “manual” Data + code making and maintaining. That where “generative code” also can be seen as a kind of Data was born. This called Data-driven architecture (solution). In AtomCore 0.2, it have features to support this trend.
</p>

</div>

<h4 id="around_bean">Around Bean</h4>
<div class="level4">

<p>
</p><p></p><div class="noteclassic">This is so important to mention that every techs Atom framework are around Bean/ POJO technologies. 
</div>
For example:

<ul>
<li class="level1"><div class="li"> AtomEX : the bridge to AKKA Actor model also use POJO as its candidate</div>
</li>
<li class="level1"><div class="li"> EJB leverage…</div>
</li>
<li class="level1"><div class="li"> Fx: use POJO as its effect elements</div>
</li>
</ul>

<p>
Here is a brief explaination why Bean/ POJO is choosed to be the Core of Atom framework?
</p>
<pre class="code">As built in Java technologies, Bean/ POJO is the only "consider good" solution as:
**"the bridge"** **from Java OOP to COP**, **from Java OOP to AOP**</pre>
<pre class="code">also can be seen as 
**from Object oriented programming to Data oriented programming**
**from Object oriented programming to Aspect oriented programming**</pre>
<pre class="code">or **Code but also Data**...</pre>

</div>
<!-- EDIT16 SECTION "Programming aspects" [7096-9185] -->
<h3 class="sectionedit17" id="polygot_programming">Polygot programming</h3>
<div class="level3">
<pre class="code"> I want Best of both worlds!!
 (.. if it's possible?)</pre>

<p>
Atom in its core try to be polymorphism (polygot programming), to suite with OOP, COP, AOP or functional … Yeah, it's java after all but good kind of Java.
</p>

<p>
Because AtomScripting and others use Groovy, so it inherit (a lot of) polygot capacity from Groovy.
</p>

<p>
Read: <a href="http://groovy.codehaus.org/Polyglot+Programming+with+Groovy" class="urlextern" title="http://groovy.codehaus.org/Polyglot+Programming+with+Groovy" rel="nofollow">http://groovy.codehaus.org/Polyglot+Programming+with+Groovy</a>
</p>

</div>

<h4 id="functional_reactive_programming">Functional reactive programming</h4>
<div class="level4">

</div>

<h4 id="flow_based_programming">Flow based programming</h4>
<div class="level4">

</div>

<h4 id="component_based_programming">Component based programming</h4>
<div class="level4">

</div>

<h4 id="composite_based_programming">Composite based programming</h4>
<div class="level4">

</div>

<h4 id="data-driven_model-driven_domain-driven">Data-driven &amp; Model-driven &amp; Domain-driven</h4>
<div class="level4">

</div>
<!-- EDIT17 SECTION "Polygot programming" [9186-9793] -->
<h3 class="sectionedit18" id="modular_architecture">Modular architecture</h3>
<div class="level3">
<pre class="code"> I want to reuse (or DRY)!!</pre>

<p>
Take a look at a JME3 game, Manager for example, what if you want the two manager's work together but loosely depend on each other, or what if you want the State to direct the Manager to do something but have minimal informations about them…
</p>

<p>
More abstract, whenever you have some kind of Service, which is loosely depend on each other, you should try Dependency Injection <a href="http://martinfowler.com/articles/injection.html" class="urlextern" title="http://martinfowler.com/articles/injection.html" rel="nofollow">http://martinfowler.com/articles/injection.html</a> .
</p>

<p>
That's where Guice help in the big picture.
</p>

</div>

<h4 id="dependency_injection">Dependency injection</h4>
<div class="level4">

<p>
<a href="https://code.google.com/p/google-guice/" class="urlextern" title="https://code.google.com/p/google-guice/" rel="nofollow">https://code.google.com/p/google-guice/</a>
</p>

</div>

<h4 id="component_injection">Component Injection</h4>
<div class="level4">

<p>
<a href="http://wiki.apidesign.org/wiki/Component_Injection" class="urlextern" title="http://wiki.apidesign.org/wiki/Component_Injection" rel="nofollow">http://wiki.apidesign.org/wiki/Component_Injection</a>
</p>

</div>

<h4 id="dependency_injection_vs_component_injection">Dependency injection VS Component Injection</h4>
<div class="level4">

<p>
<a href="http://code.imagej.net/gbh/lookup/DependencyInjectionandLookup.html" class="urlextern" title="http://code.imagej.net/gbh/lookup/DependencyInjectionandLookup.html" rel="nofollow">http://code.imagej.net/gbh/lookup/DependencyInjectionandLookup.html</a>
</p>

</div>

<h4 id="dependency_management_coolness">Dependency management coolness</h4>
<div class="level4">

<p>
So what's cool about dependency in real-time application and game that Atom included…
A lot of things, but let me point out fews: 
</p>

<p>
<strong>Real-time dependency</strong> is a new feature for game developing…
Imagine that even the game just can load part of assets, with the other are delayed or missing, the dependency graph can help the game cycle continue to run, part of it in the mean time. 
</p>

<p>
In fact the dependency graph can be considered the topo structure of JME assets dependency graph before it built, means hard links via references. Now even when the assets graph are just partly loaded, the game can run because it know a resolution to safety resolve the assets graph and scene graph afterward.
</p>

<p>
<strong>Enterprise features</strong>
You can imagine how Atom framework tend to bridge JME game and the Web universal. It's not so hard in fact. Cause Java enterprise technologies are already there to use. Lot of them are built on the top of Dependency injection and Inversion of control (or else)… I really like dependency injection but I can not agree that i should always couple with IoC per se. This will be discuss later in this documentation
</p>

</div>
<!-- EDIT18 SECTION "Modular architecture" [9794-11767] -->
<h2 class="sectionedit19" id="enterprise_facilities">Enterprise facilities</h2>
<div class="level2">

</div>

<h4 id="services_dependency_and_decoupling">Services, Dependency and Decoupling</h4>
<div class="level4">

<p>
The world of enteprise evolve Modular paradigm a lot to link services (database, configurations, network protocols, web…) and help they work together in one application. 
</p>

</div>
<!-- EDIT19 SECTION "Enterprise facilities" [11768-12014] -->
<h3 class="sectionedit20" id="available_services">Available Services</h3>
<div class="level3">

<p>
Try AtomEx
</p>

</div>

<h4 id="to_database">To Database</h4>
<div class="level4">

</div>

<h4 id="to_other_repository">To other repository</h4>
<div class="level4">

</div>

<h4 id="to_configurations">To configurations</h4>
<div class="level4">

</div>

<h4 id="to_web">To web</h4>
<div class="level4">

</div>
<!-- EDIT20 SECTION "Available Services" [12015-12136] -->
<h2 class="sectionedit21" id="monitoring_and_development_workflow">Monitoring and development workflow</h2>
<div class="level2">

</div>
<!-- EDIT21 SECTION "Monitoring and development workflow" [12137-12182] -->
<h2 class="sectionedit22" id="future_vision">Future vision</h2>
<div class="level2">

</div>
<!-- EDIT22 SECTION "Future vision" [12183-12206] -->
<h2 class="sectionedit23" id="references_and_inspiration">References and Inspiration</h2>
<div class="level2">

<p>
Atom framework's design is inspried by:
</p>
<ul>
<li class="level1"><div class="li"> Game Engine Architcture book</div>
</li>
<li class="level1"><div class="li"> Game Programming gems serires</div>
</li>
<li class="level1"><div class="li"> AI Game Engine book</div>
</li>
<li class="level1"><div class="li"> AI Game Wisdom book</div>
</li>
</ul>

<p>
other GameEngine that I did use:
</p>
<ul>
<li class="level1"><div class="li"> UDK</div>
</li>
<li class="level1"><div class="li"> Unity</div>
</li>
<li class="level1"><div class="li"> CryEngineSDK</div>
</li>
<li class="level1"><div class="li"> JavaScript game engines : CraftyJs, GameQuery ..</div>
</li>
<li class="level1"><div class="li"> Flash game engines : Starling ,</div>
</li>
<li class="level1"><div class="li"> … dozen of close-source engine.</div>
</li>
</ul>

<p>
other Java techs:
</p>
<ul>
<li class="level1"><div class="li"> EJB</div>
</li>
<li class="level1"><div class="li"> Spring</div>
</li>
<li class="level1"><div class="li"> Groovy</div>
</li>
<li class="level1"><div class="li"> Netbean</div>
</li>
<li class="level1"><div class="li"> … hunread of open-source projects</div>
</li>
</ul>

<p>
Full researched papers list are comming.
</p>

</div>
<!-- EDIT23 SECTION "References and Inspiration" [12207-] -->
