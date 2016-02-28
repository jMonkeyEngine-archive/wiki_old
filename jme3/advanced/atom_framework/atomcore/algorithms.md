---
title: Algorimths for games
---
<h2 class="sectionedit1" id="algorimths_for_games">Algorimths for games</h2>
<div class="level2">

<p>
Single (or serveral) objective algorimths useful for games.
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Algorithm" class="urlextern" title="http://en.wikipedia.org/wiki/Algorithm" rel="nofollow">http://en.wikipedia.org/wiki/Algorithm</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Linear_programming" class="urlextern" title="http://en.wikipedia.org/wiki/Linear_programming" rel="nofollow">http://en.wikipedia.org/wiki/Linear_programming</a>
</p>

<p>
Algorithm is a step-by-step procedure for calculations. An algorithm is an effective method expressed as a finite list[1] of well-defined instructions[2] for calculating a function.[3] Starting from an initial state and initial input (perhaps empty),[4] the instructions describe a computation that, when executed, proceeds through a finite[5] number of well-defined successive states, eventually producing “output”[6] and terminating at a final ending state. The transition from one state to the next is not necessarily deterministic; some algorithms, known as randomized algorithms, incorporate random input.[7]
</p>

<p>
Linear programming (LP, or linear optimization) is a method to achieve the best outcome (such as maximum profit or lowest cost) in a mathematical model whose requirements are represented by linear relationships. More formally, linear programming is a technique for the optimization of a linear objective function, subject to linear equality and linear inequality constraints. Its feasible region is a convex polyhedron, which is a set defined as the intersection of finitely many half spaces, each of which is defined by a linear inequality. Its objective function is a real-valued affine function defined on this polyhedron. A linear programming algorithm finds a point in the polyhedron where this function has the smallest (or largest) value if such a point exists.
</p>

</div>
<!-- EDIT1 SECTION "Algorimths for games" [1-1567] -->
<h3 class="sectionedit2" id="why_use_this__for_games">Why use this ... for games?</h3>
<div class="level3">

<p>
This package provides algorithms common in game developments. More to come but first let's take a look of those problems it trying to solve to distingish the objective and goals of this package compare to collection and others.
</p>

</div>

<h4 id="it_s_not_another_collection_datastructure_or_pattern_package">It's not another Collection (DataStructure) or Pattern package!</h4>
<div class="level4">

<p>
Sort, concurrent, packing, data compressing is also partial relate to its processing method (that's algorithm) but first, they are provided as the core of the programming language, second we want to care more about the high level of abstraction, not the details. It use “interface” of structure for its explaination and progress.
</p>

<p>
Also, pattern is the term refered to a popular method in software developmenet. Pattern is also in higher level of abstraction compare to algorimths. So consider pattern is the law and algorimth is the effective way of making the job work effectively obey that law.
</p>

<p>
Algorithms involve logic, a lot of them. But it higher level than logic. And of course algorithms need math (some physics, philosophy also) to be smart!
</p>

<p>
Algorithms are used heavily in AI. But this package only provide pure algorithms which can be used also outside of AI topics.
</p>

<p>
That's said:
</p>
<ul>
<li class="level1"><div class="li"> Datastructure, Pattern, Logic and AI are supported elsewhere!</div>
</li>
<li class="level2"><div class="li"> Algorimths depends in Pattern, Logic, Interface of Structure.</div>
</li>
</ul>

</div>

<h4 id="each_algorithm_has_a_goal_or_several_to_accomplish">Each algorithm has a goal (or several) to accomplish!</h4>
<div class="level4">

<p>
Developer want to use the algorithm they know to solve one or more goals (problem, requirement, aspect, situation, … what ever you call it). The algorithms provided here are the bricks for you to use and reuse, for different purposes. And you may notice the package also be arranged into purposes instead of implementations - techniques or another structure. That's explained the reason!
</p>

</div>

<h4 id="for_games">For games?</h4>
<div class="level4">

<p>
Yes, not all of the problems we know are solved by this library…??? You've already know. It not even sotiphicated like the alternatives below but they are extremely useful for average programmers; especially game programmer, who, usually focus in the fun side (Am I right? :) )
</p>

<p>
The library try to provide useful algorithms (best practices and wisdoms) enough for a wide range of usecases and also used in Atom framework its self. The algorimths them self may use another algorimths to solve sub-problems. Of course, it also come with examples and a lot of applications &amp; suggestion, which its the algorithms use for you to quickly and smartly solve your own problem thank to it.
Support algorithms by purposes
</p>
<pre class="code"> 1. Allocation: solve problems about resources.
       1. Allocate resources efficiently on demand and sastify requirements:
             1. in an amount of time (interval, arrangement, progess, budget)
             2. with specific capacities of the network and memory (flow, route, budget)
             3. with dependencies (order)
             4. skip or retry if unsuccess (fault-tolerant)
             5. cache
       2. Skip resources that fault-tolerant: ( aka Reject)
             1. Not affect its dependencies, or skip those dependant
             2. Preseved the continuous, so the flow still smooth
       3. Release resources ( aka Remove)
             1. Determiate which resource are no more needed
             2. Help the gabbage collector, cache to remove it
       4. Update resources
             1. Only what that need to be update
             2. Deffered till the update process not abuse the other pioritied operations
 2. Balance: find a division, equallity equilibrium between inputs of forces (presure).
       1. Exchange: when force interact
       2. Equilibrium: when force include, conccure together and zero total
 3. Energy : more than just physics simulation, its applied physics-math based methods
       1. Static:
       2. Dynamic:
       3. Potential: 
       4. Tension:
 4. Constraint: find a solution that sastify a list of constraints.
       1. Search for sollution in avaiable space (travel)
       2. Generate a sollution base in template
 5. Interval: various problems related to intervals (values a duration of time).
       1. Progress monitoring
       2. Schedule jobs
 6. Optimization: to optimize toward a goal
       1. Maximize - minimize:
       2. Resolution: Find a solution upon a known solution (aka neirghboor search)
       3. Boost: wisdoms  to make higher performance and more efficient algorithms if not saturated (without resolution)
             1. Reactive
             2. Adaptive
             3. Fractal
 7. Relate: solve problems between things relate to other (Very close to abstract aglebra):
       1. Reconfiguration: if one change, others react
       2. Coupling: link-relink-relax link-remove link between two or a group by cateria (aka clustering)
       3. Dependency: direct/ indirect depend on other and how to isolate
       4. Order: study of ordering, very similar to sorting wisdoms but in higher level.
 8. Score: Study the "number","amount" (aka quantity) of things; summarize and judge (aka quality). Wisdoms about: Measuring, scale, approximation, coloring or the alike.
       1. Budget:
       2. Audit: (aka Accounting)
       3. Cardinality:
 9. Travel: Study the step by step "move" between unit of things. This is a fundamental and essential spirit of algorithms.
       1. Search: Study the exploring in space.
       2. Trace: Study the affection (footprint, operations, cost.. ) the algorithms left each step
       3. Track:  Study the  route  (path, track, flow,...)  the algorithms  pass.
10.  Generation: good practises in making new things
       1. Template is the resource of generation
       2. Production is the progress of creating new things</pre>

</div>
<!-- EDIT2 SECTION "Why use this ... for games?" [1568-7375] -->
<h2 class="sectionedit3" id="concepts">Concepts</h2>
<div class="level2">

<p>
First of all this package has some degree similar to JScience and Opt4J… I can't denied I had used them intensively to know what is good and what is not. About the similarity between Ptolemy and Atom, even the two take different approaches and implementation, you can read from the Atom framework introduction.
</p>

<p>
Algorimths in computing, programming and game programming has grown, based in knowledges and wisdoms from a lot of other sciences: math, physics, philosophy, chemistry, biology… etc. Here and there the concepts are familiar with developer because they've taught in schools. Some may require extra knowledge from mathematics and physics per se… But you know google can have any way.
</p>

<p>
Here is the part where the concepts which used in algorithms in Atom framework which you can reference and research futher. Almost every part you can also google about them or try to find it in jscience <abbr title="Application Programming Interface">API</abbr> javadoc:
</p>

<p>
<a href="http://jscience.org/api/index.html" class="urlextern" title="http://jscience.org/api/index.html" rel="nofollow">http://jscience.org/api/index.html</a>
</p>

<p>
<a href="http://jscience.org/experimental/javadoc/" class="urlextern" title="http://jscience.org/experimental/javadoc/" rel="nofollow">http://jscience.org/experimental/javadoc/</a>
</p>

</div>
<!-- EDIT3 SECTION "Concepts" [7376-8392] -->
<h3 class="sectionedit4" id="from_mathematics">From Mathematics</h3>
<div class="level3">

</div>

<h4 id="algebra">Algebra</h4>
<div class="level4">

</div>

<h4 id="topo_graph">Topo &amp; Graph</h4>
<div class="level4">

</div>
<!-- EDIT4 SECTION "From Mathematics" [8393-8454] -->
<h3 class="sectionedit5" id="from_physics">From Physics</h3>
<div class="level3">

</div>

<h4 id="common">Common</h4>
<div class="level4">

</div>

<h4 id="kinematic">Kinematic</h4>
<div class="level4">

</div>
<!-- EDIT5 SECTION "From Physics" [8455-8508] -->
<h3 class="sectionedit6" id="from_computing_techs">From computing techs</h3>
<div class="level3">

</div>
<!-- EDIT6 SECTION "From computing techs" [8509-8539] -->
<h3 class="sectionedit7" id="saturation_of_algorithms">Saturation of algorithms:</h3>
<div class="level3">

<p>
You may notice that if there is a “pattern” or “algorimth” to optimize a progress. Can we use them repeatly until processing time toward minimum or even zero????
</p>

<p>
This sounds totally untrue and also ridiculous but an interesting captious way of thinking. 
</p>

<p>
<a href="http://algs4.cs.princeton.edu/66intractability/" class="urlextern" title="http://algs4.cs.princeton.edu/66intractability/" rel="nofollow">http://algs4.cs.princeton.edu/66intractability/</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Time_hierarchy_theorem" class="urlextern" title="http://en.wikipedia.org/wiki/Time_hierarchy_theorem" rel="nofollow">http://en.wikipedia.org/wiki/Time_hierarchy_theorem</a>
</p>

<p>
<a href="http://www.npr.org/blogs/13.7/2011/09/19/140599268/minds-and-machines-the-limits-of-turing-complete-machines" class="urlextern" title="http://www.npr.org/blogs/13.7/2011/09/19/140599268/minds-and-machines-the-limits-of-turing-complete-machines" rel="nofollow">http://www.npr.org/blogs/13.7/2011/09/19/140599268/minds-and-machines-the-limits-of-turing-complete-machines</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Turing_machine#Computational_complexity_theory" class="urlextern" title="http://en.wikipedia.org/wiki/Turing_machine#Computational_complexity_theory" rel="nofollow">http://en.wikipedia.org/wiki/Turing_machine#Computational_complexity_theory</a>
</p>

<p>
Here i used the term the <strong>saturation of algorithms</strong> to describle the problem from overview.
</p>

<p>
Let say the algorithm A needs B to compute, and than B needs A to compute. The Recursion will be forever in the turing machine such as our computer, until we out of memory or can even cause a crash in some programming language and computer-small scale ones (pc,console…). In real-life, it's hardly useful for game developing. 
</p>

<p>
For example: 
</p>

<p>
In Allocation package, we need to compute the dependencies between resources, si call Dependency package. In computing dependency, we need resource so we call allocation package… This loop is actually fine but its will run forever if there is no saturation point or the end point of the recursion calls. 
</p>

<p>
So in AtomAA, there is a detection of Recursion and cyclic dependency that can break-out early from the infinite loops. Also if Dependency package call, it tell Allocation not to call it again in the amount of time. Allocation then will chose another path of computing by just allocate directly. This not gaurantee to prevent the problem but ease out the percentage you fall into a dead trap. It work pretty much like concurrent contention resolving in by synchronization in Java. 
</p>

<p>
This mean the context of computing is affect the algorithms, lead the algorithm to context-depend. So is it conflict with the definition of algorithm and wrong? Well, in real-life, some algorithms actually work upon a data structure and context, if not to say all of them. The abstraction and agnostic of algorithm is limit but higher than data structure, it just depend in the “context of computing” but work in various data structure, even a new one. It's also better than normal datastructure in this “loop” situation. You may experience the situation that datastructure implementation may cause infinite loop with them self or others. At least algorithms try to prevent that…
</p>

<p>
</p><p></p><div class="notewarning"><strong>Note:</strong> Actually when the situation happen, there is a way to stop the whole!… but not a clean way to set a flag, clear the flag and continue again, because the next time, the progress can not distingish between the normal processing and the invalid one. At least not a simple way without Tranactional Memeory Model.
</div>


<p>
In development mode, with AtomAA , the programmer will be notified and the progress will stop. A monitoring framework can also help. The determistic of the algorithms over arbitrary data (in real-life) is also quite a challange problem. That's also a caveat in AtomAA its self.
</p>

</div>
<!-- EDIT7 SECTION "Saturation of algorithms:" [8540-11657] -->
<h2 class="sectionedit8" id="implementation_details">Implementation details</h2>
<div class="level2">

<p>
</p><p></p><div class="notetip">The <strong>[JavaAA]</strong> (Java Atom Algorithms) tags mark what this package support.
</div>


</div>
<!-- EDIT8 SECTION "Implementation details" [11658-11784] -->
<h3 class="sectionedit9" id="allocation">Allocation</h3>
<div class="level3">

<p>
solve problems about resources.
</p>
<pre class="code">Allocate resources efficiently on demand and sastify requirements:
  in an amount of time (interval, arrangement, progess, budget)
  with specific capacities of the network and memory (flow, route, budget)
  with dependencies (order)
  skip or retry if unsuccess (fault-tolerant)
  cache
Skip resources that fault-tolerant: ( aka Reject)
  Not affect its dependencies, or skip those dependant
  Preseved the continuous, so the flow still smooth
Release resources ( aka Remove)
  Determiate which resource are no more needed
  Help the gabbage collector, cache to remove it
Update resources
  Only what that need to be update
  Deffered till the update process not abuse the other pioritied operations</pre>

</div>
<!-- EDIT9 SECTION "Allocation" [11785-12566] -->
<h3 class="sectionedit10" id="balance">Balance:</h3>
<div class="level3">
<pre class="code">find a division, distribution for equality, find equilibrium between inputs of forces (presure).
 Exchange: when force interact
 Equilibrium: when force include, concur together and zero total
 </pre>

<p>
higher wisdoms than equality and difference. Its the progress of making two or more things equal by exchanging one by one (local optimal or greedy). It's also a study of distribution to find equilibrium between inputs of forces. This problem araise a lot in classical game theory and later game developing. 
</p>

<p>
Read: 
<a href="http://en.wikipedia.org/wiki/Game_theory" class="urlextern" title="http://en.wikipedia.org/wiki/Game_theory" rel="nofollow">http://en.wikipedia.org/wiki/Game_theory</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Solution_concept" class="urlextern" title="http://en.wikipedia.org/wiki/Solution_concept" rel="nofollow">http://en.wikipedia.org/wiki/Solution_concept</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Nash_equilibrium" class="urlextern" title="http://en.wikipedia.org/wiki/Nash_equilibrium" rel="nofollow">http://en.wikipedia.org/wiki/Nash_equilibrium</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Ultimatum_game" class="urlextern" title="http://en.wikipedia.org/wiki/Ultimatum_game" rel="nofollow">http://en.wikipedia.org/wiki/Ultimatum_game</a>
</p>

</div>
<!-- EDIT10 SECTION "Balance:" [12567-13290] -->
<h3 class="sectionedit11" id="energy">Energy :</h3>
<div class="level3">
<pre class="code">more than just physics simulation, its applied physics-math based methods
  Static:
  Dynamic:
  Potential: 
  Tension:</pre>

</div>
<!-- EDIT11 SECTION "Energy :" [13291-13437] -->
<h3 class="sectionedit12" id="constraint">Constraint:</h3>
<div class="level3">

<p>
find a solution that sastify a list of constraints.
</p>
<pre class="code">Search for sollution in avaiable space (travel)
Generate a sollution base in template
  </pre>

</div>
<!-- EDIT12 SECTION "Constraint:" [13438-13606] -->
<h3 class="sectionedit13" id="interval">Interval:</h3>
<div class="level3">

<p>
various problems related to intervals (values a duration of time).
 Progress monitoring
 Schedule jobs
</p>

</div>
<!-- EDIT13 SECTION "Interval:" [13607-13729] -->
<h3 class="sectionedit14" id="optimization">Optimization:</h3>
<div class="level3">

<p>
to optimize toward a goal
</p>
<pre class="code"> Maximize - minimize:
 Resolution: Find a solution upon a known solution (aka neirghboor search)
 Boost: wisdoms  to make higher performance and more efficient algorithms if not saturated (without resolution)
   Reactive
   Adaptive
   Fractal
 Evolutionary: </pre>

</div>
<!-- EDIT14 SECTION "Optimization:" [13730-14051] -->
<h3 class="sectionedit15" id="relate">Relate:</h3>
<div class="level3">

<p>
 solve problems between things relate to other (Very close to abstract aglebra):
</p>
<pre class="code"> Reconfiguration: if one change, others react
 Coupling: link-relink-relax link-remove link between two or a group by cateria (aka clustering)
 Dependency: direct/ indirect depend on other and how to isolate
 Order: study of ordering, very similar to sorting wisdoms but in higher level.</pre>

<p>
The relationship between things cause complex problems, this package try to solve a subset of problems which is useful in programming and gamedev in general. Relation is very abstract, but some of  “relationship problems” are well-defined like:
</p>
<ul>
<li class="level1"><div class="li"> the cause of declaration of relationships </div>
</li>
<li class="level1"><div class="li"> the dependency between two subject</div>
</li>
<li class="level1"><div class="li"> the direction, order of relation or force</div>
</li>
<li class="level1"><div class="li"> the configuration need to the relationship</div>
</li>
</ul>

<p>
<strong>Dependency</strong>: If one object “declare” relationship to another, aka one-direction link:
<strong>Coupling</strong>: If two objects “declare” relationship between each other, aka bi-direction link:
</p>
<ul>
<li class="level1"><div class="li"> [Real-life] Imagine the marriage law when two get married :) </div>
</li>
<li class="level1"><div class="li"> [Computing] The dependency between packages, modules, operations, tasks.</div>
</li>
<li class="level1"><div class="li"> [JavaAA] </div>
<ul>
<li class="level2"><div class="li"> The links can be create or not? </div>
<ul>
<li class="level3"><div class="li"> to prevent NullPointException if you invoke an empty link.</div>
</li>
<li class="level3"><div class="li"> to prevent IllegalException because of tabboo</div>
</li>
<li class="level3"><div class="li"> full satifaction conditions?</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> What need for a link to be create? </div>
<ul>
<li class="level3"><div class="li"> load needed assets, classes, modules.. - like what osgi and maven does</div>
</li>
<li class="level3"><div class="li"> the first-attempt configuration in the two subjects.</div>
</li>
</ul>
</li>
</ul>
</li>
</ul>

<p>
<strong>Reconfiguration</strong>: If two objet “change” the relationship and the affections.
</p>
<ul>
<li class="level1"><div class="li"> [Real-life] Imagine a devote, and the fate of the property and children</div>
</li>
<li class="level1"><div class="li"> [Computing] Reconfiguration cause computation in the said domain and cause a chains of reaction in the network. The reconfiguration can cause “bigger” affection than the first time config, but how to decrease the cost?</div>
</li>
<li class="level1"><div class="li"> [JavaAA] </div>
<ul>
<li class="level2"><div class="li"> Is there anything i can save?</div>
<ul>
<li class="level3"><div class="li"> what is still valid and update just the delta?</div>
</li>
<li class="level3"><div class="li"> what is properly unchanged and really can not be changed?</div>
</li>
<li class="level3"><div class="li"> what will be abandond after reconfig?</div>
</li>
<li class="level3"><div class="li"> can the reconfig progress delay or divide-to-conquer?</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> This also envolve in general LOD (LevelOfDetail) problems, which mainly focus in reconfig after changes. Divide-to-conquer is the main wisdom of this class of problems.</div>
</li>
</ul>
</li>
</ul>

<p>
<strong>Order</strong>: directions, or the order of travelling when bunch of objects are related.
</p>
<ul>
<li class="level1"><div class="li"> [Real-life] I want to travel in a city by roads. I have to know the map.</div>
</li>
<li class="level1"><div class="li"> [Computing] Graph problems and how to change the direction of processing</div>
</li>
<li class="level1"><div class="li"> [JavaAA] </div>
<ul>
<li class="level2"><div class="li"> Sort in graphs &amp; Order of Nodes</div>
</li>
<li class="level2"><div class="li"> Direction of Track</div>
</li>
<li class="level2"><div class="li"> Order of Intervals (conccurent progresses)</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT15 SECTION "Relate:" [14052-16791] -->
<h3 class="sectionedit16" id="score">Score:</h3>
<div class="level3">

<p>
Study the “number”,“amount” (aka quantity) of things; summarize and judge (aka quality). Wisdoms about: Measuring, scale, approximation, coloring or the alike.
</p>
<pre class="code"> Budget:
 Audit: (aka Accounting)
 Cardinality:
 </pre>

<p>
This package support the invoke of functions and actions for measurement in single step or a chain of steps. Also it provide the remain of power within a Budget. After serveral of steps, it can invoke audit for examine the progress. For doing this, it has to know detail about Unit by understand Cardinality in the context. 
</p>

<p>
This package depend in Commons Math and JScience for useful functions.
</p>

</div>
<!-- EDIT16 SECTION "Score:" [16792-17421] -->
<h3 class="sectionedit17" id="travel">Travel:</h3>
<div class="level3">

<p>
Study the step by step “move” between unit of things. This is a fundamental and essential spirit of algorithms. <span class="curid"><a href="/jme3/advanced/atom_framework/atomcore/algorithms.html" class="wikilink1" title="jme3:advanced:atom_framework:atomcore:algorithms">Read back algorithm definition above</a></span>
</p>
<pre class="code"> Search: Study the exploring in space.
 Trace: Study the affection (footprint, operations, cost.. ) the algorithms left each step
 Track:  Study the  route  (path, track, flow,...)  the algorithms  pass.
 </pre>

<p>
Travel depend in relate. It Explores bunch of things that relate to each others in a space (Data space, time space). The process known as Search. Doing Search, it left Traces. Flowing trace in each step, one can see a Track or a Flow of the progress.
</p>

<p>
This package support: datastructure-agnostic search, traces and tracks (beside of those already supported in Java, Guava…)
</p>

<p>
Search:  
DFS, BFS, Traveler 
</p>

<p>
Trace: 
Visit, Footprint (mark), Cost
</p>

<p>
Track: 
ForwardTrack, BackwardTrack, Flow (TotalCostTrack-SingleStepCostTrack), FlowCapacity
</p>

</div>
<!-- EDIT17 SECTION "Travel:" [17422-18416] -->
<h3 class="sectionedit18" id="generation">Generation:</h3>
<div class="level3">

<p>
 good practises in making new things
</p>
<pre class="code"> Template is the resource of generation
 Production is the progress of creating new things</pre>

<p>
A collections of wisdoms explain what/why/how to generate new things smart and efficiently.
</p>
<ul>
<li class="level1"><div class="li"> [Math] A function from one domain to another domain. </div>
<ul>
<li class="level2"><div class="li"> <a href="http://en.wikipedia.org/wiki/Function_%28mathematics%29" class="urlextern" title="http://en.wikipedia.org/wiki/Function_%28mathematics%29" rel="nofollow">http://en.wikipedia.org/wiki/Function_%28mathematics%29</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> [Physics] Energy from one form to another. </div>
<ul>
<li class="level2"><div class="li"> <a href="http://en.wikipedia.org/wiki/Conservation_of_energy" class="urlextern" title="http://en.wikipedia.org/wiki/Conservation_of_energy" rel="nofollow">http://en.wikipedia.org/wiki/Conservation_of_energy</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> [Language] Translate sematic from one to another language need a dictionary. </div>
<ul>
<li class="level2"><div class="li"> <a href="http://en.wikipedia.org/wiki/Semantic_similarity" class="urlextern" title="http://en.wikipedia.org/wiki/Semantic_similarity" rel="nofollow">http://en.wikipedia.org/wiki/Semantic_similarity</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> [Art] Nothing new, just a cover. </div>
<ul>
<li class="level2"><div class="li"> <a href="http://www.brainyquote.com/quotes/quotes/p/pablopicas380469.html" class="urlextern" title="http://www.brainyquote.com/quotes/quotes/p/pablopicas380469.html" rel="nofollow">http://www.brainyquote.com/quotes/quotes/p/pablopicas380469.html</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://idioms.thefreedictionary.com/There+is+nothing+new+under+the+sun" class="urlextern" title="http://idioms.thefreedictionary.com/There+is+nothing+new+under+the+sun" rel="nofollow">http://idioms.thefreedictionary.com/There+is+nothing+new+under+the+sun</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://thephilthyway.files.wordpress.com/2012/09/boycottapple.png?w=549&amp;h=279" class="urlextern" title="http://thephilthyway.files.wordpress.com/2012/09/boycottapple.png?w=549&amp;h=279" rel="nofollow">http://thephilthyway.files.wordpress.com/2012/09/boycottapple.png?w=549&amp;h=279</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> [Computing] Template is a good abstraction of algorimths. </div>
<ul>
<li class="level2"><div class="li"> <a href="http://en.wikipedia.org/wiki/Generic_programming" class="urlextern" title="http://en.wikipedia.org/wiki/Generic_programming" rel="nofollow">http://en.wikipedia.org/wiki/Generic_programming</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> [Programming] DRY , data-driven and open source. </div>
<ul>
<li class="level2"><div class="li"> <a href="http://en.wikipedia.org/wiki/Don%27t_repeat_yourself" class="urlextern" title="http://en.wikipedia.org/wiki/Don%27t_repeat_yourself" rel="nofollow">http://en.wikipedia.org/wiki/Don%27t_repeat_yourself</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://en.wikipedia.org/wiki/Open_source" class="urlextern" title="http://en.wikipedia.org/wiki/Open_source" rel="nofollow">http://en.wikipedia.org/wiki/Open_source</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://en.wikipedia.org/wiki/Data-driven_programming" class="urlextern" title="http://en.wikipedia.org/wiki/Data-driven_programming" rel="nofollow">http://en.wikipedia.org/wiki/Data-driven_programming</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> [New techs &amp; trends] Topology and well defined network actually a virtue. </div>
<ul>
<li class="level2"><div class="li"> <a href="http://en.wikipedia.org/wiki/Distributed_computing" class="urlextern" title="http://en.wikipedia.org/wiki/Distributed_computing" rel="nofollow">http://en.wikipedia.org/wiki/Distributed_computing</a> </div>
</li>
<li class="level2"><div class="li"> <a href="http://storm.incubator.apache.org/" class="urlextern" title="http://storm.incubator.apache.org/" rel="nofollow">http://storm.incubator.apache.org/</a></div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT18 SECTION "Generation:" [18417-19813] -->
<h3 class="sectionedit19" id="limitations_and_futures">Limitations and futures</h3>
<div class="level3">

<p>
Only simple forms. But External libs can be hooked!
</p>

<p>
Usage of interface from sg.atom.world.physics package, should be all in sg.atom.utils only!
</p>

<p>
Lack of unit tests. But in the future
</p>

<p>
Lack of better documentation and education. Here you are, improve it your self.
</p>

</div>
<!-- EDIT19 SECTION "Limitations and futures" [19814-20113] -->
<h2 class="sectionedit20" id="applications">Applications</h2>
<div class="level2">

</div>
<!-- EDIT20 SECTION "Applications" [20114-20136] -->
<h3 class="sectionedit21" id="in_atom_framework">In Atom framework</h3>
<div class="level3">

<p>
Used in Asset/Task packages
</p>

</div>
<!-- EDIT21 SECTION "In Atom framework" [20137-20192] -->
<h3 class="sectionedit22" id="others">Others</h3>
<div class="level3">

<p>
This small library can be used in a wide range of applications especially games and simulations. 
</p>

<p>
</p><p></p><div class="notetip">Don't limit your imagination
</div>


<p>
<a href="http://en.wikipedia.org/wiki/Algorithmic_game_theory" class="urlextern" title="http://en.wikipedia.org/wiki/Algorithmic_game_theory" rel="nofollow">http://en.wikipedia.org/wiki/Algorithmic_game_theory</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/LP-type_problem" class="urlextern" title="http://en.wikipedia.org/wiki/LP-type_problem" rel="nofollow">http://en.wikipedia.org/wiki/LP-type_problem</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Multi-agent_systems" class="urlextern" title="http://en.wikipedia.org/wiki/Multi-agent_systems" rel="nofollow">http://en.wikipedia.org/wiki/Multi-agent_systems</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Auction_Theory" class="urlextern" title="http://en.wikipedia.org/wiki/Auction_Theory" rel="nofollow">http://en.wikipedia.org/wiki/Auction_Theory</a>
</p>

</div>
<!-- EDIT22 SECTION "Others" [20193-20552] -->
<h2 class="sectionedit23" id="alternatives">Alternatives</h2>
<div class="level2">

<p>
For scientific wisdom in Java:
</p>

<p>
<a href="http://jscience.org/" class="urlextern" title="http://jscience.org/" rel="nofollow">http://jscience.org/</a>
</p>

<p>
For full-ledged multi objective meta heristic algorithms, try:
</p>

<p>
<a href="http://www.joptimizer.com" class="urlextern" title="http://www.joptimizer.com" rel="nofollow">http://www.joptimizer.com</a>
</p>

<p>
<a href="http://opt4j.sourceforge.net/" class="urlextern" title="http://opt4j.sourceforge.net/" rel="nofollow">http://opt4j.sourceforge.net/</a>
</p>

<p>
<a href="http://jmetal.sourceforge.net/" class="urlextern" title="http://jmetal.sourceforge.net/" rel="nofollow">http://jmetal.sourceforge.net/</a>
</p>

<p>
Constraint programming and solver:
</p>

<p>
Choco
</p>

<p>
JACK
</p>

<p>
JaCop
</p>

</div>
<!-- EDIT23 SECTION "Alternatives" [20553-] -->
