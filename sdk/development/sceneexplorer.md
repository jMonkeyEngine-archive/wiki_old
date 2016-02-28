---
title: The SceneExplorer
---
<h1 class="sectionedit1" id="the_sceneexplorer">The SceneExplorer</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "The SceneExplorer" [1-32] -->
<h2 class="sectionedit2" id="adding_node_types_to_sceneexplorer">Adding Node types to SceneExplorer</h2>
<div class="level2">

<p>
If your plugin brings in its own SceneGraph objects you can still have them work like any other SceneExplorer item, including its special properties.
</p>

<p>
If you want to support special properties of your objects that are not exposed by the SDK automatically, you will have to create your own class that extends org.openide.nodes.Node and implement the interface com.jme3.gde.core.sceneexplorer.nodes.AbstractSceneExplorerNode. Then you register that class by adding 
</p>
<pre class="code">@org.openide.util.lookup.ServiceProvider(service=SceneExplorerNode.class)</pre>

<p>
 above the body of your class. Thats all, your Spatial type will automatically be used and displayed in the SceneExplorer. Make sure you register a jar with the used classes in the plugin preferences under “wrapped libraries”, otherwise the IDE cannot access those classes.
</p>

<p>
AbstractSceneExplorerNode brings some other useful features you might want to include like automatic creation of properly threaded properties etc. JmeSpatial for example bases on it. A simple SceneExplorerNode example for an object extending Spatial would be JmeGeometry (see below). Editors for special variable types can be added using the SceneExplorerPropertyEditor interface, which can be registered as a ServiceProvider as well.
</p>

<p>
The SceneExplorerNode can be used for Spatial and Control type objects.
</p>
<ul>
<li class="level1"><div class="li"><em>Add the “Nodes <abbr title="Application Programming Interface">API</abbr>” and “Lookup <abbr title="Application Programming Interface">API</abbr>” libraries to your project when you want to use this</em></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Adding Node types to SceneExplorer" [33-1510] -->
<h3 class="sectionedit3" id="spatial_example">Spatial Example</h3>
<div class="level3">
<pre class="code java">@org.<span class="me1">openide</span>.<span class="me1">util</span>.<span class="me1">lookup</span>.<span class="me1">ServiceProvider</span><span class="br0">(</span>service<span class="sy0">=</span>SceneExplorerNode.<span class="kw1">class</span><span class="br0">)</span>
<span class="kw1">public</span> <span class="kw1">class</span> JmeGeometry <span class="kw1">extends</span> JmeSpatial <span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">static</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+image"><span class="kw3">Image</span></a> smallImage <span class="sy0">=</span>
            ImageUtilities.<span class="me1">loadImage</span><span class="br0">(</span><span class="st0">"com/jme3/gde/core/sceneexplorer/nodes/icons/geometry.gif"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">private</span> Geometry geom<span class="sy0">;</span>
 
    <span class="kw1">public</span> JmeGeometry<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> JmeGeometry<span class="br0">(</span>Geometry spatial, SceneExplorerChildren children<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span><span class="br0">(</span>spatial, children<span class="br0">)</span><span class="sy0">;</span>
        getLookupContents<span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>spatial<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">geom</span> <span class="sy0">=</span> spatial<span class="sy0">;</span>
        setName<span class="br0">(</span>spatial.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+image"><span class="kw3">Image</span></a> getIcon<span class="br0">(</span><span class="kw4">int</span> type<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> smallImage<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+image"><span class="kw3">Image</span></a> getOpenedIcon<span class="br0">(</span><span class="kw4">int</span> type<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> smallImage<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> Sheet createSheet<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        Sheet sheet <span class="sy0">=</span> <span class="kw1">super</span>.<span class="me1">createSheet</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        Sheet.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+set"><span class="kw3">Set</span></a> set <span class="sy0">=</span> Sheet.<span class="me1">createPropertiesSet</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">setDisplayName</span><span class="br0">(</span><span class="st0">"Geometry"</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">setName</span><span class="br0">(</span>Geometry.<span class="kw1">class</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry obj <span class="sy0">=</span> geom<span class="sy0">;</span><span class="co1">//getLookup().lookup(Geometry.class);</span>
        <span class="kw1">if</span> <span class="br0">(</span>obj <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span> sheet<span class="sy0">;</span>
        <span class="br0">}</span>
 
        set.<span class="me1">put</span><span class="br0">(</span>makeProperty<span class="br0">(</span>obj, <span class="kw4">int</span>.<span class="kw1">class</span>, <span class="st0">"getLodLevel"</span>, <span class="st0">"setLodLevel"</span>, <span class="st0">"Lod Level"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">put</span><span class="br0">(</span>makeProperty<span class="br0">(</span>obj, Material.<span class="kw1">class</span>, <span class="st0">"getMaterial"</span>, <span class="st0">"setMaterial"</span>, <span class="st0">"Material"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">put</span><span class="br0">(</span>makeProperty<span class="br0">(</span>obj, Mesh.<span class="kw1">class</span>, <span class="st0">"getMesh"</span>, <span class="st0">"Mesh"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        sheet.<span class="me1">put</span><span class="br0">(</span>set<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> sheet<span class="sy0">;</span>
 
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw1">Class</span> getExplorerObjectClass<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> Geometry.<span class="kw1">class</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw1">Class</span> getExplorerNodeClass<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> JmeGeometry.<span class="kw1">class</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> org.<span class="me1">openide</span>.<span class="me1">nodes</span>.<span class="me1">Node</span><span class="br0">[</span><span class="br0">]</span> createNodes<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> key, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> key2, <span class="kw4">boolean</span> readOnly<span class="br0">)</span> <span class="br0">{</span>
        SceneExplorerChildren children<span class="sy0">=</span><span class="kw1">new</span> SceneExplorerChildren<span class="br0">(</span><span class="br0">(</span>com.<span class="me1">jme3</span>.<span class="me1">scene</span>.<span class="me1">Spatial</span><span class="br0">)</span>key<span class="br0">)</span><span class="sy0">;</span>
        children.<span class="me1">setReadOnly</span><span class="br0">(</span>readOnly<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> <span class="kw1">new</span> org.<span class="me1">openide</span>.<span class="me1">nodes</span>.<span class="me1">Node</span><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="kw1">new</span> JmeGeometry<span class="br0">(</span><span class="br0">(</span>Geometry<span class="br0">)</span> key, children<span class="br0">)</span>.<span class="me1">setReadOnly</span><span class="br0">(</span>readOnly<span class="br0">)</span><span class="br0">}</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Spatial Example" [1511-3452] -->
<h3 class="sectionedit4" id="control_example">Control Example</h3>
<div class="level3">
<pre class="code java">@org.<span class="me1">openide</span>.<span class="me1">util</span>.<span class="me1">lookup</span>.<span class="me1">ServiceProvider</span><span class="br0">(</span>service<span class="sy0">=</span>SceneExplorerNode.<span class="kw1">class</span><span class="br0">)</span>
<span class="kw1">public</span> <span class="kw1">class</span> JmeGhostControl <span class="kw1">extends</span> AbstractSceneExplorerNode <span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">static</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+image"><span class="kw3">Image</span></a> smallImage <span class="sy0">=</span>
            ImageUtilities.<span class="me1">loadImage</span><span class="br0">(</span><span class="st0">"com/jme3/gde/core/sceneexplorer/nodes/icons/ghostcontrol.gif"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">private</span> GhostControl control<span class="sy0">;</span>
 
    <span class="kw1">public</span> JmeGhostControl<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> JmeGhostControl<span class="br0">(</span>GhostControl control, DataObject dataObject<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span><span class="br0">(</span>dataObject<span class="br0">)</span><span class="sy0">;</span>
        getLookupContents<span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
        getLookupContents<span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">control</span> <span class="sy0">=</span> control<span class="sy0">;</span>
        setName<span class="br0">(</span><span class="st0">"GhostControl"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+image"><span class="kw3">Image</span></a> getIcon<span class="br0">(</span><span class="kw4">int</span> type<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> smallImage<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+image"><span class="kw3">Image</span></a> getOpenedIcon<span class="br0">(</span><span class="kw4">int</span> type<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> smallImage<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> SystemAction<span class="br0">[</span><span class="br0">]</span> createActions<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw1">new</span> SystemAction<span class="br0">[</span><span class="br0">]</span><span class="br0">{</span>
                    <span class="co1">//                    SystemAction.get(CopyAction.class),</span>
                    <span class="co1">//                    SystemAction.get(CutAction.class),</span>
                    <span class="co1">//                    SystemAction.get(PasteAction.class),</span>
                    SystemAction.<span class="me1">get</span><span class="br0">(</span>DeleteAction.<span class="kw1">class</span><span class="br0">)</span>
                <span class="br0">}</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">boolean</span> canDestroy<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> <span class="sy0">!</span>readOnly<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> destroy<span class="br0">(</span><span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">destroy</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">final</span> Spatial spat<span class="sy0">=</span>getParentNode<span class="br0">(</span><span class="br0">)</span>.<span class="me1">getLookup</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookup</span><span class="br0">(</span>Spatial.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            SceneApplication.<span class="me1">getApplication</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">enqueue</span><span class="br0">(</span><span class="kw1">new</span> Callable<span class="sy0">&lt;</span>Void<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
                <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+void"><span class="kw3">Void</span></a> call<span class="br0">(</span><span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> <span class="br0">{</span>
                    spat.<span class="me1">removeControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
                    <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
                <span class="br0">}</span>
            <span class="br0">}</span><span class="br0">)</span>.<span class="me1">get</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">(</span><span class="br0">(</span>AbstractSceneExplorerNode<span class="br0">)</span>getParentNode<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">refresh</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+interruptedexception"><span class="kw3">InterruptedException</span></a> ex<span class="br0">)</span> <span class="br0">{</span>
            Exceptions.<span class="me1">printStackTrace</span><span class="br0">(</span>ex<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span>ExecutionException ex<span class="br0">)</span> <span class="br0">{</span>
            Exceptions.<span class="me1">printStackTrace</span><span class="br0">(</span>ex<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> Sheet createSheet<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        Sheet sheet <span class="sy0">=</span> <span class="kw1">super</span>.<span class="me1">createSheet</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        Sheet.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+set"><span class="kw3">Set</span></a> set <span class="sy0">=</span> Sheet.<span class="me1">createPropertiesSet</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">setDisplayName</span><span class="br0">(</span><span class="st0">"GhostControl"</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">setName</span><span class="br0">(</span>GhostControl.<span class="kw1">class</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        GhostControl obj <span class="sy0">=</span> control<span class="sy0">;</span><span class="co1">//getLookup().lookup(Spatial.class);</span>
        <span class="kw1">if</span> <span class="br0">(</span>obj <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span> sheet<span class="sy0">;</span>
        <span class="br0">}</span>
 
        set.<span class="me1">put</span><span class="br0">(</span>makeProperty<span class="br0">(</span>obj, Vector3f.<span class="kw1">class</span>, <span class="st0">"getPhysicsLocation"</span>, <span class="st0">"setPhysicsLocation"</span>, <span class="st0">"Physics Location"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">put</span><span class="br0">(</span>makeProperty<span class="br0">(</span>obj, Quaternion.<span class="kw1">class</span>, <span class="st0">"getPhysicsRotation"</span>, <span class="st0">"setPhysicsRotation"</span>, <span class="st0">"Physics Rotation"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        set.<span class="me1">put</span><span class="br0">(</span>makeProperty<span class="br0">(</span>obj, CollisionShape.<span class="kw1">class</span>, <span class="st0">"getCollisionShape"</span>, <span class="st0">"setCollisionShape"</span>, <span class="st0">"Collision Shape"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">put</span><span class="br0">(</span>makeProperty<span class="br0">(</span>obj, <span class="kw4">int</span>.<span class="kw1">class</span>, <span class="st0">"getCollisionGroup"</span>, <span class="st0">"setCollisionGroup"</span>, <span class="st0">"Collision Group"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        set.<span class="me1">put</span><span class="br0">(</span>makeProperty<span class="br0">(</span>obj, <span class="kw4">int</span>.<span class="kw1">class</span>, <span class="st0">"getCollideWithGroups"</span>, <span class="st0">"setCollideWithGroups"</span>, <span class="st0">"Collide With Groups"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        sheet.<span class="me1">put</span><span class="br0">(</span>set<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> sheet<span class="sy0">;</span>
 
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw1">Class</span> getExplorerObjectClass<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> GhostControl.<span class="kw1">class</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw1">Class</span> getExplorerNodeClass<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> JmeGhostControl.<span class="kw1">class</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> org.<span class="me1">openide</span>.<span class="me1">nodes</span>.<span class="me1">Node</span><span class="br0">[</span><span class="br0">]</span> createNodes<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> key, DataObject key2, <span class="kw4">boolean</span> cookie<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> <span class="kw1">new</span> org.<span class="me1">openide</span>.<span class="me1">nodes</span>.<span class="me1">Node</span><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span><span class="kw1">new</span> JmeGhostControl<span class="br0">(</span><span class="br0">(</span>GhostControl<span class="br0">)</span> key, key2<span class="br0">)</span>.<span class="me1">setReadOnly</span><span class="br0">(</span>cookie<span class="br0">)</span><span class="br0">}</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "Control Example" [3453-6864] -->
<h2 class="sectionedit5" id="adding_items_to_the_add_and_tools_menus">Adding items to the add and tools menus</h2>
<div class="level2">

<p>
For adding Spatials, Contols and for general tools theres premade abstract classes that you can use to extend the options. Undo/Redo is handled by the abstract class. AbstractNewSpatial<strong>Wizard</strong>Action allows you to show an AWT wizard before creating the Spatial. You can also just implement the base ServiceProvider class and return any kind of action (such as a wizard), in this case you have to handle the threading yourself!
</p>

<p>
</p><p></p><div class="noteimportant">Note that the classes you create are singletons which are used across multiple nodes and you should not store any data in local variables!
</div>


<p>
To add a new Tool, create a new AbstractToolAction:
</p>
<pre class="code java">@org.<span class="me1">openide</span>.<span class="me1">util</span>.<span class="me1">lookup</span>.<span class="me1">ServiceProvider</span><span class="br0">(</span>service <span class="sy0">=</span> ToolAction.<span class="kw1">class</span><span class="br0">)</span>
<span class="kw1">public</span> <span class="kw1">class</span> GenerateTangentsTool <span class="kw1">extends</span> AbstractToolAction <span class="br0">{</span>
 
    <span class="kw1">public</span> GenerateTangentsTool<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        name <span class="sy0">=</span> <span class="st0">"Generate Tangents"</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> doApplyTool<span class="br0">(</span>AbstractSceneExplorerNode rootNode<span class="br0">)</span> <span class="br0">{</span>
        Geometry geom <span class="sy0">=</span> rootNode.<span class="me1">getLookup</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookup</span><span class="br0">(</span>Geometry.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        Mesh mesh <span class="sy0">=</span> geom.<span class="me1">getMesh</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>mesh <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            TangentBinormalGenerator.<span class="me1">generate</span><span class="br0">(</span>mesh<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">return</span> geom<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> <span class="kw4">void</span> doUndoTool<span class="br0">(</span>AbstractSceneExplorerNode rootNode, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> undoObject<span class="br0">)</span> <span class="br0">{</span>
        Geometry geom <span class="sy0">=</span> rootNode.<span class="me1">getLookup</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookup</span><span class="br0">(</span>Geometry.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        Mesh mesh <span class="sy0">=</span> geom.<span class="me1">getMesh</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>mesh <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            mesh.<span class="me1">clearBuffer</span><span class="br0">(</span>Type.<span class="me1">Tangent</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> Class<span class="sy0">&lt;?&gt;</span> getNodeClass<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> JmeGeometry.<span class="kw1">class</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
<span class="br0">}</span></pre>

<p>
For a new Spatial or Control, use AbstractNewSpatialAction
</p>
<pre class="code java">@org.<span class="me1">openide</span>.<span class="me1">util</span>.<span class="me1">lookup</span>.<span class="me1">ServiceProvider</span><span class="br0">(</span>service <span class="sy0">=</span> NewSpatialAction.<span class="kw1">class</span><span class="br0">)</span>
<span class="kw1">public</span> <span class="kw1">class</span> NewSpecialSpatialAction <span class="kw1">extends</span> AbstractNewSpatialAction <span class="br0">{</span>
 
    <span class="kw1">public</span> NewSpecialSpatialAction<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        name <span class="sy0">=</span> <span class="st0">"Spatial"</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> Spatial doCreateSpatial<span class="br0">(</span>Node parent<span class="br0">)</span> <span class="br0">{</span>
        Spatial spatial<span class="sy0">=</span><span class="kw1">new</span> Node<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> spatial<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
or AbstractNewControlAction:
</p>
<pre class="code java">@org.<span class="me1">openide</span>.<span class="me1">util</span>.<span class="me1">lookup</span>.<span class="me1">ServiceProvider</span><span class="br0">(</span>service <span class="sy0">=</span> NewControlAction.<span class="kw1">class</span><span class="br0">)</span>
<span class="kw1">public</span> <span class="kw1">class</span> NewRigidBodyAction <span class="kw1">extends</span> AbstractNewControlAction <span class="br0">{</span>
 
    <span class="kw1">public</span> NewRigidBodyAction<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        name <span class="sy0">=</span> <span class="st0">"Static RigidBody"</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+control"><span class="kw3">Control</span></a> doCreateControl<span class="br0">(</span>Spatial spatial<span class="br0">)</span> <span class="br0">{</span>
        RigidBodyControl control <span class="sy0">=</span> spatial.<span class="me1">getControl</span><span class="br0">(</span>RigidBodyControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>control <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            spatial.<span class="me1">removeControl</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        Node parent <span class="sy0">=</span> spatial.<span class="me1">getParent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        spatial.<span class="me1">removeFromParent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        control <span class="sy0">=</span> <span class="kw1">new</span> RigidBodyControl<span class="br0">(</span><span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>parent <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            parent.<span class="me1">attachChild</span><span class="br0">(</span>spatial<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">return</span> control<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>

<h4 id="adding_using_a_wizard">Adding using a Wizard</h4>
<div class="level4">

<p>
You can create a new wizard using the wizard template in the SDK (New File→Module Development→Wizard). The Action that the template creates can easily be changed to one for adding a Control or Spatial or for applying a Tool. Note that we extend AbstractNewSpatial<strong>Wizard</strong>Action here.
</p>

<p>
A good example is the “Add SkyBox” Wizard:
</p>
<pre class="code java">@org.<span class="me1">openide</span>.<span class="me1">util</span>.<span class="me1">lookup</span>.<span class="me1">ServiceProvider</span><span class="br0">(</span>service <span class="sy0">=</span> NewSpatialAction.<span class="kw1">class</span><span class="br0">)</span>
<span class="kw1">public</span> <span class="kw1">class</span> AddSkyboxAction <span class="kw1">extends</span> AbstractNewSpatialWizardAction <span class="br0">{</span>
 
    <span class="kw1">private</span> WizardDescriptor.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a><span class="br0">[</span><span class="br0">]</span> panels<span class="sy0">;</span>
 
    <span class="kw1">public</span> AddSkyboxAction<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        name <span class="sy0">=</span> <span class="st0">"Skybox.."</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> showWizard<span class="br0">(</span>org.<span class="me1">openide</span>.<span class="me1">nodes</span>.<span class="me1">Node</span> node<span class="br0">)</span> <span class="br0">{</span>
        WizardDescriptor wizardDescriptor <span class="sy0">=</span> <span class="kw1">new</span> WizardDescriptor<span class="br0">(</span>getPanels<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        wizardDescriptor.<span class="me1">setTitleFormat</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+messageformat"><span class="kw3">MessageFormat</span></a><span class="br0">(</span><span class="st0">"{0}"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        wizardDescriptor.<span class="me1">setTitle</span><span class="br0">(</span><span class="st0">"Skybox Wizard"</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+dialog"><span class="kw3">Dialog</span></a> dialog <span class="sy0">=</span> DialogDisplayer.<span class="me1">getDefault</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">createDialog</span><span class="br0">(</span>wizardDescriptor<span class="br0">)</span><span class="sy0">;</span>
        dialog.<span class="me1">setVisible</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
        dialog.<span class="me1">toFront</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw4">boolean</span> cancelled <span class="sy0">=</span> wizardDescriptor.<span class="me1">getValue</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">!=</span> WizardDescriptor.<span class="me1">FINISH_OPTION</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>cancelled<span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span> wizardDescriptor<span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">protected</span> Spatial doCreateSpatial<span class="br0">(</span>Node parent, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> properties<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>properties <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span> generateSkybox<span class="br0">(</span><span class="br0">(</span>WizardDescriptor<span class="br0">)</span> properties<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">private</span> Spatial generateSkybox<span class="br0">(</span>WizardDescriptor wiz<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+boolean"><span class="kw3">Boolean</span></a><span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"multipleTextures"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            Texture south <span class="sy0">=</span> <span class="br0">(</span>Texture<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"textureSouth"</span><span class="br0">)</span><span class="sy0">;</span>
            Texture north <span class="sy0">=</span> <span class="br0">(</span>Texture<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"textureNorth"</span><span class="br0">)</span><span class="sy0">;</span>
            Texture east <span class="sy0">=</span> <span class="br0">(</span>Texture<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"textureEast"</span><span class="br0">)</span><span class="sy0">;</span>
            Texture west <span class="sy0">=</span> <span class="br0">(</span>Texture<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"textureWest"</span><span class="br0">)</span><span class="sy0">;</span>
            Texture top <span class="sy0">=</span> <span class="br0">(</span>Texture<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"textureTop"</span><span class="br0">)</span><span class="sy0">;</span>
            Texture bottom <span class="sy0">=</span> <span class="br0">(</span>Texture<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"textureBottom"</span><span class="br0">)</span><span class="sy0">;</span>
            Vector3f normalScale <span class="sy0">=</span> <span class="br0">(</span>Vector3f<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"normalScale"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span> SkyFactory.<span class="me1">createSky</span><span class="br0">(</span>pm, west, east, north, south, top, bottom, normalScale<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
            Texture textureSingle <span class="sy0">=</span> <span class="br0">(</span>Texture<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"textureSingle"</span><span class="br0">)</span><span class="sy0">;</span>
            Vector3f normalScale <span class="sy0">=</span> <span class="br0">(</span>Vector3f<span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"normalScale"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw4">boolean</span> useSpheremap <span class="sy0">=</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+boolean"><span class="kw3">Boolean</span></a><span class="br0">)</span> wiz.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"useSpheremap"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span> SkyFactory.<span class="me1">createSky</span><span class="br0">(</span>pm, textureSingle, normalScale, useSpheremap<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Initialize panels representing individual wizard's steps and sets
     * various properties for them influencing wizard appearance.
     */</span>
    <span class="kw1">private</span> WizardDescriptor.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a><span class="br0">[</span><span class="br0">]</span> getPanels<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>panels <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            panels <span class="sy0">=</span> <span class="kw1">new</span> WizardDescriptor.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+panel"><span class="kw3">Panel</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span>
                        <span class="kw1">new</span> SkyboxWizardPanel1<span class="br0">(</span><span class="br0">)</span>,
                        <span class="kw1">new</span> SkyboxWizardPanel2<span class="br0">(</span><span class="br0">)</span>
                    <span class="br0">}</span><span class="sy0">;</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> steps <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span>panels.<span class="me1">length</span><span class="br0">]</span><span class="sy0">;</span>
            <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> panels.<span class="me1">length</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
                <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+component"><span class="kw3">Component</span></a> c <span class="sy0">=</span> panels<span class="br0">[</span>i<span class="br0">]</span>.<span class="me1">getComponent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="co1">// Default step name to component name of panel. Mainly useful</span>
                <span class="co1">// for getting the name of the target chooser to appear in the</span>
                <span class="co1">// list of steps.</span>
                steps<span class="br0">[</span>i<span class="br0">]</span> <span class="sy0">=</span> c.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="kw1">if</span> <span class="br0">(</span>c <span class="kw1">instanceof</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jcomponent"><span class="kw3">JComponent</span></a><span class="br0">)</span> <span class="br0">{</span> <span class="co1">// assume Swing components</span>
                    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jcomponent"><span class="kw3">JComponent</span></a> jc <span class="sy0">=</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+jcomponent"><span class="kw3">JComponent</span></a><span class="br0">)</span> c<span class="sy0">;</span>
                    <span class="co1">// Sets step number of a component</span>
                    <span class="co1">// TODO if using org.openide.dialogs &gt;= 7.8, can use WizardDescriptor.PROP_*:</span>
                    jc.<span class="me1">putClientProperty</span><span class="br0">(</span><span class="st0">"WizardPanel_contentSelectedIndex"</span>, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+integer"><span class="kw3">Integer</span></a><span class="br0">(</span>i<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="co1">// Sets steps names for a panel</span>
                    jc.<span class="me1">putClientProperty</span><span class="br0">(</span><span class="st0">"WizardPanel_contentData"</span>, steps<span class="br0">)</span><span class="sy0">;</span>
                    <span class="co1">// Turn on subtitle creation on each step</span>
                    jc.<span class="me1">putClientProperty</span><span class="br0">(</span><span class="st0">"WizardPanel_autoWizardStyle"</span>, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+boolean"><span class="kw3">Boolean</span></a>.<span class="kw2">TRUE</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="co1">// Show steps on the left side with the image on the background</span>
                    jc.<span class="me1">putClientProperty</span><span class="br0">(</span><span class="st0">"WizardPanel_contentDisplayed"</span>, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+boolean"><span class="kw3">Boolean</span></a>.<span class="kw2">TRUE</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="co1">// Turn on numbering of all steps</span>
                    jc.<span class="me1">putClientProperty</span><span class="br0">(</span><span class="st0">"WizardPanel_contentNumbered"</span>, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+boolean"><span class="kw3">Boolean</span></a>.<span class="kw2">TRUE</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
        <span class="kw1">return</span> panels<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
</p><p></p><div class="notetip">The abstract spatial and control actions implement undo/redo automatically, for the ToolActions you have to implement it yourself.
</div>


</div>
<!-- EDIT5 SECTION "Adding items to the add and tools menus" [6865-] -->
