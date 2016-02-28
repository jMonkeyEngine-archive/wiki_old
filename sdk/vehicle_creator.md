---
title: jMonkeyEngine SDK: Vehicle Creator
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkvehicle_creator">jMonkeyEngine SDK: Vehicle Creator</h1>
<div class="level1">

<p>
Best results when car is facing in z direction (towards you).
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Vehicle Creator" [1-113] -->
<h2 class="sectionedit2" id="usage">Usage</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Select a j3o that contains a vehicle model and press the vehicle button (or right-click → edit vehicle)</div>
</li>
<li class="level1"><div class="li"> The VehicleCreator automatically adds a PhysicsVehicleControl to the rootNode of the model if there is none</div>
</li>
<li class="level1"><div class="li"> Select the Geometry or Node that contains the chassis in the SceneExplorer and press “create hull shape from selected”</div>
</li>
<li class="level1"><div class="li"> Select a Geometry that contains a wheel and press “make selected spatial wheel”, select the “front wheel” checkboxes for front wheels</div>
</li>
<li class="level1"><div class="li"> Do so for all wheels</div>
</li>
</ol>

<p>
New wheels will get the current suspension settings, you can edit single wheels via the SceneExplorer (update VehicleControl if wheels dont show up) or apply settings created with the settings generator to wheel groups.
</p>

<p>
Press the “test vehicle” button to drive the vehicle, use WASD to control, Enter to reset.
</p>

</div>
<!-- EDIT2 SECTION "Usage" [114-950] -->
<h2 class="sectionedit3" id="known_issues">Known Issues</h2>
<div class="level2">

<p>
Don't save while testing the vehicle, you will save the location and acceleration info in the j3o.
</p>

</div>
<!-- EDIT3 SECTION "Known Issues" [951-1075] -->
<h2 class="sectionedit4" id="code_sample">Code Sample</h2>
<div class="level2">

<p>
Code Example to load vehicle:
</p>
<pre class="code java"><span class="co1">//load vehicle and access VehicleControl</span>
Spatial car<span class="sy0">=</span>assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/MyCar.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
VehicleControl control<span class="sy0">=</span>car.<span class="me1">getControl</span><span class="br0">(</span>VehicleControl.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>car<span class="br0">)</span><span class="sy0">;</span>
physicsSpace.<span class="me1">add</span><span class="br0">(</span>control<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">//then use the control to control the vehicle:</span>
control.<span class="me1">setPhysicsLocation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">10</span>,<span class="nu0">2</span>,<span class="nu0">10</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
control.<span class="me1">accelerate</span><span class="br0">(</span><span class="nu0">100</span><span class="br0">)</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>,
	<a href="/tag/asset.html" class="wikilink1" title="tag:asset" rel="tag">asset</a>,
	<a href="/tag/editor.html" class="wikilink1" title="tag:editor" rel="tag">editor</a>,
	<a href="/tag/physics.html" class="wikilink1" title="tag:physics" rel="tag">physics</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Code Sample" [1076-] -->
