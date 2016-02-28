---
title: Atom Configurations
---
<h2 class="sectionedit1" id="atom_configurations">Atom Configurations</h2>
<div class="level2">

<p>
Atom Configurations provide facilities for do configurations and profiles for enviroments, Games of course instead of just normal Java applications.
</p>

</div>
<!-- EDIT1 SECTION "Atom Configurations" [1-182] -->
<h3 class="sectionedit2" id="the_past">The past</h3>
<div class="level3">

<p>
First let's take a look into the past of years and see how Java developers do configurations for their applications: 
</p>
<ul>
<li class="level1"><div class="li"> The config files for application in desktop enviroments may loaded from user's home, or the app's folder. The config files can be plain text, XML, JSON, binary or something else.</div>
</li>
<li class="level1"><div class="li"> The config can also be received from external sources like from network services, database. The protocol for them can be object base (POJO), relational structure based (resultset) or else …</div>
</li>
<li class="level1"><div class="li"> The config can also be intelligently procedure based in the stats and infos of the device or deployed enviroment…</div>
</li>
</ul>

<p>
So there is not a single way to do configurations. Is there an unified way now?
The answer is still NO. Configurations is the aspect of gamedev SHOULD be kept flexible the most. Tricks and smart stuffs can involve in this progress a lot: optimizations, per device &amp; per user configuration, policies… In another hand, it keep you busy with tricky parts and complexibilities of underlying datastructure and extra progress.
</p>

<p>
Some other libraries and game engine tend to hide the detail from developer and provide a premade solutions for configurations in supported enviroment. 
</p>

<p>
Ex: LibGDX with Prefs, Unity with Metadata, XNA with Properties…
</p>

<p>
The more configurations apart from Data and Code, the more it getting complex. In the other hand, getting closer, it mixed and tangled with Data and Code. So how can we make it the right way?
</p>

</div>
<!-- EDIT2 SECTION "The past" [183-1659] -->
<h3 class="sectionedit3" id="the_solutions">The solutions</h3>
<div class="level3">

<p>
The Solution is actually very practical as it should. It's the corporation of existed techniques but with a fine-tuned and industrial approaches. The “Fine tuning” are predefined or customized by the user them self (if they know how to do it). Isn't it what is configurations is all about. Think about a ridiculous control panel which have only one button, and the other complex and also not very useful with 300 of them… This framework is your control panel, tailored by you! What it help:
</p>
<ol>
<li class="level1"><div class="li"> There are “fine-tuned” configurations for enviroments , devices, users, or aspects… and custom configurations for arbitrary scope and context.</div>
</li>
<li class="level1"><div class="li"> Abstract out the data structure of configurations and its lower level of persist, load and communications.</div>
</li>
<li class="level1"><div class="li"> Revolution in the publish, deloy enviroment and progress: to make the configuration actually is data (and code…), not something else.</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "The solutions" [1660-2578] -->
<h3 class="sectionedit4" id="technologies">Technologies</h3>
<div class="level3">
<ol>
<li class="level1"><div class="li"> AtomEx's Universe provide a repository of configuration profiles. Concepts and mechanisms of Atom's Universe is the similar to Maven repository. So Java dev can use Maven or Gradle to include them at development time (or even runtime). In runtime, an IOC mechanism is provide for configurations initialization similar to Spring system.</div>
</li>
<li class="level1"><div class="li"> Apache Commons &amp; Archaius to abstract out the data structure of configurations. Under them are Utils that consider appliance of configurations as watchable Tasks.</div>
</li>
<li class="level1"><div class="li"> Gradle and Go is employed in the deploy progress make it very flexible and watchable. Configuration publishing is supported by tailored <abbr title="Graphical User Interface">GUI</abbr> Editors in JMP. Generic configuration editors for Text, Properties, XML, JSON… are also provided.</div>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "Technologies" [2579-3353] -->
<h2 class="sectionedit5" id="toolset">Toolset</h2>
<div class="level2">

</div>
<!-- EDIT5 SECTION "Toolset" [3354-3373] -->
<h2 class="sectionedit6" id="documentation">Documentation</h2>
<div class="level2">

</div>
<!-- EDIT6 SECTION "Documentation" [3374-] -->
