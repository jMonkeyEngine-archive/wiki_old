---
title: jMonkeyEngine SDK -- The Scene
---
<h1 class="sectionedit1" id="jmonkeyengine_sdk_--_the_scene">jMonkeyEngine SDK -- The Scene</h1>
<div class="level1">

<p>
To reduce system overhead the jMonkeyEngine SDK Core supplies one scene/jme3 application that is shared between plugins. Furthermore there's the “SceneExplorer” that shows a visual representation of the scenegraph and its objects properties across plugins.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK -- The Scene" [1-304] -->
<h2 class="sectionedit2" id="how_to_access_the_scene">How to access the Scene</h2>
<div class="level2">

<p>
There are several ways for your plugin to interact with the Scene:
</p>
<ul>
<li class="level1"><div class="li"> It listens for selected spatials / objects and offers options for those</div>
</li>
<li class="level1"><div class="li"> It requests the whole scene for itself and loads/arranges the content in it (e.g. a terrain editor or model animation plugin).</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "How to access the Scene" [305-616] -->
<h2 class="sectionedit3" id="listening_for_node_selection">Listening for Node selection</h2>
<div class="level2">

<p>
In the jMonkeyEngine SDK, all objects are wrapped into NetBeans “Nodes” (different thing than jme Nodes!). Such nodes can have properties and icons and can be displayed and selected in the jMonkeyEngine SDK UI. The SceneExplorer shows a tree of Nodes that wrap the Spatials of the current scene and allows manipulating their properties on selection. A jME “Spatial” is wrapped by a “JmeSpatial” node, for example. One advantage of these Nodes is that one can manipulate properties of Spatials directly from the AWT thread.
</p>

<p>
To listen to the current selection, implement org.openide.util.LookupListener and register like this:
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw1">final</span> Result<span class="sy0">&lt;</span>JmeSpatial<span class="sy0">&gt;</span> result<span class="sy0">;</span>
 
<span class="co1">//method to register the listener;</span>
<span class="kw1">private</span> <span class="kw4">void</span> registerListener<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    result <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+utilities"><span class="kw3">Utilities</span></a>.<span class="me1">actionsGlobalContext</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookupResult</span><span class="br0">(</span>JmeSpatial.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    result.<span class="me1">addLookupListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="co1">//implements org.openide.util.LookupListener (called from AWT thread)</span>
<span class="kw1">public</span> <span class="kw4">void</span> resultChanged<span class="br0">(</span>LookupEvent ev<span class="br0">)</span> <span class="br0">{</span>
    Collection<span class="sy0">&lt;</span>JmeSpatial<span class="sy0">&gt;</span> items <span class="sy0">=</span> <span class="br0">(</span>Collection<span class="sy0">&lt;</span>JmeSpatial<span class="sy0">&gt;</span><span class="br0">)</span> result.<span class="me1">allInstances</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">for</span> <span class="br0">(</span>JmeSpatial jmeSpatial <span class="sy0">:</span> items<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">//Using the JmeSpatials properties you can modify the spatial directly from the AWT thread:</span>
        jmeSpatial.<span class="me1">getPropertySets</span><span class="br0">(</span><span class="br0">)</span><span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span>.<span class="me1">setValue</span><span class="br0">(</span><span class="st0">"Local Translation"</span>, Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
You can also access the “real” spatial but since its part of the scenegraph you will have to modify it on that thread:
</p>
<pre class="code java"><span class="co1">//retrieve the "real" spatial class from the JmeNode</span>
<span class="kw1">for</span> <span class="br0">(</span>JmeSpatial jmeSpatial <span class="sy0">:</span> items<span class="br0">)</span> <span class="br0">{</span>
    <span class="co1">//the spatial is stored inside the JmeSpatials "Lookup", a general container for Objects</span>
    <span class="kw1">final</span> Spatial realSpatial <span class="sy0">=</span> jmeSpatial.<span class="me1">getLookup</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookup</span><span class="br0">(</span>Spatial.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//use a Callable to execute on the render thread:</span>
    SceneApplication.<span class="me1">getApplication</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">enqueue</span><span class="br0">(</span><span class="kw1">new</span> Callable<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a> call<span class="br0">(</span><span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> <span class="br0">{</span>
            realSpatial.<span class="me1">setLocalTranslation</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Listening for Node selection" [617-2667] -->
<h2 class="sectionedit4" id="requesting_the_scene">Requesting the Scene</h2>
<div class="level2">

<p>
If your plugin wants to use the scene by itself, it first has to implement SceneListener and register at the scene and then send a SceneRequest to the SceneApplication. When the SceneRequest has been approved and the current Scene has been closed, the SceneListener (your class) is called with its own SceneRequest as a parameter. When another plugin sends a SceneRequest it is also reported to you and its a hint that your RootNode has been removed from the Scene and you are no longer in control of it. You could also hook into the SceneRequests of other plugins to see if/when they are activated to display add-on plugins for that plugin.
</p>

<p>
<br />

The SceneRequest object has to contain several things. A thing that you must supply is a jme “Node” wrapped into a “JmeNode” object. This is your rootNode that you use to display and build your scene. As soon as you control the scene, you will have to control the camera etc. yourself.
</p>
<pre class="code java">com.<span class="me1">jme3</span>.<span class="me1">scene</span>.<span class="me1">Node</span> rootNode <span class="sy0">=</span> <span class="kw1">new</span> com.<span class="me1">jme3</span>.<span class="me1">scene</span>.<span class="me1">Node</span><span class="br0">(</span><span class="st0">"MyRootNode"</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">private</span> <span class="kw4">void</span> registerSceneListener<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    SceneApplication.<span class="me1">getApplication</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">addSceneListener</span><span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">private</span> <span class="kw4">void</span> requestScene<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    <span class="co1">//create a jmeNode from the rootNode using the NodeUtility</span>
    JmeNode jmeNode <span class="sy0">=</span> NodeUtility.<span class="me1">createNode</span><span class="br0">(</span>rootNode<span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//create the scene request</span>
    SceneRequest request<span class="sy0">=</span><span class="kw1">new</span> SceneRequest<span class="br0">(</span><span class="kw1">this</span>, jmeNode, assetManager<span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//request the scene</span>
    SceneApplication.<span class="me1">getApplication</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">openScene</span><span class="br0">(</span>request<span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="co1">//implements SceneListener (called from AWT thread)</span>
<span class="kw1">public</span> <span class="kw4">void</span> sceneOpened<span class="br0">(</span>SceneRequest request<span class="br0">)</span><span class="br0">{</span>
    <span class="co1">//check if its our request</span>
    <span class="kw1">if</span> <span class="br0">(</span>request.<span class="me1">getRequester</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">==</span> <span class="kw1">this</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">//we now own the scene, any operations on the scene have to be done via Callables</span>
    <span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw1">public</span> <span class="kw4">void</span> sceneClosed<span class="br0">(</span>SceneRequest request<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span>request.<span class="me1">getRequester</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">==</span> <span class="kw1">this</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">//we have to close the scene,  any operations on the scene have to be done via Callables</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "Requesting the Scene" [2668-4630] -->
<h2 class="sectionedit5" id="undo_redo_support">Undo/Redo support</h2>
<div class="level2">

<p>
The jMonkeyEngine SDK has a global undo/redo queue that activates the undo/redo buttons. To use it in your TopComponent, add the following method:
</p>
<pre class="code java">@Override 
<span class="kw1">public</span> UndoRedo getUndoRedo<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> 
<span class="kw1">return</span> Lookup.<span class="me1">getDefault</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookup</span><span class="br0">(</span>SceneUndoRedoManager.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span> 
<span class="br0">}</span> </pre>

<p>
To add a undo/redo event that modifies objects on the Scenegraph, theres a special version of AbstractUndoableEdit which executes the undo/redo calls on the scene thread. Simply implement that class and add it to the queue like this:
</p>
<pre class="code java">Lookup.<span class="me1">getDefault</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">lookup</span><span class="br0">(</span>SceneUndoRedoManager.<span class="kw1">class</span><span class="br0">)</span>.<span class="me1">addEdit</span><span class="br0">(</span><span class="kw1">this</span>, <span class="kw1">new</span> AbstractUndoableSceneEdit<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> 
 
@Override 
<span class="kw1">public</span> <span class="kw4">void</span> sceneUndo<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> 
    <span class="co1">//undo stuff in scene here</span>
<span class="br0">}</span> 
 
@Override 
<span class="kw1">public</span> <span class="kw4">void</span> sceneRedo<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> 
    <span class="co1">//redo stuff in scene here</span>
<span class="br0">}</span> 
 
@Override 
<span class="kw1">public</span> <span class="kw4">void</span> awtUndo<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> 
    <span class="co1">//undo stuff on awt thread here (updating of visual nodes etc, called post scene edit)</span>
<span class="br0">}</span> 
 
@Override 
<span class="kw1">public</span> <span class="kw4">void</span> awtRedo<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span> 
    <span class="co1">//redo stuff on awt thread here</span>
<span class="br0">}</span> 
<span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Note: Its important that you use the method addEdit(Object source, UndoableEdit edit);
</p>

</div>
<!-- EDIT5 SECTION "Undo/Redo support" [4631-] -->
