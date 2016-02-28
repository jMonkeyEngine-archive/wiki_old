---
title: jME3 Headless Server
---
<h1 class="sectionedit1" id="jme3_headless_server">jME3 Headless Server</h1>
<div class="level1">

<p>
When adding multiplayer to your game, you may find that your server needs to know about game state (e.g. where are players, objects? Was that a direct hit? etc.) You can code all this up yourself, but there's an easier way. 
</p>

<p>
It's very easy to change your current (client) game to function as a server as well.
</p>

</div>
<!-- EDIT1 SECTION "jME3 Headless Server" [1-348] -->
<h2 class="sectionedit2" id="what_does_headless_mean">What Does Headless Mean?</h2>
<div class="level2">

<p>
A headless server…
</p>
<ul>
<li class="level1"><div class="li"> does not display any output – no window opens, no audio plays, no graphics are rendered.</div>
</li>
<li class="level1"><div class="li"> ignores all input – no input handling.</div>
</li>
<li class="level1"><div class="li"> keeps game state – you can attach to, transform, and save the rootNode, although the scene is not displayed.</div>
</li>
<li class="level1"><div class="li"> calls the <code>simpleUpdate()</code> loop – you can run tests and trigger events as usual.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "What Does Headless Mean?" [349-748] -->
<h2 class="sectionedit3" id="client_code">Client Code</h2>
<div class="level2">

<p>
First, let's take a look at the default way of creating a new game (in its simplest form):
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
  Application app <span class="sy0">=</span> <span class="kw1">new</span> Main<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Client Code" [749-975] -->
<h2 class="sectionedit4" id="headless_server_code">Headless Server Code</h2>
<div class="level2">

<p>
Now, with a simple change you can start your game in Headless mode. This means that all input and audio/visual output will be ignored. That's a good thing for a server.
</p>
<pre class="code java"><span class="kw1">import</span> <span class="co2">com.jme3.system.JmeContext</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.system.JmeContext.Type</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
  Application app <span class="sy0">=</span> <span class="kw1">new</span> Main<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  app.<span class="me1">start</span><span class="br0">(</span>JmeContext.<span class="me1">Type</span>.<span class="me1">Headless</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "Headless Server Code" [976-1390] -->
<h2 class="sectionedit5" id="next_steps">Next steps</h2>
<div class="level2">

<p>
Okay, so you can now start your game in a headless 'server mode', where to go from here?
</p>
<ul>
<li class="level1"><div class="li"> Parse <code>String[] args</code> from the <code>main</code>-method to enable server mode on demand (e.g. start your server like <code>java -jar mygame.jar –server</code>.</div>
</li>
<li class="level1"><div class="li"> Integrate <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">SpiderMonkey</a>, to provide game updates to the server over a network.</div>
</li>
<li class="level1"><div class="li"> Only execute code that's needed. (E.g. place all rendering code inside an <code>if (servermode)</code>-block) (or <code>if (!servermode)</code> for the client).</div>
</li>
<li class="level1"><div class="li"> Add decent <a href="/jme3/advanced/logging.html" class="wikilink1" title="jme3:advanced:logging">logging</a> so your server actually makes sense.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/server.html" class="wikilink1" title="tag:server" rel="tag">server</a>,
	<a href="/tag/spidermonkey.html" class="wikilink1" title="tag:spidermonkey" rel="tag">spidermonkey</a>,
	<a href="/tag/headless.html" class="wikilink1" title="tag:headless" rel="tag">headless</a>,
	<a href="/tag/network.html" class="wikilink1" title="tag:network" rel="tag">network</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT5 SECTION "Next steps" [1391-] -->
