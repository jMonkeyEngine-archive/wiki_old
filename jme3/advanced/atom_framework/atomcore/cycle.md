---
title: Well defined Cycles
---
<h2 class="sectionedit1" id="well_defined_cycles">Well defined Cycles</h2>
<div class="level2">

<p>
Cycle are ordered activities which repeat over and over during the entire application life time. It's usually referred as game loop. 
</p>

<p>
If you see a cycle as a list (ordered collection) of actions that the application does one at a time. You will see the application Iterate over them. In the opposite view (or in the action body), a traveller (usually data) seen it drag from one to the next one, so call pull to next step.
</p>

<p>
As Atom also support reactive programming, it's essential that developer should understand clearly what is the benefit of program with this direction or other. To get (Between) BEST OF BOTH WORLD! 
</p>

</div>
<!-- EDIT1 SECTION "Well defined Cycles" [1-655] -->
<h3 class="sectionedit2" id="why_6">Why 6?</h3>
<div class="level3">

<p>
Game programmer usually stick with 3 steps execution
</p>
<ol>
<li class="level1"><div class="li"> init </div>
</li>
<li class="level1"><div class="li"> update</div>
</li>
<li class="level1"><div class="li"> destroy</div>
</li>
</ol>

<p>
Instead of that, Atom use 6 steps execution cycle:
</p>
<ol>
<li class="level1"><div class="li"> init</div>
</li>
<li class="level1"><div class="li"> start</div>
</li>
<li class="level1"><div class="li"> load</div>
</li>
<li class="level1"><div class="li"> config</div>
</li>
<li class="level1"><div class="li"> update</div>
</li>
<li class="level1"><div class="li"> finish</div>
</li>
</ol>

<p>
These 6, I carefully learnt from other “good” module and component framework I 've use: Wicket, OSGi,Spring…they have different steps number! 
</p>

<p>
<a href="http://wicketguide.comsysto.com/guide/chapter6.html#chapter6_1" class="urlextern" title="http://wicketguide.comsysto.com/guide/chapter6.html#chapter6_1" rel="nofollow">http://wicketguide.comsysto.com/guide/chapter6.html#chapter6_1</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/OSGi#Life-cycle" class="urlextern" title="http://en.wikipedia.org/wiki/OSGi#Life-cycle" rel="nofollow">http://en.wikipedia.org/wiki/OSGi#Life-cycle</a>
</p>

<p>
<a href="http://www.tutorialspoint.com/spring/spring_bean_life_cycle.htm" class="urlextern" title="http://www.tutorialspoint.com/spring/spring_bean_life_cycle.htm" rel="nofollow">http://www.tutorialspoint.com/spring/spring_bean_life_cycle.htm</a>
</p>

<p>
The reason of these 6 step routine compare to 2,3,4,5.. or any other division is to support lazy loading, heavy task, gabage collection wise, much more…
</p>

<p>
So we usually have these 3 main methods:
</p>
<pre class="code">init , start , end</pre>

<p>
For a real-time game, we need 2 more:
</p>
<pre class="code">load, update
 </pre>

<p>
“Config” method is kind of a replicate of “init” or “load”, or confusion of these two, even can be done in “update” somehow but in fact, it's worth to be separated. The config step will help you gain a lot in the way to extend the frameworks or to adapt/scale  your game to smaller or bigger usecase, anyway 6 “is not too much but enough” !
</p>

<p>
Anyway this is a common cycle and compromise between ICycle who join the Atom conversations; that's hook in methods (classic style isn't it?). Beside of that, you can define your own routines through safe tasks and channels which provided by AtomMain. Though this tunnels, all your operations are guarantee to be not conflict in concurrent term with any other jobs of Managers, actors or helpers. So the Data is for you until you end the tasks (or be shut by forced because timeout for ex)!!
</p>

</div>
<!-- EDIT2 SECTION "Why 6?" [656-2304] -->
<h3 class="sectionedit3" id="pull_or_push">Pull or push?</h3>
<div class="level3">

<p>
As said in the analysis about JME3's patterns, especially rendering and update loop, it's pull and push at the same time. Confused? Yes it's… Why is so confused?
</p>

<p>
Java developers are “toooo” familiar with MVC architecture that bring to us by Swing and all classic sun solutions. That's why we find them in every programming books and every beginner's articles, especially if you develops game in desktop, (obviously in swing also). OpenGL and LWJGL also start as window based solution. So that we get “used to it”… Latter, a lot of web frameworks also make tanged mess of push &amp; pull concepts?
</p>

<p>
Swing-MVC concepts are embeded in a event-driven enviroment… and it's actually pull.
</p>

<p>
Real-time application can be event-driven or not. As my exprience, apply this Swing-MVC to real-time application not usually help greatly but sounds very confused and blury. It can help if you too familiar with it anyway, but be careful or you break the MVC contracts easily and make it not useful. You can blindy apply it without concerning of consequence, but that don’t make any sense.
</p>

<p>
The solid and only reason to say JME3 is pull and push, and why we still has to stop once for a while because of OpenGL via LWJGL is still monotholic! Not the GPU processing or GPU-CPU data exchange. So we still have to stop at the renderer's door, knock and wait until its done, then go to next step? Umh not quite. 
</p>

<p>
But to do this, we have to not depend in the update() and render() methods to get to total freedom. 
</p>

</div>

<h4 id="concurrent_parallel_world">Concurrent / Parallel world</h4>
<div class="level4">

<p>
Welcome to the parallel world which some time the well-defined cycle not even exist.
</p>

<p>
But the routine or the flow does exist indeed!
</p>

<p>
Just look at how your “data” or “signal” actually run through your systems, though “node” and “stages” as a network of roads &amp; cars. This actually a well-study area known as data flow analysis. In a perspective, data seem to be “pushed” from sources to targets. Some may also view its as data are “requested” by some nodes and “pulled” by those nodes.
</p>

<p>
<a href="https://github.com/Netflix/RxJava/wiki" class="urlextern" title="https://github.com/Netflix/RxJava/wiki" rel="nofollow">https://github.com/Netflix/RxJava/wiki</a>
</p>

</div>

<h4 id="what_is_the_new_routines_options">What is the new routines options?</h4>
<div class="level4">

<p>
Even if “Cycle”- which we used to known is just a conceptual view of points, my solution for this problem is to declare several new kinds of well-defined “Cycle” :
</p>
<ol>
<li class="level1"><div class="li"> Push cycle </div>
</li>
<li class="level1"><div class="li"> Pull cycle </div>
</li>
<li class="level1"><div class="li"> Non-cycle</div>
</li>
</ol>

<p>
… because defining routines in Atom is not only free but also helps in a lot of situations like when you interact with GUIs, networks or webs.
</p>

</div>

<h5 id="pull_cycle">Pull cycle</h5>
<div class="level5">

<p>
To connect to Swing MVC (also a pull cycle) with events, you can wrap them in Actors and let events send as messages between actors. The Swing actor in the EDT act as the brigde here. 
</p>

</div>

<h5 id="push_cycle">Push cycle</h5>
<div class="level5">

<p>
As in functional reactive programming and flow based programming, functions (small piece of jobs) are flow with their data. A flow is not a well defined cycle but a routine and can be monitored.
</p>

</div>

<h5 id="non-cycle">Non-cycle</h5>
<div class="level5">

<p>
A serial of Tasks can also form atribinary routines ( non-cycle) and be coordinated together via Data they exchange. 
</p>

<p>
</p><p></p><div class="notetip">Goto AtomPar for more concurrent/ paralell concepts and advices
</div>


</div>
<!-- EDIT3 SECTION "Pull or push?" [2305-5419] -->
<h2 class="sectionedit4" id="customable_cycles">Customable cycles</h2>
<div class="level2">

</div>

<h4 id="customable_routines">Customable routines</h4>
<div class="level4">

<p>
Via tasks and workers, you can atribinary make your own cycle that do anything around and later participate in the rendering stage and JME logic stage (if they want).
</p>

<p>
This freedom of doing things (in parallel if you want) is thanks to lock-free concurrent algorimths and data structure that Atom use. In other hand, the synchonizing problem is under research!
</p>

<p>
Read: <a href="/doku.php/jme3:advanced:atom_framework:atomcore:concurrent" class="wikilink2" title="jme3:advanced:atom_framework:atomcore:concurrent" rel="nofollow"> AtomPar</a>
</p>

</div>

<h4 id="customable_rendering_bucket">Customable (rendering) bucket</h4>
<div class="level4">

<p>
Bucket is a way to layered your rendering queue into layers or separate them into different categories (aka buckets) to handle differently.
</p>

<p>
With a composable comperator, a sub-list from a list, or a sub-tree from a tree, even a sub-graph from a entire scene graph can be extracted, or the whole collection can be sorted arcordingly. Custom bucket in Atom framework is implemented in AtomLight package to extend JME3 rendering pipeline. 
</p>

<p>
Note that a custom bucket is not very efficient! Even though if you enable a setting, Atom will take care of its render order and the update will be “IO wise” with special indexing structure call B-Tree. If you use it without cautions it can require a lot of memory and make your rendering suffer. 
</p>

</div>
<!-- EDIT4 SECTION "Customable cycles" [5420-6684] -->
<h2 class="sectionedit5" id="cycle_scale">Cycle &amp; Scale</h2>
<div class="level2">

<p>
You can see there is a trend for networks call non blocking IO, which Node.js is the first most and remarkable success. In that world, there is actually not a wellform cycle or turn at all. Because if there is a Queue or a lock, a insist port holder or an strict order (like a cycle), it can not scale at all!!
</p>

<p>
In fact the atribinary networks and async data signals have a lot more problems than we can possible imagine. Not everything can be fast and precise…Some parts (services) may be slow by intend, some parts cause errors frequently. 
</p>

<p>
The fault torrent architecture of AtomEx make sure some sercurity and transactional problems are shielded. AtomDust in another hand focus in highly loose mobile devices and atribinay short range connections. Those carefully design systems for usecases actually make Atom suitable even without a real Cycle.
</p>

<p>
</p><p></p><div class="notetip">Read more about AtomEx for Cloud scale and AtomDust of Mobile scale.
</div>


</div>
<!-- EDIT5 SECTION "Cycle & Scale" [6685-7651] -->
<h2 class="sectionedit6" id="technical_reviews">Technical reviews</h2>
<div class="level2">

</div>

<h4 id="cycle_or_ring">Cycle (or ring)</h4>
<div class="level4">

</div>

<h4 id="cicular_or_ring_buffer">Cicular (or ring) buffer</h4>
<div class="level4">

<p>
Ring buffer is fast way to make concurrent real time data streaming…
</p>

<p>
<a href="http://mechanitis.blogspot.com/2011/06/dissecting-disruptor-whats-so-special.html" class="urlextern" title="http://mechanitis.blogspot.com/2011/06/dissecting-disruptor-whats-so-special.html" rel="nofollow">http://mechanitis.blogspot.com/2011/06/dissecting-disruptor-whats-so-special.html</a>
</p>

</div>

<h4 id="is_there_a_real_cycle_or_just_a_lot_of_streams">Is there a real cycle? or just a lot of streams</h4>
<div class="level4">

</div>
<!-- EDIT6 SECTION "Technical reviews" [7652-] -->
