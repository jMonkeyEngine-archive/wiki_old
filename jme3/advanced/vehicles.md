---
title: Controlling a Physical Vehicle
---
<h1 class="sectionedit1" id="controlling_a_physical_vehicle">Controlling a Physical Vehicle</h1>
<div class="level1">

<p>
For physical vehicles, jME's uses the jBullet ray-cast vehicle. In this vehicle implementation, the physical chassis 'floats' along on four non-physical vertical rays. 
</p>

<p>
Internally, each wheel casts a ray down, and using the ray's intersection point, jBullet calculates the suspension length, and the suspension force. The suspension force is applied to the chassis, keeping it from hitting the ground. The friction force is calculated for each wheel where the ray intersects with the ground. Friction is applied as a sideways and forwards force. <sup><a href="#fn__1" id="fnt__1" class="fn_top">1)</a></sup>
</p>

<p>
This article shows how you use this vehicle implementation in a jME3 application.
</p>

<p>
<a href="/resources/jme3-advanced-physics-vehicle.png" class="media" title="jme3:advanced:physics-vehicle.png"><img src="/resources/jme3-advanced-physics-vehicle.png" class="mediacenter" alt="" /></a>
</p>

</div>
<!-- EDIT1 SECTION "Controlling a Physical Vehicle" [1-806] -->
<h2 class="sectionedit2" id="sample_code">Sample Code</h2>
<div class="level2">

<p>
Full code samples are here:
</p>
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsCar.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsCar.java" rel="nofollow">TestPhysicsCar.java</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestFancyCar.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestFancyCar.java" rel="nofollow">TestFancyCar.java</a></div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Sample Code" [807-1159] -->
<h2 class="sectionedit3" id="overview_of_this_physics_application">Overview of this Physics Application</h2>
<div class="level2">

<p>
The goal is to create a physical vehicle with wheels that can be steered and that interacts (collides with) with the floor and obstacles.
</p>
<ol>
<li class="level1"><div class="li"> Create a SimpleApplication with a <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">BulletAppState</a> </div>
<ul>
<li class="level2"><div class="li"> This gives us a PhysicsSpace for PhysicsNodes</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Create a VehicleControl + CompoundCollisionShape for the physical vehicle behaviour</div>
<ol>
<li class="level2"><div class="li"> Set physical properties of the vehicle, such as suspension.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Create a VehicleNode for the car model</div>
<ol>
<li class="level2"><div class="li"> Create a box plus 4 cylinders as wheels (using <code>vehicle.addWheel()</code>).</div>
</li>
<li class="level2"><div class="li"> Add the VehicleControl behaviour to the VehicleNode geometry.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Create a RigidBodyControl and CollisionShape for the floor</div>
</li>
<li class="level1"><div class="li"> Map key triggers and add input listeners</div>
<ul>
<li class="level2"><div class="li"> Navigational commands Left, Right, Foward, Brake.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Define the steering actions to be triggered by the key events.</div>
<ul>
<li class="level2"><div class="li"> <code>vehicle.steer()</code></div>
</li>
<li class="level2"><div class="li"> <code>vehicle.accelerate()</code></div>
</li>
<li class="level2"><div class="li"> <code>vehicle.brake()</code></div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Overview of this Physics Application" [1160-2139] -->
<h2 class="sectionedit4" id="creating_the_vehicle_chassis">Creating the Vehicle Chassis</h2>
<div class="level2">

<p>
The vehicle that we create here in the <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsCar.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsCar.java" rel="nofollow">TestPhysicsCar.java</a> example is just a “box on wheels”, a basic vehicle shape that you can replace with a fancy car model, as demonstrated in <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestFancyCar.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestFancyCar.java" rel="nofollow">TestFancyCar.java</a>.
</p>

<p>
Every physical object must have a collision shape, that we prepare first. For the vehicle, we choose a compound collision shape that is made up of a box-shaped body of the right size for the vehicle. We will add the wheels later. 
</p>
<pre class="code java">CompoundCollisionShape compoundShape <span class="sy0">=</span> <span class="kw1">new</span> CompoundCollisionShape<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
BoxCollisionShape box <span class="sy0">=</span> <span class="kw1">new</span> BoxCollisionShape<span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>1.2f, 0.5f, 2.4f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Best Practice:</strong> We attach the BoxCollisionShape (the vehicle body) to the CompoundCollisionShape at a Vector of (0,1,0): This shifts the effective center of mass of the BoxCollisionShape downwards to 0,-1,0 and makes a moving vehicle more stable! 
</p>
<pre class="code java">compoundShape.<span class="me1">addChildShape</span><span class="br0">(</span>box, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Any kind of geometry can make up the visible part of the vehicle, here we use a wireframe box. We create a node that we use to group the geometry. 
</p>
<pre class="code java">Node vehicleNode<span class="sy0">=</span><span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"vehicleNode"</span><span class="br0">)</span><span class="sy0">;</span>
vehicle <span class="sy0">=</span> <span class="kw1">new</span> VehicleControl<span class="br0">(</span>compoundShape, <span class="nu0">400</span><span class="br0">)</span><span class="sy0">;</span>
vehicleNode.<span class="me1">addControl</span><span class="br0">(</span>vehicle<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
We initialize the Vehicle Control with the compound shape, and set its mass to a heavy value, 400f. The Vehicle Control represents the car's physical behaviour.
</p>
<pre class="code java">vehicle <span class="sy0">=</span> <span class="kw1">new</span> VehicleControl<span class="br0">(</span>compoundShape, <span class="nu0">400</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Finally we add the behaviour (VehicleControl) to the visible Geometry (node).
</p>
<pre class="code java">vehicleNode.<span class="me1">addControl</span><span class="br0">(</span>vehicle<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
We configure the physical properties of the vehicle's suspension: Compresion, Damping, Stiffness, and MaxSuspenionForce. Picking workable values for the wheel suspension can be tricky – for background info have a look at these <a href="https://docs.google.com/Doc?docid=0AXVUZ5xw6XpKZGNuZG56a3FfMzU0Z2NyZnF4Zmo&amp;hl=en" class="urlextern" title="https://docs.google.com/Doc?docid=0AXVUZ5xw6XpKZGNuZG56a3FfMzU0Z2NyZnF4Zmo&amp;hl=en" rel="nofollow">Suspension Settings Tips</a>. For now, let's work with the following values:
</p>
<pre class="code java"><span class="kw4">float</span> stiffness <span class="sy0">=</span> 60.0f<span class="sy0">;</span><span class="co1">//200=f1 car</span>
<span class="kw4">float</span> compValue <span class="sy0">=</span> .3f<span class="sy0">;</span> <span class="co1">//(should be lower than damp)</span>
<span class="kw4">float</span> dampValue <span class="sy0">=</span> .4f<span class="sy0">;</span>
vehicle.<span class="me1">setSuspensionCompression</span><span class="br0">(</span>compValue <span class="sy0">*</span> 2.0f <span class="sy0">*</span> FastMath.<span class="me1">sqrt</span><span class="br0">(</span>stiffness<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
vehicle.<span class="me1">setSuspensionDamping</span><span class="br0">(</span>dampValue <span class="sy0">*</span> 2.0f <span class="sy0">*</span> FastMath.<span class="me1">sqrt</span><span class="br0">(</span>stiffness<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
vehicle.<span class="me1">setSuspensionStiffness</span><span class="br0">(</span>stiffness<span class="br0">)</span><span class="sy0">;</span>
vehicle.<span class="me1">setMaxSuspensionForce</span><span class="br0">(</span>10000.0f<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
We now have a node <code>vehicleNode</code> with a visible “car” geometry, which acts like a vehicle. One thing that's missing are wheels.
</p>

</div>
<!-- EDIT4 SECTION "Creating the Vehicle Chassis" [2140-4905] -->
<h2 class="sectionedit5" id="adding_the_wheels">Adding the Wheels</h2>
<div class="level2">

<p>
We create four wheel Geometries and add them to the vehicle. Our wheel geometries are simple, non-physical discs (flat Cylinders), they are just visual decorations. Note that the physical wheel behaviour (the com.jme3.bullet.objects.VehicleWheel objects) is created internally by the <code>vehicle.addWheel()</code> method. 
</p>

<p>
The <code>addWheel()</code> method sets following properties:
</p>
<ul>
<li class="level1"><div class="li"> Vector3f connectionPoint – Coordinate where the suspension connects to the chassis (internally, this is where the Ray is casted downwards).</div>
</li>
<li class="level1"><div class="li"> Vector3f direction – Wheel direction is typically a (0,-1,0) vector.</div>
</li>
<li class="level1"><div class="li"> Vector3f axle – Axle direction is typically a (-1,0,0) vector.</div>
</li>
<li class="level1"><div class="li"> float suspensionRestLength – Suspension rest length in world units</div>
</li>
<li class="level1"><div class="li"> float wheelRadius – Wheel radius in world units</div>
</li>
<li class="level1"><div class="li"> boolean isFrontWheel – Whether this wheel is one of the steering wheels. <br />
Front wheels are the ones that rotate visibly when the vehicle turns.</div>
</li>
</ul>

<p>
We initialize a few variables that we will reuse when we add the four wheels. yOff, etc, are the particular wheel offsets for our small vehicle model.
</p>
<pre class="code java">Vector3f wheelDirection <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span><span class="nu0">1</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
Vector3f wheelAxle <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span><span class="nu0">1</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw4">float</span> radius <span class="sy0">=</span> 0.5f<span class="sy0">;</span>
<span class="kw4">float</span> restLength <span class="sy0">=</span> 0.3f<span class="sy0">;</span>
<span class="kw4">float</span> yOff <span class="sy0">=</span> 0.5f<span class="sy0">;</span>
<span class="kw4">float</span> xOff <span class="sy0">=</span> 1f<span class="sy0">;</span>
<span class="kw4">float</span> zOff <span class="sy0">=</span> 2f<span class="sy0">;</span></pre>

<p>
We create a Cylinder mesh shape that we use to create the four visible wheel geometries.
</p>
<pre class="code java">Cylinder wheelMesh <span class="sy0">=</span> <span class="kw1">new</span> Cylinder<span class="br0">(</span><span class="nu0">16</span>, <span class="nu0">16</span>, radius, radius <span class="sy0">*</span> 0.6f, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
For each wheel, we create a Node and a Geometry. We attach the Cylinder Geometry to the Node. We rotate the wheel by 90° around the Y axis. We set a material to make it visible. Finally we add the wheel (plus its properties) to the vehicle.
</p>
<pre class="code java">Node node1 <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"wheel 1 node"</span><span class="br0">)</span><span class="sy0">;</span>
Geometry wheels1 <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"wheel 1"</span>, wheelMesh<span class="br0">)</span><span class="sy0">;</span>
node1.<span class="me1">attachChild</span><span class="br0">(</span>wheels1<span class="br0">)</span><span class="sy0">;</span>
wheels1.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, FastMath.<span class="me1">HALF_PI</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
wheels1.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
 
vehicle.<span class="me1">addWheel</span><span class="br0">(</span>node1, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>xOff, yOff, zOff<span class="br0">)</span>,
    wheelDirection, wheelAxle, restLength, radius, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
The three next wheels are created in the same fashion, only the offsets are different. Remember to set the Boolean parameter correctly to indicate whether it's a front wheel.
</p>
<pre class="code java">...
<span class="me1">vehicle</span>.<span class="me1">addWheel</span><span class="br0">(</span>node2, <span class="kw1">new</span> Vector3f<span class="br0">(</span>xOff, yOff, zOff<span class="br0">)</span>,
  wheelDirection, wheelAxle, restLength, radius, <span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">vehicle</span>.<span class="me1">addWheel</span><span class="br0">(</span>node3, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>xOff, yOff, <span class="sy0">-</span>zOff<span class="br0">)</span>,
  wheelDirection, wheelAxle, restLength, radius, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
...
<span class="me1">vehicle</span>.<span class="me1">addWheel</span><span class="br0">(</span>node4, <span class="kw1">new</span> Vector3f<span class="br0">(</span>xOff, yOff, <span class="sy0">-</span>zOff<span class="br0">)</span>,
  wheelDirection, wheelAxle, restLength, radius, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Attach the wheel Nodes to the vehicle Node to group them, so they move together.
</p>
<pre class="code java">vehicleNode.<span class="me1">attachChild</span><span class="br0">(</span>node1<span class="br0">)</span><span class="sy0">;</span>
vehicleNode.<span class="me1">attachChild</span><span class="br0">(</span>node2<span class="br0">)</span><span class="sy0">;</span>
vehicleNode.<span class="me1">attachChild</span><span class="br0">(</span>node3<span class="br0">)</span><span class="sy0">;</span>
vehicleNode.<span class="me1">attachChild</span><span class="br0">(</span>node4<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
As always, attach the vehicle Node to the rootNode to make it visible, and add the Vehicle Control to the PhysicsSpace to make the car physical.
</p>
<pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>vehicleNode<span class="br0">)</span><span class="sy0">;</span>
getPhysicsSpace<span class="br0">(</span><span class="br0">)</span>.<span class="me1">add</span><span class="br0">(</span>vehicle<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Not shown here is that we also created a Material <code>mat</code>.
</p>

</div>
<!-- EDIT5 SECTION "Adding the Wheels" [4906-8061] -->
<h2 class="sectionedit6" id="steering_the_vehicle">Steering the Vehicle</h2>
<div class="level2">

<p>
Not shown here is the standard way how we map the input keys to actions (see full code sample). Also refer to <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">Input Handling</a>).
</p>

<p>
In the ActionListener, we implement the actions that control the vehicle's direction and speed. For the four directions (accelerate=up, brake=down, left, right), we specify how we want the vehicle to move. 
</p>
<ul>
<li class="level1"><div class="li"> The braking action is pretty straightforward: <br />
<code>vehicle.brake(brakeForce)</code></div>
</li>
<li class="level1"><div class="li"> For left and right turns, we add a constant to <code>steeringValue</code> when the key is pressed, and subtract it when the key is released. <br />
<code>vehicle.steer(steeringValue);</code></div>
</li>
<li class="level1"><div class="li"> For acceleration we add a constant to <code>accelerationValue</code> when the key is pressed, and substract it when the key is released. <br />
<code>vehicle.accelerate(accelerationValue);</code></div>
</li>
<li class="level1"><div class="li"> Because we can and it's fun, we also add a turbo booster that makes the vehicle jump when you press the assigned key (spacebar). <br />
<code>vehicle.applyImpulse(jumpForce, Vector3f.ZERO);</code></div>
</li>
</ul>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> onAction<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> binding, <span class="kw4">boolean</span> value, <span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
  <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Lefts"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span> steeringValue <span class="sy0">+=</span> .5f<span class="sy0">;</span> <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span> steeringValue <span class="sy0">+=</span> <span class="sy0">-</span>.5f<span class="sy0">;</span> <span class="br0">}</span>
      vehicle.<span class="me1">steer</span><span class="br0">(</span>steeringValue<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Rights"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span> steeringValue <span class="sy0">+=</span> <span class="sy0">-</span>.5f<span class="sy0">;</span> <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span> steeringValue <span class="sy0">+=</span> .5f<span class="sy0">;</span> <span class="br0">}</span>
      vehicle.<span class="me1">steer</span><span class="br0">(</span>steeringValue<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Ups"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span>
        accelerationValue <span class="sy0">+=</span> accelerationForce<span class="sy0">;</span>
      <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
        accelerationValue <span class="sy0">-=</span> accelerationForce<span class="sy0">;</span>
      <span class="br0">}</span>
      vehicle.<span class="me1">accelerate</span><span class="br0">(</span>accelerationValue<span class="br0">)</span><span class="sy0">;</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Downs"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span> vehicle.<span class="me1">brake</span><span class="br0">(</span>brakeForce<span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span> vehicle.<span class="me1">brake</span><span class="br0">(</span>0f<span class="br0">)</span><span class="sy0">;</span> <span class="br0">}</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Space"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span>
        vehicle.<span class="me1">applyImpulse</span><span class="br0">(</span>jumpForce, Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span>
  <span class="br0">}</span> <span class="kw1">else</span> <span class="kw1">if</span> <span class="br0">(</span>binding.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Reset"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span>value<span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Reset"</span><span class="br0">)</span><span class="sy0">;</span>
        vehicle.<span class="me1">setPhysicsLocation</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="sy0">;</span>
        vehicle.<span class="me1">setPhysicsRotation</span><span class="br0">(</span><span class="kw1">new</span> Matrix3f<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        vehicle.<span class="me1">setLinearVelocity</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="sy0">;</span>
        vehicle.<span class="me1">setAngularVelocity</span><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span><span class="br0">)</span><span class="sy0">;</span>
        vehicle.<span class="me1">resetSuspension</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
    <span class="br0">}</span>
  <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
For your reference, this is how we initialized the constants for this example:
</p>
<pre class="code java"><span class="kw1">private</span> <span class="kw1">final</span> <span class="kw4">float</span> accelerationForce <span class="sy0">=</span> 1000.0f<span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw1">final</span> <span class="kw4">float</span> brakeForce <span class="sy0">=</span> 100.0f<span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">float</span> steeringValue <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
<span class="kw1">private</span> <span class="kw4">float</span> accelerationValue <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
<span class="kw1">private</span> Vector3f jumpForce <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">3000</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Remember, the standard input listener code that maps the actions to keys can be found in the code samples.
</p>

</div>
<!-- EDIT6 SECTION "Steering the Vehicle" [8062-10699] -->
<h2 class="sectionedit7" id="detecting_collisions">Detecting Collisions</h2>
<div class="level2">

<p>
Read the <a href="/jme3/advanced/physics.html" class="wikilink1" title="jme3:advanced:physics">Responding to a PhysicsCollisionEvent</a> chapter in the general physics documentation on how to detect collisions. You would do this if you want to react to collisions with custom events, such as adding points or substracting health.
</p>

</div>
<!-- EDIT7 SECTION "Detecting Collisions" [10700-11039] -->
<h2 class="sectionedit8" id="best_practices">Best Practices</h2>
<div class="level2">

<p>
This example shows a very simple but functional vehicle. For a game you would implement steering behaviour and acceleration with values that are typical for the type of vehicle that you want to simulate. Instead of a box, you load a chassis model. You can consider using an <a href="/jme3/advanced/input_handling.html" class="wikilink1" title="jme3:advanced:input_handling">AnalogListener</a> to respond to key events in a more sophisticated way.
</p>

<p>
For a more advanced example, look at <a href="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestFancyCar.java" class="urlextern" title="https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestFancyCar.java" rel="nofollow">TestFancyCar.java</a>.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>,
	<a href="/tag/vehicle.html" class="wikilink1" title="tag:vehicle" rel="tag">vehicle</a>,
	<a href="/tag/collision.html" class="wikilink1" title="tag:collision" rel="tag">collision</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Best Practices" [11040-] --><div class="footnotes">
<div class="fn"><sup><a href="#fnt__1" id="fn__1" class="fn_bot">1)</a></sup> 
 <a href="https://docs.google.com/Doc?docid=0AXVUZ5xw6XpKZGNuZG56a3FfMzU0Z2NyZnF4Zmo&amp;hl=en" class="urlextern" title="https://docs.google.com/Doc?docid=0AXVUZ5xw6XpKZGNuZG56a3FfMzU0Z2NyZnF4Zmo&amp;hl=en" rel="nofollow">https://docs.google.com/Doc?docid=0AXVUZ5xw6XpKZGNuZG56a3FfMzU0Z2NyZnF4Zmo&amp;hl=en</a> </div>
</div>
