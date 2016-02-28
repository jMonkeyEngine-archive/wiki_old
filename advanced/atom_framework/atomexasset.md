---
title: AtomExAssets
---
<h2 class="sectionedit1" id="atomexassets">AtomExAssets</h2>
<div class="level2">

<p>
The future assets pipeline for JME3 games!
</p>

</div>
<!-- EDIT1 SECTION "AtomExAssets" [1-69] -->
<h3 class="sectionedit2" id="features">Features</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Real pipeline</div>
</li>
<li class="level1"><div class="li"> Multi sources &amp; Multi targets</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Features" [70-141] -->
<h3 class="sectionedit3" id="the_real_pipeline">The "real" pipeline</h3>
<div class="level3">

<p>
Pipeline is a common term in computing and also asset making. From sattelite view, pipeline is progresses between input and output.
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://storm.incubator.apache.org/images/topology.png"><img src="/resources/fetch.php" class="media" title="400px" alt="400px" /></a>
</p>

<p>
Here in game we talking about Assets aspect, mostly! 
</p>

<p>
In real world, converting-processing data and assets also require amount of times, efforts and cause headaches, almost comparable to making data and assets.
</p>

<p>
</p><p></p><div class="notetip">Some of the problems and solutions here can also be applied to other situation and usecaces
</div>


</div>

<h4 id="converting">Converting</h4>
<div class="level4">

<p>
Converting between things is a hard problem:
</p>
<ul>
<li class="level1"><div class="li"> Semantic: “things” are different “in contexts”. </div>
</li>
<li class="level1"><div class="li"> Incompatible: Converting almost one-direction only. Converter programs sometime not reliable and not support your data</div>
</li>
<li class="level1"><div class="li"> Hidden: Some format is unknown. Some require commercial and $$$</div>
</li>
<li class="level1"><div class="li"> Fault-tolerant: Currently almost asset pipeline is easy to fail and do not support recovery.</div>
</li>
</ul>

</div>

<h4 id="processing">Processing</h4>
<div class="level4">

<p>
Processing again is require a lot power:
</p>
<ul>
<li class="level1"><div class="li"> Time: Did you ever generate lightmap or PVS? - It may take a long long wait and easy to fail.</div>
</li>
<li class="level1"><div class="li"> Power and units: Did you ever render a movie? - It may require a render farm.</div>
</li>
<li class="level1"><div class="li"> Connections: Is there anything has to transfer between units? - It may delay the whole progress.</div>
</li>
</ul>

</div>

<h4 id="innovations">Innovations</h4>
<div class="level4">

<p>
AtomExAsset try to leverage pipelines from ideas inspired:
</p>

</div>

<h5 id="from_preon">From Preon</h5>
<div class="level5">

<p>
Bit stream language
</p>

</div>

<h5 id="from_dataturbine">From DataTurbine</h5>
<div class="level5">

<p>
Real-time data over network
</p>

</div>

<h5 id="from_distributed_computing">From Distributed computing</h5>
<div class="level5">

<p>
<a href="http://storm.incubator.apache.org/" class="urlextern" title="http://storm.incubator.apache.org/" rel="nofollow">http://storm.incubator.apache.org/</a> -
</p>

</div>

<h5 id="from_other_ccds_and_engines">From Other CCDs and Engines</h5>
<div class="level5">

<p>
3DSMax and Autodesk programs: Render farm integrated.
</p>

<p>
Blender: DNA structure
</p>

<p>
Unity: Metadata and SVN integrated
</p>

</div>
<!-- EDIT3 SECTION "The real pipeline" [142-1812] -->
<h3 class="sectionedit4" id="multi_sources_multi_targets">Multi sources &amp; Multi targets</h3>
<div class="level3">

</div>
<!-- EDIT4 SECTION "Multi sources & Multi targets" [1813-1853] -->
<h2 class="sectionedit5" id="first_look">First look</h2>
<div class="level2">

</div>
<!-- EDIT5 SECTION "First look" [1854-1877] -->
<h3 class="sectionedit6" id="slides">Slides</h3>
<div class="level3">

<p>
<iframe title="" src="https://docs.google.com/presentation/d/1gvh00FBoSYgvryw7Czbcjxrt5TmlK12P14QRdjKo4NA/embed?start=false&amp;loop=false&amp;delayms=3000" style="width:100%; height:600px"></iframe>
</p>

</div>
<!-- EDIT6 SECTION "Slides" [1878-2037] -->
<h3 class="sectionedit7" id="architecture">Architecture</h3>
<div class="level3">

</div>
<!-- EDIT7 SECTION "Architecture" [2038-2060] -->
<h3 class="sectionedit8" id="supported_sources_targets">Supported sources &amp; targets</h3>
<div class="level3">

</div>
<!-- EDIT8 SECTION "Supported sources & targets" [2061-2098] -->
<h3 class="sectionedit9" id="quickstart">Quickstart</h3>
<div class="level3">

</div>

<h4 id="unified_format_how_about_no">Unified Format? How about NO</h4>
<div class="level4">

<p>
“Unified Format” (use one format to encoded, decoded all kind of assets) is actually a nice idea but it's not real useful in real life situtations (or not even possible?)
</p>

<p>
AtomExAsset in other hand has unified pipeline via: Codecs, Flows, EntryPoints. Its “unified” data are actually a temporial data which has meta-data embeded.
</p>

</div>

<h4 id="temporial_scene_data">Temporial scene data</h4>
<div class="level4">

</div>

<h4 id="codecs">Codecs</h4>
<div class="level4">

<p>
Models
</p>

<p>
Textures
</p>

<p>
Animations
</p>

<p>
Basic usages
</p>

</div>

<h4 id="entrypoints">EntryPoints</h4>
<div class="level4">

<p>
EntryPoint is a higher abstract level of AssetKey where we accept the fact that Assets is not actually separated but reference in nested way, via each other and form a topology. We are talking about batch solutions which are very popular in real-life gamedev, and a way to integrate the flow of assets to the normal pipeline…
</p>

<p>
A lot of AAA games of big company relied on packed and streaming assets (online, from disks..). This assets usually get loaded by chunks instead of a whole at a time, make it possible to process as fast and smooth as possible.
</p>

<p>
You can see one simple example of the situation when:
</p>
<ul>
<li class="level1"><div class="li"> We reference to a Texture assetkey of a single Tile: assetManager.load(“tile1.png”);</div>
</li>
<li class="level1"><div class="li"> We later make a texture atlas of Tiles: tiles.png</div>
</li>
<li class="level1"><div class="li"> How can we reference to the original tile the old way, ignore the fact that it got batched!?</div>
</li>
</ul>

<p>
Texture atlas for ex and all kind of batching assets (pack, atlas, uber …) are techniques to optimize/boost  load time and real-time performance. Obfucasion, encoding add an extra layer technique that hide the real data from the back-end user; who shouldn't touch that data and modify them.
</p>

<p>
Also the always processing nature of the the asset in Atom pipeline require “dynamic entry point” which AssetKey's abstraction is not enough. EntryPoint and Flow are two new concept in the playground that you should take time to get familiar with.
</p>

</div>

<h4 id="flows">Flows</h4>
<div class="level4">

</div>

<h4 id="j3a">J3A</h4>
<div class="level4">

<p>
.j3a (see, it looks like j3o) stand for “Alternate Automatic Assets” is not actually format, but a meta-data or entry point in the asset system. One can use .j3a as entry point to load what ever he want with just the name, for ex:
</p>
<pre class="code"> assetManager.load("monkey.j3o")</pre>

<p>
is equal with:
</p>
<pre class="code"> assetManager.load("monkey.j3a")</pre>

<p>
but the later has extra effects:
</p>
<ul>
<li class="level1"><div class="li"> It put a update watcher over the entry point </div>
<ul>
<li class="level2"><div class="li"> the file in filesystem</div>
</li>
<li class="level2"><div class="li"> if you has config for that entry to “link” to another remote point (git, remote asset central), it actually manage the linkage for you</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> It manage the flows of the loading progress of that entry</div>
</li>
<li class="level1"><div class="li"> It manage the avaiablility, validation, necessarility of that entry if you are in a streaming scenario</div>
</li>
<li class="level1"><div class="li"> It let the assets pipeline fault tolerant.</div>
<ul>
<li class="level2"><div class="li"> So if the entry point is not available yet, you has a place holder util the file is available. The “holding back effect” also can be set if need</div>
</li>
<li class="level2"><div class="li"> If the request to the entry point actually timeouted, cached assets are used </div>
</li>
</ul>
</li>
</ul>

</div>

<h4 id="usage_along_with_the_official_asset_pipeline">Usage along with the "official" asset pipeline</h4>
<div class="level4">

<p>
You can see the Atom's asset pipeline as a replacement of the official one. In fact, you can also let them work together seamlessly because Atom pipeline just bypass JME3's assetManager in a few special case.
</p>

<p>
</p><p></p><div class="notewarning">Remember Atom's asset pipeline is better for “not-well formed” assets. In normal situation, you can use JME3's asset without a doubt!
</div>


<p>
Way1 - Atom over JME3: Put assetManager under an entry point, let call it “SEP” - StaticEntryPoint.
</p>
<pre class="code"> assetManager.load("SEP\")</pre>

<p>
Way2 - Atom with JME#:
</p>
<pre class="code"> assetManager.load(".j3a")</pre>

</div>
<!-- EDIT9 SECTION "Quickstart" [2099-5640] -->
<h2 class="sectionedit10" id="documentation">Documentation</h2>
<div class="level2">

</div>
<!-- EDIT10 SECTION "Documentation" [5641-5666] -->
<h3 class="sectionedit11" id="write_encoder_decoder">Write encoder &amp; decoder</h3>
<div class="level3">

<p>
Models
</p>

<p>
Textures
</p>

<p>
Animations
</p>

<p>
Basic usage
</p>

<p>
Preon reference:
</p>

<p>
<a href="http://preon.codehaus.org/preon-binding/apidocs/1.1-SNAPSHOT/nl/flotsam/preon/codec/package-summary.html" class="urlextern" title="http://preon.codehaus.org/preon-binding/apidocs/1.1-SNAPSHOT/nl/flotsam/preon/codec/package-summary.html" rel="nofollow">http://preon.codehaus.org/preon-binding/apidocs/1.1-SNAPSHOT/nl/flotsam/preon/codec/package-summary.html</a>
</p>

</div>
<!-- EDIT11 SECTION "Write encoder & decoder" [5667-5866] -->
<h3 class="sectionedit12" id="manage_dataflow_turbine">Manage dataflow &amp; turbine</h3>
<div class="level3">

</div>
<!-- EDIT12 SECTION "Manage dataflow & turbine" [5867-5902] -->
<h3 class="sectionedit13" id="server_nodes">Server &amp; Nodes</h3>
<div class="level3">

<p>
AtomExAssets ultimately use Building tools and Framework to help Java developer doing Game assets!
</p>

<p>
Beside of Defacto of the building tools: Ant &amp; Maven, the new rising star Gradle. AtomExAssets also use the powerful framework:
</p>

<p>
<a href="http://www.go.cd/" class="urlextern" title="http://www.go.cd/" rel="nofollow">http://www.go.cd/</a>
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://www.go.cd/images/home-image1.png"><img src="/resources/fetch.php" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT13 SECTION "Server & Nodes" [5903-] -->
