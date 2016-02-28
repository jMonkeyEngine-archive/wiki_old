---
title: Combo Moves
---
<h1 class="sectionedit1" id="combo_moves">Combo Moves</h1>
<div class="level1">

<p>
The ComboMoves class allows you to define combinations of inputs that trigger special actions. Entering an input combo correctly can bring the player incremental rewards, such as an increased chance to hit, an increased effectiveness, or decreased change of being blocked, whatever the game designer chooses. <a href="http://en.wikipedia.org/wiki/Combo_%28video_gaming%29" class="urlextern" title="http://en.wikipedia.org/wiki/Combo_%28video_gaming%29" rel="nofollow">More background info</a>
</p>

<p>
Combos are usually a series of inputs, in a fixed order: For example a keyboard combo can look  like: “press Down, then Down+Right together, then Right”. 
</p>

<p>
Usage:
</p>
<ol>
<li class="level1"><div class="li"> Create input triggers </div>
</li>
<li class="level1"><div class="li"> Define combos</div>
</li>
<li class="level1"><div class="li"> Detect combos in ActionListener </div>
</li>
<li class="level1"><div class="li"> Execute combos in update loop </div>
</li>
</ol>

<p>
Copy the two classes ComboMoveExecution.java and ComboMove.java into your application and adjust them to your package paths.
</p>

</div>
<!-- EDIT1 SECTION "Combo Moves" [1-824] -->
<h2 class="sectionedit2" id="example_code">Example Code</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/combomoves/TestComboMoves.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/combomoves/TestComboMoves.java" rel="nofollow">TestComboMoves.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/combomoves/ComboMoveExecution.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/combomoves/ComboMoveExecution.java" rel="nofollow">ComboMoveExecution.java</a> ← required</div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/combomoves/ComboMove.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/combomoves/ComboMove.java" rel="nofollow">ComboMove.java</a> ← required</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Example Code" [825-1321] -->
<h2 class="sectionedit3" id="create_input_triggers">Create Input Triggers</h2>
<div class="level2">

<p>
First you <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">define your game's inputs</a> as you usually do: Implement the com.jme3.input.controls.ActionListener interface for your class, and add triggers mappings such as com.jme3.input.controls.KeyTrigger and com.jme3.input.KeyInput. 
</p>

<p>
For example:
</p>
<pre class="code java">inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Left"</span>,    <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Right"</span>,   <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_RIGHT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Up"</span>,      <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_UP</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Down"</span>,    <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_DOWN</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Attack1"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">inputManager</span>.<span class="me1">addListener</span><span class="br0">(</span><span class="kw1">this</span>, <span class="st0">"Left"</span>, <span class="st0">"Right"</span>, <span class="st0">"Up"</span>, <span class="st0">"Down"</span>, <span class="st0">"Attack1"</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT3 SECTION "Create Input Triggers" [1322-2092] -->
<h2 class="sectionedit4" id="define_combos">Define Combos</h2>
<div class="level2">

<p>
For each of  your combo moves, you specify the series of inputs that will trigger it. The order in which you define them is the order the player has to press them for the step to be recorded. When all steps have been recorded, the combo is triggered. 
</p>

<p>
The following example shows how a fireball combo move is triggered by pressing the navigation keys for “down, down+right, right”, in this order.
</p>
<pre class="code java">ComboMove fireball <span class="sy0">=</span> <span class="kw1">new</span> ComboMove<span class="br0">(</span><span class="st0">"Fireball"</span><span class="br0">)</span><span class="sy0">;</span>
fireball.<span class="me1">press</span><span class="br0">(</span><span class="st0">"Down"</span><span class="br0">)</span>.<span class="me1">notPress</span><span class="br0">(</span><span class="st0">"Right"</span><span class="br0">)</span>.<span class="me1">done</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
fireball.<span class="me1">press</span><span class="br0">(</span><span class="st0">"Right"</span>, <span class="st0">"Down"</span><span class="br0">)</span>.<span class="me1">done</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
fireball.<span class="me1">press</span><span class="br0">(</span><span class="st0">"Right"</span><span class="br0">)</span>.<span class="me1">notPress</span><span class="br0">(</span><span class="st0">"Down"</span><span class="br0">)</span>.<span class="me1">done</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
fireball.<span class="me1">notPress</span><span class="br0">(</span><span class="st0">"Right"</span>, <span class="st0">"Down"</span><span class="br0">)</span>.<span class="me1">done</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
fireball.<span class="me1">setUseFinalState</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Also create a ComboMoveExecution object for each ComboMove. You need it later to execute the detected combo.
</p>
<pre class="code java">ComboMoveExecution fireballExec <span class="sy0">=</span> <span class="kw1">new</span> ComboMoveExecution<span class="br0">(</span>fireball<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Define Combos" [2093-3001] -->
<h3 class="sectionedit5" id="combomove_class_methods">ComboMove Class Methods</h3>
<div class="level3">

<p>
Use the following ComboMove methods to specify the combo:
</p>
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">ComboMove Method</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">press(“A”).done(); <br />
press(“A”,“B”).done();</td><td class="col1">Combo step is recorded if A is entered. <br />
Combo step is recorded if A and B are entered simultaneously.</td>
	</tr>
	<tr class="row2">
		<td class="col0">notPress(“A”).done(); <br />
notPress(“A”,“B”).done();</td><td class="col1">Combo step is recorded if A is released. <br />
Combo step is recorded if A and B are both released.</td>
	</tr>
	<tr class="row3">
		<td class="col0">press(“A”).notPress(“B”).done();</td><td class="col1">Combo step is recorded if A is entered, and not B</td>
	</tr>
	<tr class="row4">
		<td class="col0">press(“A”).notPress(“B”).timeElapsed(0.11f).done();</td><td class="col1">Combo step is recorded a certain time after A and not B is entered. <br />
etc, etc …</td>
	</tr>
	<tr class="row5">
		<td class="col0">setPriority(0.5f);</td><td class="col1">If there is an ambiguity, a high-priority combo will trigger instead of a low-priority combo. This prevents that a similar looking combo step “hijacks” another Combo. Use only once per ComboMove.</td>
	</tr>
	<tr class="row6">
		<td class="col0">setUseFinalState(false); <br />
setUseFinalState(true);</td><td class="col1">This is the final command of the series. <br />
False: Do not wait on a final state, chain combo steps. (?) <br />
True: This is the final state, do not chain combo steps. (?)</td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [3096-4090] -->
<p>
The <code>press()</code> and <code>notPress()</code> methods accept sets of Input Triggers, e.g. <code>fireball.press(“A”,“B”,“C”).done()</code>.
</p>

<p>
The following getters give you more information about the game state:
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">ComboMove Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">getCastTime()</td><td class="col1">Returns the time since the last step has been recorded. (?)</td>
	</tr>
	<tr class="row2">
		<td class="col0">getMoveName()</td><td class="col1">Returns the string of the current combo</td>
	</tr>
	<tr class="row3">
		<td class="col0">getPriority()</td><td class="col1">Returns the priority of this move</td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [4283-4489] -->
</div>
<!-- EDIT5 SECTION "ComboMove Class Methods" [3002-4490] -->
<h2 class="sectionedit8" id="detect_combos_in_actionlistener">Detect Combos in ActionListener</h2>
<div class="level2">

<p>
Now that you have specified the combo steps, you want to detect them. You do that in the onAction() method that you get from the ActionListener interface.
</p>

<p>
Create a HashSet <code>pressMappings</code> to track curently pressed mappings, and a ComboMove object <code>currentMove</code> to track the current move. 
</p>

<p>
We also track the cast time of a combo to determine if it has timed out (see update loop below).
</p>
<pre class="code java"><span class="kw1">private</span> HashSet<span class="sy0">&lt;</span>String<span class="sy0">&gt;</span> pressedMappings <span class="sy0">=</span> <span class="kw1">new</span> HashSet<span class="sy0">&lt;</span>String<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">private</span> ComboMove currentMove <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">float</span> currentMoveCastTime <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">float</span> time <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
...
 
<span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> isPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// Record pressed mappings</span>
    <span class="kw1">if</span> <span class="br0">(</span>isPressed<span class="br0">)</span><span class="br0">{</span>
        pressedMappings.<span class="me1">add</span><span class="br0">(</span>name<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span><span class="kw1">else</span><span class="br0">{</span>
        pressedMappings.<span class="me1">remove</span><span class="br0">(</span>name<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">// The pressed mappings have changed: Update ComboExecution objects</span>
    List<span class="sy0">&lt;</span>ComboMove<span class="sy0">&gt;</span> invokedMoves <span class="sy0">=</span> <span class="kw1">new</span> ArrayList<span class="sy0">&lt;</span>ComboMove<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">if</span> <span class="br0">(</span>fireballExec.<span class="me1">updateState</span><span class="br0">(</span>pressedMappings, time<span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
        invokedMoves.<span class="me1">add</span><span class="br0">(</span>fireball<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="co1">// ... add more ComboExecs here...</span>
 
    <span class="co1">// If any ComboMoves have been sucessfully triggered:</span>
    <span class="kw1">if</span> <span class="br0">(</span>invokedMoves.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> <span class="nu0">0</span><span class="br0">)</span><span class="br0">{</span>
        <span class="co1">// identify the move with highest priority</span>
        <span class="kw4">float</span> priority <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
        ComboMove toExec <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="kw1">for</span> <span class="br0">(</span>ComboMove move <span class="sy0">:</span> invokedMoves<span class="br0">)</span><span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>move.<span class="me1">getPriority</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> priority<span class="br0">)</span><span class="br0">{</span>
                priority <span class="sy0">=</span> move.<span class="me1">getPriority</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                toExec <span class="sy0">=</span> move<span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>currentMove <span class="sy0">!=</span> <span class="kw2">null</span> <span class="sy0">&amp;&amp;</span> currentMove.<span class="me1">getPriority</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> toExec.<span class="me1">getPriority</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
            <span class="kw1">return</span><span class="sy0">;</span> <span class="co1">// skip lower-priority moves</span>
        <span class="br0">}</span>
 
        <span class="co1">// If a ComboMove has been identified, store it in currentMove</span>
        currentMove <span class="sy0">=</span> toExec<span class="sy0">;</span>
        currentMoveCastTime <span class="sy0">=</span> currentMove.<span class="me1">getCastTime</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT8 SECTION "Detect Combos in ActionListener" [4491-6314] -->
<h2 class="sectionedit9" id="execute_combos_in_the_update_loop">Execute Combos in the Update Loop</h2>
<div class="level2">

<p>
Now that you have detected the current move, you want to execute it. You do that in the update loop.
</p>
<pre class="code java">@Override
<span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span><span class="br0">{</span>
    time <span class="sy0">+=</span> tpf<span class="sy0">;</span>
    fireballExec.<span class="me1">updateExpiration</span><span class="br0">(</span>time<span class="br0">)</span><span class="sy0">;</span> 
    <span class="co1">// ... update more ComboExecs here....</span>
 
    <span class="kw1">if</span> <span class="br0">(</span>currentMove <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
        currentMoveCastTime <span class="sy0">-=</span> tpf<span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>currentMoveCastTime <span class="sy0">&lt;=</span> <span class="nu0">0</span><span class="br0">)</span><span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"THIS COMBO WAS TRIGGERED: "</span> <span class="sy0">+</span> currentMove.<span class="me1">getMoveName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co1">// TODO: for each combo, implement special actions here</span>
            currentMoveCastTime <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
            currentMove <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Test <code>currentMove.getMoveName()</code> and proceed to call methods that implement any special actions and bonuses. This is up to you and depends individually on your game.
</p>

</div>
<!-- EDIT9 SECTION "Execute Combos in the Update Loop" [6315-7152] -->
<h2 class="sectionedit10" id="why_combos">Why Combos?</h2>
<div class="level2">

<p>
Depending on the game genre, the designer can reward the players' intrinsical or extrinsical skills:
</p>
<ul>
<li class="level1"><div class="li"> (intrinsical:) RPGs typically calculate the success of an attack from the character's in-game training level: The player plays the role of a character whose skill level is defined in numbers. RPGs typically do not offer any Combos.</div>
</li>
<li class="level1"><div class="li"> (extrinsical:) Sport and fighter games typically choose to reward the player's “manual” skills: The success of a special move solely depends on the player's own dexterity. These games typically offer optional Combos.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/keyinput.html" class="wikilink1" title="tag:keyinput" rel="tag">keyinput</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT10 SECTION "Why Combos?" [7153-] -->
