---
title: LEARN GROOVY
---
<h2 class="sectionedit1" id="learn_groovy">LEARN GROOVY</h2>
<div class="level2">

</div>
<!-- EDIT1 SECTION "LEARN GROOVY" [1-24] -->
<h3 class="sectionedit2" id="syntax">Syntax</h3>
<div class="level3">

<p>
Groovy's syntax can be made far more compact than Java. For example, a declaration in Standard Java 5+ such as:
</p>
<pre class="code java"> <span class="kw1">for</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> it <span class="sy0">:</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> <span class="br0">{</span><span class="st0">"Rod"</span>, <span class="st0">"Carlos"</span>, <span class="st0">"Chris"</span><span class="br0">}</span><span class="br0">)</span>
     <span class="kw1">if</span> <span class="br0">(</span>it.<span class="me1">length</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&lt;=</span> <span class="nu0">4</span><span class="br0">)</span>
         <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span>it<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
can be expressed in Groovy as:
</p>
<pre class="code java"> <span class="br0">[</span><span class="st0">"Rod"</span>, <span class="st0">"Carlos"</span>, <span class="st0">"Chris"</span><span class="br0">]</span>.<span class="me1">findAll</span><span class="br0">{</span>it.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&lt;=</span> <span class="nu0">4</span><span class="br0">}</span>.<span class="me1">each</span><span class="br0">{</span>println it<span class="br0">}</span></pre>

<p>
What you see in the parentheses \{ \} is a magical <strong>Closure </strong> . What make Groovy so powerful compare to Java!
We will learn about it later.
</p>

</div>

<h4 id="official_syntax_description">Official syntax description</h4>
<div class="level4">

<p>
<a href="http://groovy.codehaus.org/For+those+new+to+both+Java+and+Groovy" class="urlextern" title="http://groovy.codehaus.org/For+those+new+to+both+Java+and+Groovy" rel="nofollow">http://groovy.codehaus.org/For+those+new+to+both+Java+and+Groovy</a>
</p>

<p>
<a href="http://groovy.codehaus.org/User+Guide" class="urlextern" title="http://groovy.codehaus.org/User+Guide" rel="nofollow">http://groovy.codehaus.org/User+Guide</a>
</p>

<p>
<a href="http://groovy.codehaus.org/Logical+Branching" class="urlextern" title="http://groovy.codehaus.org/Logical+Branching" rel="nofollow">http://groovy.codehaus.org/Logical+Branching</a>
</p>

<p>
<a href="http://groovy.codehaus.org/Looping" class="urlextern" title="http://groovy.codehaus.org/Looping" rel="nofollow">http://groovy.codehaus.org/Looping</a>
</p>

<p>
For your overview, I will introduce the most important syntax of the language:
</p>

</div>

<h4 id="logical_branching">Logical Branching</h4>
<div class="level4">

</div>

<h4 id="looping">Looping</h4>
<div class="level4">

</div>

<h4 id="operation">Operation</h4>
<div class="level4">

</div>
<!-- EDIT2 SECTION "Syntax" [25-919] -->
<h3 class="sectionedit3" id="highlight_language_features">Highlight language features</h3>
<div class="level3">

<p>
Beside with elegant syntax, Groovy has features you always wish that Java have, below paragraph will call out few features that actually help a lot in Game programming:
</p>

</div>

<h4 id="operation_overload">Operation overload</h4>
<div class="level4">

</div>

<h4 id="collections">Collections</h4>
<div class="level4">

</div>

<h4 id="reflection">Reflection</h4>
<div class="level4">

</div>
<!-- EDIT3 SECTION "Highlight language features" [920-1196] -->
<h3 class="sectionedit4" id="closure">Closure</h3>
<div class="level3">

<p>
Read more about it here:
</p>

<p>
<a href="http://groovy.codehaus.org/Closures" class="urlextern" title="http://groovy.codehaus.org/Closures" rel="nofollow">http://groovy.codehaus.org/Closures</a>
<a href="http://groovy.codehaus.org/Closures+-+Informal+Guide" class="urlextern" title="http://groovy.codehaus.org/Closures+-+Informal+Guide" rel="nofollow">http://groovy.codehaus.org/Closures+-+Informal+Guide</a>
<a href="http://groovy.codehaus.org/Closures+-+Formal+Definition" class="urlextern" title="http://groovy.codehaus.org/Closures+-+Formal+Definition" rel="nofollow">http://groovy.codehaus.org/Closures+-+Formal+Definition</a>
</p>

<p>
What is a <strong>Closure</strong>?
</p>

<p>
A Groovy Closure is like a “code block” or a method pointer. It is a piece of code that is defined and then executed at a later point. It has some special properties like implicit variables, support for currying and support for free variables (which we'll see later on). We'll ignore the nitty gritty details for now (see the formal definition if you want those) and look at some simple examples.
Simple Example
</p>
<pre class="code java">def clos <span class="sy0">=</span> <span class="br0">{</span> println <span class="st0">"hello!"</span> <span class="br0">}</span>
 
println <span class="st0">"Executing the Closure:"</span>
clos<span class="br0">(</span><span class="br0">)</span>                          <span class="co1">//prints "hello!"</span></pre>

<p>
Note that in the above example, “hello!” is printed when the Closure is called, not when it is defined.
</p>

</div>
<!-- EDIT4 SECTION "Closure" [1197-2063] -->
<h3 class="sectionedit5" id="and_gotchas">and Gotchas</h3>
<div class="level3">

<p>
<a href="http://groovy.codehaus.org/Differences+from+Java" class="urlextern" title="http://groovy.codehaus.org/Differences+from+Java" rel="nofollow">http://groovy.codehaus.org/Differences+from+Java</a>
</p>

</div>
<!-- EDIT5 SECTION "and Gotchas" [2064-2133] -->
<h3 class="sectionedit6" id="meta-programming">Meta-programming</h3>
<div class="level3">

<p>
Here come the Good! For those who remember the power of JavaScript’s prototype keyword, you can do them same with Groovy. For those who don’t even know what JavaScript is, Meta-programming is the way to expand the class with methods and attributes on the fly. 
</p>

</div>
<!-- EDIT6 SECTION "Meta-programming" [2134-2424] -->
<h3 class="sectionedit7" id="groovy_builder_swingbuilder">Groovy Builder – SwingBuilder</h3>
<div class="level3">

<p>
Groovy use a lot power the of Builder pattern.
</p>

<p>
In the snippets below I will show you write a few builders to speed up your JME code. The full list of Builder come in Part3 and 4.
</p>

</div>
<!-- EDIT7 SECTION "Groovy Builder – SwingBuilder" [2425-2645] -->
<h3 class="sectionedit8" id="language_comperation">Language comperation</h3>
<div class="level3">

</div>

<h4 id="javascript_comperation">JavaScript comperation</h4>
<div class="level4">

</div>
<!-- EDIT8 SECTION "Language comperation" [2646-] -->
