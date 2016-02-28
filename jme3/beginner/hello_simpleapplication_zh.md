---
title: 第一个JME3应用程序
---
<h1 class="sectionedit1" id="第一个jme3应用程序">第一个JME3应用程序</h1>
<div class="level1">

<p>
上一篇: <a href="/documentation_zh.html" class="wikilink1" title="documentation_zh">下载和安装</a>, 下一篇: <a href="/jme3/beginner/hello_node_zh.html" class="wikilink1" title="jme3:beginner:hello_node_zh">节点(Node)</a>
</p>

<p>
<strong>预备知识:</strong> 开始之前假设你已经<a href="/documentation_zh.html" class="wikilink1" title="documentation_zh">下载和安装jMonkeyEngine SDK</a>，并且可以顺利地运行其中的一些例子。
</p>

<p>
在JME3初级系列教程的学习过程中，我们假设你使用的是<a href="/sdk.html" class="wikilink1" title="sdk"> jMonkeyEngine SDK</a>，并且是一名具有中、高级水准的Java开发者。很快你就将学会如何使用你熟悉的IDE(如NetBeans IDE、<a href="/jme3/setting_up_jme3_in_eclipse_zh.html" class="wikilink1" title="jme3:setting_up_jme3_in_eclipse_zh">Eclipse</a>、IntelliJ，甚至是<a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline">命令行</a>)来开发JME3项目。
</p>

</div>
<!-- EDIT1 SECTION "第一个JME3应用程序" [1-706] -->
<h2 class="sectionedit2" id="创建项目">创建项目</h2>
<div class="level2">

<p>
在jMonkeyEngine SDK 里：
</p>
<ol>
<li class="level1"><div class="li"> 按 Choose File→New Project…</div>
</li>
<li class="level1"><div class="li"> 找 JME3→Basic Game，按 Next。</div>
<ol>
<li class="level2"><div class="li"> 在 Project Name 里，填写你的游戏名字。 </div>
</li>
<li class="level2"><div class="li"> 按 Project Location 右边 Browse 找你要放游戏的地方。</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> 按Finnish。</div>
</li>
</ol>

<p>
如果你有别的问题的话，请阅读<a href="/sdk/project_creation.html" class="wikilink1" title="sdk:project_creation">创建项目</a>。
</p>

</div>
<!-- EDIT2 SECTION "创建项目" [707-1069] -->
<h2 class="sectionedit3" id="写一个程序">写一个程序</h2>
<div class="level2">

<p>
在jMonkeyEngine SDK 里:
</p>
<ol>
<li class="level1"><div class="li"> 右按你的 Source Packages</div>
</li>
<li class="level1"><div class="li"> 按 New…→Java Class</div>
</li>
<li class="level1"><div class="li"> 在 Class Name 里放: <code>HelloJME3</code></div>
</li>
<li class="level1"><div class="li"> 在 Package 里放: <code>jme3test.helloworld</code>. </div>
</li>
<li class="level1"><div class="li"> 按 Finish.</div>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "写一个程序" [1070-1293] -->
<h2 class="sectionedit4" id="例子">例子</h2>
<div class="level2">

<p>
在HelloJME3.java里面，方静下面的Java：
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 1 - 怎么写一个很简单的程序。
 * 放一个蓝色的立方体在 scene graph 上。
 * 用 WASD 去动 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloJME3 <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 开始！</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 盖一个立方体在（0,0,0）</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// 用立方体盖一个 Geometry。</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// 图一个 Material。</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// 图蓝色在 Material 上。</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>                   <span class="co1">// 方 Material 在立方体上。</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>              <span class="co1">// 放 Geometry 在 Root Node 上。（让大家看到那个 Geometry）</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
按 HelloJME3，找 Run. 如果 SDK 问你要用什么 Settings，按 Default Settings。
</p>
<ol>
<li class="level1"><div class="li"> 你会看到一个蓝色的立方体。</div>
</li>
<li class="level1"><div class="li"> 按 WASD 去动来动去。</div>
</li>
<li class="level1"><div class="li"> 如果你要关 HelloJME 就按 ESC。</div>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "例子" [1294-2772] -->
<h2 class="sectionedit5" id="软件做了什么">软件做了什么</h2>
<div class="level2">

<p>
我写了一个很简单的程序。它会盖一个蓝色的立方体.
</p>

</div>
<!-- EDIT5 SECTION "软件做了什么" [2773-2874] -->
<h3 class="sectionedit6" id="开始_simpleapplication">开始 SimpleApplication</h3>
<div class="level3">

<p>
看第一行。HelloJME3 extends <code>com.jme3.app.SimpleApplication</code>。 
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HelloJME3 <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
  <span class="co1">// ...</span>
<span class="br0">}</span></pre>

<p>
每一个 JME3 游戏 是一个 <code>com.jme3.app.SimpleApplication</code> instance。 SimpleApplication 会帮你图上屏幕和你的3D Scene。
</p>

<p>
JME3 从 <code>main()</code> 来开始。在 <code>main()</code> 里面，你要:
</p>
<ol>
<li class="level1"><div class="li"> 盖一个 <code>SimpleAppliction</code> instance。（instantiate）</div>
</li>
<li class="level1"><div class="li"> 叫它的 <code>start()</code> 去开始你的程序。</div>
</li>
</ol>
<pre class="code java">    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// instantiate 你的游戏。</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>                     <span class="co1">// 开始！</span>
    <span class="br0">}</span></pre>

</div>
<!-- EDIT6 SECTION "开始 SimpleApplication" [2875-3583] -->
<h3 class="sectionedit7" id="口语到_jme_语">口语到 JME 语</h3>
<div class="level3">
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">你要做什么</th><th class="col1">怎么说在JME语言</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">你要盖一个立方体。</td><td class="col1">我盖一个用 1x1x1 Box 的 Geometry。</td>
	</tr>
	<tr class="row2">
		<td class="col0">你要用蓝色。</td><td class="col1">我图一个资料，就放蓝色在资料上面。</td>
	</tr>
	<tr class="row3">
		<td class="col0">你要一个蓝色的立方体。</td><td class="col1">我图蓝色的资料在立方体上。</td>
	</tr>
	<tr class="row4">
		<td class="col0">你要看到你的 Geometry</td><td class="col1">我放 Geometry 在 Root Node 上。</td>
	</tr>
	<tr class="row5">
		<td class="col0">我要我的立方体在中间</td><td class="col1">我放立方体在（0,0,0）<code>Vector3f.ZERO</code>。</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [3613-4023] -->
<p>
如果你还是有问题，请你看<a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph">the Scene Graph</a>。
</p>

</div>
<!-- EDIT7 SECTION "口语到 JME 语" [3584-4089] -->
<h3 class="sectionedit9" id="initialize_the_scene">Initialize the Scene</h3>
<div class="level3">

<p>
你的程序一开始后，就会自动叫<code>simpleInitApp()</code>。 每一个 JME3 游戏要有它。<code>simpleInitApp()</code>要方一开始要看到／做到的东西
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
       ／／先看到／做到的东西...
    <span class="br0">}</span></pre>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// 盖一个立方体在（0,0,0）</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// 用立方体盖一个 Geometry。</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// 图一个资料。</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// 方蓝色在资料上。</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>                   <span class="co1">// 图资料到立方体上。</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>              <span class="co1">// 放 Geometry 在 Root Node 上。（让大家看到你的 Geometry）</span>
    <span class="br0">}</span></pre>

</div>
<!-- EDIT9 SECTION "Initialize the Scene" [4090-5019] -->
<h2 class="sectionedit10" id="最后">最后</h2>
<div class="level2">

<p>
你学了 SimpleApplication 的作用：
</p>
<ul>
<li class="level1"><div class="li"> <code>simpleInitApp()</code> 里面放开始要看或做的东西。</div>
</li>
<li class="level1"><div class="li"> 要是你要看到 东西，你就要放它在 <code>rootNode</code> 上。</div>
</li>
<li class="level1"><div class="li"> 用 WASD 去动。</div>
</li>
</ul>

<p>
继续去 <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a> 你会学什么是，和你真么用 Scene Graph。
</p>
<hr />

<p>
还看:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/wiki/doku.php/" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/" rel="nofollow">下载JME3SDK</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline">SimpleApplication From the Commandline</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/project_creation.html" class="wikilink1" title="sdk:project_creation">写一个JME3 Project</a>.</div>
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
<!-- EDIT10 SECTION "最后" [5020-] -->
