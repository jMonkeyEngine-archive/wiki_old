---
title: AtomAI
---
<h2 class="sectionedit1" id="atomai">AtomAI</h2>
<div class="level2">

<p>
AtomAI is an innovative framework for doing AI for simulations and interactive applications, focus in Games!
</p>

</div>
<!-- EDIT1 SECTION "AtomAI" [1-128] -->
<h3 class="sectionedit2" id="technologies">Technologies</h3>
<div class="level3">

<p>
AtomAI built up by bleeding-edge of AI technologies based in lastest researches. Underlying, it depends in extensible framework to leverage maximum Java language in spirit of Atom framework.
</p>

<p>
Many parts of AtomAI are very innovative and actually release the developer from low level concerning and save a lot of time redo common usecases implementations; without errors.
</p>

</div>
<!-- EDIT2 SECTION "Technologies" [129-520] -->
<h3 class="sectionedit3" id="dependencies">Dependencies</h3>
<div class="level3">

<p>
AtomAI depend a lot in good AI opensource projects
</p>

</div>

<h4 id="java_datastructures_mechanisms">Java DataStructures &amp; Mechanisms</h4>
<div class="level4">

</div>

<h5 id="javolution">Javolution</h5>
<div class="level5">

<p>
<a href="http://javolution.org/" class="urlextern" title="http://javolution.org/" rel="nofollow">http://javolution.org/</a>
</p>
<pre class="code"> Because real-time programming requires a time-predictable standard library. Javolution real-time goals are simple: To make your application faster and more time predictable!</pre>

<p>
Javolution solve some fundamental real-time problems with innovative technologies. Javolution is one of core dependencies of AtomCore and so AtomAI. 
</p>

</div>

<h5 id="guava_guice">Guava &amp; Guice</h5>
<div class="level5">

<p>
Two google opensource projects that make Java developer's life easier.
</p>

</div>

<h5 id="apache_commons">Apache Commons</h5>
<div class="level5">

<p>
Lang
</p>

<p>
BeanUtils 
</p>

<p>
Math
</p>

<p>
Logging
</p>

<p>
</p><p></p><div class="notetip">Javolution, Guava, Guice, Commons Lang, BeanUtils, Math, Logging are a complete sets of libraries for Real-time applications with testable, logable capacities, fullfill each other and has just a little bit overlaps. You can setup them easily via Maven or gradle with JME3.
</div>


</div>

<h5 id="xxl">XXL</h5>
<div class="level5">

<p>
<a href="http://code.google.com/p/xxl/" class="urlextern" title="http://code.google.com/p/xxl/" rel="nofollow">http://code.google.com/p/xxl/</a>
</p>
<pre class="code"> XXL is a Java library that contains a rich infrastructure for implementing advanced query processing functionality. The library offers low-level components like access to raw disks as well as high-level ones like a query optimizer. On the intermediate levels, XXL provides a demand-driven cursor algebra, a framework for indexing and a powerful package for supporting aggregation.</pre>

<p>
XXL already solved a lot of problems in spatial, relational and metadata… Upon that base, AtomAI focus in higher level of abstraction like Graph, State, Tree; Flow, Stream, Load balance;  later focus more in AI stuffs without worry about lower levels.
</p>

</div>

<h5 id="qi4j">Qi4j</h5>
<div class="level5">

<p>
<a href="http://qi4j.org/" class="urlextern" title="http://qi4j.org/" rel="nofollow">http://qi4j.org/</a>
</p>
<pre class="code"> is a framework for domain centric application development, including evolved concepts from Aspect Oriented Programming, Dependency Injection and Domain Driven Design.</pre>
<pre class="code"> Qi4j™ is an implementation of Composite Oriented Programming, using the standard Java platform, without the use of any pre-processors or new language elements. Everything you know from Java still applies and you can leverage both your experience and toolkits to become more productive with Composite Oriented Programming today.</pre>

<p>
Qi4j offers a way to config the system by layers and entities. More over, Entity-Composite (with relasionship enable) compare to Entity-components is a better way to compose things.
</p>

</div>

<h5 id="rxjava">RxJava</h5>
<div class="level5">

<p>
<a href="https://github.com/Netflix/RxJava" class="urlextern" title="https://github.com/Netflix/RxJava" rel="nofollow">https://github.com/Netflix/RxJava</a>
</p>
<pre class="code"> Reactive Extensions for the JVM – a library for composing asynchronous and event-based programs using observable sequences for the Java VM.</pre>

<p>
RxJava already provided mechanisms for composing asynchronous and event-based programs. AtomAI then focus in design the flows of events of agents. This is a win-win scenario for boths.
</p>

</div>

<h4 id="scripting">Scripting</h4>
<div class="level4">

</div>

<h5 id="groovy">Groovy</h5>
<div class="level5">

<p>
Groovy leverage Java in a very elegent way. Make itself the most valid candidate to being a scripting language for Java and AtomAI to construct a very flexible framework. AtomAI also provide better mechanisms to automatic tasks and tools, give developer more power in editing scripts and actions.
</p>

</div>

<h4 id="ai_model_and_source_structure">AI Model and source structure</h4>
<div class="level4">

</div>

<h5 id="aima">AIMA</h5>
<div class="level5">

<p>
<a href="http://code.google.com/p/aima-java/" class="urlextern" title="http://code.google.com/p/aima-java/" rel="nofollow">http://code.google.com/p/aima-java/</a>
</p>
<pre class="code"> Java implementation of algorithms from Norvig and Russell's Artificial Intelligence - A Modern Approach 3rd Edition
 </pre>

<p>
is de-facto for AI techs. AtomAI <strong>modify</strong> and <strong>add implementations</strong> to AIMA-java that intergrate deeply with above technologies, make AIMA the most complete, powerful and open java AI framework.
</p>

</div>

<h5 id="choco">Choco</h5>
<div class="level5">

<p>
<a href="https://github.com/chocoteam/choco3" class="urlextern" title="https://github.com/chocoteam/choco3" rel="nofollow">https://github.com/chocoteam/choco3</a>
</p>
<pre class="code">  Choco3 is an open-source Java library for Constraint Programming. 
  Choco3 comes with:</pre>
<pre class="code">  various type of variables (integer, boolean, set, graph and real),
  various state-of-the-art constraints (alldifferent, count, nvalues, etc.),
  various search strategies, from basic ones (first_fail, smallest, etc.) to most complex (impact-based and activity-based search),
  explanation-based engine, that enables conflict-based back jumping, dynamic backtracking and path repair</pre>

</div>
<!-- EDIT3 SECTION "Dependencies" [521-] -->
