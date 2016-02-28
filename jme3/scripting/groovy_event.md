---
title: Event - Trigger - Manager
---
<h2 class="sectionedit1" id="event_-_trigger_-_manager">Event - Trigger - Manager</h2>
<div class="level2">

<p>
Event , Trigger , Manager are the 3 most important terms in game programming and scripting that worth to mention in the first place!
</p>

</div>
<!-- EDIT1 SECTION "Event - Trigger - Manager" [1-169] -->
<h3 class="sectionedit2" id="event">Event</h3>
<div class="level3">

<p>
Event is the core element (concept) and the unit of the Messaging System. When components in the game world communicate with each other through pipelines, Messages from one object need to be sent to other objects should also aware of it (to nofity) when some thing happen that. It's called an event; and inside of the event contain piece of imformations that describe the Message.
</p>

<p>
If Scripting, Event play important role too. It's almost shown up in EventHook to the cycle as: onInit, onUpdate, onClick.. It also provide ad-hoc communicate which in turn enable additional complex and flexible usage to existed systems. We will go deep into its usages later.
</p>

</div>

<h4 id="eventbus">EventBus</h4>
<div class="level4">

<p>
Event paradigm is implemented differently in every software that require it, to fit with the specific requirements. Recently we (Java world) have something quite generic that suite for wide range of cases and use intuitive methods to program. It's called EventBus. And fortunately , EventBus fit very well with Groovy scripting solution (kudos!)
</p>

<p>
…and few Event concepts Explained!
</p>

<p>
<a href="http://code.google.com/p/guava-libraries/wiki/EventBusExplained" class="urlextern" title="http://code.google.com/p/guava-libraries/wiki/EventBusExplained" rel="nofollow">http://code.google.com/p/guava-libraries/wiki/EventBusExplained</a>
</p>

<p>
<a href="http://codingjunkie.net/guava-eventbus/" class="urlextern" title="http://codingjunkie.net/guava-eventbus/" rel="nofollow">http://codingjunkie.net/guava-eventbus/</a>
</p>

</div>

<h4 id="groovy_eventbus_helloworld">Groovy Eventbus HelloWorld</h4>
<div class="level4">
<pre class="code java"><span class="kw1">import</span> <span class="co2">com.google.common.eventbus.EventBus</span>
<span class="kw1">import</span> <span class="co2">com.google.common.eventbus.Subscribe</span>
 
EventBus eventBus <span class="sy0">=</span> <span class="kw1">new</span> EventBus<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">class</span> EventHandler<span class="br0">{</span>
    @Subscribe
    <span class="kw1">public</span> <span class="kw4">void</span> hello<span class="br0">(</span>CustomEvent event<span class="br0">)</span><span class="br0">{</span>
        println <span class="st0">"Hello world"</span>
    <span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw1">class</span> CustomEvent<span class="br0">{</span>
 
<span class="br0">}</span>
handler <span class="sy0">=</span> <span class="kw1">new</span> EventHandler<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
eventBus.<span class="me1">register</span><span class="br0">(</span>handler<span class="br0">)</span><span class="sy0">;</span>
 
eventBus.<span class="me1">post</span><span class="br0">(</span><span class="kw1">new</span> CustomEvent<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
In this example,
</p>

<p>
Here, EventBus will play the communicate media in our Groovy scripting solution.
</p>

</div>

<h4 id="hooks">Hooks</h4>
<div class="level4">

</div>
<!-- EDIT2 SECTION "Event" [170-1876] -->
<h3 class="sectionedit3" id="trigger">Trigger</h3>
<div class="level3">

<p>
If you build up your game world's activites from Action, Trigger is the brick to build Gameplay. It's the combination of : Event + Condition → Action 
</p>

<p>
The concept of trigger can be describle like this: When an Event happen, if it's passed a Condition check, the Action is taken. A more detailed description envolve: the Enviroment - a specific Context of those 3 (E - C - A), Durations , Threaded or not, Executor … But here we concern the most simple form, the Context is the single specific that procedure the Event and its Global awareness.
</p>

<p>
In Groovy,
</p>
<ul>
<li class="level1"><div class="li"> Event is Class based, mentioned in the chapter above.</div>
</li>
<li class="level1"><div class="li"> Condition can be modeled with a Closure </div>
</li>
<li class="level1"><div class="li"> Action also very suitable with a Closure representation.</div>
</li>
</ul>

</div>

<h5 id="example1">Example1:</h5>
<div class="level5">
<pre class="code java">Example1<span class="sy0">:</span></pre>

</div>

<h5 id="example2">Example2:</h5>
<div class="level5">
<pre class="code java">Example2<span class="sy0">:</span></pre>

</div>
<!-- EDIT3 SECTION "Trigger" [1877-2707] -->
<h3 class="sectionedit4" id="manager">Manager</h3>
<div class="level3">

<p>
Manager is the concept of who have responsibities and power over others (as its children or employee in the real world), essentially it is a list of its children, and have basic opertions like add,remove to manage that list… You can also think about it as the Control of the MVC paradigm where it is the mediator between Model and View. In JME3, you see Manager every where such as AssetManager, StateManager as the wraper of underlying functions. So, event mixed up quite a lot concepts at once, Manager in Scripting is extremely useful and fullfill the missing piece of the picture we are painting for a while here.
</p>

<p>
To clean the mist of confusion about mixed of concepts a little bit, there are some practical wisdoms about Manager implementation:
</p>
<ul>
<li class="level1"><div class="li"> Manager acts globally, handy: usually a Singleton, or really easy to reference in script</div>
</li>
<li class="level2"><div class="li"> Manager wrap underlying details in intuitive way</div>
</li>
<li class="level2"><div class="li"> Manager share common informations</div>
</li>
<li class="level2"><div class="li"> Manager executions are frequently : like in an default update cycle</div>
</li>
<li class="level2"><div class="li"> Manager have power over its children : its handle it children; in almost scenarios child has left its Manager's list come hollow (as null)</div>
</li>
</ul>

<p>
All the concepts and wisdoms is describes much more detail in Atom framework Design <a href="/jme3/advanced/atom_framework/design.html" class="wikilink1" title="jme3:advanced:atom_framework:design"> Game architecture &amp; Design</a>
</p>

</div>
<!-- EDIT4 SECTION "Manager" [2708-4039] -->
<h3 class="sectionedit5" id="gquery">GQuery</h3>
<div class="level3">

<p>
GQuery stand for “JQuery like in Groovy”. JQuery is a famous framework in the JavaScript and Web world. GQuery try to provide some of its features, immtimate its syntax and sugars, leverage by Groovy:
</p>
<ul>
<li class="level1"><div class="li"> Query, select a Node Tree (like <abbr title="HyperText Markup Language">HTML</abbr>, Nifty elements,…) with a minimal Path syntax , same as XPath</div>
</li>
<li class="level1"><div class="li"> Hooks to Node's (components, elements..) events with Eventbus</div>
</li>
</ul>

<p>
GQuery is a part of my additions for NiftyGUI, others are:
</p>
<ul>
<li class="level1"><div class="li"> a Groovy builder</div>
</li>
<li class="level1"><div class="li"> a <abbr title="Cascading Style Sheets">CSS</abbr> (Cascaded Style Sheet) implementation (for NiftyGUI), even a LESS</div>
</li>
<li class="level1"><div class="li"> a simplier Localization framework</div>
</li>
<li class="level1"><div class="li"> a lot of scripting and functional sugar for NiftyGUI</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "GQuery" [4040-] -->
