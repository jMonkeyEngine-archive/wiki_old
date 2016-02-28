---
title: Steer Behaviors
---
<h1 class="sectionedit1" id="steer_behaviors">Steer Behaviors</h1>
<div class="level1">

<p>
Steer behaviors allows you to control the locomotion of “characters”, this can reduce drastically the time needed to develop a game since for almost every game we need to set how these “characters” will be moving around the scene.
<br />

<br />

<strong>Steer behaviors in action:</strong>
<a href="/lib/exe/fetch.php/jme3:advanced:youtube_yyztntsgv00" class="media mediafile mf_ wikilink2" title="jme3:advanced:youtube_yyztntsgv00">youtube_yyztntsgv00</a>
<br />

Be sure that you have checked the demos: They can be downloaded here: <a href="http://localhost/jmeSteerTesting/downloads.php" class="urlextern" title="http://localhost/jmeSteerTesting/downloads.php" rel="nofollow">jmesteer.bdevel.org</a>
</p>

</div>
<!-- EDIT1 SECTION "Steer Behaviors" [1-482] -->
<h2 class="sectionedit2" id="first_steps">First steps</h2>
<div class="level2">

<p>
The steer behaviors AI is integrated with MonkeyBrains so before start coding be sure that you have checked the <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:monkey_brains" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:advanced:monkey_brains" rel="nofollow">monkey brains documentation</a>
</p>

<p>
Be sure to create a reference to MonkeyBrains from your project.
</p>

<p>
Finally, do not forget to import the <code>com.jme3.ai.agents.behaviors.npc.steering</code> package.
</p>

</div>
<!-- EDIT2 SECTION "First steps" [483-881] -->
<h2 class="sectionedit3" id="overview">Overview</h2>
<div class="level2">

<p>
<strong>Avaliable behaviours:</strong>
</p>
<ul>
<li class="level1"><div class="li"> Move</div>
</li>
<li class="level1"><div class="li"> Seek</div>
</li>
<li class="level1"><div class="li"> Arrive</div>
</li>
<li class="level1"><div class="li"> Flee</div>
</li>
<li class="level1"><div class="li"> Pursuit</div>
</li>
<li class="level1"><div class="li"> Leader follow</div>
</li>
<li class="level1"><div class="li"> Evade</div>
</li>
<li class="level1"><div class="li"> Cohesion</div>
</li>
<li class="level1"><div class="li"> Alignment</div>
</li>
<li class="level1"><div class="li"> Obstacle Avoidance</div>
</li>
<li class="level1"><div class="li"> Unaligned obstacle avoidance</div>
</li>
<li class="level1"><div class="li"> Hide </div>
</li>
<li class="level1"><div class="li"> Slow</div>
</li>
<li class="level1"><div class="li"> Queuing</div>
</li>
<li class="level1"><div class="li"> Containment</div>
</li>
<li class="level1"><div class="li"> Path follow</div>
</li>
<li class="level1"><div class="li"> Wall approach</div>
</li>
<li class="level1"><div class="li"> Wander Area</div>
</li>
<li class="level1"><div class="li"> Simple Wander</div>
</li>
<li class="level1"><div class="li"> Relative wander</div>
</li>
<li class="level1"><div class="li"> Sphere wander</div>
</li>
<li class="level1"><div class="li"> Box explore</div>
</li>
<li class="level1"><div class="li"> Separation</div>
</li>
</ul>

<p>
All the behaviours extend from the <code>AbstractSteeringBehavior</code> class.
</p>

</div>
<!-- EDIT3 SECTION "Overview" [882-1348] -->
<h2 class="sectionedit4" id="adding_a_steer_behavior">Adding a steer behavior</h2>
<div class="level2">

<p>
Create instances from the steer behavior classes, They are located in the <code>com.jme3.ai.agents.behaviors.npc.steering</code> package. 
</p>

<p>
If we want to add more than one steer behavior, we need to create a container: </p><p></p><div class="notewarning">If you add more than one steer behavior to a <code>SimpleMainBehavior</code> it will cause problems in the rotation of the agents. 
</div>

<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Container </th><th class="col1"> Purpose </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> CompoundSteeringBehavior </td><td class="col1"> Contains and merges several <code>AbstractSteeringBehavior</code> instances </td>
	</tr>
	<tr class="row2">
		<td class="col0"> BalancedCompoundSteeringBehavior </td><td class="col1 leftalign"> Each force generated inside this container is reduced in relation with a proportion factor: “Partial Force” / “Total container force”  </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [1740-2036] -->
<p>
Once we know which container fits better for our agent, We create a new instance and add all the behaviors that we need:
</p>
<pre class="code java">SimpleMainBehaviour mainBehavior <span class="sy0">=</span> <span class="kw1">new</span> SimpleMainBehavior<span class="br0">(</span>myAgent<span class="br0">)</span><span class="sy0">;</span>
    CompoundSteeringBehavior steer <span class="sy0">=</span> <span class="kw1">new</span> CompoundSteeringBehavior<span class="br0">(</span>myAgent<span class="br0">)</span><span class="sy0">;</span>
    <span class="co1">//BalancedCompoundSteeringBehavior steer = new BalancedCompoundSteeringBehavior(myAgent);</span>
    steer.<span class="me1">addSteerBehavior</span><span class="br0">(</span>steerBehavior1<span class="br0">)</span><span class="sy0">;</span>
    steer.<span class="me1">addSteerBehavior</span><span class="br0">(</span>steerBehavior2<span class="br0">)</span><span class="sy0">;</span>
mainBehaviour.<span class="me1">addBehavior</span><span class="br0">(</span>steer<span class="br0">)</span><span class="sy0">;</span>
myAgent.<span class="me1">setMainBehavior</span><span class="br0">(</span>mainBehavior<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
</p><p></p><div class="noteclassic">Note that you can have nested containers, like is shown in the following example:
</div>

<pre class="code java">SimpleMainBehaviour mainBehavior <span class="sy0">=</span> <span class="kw1">new</span> SimpleMainBehavior<span class="br0">(</span>myAgent<span class="br0">)</span><span class="sy0">;</span>
    CompoundSteeringBehavior steer <span class="sy0">=</span> <span class="kw1">new</span> CompoundSteeringBehavior<span class="br0">(</span>myAgent<span class="br0">)</span><span class="sy0">;</span>
        BalancedCompoundSteeringBehavior nestedSteer <span class="sy0">=</span> <span class="kw1">new</span> BalancedCompoundSteeringBehavior<span class="br0">(</span>myAgent<span class="br0">)</span><span class="sy0">;</span>
        nestedSteer.<span class="me1">addSteerBehavior</span><span class="br0">(</span>steerBehavior1<span class="br0">)</span><span class="sy0">;</span>
    steer.<span class="me1">addSteerBehavior</span><span class="br0">(</span>nestedSteer<span class="br0">)</span><span class="sy0">;</span>
    steer.<span class="me1">addSteerBehavior</span><span class="br0">(</span>steerBehavior2<span class="br0">)</span><span class="sy0">;</span>
mainBehavior.<span class="me1">addBehavior</span><span class="br0">(</span>steer<span class="br0">)</span><span class="sy0">;</span>
myAgent.<span class="me1">setMainBehavior</span><span class="br0">(</span>mainBehavior<span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Adding a steer behavior" [1349-3151] -->
<h2 class="sectionedit6" id="prioritizing_behaviors">Prioritizing behaviors</h2>
<div class="level2">

<p>
You can assign priority layers: The steering controller first checks the higher layer to see if all the behaviors returns a value higher than <code>minLengthToInvalidSteer</code>, if so it uses that layer. Otherwise, it moves on to the second layer, and so on.
</p>

<p>
To assign priority layers add behaviors with the following function:
</p>
<pre class="code">  addSteerBehavior (AbstractSteeringBehavior behavior, int priority, float minLengthToInvalidSteer)</pre>

<p>
</p><p></p><div class="notetip">To optimize the process speed add the behaviors with the lowest priority first. 
</div>
<p></p><div class="noteclassic">The layer and the min length to consider the behavior invalid are 0 by default.
</div>


</div>
<!-- EDIT6 SECTION "Prioritizing behaviors" [3152-3802] -->
<h2 class="sectionedit7" id="setting_up_forces">Setting up forces</h2>
<div class="level2">

<p>
If a behavior extends from the <code>AbstractStrengthSteeringBehavior</code> class, you can manage how the produced forces will work.
</p>

<p>
Use <code>setupStrengthControl(float scalar)</code> to increase/decrease the steer force produced by a behavior or <code>setupStrengthControl(Plane plane)</code> If you want to work with 2D behaviors.
</p>

<p>
Example:
</p>
<pre class="code java">    Plane horizontalPlane <span class="sy0">=</span> <span class="kw1">new</span> Plane<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>,<span class="nu0">1</span>,<span class="nu0">0</span><span class="br0">)</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
 
    steerBehavior1.<span class="me1">setupStrengthControl</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Force reduced a 50%</span>
    steerBehavior2.<span class="me1">setupStrengthControl</span><span class="br0">(</span>horizontalPlane<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Force contained in the XZ plane</span>
    steerContainer.<span class="me1">setupStrengthControl</span><span class="br0">(</span>horizontalPlane, 2f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Contained in the XZ plane and increased a 100%</span></pre>

</div>
<!-- EDIT7 SECTION "Setting up forces" [3803-4512] -->
<h2 class="sectionedit8" id="implementing_your_own_steer_behavior">Implementing your own steer behavior</h2>
<div class="level2">

<p>
To benefit from all the features, you have to create a new class that extends from <code>AbstractStrengthSteeringBehavior</code>.
</p>

<p>
The responsible for the agent's acceleration is the vector returned in the <code>calculateRawSteering()</code> method:
</p>
<pre class="code java">    @Override
    <span class="kw1">protected</span> Vector3f calculateRawSteering<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        Vector3f steerForce <span class="sy0">=</span> Vector3f.<span class="me1">ZERO</span><span class="sy0">;</span>
 
        <span class="co1">//calculations</span>
 
        <span class="kw1">return</span> steerForce<span class="sy0">;</span>
    <span class="br0">}</span></pre>

<p>
In addition, you can change a brake factor which will reduce the resultant velocity for the agent:
</p>
<pre class="code java">    @Override
    <span class="kw1">protected</span> Vector3f calculateRawSteering<span class="br0">(</span><span class="br0">)</span><span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">setBrakingFactor</span><span class="br0">(</span>0.5f<span class="br0">)</span><span class="sy0">;</span> <span class="co1">//The agent's velocity will be reduced a 50%</span>
        <span class="kw1">return</span> Vector3f.<span class="me1">ZERO</span><span class="sy0">;</span>
    <span class="br0">}</span></pre>

<p>
</p><p></p><div class="notewarning">The braking force must be a float contained in the [0,1] interval
</div>
<p></p><div class="noteclassic">0 means the maximum braking force and 1 No braking force
</div>


</div>
<!-- EDIT8 SECTION "Implementing your own steer behavior" [4513-5455] -->
<h3 class="sectionedit9" id="strict_arguments">Strict arguments</h3>
<div class="level3">

<p>
To ensure that the behavior will work as you had planned it to work It's recommended to create your own <a href="http://docs.oracle.com/javase/7/docs/api/java/lang/IllegalArgumentException.html" class="urlextern" title="http://docs.oracle.com/javase/7/docs/api/java/lang/IllegalArgumentException.html" rel="nofollow">IllegalArgumentException</a> class. To do this, create your own container class extending from <code>com.jme3.ai.agents.behaviors.npc.steering.SteeringExceptions</code>; Each exception inside the container class extends from <code>SteeringBehaviorException</code>. Furthermore, It will help users to recognize better which is the origin of any problem.
</p>

<p>
Example:
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw1">class</span> CustomSteeringExceptions <span class="kw1">extends</span> SteeringExceptions  <span class="br0">{</span>
 
        <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw1">class</span> CustomRuntimeException <span class="kw1">extends</span> SteeringBehaviorException <span class="br0">{</span>
            <span class="kw1">public</span> CustomRuntimeException<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> msg<span class="br0">)</span> <span class="br0">{</span> <span class="kw1">super</span><span class="br0">(</span>msg<span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
        <span class="br0">}</span>
 
        <span class="co1">// ... other exceptions ...</span>
    <span class="br0">}</span></pre>
<pre class="code java">    <span class="kw1">public</span> SteerBehaviorConstructor<span class="br0">(</span>Agent agent, <span class="kw4">int</span> value, Spatial spatial<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">super</span><span class="br0">(</span>agent, spatial<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span><span class="br0">(</span>value <span class="sy0">&gt;</span> <span class="nu0">5</span><span class="br0">)</span> <span class="kw1">throw</span> <span class="kw1">new</span> CustomSteeringExceptions.<span class="me1">customRuntimeException</span> <span class="br0">(</span><span class="st0">"Value must be lower than 5"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">value</span> <span class="sy0">=</span> value<span class="sy0">;</span>
    <span class="br0">}</span></pre>

</div>
<!-- EDIT9 SECTION "Strict arguments" [5456-6600] -->
<h2 class="sectionedit10" id="useful_links">Useful links</h2>
<div class="level2">

<p>
java steer behaviors project: <a href="http://jmesteer.bdevel.org/" class="urlextern" title="http://jmesteer.bdevel.org/" rel="nofollow">jmesteer.bdevel.org</a>
</p>

</div>
<!-- EDIT10 SECTION "Useful links" [6601-] -->
