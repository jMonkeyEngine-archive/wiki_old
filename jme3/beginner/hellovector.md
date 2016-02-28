---
title: 
---
<p>
<a href="/resources/jme3-beginner-hellovectorsumm2.png" class="media" title="jme3:beginner:hellovectorsumm2.png"><img src="/resources/jme3-beginner-hellovectorsumm2.png" class="media" alt="" /></a>
</p>

<p>
HelloVectorSumm.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey.chapter2.hellovector</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.renderer.RenderManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">org.jmonkey.utils.Debug</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">org.jmonkey.utils.MaterialUtils</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">org.jmonkey.utils.SpatialUtils</span><span class="sy0">;</span>
 
<span class="co3">/**
 Example Vector Summ
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloVectorSumm <span class="kw1">extends</span> SimpleApplication
<span class="br0">{</span>
 
    <span class="kw1">private</span> Node vctrNode <span class="sy0">=</span> SpatialUtils.<span class="me1">makeNode</span><span class="br0">(</span><span class="st0">"vectorNode"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> Vector3f vctrNodeLoc <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>64.0f, 64.0f, 64.0f<span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">private</span> Vector3f camLocVctr <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>512.0f, 64.0f, 0.0f<span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> Vector3f vctrNodeSpatLoc <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>64.0f, 128.0f, <span class="sy0">-</span>32.0f<span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//</span>
    <span class="kw1">private</span> Vector3f vctrSumm <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
    <span class="kw1">private</span> Vector3f scale <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">8</span>, <span class="nu0">8</span>, <span class="nu0">8</span><span class="br0">)</span><span class="sy0">;</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span>
    <span class="br0">{</span>
        HelloVectorSumm app <span class="sy0">=</span> <span class="kw1">new</span> HelloVectorSumm<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//app.setShowSettings(false);</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
        cam.<span class="me1">setLocation</span><span class="br0">(</span>camLocVctr<span class="br0">)</span><span class="sy0">;</span>
        cam.<span class="me1">lookAt</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, cam.<span class="me1">getUp</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        flyCam.<span class="me1">setMoveSpeed</span><span class="br0">(</span>100.0f<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        Debug.<span class="me1">showNodeAxes</span><span class="br0">(</span>assetManager, rootNode, <span class="nu0">128</span><span class="br0">)</span><span class="sy0">;</span>
        Debug.<span class="me1">attachWireFrameDebugGrid</span><span class="br0">(</span>assetManager, rootNode, Vector3f.<span class="me1">ZERO</span>, <span class="nu0">256</span>, ColorRGBA.<span class="me1">DarkGray</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//     </span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span><span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        Material mat <span class="sy0">=</span> MaterialUtils.<span class="me1">makeMaterial</span><span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> SpatialUtils.<span class="me1">makeGeometry</span><span class="br0">(</span>vctrNodeSpatLoc, scale, box, mat, <span class="st0">"box"</span><span class="br0">)</span><span class="sy0">;</span>
        vctrNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
        vctrNode.<span class="me1">setLocalTranslation</span><span class="br0">(</span>vctrNodeLoc<span class="br0">)</span><span class="sy0">;</span>
        vctrSumm <span class="sy0">=</span> vctrNodeLoc.<span class="me1">add</span><span class="br0">(</span>vctrNodeSpatLoc<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        Debug.<span class="me1">showNodeAxes</span><span class="br0">(</span>assetManager, vctrNode, 4.0f<span class="br0">)</span><span class="sy0">;</span>
        Debug.<span class="me1">showVector3fArrow</span><span class="br0">(</span>assetManager, rootNode, vctrNodeLoc, ColorRGBA.<span class="me1">Red</span>, <span class="st0">"vctrNodeLoc"</span><span class="br0">)</span><span class="sy0">;</span>
        Debug.<span class="me1">showVector3fArrow</span><span class="br0">(</span>assetManager, vctrNode, vctrNodeSpatLoc, ColorRGBA.<span class="me1">Green</span>, <span class="st0">"vctrNodeSpatLoc"</span><span class="br0">)</span><span class="sy0">;</span>
        Debug.<span class="me1">showVector3fArrow</span><span class="br0">(</span>assetManager, rootNode, vctrSumm, ColorRGBA.<span class="me1">Blue</span>, <span class="st0">"vctrSumm"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>vctrNode<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//n.move(tpf * 10, 0, 0);</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleRender<span class="br0">(</span>RenderManager rm<span class="br0">)</span>
    <span class="br0">{</span>
        <span class="co1">//TODO: add render code</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey.utils</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
 
<span class="co3">/**
 * Example Vector Summ
 * @author Alex Cham aka Jcrypto
 */</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> MaterialUtils
<span class="br0">{</span>
 
    <span class="kw1">public</span> MaterialUtils<span class="br0">(</span><span class="br0">)</span>
    <span class="br0">{</span>
    <span class="br0">}</span>
 
 
    <span class="co1">//"Common/MatDefs/Misc/Unshaded.j3md"</span>
    <span class="kw1">public</span> <span class="kw1">static</span> Material makeMaterial<span class="br0">(</span>AssetManager am, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name, ColorRGBA color<span class="br0">)</span>
    <span class="br0">{</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, name<span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, color<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> mat<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey.utils</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Mesh</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="co3">/**
 * Example Vector Summ
 * @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> SpatialUtils
<span class="br0">{</span>
    <span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> Node makeNode<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        Node n <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span>name<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> n<span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> Geometry makeGeometry<span class="br0">(</span>Mesh mesh, Material mat, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>name, mesh<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> geom<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> Geometry makeGeometry<span class="br0">(</span>Vector3f loc, Vector3f scl, Mesh mesh, Material mat, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>name, mesh<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setLocalTranslation</span><span class="br0">(</span>loc<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setLocalScale</span><span class="br0">(</span>scl<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> geom<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
—
Debug.java
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">org.jmonkey.utils</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.animation.AnimControl</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.asset.AssetManager</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.Arrow</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.Grid</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.debug.SkeletonDebugger</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Line</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">static</span> org.<span class="me1">jmonkey</span>.<span class="me1">utils</span>.<span class="me1">SpatialUtils</span>.<span class="me1">makeGeometry</span><span class="sy0">;</span>
 
<span class="co3">/**
 Example Vector Summ
 
 @author Alex Cham aka Jcrypto
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> Debug
<span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> showNodeAxes<span class="br0">(</span>AssetManager am, Node n, <span class="kw4">float</span> axisLen<span class="br0">)</span>
    <span class="br0">{</span>
        Vector3f v <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span>axisLen, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        Arrow a <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>n.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"XAxis"</span>, a<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
 
 
        <span class="co1">//</span>
        v <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, axisLen, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        a <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
        mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Green</span><span class="br0">)</span><span class="sy0">;</span>
        geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>n.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"YAxis"</span>, a<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
 
 
        <span class="co1">//</span>
        v <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, axisLen<span class="br0">)</span><span class="sy0">;</span>
        a <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
        mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span>n.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"ZAxis"</span>, a<span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">//</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> showVector3fArrow<span class="br0">(</span>AssetManager am, Node n, Vector3f v, ColorRGBA color, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        Arrow a <span class="sy0">=</span> <span class="kw1">new</span> Arrow<span class="br0">(</span>v<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> MaterialUtils.<span class="me1">makeMaterial</span><span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span>, color<span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> makeGeometry<span class="br0">(</span>a, mat, name<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> showVector3fLine<span class="br0">(</span>AssetManager am, Node n, Vector3f v, ColorRGBA color, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> name<span class="br0">)</span>
    <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+line"><span class="kw3">Line</span></a> l <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+line"><span class="kw3">Line</span></a><span class="br0">(</span>v.<span class="me1">subtract</span><span class="br0">(</span>v<span class="br0">)</span>, v<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> MaterialUtils.<span class="me1">makeMaterial</span><span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span>, color<span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> makeGeometry<span class="br0">(</span>l, mat, name<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="co1">//Skeleton Debugger</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> attachSkeleton<span class="br0">(</span>AssetManager am, Node player, AnimControl control<span class="br0">)</span>
    <span class="br0">{</span>
        SkeletonDebugger skeletonDebug <span class="sy0">=</span> <span class="kw1">new</span> SkeletonDebugger<span class="br0">(</span><span class="st0">"skeleton"</span>, control.<span class="me1">getSkeleton</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>am, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Yellow</span><span class="br0">)</span><span class="sy0">;</span>
        mat2.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setDepthTest</span><span class="br0">(</span><span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
        skeletonDebug.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span>
        player.<span class="me1">attachChild</span><span class="br0">(</span>skeletonDebug<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co1">///</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> attachWireFrameDebugGrid<span class="br0">(</span>AssetManager assetManager, Node n, Vector3f pos, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+integer"><span class="kw3">Integer</span></a> size, ColorRGBA color<span class="br0">)</span>
    <span class="br0">{</span>
        Geometry g <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"wireFrameDebugGrid"</span>, <span class="kw1">new</span> Grid<span class="br0">(</span>size, size, 1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span><span class="co1">//1WU</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">getAdditionalRenderState</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">setWireframe</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, color<span class="br0">)</span><span class="sy0">;</span>
        g.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        g.<span class="me1">center</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">move</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
        n.<span class="me1">attachChild</span><span class="br0">(</span>g<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>
