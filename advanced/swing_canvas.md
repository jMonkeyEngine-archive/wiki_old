---
title: JME3 Canvas in a Swing GUI
---
<h1 class="sectionedit1" id="jme3_canvas_in_a_swing_gui">JME3 Canvas in a Swing GUI</h1>
<div class="level1">

<p>
3D games are typically played full-screen, or in a window that takes over the mouse and all inputs. However it is also possible to embed a jME 3 canvas in a standard Swing application. <br />
<br />

This can be useful when you create some sort of interactive 3D viewer with a user interface that is more complex than just a HUD: For instance an interactive scientific demo, a level editor, or a game character designer. <br />
<br />

</p>
<ul>
<li class="level1"><div class="li"> Advantages:</div>
<ul>
<li class="level2"><div class="li"> You can use Swing components (frame, panels, menus, controls) next to your jME3 game.</div>
</li>
<li class="level2"><div class="li"> The NetBeans <abbr title="Graphical User Interface">GUI</abbr> builder is compatible with the jMonkeyEngine; you can use it it to lay out the Swing <abbr title="Graphical User Interface">GUI</abbr> frame, and then add() the jME canvas into it. Install the <abbr title="Graphical User Interface">GUI</abbr> builder via Tools → Plugins → Available Plugins.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Disadvantages:</div>
<ul>
<li class="level2"><div class="li"> You cannot use SimpleApplication's default mouse capturing for camera navigation, but have to come up with a custom solution.</div>
</li>
</ul>
</li>
</ul>

<p>
Here is the full <a href="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/awt/TestCanvas.java" class="urlextern" title="http://code.google.com/p/jmonkeyengine/source/browse/trunk/engine/src/test/jme3test/awt/TestCanvas.java" rel="nofollow">TestCanvas.java</a> code sample.
</p>

</div>
<!-- EDIT1 SECTION "JME3 Canvas in a Swing GUI" [1-1097] -->
<h2 class="sectionedit2" id="extending_simpleapplication">Extending SimpleApplication</h2>
<div class="level2">

<p>
You start out just the same as for any jME3 game: The base application, here SwingCanvasTest, extends <code>com.jme3.app.SimpleApplication</code>. As usual, you use <code>simpleInitApp()</code> to initialize the scene, and <code>simpleUpdate()</code> as event loop. <br />
<br />

The camera's default behaviour in SimpleApplication is to capture the mouse, which doesn't make sense in a Swing window. You have to deactivate and replace this behaviour by <code>flyCam.setDragToRotate(true);</code> when you initialize the application:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
  <span class="co1">// activate windowed input behaviour</span>
  flyCam.<span class="me1">setDragToRotate</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="co1">// Set up inputs and load your scene as usual</span>
  ...
<span class="br0">}</span></pre>

<p>
In short: The first thing that is different is the <code>main()</code> method. We don't call start() on the SwingCanvasTest object as usual. Instead we create a Runnable() that creates and opens a standard Swing jFrame. In the runnable, we also create our SwingCanvasTest game with special settings, create a Canvas for it, and add that to the jFrame. Then we call startCanvas().
</p>

</div>
<!-- EDIT2 SECTION "Extending SimpleApplication" [1098-2174] -->
<h2 class="sectionedit3" id="main_and_runnable">Main() and Runnable()</h2>
<div class="level2">

<p>
The Swing isn't thread-safe and doesn't allow us to keep the jME3 canvas up-to-date. This is why we create a runnable for the jME canvas and queue it in the AWT event thread, so it can be invoked “later” in the loop, when Swing is ready with updating its own stuff. <br />
<br />

In the SwingCanvasTest's main() method, create a queued runnable(). It will contain the jME canvas and the Swing frame.
</p>
<pre class="code java">  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    java.<span class="me1">awt</span>.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+eventqueue"><span class="kw3">EventQueue</span></a>.<span class="me1">invokeLater</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+runnable"><span class="kw3">Runnable</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">public</span> <span class="kw4">void</span> run<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
         <span class="co1">// ... see below ...</span>
      <span class="br0">}</span>
    <span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span></pre>

<p>
</p><p></p><div class="noteimportant">Note that you have to use app.enqueue() when modifying objects in the scene from the AWT Event Queue like you have to use java.awt.EventQueue.invokeLater() from other threads (e.g. the update loop) when changing swing elements. This can get hairy quickly if you don’t have a proper threading model planned so you might want to use NiftyGUI as it is embedded in the update loop thread and is also cross-platform compatible (e.g. android etc.).
</div>


</div>
<!-- EDIT3 SECTION "Main() and Runnable()" [2175-3260] -->
<h3 class="sectionedit4" id="creating_the_canvas">Creating the Canvas</h3>
<div class="level3">

<p>
Here in the <code>run()</code> method, we start the jME application, create its canvas, create a Swing frame, and add everything together. <br />
<br />

Specify the com.jme3.system.AppSettings so jME knows the size of the Swing panel that we put it into. The application will not ask the user for display settings, you have to specify them in advance.
</p>
<pre class="code java">AppSettings settings <span class="sy0">=</span> <span class="kw1">new</span> AppSettings<span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
settings.<span class="me1">setWidth</span><span class="br0">(</span><span class="nu0">640</span><span class="br0">)</span><span class="sy0">;</span>
settings.<span class="me1">setHeight</span><span class="br0">(</span><span class="nu0">480</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
We create our canvas application SwingCanvasTest, and give it the settings. We manually create a canvas for this game and configure the com.jme3.system.JmeCanvasContext. The method setSystemListener() makes sure that the listener receives events relating to context creation, update, and destroy.
</p>
<pre class="code java">SwingCanvasTest canvasApplication <span class="sy0">=</span> <span class="kw1">new</span> SwingCanvasTest<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
canvasApplication.<span class="me1">setSettings</span><span class="br0">(</span>settings<span class="br0">)</span><span class="sy0">;</span>
canvasApplication.<span class="me1">createCanvas</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// create canvas!</span>
JmeCanvasContext ctx <span class="sy0">=</span> <span class="br0">(</span>JmeCanvasContext<span class="br0">)</span> canvasApplication.<span class="me1">getContext</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
ctx.<span class="me1">setSystemListener</span><span class="br0">(</span>canvasApplication<span class="br0">)</span><span class="sy0">;</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+dimension"><span class="kw3">Dimension</span></a> dim <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+dimension"><span class="kw3">Dimension</span></a><span class="br0">(</span><span class="nu0">640</span>, <span class="nu0">480</span><span class="br0">)</span><span class="sy0">;</span>
ctx.<span class="me1">getCanvas</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setPreferredSize</span><span class="br0">(</span>dim<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Note that we have not called start() on the application, as we would usually do in the main() method. We will call startCanvas() later instead.
</p>

</div>
<!-- EDIT4 SECTION "Creating the Canvas" [3261-4545] -->
<h3 class="sectionedit5" id="creating_the_swing_frame">Creating the Swing Frame</h3>
<div class="level3">

<p>
Inside the run() method, you create the Swing window as you would usually do. Create an empty jFrame and add() components to it, or create a custom jFrame object in another class file (for example, by using the NetBeans <abbr title="Graphical User Interface">GUI</abbr> builder) and create an instance of it here.
Which ever you do, let's call the jFrame <code>window</code>.
</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jframe"><span class="kw3">JFrame</span></a> window <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jframe"><span class="kw3">JFrame</span></a><span class="br0">(</span><span class="st0">"Swing Application"</span><span class="br0">)</span><span class="sy0">;</span>
window.<span class="me1">setDefaultCloseOperation</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jframe"><span class="kw3">JFrame</span></a>.<span class="me1">EXIT_ON_CLOSE</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
We create a standard JPanel inside the JFrame. Give it any Layout you wish – here we use a simple Flow Layout. Where the code sample says “Some Swing Component”, this is where you add your buttons and controls. <br />
<br />

The important step is to add() the canvas component into the panel, like all the other Swing components.
</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jpanel"><span class="kw3">JPanel</span></a> panel <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jpanel"><span class="kw3">JPanel</span></a><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+flowlayout"><span class="kw3">FlowLayout</span></a><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// a panel</span>
<span class="co1">// add all your Swing components ...</span>
panel.<span class="me1">add</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jbutton"><span class="kw3">JButton</span></a><span class="br0">(</span><span class="st0">"Some Swing Component"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
...
<span class="co1">// add the JME canvas</span>
panel.<span class="me1">add</span><span class="br0">(</span>ctx.<span class="me1">getCanvas</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
OK, the jFrame and the panel are ready. We add the panel into the jFrame, and pack everything together. Set the window's visibility to true make it appear.
</p>
<pre class="code java">window.<span class="me1">add</span><span class="br0">(</span>panel<span class="br0">)</span><span class="sy0">;</span>
window.<span class="me1">pack</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
window.<span class="me1">setVisible</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Remember that we haven't called start() on the jME appliation yet? For the canvas, there is a special <code>startCanvas()</code> method that you must call now:
</p>
<pre class="code java">canvasApplication.<span class="me1">startCanvas</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Clean, build, and run!
</p>

</div>
<!-- EDIT5 SECTION "Creating the Swing Frame" [4546-6019] -->
<h2 class="sectionedit6" id="navigation">Navigation</h2>
<div class="level2">

<p>
Remember, to navigate in the scene, click and drag (!) the mouse, or press the WASD keys. Depending on your game you may even want to define custom inputs to handle navigation in this untypical environment.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>
</span></div>

</div>
<!-- EDIT6 SECTION "Navigation" [6020-] -->
