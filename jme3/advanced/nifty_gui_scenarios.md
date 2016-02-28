---
title: Nifty GUI 1.3 - Usecase Scenarios
---
<h1 class="sectionedit1" id="nifty_gui_13_-_usecase_scenarios">Nifty GUI 1.3 - Usecase Scenarios</h1>
<div class="level1">

<p>
This document contains typical NiftyGUI usecase scenarios, such as adding effects, game states, and creating typical game screens. 
</p>

<p>
Requirements: These tips assume that you have read and understood the <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Creating JME3 User Interfaces with Nifty GUI</a> tutorial, and have already laid out a basic <abbr title="Graphical User Interface">GUI</abbr> that interacts with your JME3 application. Here you learn how you integrate the <abbr title="Graphical User Interface">GUI</abbr> better, and add effects and advanced controls.
</p>

</div>
<!-- EDIT1 SECTION "Nifty GUI 1.3 - Usecase Scenarios" [1-506] -->
<h2 class="sectionedit2" id="switch_game_states">Switch Game States</h2>
<div class="level2">

<p>
In a JME game, you typically have three game states:
</p>
<ol>
<li class="level1"><div class="li"> Stopped: The game is stopped, a StartScreen is displayed. </div>
</li>
<li class="level1"><div class="li"> Running: The game is running, the in-game HudScreen is displayed. </div>
</li>
<li class="level1"><div class="li"> Paused: The game is paused, a PausedScreen is displayed.</div>
</li>
</ol>

<p>
(Aside: Additionally, the Stopped state often contains a LoadScreen, LogonScreen, OptionsScreen, CharacterCreationScreen, HighScoreScreen, CreditsScreen, etc. Some games let you access the OptionsScreen in the Paused state as well. The Running state can also contain an InventoryScreen, ItemShopScreen, StatsScreen, SkillScreen, etc.)
</p>

<p>
In JME, game states are implemented as custom <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AppState</a> objects. Write each AppState so it brings its own input mappings, rootNode content, update loop behaviour, etc with it.
</p>
<ol>
<li class="level1"><div class="li"> Stopped: StartScreen AppState + GuiInputs AppState</div>
</li>
<li class="level1"><div class="li"> Paused: PausedScreen AppState + GuiInputs AppState</div>
</li>
<li class="level1"><div class="li"> Running: HudScreen AppState + InGameInputs AppState + BulletAppState (jme physics), …</div>
</li>
</ol>

<p>
When the player switches between game states, you detach one set of AppStates, and attach another. For example, when the player pauses the running game, you use a boolean switch to pause the game loop and deactivate the game inputs (shooting, navigation). The screen is overlayed with a PausedScreen, which contains a visible mouse pointer and a Continue button. When the player clicks Continue, the mouse pointer is deactivated, the in-game input and navigational mappings are activated, and the game loop continues.
</p>

</div>
<!-- EDIT2 SECTION "Switch Game States" [507-2043] -->
<h2 class="sectionedit3" id="get_access_to_application_and_update_loop">Get Access to Application and Update Loop</h2>
<div class="level2">

<p>
Since you are writing a jME3 application, you can additionally make any ScreenController class extend the <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AbstractAppState</a> class. 
This gives the ScreenController access to the application object and to the update loop!
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> StartScreenState <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
 
  <span class="kw1">private</span> ViewPort viewPort<span class="sy0">;</span>
  <span class="kw1">private</span> Node rootNode<span class="sy0">;</span>
  <span class="kw1">private</span> Node guiNode<span class="sy0">;</span>
  <span class="kw1">private</span> AssetManager assetManager<span class="sy0">;</span>
  <span class="kw1">private</span> Node localRootNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Start Screen RootNode"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> Node localGuiNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Start Screen GuiNode"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">final</span> ColorRGBA backgroundColor <span class="sy0">=</span> ColorRGBA.<span class="me1">Gray</span><span class="sy0">;</span>  
 
<span class="kw1">public</span> StartScreenState<span class="br0">(</span>SimpleApplication app<span class="br0">)</span><span class="br0">{</span>
    <span class="kw1">this</span>.<span class="me1">rootNode</span>     <span class="sy0">=</span> app.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">viewPort</span>     <span class="sy0">=</span> app.<span class="me1">getViewPort</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">guiNode</span>      <span class="sy0">=</span> app.<span class="me1">getGuiNode</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">assetManager</span> <span class="sy0">=</span> app.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>  
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
 
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>localRootNode<span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">attachChild</span><span class="br0">(</span>localGuiNode<span class="br0">)</span><span class="sy0">;</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>backgroundColor<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** init the screen */</span>    
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** any main loop action happens here */</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> cleanup<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    rootNode.<span class="me1">detachChild</span><span class="br0">(</span>localRootNode<span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">detachChild</span><span class="br0">(</span>localGuiNode<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">super</span>.<span class="me1">cleanup</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
</p><p></p><div class="noteimportant">It is not sufficient to just inherit from AbstractAppState. You need to instantiate your controller class, register it with app's stateManager and then pass it to nifty. See code sample below.
</div>

<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> TestNiftyGui <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
     StartScreenState startScreenState <span class="sy0">=</span> <span class="kw1">new</span> StartScreenState<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
     stateManager.<span class="me1">attach</span><span class="br0">(</span>startScreenState<span class="br0">)</span><span class="sy0">;</span>
     <span class="co1">// [...] boilerplate init nifty omitted</span>
     nifty.<span class="me1">fromXml</span><span class="br0">(</span><span class="st0">"Interface/myGui.xml"</span>, <span class="st0">"start"</span>, startScreenState<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//one of the XML screen elements needs to reference StartScreenState controller class</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Get Access to Application and Update Loop" [2044-4170] -->
<h2 class="sectionedit4" id="know_your_variables">Know Your Variables</h2>
<div class="level2">
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">Variable</th><th class="col1">Description</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">${CALL.myMethod()} </td><td class="col1"> Calls a method in the current ScreenController and gets the method's return String. The method can also be void and have a side effect, e.g. play a sound etc.</td>
	</tr>
	<tr class="row2">
		<td class="col0">${ENV.HOME}</td><td class="col1"> Returns the path to user's home directory.</td>
	</tr>
	<tr class="row3">
		<td class="col0">${ENV.key} </td><td class="col1"> Looks up <code>key</code> in the environment variables. Use it like Java's System.getEnv(“key”).</td>
	</tr>
	<tr class="row4">
		<td class="col0">${PROP.key}</td><td class="col1"> looks up <code>key</code> in the Nifty properties. Use Nifty.setGlobalproperties(properties) and Nifty.getGlobalproperties(“key”). Or SystemGetProperties(key);</td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [4203-4734] -->
<p>
See also: <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=MarkUp" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=MarkUp" rel="nofollow">http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=MarkUp</a>
</p>

</div>
<!-- EDIT4 SECTION "Know Your Variables" [4171-4817] -->
<h2 class="sectionedit6" id="use_screencontrollers_for_mutally_exclusive_functionality">Use ScreenControllers for Mutally Exclusive Functionality</h2>
<div class="level2">

<p>
Technically you are free to create one ScreenController class for each screen, or reuse the same ScreenController for all or some of them. In the end it may be best to create individual ScreenControllers for functionality that is mutually exclusive.
</p>

<p>
For example, create a <code>MyHudScreen.java</code> for the <code>hud</code> screen, and a <code>MyStartScreen.java</code> for the <code>start</code> screen.
</p>
<ul>
<li class="level1"><div class="li"> Include all user interface methods that are needed during the game (while the HUD is up) in <code>MyHudScreen.java</code>. Then make this class control all screens that can be up during the game (the HUD screen, a MiniMap screen, an Inventory screen, an Abilities or Skills screen, etc). All these screens possibly share data (game data, player data), so it makes sense to control them all with methods of the same <code>MyHudScreen.java</code> class.</div>
</li>
<li class="level1"><div class="li"> The start screen, however, is mostly independent of the running game. Include all user interface methods that are needed outside the game (while you are on the start screen) in <code>MyStartScreen.java</code>. Then make this class control all screens that can be up outside the game (the Start screen, a Settings/Options screen, a HighScore screen, etc). All these classes need to read and write saved game data, so it makes sense to control them all with methods of the same <code>MyStartScreen.java</code> class.</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Use ScreenControllers for Mutally Exclusive Functionality" [4818-6200] -->
<h2 class="sectionedit7" id="create_a_loading_screen">Create a "Loading..." Screen</h2>
<div class="level2">

<p>
Get the full <a href="/jme3/advanced/loading_screen.html" class="wikilink1" title="jme3:advanced:loading_screen">Loading Screen</a> tutorial here.
</p>

</div>
<!-- EDIT7 SECTION "Create a Loading... Screen" [6201-6305] -->
<h2 class="sectionedit8" id="create_a_popup_menu">Create a Popup Menu</h2>
<div class="level2">

<p>
Get the full <a href="/jme3/advanced/nifty_gui_popup_menu.html" class="wikilink1" title="jme3:advanced:nifty_gui_popup_menu">Nifty GUI PopUp Menu</a> tutorial here.
</p>

</div>
<!-- EDIT8 SECTION "Create a Popup Menu" [6306-6408] -->
<h2 class="sectionedit9" id="add_visual_effects">Add Visual Effects</h2>
<div class="level2">

<p>
You can register effects to screen elements.
</p>
<ul>
<li class="level1"><div class="li"> Respond to element events such as onStartScreen, onEndScreen, onHover, onFocus, onActive,</div>
</li>
<li class="level1"><div class="li"> Trigger effects that change movement, blending, size, color, fading, and much more.</div>
</li>
</ul>

<p>
Here is an example that moves a panel when the startScreen opens. You place an &lt; effect &gt; tag inside the element that you want to  be affected.
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">height</span>=<span class="st0">"25%"</span> <span class="re0">width</span>=<span class="st0">"35%"</span> ...<span class="re2">&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;effect<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;onStartScreen</span> <span class="re0">name</span>=<span class="st0">"move"</span> <span class="re0">mode</span>=<span class="st0">"in"</span> <span class="re0">direction</span>=<span class="st0">"top"</span> <span class="re0">length</span>=<span class="st0">"300"</span> <span class="re0">startDelay</span>=<span class="st0">"0"</span> <span class="re0">inherit</span>=<span class="st0">"true"</span><span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;/effect<span class="re2">&gt;</span></span></span>
<span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
Learn more from the NiftyGUI page:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Effects" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Effects" rel="nofollow">http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Effects</a></div>
</li>
</ul>

</div>
<!-- EDIT9 SECTION "Add Visual Effects" [6409-7121] -->
<h2 class="sectionedit10" id="add_sound_effects">Add Sound Effects</h2>
<div class="level2">

<p>
Playing sounds using Nifty is also possible with a <code>playSound</code> effect as trigger. Remember to first register the sound that you want to play:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;registerSound</span> <span class="re0">id</span>=<span class="st0">"myclick"</span> <span class="re0">filename</span>=<span class="st0">"Interface/sounds/ButtonClick.ogg"</span> <span class="re2">/&gt;</span></span>
...
<span class="sc3"><span class="re1">&lt;label<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;effect<span class="re2">&gt;</span></span></span>
    <span class="sc3"><span class="re1">&lt;onClick</span> <span class="re0">name</span>=<span class="st0">"playSound"</span> <span class="re0">sound</span>=<span class="st0">"myclick"</span><span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;/effect<span class="re2">&gt;</span></span></span>
<span class="sc3"><span class="re1">&lt;/label<span class="re2">&gt;</span></span></span></pre>

</div>
<!-- EDIT10 SECTION "Add Sound Effects" [7122-7484] -->
<h2 class="sectionedit11" id="pass_clickloc_from_nifty_to_java">Pass ClickLoc From Nifty to Java</h2>
<div class="level2">

<p>
After a mouse click, you may want to record the 2D clickLoc and send this info to your Java application. Typical ScreenController methods however only have a String argument. You'd have to convert the String to ints.
</p>

<p>
To pass the clickLoc as two ints, you can use the special <code>(int x, int y)</code> syntax in the ScreenController:
</p>
<pre class="code java">  <span class="kw1">public</span> <span class="kw4">void</span> clicked<span class="br0">(</span><span class="kw4">int</span> x, <span class="kw4">int</span> y<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">// here you can use the x and y of the clickLoc</span>
  <span class="br0">}</span></pre>

<p>
In the Nifty <abbr title="Graphical User Interface">GUI</abbr> screen code (e.g. XML file) you must call the <code>(int x, int y)</code> method <em>without</em> any parameters! 
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;interact</span> <span class="re0">onClick</span>=<span class="st0">"clicked()"</span><span class="re2">/&gt;</span></span>  </pre>

<p>
You can name the method (here <code>clicked</code>) what ever you like, as long as you keep the argument syntax.
</p>

</div>
<!-- EDIT11 SECTION "Pass ClickLoc From Nifty to Java" [7485-8246] -->
<h2 class="sectionedit12" id="load_several_xml_files">Load Several XML Files</h2>
<div class="level2">

<p>
The basic Nifty <abbr title="Graphical User Interface">GUI</abbr> example showed how to use the <code>nifty.fromXML()</code> method to load one XML file containing all Nifty <abbr title="Graphical User Interface">GUI</abbr> screens.
The following code sample shows how you can load several XML files into one nifty object. Loading several files with <code>nifty.addXml()</code> allows you to split up each screen into one XML file, instead of all into one hard-to-read XML file. 
</p>
<pre class="code java">NiftyJmeDisplay niftyDisplay <span class="sy0">=</span> <span class="kw1">new</span> NiftyJmeDisplay<span class="br0">(</span>assetManager, inputManager, audioRenderer, viewPort<span class="br0">)</span><span class="sy0">;</span>
Nifty nifty <span class="sy0">=</span> niftyDisplay.<span class="me1">getNifty</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
nifty.<span class="me1">addXml</span><span class="br0">(</span><span class="st0">"Interface/Screens/OptionsScreen.xml"</span><span class="br0">)</span><span class="sy0">;</span>
nifty.<span class="me1">addXml</span><span class="br0">(</span><span class="st0">"Interface/Screens/StartScreen.xml"</span><span class="br0">)</span><span class="sy0">;</span>
nifty.<span class="me1">gotoScreen</span><span class="br0">(</span><span class="st0">"startScreen"</span><span class="br0">)</span><span class="sy0">;</span>
StartScreenControl screenControl <span class="sy0">=</span> <span class="br0">(</span>StartScreenControl<span class="br0">)</span> nifty.<span class="me1">getScreen</span><span class="br0">(</span><span class="st0">"startScreen"</span><span class="br0">)</span>.<span class="me1">getScreenController</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
OptionsScreenControl optionsControl <span class="sy0">=</span> <span class="br0">(</span>OptionsScreenControl<span class="br0">)</span> nifty.<span class="me1">getScreen</span><span class="br0">(</span><span class="st0">"optionsScreen"</span><span class="br0">)</span>.<span class="me1">getScreenController</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
stateManager.<span class="me1">attach</span><span class="br0">(</span>screenControl<span class="br0">)</span><span class="sy0">;</span>
stateManager.<span class="me1">attach</span><span class="br0">(</span>optionsControl<span class="br0">)</span><span class="sy0">;</span>
guiViewPort.<span class="me1">addProcessor</span><span class="br0">(</span>niftyDisplay<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT12 SECTION "Load Several XML Files" [8247-9295] -->
<h2 class="sectionedit13" id="register_additional_explicit_screen_controllers">Register additional explicit screen controllers</h2>
<div class="level2">

<p>
In addition to the <code>nifty.addXml()</code> methods to attach many nifty XML files, there exists a <code>nifty.registerScreenController()</code> method to explicitly attach more screen controllers. 
</p>

<p>
The following code sample shows how you can explicitly attach several screen controllers before adding the XML file to nifty, which would otherwise cause nifty to implicitly instantiate the screen controller class. 
</p>
<pre class="code java">NiftyJmeDisplay niftyDisplay <span class="sy0">=</span> <span class="kw1">new</span> NiftyJmeDisplay<span class="br0">(</span>assetManager, inputManager, audioRenderer, viewPort<span class="br0">)</span><span class="sy0">;</span>
Nifty nifty <span class="sy0">=</span> niftyDisplay.<span class="me1">getNifty</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
nifty.<span class="me1">registerScreenController</span><span class="br0">(</span><span class="kw1">new</span> OptionsScreenController<span class="br0">(</span>randomConstructorArgument<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
nifty.<span class="me1">addXml</span><span class="br0">(</span><span class="st0">"Interface/Screens/OptionsScreen.xml"</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT13 SECTION "Register additional explicit screen controllers" [9296-10064] -->
<h2 class="sectionedit14" id="design_your_own_styles">Design Your Own Styles</h2>
<div class="level2">

<p>
By default, your Nifty XML screens use the built.in styles:
</p>
<pre class="code xml"> <span class="sc3"><span class="re1">&lt;useStyles</span> <span class="re0">filename</span>=<span class="st0">"nifty-default-styles.xml"</span> <span class="re2">/&gt;</span></span> </pre>

<p>
But you can switch to a set of custom styles in your game project's asset directory like this:
</p>
<pre class="code xml"> <span class="sc3"><span class="re1">&lt;useStyles</span> <span class="re0">filename</span>=<span class="st0">"Interface/Styles/myCustomStyles.xml"</span> <span class="re2">/&gt;</span></span> </pre>

<p>
Inside myCustomStyles.xml you define styles like this:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;?xml</span> <span class="re0">version</span>=<span class="st0">"1.0"</span> <span class="re0">encoding</span>=<span class="st0">"UTF-8"</span><span class="re2">?&gt;</span></span>
<span class="sc3"><span class="re1">&lt;nifty-styles<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;useStyles</span> <span class="re0">filename</span>=<span class="st0">"Interface/Styles/Font/myCustomFontStyle.xml"</span> <span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;useStyles</span> <span class="re0">filename</span>=<span class="st0">"Interface/Styles/Button/myCustomButtonStyle.xml"</span> <span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;useStyles</span> <span class="re0">filename</span>=<span class="st0">"Interface/Styles/Label/myCustomLabelStyle.xml"</span> <span class="re2">/&gt;</span></span>
  ...
<span class="sc3"><span class="re1">&lt;/nifty-styles<span class="re2">&gt;</span></span></span></pre>

<p>
Learn more about how to create styles by looking at the <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Build_from_Source" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Build_from_Source" rel="nofollow">Nifty GUI source code</a> for “nifty-style-black”. Copy it as a template and change it to create your own style.
</p>
<hr />

<p>
Learn more from the NiftyGUI page:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Effects" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Effects" rel="nofollow">http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Effects</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/nifty.html" class="wikilink1" title="tag:nifty" rel="tag">nifty</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>,
	<a href="/tag/click.html" class="wikilink1" title="tag:click" rel="tag">click</a>,
	<a href="/tag/state.html" class="wikilink1" title="tag:state" rel="tag">state</a>,
	<a href="/tag/states.html" class="wikilink1" title="tag:states" rel="tag">states</a>,
	<a href="/tag/sound.html" class="wikilink1" title="tag:sound" rel="tag">sound</a>,
	<a href="/tag/effect.html" class="wikilink1" title="tag:effect" rel="tag">effect</a>
</span></div>

</div>
<!-- EDIT14 SECTION "Design Your Own Styles" [10065-] -->
