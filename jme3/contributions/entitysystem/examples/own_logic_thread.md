---
title: Your Own Logic Thread
---
<h1 class="sectionedit1" id="your_own_logic_thread">Your Own Logic Thread</h1>
<div class="level1">

<p>
You can add AppStates to the SimpleApplication and your whole program will run on a single thread.
This can have benefits, but this Entity System is optimized to run on several Threads.
Because of this, it is recommended that you run the game logic in a separate thread and independent from the framerate.
In this example, we will say that we want to run the game logic every 20 milliseconds. This means 50 updates per second and a tpf value of 0.2f   .
</p>

</div>
<!-- EDIT1 SECTION "Your Own Logic Thread" [1-491] -->
<h2 class="sectionedit2" id="gamelogic_class">GameLogic class</h2>
<div class="level2">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> GameLogicThread <span class="kw1">implements</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+runnable"><span class="kw3">Runnable</span></a> <span class="br0">{</span>
 
    <span class="kw1">private</span> <span class="kw1">final</span> <span class="kw4">float</span> tpf <span class="sy0">=</span> 0.02f<span class="sy0">;</span>
    <span class="kw1">private</span> AppStateManager stateManager<span class="sy0">;</span>
 
    <span class="kw1">public</span> GameLogicThread<span class="br0">(</span>Application app<span class="br0">)</span> <span class="br0">{</span>
        stateManager <span class="sy0">=</span> <span class="kw1">new</span> AppStateManager<span class="br0">(</span>app<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//add the logic AppStates to this thread</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">new</span> MovementAppState<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">new</span> ExpiresAppState<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">new</span> CollisionAppState<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">new</span> EnemyAppState<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw4">void</span> run<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        stateManager.<span class="me1">update</span><span class="br0">(</span>tpf<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "GameLogic class" [492-1099] -->
<h2 class="sectionedit3" id="application">Application</h2>
<div class="level2">
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> Example <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">private</span> EntitySystem entitySystem<span class="sy0">;</span>
    <span class="kw1">private</span> ScheduledExecutorService exec<span class="sy0">;</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        <span class="co1">//Init the Entity System</span>
        entitySystem <span class="sy0">=</span> <span class="kw1">new</span> EntitySystem<span class="br0">(</span><span class="kw1">new</span> MapEntityData<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//Init the Game Systems for the visualisation</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">new</span> EntityDisplayAppState<span class="br0">(</span>rootNode<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        stateManager.<span class="me1">attach</span><span class="br0">(</span><span class="kw1">new</span> PlayerInputAppState<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">//create the Thread for the game logic</span>
        exec <span class="sy0">=</span> Executors.<span class="me1">newSingleThreadScheduledExecutor</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        exec.<span class="me1">scheduleAtFixedRate</span><span class="br0">(</span><span class="kw1">new</span> GameLogicThread<span class="br0">(</span><span class="kw1">this</span><span class="br0">)</span>, <span class="nu0">0</span>, <span class="nu0">20</span>, TimeUnit.<span class="me1">MILLISECONDS</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> EntitySystem getEntitySystem<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> entitySystem<span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> destroy<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span>.<span class="me1">destroy</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">//Shutdown the thread when the game is closed</span>
        exec.<span class="me1">shutdown</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT3 SECTION "Application" [1100-] -->
