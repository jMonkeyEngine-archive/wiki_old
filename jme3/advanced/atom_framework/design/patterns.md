---
title: [Focus in] Design patterns and paradigms
---
<h2 class="sectionedit1" id="focus_in_design_patterns_and_paradigms">[Focus in] Design patterns and paradigms</h2>
<div class="level2">

<p>
This page is about design patterns, programming paradigms in game developing and those supported in AtomCore.
</p><p></p><div class="notewarning">This is <strong>NOT</strong> 1st Computer science class!! Understanding programming paradigms and patterns are very important to who want to do game programming, espeacially in Atom framework; which require <strong>very good</strong> knowledge of paradigms and patterns!
</div>


</div>
<!-- EDIT1 SECTION "[Focus in] Design patterns and paradigms" [1-430] -->
<h3 class="sectionedit2" id="programming_paradigms">Programming paradigms</h3>
<div class="level3">

<p>
Programming generally and programming languages usually designed toward a paradigm, but some of them are multi-paradigm also.
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Programming_paradigm" class="urlextern" title="http://en.wikipedia.org/wiki/Programming_paradigm" rel="nofollow">http://en.wikipedia.org/wiki/Programming_paradigm</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Comparison_of_programming_paradigms" class="urlextern" title="http://en.wikipedia.org/wiki/Comparison_of_programming_paradigms" rel="nofollow">http://en.wikipedia.org/wiki/Comparison_of_programming_paradigms</a>
</p>

</div>

<h4 id="java_programming_language">Java programming language</h4>
<div class="level4">

<p>
<a href="/resources/fetch.php" class="media" title="http://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Java_logo_and_wordmark.svg/150px-Java_logo_and_wordmark.svg.png"><img src="/resources/fetch.php" class="medialeft" title="200" alt="200" /></a> <strong>Java</strong> is a computer programming language that is concurrent, class-based, object-oriented, (mostly) imperative, structured (also referred as strictly typed)
</p>

<p>
<img src="/lib/images/smileys/icon_cool.gif" class="icon" alt="8-)" /> Suppose that when you read this wiki you already know what Java is (partly)
</p>

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

<p>
</p><p></p><div class="notetip">Learn groovy: <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:scripting" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:scripting" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:scripting</a>
</div>


</div>
<!-- EDIT2 SECTION "Programming paradigms" [431-1459] -->
<h3 class="sectionedit3" id="game_programming_paradigms">Game Programming paradigms</h3>
<div class="level3">

<p>
Game framework or game engines also be comparasion (along with its programming language) into some category (not include graphics capacity):
</p>

</div>

<h4 id="by">By</h4>
<div class="level4">

<p>
Entity System
</p>

</div>

<h4 id="by_concurrent_capicity">By concurrent capicity</h4>
<div class="level4">

<p>
Active
</p>

<p>
Reactive
</p>

<p>
Interactive
</p>

</div>
<!-- EDIT3 SECTION "Game Programming paradigms" [1460-1725] -->
<h3 class="sectionedit4" id="design_patterns">Design patterns</h3>
<div class="level3">

<p>
<a href="http://en.wikipedia.org/wiki/Software_design_pattern" class="urlextern" title="http://en.wikipedia.org/wiki/Software_design_pattern" rel="nofollow">http://en.wikipedia.org/wiki/Software_design_pattern</a>
</p>

<p>
<a href="http://sourcemaking.com/" class="urlextern" title="http://sourcemaking.com/" rel="nofollow">http://sourcemaking.com/</a>
</p>

<p>
<a href="http://wiki.apidesign.org/wiki/Main_Page" class="urlextern" title="http://wiki.apidesign.org/wiki/Main_Page" rel="nofollow">http://wiki.apidesign.org/wiki/Main_Page</a>
</p>

</div>
<!-- EDIT4 SECTION "Design patterns" [1726-1873] -->
<h3 class="sectionedit5" id="design_patterns_in_game_developing">Design patterns in game developing</h3>
<div class="level3">

<p>
<a href="http://gameprogrammingpatterns.com/" class="urlextern" title="http://gameprogrammingpatterns.com/" rel="nofollow">http://gameprogrammingpatterns.com/</a>
</p>

</div>

<h4 id="singleton__central__law_of_detemer">Singleton . Central . Law of detemer</h4>
<div class="level4">

</div>

<h4 id="lightweight_decorator">Lightweight &amp; Decorator</h4>
<div class="level4">

</div>

<h4 id="inversion_of_control">Inversion of Control</h4>
<div class="level4">

</div>

<h4 id="factory">Factory</h4>
<div class="level4">

</div>

<h4 id="mvc_mvc">MVC &amp; MVC?</h4>
<div class="level4">

<p>
MPV: Model View Presenter is the two way of
MVC Model View Controller; where Presenter is the middle-man, the mediator between Model and View know and get notificated by both Model and View.
</p>

<p>
Talk about MVC first: Assume you know about web
</p>

<p>
from Wikipedia <a href="http://en.wikipedia.org/wiki/Web_application_framework#Push-based_vs._pull-based" class="urlextern" title="http://en.wikipedia.org/wiki/Web_application_framework#Push-based_vs._pull-based" rel="nofollow">http://en.wikipedia.org/wiki/Web_application_framework#Push-based_vs._pull-based</a>
</p>

<p>
<strong>Push-based vs. pull-based</strong>
</p>
<pre class="code">Most MVC frameworks follow a push-based architecture also called “action-based”. These frameworks use actions that do the required processing, and then “push” the data to the view layer to render the results.[5] Struts, Django, Ruby on Rails, Symfony, Yii, Spring MVC, Stripes, Play, CodeIgniter, and Struts2[6] are good examples of this architecture. An alternative to this is pull-based architecture, sometimes also called “component-based”. These frameworks start with the view layer, which can then “pull” results from multiple controllers as needed. In this architecture, multiple controllers can be involved with a single view. Lift, Tapestry, JBoss Seam, JavaServer Faces, and Wicket are examples of pull-based architectures.</pre>

<p>
MVC Push was born in the world of “none frequent” and not suite well for kind of application almost done update every-frame. So there is some kind of Event,Action embed on it.
</p>

<p>
MVC Pull in another hand, suite better for “frequent update” and assume that View is the one trigger the update call.
</p>

<p>
Back to real-time game, if you not making a chess game, almost you “are doing” a pull based MVC, or apply this pattern privately. 
</p>

</div>
<!-- EDIT5 SECTION "Design patterns in game developing" [1874-3653] -->
<h2 class="sectionedit6" id="design_patterns_in_jme3">Design patterns in JME3</h2>
<div class="level2">

<p>
Here some analysing about patterns in JME3 world so Atom bypass or inherit them.
</p>

</div>

<h4 id="push_or_pull">Push or pull ?</h4>
<div class="level4">

<p>
worth to note:
even some part of JME3 assemble MPV, it’s not the whole!
also for a game, apply MPV is quite annoying and also tricky!
</p>

<p>
</p><p></p><div class="notetip">Here is the twist: Actually in JME3, you are doing both, that’s why it look like MVP!
</div>


<p>
because of this cycle 
</p>

</div>
<!-- EDIT6 SECTION "Design patterns in JME3" [3654-4058] -->
<h2 class="sectionedit7" id="design_patterns_in_atom">Design patterns in Atom</h2>
<div class="level2">

</div>
<!-- EDIT7 SECTION "Design patterns in Atom" [4059-] -->
