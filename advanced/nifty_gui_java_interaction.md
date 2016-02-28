---
title: Interacting with the GUI from Java
---
<h1 class="sectionedit1" id="interacting_with_the_gui_from_java">Interacting with the GUI from Java</h1>
<div class="level1">
<ol>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui.html" class="wikilink1" title="jme3:advanced:nifty_gui">Nifty GUI Concepts</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_best_practices.html" class="wikilink1" title="jme3:advanced:nifty_gui_best_practices">Nifty GUI Best Practices</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_xml_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_xml_layout">Nifty GUI XML Layout</a> or <a href="/jme3/advanced/nifty_gui_java_layout.html" class="wikilink1" title="jme3:advanced:nifty_gui_java_layout">Nifty GUI Java Layout</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_overlay.html" class="wikilink1" title="jme3:advanced:nifty_gui_overlay">Nifty GUI Overlay</a> or <a href="/jme3/advanced/nifty_gui_projection.html" class="wikilink1" title="jme3:advanced:nifty_gui_projection">Nifty GUI Projection</a></div>
</li>
<li class="level1"><div class="li"> <strong>Nifty <abbr title="Graphical User Interface">GUI</abbr> Java Interaction</strong></div>
</li>
</ol>

<p>
In the previous parts of the tutorial, you created a two-screen user interface. But it is still static, and when you click the buttons, nothing happens yet. The purpose of the <abbr title="Graphical User Interface">GUI</abbr> is to communicate with your Java classes: Your game needs to know what the users clicked, which settings they chose, which values they entered into a field, etc. Similarly, the user needs to know what the currently game state is (score, health, etc). 
</p>

</div>
<!-- EDIT1 SECTION "Interacting with the GUI from Java" [1-791] -->
<h2 class="sectionedit2" id="connect_gui_to_java_controller">Connect GUI to Java Controller</h2>
<div class="level2">

<p>
To let a Nifty screen communicate with the Java application, you register a <code>ScreenController</code> to every NiftyGUI screen. You create a ScreenController by creating a Java class that implements the <code>de.lessvoid.nifty.screen.ScreenController</code> interface and its abstract methods.
</p>

<p>
Create an AppState <strong>MyStartScreen</strong>.java file in your package. ( Rightclick on your package → New → Other… → JME3 Classes → New AppState)
</p>

<p>
<strong>Pro Tip:</strong> Since you are writing a jME3 application, you can additionally make the ScreenController class extend the <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">AbstractAppState</a> class! This gives the ScreenController access to the application object and to the update loop!
</p>

<p>
Now add <strong>implements ScreenController</strong> to <em>public class MyStartScreen extends AbstractAppState{</em> and add <strong>import de.lessvoid.nifty.screen.ScreenController;</strong>
</p>

<p>
Continue with adding:
</p>
<pre class="code java"><span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.screen.Screen</span><span class="sy0">;</span>
 
...
 
<span class="kw1">public</span> <span class="kw4">void</span> bind<span class="br0">(</span>Nifty nifty, Screen screen<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">throw</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+unsupportedoperationexception"><span class="kw3">UnsupportedOperationException</span></a><span class="br0">(</span><span class="st0">"Not supported yet."</span><span class="br0">)</span><span class="sy0">;</span> 
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> onStartScreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">throw</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+unsupportedoperationexception"><span class="kw3">UnsupportedOperationException</span></a><span class="br0">(</span><span class="st0">"Not supported yet."</span><span class="br0">)</span><span class="sy0">;</span> 
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> onEndScreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">throw</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+unsupportedoperationexception"><span class="kw3">UnsupportedOperationException</span></a><span class="br0">(</span><span class="st0">"Not supported yet."</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>
<pre class="code java"><span class="coMULTI">/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */</span>
<span class="kw1">package</span> <span class="co2">mygame</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.Application</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AbstractAppState</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.state.AppStateManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.Nifty</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.screen.Screen</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">de.lessvoid.nifty.screen.ScreenController</span><span class="sy0">;</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> MyStartScreen <span class="kw1">extends</span> AbstractAppState <span class="kw1">implements</span> ScreenController <span class="br0">{</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> initialize<span class="br0">(</span>AppStateManager stateManager, Application app<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">initialize</span><span class="br0">(</span>stateManager, app<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//TODO: initialize your AppState, e.g. attach spatials to rootNode</span>
        <span class="co1">//this is called on the OpenGL thread after the AppState has been attached</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">//TODO: implement behavior during runtime</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> cleanup<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">cleanup</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//TODO: clean up what you initialized in the initialize method,</span>
        <span class="co1">//e.g. remove all spatials from rootNode</span>
        <span class="co1">//this is called on the OpenGL thread after the AppState has been detached</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> bind<span class="br0">(</span>Nifty nifty, Screen screen<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">throw</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+unsupportedoperationexception"><span class="kw3">UnsupportedOperationException</span></a><span class="br0">(</span><span class="st0">"Not supported yet."</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onStartScreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">throw</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+unsupportedoperationexception"><span class="kw3">UnsupportedOperationException</span></a><span class="br0">(</span><span class="st0">"Not supported yet."</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> onEndScreen<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">throw</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+unsupportedoperationexception"><span class="kw3">UnsupportedOperationException</span></a><span class="br0">(</span><span class="st0">"Not supported yet."</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
The name and package of your custom ScreenController class (here <code>mygame.MyStartScreen</code>) goes into the controller parameter of the respective XML screen it belongs to. For example:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;nifty<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;screen</span> <span class="re0">id</span>=<span class="st0">"start"</span> <span class="re0">controller</span>=<span class="st0">"mygame.MyStartScreen"</span><span class="re2">&gt;</span></span>
      <span class="sc-1">&lt;!-- layer and panel code ... --&gt;</span>
  <span class="sc3"><span class="re1">&lt;/screen<span class="re2">&gt;</span></span></span>
<span class="sc3"><span class="re1">&lt;/nifty<span class="re2">&gt;</span></span></span></pre>

<p>
Or the same in a Java syntax, respectively:
</p>
<pre class="code java">  nifty.<span class="me1">addScreen</span><span class="br0">(</span><span class="st0">"start"</span>, <span class="kw1">new</span> ScreenBuilder<span class="br0">(</span><span class="st0">"start"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
      controller<span class="br0">(</span><span class="kw1">new</span> mygame.<span class="me1">MyStartScreen</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Now the Java class <code>MyStartScreen</code> and this <abbr title="Graphical User Interface">GUI</abbr> screen (<code>start</code>) are connected. For this example you can also connect the <code>hud</code> screen to MyStartScreen.
</p>

</div>
<!-- EDIT2 SECTION "Connect GUI to Java Controller" [792-4282] -->
<h2 class="sectionedit3" id="make_gui_and_java_interact">Make GUI and Java Interact</h2>
<div class="level2">

<p>
In most cases, you will want to pass game data in and out of the ScreenController. Note that you can pass any custom arguments from your Java class into your ScreenController constructor (<code>public MyStartScreen(GameData data) {}</code>).
</p>

<p>
Use any combination of the three following approaches to make Java classes interact with the <abbr title="Graphical User Interface">GUI</abbr>.
</p>

</div>
<!-- EDIT3 SECTION "Make GUI and Java Interact" [4283-4655] -->
<h3 class="sectionedit4" id="gui_calls_a_void_java_method">GUI Calls a Void Java Method</h3>
<div class="level3">

<p>
This is how you respond to an <abbr title="Graphical User Interface">GUI</abbr> interaction such as clicks in XML GUIs:
</p>
<ol>
<li class="level1"><div class="li"> Add <code>visibleToMouse=“true”</code> to the parent element!</div>
</li>
<li class="level1"><div class="li"> Embed the <code>&lt;interact /&gt;</code> element into the parent element. </div>
</li>
<li class="level1"><div class="li"> Specify the Java methods that you want to call when the users performs certain actions, such as clicking. <br />
Example: <code>&lt;interact onClick=“startGame(hud)” /&gt;</code></div>
</li>
</ol>

<p>
Or this is how you respond to an <abbr title="Graphical User Interface">GUI</abbr> interaction such as clicks in Java GUIs:
</p>
<ol>
<li class="level1"><div class="li"> Add <code>visibleToMouse(true);</code> to the parent element!</div>
</li>
<li class="level1"><div class="li"> Embed one of the <code>interact…()</code> elements into the parent element</div>
</li>
<li class="level1"><div class="li"> Specify the Java method that you want to call after the interaction. <br />
Example: <code>interactOnClick(“startGame(hud)”);</code></div>
</li>
</ol>

<p>
In the following example, we call the <code>startGame()</code> method when the player clicks the Start button, and <code>quitGame()</code> when the player clicks the Quit button.
</p>
<pre class="code xml">        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom_left"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>  
          <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"button"</span> <span class="re0">label</span>=<span class="st0">"Start"</span> <span class="re0">id</span>=<span class="st0">"StartButton"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> </span>
<span class="sc3">          <span class="re0">visibleToMouse</span>=<span class="st0">"true"</span> <span class="re2">&gt;</span></span> 
            <span class="sc3"><span class="re1">&lt;interact</span> <span class="re0">onClick</span>=<span class="st0">"startGame(hud)"</span><span class="re2">/&gt;</span></span>
          <span class="sc3"><span class="re1">&lt;/control<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span>
 
        <span class="sc3"><span class="re1">&lt;panel</span> <span class="re0">id</span>=<span class="st0">"panel_bottom_right"</span> <span class="re0">height</span>=<span class="st0">"50%"</span> <span class="re0">width</span>=<span class="st0">"50%"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> <span class="re0">childLayout</span>=<span class="st0">"center"</span><span class="re2">&gt;</span></span>  
          <span class="sc3"><span class="re1">&lt;control</span> <span class="re0">name</span>=<span class="st0">"button"</span> <span class="re0">label</span>=<span class="st0">"Quit"</span> <span class="re0">id</span>=<span class="st0">"QuitButton"</span> <span class="re0">align</span>=<span class="st0">"center"</span> <span class="re0">valign</span>=<span class="st0">"center"</span> </span>
<span class="sc3">          <span class="re0">visibleToMouse</span>=<span class="st0">"true"</span> <span class="re2">&gt;</span></span> 
            <span class="sc3"><span class="re1">&lt;interact</span> <span class="re0">onClick</span>=<span class="st0">"quitGame()"</span><span class="re2">/&gt;</span></span>
          <span class="sc3"><span class="re1">&lt;/control<span class="re2">&gt;</span></span></span>
        <span class="sc3"><span class="re1">&lt;/panel<span class="re2">&gt;</span></span></span></pre>

<p>
Or the same in a Java syntax, respectively:
</p>
<pre class="code java">control<span class="br0">(</span><span class="kw1">new</span> ButtonBuilder<span class="br0">(</span><span class="st0">"StartButton"</span>, <span class="st0">"Start"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
  alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
  width<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
  visibleToMouse<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  interactOnClick<span class="br0">(</span><span class="st0">"startGame(hud)"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
...
 
<span class="me1">control</span><span class="br0">(</span><span class="kw1">new</span> ButtonBuilder<span class="br0">(</span><span class="st0">"QuitButton"</span>, <span class="st0">"Quit"</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
  alignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  valignCenter<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
  height<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
  width<span class="br0">(</span><span class="st0">"50%"</span><span class="br0">)</span><span class="sy0">;</span>
  visibleToMouse<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  interactOnClick<span class="br0">(</span><span class="st0">"quitGame()"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Back in the MyStartScreen class, you specify what the <code>startGame()</code> and <code>quitGame()</code> methods do. As you see, you can pass String arguments (here <code>hud</code>) in the method call. You also see that you have access to the app object.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyStartScreen <span class="kw1">implements</span> ScreenController <span class="br0">{</span>
  ...
 
  <span class="co3">/** custom methods */</span> 
  <span class="kw1">public</span> <span class="kw4">void</span> startGame<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> nextScreen<span class="br0">)</span> <span class="br0">{</span>
    nifty.<span class="me1">gotoScreen</span><span class="br0">(</span>nextScreen<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// switch to another screen</span>
    <span class="co1">// start the game and do some more stuff...</span>
  <span class="br0">}</span>
 
  <span class="kw1">public</span> <span class="kw4">void</span> quitGame<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    app.<span class="me1">stop</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> 
  <span class="br0">}</span>
 
  ...
<span class="br0">}</span></pre>

<p>
The startGame() example simply switches the <abbr title="Graphical User Interface">GUI</abbr> to the <code>hud</code> screen when the user clicks Start. Of course, in a real game, you would perform more steps here: Load the game level, switch to in-game input and navigation handling, set a custom <code>running</code> boolean to true, attach custom in-game AppStates – and lots more.
</p>

<p>
The quitGame() example shows that you have access to the application <code>app</code> object because you made the ScreenController extend AbstractAppState.  (If you're creating code from this example, note that you'll need to make sure <code>app</code> is initialized before you can successfully call its methods.)
</p>

</div>
<!-- EDIT4 SECTION "GUI Calls a Void Java Method" [4656-7832] -->
<h3 class="sectionedit5" id="gui_gets_return_value_from_java_method">GUI Gets Return Value from Java Method</h3>
<div class="level3">

<p>
When the Nifty <abbr title="Graphical User Interface">GUI</abbr> is initialized, you can get data from Java. In this example, the Java class <code>getPlayerName()</code> in <code>MyStartScreen</code> defines the Text that is displayed in the textfield before the words <code>'s Cool Game</code>. 
</p>

<p>
First define a Java method in the screen controller, in this example, <code>getPlayerName()</code>.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MySettingsScreen <span class="kw1">implements</span> ScreenController <span class="br0">{</span>
  ...
  <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> getPlayerName<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    <span class="kw1">return</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"user.name"</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Nifty uses <code>${CALL.getPlayerName()}</code> to get the return value of the getPlayerName() method from your ScreenController Java class.
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;text</span> <span class="re0">text</span>=<span class="st0">"${CALL.getPlayerName()}'s Cool Game"</span> <span class="re0">font</span>=<span class="st0">"Interface/Fonts/Default.fnt"</span> <span class="re0">width</span>=<span class="st0">"100%"</span> <span class="re0">height</span>=<span class="st0">"100%"</span> <span class="re2">/&gt;</span></span></pre>

<p>
Or the same in a Java syntax, respectively:
</p>
<pre class="code java">text<span class="br0">(</span><span class="kw1">new</span> TextBuilder<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span><span class="br0">{</span>
  text<span class="br0">(</span><span class="st0">"${CALL.getPlayerName()}'s Cool Game"</span><span class="br0">)</span><span class="sy0">;</span>
  font<span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
  height<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
  width<span class="br0">(</span><span class="st0">"100%"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span><span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
You can use this for Strings and numeric values (e.g. when you read settings from a file, you display the results in the <abbr title="Graphical User Interface">GUI</abbr>) and also for methods with side effects.
</p>

</div>
<!-- EDIT5 SECTION "GUI Gets Return Value from Java Method" [7833-9020] -->
<h3 class="sectionedit6" id="java_modifies_nifty_elements_and_events">Java Modifies Nifty Elements and Events</h3>
<div class="level3">

<p>
You can also alter the appearance and functions of your nifty elements from Java. Make certain that the element that you want to alter has its <code>id=“name”</code> attribute set, so you can identy and address it.
</p>

<p>
Here's an example of how to change an image called <code>playerhealth</code>:
</p>
<pre class="code java"><span class="co1">// load or create new image</span>
NiftyImage img <span class="sy0">=</span> nifty.<span class="me1">getRenderEngine</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">createImage</span><span class="br0">(</span><span class="st0">"Interface/Images/face2.png"</span>, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// find old image</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> niftyElement <span class="sy0">=</span> nifty.<span class="me1">getCurrentScreen</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"playerhealth"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// swap old with new image</span>
niftyElement.<span class="me1">getRenderer</span><span class="br0">(</span>ImageRenderer.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setImage</span><span class="br0">(</span>img<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The same is valid for other elements, for example a text label “score”:
</p>
<pre class="code java"><span class="co1">// find old text</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> niftyElement <span class="sy0">=</span> nifty.<span class="me1">getCurrentScreen</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"score"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// swap old with new text</span>
niftyElement.<span class="me1">getRenderer</span><span class="br0">(</span>TextRenderer.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"124"</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Similarly, to change the onClick() event of an element, create an <code>ElementInteraction</code> object:
</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+element"><span class="kw3">Element</span></a> niftyElement <span class="sy0">=</span> nifty.<span class="me1">getCurrentScreen</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">findElementByName</span><span class="br0">(</span><span class="st0">"myElement"</span><span class="br0">)</span><span class="sy0">;</span>
niftyElement.<span class="me1">getElementInteraction</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getPrimary</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setOnMouseOver</span><span class="br0">(</span><span class="kw1">new</span> NiftyMethodInvoker<span class="br0">(</span>nifty, <span class="st0">"myCustomMethod()"</span>, <span class="kw1">this</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For this to work, there already needs to be a (possibly inactive) <code>&lt;interact /&gt;</code> tag inside your xml element:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;interact</span> <span class="re0">onClick</span>=<span class="st0">"doNothing()"</span><span class="re2">/&gt;</span></span></pre>

</div>
<!-- EDIT6 SECTION "Java Modifies Nifty Elements and Events" [9021-10437] -->
<h2 class="sectionedit7" id="next_steps">Next Steps</h2>
<div class="level2">

<p>
You're done with the basic Nifty <abbr title="Graphical User Interface">GUI</abbr> for jME3 tutorial. You can proceed to advanced topics and learn how add controls and effects:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/nifty_gui_scenarios.html" class="wikilink1" title="jme3:advanced:nifty_gui_scenarios"> Nifty GUI Scenarios</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://sourceforge.net/projects/nifty-gui/files/nifty-gui/nifty-gui-the-manual-v1.0.pdf/download" class="urlextern" title="http://sourceforge.net/projects/nifty-gui/files/nifty-gui/nifty-gui-the-manual-v1.0.pdf/download" rel="nofollow">Nifty GUI - the Manual</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/input.html" class="wikilink1" title="tag:input" rel="tag">input</a>,
	<a href="/tag/control.html" class="wikilink1" title="tag:control" rel="tag">control</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>,
	<a href="/tag/nifty.html" class="wikilink1" title="tag:nifty" rel="tag">nifty</a>
</span></div>

</div>
<!-- EDIT7 SECTION "Next Steps" [10438-] -->
