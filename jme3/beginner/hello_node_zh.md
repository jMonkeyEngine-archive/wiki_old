---
title: jMonkeyEngine 3 第二颗 (2) - Hello Node
---
<h1 class="sectionedit1" id="jmonkeyengine_3_第二颗_2_-_hello_node">jMonkeyEngine 3 第二颗 (2) - Hello Node</h1>
<div class="level1">

<p>
先看: <a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph">Hello SimpleApplication</a>,
在看: <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">Hello Assets</a>. 
</p>

<p>
我的中文不是呢么好，请你们帮我咻咻他。谢谢。
</p>

<p>
在这一课，你会学怎么去盖一个3D场景。
</p>
<ul>
<li class="level1"><div class="li"> 学这一棵前，你先好知道什么是<a href="http://jmonkeyengine.org/wiki/doku.php/jme3:setting_up_jme3_in_eclipse" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jme3:setting_up_jme3_in_eclipse" rel="nofollow">Scene Graph</a>，</div>
</li>
<li class="level1"><div class="li"> 如果你不知道他是什么，就看<a href="/jme3/scenegraph_for_dummies.html" class="wikilink1" title="jme3:scenegraph_for_dummies">Scene Graph for Dummies</a>.</div>
</li>
</ul>

<p>
盖3D游戏时：
</p>
<ol>
<li class="level1"><div class="li"> 你要雕塑3D人，房子，ect。</div>
</li>
<li class="level1"><div class="li"> 你要方静你的模型在游戏场景里</div>
</li>
<li class="level1"><div class="li"> 你要动，便形，转，图上颜色，和动画他们。</div>
</li>
</ol>

<p>
你会学怎么用 Scene Graph 做什么，学为什么 RootNode 呢么重要，学怎么放变量比如活力或钱经一个 Node，学怎么动，转或变你的模型的形状，和你会学 Node 和 Geometry 有什么分别。
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 第二颗 (2) - Hello Node" [1-937] -->
<h2 class="sectionedit2" id="例子">例子</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 2 - 怎么用 Nodes 去动或变模型。
 *Root Node 很特别，你只能看到放在它上的模型*/</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> HelloNode <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloNode app <span class="sy0">=</span> <span class="kw1">new</span> HelloNode<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        <span class="co3">/** 改一个新蓝色的立方体在（1,1,1）*/</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box1 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry blue <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box1<span class="br0">)</span><span class="sy0">;</span>
        Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
                <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        blue.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
        blue.<span class="me1">move</span><span class="br0">(</span><span class="nu0">1</span>,<span class="sy0">-</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co3">/**盖一个新红色的立方体在（1,3,1）*/</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry red <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box2<span class="br0">)</span><span class="sy0">;</span>
        Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
                <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
        red.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span>
        red.<span class="me1">move</span><span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">3</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co3">/** 改一个新 Node 叫 ”pivot“ 在 （0,0,0），放他在 Root Node 上*/</span>
        Node pivot <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"pivot"</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pivot<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 放 pivot 在 Root Node 上。</span>
 
        <span class="co3">/** 放那两个立方体在在 pivot 上 */</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>blue<span class="br0">)</span><span class="sy0">;</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>red<span class="br0">)</span><span class="sy0">;</span>
        <span class="co3">/** 转 pivot：那两个立方体会跟他转*/</span>
        pivot.<span class="me1">rotate</span><span class="br0">(</span>.4f,.4f,0f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
开始 Hello Node 后，你会看到两个一样斜的立方体。
</p>

</div>
<!-- EDIT2 SECTION "例子" [938-2806] -->
<h2 class="sectionedit3" id="口语到_jme_语">口语到 JME 语</h2>
<div class="level2">

<p>
在这一个，你学到了几个东西:
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">你要做什么</th><th class="col1">怎么说在JME语言</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Lay out the 3D scene</td><td class="col1">Populate the scene graph</td>
	</tr>
	<tr class="row2">
		<td class="col0">Create scene objects</td><td class="col1">Create Spatials (e.g. create Geometries)</td>
	</tr>
	<tr class="row3">
		<td class="col0">Make an object appear in the scene</td><td class="col1">Attach a Spatial to the rootNode</td>
	</tr>
	<tr class="row4">
		<td class="col0">Make an object disappear from the scene</td><td class="col1">Detach the Spatial from the rootNode</td>
	</tr>
	<tr class="row5">
		<td class="col0">Position/move, turn, or resize an object</td><td class="col1">Translate, or rotate, or scale an object = transform an object.</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [2880-3287] -->
<p>
Every JME3 application has a rootNode: Your game automatically inherits the <code>rootNode</code> object from SimpleApplication. Everything attached to the rootNode is part of the scene graph. The elements of the scene graph are Spatials.
</p>
<ul>
<li class="level1"><div class="li"> A Spatial contains the location, rotation, and scale of an object.</div>
</li>
<li class="level1"><div class="li"> A Spatial can be loaded, transformed, and saved.</div>
</li>
<li class="level1"><div class="li"> There are two types of Spatials: Nodes and Geometries.</div>
</li>
</ul>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0 leftalign">  </td><th class="col1"> Geometry </th><th class="col2"> Node </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> Visibility: </th><td class="col1"> A Geometry is a visible scene object. </td><td class="col2"> A Node is an invisible “handle” for scene objects. </td>
	</tr>
	<tr class="row2">
		<th class="col0"> Purpose: </th><td class="col1"> A Geometry stores an object's looks. </td><td class="col2"> A Node groups Geometries and other Nodes together. </td>
	</tr>
	<tr class="row3">
		<th class="col0"> Examples: </th><td class="col1"> A box, a sphere, a player, a building, a piece of terrain, a vehicle, missiles, NPCs, etc… </td><td class="col2"> The <code>rootNode</code>, a floor node grouping several terrains, a custom vehicle-with-passengers node, a player-with-weapon node, an audio node, etc… </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [3703-4196] -->
</div>
<!-- EDIT3 SECTION "口语到 JME 语" [2807-4196] -->
<h2 class="sectionedit6" id="understanding_the_code">Understanding the Code</h2>
<div class="level2">

<p>
What happens in the code snippet? You use the <code>simpleInitApp()</code> method that was introduced in the first tutorial to initialize the scene.
</p>
<ol>
<li class="level1"><div class="li"> You create the first box Geometry.</div>
<ul>
<li class="level2"><div class="li"> Create a Box shape with a radius of (1,1,1), that makes the box 2x2x2 world units big.</div>
</li>
<li class="level2"><div class="li"> Position the box at (1,-1,1) using the move() method. (Don't change the Vector3f.ZERO unless you want to change the center of rotation)</div>
</li>
<li class="level2"><div class="li"> Wrap the Box shape into a Geometry.</div>
</li>
<li class="level2"><div class="li"> Create a blue material. </div>
</li>
<li class="level2"><div class="li"> Apply the blue material to the Box Geometry. <pre class="code java">    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box1 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    Geometry blue <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box1<span class="br0">)</span><span class="sy0">;</span>
    Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
      <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
    blue.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
    blue.<span class="me1">move</span><span class="br0">(</span><span class="nu0">1</span>,<span class="sy0">-</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> You create a second box Geometry.</div>
<ul>
<li class="level2"><div class="li"> Create a second Box shape with the same size.</div>
</li>
<li class="level2"><div class="li"> Position the second box at (1,3,1). This is straight above the first box, with a gap of 2 world units inbetween.</div>
</li>
<li class="level2"><div class="li"> Wrap the Box shape into a Geometry.</div>
</li>
<li class="level2"><div class="li"> Create a red material. </div>
</li>
<li class="level2"><div class="li"> Apply the red material to the Box Geometry. <pre class="code java">    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    Geometry red <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box2<span class="br0">)</span><span class="sy0">;</span>
    Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
      <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
    red.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span>
    red.<span class="me1">move</span><span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">3</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> You create a pivot Node. </div>
<ul>
<li class="level2"><div class="li"> Name the Node “pivot”.</div>
</li>
<li class="level2"><div class="li"> By default the Node is positioned at (0,0,0). </div>
</li>
<li class="level2"><div class="li"> Attach the Node to the rootNode.</div>
</li>
<li class="level2"><div class="li"> The Node has no visible appearance in the scene. <pre class="code java">    Node pivot <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"pivot"</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pivot<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
If you run the application with only the code up to here, the scene appears empty. This is because a Node is invisible, and you have not yet attached any visible Geometries to the rootNode. 
</p>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Attach the two boxes to the pivot node. <pre class="code java">        pivot.<span class="me1">attachChild</span><span class="br0">(</span>blue<span class="br0">)</span><span class="sy0">;</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>red<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
If you run the app with only the code up to here, you see two cubes: A red cube straight above a blue cube.
</p>
</div>
</li>
<li class="level1"><div class="li"> Rotate the pivot node.<pre class="code java">        pivot.<span class="me1">rotate</span><span class="br0">(</span> 0.4f , 0.4f , 0.0f <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 If you run the app now, you see two boxes on top of each other – both tilted at the same angle.
</p>
</div>
</li>
</ol>

</div>
<!-- EDIT6 SECTION "Understanding the Code" [4197-6600] -->
<h3 class="sectionedit7" id="what_is_a_pivot_node">What is a Pivot Node?</h3>
<div class="level3">

<p>
You can transform (e.g. rotate) Geometries around their own center, or around a user defined center point. A user defined center point for one or more Geometries is called pivot.
</p>
<ul>
<li class="level1"><div class="li"> In this example, you have grouped two Geometries by attaching them to one pivot Node. You use the pivot Node as a handle to rotate the two Geometries together around one common center. Rotating the pivot Node rotates all attached Geometries, in one step. The pivot node is the center of the rotation. Before attaching the other Geometries, make certain that the pivot node is at (0,0,0). Transforming a parent Node to transform all attached child Spatials is a common task. You will use this method a lot in your games when you move Spatials around. <br />
<strong>Examples:</strong> A vehicle and its driver move together; a planet with its moon orbits the sun. </div>
</li>
<li class="level1"><div class="li"> Contrast this case with the other option: If you don't create an extra pivot node and transform a Geometry, then every transformation is done relative to the Geometry's origin (typically the center). <br />
<strong>Examples:</strong> If you rotate each cube directly (using <code>red.rotate(0.1f , 0.2f , 0.3f);</code> and <code>blue.rotate(0.5f , 0.0f , 0.25f);</code>), then each cube is rotated individually around its center. This is similar to a planet rotating around its own center.</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "What is a Pivot Node?" [6601-7921] -->
<h2 class="sectionedit8" id="how_do_i_populate_the_scenegraph">How do I Populate the Scenegraph?</h2>
<div class="level2">
<div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Task…? </th><th class="col1"> Solution! </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Create a Spatial </td><td class="col1"> Create a Mesh shape, wrap it into a Geometry, and give it a Material. For example: <pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// a cuboid default mesh</span>
Geometry thing <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"thing"</span>, mesh<span class="br0">)</span><span class="sy0">;</span> 
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
   <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
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
		<td class="col0"> Find a Spatial in the scene by the object's name, or ID, or by its position in the parent-child hierarchy. </td><td class="col1"> Look at the node's children or parent: <pre class="code java">Spatial thing <span class="sy0">=</span> rootNode.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"thing"</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial twentyThird <span class="sy0">=</span> rootNode.<span class="me1">getChild</span><span class="br0">(</span><span class="nu0">22</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial parent <span class="sy0">=</span> myNode.<span class="me1">getParent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row5">
		<td class="col0"> Specify what should be loaded at the start </td><td class="col1"> Everything you initialize and attach to the <code>rootNode</code> in the <code>simpleInitApp()</code> method is part of the scene at the start of the game. </td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [7969-9262] -->
</div>
<!-- EDIT8 SECTION "How do I Populate the Scenegraph?" [7922-9263] -->
<h2 class="sectionedit10" id="how_do_i_transform_spatials">How do I Transform Spatials?</h2>
<div class="level2">

<p>
There are three types of 3D transformation: Translation, Scaling, and Rotation.
</p>
<div class="table sectionedit11"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Translation moves Spatials </th><th class="col1"> X-axis </th><th class="col2"> Y-axis </th><th class="col3"> Z-axis </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Specify the new location in three dimensions: How far away is it from the origin going right-up-forward? <br />
To move a Spatial <em>to</em> specific coordinates, such as (0,40.2f,-2), use: <pre class="code java">thing.<span class="me1">setLocalTranslation</span><span class="br0">(</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.0f, 40.2f, <span class="sy0">-</span>2.0f <span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 To move a Spatial <em>by</em> a certain amount, e.g. higher up (y=40.2f) and further back (z=-2.0f): 
</p>
<pre class="code java">thing.<span class="me1">move</span><span class="br0">(</span> 0.0f, 40.2f, <span class="sy0">-</span>2.0f <span class="br0">)</span><span class="sy0">;</span></pre>
</td><td class="col1">+right -left</td><td class="col2">+up -down</td><td class="col3">+forward -backward</td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [9387-9903] --><div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Scaling resizes Spatials </th><th class="col1"> X-axis </th><th class="col2"> Y-axis </th><th class="col3"> Z-axis </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Specify the scaling factor in each dimension: length, height, width. <br />
A value between 0.0f and 1.0f shrinks the Spatial; bigger than 1.0f stretches it; 1.0f keeps it the same. <br />
Using the same value for each dimension scales proportionally, different values stretch it. <br />
To scale a Spatial 10 times longer, one tenth the height, and keep the same width: <pre class="code java">thing.<span class="me1">scale</span><span class="br0">(</span> 10.0f, 0.1f, 1.0f <span class="br0">)</span><span class="sy0">;</span></pre>
</td><td class="col1">length</td><td class="col2">height</td><td class="col3">width</td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [9905-10394] --><div class="table sectionedit13"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Rotation turns Spatials </th><th class="col1"> X-axis </th><th class="col2"> Y-axis </th><th class="col3"> Z-axis </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">3-D rotation is a bit tricky (<a href="/jme3/rotate.html" class="wikilink1" title="jme3:rotate">learn details here</a>). In short: You can rotate around three axes: Pitch, yaw, and roll. You can specify angles in degrees by multiplying the degrees value with <code>FastMath.DEG_TO_RAD</code>. <br />
To roll an object 180° around the z axis: <pre class="code java">thing.<span class="me1">rotate</span><span class="br0">(</span> 0f , 0f , <span class="nu0">180</span><span class="sy0">*</span>FastMath.<span class="me1">DEG_TO_RAD</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Tip: If your game idea calls for a serious amount of rotations, it is worth looking into <a href="/jme3/quaternion.html" class="wikilink1" title="jme3:quaternion">quaternion</a>s, a data structure that can combine and store rotations efficiently. 
</p>
<pre class="code java">thing.<span class="me1">setLocalRotation</span><span class="br0">(</span> 
  <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span><span class="nu0">180</span><span class="sy0">*</span>FastMath.<span class="me1">DEG_TO_RAD</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</td><td class="col1">pitch = nodding your head</td><td class="col2">yaw = shaking your head</td><td class="col3">roll = cocking your head</td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [10396-11177] -->
</div>
<!-- EDIT10 SECTION "How do I Transform Spatials?" [9264-11178] -->
<h2 class="sectionedit14" id="how_do_i_troubleshoot_spatials">How do I Troubleshoot Spatials?</h2>
<div class="level2">

<p>
If you get unexpected results, check whether you made the following common mistakes:
</p>
<div class="table sectionedit15"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Problem? </th><th class="col1"> Solution! </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> A created Geometry does not appear in the scene. </td><td class="col1"> Have you attached it to (a node that is attached to) the rootNode? <br />
Does it have a Material? <br />
What is its translation (position)? Is it behind the camera or covered up by another Geometry? <br />
Is it to tiny or too gigantic to see? <br />
Is it too far from the camera? (Try <a href="http://jmonkeyengine.org/javadoc/com/jme3/renderer/Camera.html#setFrustumFar%28float%29" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/renderer/Camera.html#setFrustumFar%28float%29" rel="nofollow">cam.setFrustumFar</a>(111111f); to see further) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> A Spatial rotates in unexpected ways. </td><td class="col1"> Did you use radian values, and not degrees? (If you used degrees, multiply them with FastMath.DEG_TO_RAD to convert them to radians)  <br />
Did you create the Spatial at the origin (Vector.ZERO) before moving it? <br />
Did you rotate around the intended pivot node or around something else? <br />
Did you rotate around the right axis? </td>
	</tr>
	<tr class="row3">
		<td class="col0"> A Geometry has an unexpected Color or Material. </td><td class="col1 leftalign"> Did you reuse a Material from another Geometry and have inadvertently changed its properties? (If so, consider cloning it: mat2 = mat.clone(); )  </td>
	</tr>
</table></div>
<!-- EDIT15 TABLE [11310-12368] -->
</div>
<!-- EDIT14 SECTION "How do I Troubleshoot Spatials?" [11179-12369] -->
<h2 class="sectionedit16" id="how_do_i_add_custom_data_to_spatials">How do I Add Custom Data to Spatials?</h2>
<div class="level2">

<p>
Many Spatials represent game characters or other entities that the player can interact with. The above code that rotates the two boxes around a common center (pivot) could be used for a spacecraft docked to a orbiting space station, for example.
</p>

<p>
Depending on your game, game entities do not only change their position, rotation, or scale (the transformations that you just learned about). Game entities also have custom properties, such as health, inventory carried, equipment worn for a character, or hull strength and fuel left for a spacecraft. In Java, you represent entity data as class variables, e.g. floats, Strings, or Arrays. 
</p>

<p>
You can add custom data directly to any Node or Geometry. <strong>You do not need to extend the Node class to include variables</strong>!
For example, to add a custom id number to a node, you would use:
</p>
<pre class="code java">pivot.<span class="me1">setUserData</span><span class="br0">(</span> <span class="st0">"pivot id"</span>, <span class="nu0">42</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To read this Node's id number elsewhere, you would use:
</p>
<pre class="code java"><span class="kw4">int</span> id <span class="sy0">=</span> pivot.<span class="me1">getUserData</span><span class="br0">(</span> <span class="st0">"pivot id"</span> <span class="br0">)</span><span class="sy0">;</span> </pre>

<p>
By using different Strings keys (here the key is <code>pivot id</code>), you can get and set several values for whatever data the Spatial needs to carry. When you start writing your game, you might add a fuel value to a car node, speed value to an airplane node, or number of gold coins to a player node, and much more. 
</p>

</div>
<!-- EDIT16 SECTION "How do I Add Custom Data to Spatials?" [12370-13735] -->
<h2 class="sectionedit17" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
You have learned that your 3D scene is a scene graph made up of Spatials: Visible Geometries and invisible Nodes. You can transform Spatials, or attach them to nodes and transform the nodes. You know the easiest way how to add custom entity properties (such as player health or vehicle speed) to Spatials.
</p>

<p>
Since standard shapes like spheres and boxes get old fast, continue with the next chapter where you learn to <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset">load assets such as 3-D models</a>.
</p>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/rootnode.html" class="wikilink1" title="tag:rootnode" rel="tag">rootNode</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/color.html" class="wikilink1" title="tag:color" rel="tag">color</a>,
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>
</span></div>

</div>
<!-- EDIT17 SECTION "Conclusion" [13736-] -->
