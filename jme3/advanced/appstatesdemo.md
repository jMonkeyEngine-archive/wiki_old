---
title: Simple AppStates Demo
---
<h1 class="sectionedit1" id="simple_appstates_demo">Simple AppStates Demo</h1>
<div class="level1">

<p>
</p><p></p><div class="noteimportant">
THIS DEMO IS OUT OF DATE AND NEEDS CORRECTING

</div>


</div>
<!-- EDIT1 SECTION "Simple AppStates Demo" [1-108] -->
<h1 class="sectionedit2" id="this_demo_is_out_of_date_and_needs_correcting_for_now_please_see">THIS DEMO IS OUT OF DATE AND NEEDS CORRECTING FOR NOW PLEASE SEE</h1>
<div class="level1">

<p>
 <a href="http://jmonkeyengine.org/wiki/doku.php/jme3:advanced:application_states" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:advanced:application_states" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jme3:advanced:application_states</a>
</p>

<p>
Note: this tutorial needs to be fixed and is currently not correct.  One should almost never override stateDetached and stateAttached… and should certainly never do anything scene related in them.
</p>

<p>
This demo is a simple example of how you use AppStates to toggle between a StartScreen and a SettingsScreen (press RETURN) while the game is paused, and start the game by switching to a GameRunning state (press BACKSPACE). 
</p>

<p>
There are four files, Main.java, GameRunningState.java, StartScreenState.java, SettingsScreenState.java. 
</p>

</div>
<!-- EDIT2 SECTION "THIS DEMO IS OUT OF DATE AND NEEDS CORRECTING FOR NOW PLEASE SEE" [109-793] -->
<h2 class="sectionedit3" id="mainjava">Main.java</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">chapter04.appstatedemo</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.KeyInput</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.ActionListener</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.KeyTrigger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.input.controls.Trigger</span><span class="sy0">;</span>
 
<span class="co3">/**
 * This demo shows a simple "game" with three AppStates. Instead of game content, 
 * it just displays three cubes on different backgrounds.
 * &lt;ul&gt;
 * &lt;li&gt;StartScreenState: This state is enabled 
 *     when the user starts the application, or the the game is paused. 
 *     Press BACKSPACE to return to the game, press RETURN to go to Settings.&lt;/li&gt;
 * &lt;li&gt;GameRunningState: This state shows the game content and is enabled while the game is running. 
 *     Press BACKSPACE to pause and return to the start screen.&lt;/li&gt;
 * &lt;li&gt;SettingsScreenState: This Settings screen state can be reached from the start screen
 *     Press RETURN to toggle it on and off.&lt;/li&gt;
 * &lt;/ul&gt;
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> Main <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
  <span class="kw1">private</span> Trigger pause_trigger <span class="sy0">=</span> <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_BACK</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> Trigger save_trigger <span class="sy0">=</span> <span class="kw1">new</span> KeyTrigger<span class="br0">(</span>KeyInput.<span class="me1">KEY_RETURN</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw4">boolean</span> isRunning <span class="sy0">=</span> <span class="kw2">false</span><span class="sy0">;</span> <span class="co1">// starts at startscreen</span>
  <span class="kw1">private</span> GameRunningState gameRunningState<span class="sy0">;</span>
  <span class="kw1">private</span> StartScreenState startScreenState<span class="sy0">;</span>
  <span class="kw1">private</span> SettingsScreenState settingsScreenState<span class="sy0">;</span>
 
 
  <span class="co3">/** Start the jMonkeyEngine application */</span>
  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    Main app <span class="sy0">=</span> <span class="kw1">new</span> Main<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="co3">/**
   * initialize the scene here
   */</span>
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    setDisplayFps<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
    setDisplayStatView<span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
 
    gameRunningState    <span class="sy0">=</span> <span class="kw1">new</span> GameRunningState<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
    startScreenState    <span class="sy0">=</span> <span class="kw1">new</span> StartScreenState<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
    settingsScreenState <span class="sy0">=</span> <span class="kw1">new</span> SettingsScreenState<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
 
    stateManager.<span class="me1">attach</span><span class="br0">(</span>startScreenState<span class="br0">)</span><span class="sy0">;</span>
 
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Game Pause Unpause"</span>, pause_trigger<span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="st0">"Game Pause Unpause"</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Toggle Settings"</span>, save_trigger<span class="br0">)</span><span class="sy0">;</span>
    inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="st0">"Toggle Settings"</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a> actionListener <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+actionlistener"><span class="kw3">ActionListener</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, <span class="kw4">boolean</span> isPressed, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
      <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"key"</span> <span class="sy0">+</span> name<span class="br0">)</span><span class="sy0">;</span>
      <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Game Pause Unpause"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>isPressed<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>isRunning<span class="br0">)</span> <span class="br0">{</span>
          stateManager.<span class="me1">detach</span><span class="br0">(</span>gameRunningState<span class="br0">)</span><span class="sy0">;</span>
          stateManager.<span class="me1">attach</span><span class="br0">(</span>startScreenState<span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"switching to startscreen..."</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
          stateManager.<span class="me1">detach</span><span class="br0">(</span>startScreenState<span class="br0">)</span><span class="sy0">;</span>
          stateManager.<span class="me1">attach</span><span class="br0">(</span>gameRunningState<span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"switching to game..."</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        isRunning <span class="sy0">=</span> <span class="sy0">!</span>isRunning<span class="sy0">;</span>
      <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>name.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Toggle Settings"</span><span class="br0">)</span> <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>isPressed <span class="sy0">&amp;&amp;</span> <span class="sy0">!</span>isRunning<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>isRunning <span class="sy0">&amp;&amp;</span> stateManager.<span class="me1">hasState</span><span class="br0">(</span>startScreenState<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          stateManager.<span class="me1">detach</span><span class="br0">(</span>startScreenState<span class="br0">)</span><span class="sy0">;</span>
          stateManager.<span class="me1">attach</span><span class="br0">(</span>settingsScreenState<span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"switching to settings..."</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>isRunning <span class="sy0">&amp;&amp;</span> stateManager.<span class="me1">hasState</span><span class="br0">(</span>settingsScreenState<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
          stateManager.<span class="me1">detach</span><span class="br0">(</span>settingsScreenState<span class="br0">)</span><span class="sy0">;</span>
          stateManager.<span class="me1">attach</span><span class="br0">(</span>startScreenState<span class="br0">)</span><span class="sy0">;</span>
          <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"switching to startscreen..."</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
      <span class="br0">}</span>
    <span class="br0">}</span>
  <span class="br0">}</span><span class="sy0">;</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span><span class="br0">}</span>
 
<span class="br0">}</span>
 </pre>

</div>
<!-- EDIT3 SECTION "Main.java" [794-4202] -->
<h2 class="sectionedit4" id="gamerunningstatejava">GameRunningState.java</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">chapter04.appstatedemo</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapFont</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapText</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.ViewPort</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/**
 * A template how to create an Application State. This example state simply
 * changes the background color depending on the camera position.
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> GameRunningState <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
 
  <span class="kw1">private</span> ViewPort viewPort<span class="sy0">;</span>
  <span class="kw1">private</span> Node rootNode<span class="sy0">;</span>
  <span class="kw1">private</span> Node guiNode<span class="sy0">;</span>
  <span class="kw1">private</span> AssetManager assetManager<span class="sy0">;</span>
  <span class="kw1">private</span> Node localRootNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Game Screen RootNode"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> Node localGuiNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Game Screen GuiNode"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">final</span> ColorRGBA backgroundColor <span class="sy0">=</span> ColorRGBA.<span class="me1">Blue</span><span class="sy0">;</span>
 
  <span class="kw1">public</span> GameRunningState<span class="br0">(</span>SimpleApplication app<span class="br0">)</span><span class="br0">{</span>
    <span class="kw1">this</span>.<span class="me1">rootNode</span>     <span class="sy0">=</span> app.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">viewPort</span>      <span class="sy0">=</span> app.<span class="me1">getViewPort</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">guiNode</span>       <span class="sy0">=</span> app.<span class="me1">getGuiNode</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">assetManager</span>  <span class="sy0">=</span> app.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>  
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** Load this scene */</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>backgroundColor<span class="br0">)</span><span class="sy0">;</span>
 
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, mesh<span class="br0">)</span><span class="sy0">;</span>
    Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
            <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
    geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
    geom.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    localRootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** Load the HUD*/</span>
    BitmapFont guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span>
            <span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
    BitmapText displaytext <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont<span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">move</span><span class="br0">(</span><span class="nu0">10</span>, displaytext.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="nu0">20</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Game running. Press BACKSPACE to pause and return to the start screen."</span><span class="br0">)</span><span class="sy0">;</span>
    localGuiNode.<span class="me1">attachChild</span><span class="br0">(</span>displaytext<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** the action happens here */</span>
    Vector3f v <span class="sy0">=</span> viewPort.<span class="me1">getCamera</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getLocation</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span><span class="kw1">new</span> ColorRGBA<span class="br0">(</span>v.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">10</span>, v.<span class="me1">getY</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">10</span>, v.<span class="me1">getZ</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">/</span> <span class="nu0">10</span>, <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"Box"</span><span class="br0">)</span>.<span class="me1">rotate</span><span class="br0">(</span>tpf, tpf, tpf<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> stateAttached<span class="br0">(</span>AppStateManager stateManager<span class="br0">)</span> <span class="br0">{</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>localRootNode<span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">attachChild</span><span class="br0">(</span>localGuiNode<span class="br0">)</span><span class="sy0">;</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>backgroundColor<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> stateDetached<span class="br0">(</span>AppStateManager stateManager<span class="br0">)</span> <span class="br0">{</span>
    rootNode.<span class="me1">detachChild</span><span class="br0">(</span>localRootNode<span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">detachChild</span><span class="br0">(</span>localGuiNode<span class="br0">)</span><span class="sy0">;</span>
 
  <span class="br0">}</span>
 
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "GameRunningState.java" [4203-7170] -->
<h2 class="sectionedit5" id="settingsscreenstatejava">SettingsScreenState.java</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">chapter04.appstatedemo</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapFont</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapText</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.ViewPort</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/**
 * A template how to create an Application State. This example state simply
 * changes the background color depending on the camera position.
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> SettingsScreenState <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
 
  <span class="kw1">private</span> ViewPort viewPort<span class="sy0">;</span>
  <span class="kw1">private</span> Node rootNode<span class="sy0">;</span>
  <span class="kw1">private</span> Node guiNode<span class="sy0">;</span>
  <span class="kw1">private</span> AssetManager assetManager<span class="sy0">;</span>
  <span class="kw1">private</span> Node localRootNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Settings Screen RootNode"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> Node localGuiNode <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Settings Screen GuiNode"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="kw1">private</span> <span class="kw1">final</span> ColorRGBA backgroundColor <span class="sy0">=</span> ColorRGBA.<span class="me1">DarkGray</span><span class="sy0">;</span>
 
  <span class="kw1">public</span> SettingsScreenState<span class="br0">(</span>SimpleApplication app<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">this</span>.<span class="me1">rootNode</span>     <span class="sy0">=</span> app.<span class="me1">getRootNode</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">viewPort</span>      <span class="sy0">=</span> app.<span class="me1">getViewPort</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">guiNode</span>       <span class="sy0">=</span> app.<span class="me1">getGuiNode</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">this</span>.<span class="me1">assetManager</span>  <span class="sy0">=</span> app.<span class="me1">getAssetManager</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** Load this scene */</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>backgroundColor<span class="br0">)</span><span class="sy0">;</span>
 
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">1</span>, <span class="sy0">-</span><span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span>, .5f, .5f, .5f<span class="br0">)</span><span class="sy0">;</span>
    Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, mesh<span class="br0">)</span><span class="sy0">;</span>
    Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
            <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
    geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
    geom.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    localRootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** Load the HUD */</span>
    BitmapFont guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span>
            <span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
    BitmapText displaytext <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont<span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">move</span><span class="br0">(</span><span class="nu0">10</span>, displaytext.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="nu0">20</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Settings screen. Press RETURN to save "</span>
            <span class="sy0">+</span> <span class="st0">"and return to start screen."</span><span class="br0">)</span><span class="sy0">;</span>
    localGuiNode.<span class="me1">attachChild</span><span class="br0">(</span>displaytext<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
     <span class="co3">/** the action happens here */</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> stateAttached<span class="br0">(</span>AppStateManager stateManager<span class="br0">)</span> <span class="br0">{</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>localRootNode<span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">attachChild</span><span class="br0">(</span>localGuiNode<span class="br0">)</span><span class="sy0">;</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>backgroundColor<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> stateDetached<span class="br0">(</span>AppStateManager stateManager<span class="br0">)</span> <span class="br0">{</span>
    rootNode.<span class="me1">detachChild</span><span class="br0">(</span>localRootNode<span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">detachChild</span><span class="br0">(</span>localGuiNode<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
<span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "SettingsScreenState.java" [7171-9985] -->
<h2 class="sectionedit6" id="startscreenstatejava">StartScreenState.java</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">chapter04.appstatedemo</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapFont</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapText</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.ViewPort</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/**
 * A template how to create an Application State. This example state simply
 * changes the background color depending on the camera position.
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> StartScreenState <span class="kw1">extends</span> AbstractAppState <span class="br0">{</span>
 
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
 
    <span class="co3">/** Init this scene */</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>backgroundColor<span class="br0">)</span><span class="sy0">;</span>
 
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span>, .5f,.5f,.5f<span class="br0">)</span><span class="sy0">;</span>
    Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, mesh<span class="br0">)</span><span class="sy0">;</span>
    Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
            <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Yellow</span><span class="br0">)</span><span class="sy0">;</span>
    geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
    geom.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    localRootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="co3">/** Load a HUD */</span>
    BitmapFont guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span>
            <span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
    BitmapText displaytext <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont<span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">move</span><span class="br0">(</span> <span class="nu0">10</span>, displaytext.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="nu0">20</span>,  <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    displaytext.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Start screen. Press BACKSPACE to resume the game, "</span>
            <span class="sy0">+</span> <span class="st0">"press RETURN to edit Settings."</span><span class="br0">)</span><span class="sy0">;</span>
    localGuiNode.<span class="me1">attachChild</span><span class="br0">(</span>displaytext<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="co3">/** the action happens here */</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> stateAttached<span class="br0">(</span>AppStateManager stateManager<span class="br0">)</span> <span class="br0">{</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>localRootNode<span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">attachChild</span><span class="br0">(</span>localGuiNode<span class="br0">)</span><span class="sy0">;</span>
    viewPort.<span class="me1">setBackgroundColor</span><span class="br0">(</span>backgroundColor<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
  @Override
  <span class="kw1">public</span> <span class="kw4">void</span> stateDetached<span class="br0">(</span>AppStateManager stateManager<span class="br0">)</span> <span class="br0">{</span>
    rootNode.<span class="me1">detachChild</span><span class="br0">(</span>localRootNode<span class="br0">)</span><span class="sy0">;</span>
    guiNode.<span class="me1">detachChild</span><span class="br0">(</span>localGuiNode<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
 
<span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "StartScreenState.java" [9986-] -->
