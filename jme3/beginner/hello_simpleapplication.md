---
title: jMonkeyEngine 3 Tutorial (1) - Hello SimpleApplication
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_1_-_hello_simpleapplication">jMonkeyEngine 3 Tutorial (1) - Hello SimpleApplication</h1>
<div class="level1">

<p>
Previous: <a href="/jme3.html" class="wikilink1" title="jme3">Installing JME3</a>,
Next: <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a>
</p>

<p>
<strong>Prerequisites:</strong> This tutorial assumes that you have <a href="http://jmonkeyengine.org/wiki/doku.php/" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/" rel="nofollow">downloaded the jMonkeyEngine SDK</a>.
</p>

<p>
In this tutorial series, we assume that you use the jMonkeyEngine <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a>. As an intermediate or advanced Java developer, you will quickly see that, in general, you can develop jMonkeyEngine code in any integrated development environment (NetBeans IDE, Eclipse, IntelliJ) or even from the <a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline">command line</a>. 
</p>

<p>
OK, let's get ready to create our first jMonkeyEngine3 application.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (1) - Hello SimpleApplication" [1-726] -->
<h2 class="sectionedit2" id="create_a_project">Create a project</h2>
<div class="level2">

<p>
In the jMonkeyEngine SDK:
</p>
<ol>
<li class="level1"><div class="li"> Choose File→New Project… from the main menu.</div>
</li>
<li class="level1"><div class="li"> In the New Project wizard, select the template JME3→Basic Game. Click Next. </div>
<ol>
<li class="level2"><div class="li"> Specify a project name, e.g. “HelloWorldTutorial”</div>
</li>
<li class="level2"><div class="li"> Specify a path where to store your new project, e.g. a <code>jMonkeyProjects</code> directory in your home directory.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Click Finish. </div>
</li>
</ol>

<p>
If you have questions, read more about <a href="/sdk/project_creation.html" class="wikilink1" title="sdk:project_creation">Project Creation</a> here.
</p>

<p>
</p><p></p><div class="notetip">We recommend to go through the steps yourself, as described in the tutorials. Alternatively, you can create a project based on the <a href="/sdk/sample_code.html" class="wikilink1" title="sdk:sample_code">JmeTests</a> template in the jMonkeyEngine SDK. It will create a project that already contains the <code>jme3test.helloworld</code> samples (and many others). For example, you can use the JmeTests project to verify whether you got the solution right.
</div>


</div>
<!-- EDIT2 SECTION "Create a project" [727-1588] -->
<h2 class="sectionedit3" id="extend_simpleapplication">Extend SimpleApplication</h2>
<div class="level2">

<p>
For this tutorial, you want to create a jme3test.helloworld package in your project, and create a file HelloJME3.java in it.
</p>

<p>
In the jMonkeyEngine SDK:
</p>
<ol>
<li class="level1"><div class="li"> Right-click the Source Packages node of your project.</div>
</li>
<li class="level1"><div class="li"> Choose New…→Java Class to create a new file.</div>
</li>
<li class="level1"><div class="li"> Enter the class name: HelloJME3</div>
</li>
<li class="level1"><div class="li"> Enter the package name: jme3test.helloworld.</div>
</li>
<li class="level1"><div class="li"> Click Finish.</div>
</li>
</ol>

<p>
The SDK creates the file HelloJME3.java for you.
</p>

</div>
<!-- EDIT3 SECTION "Extend SimpleApplication" [1589-2049] -->
<h2 class="sectionedit4" id="code_sample">Code Sample</h2>
<div class="level2">

<p>
Replace the contents of the HelloJME3.java file with the following code.
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 1 - how to get started with the most simple JME 3 application.
 * Display a blue 3D cube and view from all sides by
 * moving the mouse and pressing the WASD keys. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloJME3 <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// start the game</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// create cube shape</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// create cube geometry from the shape</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// create a simple material</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// set color of material to blue</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>                   <span class="co1">// set the cube's material</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>              <span class="co1">// make the cube appear in the scene</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Right-click the HelloJME3 class and choose Run. If a jME3 settings dialog pops up, confirm the default settings.
</p>
<ol>
<li class="level1"><div class="li"> You should see a simple window displaying a 3D cube.</div>
</li>
<li class="level1"><div class="li"> Press the WASD keys and move the mouse to navigate around.</div>
</li>
<li class="level1"><div class="li"> Look at the FPS text and object count information in the bottom left. You will use this information during development, and you will remove it for the release. (To read the numbers correctly, consider that the 14 lines of text counts as 14 objects with 914 vertices.)</div>
</li>
<li class="level1"><div class="li"> Press Escape to close the application.</div>
</li>
</ol>

<p>
Congratulations! Now let's find out how it works!
</p>

</div>
<!-- EDIT4 SECTION "Code Sample" [2050-3935] -->
<h2 class="sectionedit5" id="understanding_the_code">Understanding the Code</h2>
<div class="level2">

<p>
The code above has initialized the scene, and started the application.
</p>

</div>
<!-- EDIT5 SECTION "Understanding the Code" [3936-4043] -->
<h3 class="sectionedit6" id="start_the_simpleapplication">Start the SimpleApplication</h3>
<div class="level3">

<p>
Look at the first line. Your HelloJME3.java class extends <code>com.jme3.app.SimpleApplication</code>. 
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HelloJME3 <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
  <span class="co1">// your code...</span>
<span class="br0">}</span></pre>

<p>
Every JME3 game is an instance of the <code>com.jme3.app.SimpleApplication</code> class. The SimpleApplication class is the simplest example of an application: It manages a 3D scene graph, checks for user input, updates the game state, and automatically draws the scene to the screen. These are the core features of a game engine. You extend this simple application and customize it to create your game.
</p>

<p>
You start every JME3 game from the main() method, as every standard Java application:
</p>
<ol>
<li class="level1"><div class="li"> Instantiate your <code>SimpleApplication</code>-based class</div>
</li>
<li class="level1"><div class="li"> Call the application's <code>start()</code> method to start the game engine. </div>
</li>
</ol>
<pre class="code java">    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// instantiate the game</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>                     <span class="co1">// start the game!</span>
    <span class="br0">}</span></pre>

<p>
The <code>app.start();</code> line opens the application window. Let's learn how you put something into this window (the scene) next.
</p>

</div>
<!-- EDIT6 SECTION "Start the SimpleApplication" [4044-5204] -->
<h3 class="sectionedit7" id="understanding_the_terminology">Understanding the Terminology</h3>
<div class="level3">
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">What you want to do</th><th class="col1">How you say that in JME3 terminology</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">You want to create a cube.</td><td class="col1">I create a Geometry with a 1x1x1 Box shape.</td>
	</tr>
	<tr class="row2">
		<td class="col0">You want to use a blue color.</td><td class="col1">I create a Material with a blue Color property.</td>
	</tr>
	<tr class="row3">
		<td class="col0">You want to colorize the cube blue.</td><td class="col1">I set the Material of the Box Geometry.</td>
	</tr>
	<tr class="row4">
		<td class="col0">You want to add the cube to the scene.</td><td class="col1">I attach the Box Geometry to the rootNode.</td>
	</tr>
	<tr class="row5">
		<td class="col0">You want the cube to appear in the center.</td><td class="col1">I create the Box at the origin = at <code>Vector3f.ZERO</code>.</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [5246-5719] -->
<p>
If you are unfamiliar with the vocabulary, read more about <a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph">the Scene Graph</a> here.
</p>

</div>
<!-- EDIT7 SECTION "Understanding the Terminology" [5205-5812] -->
<h3 class="sectionedit9" id="initialize_the_scene">Initialize the Scene</h3>
<div class="level3">

<p>
Look at rest of the code sample. The <code>simpleInitApp()</code> method is automatically called once at the beginning when the application starts. Every JME3 game must have this method. In the <code>simpleInitApp()</code> method, you load game objects before the game starts. 
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
       <span class="co1">// your initialization code...</span>
    <span class="br0">}</span></pre>

<p>
The initialization code of a blue cube looks as follows:
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// create a 1x1x1 box shape</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// create a cube geometry from the box shape</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// create a simple material</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// set color of material to blue</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>                   <span class="co1">// set the cube geometry 's material</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>              <span class="co1">// make the cube geometry appear in the scene</span>
    <span class="br0">}</span></pre>

<p>
A typical JME3 game has the following initialization process:
</p>
<ol>
<li class="level1"><div class="li"> You initialize game objects:</div>
<ul>
<li class="level2"><div class="li"> You create or load objects and position them.</div>
</li>
<li class="level2"><div class="li"> You make objects appear in the scene by attaching them to the <code>rootNode</code>.</div>
</li>
<li class="level2"><div class="li"> <strong>Examples:</strong> Load player, terrain, sky, enemies, obstacles, …, and place them in their start positions.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> You initialize variables</div>
<ul>
<li class="level2"><div class="li"> You create variables to track the game state. </div>
</li>
<li class="level2"><div class="li"> You set variables to their start values. </div>
</li>
<li class="level2"><div class="li"> <strong>Examples:</strong> Set the <code>score</code> to 0, set <code>health</code> to 100%, …</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> You initialize keys and mouse actions.</div>
<ul>
<li class="level2"><div class="li"> The following input bindings are pre-configured:</div>
<ul>
<li class="level3"><div class="li"> W,A,S,D keys – Move around in the scene</div>
</li>
<li class="level3"><div class="li"> Mouse movement and arrow keys – Turn the camera</div>
</li>
<li class="level3"><div class="li"> Escape key – Quit the game</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> Define your own additional keys and mouse click actions.</div>
</li>
<li class="level2"><div class="li"> <strong>Examples:</strong> Click to shoot, press Space to jump, …</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT9 SECTION "Initialize the Scene" [5813-7783] -->
<h2 class="sectionedit10" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned that a SimpleApplication is a good starting point because it provides you with:
</p>
<ul>
<li class="level1"><div class="li"> A <code>simpleInitApp()</code> method where you create objects.</div>
</li>
<li class="level1"><div class="li"> A <code>rootNode</code> where you attach objects to make them appear in the scene.</div>
</li>
<li class="level1"><div class="li"> Useful default input settings that you can use for navigation in the scene.</div>
</li>
</ul>

<p>
When developing a game application, you want to:
</p>
<ol>
<li class="level1"><div class="li"> Initialize the game scene</div>
</li>
<li class="level1"><div class="li"> Trigger game actions </div>
</li>
<li class="level1"><div class="li"> Respond to user input.</div>
</li>
</ol>

<p>
The now following tutorials teach how you accomplish these tasks with the jMonkeyEngine 3.
</p>

<p>
Continue with the <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a> tutorial, where you learn more details about how to initialize the game world, also known as the scene graph.
</p>
<hr />

<p>
See also:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/wiki/doku.php/" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/" rel="nofollow">Install the jMonkeyEngine</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline">SimpleApplication From the Commandline</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/project_creation.html" class="wikilink1" title="sdk:project_creation">Create a JME3 project</a>.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/init.html" class="wikilink1" title="tag:init" rel="tag">init</a>,
	<a href="/tag/simpleapplication.html" class="wikilink1" title="tag:simpleapplication" rel="tag">simpleapplication</a>,
	<a href="/tag/basegame.html" class="wikilink1" title="tag:basegame" rel="tag">basegame</a>
</span></div>

</div>
<!-- EDIT10 SECTION "Conclusion" [7784-] -->
