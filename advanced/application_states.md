---
title: Application States
---
<h1 class="sectionedit1" id="application_states">Application States</h1>
<div class="level1">

<p>
The <code>com.jme3.app.state.AppState</code> class is a customizable jME3 interface that allows you to control the global game logic, the overall game mechanics. (To control the behaviour of a Spatial, see <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a> instead. Controls and AppStates can be used together.)
</p>

</div>
<!-- EDIT1 SECTION "Application States" [1-322] -->
<h2 class="sectionedit2" id="overview">Overview</h2>
<div class="level2">

</div>
<!-- EDIT2 SECTION "Overview" [323-344] -->
<h3 class="sectionedit3" id="use_case_examples">Use Case Examples</h3>
<div class="level3">

<p>
There are situations during your game development where you think:
</p>
<ul>
<li class="level1"><div class="li"> Mouse and key inputs are handled differently in-game versus in the main menu. Can I group a set of input handler settings, and activate and deactivate them all in one step?  </div>
</li>
<li class="level1"><div class="li"> I have the in-game scene, and a character editor, and a Captain's Quarters screen. Can I group a set of nodes and behaviours, and swap them in and out in one step?</div>
</li>
<li class="level1"><div class="li"> When I pause the game, I want the character's “idle” animation to continue, but all other loops and game events should stop. How do I define what happens when the game is paused/unpaused? </div>
</li>
<li class="level1"><div class="li"> I have a conditional block that takes up a lot of space in my simpleUpdate() loop. Can I wrap up this block of code, and switch it on and off in one step?</div>
</li>
<li class="level1"><div class="li"> Can I package everything that belongs in-game, and everything that belongs to the menu screen, and switch between these two “big states” in one step? </div>
</li>
</ul>

<p>
You can! This is what AppStates are there for. An AppState class is subset of (or an extension to) your application. Every AppState class has access to all fields in your main application (AssetManager, ViewPort, StateManager, InputManager, RootNode, GuiNode, etc) and hooks into the main update loop. An AppState can contain:
</p>
<ul>
<li class="level1"><div class="li"> a subset of class fields, functions, methods (game state data and accessors), </div>
</li>
<li class="level1"><div class="li"> a subset of <abbr title="Graphical User Interface">GUI</abbr> elements and their listeners, </div>
</li>
<li class="level1"><div class="li"> a subset of input handlers and mappings, </div>
</li>
<li class="level1"><div class="li"> a subset of nodes that you load and attach to the rootNode, </div>
</li>
<li class="level1"><div class="li"> a subset of conditional actions that you branch to in the simpleUpdate() loop, </div>
</li>
<li class="level1"><div class="li"> a subset of other AppStates and Controls</div>
</li>
<li class="level1"><div class="li"> … or combinations thereof. </div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Use Case Examples" [345-2032] -->
<h3 class="sectionedit4" id="supported_features">Supported Features</h3>
<div class="level3">

<p>
Each AppState lets you define what happens to it in the following situations:
</p>
<ul>
<li class="level1"><div class="li"> <strong>The AppState is initialized:</strong> You load and initialize game data, InputHandlers, AppStates and Controls and attach nodes. <br />
The AppState executes its own simpleInitApp() method when it is attached, so to speak.</div>
</li>
<li class="level1"><div class="li"> <strong>The AppState has been enabled (unpaused):</strong> This toggles a boolean isEnabled() to true. Here you attach nodes and listeners that should become active while it's running. </div>
</li>
<li class="level1"><div class="li"> <strong>While the AppState is running/paused:</strong> You can poll isEnabled() to define paused and unpaused game behaviour in the update() loop. In update(), you poll and modify the game state, modify the scene graph, and trigger events. Test if <code>!isEnabled()</code>, and write code that skips the running sections of this AppState's <code>update()</code> loop. <br />
Each AppState has its own update loop, which hooks into the main simpleUpdate() loop (callback). </div>
</li>
<li class="level1"><div class="li"> <strong>The AppState has been disabled (paused):</strong> This toggles a boolean isEnabled() to false. Here you switch all objects to their specific “paused” behaviour. </div>
</li>
<li class="level1"><div class="li"> <strong>The AppState is cleaned up:</strong> Here you decide what happens when the AppState is detached. Save this AppState's game state, unregister Controls and InputHandlers, detach related AppStates, detach nodes from the rootNode, etc.</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">Tip: AppStates are extremely handy to swap out, or pause/unpause whole sets of other AppStates. For example, an InGameState (loads in-game <abbr title="Graphical User Interface">GUI</abbr>, activates click-to-shoot input mappings, inits game content, starts game loop) versus MainScreenState (stops game loop, saves and detaches game content, switches to menu screen <abbr title="Graphical User Interface">GUI</abbr>, switches to click-to-select input mappings).
</div>


</div>
<!-- EDIT4 SECTION "Supported Features" [2033-3761] -->
<h3 class="sectionedit5" id="usage">Usage</h3>
<div class="level3">

<p>
To implement game logic:
</p>
<ol>
<li class="level1"><div class="li"> Create one AbstractAppState instance for each set of game mechanics. </div>
</li>
<li class="level1"><div class="li"> Implement game behaviour in the AppState's update() method.</div>
<ul>
<li class="level2"><div class="li"> You can pass custom data as arguments in the constructor.</div>
</li>
<li class="level2"><div class="li"> The AppState has access to everything inside the app's scope via the Application <code>app</code> object.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Create and attach the AppState to the AppStateManager (<code>stateManager.attach(myAppState);</code>) and initialize it.</div>
</li>
<li class="level1"><div class="li"> Enable and disable (unpause and pause) the AppStates that you need during the game.</div>
</li>
<li class="level1"><div class="li"> Detach the AppState from the AppStateManager (<code>stateManager.detach(myAppState);</code>) and clean it up.</div>
</li>
</ol>

<p>
When you add several AppStates to one Application and activate them, their initialize() methods and update() loops are executed in the order in which the AppStates were added to the AppStateManager.
</p>

</div>
<!-- EDIT5 SECTION "Usage" [3762-4620] -->
<h3 class="sectionedit6" id="code_samples">Code Samples</h3>
<div class="level3">

<p>
JME3 comes with a BulletAppState that implements Physical behaviour (using the jBullet library). You, for example, could write an Artificial Intelligence AppState to control all your enemy units. Existing examples in the code base include:
</p>
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-bullet/src/common/java/com/jme3/bullet/BulletAppState.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-bullet/src/common/java/com/jme3/bullet/BulletAppState.java" rel="nofollow">BulletAppState</a> controls physical behaviour in PhysicsControl'ed Spatials.</div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/app/state/TestAppStates.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/app/state/TestAppStates.java" rel="nofollow">TestAppStates.java</a> an example of a custom AppState</div>
<ul>
<li class="level2"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/app/state/RootNodeState.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/app/state/RootNodeState.java" rel="nofollow">RootNodeState.java</a></div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Code Samples" [4621-5428] -->
<h2 class="sectionedit7" id="appstate">AppState</h2>
<div class="level2">

<p>
The AppState interface lets you initialize sets of objects, and hook a set of continously executing code into the main loop.
</p>
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AppState Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">initialize(asm,app)</td><td class="col1">When this AppState is added to the game, the RenderThread initializes the AppState and then calls this method. You can modify the scene graph from here (e.g. attach nodes). To get access to the main app, call: <pre class="code java"><span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">this</span>.<span class="me1">app</span> <span class="sy0">=</span> <span class="br0">(</span>SimpleApplication<span class="br0">)</span> app<span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row2">
		<td class="col0">cleanup()</td><td class="col1">This method is executed after you remove the AppState from the game. Here you implement clean-up code for when this state is detached. You can modify the scene graph from here (e.g. detach nodes).</td>
	</tr>
	<tr class="row3">
		<td class="col0">update(float tpf)</td><td class="col1">Here you implement the behaviour that you want to hook into the simpleUpdate() loop while this state is attached to the game. You can modify the scene graph from here.</td>
	</tr>
	<tr class="row4">
		<td class="col0">isInitialized()</td><td class="col1">Your implementations of this interface should return the correct respective boolean value. (See AbstractAppState)</td>
	</tr>
	<tr class="row5">
		<td class="col0">setActive(true) <br />
setActive(false)</td><td class="col1">Temporarily enables or disables an AppState. (See AbstractAppState) </td>
	</tr>
	<tr class="row6">
		<td class="col0">isActive()</td><td class="col1">Test whether AppState is enabled or disabled. Your implementation should consider the boolean. (See AbstractAppState)</td>
	</tr>
	<tr class="row7">
		<td class="col0">stateAttached(asm) <br />
stateDetached(asm)</td><td class="col1">The AppState knows when it is attached to, or detached from, the AppStateManager, and triggers these two methods. Don't modify the scene graph from here! (Typically not used.) </td>
	</tr>
	<tr class="row8">
		<td class="col0">render(RenderManager rm)</td><td class="col1">Renders the state, plus your optional customizations. (Typically not used.)</td>
	</tr>
	<tr class="row9">
		<td class="col0">postRender()</td><td class="col1">Called after all rendering commands are flushed, including your optional customizations. (Typically not used.)</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [5577-7139] -->
</div>
<!-- EDIT7 SECTION "AppState" [5429-7140] -->
<h2 class="sectionedit9" id="abstractappstate">AbstractAppState</h2>
<div class="level2">

<p>
The AbstractAppState class already implements some common methods (<code>isInitialized(), setActive(), isActive()</code>) and makes creation of custom AppStates a bit easier. We recommend you extend AbstractAppState and override the remaining AppState methods: <code>initialize(), setEnabled(), cleanup()</code>.
</p>

<p>
Definition:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyAppState <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
 
    <span class="kw1">private</span> SimpleApplication app<span class="sy0">;</span>
 
    <span class="kw1">private</span> Node x <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"x"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// some custom class fields...    </span>
    <span class="kw1">public</span> Node getX<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span> <span class="kw1">return</span> x<span class="sy0">;</span> <span class="br0">}</span>  <span class="co1">// some custom methods... </span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span> 
      <span class="kw1">this</span>.<span class="me1">app</span> <span class="sy0">=</span> <span class="br0">(</span>SimpleApplication<span class="br0">)</span>app<span class="sy0">;</span>          <span class="co1">// cast to a more specific class</span>
 
      <span class="co1">// init stuff that is independent of whether state is PAUSED or RUNNING</span>
      <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">attachChild</span><span class="br0">(</span>getX<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// modify scene graph...</span>
      <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">doSomething</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>                     <span class="co1">// call custom methods...</span>
   <span class="br0">}</span>
 
   @Override
    <span class="kw1">public</span> <span class="kw4">void</span> cleanup<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">super</span>.<span class="me1">cleanup</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="co1">// unregister all my listeners, detach all my nodes, etc...</span>
      <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">detachChild</span><span class="br0">(</span>getX<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// modify scene graph...</span>
      <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">doSomethingElse</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>                 <span class="co1">// call custom methods...</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> setEnabled<span class="br0">(</span><span class="kw4">boolean</span> enabled<span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// Pause and unpause</span>
      <span class="kw1">super</span>.<span class="me1">setEnabled</span><span class="br0">(</span>enabled<span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">if</span><span class="br0">(</span>enabled<span class="br0">)</span><span class="br0">{</span>
        <span class="co1">// init stuff that is in use while this state is RUNNING</span>
        <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">attachChild</span><span class="br0">(</span>getX<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// modify scene graph...</span>
        <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">doSomethingElse</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>                 <span class="co1">// call custom methods...</span>
      <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        <span class="co1">// take away everything not needed while this state is PAUSED</span>
        ...
      <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="co1">// Note that update is only called while the state is both attached and enabled.</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// do the following while game is RUNNING</span>
      <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"blah"</span><span class="br0">)</span>.<span class="me1">scale</span><span class="br0">(</span>tpf<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// modify scene graph...</span>
      x.<span class="me1">setUserData</span><span class="br0">(</span>...<span class="br0">)</span><span class="sy0">;</span>                                 <span class="co1">// call some methods...</span>
    <span class="br0">}</span>
 
<span class="br0">}</span></pre>

</div>
<!-- EDIT9 SECTION "AbstractAppState" [7141-9313] -->
<h2 class="sectionedit10" id="pausing_and_unpausing">Pausing and Unpausing</h2>
<div class="level2">

<p>
You define what an AppState does when Paused or Unpaused, in the <code>setEnabled()</code> and <code>update()</code> methods. Call <code>myState.setEnabled(false)</code> on all states that you want to pause. Call <code>myState.setEnabled(true)</code> on all states that you want to unpause.
</p>

</div>
<!-- EDIT10 SECTION "Pausing and Unpausing" [9314-9604] -->
<h2 class="sectionedit11" id="appstatemanager">AppStateManager</h2>
<div class="level2">

<p>
The com.jme3.app.state.AppStateManager holds the list of AppStates for an application. AppStateManager ensures that active AppStates can modify the scene graph, and that the update() loops of active AppStates is executed. There is one AppStateManager per application. You typically attach several AppStates to one AppStateManager, but the same state can only be attached once.
</p>
<div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">AppStateManager Method</th><th class="col1">Usage</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">hasState(myState)</td><td class="col1">Is AppState object 'myState' attached?</td>
	</tr>
	<tr class="row2">
		<td class="col0">getState(MyAppState.class)</td><td class="col1">Returns the first attached state that is an instance of a subclass of <code>MyAppState.class</code>.</td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [10012-10222] -->
<p>
The AppStateManager's <code>render(), postRender(), cleanup()</code> methods are internal, ignore them, users never call them directly.
</p>
<ul>
<li class="level1"><div class="li"> If a detached AppState is attached then initialize() will be called on the following render pass.</div>
</li>
<li class="level1"><div class="li"> If an attached AppState is detached then cleanup() will be called on the following render pass.</div>
</li>
<li class="level1"><div class="li"> If you attach an already-attached AppState then the second attach is a no-op and will return false.</div>
</li>
<li class="level1"><div class="li"> If you both attach and detach an AppState within one frame then neither initialize() or cleanup() will be called, although if either is called both will be.</div>
</li>
<li class="level1"><div class="li"> If you both detach and then re-attach an AppState within one frame then on the next update pass its cleanup() and initialize() methods will be called in that order.</div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "AppStateManager" [9605-10988] -->
<h2 class="sectionedit13" id="best_practices">Best Practices</h2>
<div class="level2">

</div>
<!-- EDIT13 SECTION "Best Practices" [10989-11016] -->
<h3 class="sectionedit14" id="communication_among_appstates">Communication Among AppStates</h3>
<div class="level3">

<p>
You can only access other AppStates (read from and write to them) from certain places: From a Control's update() method, from an AppState's update() method, and from the SimpleApplication's simpleUpdate() loop. Don't mess with the AppState from other places, because from other methods you have no control over the order of modifications; the game can go out of sync because you can't know when (during which half-finished step of another state change) your modification will be performed.
</p>

<p>
You can use custom accessors to get data from AppStates, to set data in AppStates, or to trigger methods in AppStates.
</p>
<pre class="code java"><span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getStateManager</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getState</span><span class="br0">(</span>MyAppState.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">doSomeCustomStuffInThisState</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT14 SECTION "Communication Among AppStates" [11017-11772] -->
<h3 class="sectionedit15" id="initialize_familiar_class_fields">Initialize Familiar Class Fields</h3>
<div class="level3">

<p>
To access class fields of the SimpleApplication the way you are used to, initialize them to local variables, as shown in the following AppState template:
</p>
<pre class="code java"><span class="kw1">private</span> SimpleApplication app<span class="sy0">;</span>
<span class="kw1">private</span> Node              rootNode<span class="sy0">;</span>
<span class="kw1">private</span> AssetManager      assetManager<span class="sy0">;</span>
<span class="kw1">private</span> AppStateManager   stateManager<span class="sy0">;</span>
<span class="kw1">private</span> InputManager      inputManager<span class="sy0">;</span>
<span class="kw1">private</span> ViewPort          viewPort<span class="sy0">;</span>
<span class="kw1">private</span> BulletAppState    physics<span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> MyAppState <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">app</span> <span class="sy0">=</span> <span class="br0">(</span>SimpleApplication<span class="br0">)</span> app<span class="sy0">;</span> <span class="co1">// can cast Application to something more specific</span>
    <span class="kw1">this</span>.<span class="me1">rootNode</span>     <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">assetManager</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">stateManager</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getStateManager</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">inputManager</span> <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getInputManager</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">viewPort</span>     <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">app</span>.<span class="me1">getViewPort</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">physics</span>      <span class="sy0">=</span> <span class="kw1">this</span>.<span class="me1">stateManager</span>.<span class="me1">getState</span><span class="br0">(</span>BulletAppState.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT15 SECTION "Initialize Familiar Class Fields" [11773-] -->
