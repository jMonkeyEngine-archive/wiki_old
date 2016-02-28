---
title: Main Update Loop
---
<h1 class="sectionedit1" id="main_update_loop">Main Update Loop</h1>
<div class="level1">

<p>
Extending your application from com.jme3.app.<a href="/jme3/intermediate/simpleapplication.html" class="wikilink1" title="jme3:intermediate:simpleapplication">SimpleApplication</a> provides you with an update loop. This is where you implement your game logic (game mechanics).
</p>

<p>
Some usage examples: Here you remote-control NPCs (computer controlled characters), generate game events, and respond to user input.
</p>

<p>
To let you see the main update loop in context, understand that the SimpleApplication does the following:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Initialization</strong> – Execute <code>simpleInitApp()</code> method once.</div>
</li>
<li class="level1"><div class="li"> <strong>Main Update Loop</strong></div>
<ol>
<li class="level2"><div class="li"> Input listeners respond to mouse clicks and keyboard presses – <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">Input handling</a> </div>
</li>
<li class="level2"><div class="li"> Update game state:</div>
<ol>
<li class="level3"><div class="li"> Update overall game state – Execute <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a></div>
</li>
<li class="level3"><div class="li"> User code update – Execute <code>simpleUpdate()</code> method</div>
</li>
<li class="level3"><div class="li"> Logical update of entities – Execute <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a></div>
</li>
</ol>
</li>
<li class="level2"><div class="li"> Render audio and video</div>
<ol>
<li class="level3"><div class="li"> <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a> rendering.</div>
</li>
<li class="level3"><div class="li"> Scene rendering.</div>
</li>
<li class="level3"><div class="li"> User code rendering – Execute <code>simpleRender()</code> method.</div>
</li>
</ol>
</li>
<li class="level2"><div class="li"> Repeat loop.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> <strong>Quit</strong> – If user requests <code>exit()</code>, execute <code>cleanup()</code> and <code>destroy()</code>. <br />
The jME window closes and the loop ends.</div>
</li>
</ul>

</div>
<!-- EDIT1 SECTION "Main Update Loop" [1-1170] -->
<h2 class="sectionedit2" id="usage">Usage</h2>
<div class="level2">

<p>
In a trivial <a href="/jme3/intermediate/simpleapplication.html" class="wikilink1" title="jme3:intermediate:simpleapplication">SimpleApplication</a> (such as a <a href="/jme3/beginner.html" class="wikilink1" title="jme3:beginner">Hello World tutorial</a>), all code is either in the <code>simpleInitApp()</code> (initialization) or <code>simpleUpdate()</code> (behaviour) method – or in a helper method/class that is called from one of these two. This trivial approach will make your main class very long, hard to read, and hard to maintain. You don't need to load the whole scene at once, and you don't need to run all conditionals tests all the time.
</p>

<p>
It's a best practice to modularize your game mechanics and spread out initialization and update loop code over several Java objects:
</p>
<ul>
<li class="level1"><div class="li"> Move modular code blocks from the <code>simpleInitApp()</code> method into <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a>. Attach AppStates to initialize custom subsets of “one dungeon”, and detach it when the player exits this “dungeon”. <br />
Examples: Weather/sky audio and visuals, physics collision shapes, sub-rootnodes of individual dungeons including dungeon NPCs, etc.</div>
</li>
<li class="level1"><div class="li"> Move modular code blocks from the <code>simpleUpdate()</code> method into the update loops of <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a> to control individual entity behavior (NPCs), and into the update method of <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a> to control world events. <br />
Examples: Weather behaviour, light behaviour, physics behaviour, individual NPC behaviour, trap behaviour, etc.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/basegame.html" class="wikilink1" title="tag:basegame" rel="tag">basegame</a>,
	<a href="/tag/control.html" class="wikilink1" title="tag:control" rel="tag">control</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/init.html" class="wikilink1" title="tag:init" rel="tag">init</a>,
	<a href="/tag/keyinput.html" class="wikilink1" title="tag:keyinput" rel="tag">keyinput</a>,
	<a href="/tag/loop.html" class="wikilink1" title="tag:loop" rel="tag">loop</a>,
	<a href="/tag/states.html" class="wikilink1" title="tag:states" rel="tag">states</a>,
	<a href="/tag/state.html" class="wikilink1" title="tag:state" rel="tag">state</a>
</span></div>

</div>
<!-- EDIT2 SECTION "Usage" [1171-] -->
