---
title: jMonkeyEngine SDK: Post-Processor Filters
---
<h1 class="sectionedit1" id="jmonkeyengine_sdkpost-processor_filters">jMonkeyEngine SDK: Post-Processor Filters</h1>
<div class="level1">

<p>
Filters are used for scene-wide effects such as glow, fog, blur. The SDK lets you create a file storing combinations of filters. You can preview the filter settings on a loaded scene in the SDK. You can load them into your application (add them to the viewPort) to activate your preconfigured set of several filters in one step.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Post-Processor Filters" [1-387] -->
<h2 class="sectionedit2" id="creating_filters">Creating Filters</h2>
<div class="level2">

<p>
<a href="/resources/sdk-filterexplorer.png" class="media" title="sdk:filterexplorer.png"><img src="/resources/sdk-filterexplorer.png" class="mediaright" alt="" /></a>
To create a new filter:
</p>
<ul>
<li class="level1"><div class="li"> In the Projects window, right-click Assets→Effects.</div>
</li>
<li class="level1"><div class="li"> Select File→New File…</div>
</li>
<li class="level1"><div class="li"> Select Filter→Empty FilterPostProcessor File in the New File Wizard. <br />
An empty filter file appears in the Assets→Effects directory.</div>
</li>
<li class="level1"><div class="li"> Double-click the created file. <br />
The file opens in the FilterExplorer window.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Creating Filters" [388-779] -->
<h2 class="sectionedit3" id="editing_filters">Editing Filters</h2>
<div class="level2">

<p>
To add filters or modify existing filters
</p>
<ol>
<li class="level1"><div class="li"> Double-click a j3f file to open it in the FilterExplorer window.</div>
</li>
<li class="level1"><div class="li"> Right-click the j3f file's root node to add a filter. <br />
Added filters are listed under the filter's root node.</div>
</li>
<li class="level1"><div class="li"> Open the Properties window and select a filter in the FilterExplorer. Configure filter options like intensity etc.</div>
</li>
</ol>

<p>
View the filter in the SceneComposer to see what you are doing:
</p>

</div>
<!-- EDIT3 SECTION "Editing Filters" [780-1220] -->
<h2 class="sectionedit4" id="viewing_filters">Viewing Filters</h2>
<div class="level2">

<p>
<a href="/resources/sdk-p3wuv.png" class="media" title="sdk:p3wuv.png"><img src="/resources/sdk-p3wuv.png" class="mediaright" alt="" /></a>
</p>

<p>
To see a loaded filter
</p>
<ol>
<li class="level1"><div class="li"> Open a model or scene in the SceneComposer. </div>
</li>
<li class="level1"><div class="li"> Double-click a j3f file to open it in the FilterExplorer window.</div>
</li>
<li class="level1"><div class="li"> Press the “show filter” button in the OpenGL window.</div>
</li>
</ol>

</div>
<!-- EDIT4 SECTION "Viewing Filters" [1221-1469] -->
<h2 class="sectionedit5" id="loading_filters_in_a_game">Loading filters in a game</h2>
<div class="level2">

<p>
To load a filter in a game (that is, to add it to your game's viewport), add the following lines to your game's simpleInit() method (or some other place):
</p>
<pre class="code java">FilterPostProcessor processor <span class="sy0">=</span> <span class="br0">(</span>FilterPostProcessor<span class="br0">)</span> assetManager.<span class="me1">loadAsset</span><span class="br0">(</span><span class="st0">"Filters/MyFilter.j3f"</span><span class="br0">)</span><span class="sy0">;</span>
viewPort.<span class="me1">addProcessor</span><span class="br0">(</span>processor<span class="br0">)</span><span class="sy0">;</span></pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/effect.html" class="wikilink1" title="tag:effect" rel="tag">effect</a>,
	<a href="/tag/file.html" class="wikilink1" title="tag:file" rel="tag">file</a>
</span></div>

</div>
<!-- EDIT5 SECTION "Loading filters in a game" [1470-] -->
