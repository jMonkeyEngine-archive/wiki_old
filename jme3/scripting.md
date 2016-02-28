---
title: Scripting in JME3 with Groovy. All about it!
---
<h1 class="sectionedit1" id="scripting_in_jme3_with_groovy_all_about_it">Scripting in JME3 with Groovy. All about it!</h1>
<div class="level1">

<p>
<strong>Monkeys</strong>,<br />

<br />

For anyone who still ask for something like <strong>“Scripting” with JME3</strong>, here is it, about it at once! 
</p>

<p>
We nearly reach 3.0, i’m so excited about it and want to write something for it. In this post you will have a good run from Zero to Hero with Groovy and Monkey :p 
Not kidding!
</p>

<p>
<a href="/resources/wiki-stll_monkey_typing.jpg" class="media wikilink2" title="wiki:stll_monkey_typing.jpg"><img src="/resources/wiki-stll_monkey_typing.jpg" class="mediaright" title="100" alt="100" /></a>
</p><p></p><div class="noteimportant"><img src="/lib/images/smileys/icon_question.gif" class="icon" alt=":?:" />
<strong>Quick question</strong>: What this related to my other tuts <img src="/lib/images/smileys/icon_doubt2.gif" class="icon" alt=":-\" /> ?<br />
[atomixtuts]
<strong>Answer</strong>: As I wrote the others, I thought I should write this first, because if no one know about Groovy, no one can understand a single line of my code <img src="/lib/images/smileys/icon_doubt.gif" class="icon" alt=":-/" /> , and it’s bad!
</div>


</div>
<!-- EDIT1 SECTION "Scripting in JME3 with Groovy. All about it!" [1-687] -->
<h2 class="sectionedit2" id="introduction">Introduction:</h2>
<div class="level2">

<p>
We will go from basic setup of Groovy in JMP and then example by example every aspect of game you can develop with Groovy.
More advanced topic come at the end, eg: the way to get the speed of Java, meta-programing, a lot of programming patterns (PP), even AI and Constraint Programming…
Sounds insanse? Nah ah… 
</p>

<p>
</p><p></p><div class="noteimportant"> Let me know if you want to write or to read other topics of Groovy or Scripting. Thanks!
</div>


<p>
Let’s start!
</p>

</div>
<!-- EDIT2 SECTION "Introduction:" [688-1161] -->
<h2 class="sectionedit3" id="content">Content:</h2>
<div class="level2">

<p>
<br />

<br />

<br />

</p>
<ol>
<li class="level1"><div class="li"> GET STARTED</div>
</li>
<li class="level1"><div class="li"> LEARN GROOVY</div>
<ol>
<li class="level2"><div class="li"> Syntax and Gotchas</div>
</li>
<li class="level2"><div class="li"> Meta-programming</div>
</li>
<li class="level2"><div class="li"> Groovy Builder – SwingBuilder</div>
</li>
<li class="level2"><div class="li"> Groovy – for smarty</div>
</li>
<li class="level2"><div class="li"> GPars</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> EMBED GROOVY</div>
<ol>
<li class="level2"><div class="li"> Groovy in JME3</div>
</li>
<li class="level2"><div class="li"> Groovy in JMP</div>
</li>
<li class="level2"><div class="li"> Groovy everywhere (snipets)</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> INTO THE GAME</div>
<ol>
<li class="level2"><div class="li"> Basic Scripts</div>
</li>
<li class="level2"><div class="li"> Event – Trigger Manager</div>
</li>
<li class="level2"><div class="li"> Configurations with Groovy</div>
</li>
<li class="level2"><div class="li"> AI Tricks with Groovy</div>
</li>
<li class="level2"><div class="li"> Build Script with Groovy</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> DESIGN PATTERNS IN GROOVY GAME (WIP)</div>
</li>
<li class="level1"><div class="li"> ADVANCED TRICKS</div>
<ol>
<li class="level2"><div class="li"> Hack the JVM with Groovy</div>
</li>
<li class="level2"><div class="li"> Codegen</div>
</li>
<li class="level2"><div class="li"> Groovy – Almighty God!</div>
</li>
</ol>
</li>
</ol>
<hr />

</div>
<!-- EDIT3 SECTION "Content:" [1162-1747] -->
<h2 class="sectionedit4" id="get_started">GET STARTED</h2>
<div class="level2">

<p>
</p><p></p><div class="notetip">If you already know about Groovy and just curious about how to intergrate Groovy into JME3. Go straight to Part <span class="curid"><a href="/jme3/scripting.html" class="wikilink1" title="jme3:scripting">into_the_game</a></span>
</div>


</div>
<!-- EDIT4 SECTION "GET STARTED" [1748-1933] -->
<h3 class="sectionedit5" id="what_is_groovy">WHAT IS GROOVY?</h3>
<div class="level3">

<p>
<strong>Groovy</strong>… 
<a href="/resources/wiki-groovy-logo.png" class="media wikilink2" title="wiki:groovy-logo.png"><img src="/resources/wiki-groovy-logo.png" class="mediaright" title="200" alt="200" /></a>
</p>

<p>
is an agile and dynamic language for the Java Virtual Machine
builds upon the strengths of Java but has additional power features inspired by languages like Python, Ruby and Smalltalk
</p>

<p>
<a href="http://groovy.codehaus.org/" class="urlextern" title="http://groovy.codehaus.org/" rel="nofollow">http://groovy.codehaus.org/</a>
</p>

</div>
<!-- EDIT5 SECTION "WHAT IS GROOVY?" [1934-2221] -->
<h3 class="sectionedit6" id="highlight">Highlight</h3>
<div class="level3">

<p>
The shortest highlight of the language can be found here:<br />

<a href="http://en.wikipedia.org/wiki/Groovy_%28programming_language%29" class="urlextern" title="http://en.wikipedia.org/wiki/Groovy_%28programming_language%29" rel="nofollow">http://en.wikipedia.org/wiki/Groovy_%28programming_language%29</a>
</p>
<ul>
<li class="level1"><div class="li"> Most valid Java files are also valid Groovy files. Although the two languages are similar, Groovy code can be more compact, because it does not require all the elements that Java requires. This makes it possible for Java programmers to gradually learn Groovy by starting with familiar Java syntax before acquiring more Groovy idioms.</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Groovy features not available in Java include both static and dynamic typing (with the def keyword), closures, operator overloading, native syntax for lists and associative arrays (maps), native support for regular expressions, polymorphic iteration, expressions embedded inside strings, additional helper methods, and the safe navigation operator “?.” to automatically check for nulls (for example, “variable?.method()”, or “variable?.field”).</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Since version 2 Groovy also supports modularity, being able to ship only the needed jars according to the project needs, thus reducing the size of groovy's lib, type checking, static compilation, Project Coin syntax enhancements, multicatch blocks and ongoing performance enhancements using JDK7's invoke dynamic instruction.</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Groovy provides native support for various markup languages such as XML and <abbr title="HyperText Markup Language">HTML</abbr>, accomplished via an inline DOM syntax. This feature enables the definition and manipulation of many types of heterogeneous data assets with a uniform and concise syntax and programming methodology.[citation needed]</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Unlike Java, a Groovy source code file can be executed as an (uncompiled) script if it contains code outside any class definition, is a class with a main method, or is a Runnable or GroovyTestCase. A Groovy script is fully parsed, compiled, and generated before execution (similar to Perl and Ruby). (This occurs under the hood, and the compiled version is not saved as an artifact of the process.)</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Highlight" [2222-4190] -->
<h3 class="sectionedit7" id="setup_groovy">SETUP GROOVY?</h3>
<div class="level3">

<p>
If you used JMP to code your game (I don’t know about Eclipse users, sorry). Go to Update Center to install Groovy plugin, then download the lastest Groovy (ver2.1) and wrap it as a Library. You are ready for the adventure!
</p>

<p>
<a href="http://groovy.codehaus.org/Download?nc" class="urlextern" title="http://groovy.codehaus.org/Download?nc" rel="nofollow">http://groovy.codehaus.org/Download?nc</a>
</p>

</div>
<!-- EDIT7 SECTION "SETUP GROOVY?" [4191-4483] -->
<h3 class="sectionedit8" id="what_can_be_script">WHAT CAN BE SCRIPT</h3>
<div class="level3">

<p>
<em><strong>or “TO SCRIPT OR NOT TO SCRIPT, is the PROBLEM”?</strong></em>
</p>

<p>
<strong>Everything</strong>. 
You can do almost every thing with Groovy just like with Java.
</p>

<p>
In this post i will show example by example every aspect of game you can develop with Groovy. 
</p>

<p>
<em class="u"><strong>Pros:</strong></em>
</p>
<ul>
<li class="level1"><div class="li"> Scripting is very common and intuitive way to do game programing. It's common because it's shorter, cleaner, easy to read, maintain and re-use.</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Groovy is young but developed by very talent people, a lot of devoted contributors. </div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Web and Enterprise in your hand. Ever heard of Grails <a href="http://grails.org/" class="urlextern" title="http://grails.org/" rel="nofollow">http://grails.org/</a>?</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Multi-additions to fullfil Java. God-like in Swing, ORM, XML…</div>
</li>
</ul>
<ul>
<li class="level1"><div class="li"> Performance improved recently: If you worry about the performance, , in the next release, it can even get to the speed of Java, and soon to be a very competitive opponent to Scala! Read this? <a href="http://java.dzone.com/articles/groovy-20-performance-compared" class="urlextern" title="http://java.dzone.com/articles/groovy-20-performance-compared" rel="nofollow">http://java.dzone.com/articles/groovy-20-performance-compared</a></div>
</li>
</ul>

<p>
<em class="u"><strong>Cons:</strong></em>
It’s good, but what about the down-side?
</p>
<ul>
<li class="level1"><div class="li"> Can not run in Android, yet!</div>
</li>
<li class="level1"><div class="li"> Some things can be wrong without noticed, appeared in run-time like every scripting language</div>
</li>
<li class="level1"><div class="li"> Still a performance problem.</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "WHAT CAN BE SCRIPT" [4484-5633] -->
<h3 class="sectionedit9" id="when_to_use_scripting">WHEN TO USE SCRIPTING:</h3>
<div class="level3">

<p>
Some obvious but always existing problems of Scripting. 
</p>

<p>
First every scripting language got the same type-safe dilemma. If you invest too much into Scripting, you fall immediately into the mess that hidden errors which are always very hard to find, only show up in run-time. The balance between benefit and hell of Scripting is thin. 
Duck-typing is not always a win-win.
</p>

</div>

<h4 id="not_type-safe">Not type-safe</h4>
<div class="level4">

<p>
As Groovy support Duck-typing, is almost impossible to know the type, methods of the object you want to use. This can be improved if you are in Static mode but this mode simply not what we really want with Scripting purpose?
</p>

<p>
So, as the question had been asked by a forum's member:
</p><p></p><div class="noteimportant">Heh. I’d love to go Groovy myself, but I’ve been finding it very hard for me to explore the set of methods that a passed-in object supports.<img src="/lib/images/smileys/icon_question.gif" class="icon" alt=":?:" />
</div>
<strong>Answer:</strong>


<p>
From my experience, just ask you self, how “natural” your code are coded, in <strong>OOP</strong> sense:
</p>

<p>
<strong>Chicken.eat(rice)</strong>
<em>You know what methods and their parameter’s type, and name.</em>
</p>

<p>
<strong>Monkey.eat(banana)</strong>
<em>You know what common in classes in a package. Without knowing the inheritance and interface they implemented.</em>
</p>

<p>
<strong>Human.eat([chicken,rice,banana])</strong>
<em>You can guess Human are derivated from Monkey and code are coded flexible, ex: methods are multi-type, optional param. etc…</em>
</p>

<p>
If it have that level of “natural” sense, you don’t have to learn by heart at all, so use scripting in the situation.
</p>

<p>
In other hand, this very related to IDE support for such language. If you watch closely, Groovy going to have better support in Netbean:
</p>

<p>
<a href="https://blogs.oracle.com/netbeansgroovy/entry/groovy_refactoring_in_netbeans" class="urlextern" title="https://blogs.oracle.com/netbeansgroovy/entry/groovy_refactoring_in_netbeans" rel="nofollow">https://blogs.oracle.com/netbeansgroovy/entry/groovy_refactoring_in_netbeans</a>
</p>

</div>
<!-- EDIT9 SECTION "WHEN TO USE SCRIPTING:" [5634-7365] -->
<h3 class="sectionedit10" id="note">NOTE:</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> You <strong>CAN</strong> use GROOVY for Java as Lua for C++ (even much more better)</div>
</li>
<li class="level1"><div class="li"> You <strong>CAN</strong> get GROOVY run as FAST as Java</div>
</li>
<li class="level1"><div class="li"> You <strong>CAN</strong> let GROOVY seamlessy intergrated with Java and other JVM languages.</div>
</li>
<li class="level1"><div class="li"> Last but not least, Groovy <strong>kick</strong> asses! :p </div>
</li>
</ul>

</div>
<!-- EDIT10 SECTION "NOTE:" [7366-7639] -->
<h2 class="sectionedit11" id="learn_groovy">LEARN GROOVY</h2>
<div class="level2">

<p>
</p><p></p><div class="notetip">If you already know about Groovy and just curious about how to intergrate Groovy into JME3. Go straight to Part <span class="curid"><a href="/jme3/scripting.html" class="wikilink1" title="jme3:scripting">into_the_game</a></span>
</div>
First, Groovy is much more shorter – cleaner than Java. It seamlessly get Java to the world of functional programming, like Python, Haskell, etc, but still make Java developer feel at home. You can read much more in the Groovy site and the internet, so I will not blow it up. 


<p>
Anyway, let’s learn some Groovy syntax, I bet you can master it in 3 hours!
</p>

<p>
GOTO <a href="/jme3/scripting/groovy_learn.html" class="wikilink1" title="jme3:scripting:groovy_learn">groovy_learn</a>
</p>

</div>
<!-- EDIT11 SECTION "LEARN GROOVY" [7640-8221] -->
<h3 class="sectionedit12" id="groovy_for_smarty">Groovy – for smarty</h3>
<div class="level3">

<p>
<img src="/lib/images/smileys/icon_question.gif" class="icon" alt=":?:" /><strong>So, what you can do with Groovy?</strong>
<img src="/lib/images/smileys/icon_lol.gif" class="icon" alt="LOL" /> everything, even get laid! <img src="/lib/images/smileys/icon_surprised.gif" class="icon" alt=":-o" />
</p>

<p>
I means use your imagination. I give you some examples:
</p>
<ul>
<li class="level1"><div class="li"> Fasten the build process</div>
</li>
<li class="level1"><div class="li"> Replace almost the configuration</div>
</li>
<li class="level1"><div class="li"> Extract infos from XML and text, web…</div>
</li>
<li class="level1"><div class="li"> Convert RenderMonkey, FXComposer shaders</div>
</li>
<li class="level1"><div class="li"> Script the Dialoge, Cinematic,…</div>
</li>
<li class="level1"><div class="li"> Make In-game Editor, JMP’s plugins</div>
</li>
<li class="level1"><div class="li"> Make a whole freaking game</div>
</li>
<li class="level1"><div class="li"> Even feed my dogs …</div>
</li>
</ul>

<p>
[10 more]
</p>

<p>
What I want to say is <strong>Groovy</strong> is for smarty, master it and it save you <em class="u">freaking big times</em> ! Java and Groovy are a sweetest combination of programing languages I ever tried beside of dozen of others. 
</p>

<p>
</p><p></p><div class="noteimportant">Some of the example above will be include in this post or in my AtomScript project!
</div>


</div>
<!-- EDIT12 SECTION "Groovy – for smarty" [8222-9001] -->
<h3 class="sectionedit13" id="official_examples_misc">Official examples &amp; Misc</h3>
<div class="level3">

<p>
Here are some website that you can find a lot of examples from simple to complicated tasks:
</p>

<p>
<a href="http://groovy.codehaus.org/Cookbook+Examples" class="urlextern" title="http://groovy.codehaus.org/Cookbook+Examples" rel="nofollow">http://groovy.codehaus.org/Cookbook+Examples</a>
</p>

<p>
<a href="http://www.groovyexamples.org/" class="urlextern" title="http://www.groovyexamples.org/" rel="nofollow">http://www.groovyexamples.org/</a>
</p>

<p>
<a href="http://snipplr.com/all/language/groovy" class="urlextern" title="http://snipplr.com/all/language/groovy" rel="nofollow">http://snipplr.com/all/language/groovy</a>
</p>

<p>
<a href="http://rosettacode.org/wiki/Rosetta_Code" class="urlextern" title="http://rosettacode.org/wiki/Rosetta_Code" rel="nofollow">http://rosettacode.org/wiki/Rosetta_Code</a> ⇐ learn Groovy and java if you come from other programming languages.
</p>

</div>
<!-- EDIT13 SECTION "Official examples & Misc" [9002-9359] -->
<h3 class="sectionedit14" id="gpars">GPars</h3>
<div class="level3">

<p>
If you already know Groovy, I recommend you to try <strong>GPars! Groovy Parallel Systems</strong>.
Why? Because <strong>it’s #$kin awesome</strong>, that’s why?
Every smart monkey and Java developer should know about it, to build apps and games!
</p>

<p>
<em>The GPars framework offers Java developers intuitive and safe ways to handle Java or Groovy tasks concurrently. Leveraging the enormous flexibility of the Groovy programing language and building on proven Java technologies, we aim to make concurrent programming for multi-core hardware intuitive, robust and enjoyable.</em>
</p>

<p>
<a href="http://gpars.codehaus.org/" class="urlextern" title="http://gpars.codehaus.org/" rel="nofollow">http://gpars.codehaus.org/</a>
</p>

<p>
</p><p></p><div class="notetip">I will explain some concepts and usages of GPars that help me a lot in JME3′s game and other tasks!
</div>


<p>
GOTO <a href="/doku.php/jme3:scripting:gpars_usecases" class="wikilink2" title="jme3:scripting:gpars_usecases" rel="nofollow">gpars_usecases</a>
</p>

</div>
<!-- EDIT14 SECTION "GPars" [9360-10112] -->
<h2 class="sectionedit15" id="embed_groovy">EMBED GROOVY</h2>
<div class="level2">

<p>
</p><p></p><div class="notetip">First I recommend all who don't know much about Groovy read this official documentation <a href="http://groovy.codehaus.org/Embedding+Groovy" class="urlextern" title="http://groovy.codehaus.org/Embedding+Groovy" rel="nofollow">http://groovy.codehaus.org/Embedding+Groovy</a> 
</div>


<p>
Groovy is very suitable for embeding in Java application, even game. Our intention here is to get Groovy to work with JME in few ways. Some common problems, difficulties may arised cause of the differencies, uncompatiable between Java-Groovy-Native OpenGL.
</p>

<p>
So technical problem and requirement will be dicussed first, then the Design of the integration is sketched, at last the full implementation. The full source code are in the AtomScript project!
</p>

</div>
<!-- EDIT15 SECTION "EMBED GROOVY" [10113-10739] -->
<h3 class="sectionedit16" id="overview">OVERVIEW</h3>
<div class="level3">

</div>

<h4 id="tech_probs">TECH PROBS</h4>
<div class="level4">

</div>

<h4 id="need_of_powerful_scripting_system">NEED OF POWERFUL SCRIPTING SYSTEM</h4>
<div class="level4">

<p>
<iframe title="" src="https://docs.google.com/presentation/d/1Kc1ehI1qLbtEGe-6-q8NikY7Q77A6jvozDaX94BqX0g/embed?start=false&amp;loop=false&amp;delayms=3000" style="width:100%; height:850px"></iframe>
</p>

</div>

<h4 id="design_architecture">DESIGN &amp; ARCHITECTURE</h4>
<div class="level4">

<p>
Slide
</p>

</div>

<h4 id="implementation">IMPLEMENTATION</h4>
<div class="level4">

<p>
Slide
</p>

</div>
<!-- EDIT16 SECTION "OVERVIEW" [10740-11034] -->
<h3 class="sectionedit17" id="groovy_in_jme3">Groovy in JME3</h3>
<div class="level3">

<p>
ScriptEngine
</p>

<p>
ScriptBase
</p>

<p>
Tools
</p>

</div>
<!-- EDIT17 SECTION "Groovy in JME3" [11035-11090] -->
<h3 class="sectionedit18" id="groovy_in_jmp">Groovy in JMP</h3>
<div class="level3">

</div>

<h4 id="scriptbasetopcomponent">ScriptBaseTopComponent</h4>
<div class="level4">

</div>

<h4 id="scriptenginemodule">ScriptEngineModule</h4>
<div class="level4">

</div>

<h4 id="advanced_tricks_to_get_jmp_scripted">Advanced Tricks to get JMP Scripted</h4>
<div class="level4">

</div>
<!-- EDIT18 SECTION "Groovy in JMP" [11091-11211] -->
<h3 class="sectionedit19" id="groovy_everywhere_snipets">Groovy everywhere (snipets)</h3>
<div class="level3">

</div>

<h4 id="extract_infos_from_xml_and_text_web">Extract infos from XML and text, web…</h4>
<div class="level4">

</div>

<h4 id="convert_rendermonkey_fxcomposer_shaders">Convert RenderMonkey, FXComposer shaders</h4>
<div class="level4">

<p>
GOTO <a href="/jme3/scripting/snippets.html" class="wikilink1" title="jme3:scripting:snippets">snippets</a>
</p>

</div>
<!-- EDIT19 SECTION "Groovy everywhere (snipets)" [11212-11376] -->
<h2 class="sectionedit20" id="into_the_game">INTO THE GAME</h2>
<div class="level2">

<p>
</p><p></p><div class="noteimportant">Grab the example code from the AtomScript project link
</div>


</div>
<!-- EDIT20 SECTION "INTO THE GAME" [11377-11479] -->
<h3 class="sectionedit21" id="basic_scripts">Basic Scripts</h3>
<div class="level3">

</div>

<h4 id="rotate_the_wheel">Rotate the wheel</h4>
<div class="level4">

</div>

<h4 id="travel_a_tree">Travel a tree</h4>
<div class="level4">

</div>

<h4 id="queue_a_task">Queue a task</h4>
<div class="level4">

</div>

<h4 id="groovyappstate">GroovyAppState</h4>
<div class="level4">

</div>

<h4 id="closurecondition">ClosureCondition</h4>
<div class="level4">

<p>
GOTO <a href="/jme3/scripting/groovy_basicscripts.html" class="wikilink1" title="jme3:scripting:groovy_basicscripts">groovy_basicscripts</a>
</p>

</div>
<!-- EDIT21 SECTION "Basic Scripts" [11480-11659] -->
<h3 class="sectionedit22" id="event_trigger_-_manager">Event – Trigger - Manager</h3>
<div class="level3">

<p>
The first idea come to my mind when think of game programming is a game cycle-update or events. 
</p>

<p>
In fact, frequently update and sudden event is quite opposite paradigm, the point is to get the best of both world in one design. But can we? At least I can answer partly yes. And such sollution I've seen in big database system use the same hyrid concept.
</p>

<p>
I also saw in the forum, guys had conversation about Entity System, which partly envolve such design… But this one it's different. It's not general, I means that the code below tent to be used in kind of RTS game like War-craft of Starcraft, and I precisely model it like those two games. And the codes are very short, extremely short, show the power of Groovy in the usecase.
</p>

<p>
GOTO <a href="/jme3/scripting/groovy_event.html" class="wikilink1" title="jme3:scripting:groovy_event">groovy_event</a>
</p>

</div>
<!-- EDIT22 SECTION "Event – Trigger - Manager" [11660-12468] -->
<h3 class="sectionedit23" id="configurations_with_groovy">Configurations with Groovy</h3>
<div class="level3">

<p>
Think about the way to config your game's screen resolution, keyboard, database connection, without have to write and parse java property or XML files. Groovy script is text file but much more powerful, like it has variables, methods (def), loop (for), conditions (if-else)…etc to build complicated things (like a program), compared to just plain text. 
In short Groovy can replace almost every configuration task you can imagine. This topic about using Groovy scrips for that purpose.
</p>

<p>
GOTO <a href="/doku.php/jme3:scripting:groovy_config" class="wikilink2" title="jme3:scripting:groovy_config" rel="nofollow">groovy_config</a>
</p>

</div>
<!-- EDIT23 SECTION "Configurations with Groovy" [12469-13032] -->
<h3 class="sectionedit24" id="ai_tricks_with_groovy">AI Tricks with Groovy</h3>
<div class="level3">

<p>
As in the introduction above I said this wiki will include everything about Scripting… So, it should also include AI (Artifacial Intelligent) … But I'm not going to tell you all about AI in this wiki, it should be more in another wiki of some AI professiors. I just want to show how a quick implementation of simple AI models can be coded in Groovy: 
</p>

<p>
GOTO <a href="/jme3/scripting/groovy/ai.html" class="wikilink1" title="jme3:scripting:groovy:ai">ai</a>
</p>

</div>

<h4 id="finite_state_machine">Finite State Machine</h4>
<div class="level4">

<p>
What is the most simple but affective techique to make AI. It's FSM
</p>

</div>

<h4 id="decision_tree">Decision Tree</h4>
<div class="level4">

<p>
Builder 
</p>

</div>

<h4 id="pattern_matching">Pattern Matching</h4>
<div class="level4">

<p>
Regexp <img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" />
</p>

</div>

<h4 id="simple_chatbot">Simple Chatbot</h4>
<div class="level4">

<p>
Builder + Closure <img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" />
</p>

</div>

<h4 id="simple_goalbase_agent">Simple Goalbase Agent</h4>
<div class="level4">

<p>
<img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" />
</p>

</div>

<h4 id="simple_path_finding">Simple Path finding</h4>
<div class="level4">

<p>
Use Groovy extension 
<img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" />
</p>

</div>

<h4 id="simple_steering_behavior">Simple Steering behavior</h4>
<div class="level4">

<p>
<img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" />
</p>

</div>
<!-- EDIT24 SECTION "AI Tricks with Groovy" [13033-13802] -->
<h3 class="sectionedit25" id="build_script_with_groovy">Build Script with Groovy</h3>
<div class="level3">

<p>
Groovy can use Ant and Maven in a snapt. but wait… it also has its own build extension named Gradle.
</p>

<p>
<a href="http://www.gradle.org/" class="urlextern" title="http://www.gradle.org/" rel="nofollow">http://www.gradle.org/</a>
</p>

<p>
Check this out:
For JME3 Desktop:
<img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" />
</p>

<p>
For JME3 Android:
<a href="http://tools.android.com/tech-docs/new-build-system/user-guide" class="urlextern" title="http://tools.android.com/tech-docs/new-build-system/user-guide" rel="nofollow">http://tools.android.com/tech-docs/new-build-system/user-guide</a>
</p>

</div>
<!-- EDIT25 SECTION "Build Script with Groovy" [13803-14087] -->
<h2 class="sectionedit26" id="design_patterns_in_groovy_game_wip">DESIGN PATTERNS IN GROOVY GAME (WIP)</h2>
<div class="level2">

</div>
<!-- EDIT26 SECTION "DESIGN PATTERNS IN GROOVY GAME (WIP)" [14088-14135] -->
<h2 class="sectionedit27" id="advanced_tricks">ADVANCED TRICKS</h2>
<div class="level2">

</div>
<!-- EDIT27 SECTION "ADVANCED TRICKS" [14136-14162] -->
<h3 class="sectionedit28" id="hack_the_jvm_with_groovy">Hack the JVM with Groovy</h3>
<div class="level3">

</div>
<!-- EDIT28 SECTION "Hack the JVM with Groovy" [14163-14196] -->
<h3 class="sectionedit29" id="codegen">Codegen</h3>
<div class="level3">

<p>
This should be in another wiki but somehow is super fit for an example of advanced Groovy usage. The project CodeGen - Code generator is my first Groovy project. It's tented to be a general code generator for Java, Groovy, GLSL and can also be a fun playground for non-developer. It inspirated by the concept of:
</p>

<p>
Alice <a href="http://www.alice.org/index.php" class="urlextern" title="http://www.alice.org/index.php" rel="nofollow">http://www.alice.org/index.php</a>
</p>

<p>
GreenFoot <a href="http://www.greenfoot.org/door" class="urlextern" title="http://www.greenfoot.org/door" rel="nofollow">http://www.greenfoot.org/door</a>
</p>

<p>
and an old plugin of PGI - a JME forum's member : PgiLogic
<a href="http://hub.jmonkeyengine.org/forum/topic/dead-combinable-logic-framework/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/dead-combinable-logic-framework/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/dead-combinable-logic-framework/</a>
</p>

<p>
It's going to be in a suite for making Jme3 Games : Atom framework. Visit :
GOTO <a href="/jme3/advanced/atom_framework.html" class="wikilink1" title="jme3:advanced:atom_framework">atom_framework</a>
GOTO <a href="/jme3/advanced/atom_framework/codegen.html" class="wikilink1" title="jme3:advanced:atom_framework:codegen">codegen</a>
</p>

</div>
<!-- EDIT29 SECTION "Codegen" [14197-14901] -->
<h3 class="sectionedit30" id="groovy_almighty_god">Groovy – Almighty God!</h3>
<div class="level3">

</div>

<h4 id="get_to_the_speed_of_java">Get to the speed of Java</h4>
<div class="level4">

</div>

<h4 id="extension_and_modulize">Extension and Modulize</h4>
<div class="level4">

</div>

<h4 id="database_and_orm">Database and ORM</h4>
<div class="level4">

</div>

<h4 id="dsl">DSL</h4>
<div class="level4">

</div>

<h4 id="visit_the_moon">Visit the Moon</h4>
<div class="level4">

</div>
<!-- EDIT30 SECTION "Groovy – Almighty God!" [14902-15065] -->
<h2 class="sectionedit31" id="conclusion">CONCLUSION</h2>
<div class="level2">

<p>
After reading for a while, I guess you are in love with Groovy already. You're welcome! <img src="/lib/images/smileys/icon_cool.gif" class="icon" alt="8-)" />
</p><p></p><div class="notewarning">
This page <strong>CAN NOT</strong> be a full description of Groovy… but a snapshot of its good with a few home grown codes for your JME3 game! 
</div>


<p>
Beside of knowing the power and the weaknesses of the language and the way to use it in your everyday life. If you want to have the full snippets, download AtomScript project.
</p>

<p>
Any correction are welcome!
</p>

</div>
<!-- EDIT31 SECTION "CONCLUSION" [15066-] -->
