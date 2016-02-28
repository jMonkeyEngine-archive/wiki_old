---
title: Serializing
---
<h1 class="sectionedit1" id="serializing">Serializing</h1>
<div class="level1">

<p>
Whenever things have to be saved and loaded again (e.g. sending a map from the server to the clients), people talk about “serialization” - Basically, this means breaking a complex structure (like our block world) down to a simple row of data.
</p>

<p>
“Cubes” supports bit-serializing - You can export your block terrain at any time to a row of bits, most of the time handled as <strong>byte[]</strong> array. Later, the complete terrain can be reconstructed by those raw bytes.
</p>

</div>
<!-- EDIT1 SECTION "Serializing" [1-487] -->
<h2 class="sectionedit2" id="serializing1">Serializing</h2>
<div class="level2">

<p>
So, how do we convert a complete block world to bytes?
</p>
<pre class="code java"><span class="kw4">byte</span><span class="br0">[</span><span class="br0">]</span> serializedTerrainData <span class="sy0">=</span> CubesSerializer.<span class="me1">writeToBytes</span><span class="br0">(</span>blockTerrain<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Well… That was pretty easy, or? You don't have to worry, <em>how</em> your terrain is magically pressed in the data, the framework directly offers you the bytes, that you need to reconstruct the whole thing.
</p>

</div>
<!-- EDIT2 SECTION "Serializing" [488-866] -->
<h2 class="sectionedit3" id="data_transport">Data Transport</h2>
<div class="level2">

<p>
Actually, this part is on your own - There are many ways how to get data from one place to another and they all depend on your application. You'll have to find out how to get those bytes to the place where you want to rebuild the terrain - Make sure, you read the possible scenarios listed below. 
</p>

</div>
<!-- EDIT3 SECTION "Data Transport" [867-1193] -->
<h2 class="sectionedit4" id="unserializing">Unserializing</h2>
<div class="level2">

<p>
At this point, you have successfully received the bytes and want to recreate your awesome block world - This is how you do it:
</p>
<pre class="code java"><span class="co1">//The old blockTerrain will be completely replaced!</span>
<span class="co1">//(Even the chunks count will be adjusted)</span>
BlockTerrainControl blockTerrainClone <span class="sy0">=</span> <span class="kw1">new</span> BlockTerrainControl<span class="br0">(</span><span class="kw1">new</span> Vector3Int<span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
CubesSerializer.<span class="me1">readFromBytes</span><span class="br0">(</span>blockTerrain, serializedTerrainData<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
This screenshot shows a terrain and it's unserialized clone - Note, that the blocks have to be registered in the <strong>same order</strong> on both sides in order to reproduce the same terrain!
</p>

<p>
<a href="/resources/fetch.php" class="media" title="http://destroflyer.mania-community.de/other/imagehost/cubes/test_serialize.png"><img src="/resources/fetch.php" class="media" alt="" width="800" /></a>
</p>

</div>
<!-- EDIT4 SECTION "Unserializing" [1194-1892] -->
<h2 class="sectionedit5" id="possible_scenarios">Possible scenarios</h2>
<div class="level2">

<p>
The most typical examples for serializing are the following:
</p>
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Application </th><th class="col1"> Data Transport </th><th class="col2 leftalign"> Resources  </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Networking </td><td class="col1"> The bytes are sent in a message over the network - The client receives them and can rebuild the block world. </td><td class="col2"> <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">Spidermonkey</a> </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Files </td><td class="col1"> The bytes are saved in a file, which can be loaded again next time. </td><td class="col2"> <a href="http://docs.oracle.com/javase/1.4.2/docs/api/java/io/File.html" class="urlextern" title="http://docs.oracle.com/javase/1.4.2/docs/api/java/io/File.html" rel="nofollow">java.io.File</a> </td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [1985-2362] -->
</div>
<!-- EDIT5 SECTION "Possible scenarios" [1893-2364] -->
<h2 class="sectionedit7" id="advancedbitserializing">Advanced: BitSerializing</h2>
<div class="level2">

<p>
<em>This part of the article will handle a more advanced way of how to access the bit serializer of the framework. As long as it's not written yet, please take a look at the classes <code>cubes.network.BitInputStream</code>, <code>cubes.network.BitOutputStream</code> and the interface <code>cubes.network.BitSerializable</code> that's implemented by the <code>cubes.BlockTerrainControl</code> class.</em>
</p>

</div>
<!-- EDIT7 SECTION "Advanced: BitSerializing" [2365-] -->
