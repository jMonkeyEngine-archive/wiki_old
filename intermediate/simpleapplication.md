---
title: SimpleApplication
---
<h1 class="sectionedit1" id="simpleapplication">SimpleApplication</h1>
<div class="level1">

<p>
The base class of the jMonkeyEngine3 is <code>com.jme3.app.SimpleApplication</code>. Your first game's Main class extends SimpleApplication directly. When you feel confident you understand the features, you will typically extend SimpleApplication to create a custom base class for the type of games that you want to develop. 
</p>

<p>
SimpleApplication gives you access to standard game features, such as a scene graph (rootNode), an asset manager, a user interface (guiNode), input manager, audio manager, a physics simulation, and a fly-by camera. You call app.start() and app.stop() on your game instance to start or quit the application. 
</p>

<p>
</p><p></p><div class="noteimportant">For each game, you (directly or indirectly) extend SimpleApplication exactly once as the central class. If you need access to any SimpleApplication features from another game class, make the other class extend <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AbstractAppState</a> (don't extend SimpleApplication once more).
</div>


<p>
The following code sample shows the typical base structure of a jME3 game:
</p>
<pre class="code java"><span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> MyBaseGame <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        MyBaseGame app <span class="sy0">=</span> <span class="kw1">new</span> MyBaseGame<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
       <span class="coMULTI">/* Initialize the game scene here */</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
       <span class="coMULTI">/* Interact with game events in the main loop */</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleRender<span class="br0">(</span>RenderManager rm<span class="br0">)</span> <span class="br0">{</span>
       <span class="coMULTI">/* (optional) Make advanced modifications to frameBuffer and scene graph. */</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Let's have a look at the <abbr title="Application Programming Interface">API</abbr> of the base class.
</p>

</div>
<!-- EDIT1 SECTION "SimpleApplication" [1-1718] -->
<h2 class="sectionedit2" id="application_class">Application Class</h2>
<div class="level2">

<p>
Internally, com.jme3.app.SimpleApplication extends com.jme3.app.Application. The Application class represents a generic real-time 3D rendering jME3 application (i.e., not necessarily a game). Typically, you do not extend com.jme3.app.Application directly to create a game.
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Application class fields</th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">viewPort <br />
getViewPort()</td><td class="col1">The view object for the default camera. You can register advanced <a href="/jme3/advanced/effects_overview.html" class="wikilink1" title="jme3:advanced:effects_overview">post-processor filters</a> here.</td>
	</tr>
	<tr class="row2">
		<td class="col0">settings <br />
setSettings()</td><td class="col1">Use this <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">AppSettings</a> object to specify the display width and height (by default 640×480), color bit depth, z-buffer bits, anti-aliasing samples, and update frequency, video and audio renderer, asset manager. See: <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">AppSettings</a>.</td>
	</tr>
	<tr class="row3">
		<td class="col0">cam <br />
getCamera()</td><td class="col1">The default <a href="/jme3/advanced/camera.html" class="wikilink1" title="jme3:advanced:camera">camera</a> provides perspective projection, 45° field of view, near plane = 1 wu, far plane = 1000 wu.</td>
	</tr>
	<tr class="row4">
		<td class="col0">assetManager <br />
getAssetManager()</td><td class="col1">An object that manages paths for loading models, textures, materials, sounds, etc. By default the <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager">Asset Manager</a> paths are relative to your project's root directory. </td>
	</tr>
	<tr class="row5">
		<td class="col0">audioRenderer <br />
getAudioRenderer()</td><td class="col1">This object gives you access to the jME3 <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">audio</a> system. </td>
	</tr>
	<tr class="row6">
		<td class="col0">listener <br />
getListener()</td><td class="col1">This object represents the user's ear for the jME3 <a href="/jme3/advanced/audio.html" class="wikilink1" title="jme3:advanced:audio">audio</a> system. </td>
	</tr>
	<tr class="row7">
		<td class="col0">inputManager <br />
getInputManager()</td><td class="col1">Use the <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">inputManager</a> to configure your custom inputs (mouse movement, clicks, key presses, etc) and set mouse pointer visibility.</td>
	</tr>
	<tr class="row8">
		<td class="col0">stateManager <br />
getStateManager()</td><td class="col1">You use the Application's state manager to activate <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppStates</a>, such as <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">Physics</a>.</td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [2024-3450] --><div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Application methods</th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">setPauseOnLostFocus(true)</td><td class="col1">Set this boolean whether the game loop should stop running when ever the window loses focus (typical for single-player game). Set this to false for real-time and multi-player games that keep running. </td>
	</tr>
	<tr class="row2">
		<td class="col0">start()</td><td class="col1">Call this method to start a jME3 game. By default this opens a new jME3 window, initializes the scene, and starts the event loop. </td>
	</tr>
	<tr class="row3">
		<td class="col0">restart()</td><td class="col1">Loads modified <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">AppSettings</a> into the current application context.</td>
	</tr>
	<tr class="row4">
		<td class="col0">stop()</td><td class="col1">Stops the running jME3 game and closes the jME3 window.</td>
	</tr>
	<tr class="row5">
		<td class="col0">start(Type.Headless) etc</td><td class="col1">Switch Context com.​jme3.​system.​JmeContext.Type when starting the application: <br />
Type.Display – jME application runs in a window of its own. (This is the default.)<br />
Type.Canvas – jME application is embedded in a <a href="/jme3/advanced/swing_canvas.html" class="wikilink1" title="jme3:advanced:swing_canvas">Swing Canvas</a>. <br />
Type.Headless – jME application runs its event loop without calculating any view and without opening any window. Can be used for a <a href="/jme3/advanced/headless_server.html" class="wikilink1" title="jme3:advanced:headless_server">Headless Server</a> application.<br />
Type.OffscreenSurface – jME application view is not shown and no window opens, but everything calculated and cached as bitmap (back buffer) for use by other applications.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [3452-4638] --><div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Internal class field/method</th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">context <br />
getContext()</td><td class="col1">The application context contains the renderer, <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">AppSettings</a>, timer, etc. Typically, you do not directly access the context object.</td>
	</tr>
	<tr class="row2">
		<td class="col0">inputEnabled</td><td class="col1">this internal boolean is true if you want the system to listen for user inputs, and false if you just want to play a non-interactive scene. You change the boolean using <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">AppSettings</a>.</td>
	</tr>
	<tr class="row3">
		<td class="col0">keyInput, mouseInput <br />
joyInput, touchInput</td><td class="col1">Default input contexts for keyboard, mouse, and joystick. Internally used to enable handling of joysticks or touch devices. The base classes contain key and mouse button enums.</td>
	</tr>
	<tr class="row4">
		<td class="col0">renderManager <br />
getRenderManager() <br />
renderer <br />
getRenderer();</td><td class="col1">Low-level and high-level rendering interface. Mostly used internally.</td>
	</tr>
	<tr class="row5">
		<td class="col0">guiViewPort <br />
getGuiViewPort()</td><td class="col1">The view object for the orthogonal <abbr title="Graphical User Interface">GUI</abbr> view. Only used internally for <a href="/jme3/advanced/hud.html" class="wikilink1" title="jme3:advanced:hud">HUD</a>s. </td>
	</tr>
	<tr class="row6">
		<td class="col0">timer</td><td class="col1">An internal update loop timer, don't use. See <code>tpf</code> in <code>simpleUpdate()</code> below to learn about timers.</td>
	</tr>
	<tr class="row7">
		<td class="col0">paused</td><td class="col1">Boolean is used only internally during runtime to pause/unpause a game. (You need to implement your own isRunning boolean or so.)</td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [4640-5782] -->
</div>
<!-- EDIT2 SECTION "Application Class" [1719-5783] -->
<h2 class="sectionedit6" id="simpleapplication_class">SimpleApplication Class</h2>
<div class="level2">

<p>
The com.jme3.app.SimpleApplication class extends the generic com.jme3.app.Application class. SimpleApplication makes it easy to start writing a game because it adds typical functionality:
</p>
<ul>
<li class="level1"><div class="li"> First-person (fly-by) camera</div>
</li>
<li class="level1"><div class="li"> Scene graph that manages your models in the rendered 3D scene.</div>
</li>
<li class="level1"><div class="li"> Useful default input mappings (details below.) </div>
</li>
</ul>

<p>
Additional to the functionality that Application brings, SimpleApplication offers the following methods and fields that can be used, for example, inside the <code>simpleInitApp()</code> method:
</p>
<div class="table sectionedit7"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">SimpleApplication Class Field</th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">rootNode <br />
getRootNode()</td><td class="col1">The root node of the scene graph. Attach a <a href="/jme3/advanced/spatial.html" class="wikilink1" title="jme3:advanced:spatial">Spatial</a> to the rootNode and it appears in the 3D scene.</td>
	</tr>
	<tr class="row2">
		<td class="col0">guiNode <br />
getGuiNode()</td><td class="col1">Attach flat <abbr title="Graphical User Interface">GUI</abbr> elements (such as <a href="/jme3/advanced/hud.html" class="wikilink1" title="jme3:advanced:hud">HUD</a> images and text) to this orthogonal <abbr title="Graphical User Interface">GUI</abbr> node to make them appear on the screen.</td>
	</tr>
	<tr class="row3">
		<td class="col0">flyCam <br />
getFlyByCamera()</td><td class="col1">The default first-person fly-by camera control. This default camera control lets you navigate the 3D scene using the preconfigured WASD and arrow keys and the mouse.</td>
	</tr>
</table></div>
<!-- EDIT7 TABLE [6351-6894] --><div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">SimpleApplication Method</th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">loadStatsView();</td><td class="col1">Call this method to print live statistic information to the screen, such as current frames-per-second and triangles/vertices counts. You use this info typically only during development or debugging.</td>
	</tr>
	<tr class="row2">
		<td class="col0">loadFPSText();</td><td class="col1">Call this method to print the current framerate (frames per second) to the screen.</td>
	</tr>
	<tr class="row3">
		<td class="col0">setDisplayFps(false);</td><td class="col1">A default SimpleApplication displays the framerate (frames per second) on the screen. You can choose to deactivate the FPS display using this command.</td>
	</tr>
	<tr class="row4">
		<td class="col0">setDisplayStatView(false);</td><td class="col1">A default SimpleApplication displays mesh statistics on the screen using the com.jme3.app.StatsView class. The information is valuable during the development and debugging phase, but for the release, you should hide the statistics HUD.</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [6896-7688] --><div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">SimpleApplication Interface</th><th class="col1">Purpose</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">public void simpleInitApp()</td><td class="col1">Override this method to initialize the game scene. Here you load and create objects, attach Spatials to the rootNode, and bring everything in its starts position. See also <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a> for best practices.</td>
	</tr>
	<tr class="row2">
		<td class="col0">public void simpleUpdate(float tpf)</td><td class="col1">Override this method to hook into the <a href="/jme3/advanced/update_loop.html" class="wikilink1" title="jme3:advanced:update_loop">update loop</a>, all code you put here is repeated in a loop. Use this loop to poll the current game state and respond to changes, or to let the game mechanics generate encounters and initiate state changes. Use the float <code>tpf</code> as a factor to time actions relative to the <em>time per frame</em> in seconds: <code>tpf</code> is large on slow PCs, and small on fast PCs. <br />
For more info on how to hook into the <a href="/jme3/advanced/update_loop.html" class="wikilink1" title="jme3:advanced:update_loop">update loop</a>, see <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a> and <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a>. </td>
	</tr>
	<tr class="row3">
		<td class="col0">public void simpleRender(RenderManager rm)</td><td class="col1"><strong>Optional:</strong> Advanced developers can override this method if the need to modify the frameBuffer and scene graph directly.</td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [7690-8760] -->
<p>
</p><p></p><div class="notetip">Use <code>app.setShowSettings(true);</code> to present the user with a splashscreen and the built-in display settings dialog when starting the game; or use <code>app.setShowSettings(false);</code> to hide the buil-in screen (in this case, you may want to provide a custom splashscreen and settings panel). Set this boolean before calling <code>app.start()</code> in the <code>main()</code> method of the SimpleApplication. See also <a href="/jme3/intermediate/appsettings.html" class="wikilink1" title="jme3:intermediate:appsettings">AppSettings</a>.
</div>


</div>
<!-- EDIT6 SECTION "SimpleApplication Class" [5784-9192] -->
<h2 class="sectionedit10" id="default_input_mappings">Default Input Mappings</h2>
<div class="level2">

<p>
The following default navigational input actions are mapped by the default <code>flyCam</code> control in a SimpleApplication: You can use these mappings for debugging and testing until you implement custom <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">input handling</a>.
</p>
<div class="table sectionedit11"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Key</th><th class="col1">Action</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">KEY_ESCAPE</td><td class="col1">Quits the game by calling <code>app.stop()</code></td>
	</tr>
	<tr class="row2">
		<td class="col0">KEY_C</td><td class="col1">Debug key: Prints camera position, rotation, and direction to the out stream.</td>
	</tr>
	<tr class="row3">
		<td class="col0">KEY_M</td><td class="col1">Debug key: Prints memory usage stats the out stream.</td>
	</tr>
	<tr class="row4">
		<td class="col0">F5</td><td class="col1">Hides or shows the statistics the bottom left.</td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [9463-9728] -->
<p>
As long as the <code>flyCam</code> is enabled, the following so-called “WASD” inputs, including MouseLook, are available:
</p>
<div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Camera Motion</th><th class="col1">Key or Mouse Input</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Move Forward</td><td class="col1">KEY_W</td>
	</tr>
	<tr class="row2">
		<td class="col0">Move Left (Strafe)</td><td class="col1">KEY_A</td>
	</tr>
	<tr class="row3">
		<td class="col0">Move Backward</td><td class="col1">KEY_S</td>
	</tr>
	<tr class="row4">
		<td class="col0">Move Right (Strafe)</td><td class="col1">KEY_D</td>
	</tr>
	<tr class="row5">
		<td class="col0">Move Vertical Upward</td><td class="col1">KEY_Q</td>
	</tr>
	<tr class="row6">
		<td class="col0">Move Vertical Downward</td><td class="col1">KEY_Z</td>
	</tr>
	<tr class="row7">
		<td class="col0">Rotate Left</td><td class="col1">KEY_LEFT, or move mouse horizontally left (-x)</td>
	</tr>
	<tr class="row8">
		<td class="col0">Rotate Right</td><td class="col1">KEY_RIGHT, or move mouse horizontally right (+x)</td>
	</tr>
	<tr class="row9">
		<td class="col0">Rotate Up</td><td class="col1">KEY_UP, or move mouse vertically forward (+y)</td>
	</tr>
	<tr class="row10">
		<td class="col0">Rotate Down</td><td class="col1">KEY_DOWN, or move mouse vertically backward (-y)</td>
	</tr>
	<tr class="row11">
		<td class="col0">Rotate</td><td class="col1">BUTTON_LEFT, or hold left mouse button and drag to rotate</td>
	</tr>
	<tr class="row12">
		<td class="col0">Zoom In</td><td class="col1">AXIS_WHEEL, or scroll mouse wheel backward</td>
	</tr>
	<tr class="row13">
		<td class="col0">Zoom Out</td><td class="col1">AXIS_WHEEL, or scroll mouse wheel forward</td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [9844-10455] -->
</div>
<!-- EDIT10 SECTION "Default Input Mappings" [9193-10456] -->
<h2 class="sectionedit13" id="defaults_and_customization">Defaults and Customization</h2>
<div class="level2">

<p>
By default, a SimpleApplication displays Statistics (<code>new StatsAppState()</code>), has debug output keys configured (<code>new DebugKeysAppState()</code>), and enables the flyCam (<code>new FlyCamAppState()</code>). You can customize which you want to reuse in your SimpleApplication.
</p>

<p>
The following example shows how you can remove one of the default AppStates, in this case, the FlyCamAppState:
</p>
<ul>
<li class="level1"><div class="li"> Either, in your application's contructor, you create the SimpleApplication with only the AppStates you want to keep: <pre class="code java"><span class="kw1">public</span> MyAppliction<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">super</span><span class="br0">(</span> <span class="kw1">new</span> StatsAppState<span class="br0">(</span><span class="br0">)</span>, <span class="kw1">new</span> DebugKeysAppState<span class="br0">(</span><span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Or, in the <code>simpleInitApp()</code> method, you remove the ones you do not want to keep: <pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    stateManager.<span class="me1">detach</span><span class="br0">(</span> stateManager.<span class="me1">getState</span><span class="br0">(</span>FlyCamAppState.<span class="kw1">class</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    ...</pre>
</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/display.html" class="wikilink1" title="tag:display" rel="tag">display</a>,
	<a href="/tag/basegame.html" class="wikilink1" title="tag:basegame" rel="tag">basegame</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/intermediate.html" class="wikilink1" title="tag:intermediate" rel="tag">intermediate</a>,
	<a href="/tag/init.html" class="wikilink1" title="tag:init" rel="tag">init</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/game.html" class="wikilink1" title="tag:game" rel="tag">game</a>,
	<a href="/tag/loop.html" class="wikilink1" title="tag:loop" rel="tag">loop</a>,
	<a href="/tag/rootnode.html" class="wikilink1" title="tag:rootnode" rel="tag">rootnode</a>,
	<a href="/tag/application.html" class="wikilink1" title="tag:application" rel="tag">application</a>,
	<a href="/tag/simpleapplication.html" class="wikilink1" title="tag:simpleapplication" rel="tag">simpleapplication</a>
</span></div>

</div>
<!-- EDIT13 SECTION "Defaults and Customization" [10457-] -->
