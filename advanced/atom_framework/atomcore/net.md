---
title: Atom Core Network framework
---
<h2 class="sectionedit1" id="atom_core_network_framework">Atom Core Network framework</h2>
<div class="level2">

<p>
<strong>Atom Core Network framework is for networked game developing in Java. Powered by JME3, SpiderMonkey, MirrorMonkey and Netty.</strong>
</p>

</div>
<!-- EDIT1 SECTION "Atom Core Network framework" [1-169] -->
<h3 class="sectionedit2" id="introduction">Introduction</h3>
<div class="level3">

<p>
To make developing networked game (multiplayer, social, even MMO..) in JME3 much more easier! With Java, with tools, with monitors!
</p>

<p>
This module depends in JME3, SpiderMonkey, MirrorMonkey and Netty. It has all the features that libries it depends on have with ultimate extra power!!
</p>

<p>
You can include Optional modules like Kryo (Kryonet), ProtocolBuffer, Zay-ES which is official extensions for various of usecaces.
</p>

</div>
<!-- EDIT2 SECTION "Introduction" [170-608] -->
<h3 class="sectionedit3" id="features">Features</h3>
<div class="level3">

</div>
<!-- EDIT3 SECTION "Features" [609-628] -->
<h3 class="sectionedit4" id="concepts_papers">Concepts &amp; Papers</h3>
<div class="level3">

<p>
<iframe title="" src="https://docs.google.com/presentation/d/1YxUR8fCc115rkokROZb3GVq1J1vRGnGSlwlu6Q_SB48/embed?start=false&amp;loop=false&amp;delayms=3000" style="width:100%; height:600px"></iframe>
</p>
<ul>
<li class="level1"><div class="li"> Annotations: @Data, @Event, @Sync</div>
</li>
<li class="level1"><div class="li"> Interfaces: Hanler, Fiber, Filter</div>
</li>
<li class="level1"><div class="li"> Ultilities: NetworkType, NetworkService, NetworkBus</div>
</li>
<li class="level1"><div class="li"> Configurations: zero, override via XML, Groovy</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Concepts & Papers" [629-986] -->
<h3 class="sectionedit5" id="quick_look">Quick look</h3>
<div class="level3">

</div>

<h4 id="a_simple_network_application">A simple network application</h4>
<div class="level4">
<pre class="code java"><span class="kw1">class</span> Client implement NetworkService<span class="br0">{</span>
     DObject dobj<span class="sy0">;</span>
 
     <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
         network.<span class="me1">mirror</span><span class="br0">(</span>dobj<span class="br0">)</span><span class="sy0">;</span>
     <span class="br0">}</span>
 
     <span class="kw1">public</span> <span class="kw4">void</span> response<span class="br0">(</span>NetworkService service<span class="br0">)</span><span class="br0">{</span>
         dobj.<span class="me1">mirror</span><span class="br0">(</span>service<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>
<pre class="code java"><span class="kw1">class</span> Server implement NetworkService<span class="br0">{</span>
     DObject dobj<span class="sy0">;</span>
 
     <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
          dobj.<span class="me1">change</span><span class="br0">(</span><span class="br0">)</span>
          network.<span class="me1">in</span><span class="br0">(</span>client1,client2<span class="br0">)</span>.<span class="me1">mirror</span><span class="br0">(</span>dobj<span class="br0">)</span>
    <span class="br0">}</span>
 
     <span class="kw1">public</span> <span class="kw4">void</span> response<span class="br0">(</span>NetworkService service<span class="br0">)</span><span class="br0">{</span>
         dobj.<span class="me1">mirror</span><span class="br0">(</span>service<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "Quick look" [987-1561] -->
<h3 class="sectionedit6" id="under_the_curtain">Under the curtain</h3>
<div class="level3">

</div>

<h4 id="dependencies">Dependencies</h4>
<div class="level4">

</div>

<h4 id="networktype">NetworkType</h4>
<div class="level4">

</div>

<h4 id="networkservice">NetworkService</h4>
<div class="level4">

</div>

<h4 id="networkbus">NetworkBus</h4>
<div class="level4">

</div>
<!-- EDIT6 SECTION "Under the curtain" [1562-1678] -->
<h2 class="sectionedit7" id="examples">Examples</h2>
<div class="level2">

<p>
Some examples 
</p>

</div>
<!-- EDIT7 SECTION "Examples" [1679-1714] -->
<h2 class="sectionedit8" id="documentation">Documentation</h2>
<div class="level2">

</div>
<!-- EDIT8 SECTION "Documentation" [1715-1740] -->
<h3 class="sectionedit9" id="basic_games_networking">Basic games networking</h3>
<div class="level3">

<p>
<a href="http://gafferongames.com/networking-for-game-programmers/" class="urlextern" title="http://gafferongames.com/networking-for-game-programmers/" rel="nofollow">http://gafferongames.com/networking-for-game-programmers/</a>
</p>

<p>
<a href="https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking" class="urlextern" title="https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking" rel="nofollow">https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking</a>
</p>

</div>
<!-- EDIT9 SECTION "Basic games networking" [1741-1903] -->
<h3 class="sectionedit10" id="programming">Programming</h3>
<div class="level3">

</div>
<!-- EDIT10 SECTION "Programming" [1904-1925] -->
<h3 class="sectionedit11" id="workflows">Workflows</h3>
<div class="level3">

</div>

<h4 id="tools">Tools</h4>
<div class="level4">

</div>
<!-- EDIT11 SECTION "Workflows" [1926-] -->
