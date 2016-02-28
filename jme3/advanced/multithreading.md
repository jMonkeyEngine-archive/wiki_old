---
title: The jME3 Threading Model
---
<h3 class="sectionedit1" id="the_jme3_threading_model">The jME3 Threading Model</h3>
<div class="level3">

<p>
jME3 is similar to Swing in that, for speed and efficiency, all changes to the scene graph must be made in a single update thread. If you make changes only in Control.update(), AppState.update(), or SimpleApplication.simpleUpdate(), this will happen automatically.  However, if you pass work to another thread, you may need to pass results back to the main jME3 thread so that scene graph changes can take place there.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> rotateGeometry<span class="br0">(</span><span class="kw1">final</span> Geometry geo, <span class="kw1">final</span> Quaternion rot<span class="br0">)</span> <span class="br0">{</span>
    mainApp.<span class="me1">enqueue</span><span class="br0">(</span><span class="kw1">new</span> Callable<span class="sy0">&lt;</span>Spatial<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">public</span> Spatial call<span class="br0">(</span><span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> <span class="br0">{</span>
            <span class="kw1">return</span> geo.<span class="me1">rotate</span><span class="br0">(</span>rot<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
Note that this example does not fetch the returned value by calling <code>get()</code> on the Future object returned from <code>enqueue()</code>. This means that the example method <code>rotateGeometry()</code> will return immediately and will not wait for the rotation to be processed before continuing.
</p>

<p>
If the processing thread needs to wait or needs the return value then <code>get()</code> or the other methods in the returned Future object such as <code>isDone()</code> can be used.
</p>

</div>
<!-- EDIT1 SECTION "The jME3 Threading Model" [1-1143] -->
<h1 class="sectionedit2" id="multithreading_optimization">Multithreading Optimization</h1>
<div class="level1">

<p>
First, make sure you know what <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states">Application States</a> and <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a> are.
</p>

<p>
More complex games may feature complex mathematical operations or artificial intelligence calculations (such as path finding for several NPCs). If you make many time-intensive calls on the same thread (in the update loop), they will block one another, and thus slow down the game to a degree that makes it unplayable. If your game requires long running tasks, you should run them concurrently on separate threads, which speeds up the application considerably.
</p>

<p>
Often multithreading means having separate detached logical loops going on in parallel, which communicate about their state. (For example, one thread for AI, one Sound, one Graphics). However we recommend to use a global update loop for game logic, and do multithreading within that loop when it is appropriate. This approach scales way better to multiple cores and does not break up your code logic. 
</p>

<p>
Effectively, each for-loop in the main update loop might be a chance for multithreading, if you can break it up into self-contained tasks.
</p>

</div>
<!-- EDIT2 SECTION "Multithreading Optimization" [1144-2274] -->
<h2 class="sectionedit3" id="java_multithreading">Java Multithreading</h2>
<div class="level2">

<p>
The java.util.concurrent package provides a good foundation for multithreading and dividing work into tasks that can be executed concurrently (hence the name). The three basic components are the Executor (supervises threads), Callable Objects (the tasks), and Future Objects (the result). You can <a href="http://download.oracle.com/javase/tutorial/essential/concurrency/" class="urlextern" title="http://download.oracle.com/javase/tutorial/essential/concurrency/" rel="nofollow">read about the concurrent package more here</a>, I will give just a short introduction.
</p>
<ul>
<li class="level1"><div class="li"> A Callable is one of the classes that gets executed on a thread in the Executor. The object represents one of several concurrent tasks (e.g, one NPC's path finding task). Each Callable is started from the updateloop by calling a method named <code>call()</code>.</div>
</li>
<li class="level1"><div class="li"> The Executor is one central object that manages all your Callables. Every time you schedule a Callable in the Executor, the Executor returns a Future object for it. </div>
</li>
<li class="level1"><div class="li"> A Future is an object that you use to check the status of an individual Callable task. The Future also gives you the return value in case one is returned.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Java Multithreading" [2275-3347] -->
<h2 class="sectionedit4" id="multithreading_in_jme3">Multithreading in jME3</h2>
<div class="level2">

<p>
So how do we implement multithreading in jME3?
</p>

<p>
Let's take the example of a Control that controls an NPC Spatial. The NPC Control has to compute a lengthy pathfinding operation for each NPC. If we would execute the operations directly in the simpleUpdate() loop, it would block the game  each time a NPC wants to move from A to B. Even if we move this behaviour into the update() method of a dedicated NPC Control, we would still get annoying freeze frames, because it still runs on the same update loop thread. 
</p>

<p>
To avoid slowdown, we decide to keep the pathfinding operations in the NPC Control, <em>but execute it on another thread</em>.
</p>

</div>
<!-- EDIT4 SECTION "Multithreading in jME3" [3348-4020] -->
<h3 class="sectionedit5" id="executor">Executor</h3>
<div class="level3">

<p>
You create the executor object in a global AppState (or the initSimpleApp() method), in any case in a high-level place where multiple controls can access it. 
</p>
<pre class="code java"><span class="coMULTI">/* This constructor creates a new executor with a core pool size of 4. */</span>
ScheduledThreadPoolExecutor executor <span class="sy0">=</span> <span class="kw1">new</span> ScheduledThreadPoolExecutor<span class="br0">(</span><span class="nu0">4</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Pool size means the executor will keep four threads alive at any time. Having more threads in the pool means that more tasks can run concurrently. But a bigger pool only results in a speed gain if the PC can handle it! Allocating a pool  that is uselessly large just wastes memory, so you need to find a good compromise: About the same to double the size of the number of cores in the computer makes sense. 
</p>

<p>
!!! Executor needs to be shut down when the application ends, in order to make the process die properly
In your simple application you can override the destroy method and shutdown the executor: 
</p>
<pre class="code java">    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> destroy<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">destroy</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        executor.<span class="me1">shutdown</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span></pre>

</div>
<!-- EDIT5 SECTION "Executor" [4021-5096] -->
<h3 class="sectionedit6" id="control_class_fields">Control Class Fields</h3>
<div class="level3">

<p>
In the NPC Control, we create the individual objects that the thread manipulates. In our example case (the pathfinding control), the task is about locations and path arrays, so we need the following variables:
</p>
<pre class="code Java"><span class="co1">//The vector to store the desired location in:</span>
Vector3f desiredLocation <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//The MyWayList object that contains the result waylist:</span>
MyWayList wayList <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
<span class="co1">//The future that is used to check the execution status:</span>
Future future <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span></pre>

<p>
Here we also created the Future variable to track the state of this task.
</p>

</div>
<!-- EDIT6 SECTION "Control Class Fields" [5097-5687] -->
<h3 class="sectionedit7" id="control_update_method">Control Update() Method</h3>
<div class="level3">

<p>
Next let's look at the update() call of the Control where the time-intensive task starts. In our example, the task is the <code>findWay</code> Callable (which contains the pathfinding process). So instead of spelling out the pathfinding process  in the Control's update() loop, we start the process via <code>future = executor.submit(findWay);</code>.
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> update<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">try</span><span class="br0">{</span>
        <span class="co1">//If we have no waylist and not started a callable yet, do so!</span>
        <span class="kw1">if</span><span class="br0">(</span>wayList <span class="sy0">==</span> <span class="kw2">null</span> <span class="sy0">&amp;&amp;</span> future <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
            <span class="co1">//set the desired location vector, after that we should not modify it anymore</span>
            <span class="co1">//because it's being accessed on the other thread!</span>
            desiredLocation.<span class="me1">set</span><span class="br0">(</span>getGoodNextLocation<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co1">//start the callable on the executor</span>
            future <span class="sy0">=</span> executor.<span class="me1">submit</span><span class="br0">(</span>findWay<span class="br0">)</span><span class="sy0">;</span>    <span class="co1">//  Thread starts!</span>
        <span class="br0">}</span>
        <span class="co1">//If we have started a callable already, we check the status</span>
        <span class="kw1">else</span> <span class="kw1">if</span><span class="br0">(</span>future <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
            <span class="co1">//Get the waylist when its done</span>
            <span class="kw1">if</span><span class="br0">(</span>future.<span class="me1">isDone</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
                wayList <span class="sy0">=</span> future.<span class="me1">get</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                future <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
            <span class="br0">}</span>
            <span class="kw1">else</span> <span class="kw1">if</span><span class="br0">(</span>future.<span class="me1">isCancelled</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">{</span>
                <span class="co1">//Set future to null. Maybe we succeed next time...</span>
                future <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span> 
    <span class="kw1">catch</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span><span class="br0">{</span> 
      Exceptions.<span class="me1">printStackTrace</span><span class="br0">(</span>e<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">if</span><span class="br0">(</span>wayList <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span><span class="br0">{</span>
        <span class="co1">//.... Success! Let's process the wayList and move the NPC...</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Note how this logic makes its decision based on the Future object.
</p>

<p>
Remember not to mess with the class fields after starting the thread, because they are being accessed and modified on the new thread. In more obvious terms: You cannot change the “desired location” of the NPC while the path finder is calculating a different path. You have to cancel the current Future first.
</p>

</div>
<!-- EDIT7 SECTION "Control Update() Method" [5688-7559] -->
<h3 class="sectionedit8" id="the_callable">The Callable</h3>
<div class="level3">

<p>
The next code sample shows the Callable that is dedicated to performing the long-running task (here, wayfinding). This is the task that used to block the rest of the application, and is now executed on a thread of its own. You implement the task in the Callable always in an inner method named <code>call()</code>.
</p>

<p>
The task code in the Callable should be self-contained! It should not write or read any data of objects that are managed by the scene graph or OpenGL thread directly. Even reading locations of Spatials can be problematic! So ideally all data that is needed for the wayfinding process should be available to the new thread when it starts already, possibly in a cloned version so no concurrent access to the data happens.
</p>

<p>
In reality, you might need access to the game state. If you must read or write a current state from the scene graph, you must have a clone of the data in your thread. There are only two ways:
</p>
<ul>
<li class="level1"><div class="li"> Use the execution queue <code>application.enqueue()</code> to create a sub-thread that clones the info. Only disadvantage is, it may be slower. <br />
The example below gets the <code>Vector3f location</code> from the scene object <code>mySpatial</code> using this way.</div>
</li>
<li class="level1"><div class="li"> Create a separate World class that allows safe access to its data via synchronized methods to access the scene graph. Alternatively it can also internally use <code>application.enqueue()</code>. <br />
The following example gets the object <code>Data data = myWorld.getData();</code> using this way.</div>
</li>
</ul>

<p>
These two ways are thread-safe, they don't mess up the game logic, and keep the Callable code readable.
</p>
<pre class="code java"><span class="co1">// A self-contained time-intensive task:</span>
<span class="kw1">private</span> Callable<span class="sy0">&lt;</span>MyWayList<span class="sy0">&gt;</span> findWay <span class="sy0">=</span> <span class="kw1">new</span> Callable<span class="sy0">&lt;</span>MyWayList<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
    <span class="kw1">public</span> MyWayList call<span class="br0">(</span><span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> <span class="br0">{</span>
 
        <span class="co1">//Read or write data from the scene graph -- via the execution queue:</span>
        Vector3f location <span class="sy0">=</span> application.<span class="me1">enqueue</span><span class="br0">(</span><span class="kw1">new</span> Callable<span class="sy0">&lt;</span>Vector3f<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">public</span> Vector3f call<span class="br0">(</span><span class="br0">)</span> <span class="kw1">throws</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> <span class="br0">{</span>
                <span class="co1">//we clone the location so we can use the variable safely on our thread</span>
                <span class="kw1">return</span> mySpatial.<span class="me1">getLocalTranslation</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">clone</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span><span class="br0">)</span>.<span class="me1">get</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// This world class allows safe access via synchronized methods</span>
        Data data <span class="sy0">=</span> myWorld.<span class="me1">getData</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> 
 
        <span class="co1">//... Now process data and find the way ...</span>
 
        <span class="kw1">return</span> wayList<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT8 SECTION "The Callable" [7560-9926] -->
<h2 class="sectionedit9" id="useful_links">Useful Links</h2>
<div class="level2">

<p>
High level description which describes how to manage the game state and the rendering in different threads - <del><a href="http://www.altdevblogaday.com/2011/07/03/threading-and-your-game-loop/" class="urlextern" title="http://www.altdevblogaday.com/2011/07/03/threading-and-your-game-loop/" rel="nofollow">link</a></del> Outdated link. A C++ example can be found at <a href="http://gamasutra.com/blogs/AndreaMagnorsky/20130527/193087/Multithreading_rendering_in_a_game_engine_with_CDouble_buffer_implementation.php" class="urlextern" title="http://gamasutra.com/blogs/AndreaMagnorsky/20130527/193087/Multithreading_rendering_in_a_game_engine_with_CDouble_buffer_implementation.php" rel="nofollow">link</a>
</p>

</div>
<!-- EDIT9 SECTION "Useful Links" [9927-10347] -->
<h2 class="sectionedit10" id="conclusion">Conclusion</h2>
<div class="level2">

<p>
The cool thing about this approach is that every entity creates one self-contained Callable for the Executor, and they are all executed in parallel. In theory, you can have one thread per entity without changing anything else but the settings of the executor.
</p>
<div class="tags"><span>
	<a href="/tag/loop.html" class="wikilink1" title="tag:loop" rel="tag">loop</a>,
	<a href="/tag/game.html" class="wikilink1" title="tag:game" rel="tag">game</a>,
	<a href="/tag/performance.html" class="wikilink1" title="tag:performance" rel="tag">performance</a>,
	<a href="/tag/state.html" class="wikilink1" title="tag:state" rel="tag">state</a>,
	<a href="/tag/states.html" class="wikilink1" title="tag:states" rel="tag">states</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>
</span></div>

</div>
<!-- EDIT10 SECTION "Conclusion" [10348-] -->
