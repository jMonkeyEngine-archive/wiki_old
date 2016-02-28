---
title: Input Handling
---
<h1 class="sectionedit1" id="input_handling">Input Handling</h1>
<div class="level1">

<p>
Users interact with your jME3 application with different input devices – the mouse, the keyboard, or a joystick. To respond to inputs we use the <code>inputManager</code> object in <code>SimpleApplication</code>.
</p>

<p>
This is how you add interaction to your game:
</p>
<ol>
<li class="level1"><div class="li"> For each action, choose the trigger(s) (a key or mouse click etc)</div>
</li>
<li class="level1"><div class="li"> For each action, add a trigger mapping to the inputManager</div>
</li>
<li class="level1"><div class="li"> Create at least one listener in SimpleApplication</div>
</li>
<li class="level1"><div class="li"> For each action, register its mappings to a listener</div>
</li>
<li class="level1"><div class="li"> Implement each action in the listener</div>
</li>
</ol>

</div>
<!-- EDIT1 SECTION "Input Handling" [1-561] -->
<h2 class="sectionedit2" id="code_samples">Code Samples</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestControls.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestControls.java" rel="nofollow">TestControls.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestJoystick.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/input/TestJoystick.java" rel="nofollow">TestJoystick.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Code Samples" [562-858] -->
<h2 class="sectionedit3" id="choose_trigger">1. Choose Trigger</h2>
<div class="level2">

<p>
Choose one or several key/mouse events for the interaction. We use <code>KeyTrigger</code>, <code>MouseAxisTrigger</code>, <code>MouseButtonTrigger</code>, <code>JoyAxisTrigger</code> and <code>JoyButtonTrigger</code> constants from the <code>com.jme3.input.controls</code> package. 
</p>

<p>
<strong>Note:</strong> The MouseAxis and JoyAxis triggers go along the X axis (right/left) or Y axis (up/down). These Triggers come with extra booleans for the negative half of the axis (left, down). Remember to write code that listens to the negative (true) and positive (false) axis!
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Trigger </th><th class="col1"> Code </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Mouse button: Left Click </td><td class="col1"> MouseButtonTrigger(MouseInput.BUTTON_LEFT) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Mouse button: Right Click </td><td class="col1"> MouseButtonTrigger(MouseInput.BUTTON_RIGHT) </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Mouse button: Middle Click </td><td class="col1"> MouseButtonTrigger(MouseInput.BUTTON_MIDDLE) </td>
	</tr>
	<tr class="row4">
		<td class="col0"> Mouse movement: Right </td><td class="col1"> MouseAxisTrigger(MouseInput.AXIS_X, true) </td>
	</tr>
	<tr class="row5">
		<td class="col0"> Mouse movement: Left </td><td class="col1"> MouseAxisTrigger(MouseInput.AXIS_X, false)</td>
	</tr>
	<tr class="row6">
		<td class="col0"> Mouse movement: Up </td><td class="col1"> MouseAxisTrigger(MouseInput.AXIS_Y, true) </td>
	</tr>
	<tr class="row7">
		<td class="col0"> Mouse movement: Down </td><td class="col1"> MouseAxisTrigger(MouseInput.AXIS_Y, false) </td>
	</tr>
	<tr class="row8">
		<td class="col0"> Mouse wheel: Up </td><td class="col1"> MouseAxisTrigger(MouseInput.AXIS_WHEEL,false) </td>
	</tr>
	<tr class="row9">
		<td class="col0"> Mouse wheel: Down </td><td class="col1"> MouseAxisTrigger(MouseInput.AXIS_WHEEL,true) </td>
	</tr>
	<tr class="row10">
		<td class="col0"> NumPad: 1, 2, 3, … </td><td class="col1"> KeyTrigger(KeyInput.KEY_NUMPAD1) … </td>
	</tr>
	<tr class="row11">
		<td class="col0"> Keyboard: 1, 2 , 3, … </td><td class="col1"> KeyTrigger(KeyInput.KEY_1) … </td>
	</tr>
	<tr class="row12">
		<td class="col0"> Keyboard: A, B, C, … </td><td class="col1"> KeyTrigger(KeyInput.KEY_A) … </td>
	</tr>
	<tr class="row13">
		<td class="col0"> Keyboard: Spacebar </td><td class="col1"> KeyTrigger(KeyInput.KEY_SPACE) </td>
	</tr>
	<tr class="row14">
		<td class="col0"> Keyboard: Shift </td><td class="col1"> KeyTrigger(KeyInput.KEY_RSHIFT), <br />
KeyTrigger(KeyInput.KEY_LSHIFT) </td>
	</tr>
	<tr class="row15">
		<td class="col0"> Keyboard: F1, F2, … </td><td class="col1"> KeyTrigger(KeyInput.KEY_F1) … </td>
	</tr>
	<tr class="row16">
		<td class="col0"> Keyboard: Return, Enter </td><td class="col1 leftalign"> KeyTrigger(KeyInput.KEY_RETURN), <br />
KeyTrigger(KeyInput.KEY_NUMPADENTER)  </td>
	</tr>
	<tr class="row17">
		<td class="col0"> Keyboard: PageUp, PageDown </td><td class="col1"> KeyTrigger(KeyInput.KEY_PGUP), <br />
KeyTrigger(KeyInput.KEY_PGDN) </td>
	</tr>
	<tr class="row18">
		<td class="col0"> Keyboard: Delete, Backspace </td><td class="col1"> KeyTrigger(KeyInput.KEY_BACK), <br />
KeyTrigger(KeyInput.KEY_DELETE) </td>
	</tr>
	<tr class="row19">
		<td class="col0"> Keyboard: Escape </td><td class="col1"> KeyTrigger(KeyInput.KEY_ESCAPE) </td>
	</tr>
	<tr class="row20">
		<td class="col0"> Keyboard: Arrows </td><td class="col1"> KeyTrigger(KeyInput.KEY_DOWN), <br />
KeyTrigger(KeyInput.KEY_UP) <br />
KeyTrigger(KeyInput.KEY_LEFT), KeyTrigger(KeyInput.KEY_RIGHT) </td>
	</tr>
	<tr class="row21">
		<td class="col0"> Joystick Button: </td><td class="col1"> JoyButtonTrigger(0, JoyInput.AXIS_POV_X), <br />
JoyButtonTrigger(0, JoyInput.AXIS_POV_Y) ? </td>
	</tr>
	<tr class="row22">
		<td class="col0"> Joystick Movement: Right </td><td class="col1"> JoyAxisTrigger(0, JoyInput.AXIS_POV_X, true) </td>
	</tr>
	<tr class="row23">
		<td class="col0"> Joystick Movement: Left </td><td class="col1"> JoyAxisTrigger(0, JoyInput.AXIS_POV_X, false) </td>
	</tr>
	<tr class="row24">
		<td class="col0"> Joystick Movement: Forward </td><td class="col1"> JoyAxisTrigger(0, JoyInput.AXIS_POV_Z, true) </td>
	</tr>
	<tr class="row25">
		<td class="col0"> Joystick Movement: Backward</td><td class="col1"> JoyAxisTrigger(0, JoyInput.AXIS_POV_Z, false) </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [1395-3373] -->
<p>
In your IDE, use code completion to quickly look up Trigger literals. In the jMonkeyEngine SDK for example, press ctrl-space or ctrl-/ after <code>KeyInput.|</code> to choose from the list of all keys.
</p>

</div>
<!-- EDIT3 SECTION "1. Choose Trigger" [859-3568] -->
<h2 class="sectionedit5" id="remove_default_trigger_mappings">2. Remove Default Trigger Mappings</h2>
<div class="level2">
<pre class="code">inputManager.deleteMapping( SimpleApplication.INPUT_MAPPING_MEMORY );</pre>
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Default Mapping</th><th class="col1">Key</th><th class="col2">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">INPUT_MAPPING_HIDE_STATS</td><td class="col1">F5</td><td class="col2">Hides the statistics in the bottom left.</td>
	</tr>
	<tr class="row2">
		<td class="col0">INPUT_MAPPING_CAMERA_POS</td><td class="col1">KEY_C</td><td class="col2">Prints debug output about the camera.</td>
	</tr>
	<tr class="row3">
		<td class="col0">INPUT_MAPPING_MEMORY</td><td class="col1">KEY_M</td><td class="col2">Prints debug output for memory usage.</td>
	</tr>
	<tr class="row4">
		<td class="col0">INPUT_MAPPING_EXIT</td><td class="col1">KEY_ESCAPE</td><td class="col2">Closes the application by calling <code>stop();</code>. Typically you do not remove this, unless you replace it by another way of quitting gracefully.</td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [3701-4117] -->
</div>
<!-- EDIT5 SECTION "2. Remove Default Trigger Mappings" [3569-4118] -->
<h2 class="sectionedit7" id="add_custom_trigger_mapping">3. Add Custom Trigger Mapping</h2>
<div class="level2">

<p>
When initializing the application, add a Mapping for each Trigger. 
</p>

<p>
Give the mapping a meaningful name. The name should reflect the action, not the button/key (because buttons/keys can change). Here some examples:
</p>
<pre class="code java">inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Pause Game"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_P</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Rotate"</span>,     <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_SPACE</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
...</pre>

<p>
There are cases where you may want to provide more then one trigger for one action. For example, some users prefer the WASD keys to navigate, while others prefer the arrow keys. Add several triggers for one mapping, by separating the Trigger objects with commas:
</p>
<pre class="code java">inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Left"</span>,  <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_A</span><span class="br0">)</span>, 
                                 <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_LEFT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// A and left arrow</span>
inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Right"</span>, <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_D</span><span class="br0">)</span>, 
                                 <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_RIGHT</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// D and right arrow</span>
                                 ...</pre>

</div>
<!-- EDIT7 SECTION "3. Add Custom Trigger Mapping" [4119-5183] -->
<h2 class="sectionedit8" id="create_listeners">4. Create Listeners</h2>
<div class="level2">

<p>
The jME3 input manager supports two types of event listeners for inputs: AnalogListener and ActionListener. You can use one or both listeners in the same application. Add one or both of the following code snippets to your main SimpleApplication-based class to activate the listeners.
</p>

<p>
<strong>Note:</strong> The two input listeners do not know, and do not care, which actual key was pressed. They only know which <em>named input mapping</em> was triggered. 
</p>

</div>
<!-- EDIT8 SECTION "4. Create Listeners" [5184-5657] -->
<h3 class="sectionedit9" id="actionlistener">ActionListener</h3>
<div class="level3">

<p>
<code>com.jme3.input.controls.ActionListener</code>
</p>
<ul>
<li class="level1"><div class="li"> Use for absolute “button pressed or released?”, “on or off?” actions. </div>
<ul>
<li class="level2"><div class="li"> Examples: Pause/unpause, a rifle or revolver shot, jump, click to select.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> JME gives you access to:</div>
<ul>
<li class="level2"><div class="li"> The mapping name of the triggered action.</div>
</li>
<li class="level2"><div class="li"> A boolean whether the trigger is still pressed or has just been released.</div>
</li>
<li class="level2"><div class="li"> A float of the current time-per-frame as timing factor</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> </div>
</li>
</ul>
<pre class="code java"><span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
     <span class="co3">/** TODO: test for mapping names and implement actions */</span>
  <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT9 SECTION "ActionListener" [5658-6324] -->
<h3 class="sectionedit10" id="analoglistener">AnalogListener</h3>
<div class="level3">

<p>
<code>com.jme3.input.controls.AnalogListener</code>
</p>
<ul>
<li class="level1"><div class="li"> Use for continuous and gradual actions.</div>
<ul>
<li class="level2"><div class="li"> Examples: Walk, run, rotate, accelerate vehicle, strafe, (semi-)automatic weapon shot</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> JME gives you access to:</div>
<ul>
<li class="level2"><div class="li"> The mapping name of the triggered action.</div>
</li>
<li class="level2"><div class="li"> A gradual float value between how long the trigger has been pressed.</div>
</li>
<li class="level2"><div class="li"> A float of the current time-per-frame as timing factor</div>
</li>
</ul>
</li>
</ul>
<pre class="code java"><span class="kw1">private</span> AnalogListener analogListener <span class="sy0">=</span> <span class="kw1">new</span> AnalogListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
     <span class="co3">/** TODO: test for mapping names and implement actions */</span>
  <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT10 SECTION "AnalogListener" [6325-6961] -->
<h2 class="sectionedit11" id="register_mappings_to_listeners">4. Register Mappings to Listeners</h2>
<div class="level2">

<p>
To activate the mappings, you must register them to a Listener. Write your registration code after the code block where you have added the mappings to the inputManager.
</p>

<p>
In the following example, you register the “Pause Game” mapping to the <code>actionListener</code> object, because pausing a game is in “either/or” decision.
</p>
<pre class="code java">inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="st0">"Pause Game"</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
In the following example, you register navigational mappings to the <code>analogListener</code> object, because walking is a continuous action. Players typically keep the key pressed to express continuity, for example when they want to “walk on” or “accelerate”.
</p>
<pre class="code java">inputManager.<span class="me1">addListener</span><span class="br0">(</span>analogListener, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="st0">"Left"</span>, <span class="st0">"Right"</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
As you see, you can add several listeners in one String array. You can call the addListener() method more than once, each time with a subset of your list, if that helps you keep you code tidy. Again, the Listeners do not care about actual which keys are configured, you only register named trigger mappings.
</p>

<p>
</p><p></p><div class="notetip">Did you register an action, but it does not work? Check the string's capitalization and spelling, it's case sensitive!
</div>


</div>
<!-- EDIT11 SECTION "4. Register Mappings to Listeners" [6962-8210] -->
<h2 class="sectionedit12" id="implement_actions_in_listeners">5. Implement Actions in Listeners</h2>
<div class="level2">

<p>
You specify the action to be triggered where it says TODO in the Listener code snippets. Typically, you write a series of if/else conditions, testing for all the mapping names, and then calling the respective action. 
</p>

<p>
Make use of the distinction between <code>if</code> and <code>else if</code> in this conditional.
</p>
<ul>
<li class="level1"><div class="li"> If several actions can be triggered simultaneously, test for all of these with a series of bare <code>if</code>s. For example, a character can be running forward <em>and</em> to the left.</div>
</li>
<li class="level1"><div class="li"> If certain actions exclude one another, test for them with <code>else if</code>, the the rest of the exclusive tests can be skipped and you save some miliseconds. For example, you either shoot or pick something up.</div>
</li>
</ul>

</div>
<!-- EDIT12 SECTION "5. Implement Actions in Listeners" [8211-8946] -->
<h3 class="sectionedit13" id="actionlistener1">ActionListener</h3>
<div class="level3">

<p>
In the most common case, you want an action to be triggered once, in the moment when the button or key trigger is released. For example, when the player presses a key to open a door, or clicks to pick up an item. For these cases, use an ActionListener and test for <code>&amp;&amp; !keyPressed</code>, like shown in the following example. 
</p>
<pre class="code java"><span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> keyPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
 
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Pause Game"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>keyPressed<span class="br0">)</span> <span class="br0">{</span> <span class="co1">// test?</span>
        isRunning <span class="sy0">=</span> <span class="sy0">!</span>isRunning<span class="sy0">;</span>                       <span class="co1">// action!</span>
      <span class="br0">}</span> 
 
      <span class="kw1">if</span> ...
 
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT13 SECTION "ActionListener" [8947-9618] -->
<h3 class="sectionedit14" id="analoglistener1">AnalogListener</h3>
<div class="level3">

<p>
The following example shows how you define actions with an AnalogListener. These actions are triggered continuously, as long (intensity <code>value</code>) as the named key or mouse button is down. Use this listeners for semi-automatic weapons and navigational actions.
</p>
<pre class="code java"><span class="kw1">private</span> AnalogListener analogListener <span class="sy0">=</span> <span class="kw1">new</span> AnalogListener<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAnalog<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">float</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
 
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Rotate"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>         <span class="co1">// test?</span>
        player.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, value<span class="sy0">*</span>speed, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// action!</span>
      <span class="br0">}</span> 
 
      <span class="kw1">if</span> ...
 
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT14 SECTION "AnalogListener" [9619-10198] -->
<h2 class="sectionedit15" id="let_users_remap_keys">Let Users Remap Keys</h2>
<div class="level2">

<p>
It is likely that your players have different keyboard layouts, are used to “reversed” mouse navigation, or prefer different navigational keys than the ones that you defined. You should create an options screen that lets users customize their mouse/key triggers for your mappings. Replace the trigger literals in the <code>inputManager.addMapping()</code> lines with variables, and load sets of triggers when the game starts. 
</p>

<p>
The abstraction of separating triggers and mappings has the advantage that you can remap triggers easily. Your code only needs to remove and add some trigger mappings. The core of the code (the listeners and actions) remains unchanged. 
</p>
<div class="tags"><span>
	<a href="/tag/keyinput.html" class="wikilink1" title="tag:keyinput" rel="tag">keyinput</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT15 SECTION "Let Users Remap Keys" [10199-] -->
