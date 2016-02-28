---
title: Object Oriented Programming
---
<h2 class="sectionedit1" id="object_oriented_programming">Object Oriented Programming</h2>
<div class="level2">

<p>
Object-oriented programming (OOP) is a programming paradigm that represents concepts as “objects” that have data fields (attributes that describe the object) and associated procedures known as methods.
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Object-oriented_programming" class="urlextern" title="http://en.wikipedia.org/wiki/Object-oriented_programming" rel="nofollow">http://en.wikipedia.org/wiki/Object-oriented_programming</a>
</p>

<p>
—————————————————————————————
</p>

</div>
<!-- EDIT1 SECTION "Object Oriented Programming" [1-391] -->
<h2 class="sectionedit2" id="data_oriented_programming">Data Oriented Programming</h2>
<div class="level2">

<p>
[This just not exist]
</p>

<p>
If you use Data-oriented_languages, you can call it Data Oriented Programming! You may talking about *Data Oriented Design (Architecture)* instead
</p>

<p>
<a href="http://stackoverflow.com/questions/4122696/what-is-data-oriented-programming" class="urlextern" title="http://stackoverflow.com/questions/4122696/what-is-data-oriented-programming" rel="nofollow">http://stackoverflow.com/questions/4122696/what-is-data-oriented-programming</a>
</p>

<p>
<a href="http://en.wikipedia.org/wiki/List_of_programming_languages_by_category#Data-oriented_languages" class="urlextern" title="http://en.wikipedia.org/wiki/List_of_programming_languages_by_category#Data-oriented_languages" rel="nofollow">http://en.wikipedia.org/wiki/List_of_programming_languages_by_category#Data-oriented_languages</a>
</p>

<p>
—————————————————————————————
</p>

</div>
<!-- EDIT2 SECTION "Data Oriented Programming" [392-860] -->
<h2 class="sectionedit3" id="component_oriented_programming">Component Oriented Programming</h2>
<div class="level2">

<p>
This is “the rising force” we are talking about!
</p>

<p>
It’s a “rather new” programming paradigm. Despite of its name and even the fact it’s was born from the marriage of “Component base architecture” and “Data oriented architecture”, but something different.
</p>

<p>
—————————————————————————————
</p>

</div>
<!-- EDIT3 SECTION "Component Oriented Programming" [861-1264] -->
<h2 class="sectionedit4" id="cop_s_entity_system_in_oop_java">COP’s Entity System in OOP java</h2>
<div class="level2">

<p>
Entity System in turn is the Core and fundamental and most obvious implementation design of COP!!!
</p>

<p>
In fact the implementation detail of Entity system is various, some may resembling database core, some may have troubles with OOP incompatibility, some may appear to get all the good of Functional language…
</p>

<p>
but note that Entity System really stand on its own terminology on this single page:
We are talking about the ES within COP, but implemented by an pure OOP like Java.
—————————————————————————————
</p>

</div>
<!-- EDIT4 SECTION "COP’s Entity System in OOP java" [1265-1873] -->
<h2 class="sectionedit5" id="data_driven_programming">Data driven programming:</h2>
<div class="level2">

<p>
You may refer to this “Data driven programming” incorrectly in this ES topic, you may talking about: *Data driven design* insted
</p>

<p>
In computer programming, data-driven programming is a programming paradigm in which the program statements describe the data to be matched and the processing required rather than defining a sequence of steps to be taken
</p>

<p>
<a href="http://en.wikipedia.org/wiki/Data-driven_programming" class="urlextern" title="http://en.wikipedia.org/wiki/Data-driven_programming" rel="nofollow">http://en.wikipedia.org/wiki/Data-driven_programming</a>
</p>

<p>
—————————————————————————————
</p>

</div>
<!-- EDIT5 SECTION "Data driven programming:" [1874-2405] -->
<h2 class="sectionedit6" id="data_driven_solution_architecture">Data driven solution (architecture):</h2>
<div class="level2">
<pre class="code">  Data driven, on the other hand, can mean a few different things. A common usage is one you may already be using. For example. abstracting something like:
  if( a == 0 ) doFoo()
  else if( a == 1 ) doBar()
  into:
  Command[] commands….
  commands[a].doIt()
  …is a data-driven design.</pre>
<pre class="code">  Data driven solution (architecture) is a software solution (architecture) where everything is from data and to data, data who decide!</pre>
<pre class="code">  http://www.enterpriseappstoday.com/business-intelligence/3-rules-for-data-driven-architecture.html</pre>
<pre class="code">  It has the “data force”, that’s why it call ‘driven’, the force sometime a “generative force”!</pre>

<p>
—————————————————————————————
</p>

</div>
<!-- EDIT6 SECTION "Data driven solution (architecture):" [2406-3204] -->
<h2 class="sectionedit7" id="data_oriented_design_architecture">Data oriented (design) architecture:</h2>
<div class="level2">
<pre class="code">  Data oriented design is an approach that extracts the operations on the data from the “objects” and flattens the things that they need to run in order to be cache friendly. According to the literature (I got my first exposure in Game Engine Gems 2, Chapter 15), in many cases it actually simplifies the code.</pre>

<p>
———————————————
From atomix ‘s overview:
—————————–
Data oriented architecture is focus in Data arrangement and process(delay of data and the dataflow) and everything is Data, with a repository! It have more aspects than Data driven architecture and not talking about “the force of generative data”.
</p>

<p>
In hardware level, data oriented appear in structure and operations of chip set, when input and output are carefullly design to get batch/cache efficient.
</p>

<p>
In software level, programming language such as Java:
Data oriented architecture appear as we save everything in a big repository (database… or file repository) then retrive it to do operations. Important note, the consideration that everything is Data is very important. We can load everything as data, code, configs, signal from network, service… Second the existence of the repository is also important, as it the premise of other concept about ports, dataflow, stream, event, process, monitoring etc…
</p>

<p>
Compare to service oriented, it care more about the delay of data and the dataflow, not the operation.
Compare to object oriented, it just only have the data concept, not object, instance or what ever…
</p>

<p>
Data oriented architecture usually envolve every generic way to descible data, common via XML. They also usually use a data oriented architecture as the base of other.
As seen in hardware level, the signal in send in CPU as the repository, via ports, in a stream, trigger interrupt as Event,…
The same in a software level system, in Java world such as Oracle’s Buisiness Process Management (BPM). They essentially use XML to describle everything and consider everything is Data, also have concept of Ports, Stream, Event, Process…
</p>

<p>
So normally Data oriented architecture go along with Data driven… but they are two different thing!
</p>

</div>
<!-- EDIT7 SECTION "Data oriented (design) architecture:" [3205-5441] -->
<h3 class="sectionedit8" id="why_so_much_people_in_java_world_get_this_wrong_at_first">Why so much people in java world get this wrong at first?</h3>
<div class="level3">

<p>
But of course Oracle solution are much more complex than a single chipset, as it also envolve EJB, SOAP… with also an candidate for “Data driven architecture”… That’s . But EJB and SOAP are essential pieces of BPM “Data oriented architecture”!!!
</p>

</div>
<!-- EDIT8 SECTION "Why so much people in java world get this wrong at first?" [5442-] -->
