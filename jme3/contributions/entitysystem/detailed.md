---
title: Entity System Details
---
<h2 class="sectionedit1" id="entity_system_details">Entity System Details</h2>
<div class="level2">

</div>
<!-- EDIT1 SECTION "Entity System Details" [1-34] -->
<h3 class="sectionedit2" id="hello_es">Hello ES</h3>
<div class="level3">

<p>
This wiki is dedicated to who want to do research about Entity System.
</p>

<p>
You should 've read a brief introduction here: <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem:introduction" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem:introduction" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem:introduction</a>
</p>

<p>
And if you still have some concerning you are in the right place! 
</p>

<p>
</p><p></p><div class="noteimportant">This wiki is a collection of known sources, authors from internet and our forum. Corrections are welcome! The main source is the discussion in this topic: <a href="http://hub.jmonkeyengine.org/forum/topic/entity-system-topic-united/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/entity-system-topic-united/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/entity-system-topic-united/</a>
</div>


</div>
<!-- EDIT2 SECTION "Hello ES" [35-576] -->
<h3 class="sectionedit3" id="why_you_here">Why you here?</h3>
<div class="level3">

<p>
'Cause:
</p>
<ol>
<li class="level1"><div class="li"> You may read famous T-machine article about entity systems in mmorpg.</div>
</li>
<li class="level1"><div class="li"> You may come from Unity, UDK, or other engine used it</div>
</li>
<li class="level1"><div class="li"> You may come from Database and web world</div>
</li>
<li class="level1"><div class="li"> You read a lot of articles, forums and try few projects with dramatic debates</div>
</li>
</ol>

<p>
But:
</p>
<ol>
<li class="level1"><div class="li"> You still un sure/ clear about OOP ,COP, data driven…</div>
</li>
<li class="level1"><div class="li"> You doubt ES concept, find its impossible to do ES right</div>
</li>
<li class="level1"><div class="li"> You want to learn more</div>
</li>
</ol>

<p>
I hope this page will help you 30% the way to reach the destination. It's the place where we concern about the design wisdoms of ES, and consider its detailed implementation in Java, eventually integrate in JME3 for a real-time game.
</p>

<p>
</p><p></p><div class="noteimportant">Before you start, I also want to mention that there are fews implementation of ES in JME3, after read this page, you can judge the design of each one arcodingly and choose one. Also read the interviews with each authors about their approaches!
</div>


</div>
<!-- EDIT3 SECTION "Why you here?" [577-1525] -->
<h3 class="sectionedit4" id="scope_structure_of_this_page">Scope &amp; Structure of this page</h3>
<div class="level3">

<p>
1) Introduction:
</p>
<ol>
<li class="level1"><div class="li"> Basic idea of ES : Entity, Processor(System), other terms.</div>
</li>
<li class="level1"><div class="li"> Core elements and its alternative</div>
</li>
<li class="level1"><div class="li"> What is NOT an ES…</div>
</li>
</ol>

<p>
2) Why, when, where ES matter.
</p>
<ol>
<li class="level1"><div class="li"> Pros – cons?</div>
</li>
<li class="level1"><div class="li"> Know issues</div>
</li>
<li class="level1"><div class="li"> OOP to COP, or else</div>
</li>
<li class="level1"><div class="li"> Change of mindset</div>
</li>
</ol>

</div>

<h4 id="cop_s_entity_system_in_oop_java">COP’s Entity System in OOP java</h4>
<div class="level4">

<p>
Entity System in turn is the Core and fundamental and most obvious implementation design of COP (Component oriented programming) in real-time application scale!!!
</p>

<p>
In fact the implementation detail of Entity system is various, some may resembling database core, some may have troubles with OOP incompatibility, some may appear to get all the good of Functional language…
</p>

<p>
but note that Entity System really stand on its own terminology on this single page:
</p><p></p><div class="notewarning">We are talking about the ES within COP, but implemented by an pure OOP like Java.

</div>


</div>
<!-- EDIT4 SECTION "Scope & Structure of this page" [1526-2425] -->
<h2 class="sectionedit5" id="ideas_concepts">Ideas &amp; Concepts</h2>
<div class="level2">

</div>
<!-- EDIT5 SECTION "Ideas & Concepts" [2426-2454] -->
<h3 class="sectionedit6" id="idea">Idea</h3>
<div class="level3">

</div>
<!-- EDIT6 SECTION "Idea" [2455-2468] -->
<h3 class="sectionedit7" id="concept">Concept</h3>
<div class="level3">

<p>
Slides
</p>

<p>
Pictures
</p>

</div>
<!-- EDIT7 SECTION "Concept" [2469-2502] -->
<h3 class="sectionedit8" id="core_elements_and_its_alternative">Core elements and its alternative</h3>
<div class="level3">

<p>
NOTE: Definition notations:
</p>
<ul>
<li class="level1"><div class="li"> Normal is clearly/no doubt in the definition. </div>
</li>
<li class="level1"><div class="li"> <strong>Bold</strong> is keywork.</div>
</li>
<li class="level1"><div class="li"> <em>Italic</em> is example</div>
</li>
<li class="level1"><div class="li"> <em class="u">Underling</em> is doubt</div>
</li>
<li class="level1"><div class="li"> <del>Strike-though</del> is implementation detail, not in the definition</div>
</li>
</ul>

</div>

<h4 id="entity">Entity</h4>
<div class="level4">

<p>
An Entity is simply <strong>an unique Id</strong>. <em>Every Unit, Item, Bullet, etc. in your game will be represented by one of there entity Ids</em>.
</p>

</div>

<h4 id="component">Component</h4>
<div class="level4">

<p>
A Component is a class which only contains data. <del>This means it has a constructor and only getter methods</del>. 
<em>Examples for Components can be:
  * PositionComponent
  * MovementComponent
  * CollsisionComponent</em>
</p>

<p>
Components are <strong>added</strong> to the Entities.
</p>

<p>
There can <strong>only exists one component</strong> of the same class for one entity at the same time.
</p>

<p>
As you can see <strong>Entities are made flexible up of different Components</strong>. <em>You need your Armored Robot?</em> No Problem, you only need to combine the right components. Besides you are able to remove/change/add components during the game <del>which is a huge benefit of Entity Systems.</del>
</p>

</div>

<h4 id="systems">Systems</h4>
<div class="level4">

<p>
Simply all other classes <strong>except the components and the entities</strong> can we consider as systems. You need to pay attention when you read about other Entity Systems because they can have different ideas of what a system is.
</p>

<p>
In the systems you can request all Entities which have special components. 
<em>For example you can say that you want all entities who have a position and a movement component and now calculate the new position for these Entities <del>by overwriting the old position component with a new one</del>.</em>
</p>

</div>
<!-- EDIT8 SECTION "Core elements and its alternative" [2503-4127] -->
<h3 class="sectionedit9" id="ideas_similarity">Ideas similarity:</h3>
<div class="level3">

<p>
from Component oriented architecture:
</p>
<ol>
<li class="level1"><div class="li"> Decoupling</div>
</li>
<li class="level1"><div class="li"> Reusable</div>
</li>
<li class="level1"><div class="li"> Primitive Unit</div>
</li>
</ol>

<p>
from Data driven architecture:
</p>
<ol>
<li class="level1"><div class="li"> Data who decide</div>
</li>
</ol>

<p>
from Data oriented architecture:
</p>
<ol>
<li class="level1"><div class="li"> Everything is data</div>
</li>
<li class="level1"><div class="li"> Repository existence</div>
</li>
<li class="level1"><div class="li"> Homogeneous data</div>
</li>
<li class="level1"><div class="li"> Regular workload</div>
</li>
<li class="level1"><div class="li"> Simple dataflow</div>
</li>
</ol>

<p>
Short explanation
</p>
<ol>
<li class="level1"><div class="li"> Decoupling : each piece can work together without aware of each other.</div>
</li>
<li class="level1"><div class="li"> Resuable : can be easily bring to use again somewhere else</div>
</li>
<li class="level1"><div class="li"> Primitive unit : each piece from a simplest form which contain, fullfil it self.</div>
</li>
<li class="level1"><div class="li"> Data who decide: data decide each and every result, activities of the software</div>
</li>
<li class="level1"><div class="li"> Everything is Data: all piece in the software system is Data</div>
</li>
<li class="level1"><div class="li"> Repository existence: exist a place to keep all the data, the one door to reach them</div>
</li>
<li class="level1"><div class="li"> Homogeneous data : data is treat the same</div>
</li>
<li class="level1"><div class="li"> Regular workload : software that run at regular rate, kind of ballance trade off between performance and complexity</div>
</li>
<li class="level1"><div class="li"> Simple dataflow: the flow of the data is easy to watch, inspect, start stop, manipulate. As the root reason for regular workload!</div>
</li>
</ol>
<pre class="code">Ideas similarities here actually is resulted from with decades of history of revolving of the paradigm. That's why you will see the same concepts of Entity system appear every where from a database to a repository. Of course because it have the same root.Check Pros and Cons chapter for full, detailed idea and design goals and successes.</pre>

</div>
<!-- EDIT9 SECTION "Ideas similarity:" [4128-5555] -->
<h2 class="sectionedit10" id="terms">Terms</h2>
<div class="level2">

<p>
</p><p></p><div class="noteimportant">Here is some terms will be mentioned below but ussually have misunderstaned or misplaced because of their confusioness. Try to do another research to make sure you understand clearly all the terms first!
</div>

<ul>
<li class="level1"><div class="li"> Object Oriented Programming</div>
</li>
<li class="level1"><div class="li"> Data Oriented Programming</div>
</li>
<li class="level1"><div class="li"> Component Oriented Programming</div>
</li>
<li class="level1"><div class="li"> Data driven programming</div>
</li>
<li class="level1"><div class="li"> Data driven solution (architecture)</div>
</li>
</ul>

<p>
Here is a short one to help you get start quickly : <a href="/jme3/contributions/entitysystem/terms.html" class="wikilink1" title="jme3:contributions:entitysystem:terms">terms</a>
</p>

</div>
<!-- EDIT10 SECTION "Terms" [5556-6063] -->
<h2 class="sectionedit11" id="what_is_not_an_es">What is NOT an ES ?</h2>
<div class="level2">

<p>
From more 'open' perspective the core elements can be viewed as, but remember the name as a noun can be mislead: 
<em>This resulted as a dicussion of @pspeed and toolforger, eventually is form a skeptical question, it's really interesting by how we all see this problem confused at first!!</em>
</p>
<pre class="code">  Entity -&gt; ID. It just binds the components together, in the sense that there is one function that creates a bunch of components with the same ID, and one function to destroy all components for an ID. An entity is the set of objects that have the same ID, entities don’t exist as coherent objects inside the code.
  
  Component -&gt; Facet. A position is a facet of an entity, as its velocity, its health, its armor, its whatever. If entities were Java objects, facets would be groups of interrelated properties.
  
  System -&gt; Processor. A function that operates on a slice of components.</pre>

<p>
This often result in mislead skepticism about the design. So get back to read it carefully one more time and some gotchas and practical wisdom below.
</p>

</div>
<!-- EDIT11 SECTION "What is NOT an ES ?" [6064-7138] -->
<h2 class="sectionedit12" id="gotchas_practical_wisdoms">Gotchas &amp; Practical wisdoms</h2>
<div class="level2">

<p>
</p><p></p><div class="notetip">This area contain some best gotchas and practical wisdom when working with ES. I change this to upper position in the page be cause I think practical works save us more than theories. This page can be called a “Design course” after all without this section!!! <img src="/lib/images/smileys/icon_eek.gif" class="icon" alt="8-O" /> <img src="/lib/images/smileys/icon_lol.gif" class="icon" alt="LOL" />
</div>


</div>
<!-- EDIT12 SECTION "Gotchas & Practical wisdoms" [7139-7464] -->
<h3 class="sectionedit13" id="system_processor">System ~ Processor?</h3>
<div class="level3">
<pre class="code">  In a pure ES, this is not a thing, really. Some implementations force this on you because they couldn’t think how to do the ES job efficiently… but it’s still not a thing. All of your code that isn’t an ES is a “system”, technically.</pre>

<p>
System = everything that isn’t an Entity or a Component but uses Entities and Components.
</p>

</div>
<!-- EDIT13 SECTION "System ~ Processor?" [7465-7837] -->
<h3 class="sectionedit14" id="entity_gameobject">Entity ~ GameObject?</h3>
<div class="level3">

<p>
Entity should just be interpreted as a bunch of its Component. GameObject or anything else represented by an Entity is by accident. So no force to represent “all-every” gameobject as Entity; and no force that “all-every” Entity is gameobject.
</p>

</div>
<!-- EDIT14 SECTION "Entity ~ GameObject?" [7838-8118] -->
<h3 class="sectionedit15" id="has_is">Has ~ Is?</h3>
<div class="level3">

<p>
From software designer POV, Relationship in COP is a sensitive topic; by nature, Component is against (or overide) Relation.
</p>

<p>
The deception ‘Has’ relationship between Entity and its Component actually represent everything in various meaning from the literature ‘Is’ , or literature ‘Has’.. to ‘related to’. BUT keep in mind, this is blury and its almost always implemented as indirect acess, not like a property in an object but envolve processing-lookup under the curtain! So you may find this difficult to extract and detect these different from your tranditional OOP software design!
</p>

</div>
<!-- EDIT15 SECTION "Has ~ Is?" [8119-8739] -->
<h3 class="sectionedit16" id="some_insights">Some insights</h3>
<div class="level3">

<p>
This is the place to share the “real world” difficuties when working with ES, here in JME3 or in other engines. In Practical wisdoms will raise some known solutions for them. This section may revive some part of the Cons or known issues sections but practically.
</p>

</div>
<!-- EDIT16 SECTION "Some insights" [8740-9025] -->
<h3 class="sectionedit17" id="practical_wisdoms">Practical wisdoms</h3>
<div class="level3">

</div>
<!-- EDIT17 SECTION "Practical wisdoms" [9026-9051] -->
<h2 class="sectionedit18" id="es_done_right">ES done right</h2>
<div class="level2">

<p>
Because this topic is so debatable, there is no solid candidate for ES done right now in my POV, but Zay-ES and Artemis are closest one, Zay-ES a little bit better as its the later born.
</p>

</div>

<h4 id="why_debatable_short">Why debatable [Short]?</h4>
<div class="level4">

<p>
Because apply to each game, the scenarios and usecases are vary difference. Situation changes, a design which should be right can be a failure!  You may see the point.
</p>

<p>
This topic start flame in almost every dicussions I've come through, someone should be like OOP versus COP, ES is not for all,..etc. At first, the debate should focus into a specific scope, specific genre. Here (this page) we still arrange the statements like general scope. But later in the interviews you can see some “real” applications and implementations.
</p>

</div>

<h4 id="should_be">Should be?</h4>
<div class="level4">

<p>
Theoricaly an Java ES done right should be:
</p>
<ol>
<li class="level1"><div class="li"> Pure data : very debatable</div>
<ol>
<li class="level2"><div class="li"> – Mutable : as bean with setter and getter</div>
</li>
<li class="level2"><div class="li"> – Immutate : as bean with getter, should be replace if changed.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Multi-threading, concurency enable : very debatable</div>
<ol>
<li class="level2"><div class="li"> – As my experience, pure data or not is not clear contract to multi-threading success. Consider other things happen outside of ES scope, so it not an solid waranty that those component will not be touched by any other thread.</div>
</li>
<li class="level2"><div class="li"> – Also if there is a contract that no other thread touching those data, in Java style via synchonization or other paradigm like actor… multi-threading also consider success but just more complicated!</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Communication: very debatable</div>
<ol>
<li class="level2"><div class="li"> – Event messaging enable</div>
</li>
<li class="level2"><div class="li"> – No event or messaging : update beat, no need of inter-com or events. How can we do network messaging?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Is database (and other kind of persistent) friendly</div>
<ol>
<li class="level2"><div class="li"> – Save to XML?</div>
</li>
<li class="level2"><div class="li"> – Send over network?</div>
</li>
<li class="level2"><div class="li"> – Change sets are resembling Databse concept, what about tranactions?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Is enterprise friendly (expanable/ extensible/ modulizable)</div>
<ol>
<li class="level2"><div class="li"> – Spring, as lazy loaded, injected?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Script possibilities</div>
<ol>
<li class="level2"><div class="li"> – Can be script, non trivial work in pure data!</div>
</li>
<li class="level2"><div class="li"> – Can be use with other JVM language than java like groovy, or scala, jython?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Restrictions and limitation</div>
<ol>
<li class="level2"><div class="li"> – No dynamic Java object methods in Component ? What about Entities and Systems ( Processors)</div>
</li>
<li class="level2"><div class="li"> – An overal way to manage and config Systems, freely chose? How to hook to its routine?</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Depedencies</div>
<ol>
<li class="level2"><div class="li"> – The separation of components are clear, as no dependencies at all. Hard cored, scripted or injected will break the overal contract!</div>
</li>
<li class="level2"><div class="li"> – The separation of Entities. What about depedencies of entities? Ex: parent/ child relationship in JME spatial. How the framework handle that?</div>
</li>
<li class="level2"><div class="li"> – The separation of Systems. Ex: any contract about that?</div>
</li>
</ol>
</li>
</ol>

<p>
Detailed explaination : <a href="/jme3/contributions/entitysystem/points.html" class="wikilink1" title="jme3:contributions:entitysystem:points">points</a>
</p>

</div>
<!-- EDIT18 SECTION "ES done right" [9052-11854] -->
<h2 class="sectionedit19" id="design">Design</h2>
<div class="level2">

<p>
</p><p></p><div class="noteimportant">In Design phase, even don't know any of implementation detail, we judge upon the design concepts and its Infrastructure!!!. Detailed implementation judge will be considered later!
</div>
<p></p><div class="noteimportant">This is a short checklist that help you open your mind before going to design an ES. It's short and trusted; the Pos and cons section needed previewing and under heavy concerning!
</div>


</div>
<!-- EDIT19 SECTION "Design" [11855-12279] -->
<h3 class="sectionedit20" id="why_when_where_es_matter">Why, when, where ES matter.</h3>
<div class="level3">

</div>

<h4 id="why">Why?</h4>
<div class="level4">
<ol>
<li class="level1"><div class="li"> BLOB aka The fall of inheritance: Complex type can not be represent as class in java OOP!</div>
</li>
<li class="level1"><div class="li"> Tired of OOP. Compose over old-skool programming . Like artists.</div>
</li>
<li class="level1"><div class="li"> Reusable via prefab (well, this is very debatable as compare OOP!!)</div>
</li>
<li class="level1"><div class="li"> …</div>
</li>
</ol>

</div>

<h4 id="when">When?</h4>
<div class="level4">
<ol>
<li class="level1"><div class="li"> Trade off between complexity and performance is carefully considered.</div>
</li>
<li class="level1"><div class="li"> Input and output are well setup. Assets are all in good format, output are well defined, workflow and routines are fixed. Seen in commercial 3D game engine.</div>
</li>
</ol>

</div>

<h4 id="where">Where?</h4>
<div class="level4">
<ol>
<li class="level1"><div class="li"> Mainly to handles/ manage your data and entities.</div>
</li>
<li class="level1"><div class="li"> Usually in MMO where BLOB happen.</div>
</li>
<li class="level1"><div class="li"> Batch/ cache processing enviroment, device. GPU, others.</div>
</li>
</ol>

</div>
<!-- EDIT20 SECTION "Why, when, where ES matter." [12280-12986] -->
<h3 class="sectionedit21" id="why_not">Why not?</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> It’s easy to get it wrong as you often come from OOP world (of course, because you are Java developer).</div>
</li>
<li class="level1"><div class="li"> Can result in done wrong too much time, that un affordable!!</div>
</li>
<li class="level1"><div class="li"> It’s *not* an certainly proved technology (that why we here)</div>
</li>
<li class="level1"><div class="li"> Its have bad issues</div>
</li>
<li class="level1"><div class="li"> Only suite for cases (not every)</div>
</li>
<li class="level1"><div class="li"> No good IDE, <abbr title="Graphical User Interface">GUI</abbr> support in Java or JME3 world currently</div>
</li>
</ol>

</div>

<h4 id="when_not">When not?</h4>
<div class="level4">
<ol>
<li class="level1"><div class="li"> Limited time and first try! ( can be good if in limited time but ES is production mode ready)</div>
</li>
<li class="level1"><div class="li"> Small game, simple gameplay …</div>
</li>
</ol>

</div>
<!-- EDIT21 SECTION "Why not?" [12987-13521] -->
<h3 class="sectionedit22" id="pros_cons">Pros – cons?</h3>
<div class="level3">

<p>
Here, I listed the pros – cons of the COP and Pure data ES. 
</p><p></p><div class="notewarning">needed previewing and under heavy concerning!
</div>


<p>
</p><p></p><div class="noteimportant">You can see I try as the one who repeat sentences that speak out by others in various sources as a short manner! So this list and information need clarification of correction afterward!
</div>


</div>
<!-- EDIT22 SECTION "Pros – cons?" [13522-13885] -->
<h3 class="sectionedit23" id="pros">Pros:</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> No BLOB anti-pattern, no deep inheritance consider bad effects</div>
</li>
</ol>

<p>
Read: <a href="http://gamearchitect.net/Articles/GameObjects1.html" class="urlextern" title="http://gamearchitect.net/Articles/GameObjects1.html" rel="nofollow">http://gamearchitect.net/Articles/GameObjects1.html</a>
</p>

<p>
A lot of good things come if done “right”!
</p>
<ol>
<li class="level1"><div class="li"> Simple, intuitive</div>
</li>
<li class="level1"><div class="li"> Communication made simple</div>
</li>
<li class="level1"><div class="li"> What you see is what you have → composing</div>
</li>
<li class="level1"><div class="li"> Reusable with prefab</div>
</li>
<li class="level1"><div class="li"> Batch / Concurent processing/caching as in modern CPU, GPU</div>
</li>
<li class="level1"><div class="li"> … ten more</div>
</li>
</ol>

<p>
<a href="http://piemaster.net/2011/07/entity-component-primer/" class="urlextern" title="http://piemaster.net/2011/07/entity-component-primer/" rel="nofollow">http://piemaster.net/2011/07/entity-component-primer/</a>
</p>

</div>
<!-- EDIT23 SECTION "Pros:" [13886-14332] -->
<h3 class="sectionedit24" id="cons">Cons:</h3>
<div class="level3">

<p>
</p><p></p><div class="noteimportant">'Problem' here means the 'problem' to solve not a bad situation!
</div>

<ol>
<li class="level1"><div class="li"> No OOP: COP Done “right” means forget about almost all OOP things: Pure data, Class become Type, no inheritance, encapsulation…etc , no best of both world!</div>
</li>
<li class="level1"><div class="li"> Spliting dilemma: Same with OOP Classify problem: How to split, how to change the data when you change the splits?</div>
</li>
<li class="level1"><div class="li">Duplicated component: Same root as confusion in component spliting but, this problem about how can we made a more than one component of a kind per object entity… Ex: Car with 4 wheels, the component will be a 1stWheel, 2ndWheel, or a single list of WheelComponent… ?</div>
</li>
<li class="level1"><div class="li"> Data resampling problem in game, data such as textures, text, 3d models everything … should be crafted: made, converted again to suite with existing data model – that’s the component in the ES.</div>
</li>
<li class="level1"><div class="li"> Mindset change problem: One will have to re-code a fews time to implement an ES, in initial, half ass and full level.</div>
</li>
<li class="level1"><div class="li"> Flat table problem: Because ES is a big table by nature, with component set is a row. It’s as efficient even less than a big table, which form the flat table problem as seen in many indexed base database. Tree, Graph and other data structure will almost immediately break the ES contract!!</div>
</li>
<li class="level1"><div class="li"> Observation problem: As update beat over listening method, ES restrict the observation methods a lot.</div>
</li>
<li class="level1"><div class="li"> Sercurity problem : No encapsulation, kind of no private POJO mean no java power in protecting data, a lot of security holes! ES implementations and COP forget all about sercurity danger as Component contracted to be processed by Processor but not hiding its content.</div>
</li>
<li class="level1"><div class="li"> Scale : In theory, ES should scale well..!!! But read this carefully or mislead it, enterprise system need much more than just a way to orginize your data!!! </div>
</li>
</ol>

<p>
</p><p></p><div class="notetip">Because a lot of people find interests about the down side of ES, I've listed them carefully here <a href="/doku.php/jme3:contributions:entitysystem:detailed:cons" class="wikilink2" title="jme3:contributions:entitysystem:detailed:cons" rel="nofollow">cons</a>. After knowing the acceptable solutions from the authors, I will remove or marked the solved problem! [Peace! :p]
</div>


</div>
<!-- EDIT24 SECTION "Cons:" [14333-16438] -->
<h3 class="sectionedit25" id="es_consider_good_design_in_real-time_app">ES consider good design in real-time app?</h3>
<div class="level3">

<p>
</p><p></p><div class="notewarning">Of course, ES has its mising features!!!!
</div>


<p>
But for some reason its design ‘s consider good for real=time application like a “common” video Game, or “common” simmulation; especially common in MMO world.
</p>

<p>
Here is a short of ‘why’ answers from a software architecture designer view, explain based on its borrowed ideas: [This is very different from various source you've read, because it's not embeded any implementation details!!!]
</p>
<ol>
<li class="level1"><div class="li"> Decoupling : each piece can work together without aware of each other.</div>
</li>
<li class="level1"><div class="li"> Resuable : can be easily bring to use again somewhere else.</div>
</li>
<li class="level1"><div class="li"> Composable : each piece can work together</div>
</li>
</ol>

<p>
have fundamental relationship with decoupling.
</p>
<ol>
<li class="level1"><div class="li"> Primitive unit : each piece from a simplest form which contain, fullfil it self.</div>
</li>
</ol>

<p>
have fundamental relationship with decoupling.
</p>

<p>
(*) These lead to advantages in development:
</p>
<ol>
<li class="level1"><div class="li"> do it in one place only when doing implementation (coding, configs…), .</div>
</li>
<li class="level1"><div class="li"> intuitive and ease of development jobs (compose entity with component drag and drop)</div>
</li>
<li class="level1"><div class="li"> distributed jobs, assets</div>
</li>
<li class="level1"><div class="li"> reuse data, code which in existed component</div>
</li>
<li class="level1"><div class="li"> unit test</div>
</li>
<li class="level1"><div class="li"> [more]</div>
</li>
</ol>

<p>
——————————————————————————————
</p>
<ol>
<li class="level1"><div class="li"> Data who decide: data decide each and every result, activities of the software</div>
</li>
<li class="level1"><div class="li"> Everything is Data: all piece in the software system is Data</div>
</li>
<li class="level1"><div class="li"> Repository existence: exist a place to keep all the data, the one door to reach them</div>
</li>
</ol>

<p>
(*) These open the world of complex gameplay and distributed persistent like seen in MMO. A single data change can result in change in the gameplay; a
——————————————————————————————
</p>
<ol>
<li class="level1"><div class="li"> Homogeneous data : data is treat the same</div>
</li>
<li class="level1"><div class="li"> Regular workload : software that run at regular rate, kind of ballance trade off between performance and complexity</div>
</li>
<li class="level1"><div class="li"> Simple dataflow: the flow of the data is easy to watch, inspect, start stop, manipulate. As the root reason for regular workload!</div>
</li>
</ol>

<p>
(*) These lead to a lot of simple but efficient algorithm to get high performance in runtime for a software such like a “common” video game, which run in console, GPU, CPU which envolve and share the same model with cache and batch intructions, an a certain hearbeat…Notice the bottleneck of CPU-GPU and between different processing unit, platform is the most headache of Game designer for decade is ease with the regular workload; let the game run smoothly and stable, result into nice visual representation..
</p>

</div>
<!-- EDIT25 SECTION "ES consider good design in real-time app?" [16439-19025] -->
<h3 class="sectionedit26" id="es_consider_bad_design_in">ES consider bad design in …?</h3>
<div class="level3">

<p>
From @pspeed:
</p>
<pre class="code">  It is a bad design choice where:
  - there aren’t many entities and/or the behavior is so clearly defined that you’d just implement it one or two classes. Thing card games, a lot of puzzle games, etc..
  - the game is so simple that it’s just implemented as JME controls and a few app states. You could use an ES here but it would be wasted.
  - the game logic cuts across all objects nearly all the time. (I think of card games and puzzle games again.) This usually implies that there are few entities, though.
  - the team doing the work will have trouble understanding an ES. To me this is a huge one. Sometimes our choice of technologies is not dictated by what might be technically best… but what is technically best for the skills of the team. For example, if your artist only knows Sketchup then Blender is probably not the right tool even if it is superior in many ways. </pre>

</div>
<!-- EDIT26 SECTION "ES consider bad design in …?" [19026-19980] -->
<h3 class="sectionedit27" id="known_issues">Known issues:</h3>
<div class="level3">

<p>
Even if done right, the ES also have it underlying issues which noticed by its authors, (that means annoying things)! 
</p>

<p>
<strong>Why this section havs things from the Cons section but consider differrently?</strong>
</p>
<pre class="code">In Cons section descible problem should be concerned, likely to be done wrong, or the limit of the design they can be solve in implementations or not is not important!</pre>
<pre class="code">Known issue is the problem persist in even the well designed; or persist due to the underlying infrastructure, application, programming language, etc!!</pre>

</div>

<h4 id="communication">Communication:</h4>
<div class="level4">

<p>
Happen in non pure data solution, when Components don’t function independently of each other. Some means of communication is necessary
• Two approaches (both viable):
</p>
<pre class="code">– Direct communication using dynamic cast and function calls
– Indirect communication using message passing</pre>

<p>
In pure data solution, by not query or just loop through interested component at one update cycle, the Processor eases out the need of other communication, but in complex scenario, such as combine with outter event handling such as Network, where message passing is nature, the problem still persist!
</p>

<p>
as decribled in reference [6]
Read: <a href="http://acmantwerp.acm.org/wp-content/uploads/2010/10/componentbasedprogramming.pdf" class="urlextern" title="http://acmantwerp.acm.org/wp-content/uploads/2010/10/componentbasedprogramming.pdf" rel="nofollow">http://acmantwerp.acm.org/wp-content/uploads/2010/10/componentbasedprogramming.pdf</a>
———————————————————–
</p>

</div>

<h4 id="script">Script</h4>
<div class="level4">

<p>
The “script problem” happen by the same reason with the “communication problem” mixed with “pure data or not” problem. When an component is hard to inspect, its outter relationship hard to define and its property is rejected to change, how can you script it?
</p>

<p>
Read: <a href="http://blog.gemserk.com/2011/11/13/scripting-with-artemis/" class="urlextern" title="http://blog.gemserk.com/2011/11/13/scripting-with-artemis/" rel="nofollow">http://blog.gemserk.com/2011/11/13/scripting-with-artemis/</a>
</p>

<p>
Nearly one end up back to half ass solution, not a pure data ES if their really need scripting in.
———————————————————–
</p>

</div>

<h4 id="arbitrary_routine_and_query">Arbitrary Routine and Query</h4>
<div class="level4">

<p>
<a href="http://hub.jmonkeyengine.org/forum/topic/in-range-detection-with-lots-of-entities/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/in-range-detection-with-lots-of-entities/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/in-range-detection-with-lots-of-entities/</a>
</p>

</div>
<!-- EDIT27 SECTION "Known issues:" [19981-21953] -->
<h2 class="sectionedit28" id="implementation_approaches">Implementation Approaches</h2>
<div class="level2">

</div>
<!-- EDIT28 SECTION "Implementation Approaches" [21954-21991] -->
<h2 class="sectionedit29" id="oop_to_cop__or_else">OOP to COP . or else?</h2>
<div class="level2">

<p>
<em class="u">@atomix POV:</em>
</p>

<p>
As said, as a long term java developer and also an artist. I can not see a strong, confident reason why we should switch over to COP at the moment.
</p>

<p>
BLOB is not a problem with a carefully designed software, same as hard as split your components… Deep inheritance even multi inheritance problem can not be reached in an indie project, and even it reached, maintain it always easier than redesign a 3D model to change the export pipeline!!!
</p>

<p>
Also the tangled wires between inheritance form the nature of programming and matter in the universal. :p 
</p>

<p>
<strong>BUT</strong> They have IDE support, profiler, proved technologies, lot more… We talking about a no IDE support paradigm with plain text editor, table and some black magic, tell me more about the company will approve your plan?
</p>

<p>
Some alternate solution may solve almost your design goal when you likely to use an ES:
</p>
<ol>
<li class="level1"><div class="li"> Smart bean framework : try Spring, EJB. For Enterprise, if you've known EJB and Spring, you will not bet in home grown ES, dont you? </div>
</li>
<li class="level1"><div class="li"> Actor framework: try AKKA</div>
</li>
<li class="level1"><div class="li"> If you see java as a failure, try Scala’s trail …</div>
</li>
</ol>

<p>
</p><p></p><div class="notewarning">So, my last advice is: If you are not doing MMO <strong>Take a look in other alternative technologies.</strong> !!!!
</div>

<ol>
<li class="level1"><div class="li"> Take a look at reference [7] and <a href="http://lambdor.net/?p=171" class="urlextern" title="http://lambdor.net/?p=171" rel="nofollow">http://lambdor.net/?p=171</a> , the guy suggest you to switch to Functional reactive programming :p</div>
</li>
<li class="level1"><div class="li"> Try Scala and AKKA and read more about concurrency , don't use flat table!!!</div>
</li>
</ol>

</div>
<!-- EDIT29 SECTION "OOP to COP . or else?" [21992-23472] -->
<h2 class="sectionedit30" id="change_of_mindset">Change of mindset</h2>
<div class="level2">

<p>
</p><p></p><div class="noteimportant">I think this should be in another page or even in a book! :p
</div>
This chapter dedicated to people still who really want to <strong>switch to this new paradigm</strong> after all the warning and awarenesses.
So this chapter will mainly answer the BIG question:


<p>
<strong>What should be change to adapt to this new paradigm?</strong>
</p>

</div>
<!-- EDIT30 SECTION "Change of mindset" [23473-23824] -->
<h3 class="sectionedit31" id="what_will_we_face">What will we face</h3>
<div class="level3">

</div>
<!-- EDIT31 SECTION "What will we face" [23825-23850] -->
<h3 class="sectionedit32" id="what_should_be_change">What should be change</h3>
<div class="level3">

</div>
<!-- EDIT32 SECTION "What should be change" [23851-23880] -->
<h3 class="sectionedit33" id="oop_object_modeling_vs_cop_object_modeling">OOP Object Modeling vs COP Object Modeling</h3>
<div class="level3">

</div>
<!-- EDIT33 SECTION "OOP Object Modeling vs COP Object Modeling" [23881-23932] -->
<h3 class="sectionedit34" id="team_management">Team management</h3>
<div class="level3">

</div>
<div class="level3">

</div>
<!-- EDIT34 SECTION "Team management" [23933-23969] -->
<h2 class="sectionedit35" id="java_entity_system_projects">Java Entity System projects</h2>
<div class="level2">

<p>
Some open source Entity System implementation projects:
</p>

</div>

<h4 id="artemisgeneral">Artemis: General</h4>
<div class="level4">

<p>
GoogleCode: <a href="https://code.google.com/p/artemis-framework/" class="urlextern" title="https://code.google.com/p/artemis-framework/" rel="nofollow">https://code.google.com/p/artemis-framework/</a>
</p>

<p>
Website: <a href="http://gamadu.com/artemis/index.html" class="urlextern" title="http://gamadu.com/artemis/index.html" rel="nofollow">http://gamadu.com/artemis/index.html</a>
</p>

<p>
Wiki: <a href="http://entity-systems.wikidot.com/artemis-entity-system-framework" class="urlextern" title="http://entity-systems.wikidot.com/artemis-entity-system-framework" rel="nofollow">http://entity-systems.wikidot.com/artemis-entity-system-framework</a>
</p>

<p>
</p><p></p><div class="noteimportant">Review: HERE! <a href="/doku.php/jme3:contributions:entitysystem:interviews:artemis" class="wikilink2" title="jme3:contributions:entitysystem:interviews:artemis" rel="nofollow">artemis</a> because I can not contact with author of Artemis at the moment so I will have a short review of it with some of my experience working on it and base on its source code!
</div>


</div>

<h4 id="spartanused_for_slick_abandoned">Spartan: [used for Slick. abandoned]</h4>
<div class="level4">

<p>
GoogleCode: <a href="http://code.google.com/p/spartanframework/" class="urlextern" title="http://code.google.com/p/spartanframework/" rel="nofollow">http://code.google.com/p/spartanframework/</a>
————————————————————-
</p>

</div>
<!-- EDIT35 SECTION "Java Entity System projects" [23970-24691] -->
<h3 class="sectionedit36" id="jme_integrated">JME integrated</h3>
<div class="level3">

</div>

<h4 id="zay-espspeed">Zay-ES : @pspeed</h4>
<div class="level4">

<p>
Post: <a href="http://hub.jmonkeyengine.org/forum/topic/my-es-in-contrib-zay-es/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/my-es-in-contrib-zay-es/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/my-es-in-contrib-zay-es/</a>
</p>

<p>
Forum : <a href="http://hub.jmonkeyengine.org/forum/board/projects/zay-es/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/board/projects/zay-es/" rel="nofollow">http://hub.jmonkeyengine.org/forum/board/projects/zay-es/</a>
</p>

<p>
Wiki: <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem</a>
</p>

<p>
Links: <a href="http://hub.jmonkeyengine.org/forum/topic/zay-es-links/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/zay-es-links/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/zay-es-links/</a>
</p>

<p>
Interview:
</p>

</div>

<h4 id="entitymonkeyzzuegg">EntityMonkey : @zzuegg</h4>
<div class="level4">

<p>
Post: <a href="http://hub.jmonkeyengine.org/forum/topic/entitymonkey-a-simple-entity-system-for-jme/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/entitymonkey-a-simple-entity-system-for-jme/" rel="nofollow">http://hub.jmonkeyengine.org/forum/topic/entitymonkey-a-simple-entity-system-for-jme/</a>
</p>

</div>

<h4 id="privateempire_phoenix">Private : @Empire phoenix</h4>
<div class="level4">

<p>
Interview:
</p>

</div>
<!-- EDIT36 SECTION "JME integrated" [24692-25204] -->
<h3 class="sectionedit37" id="implementation_and_scope_of_each_projects">Implementation, and scope of each projects:</h3>
<div class="level3">

<p>
The comparasions will focus in these below points, follow with the scope, status of each projects
</p>
<ol>
<li class="level1"><div class="li"> Initial philosophy</div>
</li>
<li class="level1"><div class="li"> Pure data or not?</div>
</li>
<li class="level1"><div class="li"> Multi-threading, concurency enable or not?</div>
</li>
<li class="level1"><div class="li"> Communication: Event messaging enable or not?</div>
</li>
<li class="level1"><div class="li"> Is database (and other kind of persistent) friendly or not?</div>
</li>
<li class="level1"><div class="li"> Is enterprise friendly (expanable/ extensible/ modulizable) or not?</div>
</li>
<li class="level1"><div class="li"> Script possibilities?</div>
</li>
<li class="level1"><div class="li"> Restrictions and limitation</div>
</li>
<li class="level1"><div class="li"> Dependencies</div>
</li>
<li class="level1"><div class="li"> Current status: Long term, stable, community?</div>
</li>
</ol>

<p>
[More]
———————————————————————————————
</p>

<p>
</p><p></p><div class="noteimportant">The Comparasion table is in Google doc: Help me fill it!!!!
</div>


<p>
<a href="https://docs.google.com/document/d/1pRTZPFtHz7pUzYcoFiSTm-mUCA-BVYvFpUp6diIsuEo/edit?usp=sharing" class="urlextern" title="https://docs.google.com/document/d/1pRTZPFtHz7pUzYcoFiSTm-mUCA-BVYvFpUp6diIsuEo/edit?usp=sharing" rel="nofollow">https://docs.google.com/document/d/1pRTZPFtHz7pUzYcoFiSTm-mUCA-BVYvFpUp6diIsuEo/edit?usp=sharing</a>
</p>

</div>
<!-- EDIT37 SECTION "Implementation, and scope of each projects:" [25205-26041] -->
<h2 class="sectionedit38" id="researches_articles">Researches &amp; Articles</h2>
<div class="level2">

<p>
Link to articles, researches and papers you should read:
</p>

<p>
<strong>Start of the wave</strong>
</p>

<p>
[1] <a href="http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/" class="urlextern" title="http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/" rel="nofollow">http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/</a>
</p>

<p>
<strong>Sploreg ES in JME introduction in indiedb</strong>
</p>

<p>
[2] <a href="http://www.indiedb.com/games/attack-of-the-gelatinous-blob/news/the-entity-system" class="urlextern" title="http://www.indiedb.com/games/attack-of-the-gelatinous-blob/news/the-entity-system" rel="nofollow">http://www.indiedb.com/games/attack-of-the-gelatinous-blob/news/the-entity-system</a>
</p>

<p>
<strong>Worth to read, pspeed conversation with Michael Leahy, also lead another ES project TyphonRT</strong>
</p>

<p>
[3] <a href="http://t-machine.org/index.php/2011/06/24/using-an-entity-system-with-jmonkeyengine-mythruna/" class="urlextern" title="http://t-machine.org/index.php/2011/06/24/using-an-entity-system-with-jmonkeyengine-mythruna/" rel="nofollow">http://t-machine.org/index.php/2011/06/24/using-an-entity-system-with-jmonkeyengine-mythruna/</a>
</p>

<p>
<strong>Our wiki link</strong>
</p>

<p>
[4] <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem:introduction" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem:introduction" rel="nofollow">http://hub.jmonkeyengine.org/wiki/doku.php/jme3:contributions:entitysystem:introduction</a>
</p>

<p>
<strong>Beside of BLOB anti pattern, explain why ES suite as data in modern GPU, CPU!</strong>
</p>

<p>
[5] <a href="http://gamesfromwithin.com/data-oriented-design" class="urlextern" title="http://gamesfromwithin.com/data-oriented-design" rel="nofollow">http://gamesfromwithin.com/data-oriented-design</a>
</p>

<p>
<strong>Worth to read, paper of another C++ ES leader of cistron project <a href="http://code.google.com/p/cistron" class="urlextern" title="http://code.google.com/p/cistron" rel="nofollow">http://code.google.com/p/cistron</a></strong>
</p>

<p>
[6] <a href="http://acmantwerp.acm.org/wp-content/uploads/2010/10/componentbasedprogramming.pdf" class="urlextern" title="http://acmantwerp.acm.org/wp-content/uploads/2010/10/componentbasedprogramming.pdf" rel="nofollow">http://acmantwerp.acm.org/wp-content/uploads/2010/10/componentbasedprogramming.pdf</a>
</p>

<p>
<strong>Stack over flow topic, links, texts and especially interesting recommendation to switch form CBSE , COP to functional programming!</strong>
</p>

<p>
[7] <a href="http://stackoverflow.com/questions/1901251/component-based-game-engine-design" class="urlextern" title="http://stackoverflow.com/questions/1901251/component-based-game-engine-design" rel="nofollow">http://stackoverflow.com/questions/1901251/component-based-game-engine-design</a>
</p>

<p>
<strong>Link to other entitiy system approaches in its own wikidot!</strong>
</p>

<p>
[8] <a href="http://entity-systems.wikidot.com/es-approaches" class="urlextern" title="http://entity-systems.wikidot.com/es-approaches" rel="nofollow">http://entity-systems.wikidot.com/es-approaches</a>
</p>

<p>
[9] An interesting write up in GDD about ES and Events in a game engine. And some production,workflow concerns
</p>

<p>
<a href="http://stefan.boxbox.org/2012/11/14/game-development-design-1-the-component-system/" class="urlextern" title="http://stefan.boxbox.org/2012/11/14/game-development-design-1-the-component-system/" rel="nofollow">http://stefan.boxbox.org/2012/11/14/game-development-design-1-the-component-system/</a>
</p>

<p>
<strong>[More?]</strong>
</p>

</div>
<!-- EDIT38 SECTION "Researches & Articles" [26042-] -->
