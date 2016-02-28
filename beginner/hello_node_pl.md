---
title: JME 3 Tutorial (2) - Hello Node
---
<h1 class="sectionedit1" id="jme_3_tutorial_2_-_hello_node">JME 3 Tutorial (2) - Hello Node</h1>
<div class="level1">

<p>
Poprzedni: <a href="/jme3/beginner/hello_simpleapplication_pl.html" class="wikilink1" title="jme3:beginner:hello_simpleapplication_pl">Hello SimpleApplication</a>,
Następny: <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">Hello Assets</a>. <br />
<br />

Kiedy tworzysz grę, zaczynasz od stworzenia sceny oraz paru obiektów. Umieszczasz obiekty na scenie, a następnie przemieszczasz, obracasz, zmniejszasz oraz animujesz je. <br />
<br />

W tym tutorialu rzucimy okiem na prostą scenę trójwymiarową.  3D world is represented in a scene graph, i dlaczego rootNode jest tak ważny. Dowiesz się jak tworzyć i manipulować obiektami – przemieszczać, skalować czy obracać. Zrozumiesz różnicę pomiędzy dwoma typami Spatials w scene graph, Node i Geometry. Aby zrozumieć jak działa scene graph zajrzyj do prezentacji introduction to the scene graph check out our <a href="/jme3/scenegraph_for_dummies.html" class="wikilink1" title="jme3:scenegraph_for_dummies"> Scene Graph for Dummies</a>.
</p>

</div>
<!-- EDIT1 SECTION "JME 3 Tutorial (2) - Hello Node" [1-862] -->
<h2 class="sectionedit2" id="kod_zrodlowy">Kod źródłowy</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="co3">/** Przykład 2 - How to use nodes as handles to manipulate objects in the scene graph.
 * You can rotate, translate, and scale objects by manipulating their parent nodes.
 * The Root Node is special: Only what is attached to the Root Node appears in the scene. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloNode <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloNode app <span class="sy0">=</span> <span class="kw1">new</span> HelloNode<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// create a blue box at coordinates (1,-1,1)</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box1 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="sy0">-</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry blue <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box1<span class="br0">)</span><span class="sy0">;</span>
        Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        blue.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// create a red box straight above the blue one at (1,3,1)</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">3</span>,<span class="nu0">1</span><span class="br0">)</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry red <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box2<span class="br0">)</span><span class="sy0">;</span>
        Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
        red.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// create a pivot node at (0,0,0) and attach it to root</span>
        Node pivot <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"pivot"</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pivot<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// attach the two boxes to the *pivot* node!</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>blue<span class="br0">)</span><span class="sy0">;</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>red<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// rotate pivot node: Both boxes have rotated!</span>
        pivot.<span class="me1">rotate</span><span class="br0">(</span> 0.4f , 0.4f , 0.0f <span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Build and run the code sample. You should see two colored boxes tilted at the same angle.
</p>

</div>
<!-- EDIT2 SECTION "Kod źródłowy" [863-2772] -->
<h2 class="sectionedit3" id="understanding_the_terminology">Understanding the Terminology</h2>
<div class="level2">

<p>
In this tutorial, you will learn some new terms:
</p>
<ol>
<li class="level1"><div class="li"> The <em>scene graph</em> represents your 3D world.</div>
</li>
<li class="level1"><div class="li"> Objects in the scene graph (such as the boxes in this example) are called <em>Spatials</em>.</div>
<ul>
<li class="level2"><div class="li"> A Spatial is a collection of information about an object: its location, rotation, and scale.</div>
</li>
<li class="level2"><div class="li"> A Spatial can be loaded, transformed, and saved.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> There are two types of Spatials, <em>Nodes</em> and <em>Geometries</em>.</div>
</li>
<li class="level1"><div class="li"> To add a Spatial to the scene graph, you attach the Spatial to the <em>rootNode</em>.</div>
</li>
<li class="level1"><div class="li"> Everything attached to the <em>rootNode</em> is part of the scene graph.</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Understanding the Terminology" [2773-3383] -->
<h2 class="sectionedit4" id="understanding_the_code">Understanding the Code</h2>
<div class="level2">

<p>
So what exactly happens in this code snippet? Note that we are using the <code>simpleInitApp()</code> method that was introduced in the first tutorial.
</p>
<ol>
<li class="level1"><div class="li"> We create a box Geometry.</div>
<ul>
<li class="level2"><div class="li"> The box Geometry's extends are (1,1,1), that makes it 2x2x2 world units big.</div>
</li>
<li class="level2"><div class="li"> We place the box at (1,-1,1)</div>
</li>
<li class="level2"><div class="li"> We give it a solid blue material. <pre class="code java">        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box1 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="sy0">-</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry blue <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box1<span class="br0">)</span><span class="sy0">;</span>
        Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        blue.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> We create a second box Geometry.</div>
<ul>
<li class="level2"><div class="li"> This box Geometry is also 2x2x2 world units big.</div>
</li>
<li class="level2"><div class="li"> We place the second box at (1,3,1). This is straight above the blue box, with a gap of 2 world units inbetween.</div>
</li>
<li class="level2"><div class="li"> We give it a solid red material<pre class="code java">        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">3</span>,<span class="nu0">1</span><span class="br0">)</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry red <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box2<span class="br0">)</span><span class="sy0">;</span>
        Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
        red.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> We create a Node.</div>
<ul>
<li class="level2"><div class="li"> By default the Node is placed at (0,0,0).</div>
</li>
<li class="level2"><div class="li"> We attach the Node to the rootNode.</div>
</li>
<li class="level2"><div class="li"> An attached Node has no visible appearance in the scene. <pre class="code java">        Node pivot <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"pivot"</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pivot<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Note that we have not attached the two boxes to anything yet!</div>
<ul>
<li class="level2"><div class="li"> <em>If we ran the application now, the scenegraph would appear empty.</em></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> We attach the two boxes to the node.</div>
<ul>
<li class="level2"><div class="li"> <em>If we ran the app now, we would see two boxes: one straight above the other.</em> <pre class="code java">        pivot.<span class="me1">attachChild</span><span class="br0">(</span>blue<span class="br0">)</span><span class="sy0">;</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>red<span class="br0">)</span><span class="sy0">;</span> </pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Now, we rotate the node.</div>
<ul>
<li class="level2"><div class="li"> <em>When we run the application now, we see two boxes on top of each other – but both are tilted at the same angle.</em> <pre class="code java">        pivot.<span class="me1">rotate</span><span class="br0">(</span> 0.4f , 0.4f , 0.0f <span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
</ol>

<p>
What has happened? We have attached two box Geometries to a Node. Then we used the Node as a handle to grab the two boxes and transform (rotate) both, in one step. This is a common task and you will use this method a lot in your games when you move game characters around.
</p>

</div>
<!-- EDIT4 SECTION "Understanding the Code" [3384-5700] -->
<h3 class="sectionedit5" id="definitiongeometry_vs_node">Definition: Geometry vs Node</h3>
<div class="level3">

<p>
You work with two types of Spatials in your scenegraph: Nodes and Geometries. Here is the difference:
</p>
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0 leftalign">  </td><th class="col1"> Geometry </th><th class="col2"> Node </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> Visibility: </th><td class="col1"> A visible 3-D object. </td><td class="col2"> An invisible “handle”. </td>
	</tr>
	<tr class="row2">
		<th class="col0"> Purpose: </th><td class="col1"> A Geometry stores an object's looks. </td><td class="col2"> A Node groups Geometries and other Nodes together. </td>
	</tr>
	<tr class="row3">
		<th class="col0"> Examples: </th><td class="col1"> A box, a sphere, player, a building, a piece of terrain, a vehicle, missiles, NPCs, etc… </td><td class="col2"> The default <code>rootNode</code>, the <code>guiNode</code> (for on-screen text); a floor node, a custom vehicle-with-passengers node, an audio node, etc… </td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [5842-6282] -->
</div>
<!-- EDIT5 SECTION "Definition: Geometry vs Node" [5701-6282] -->
<h2 class="sectionedit7" id="faqhow_to_populate_the_scenegraph">FAQ: How to Populate the Scenegraph?</h2>
<div class="level2">
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Task? </th><th class="col1"> Solution! </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Create a Spatial </td><td class="col1"> Create a shape and give it a Material. For instance a box shape: <pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
Geometry thing <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"thing"</span>, mesh<span class="br0">)</span><span class="sy0">;</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
thing.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row2">
		<td class="col0"> Make an object appear in the scene </td><td class="col1"> Attach the Spatial to the <code>rootNode</code>, or to any node that is attached to the rootNode. <pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>thing<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row3">
		<td class="col0"> Remove objects from the scene </td><td class="col1"> Detach the Spatial from the <code>rootNode</code>, and from any node that is attached to the rootNode. <pre class="code java">rootNode.<span class="me1">detachChild</span><span class="br0">(</span>thing<span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">rootNode.<span class="me1">detachAllChildren</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row4">
		<td class="col0"> Find a Spatial in the scene by the object's name or ID </td><td class="col1"> Look at the node's children. <pre class="code java">Spatial thing <span class="sy0">=</span> rootNode.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"thing"</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial twentyThird <span class="sy0">=</span> rootNode.<span class="me1">getChild</span><span class="br0">(</span><span class="nu0">22</span><span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row5">
		<td class="col0"> Specify what should be loaded at the start </td><td class="col1"> Everything you initialize and attach to the <code>rootNode</code> in the <code>simpleInitApp()</code> method is part of the scene at the start of the game. </td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [6332-7459] -->
</div>
<!-- EDIT7 SECTION "FAQ: How to Populate the Scenegraph?" [6283-7459] -->
<h2 class="sectionedit9" id="how_to_transform_objects">How to Transform Objects?</h2>
<div class="level2">

<p>
There are three types of 3D transformation: Translation (moving), Scaling (resizing), and Rotation (turning).
</p>
<div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Task? </th><th class="col1"> Solution! </th><th class="col2"> X </th><th class="col3"> Y </th><th class="col4"> Z </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Position and move objects </td><td class="col1"> <strong>Translation:</strong> Specify the new location in three dimensions: right/left, up/down, forward/backward. <br />
Example 1. To move an object <em>to</em> specific coordinates, such as (0,40.2f,-2), use: <pre class="code java">thing.<span class="me1">setLocalTranslation</span><span class="br0">(</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.0f, 40.2f, <span class="sy0">-</span>2.0f <span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 <br />
Example 2: To move an object <em>by</em> a certain amount, e.g. higher up (y=40.2f) and further back (z=-2.0f): 
</p>
<pre class="code java">thing.<span class="me1">move</span><span class="br0">(</span> 0.0f, 40.2f, <span class="sy0">-</span>2.0f <span class="br0">)</span><span class="sy0">;</span></pre>
</td><td class="col2">right/left</td><td class="col3">up/down</td><td class="col4">forward/ backward</td>
	</tr>
	<tr class="row2">
		<td class="col0"> Resize objects </td><td class="col1"> <strong>Scaling:</strong> To resize a Spatial, specify the scale factor in each dimension: length, height, width. A value between 0.0f and 1.0f will shrink the object; a value bigger than 1.0f will make it grow; and 1.0f will keep this dimension the same. Using the same value for each dimension scales an object proportionally, using different values stretches it. <br />
Example: Make it 10 times longer, one tenth of the height, same width: <pre class="code java">thing.<span class="me1">setLocalScale</span><span class="br0">(</span> 10.0f, 0.1f, 1.0f  <span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">thing.<span class="me1">scale</span><span class="br0">(</span> 10.0f, 0.1f, 1.0f <span class="br0">)</span><span class="sy0">;</span></pre>
</td><td class="col2">length</td><td class="col3">height</td><td class="col4">width</td>
	</tr>
	<tr class="row3">
		<td class="col0"> Turn objects </td><td class="col1"> <strong>Rotation:</strong> 3-D rotation is a bit tricky (<a href="/doku.php/jme2:rotate" class="wikilink2" title="jme2:rotate" rel="nofollow">learn details here</a>). In short: You can rotate around three axes, pitch, yaw, and roll. <br />
Important: <strong>You do not specify the rotation in degrees from 0° to 360°, but in radians from 0.0f to 6.28f (FastMath.PI*2) !</strong> <br />
Example: To roll an object 180° around the z axis: <pre class="code java">thing.<span class="me1">rotate</span><span class="br0">(</span> 0f , 0f , FastMath.<span class="me1">PI</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 If you do want to specify angles in degrees then multiply your degrees value with FastMath.DEG_TO_RAD <br />
Example: 
</p>
<pre class="code java">thing.<span class="me1">rotate</span><span class="br0">(</span> 0f , 0f , <span class="nu0">180</span><span class="sy0">*</span>FastMath.<span class="me1">DEG_TO_RAD</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
  Tip: If your game idea calls for a serious amount of rotations, it is worth looking into <a href="/doku.php/jme2:quaternion" class="wikilink2" title="jme2:quaternion" rel="nofollow">quaternion</a>s, a data structure that can combine and store rotations efficiently. 
</p>
<pre class="code java">thing.<span class="me1">setLocalRotation</span><span class="br0">(</span> <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>. <span class="me1">fromAngleAxis</span><span class="br0">(</span>FastMath.<span class="me1">PI</span><span class="sy0">/</span><span class="nu0">2</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</td><td class="col2">pitch</td><td class="col3">yaw</td><td class="col4">roll</td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [7608-9628] -->
</div>
<!-- EDIT9 SECTION "How to Transform Objects?" [7460-9628] -->
<h2 class="sectionedit11" id="how_to_troubleshoot_nodes">How to Troubleshoot Nodes?</h2>
<div class="level2">

<p>
If you get unexpected results, check whether you made the following common mistakes:
</p>
<div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Problem? </th><th class="col1"> Solution! </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Created Geometry does not appear in scene </td><td class="col1"> Have you attached it to (a node that is attached to) the rootNode? <br />
Does it have a Material? <br />
What is its translation (position)? Is it covered up by another Geometry? <br />
Is it too far from the camera? try <a href="http://jmonkeyengine.org/javadoc/com/jme3/renderer/Camera.html#setFrustumFar%28float%29" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/renderer/Camera.html#setFrustumFar%28float%29" rel="nofollow">cam.setFrustumFar</a>(111111f); </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Spatial rotates wrong </td><td class="col1"> Did you use radian values, and not degrees? (if you used degrees multiply them with FastMath.DEG_TO_RAD to get them converted to radians)<br />
Did you rotate the intended pivot node? <br />
Did you rotate around the right axis? </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Geometry has an unexpected Material </td><td class="col1 leftalign"> Did you reuse a Material from another Geometry and have inadvertently changed its properties? <br />
(if so, maybe consider cloning: mat2 = mat.clone(); )  </td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [9753-10598] -->
</div>
<!-- EDIT11 SECTION "How to Troubleshoot Nodes?" [9629-10598] -->
<h2 class="sectionedit13" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned that the 3D world is a Scene Graph of Spatials: Visible Geometries and invisible Nodes. You can transform Spatials, or attach them to nodes and transform the nodes. <br />
<br />

Since standard shapes like spheres and boxes get old fast, continue with the next chapter where you learn to <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">load assets, such as 3-D models</a>.
</p>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/rootnode.html" class="wikilink1" title="tag:rootnode" rel="tag">rootNode</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/color.html" class="wikilink1" title="tag:color" rel="tag">color</a>,
	<a href="/tag/polish.html" class="wikilink1" title="tag:polish" rel="tag">polish</a>
</span></div>

</div>
<!-- EDIT13 SECTION "Conclusion" [10599-] -->
