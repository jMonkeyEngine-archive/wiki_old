---
title: Recast Navigation for JME
---
<h1 class="sectionedit1" id="recast_navigation_for_jme">Recast Navigation for JME</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Recast Navigation for JME" [1-41] -->
<h2 class="sectionedit2" id="what_is_recast_navigation">What is Recast Navigation</h2>
<div class="level2">

<p>
Recast Navigation is C++ library for path-finding in 3D, continuous space. Recast has two big modules:
</p>
<ol>
<li class="level1"><div class="li"> Recast</div>
</li>
<li class="level1"><div class="li"> Detour</div>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "What is Recast Navigation" [42-205] -->
<h3 class="sectionedit3" id="recast">Recast</h3>
<div class="level3">

<p>
Recast is state of the art navigation mesh construction tool set for games.
</p>
<ul>
<li class="level1"><div class="li"> It is automatic, which means that you can throw any level geometry at it and you will get robust mesh out</div>
</li>
<li class="level1"><div class="li"> It is fast which means swift turnaround times for level designers</div>
</li>
<li class="level1"><div class="li"> It is open source so it comes with full source and you can customize it to your heart's content.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Recast" [206-582] -->
<h3 class="sectionedit4" id="detour">Detour</h3>
<div class="level3">

<p>
Recast is accompanied with Detour, path-finding and spatial reasoning toolkit. You can use any navigation mesh with Detour, but of course the data generated with Recast fits perfectly.
</p>

<p>
Detour offers simple static navigation mesh which is suitable for many simple cases, as well as tiled navigation mesh which allows you to plug in and out pieces of the mesh. The tiled mesh allows you to create systems where you stream new navigation data in and out as the player progresses the level, or you may regenerate tiles as the world changes.
</p>

</div>
<!-- EDIT4 SECTION "Detour" [583-1139] -->
<h2 class="sectionedit5" id="jnavigation">jNavigation</h2>
<div class="level2">

<p>
jNavigation is port Java library for <a href="https://github.com/memononen/recastnavigation" class="urlextern" title="https://github.com/memononen/recastnavigation" rel="nofollow">Recast navigation</a>. jNavigation is the project in progress, and currently it enables building <a href="http://en.wikipedia.org/wiki/Navigation_mesh" class="urlextern" title="http://en.wikipedia.org/wiki/Navigation_mesh" rel="nofollow">Navigation meshes</a> and path-finding for one agent (bot).
</p>

</div>
<!-- EDIT5 SECTION "jNavigation" [1140-1451] -->
<h2 class="sectionedit6" id="example">Example</h2>
<div class="level2">

<p>
In next code is described how the user should build navigation mesh, and query for it.
</p>
<pre class="code java"><span class="co1">// Step 1. Initialize build config.</span>
Config config <span class="sy0">=</span> <span class="kw1">new</span> Config<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
Mesh mesh <span class="sy0">=</span> <span class="br0">(</span><span class="br0">(</span>Geometry<span class="br0">)</span> scene.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"terrain"</span><span class="br0">)</span><span class="br0">)</span>.<span class="me1">getMesh</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
Vector3f minBounds <span class="sy0">=</span> RecastBuilder.<span class="me1">calculateMinBounds</span><span class="br0">(</span>mesh<span class="br0">)</span><span class="sy0">;</span>
Vector3f maxBounds <span class="sy0">=</span> RecastBuilder.<span class="me1">calculateMaxBounds</span><span class="br0">(</span>mesh<span class="br0">)</span><span class="sy0">;</span>
 
config.<span class="me1">setMaxBounds</span><span class="br0">(</span>maxBounds<span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setMinBounds</span><span class="br0">(</span>minBounds<span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setCellSize</span><span class="br0">(</span>0.3f<span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setCellHeight</span><span class="br0">(</span>0.2f<span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setWalkableSlopeAngle</span><span class="br0">(</span><span class="nu0">45</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setWalkableClimb</span><span class="br0">(</span><span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setWalkableHeight</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setWalkableRadius</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setMinRegionArea</span><span class="br0">(</span><span class="nu0">8</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setMergeRegionArea</span><span class="br0">(</span><span class="nu0">20</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setBorderSize</span><span class="br0">(</span><span class="nu0">20</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setMaxEdgeLength</span><span class="br0">(</span><span class="nu0">12</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setMaxVerticesPerPoly</span><span class="br0">(</span><span class="nu0">6</span><span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setDetailSampleMaxError</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
config.<span class="me1">setDetailSampleDistance</span><span class="br0">(</span><span class="nu0">6</span><span class="br0">)</span><span class="sy0">;</span>
 
RecastBuilder.<span class="me1">calculateGridWidth</span><span class="br0">(</span>config<span class="br0">)</span><span class="sy0">;</span>
RecastBuilder.<span class="me1">calculatesGridHeight</span><span class="br0">(</span>config<span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Step 2. Rasterize input polygon soup.</span>
 
<span class="co1">//context is needed for logging that is not yet fully supported in native library.</span>
<span class="co1">//It must NOT be null.</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+context"><span class="kw3">Context</span></a> context <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+context"><span class="kw3">Context</span></a><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="co1">// Allocate voxel heightfield where we rasterize our input data to.</span>
Heightfield heightfield <span class="sy0">=</span> <span class="kw1">new</span> Heightfield<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">createHeightfield</span><span class="br0">(</span>context, heightfield, config<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not create solid heightfield"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="co1">// Allocate array that can hold triangle area types. </span>
 
<span class="co1">// In Recast terminology, triangles are what indices in jME is. I left this,</span>
 
<span class="co1">// Find triangles which are walkable based on their slope and rasterize them.</span>
<span class="kw4">char</span><span class="br0">[</span><span class="br0">]</span> areas <span class="sy0">=</span> RecastBuilder.<span class="me1">markWalkableTriangles</span><span class="br0">(</span>context, config.<span class="me1">getWalkableSlopeAngle</span><span class="br0">(</span><span class="br0">)</span>, mesh<span class="br0">)</span><span class="sy0">;</span>
RecastBuilder.<span class="me1">rasterizeTriangles</span><span class="br0">(</span>context, mesh, areas, heightfield, <span class="nu0">20</span><span class="br0">)</span><span class="sy0">;</span>
 
 
<span class="co1">// Step 3. Filter walkables surfaces.</span>
<span class="co1">// Once all geometry is rasterized, we do initial pass of filtering to</span>
<span class="co1">// remove unwanted overhangs caused by the conservative rasterization</span>
<span class="co1">// as well as filter spans where the character cannot possibly stand.</span>
RecastBuilder.<span class="me1">filterLowHangingWalkableObstacles</span><span class="br0">(</span>context, config.<span class="me1">getWalkableClimb</span><span class="br0">(</span><span class="br0">)</span>, heightfield<span class="br0">)</span><span class="sy0">;</span>
RecastBuilder.<span class="me1">filterLedgeSpans</span><span class="br0">(</span>context, config, heightfield<span class="br0">)</span><span class="sy0">;</span>
RecastBuilder.<span class="me1">filterWalkableLowHeightSpans</span><span class="br0">(</span>context, config.<span class="me1">getWalkableHeight</span><span class="br0">(</span><span class="br0">)</span>, heightfield<span class="br0">)</span><span class="sy0">;</span>
 
 
<span class="co1">// Step 4. Partition walkable surface to simple regions.</span>
<span class="co1">// Compact the heightfield so that it is faster to handle from now on.</span>
<span class="co1">// This will result more cache coherent data as well as the neighbours</span>
<span class="co1">// between walkable cells will be calculated.</span>
CompactHeightfield compactHeightfield <span class="sy0">=</span> <span class="kw1">new</span> CompactHeightfield<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">buildCompactHeightfield</span><span class="br0">(</span>context, config, heightfield, compactHeightfield<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not build compact data"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">erodeWalkableArea</span><span class="br0">(</span>context, config.<span class="me1">getWalkableRadius</span><span class="br0">(</span><span class="br0">)</span>, compactHeightfield<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not erode"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="co1">// Partition the heightfield so that we can use simple algorithm later to triangulate the walkable areas.</span>
<span class="co1">// There are 3 martitioning methods, each with some pros and cons:</span>
<span class="co1">// 1) Watershed partitioning</span>
<span class="co1">//   - the classic Recast partitioning</span>
<span class="co1">//   - creates the nicest tessellation</span>
<span class="co1">//   - usually slowest</span>
<span class="co1">//   - partitions the heightfield into nice regions without holes or overlaps</span>
<span class="co1">//   - the are some corner cases where this method creates produces holes and overlaps</span>
<span class="co1">//      - holes may appear when a small obstacles is close to large open area (triangulation can handle this)</span>
<span class="co1">//      - overlaps may occur if you have narrow spiral corridors (i.e stairs), this make triangulation to fail</span>
<span class="co1">//   * generally the best choice if you precompute the nacmesh, use this if you have large open areas</span>
<span class="co1">// 2) Monotone partioning</span>
<span class="co1">//   - fastest</span>
<span class="co1">//   - partitions the heightfield into regions without holes and overlaps (guaranteed)</span>
<span class="co1">//   - creates long thin polygons, which sometimes causes paths with detours</span>
<span class="co1">//   * use this if you want fast navmesh generation</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> partitionType <span class="sy0">=</span> <span class="st0">"Sample partition watershed"</span><span class="sy0">;</span>
 
<span class="kw1">if</span> <span class="br0">(</span>partitionType.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Sample partition watershed"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">buildDistanceField</span><span class="br0">(</span>context, compactHeightfield<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not build distance field"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span><span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">buildRegions</span><span class="br0">(</span>context, compactHeightfield, config<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not build watershed regions"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span>
 
<span class="kw1">if</span> <span class="br0">(</span>partitionType.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"Sample partition monotone"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">buildRegionsMonotone</span><span class="br0">(</span>context, compactHeightfield, config<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not build monotone regions"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span>
 
<span class="co1">// Step 5. Trace and simplify region contours.</span>
<span class="co1">// Create contours.</span>
ContourSet contourSet <span class="sy0">=</span> <span class="kw1">new</span> ContourSet<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">buildContours</span><span class="br0">(</span>context, compactHeightfield, 2f, config.<span class="me1">getMaxEdgeLength</span><span class="br0">(</span><span class="br0">)</span>, contourSet<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not create contours"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="co1">// Step 6. Build polygons mesh from contours.</span>
<span class="co1">// Build polygon navmesh from the contours.</span>
PolyMesh polyMesh <span class="sy0">=</span> <span class="kw1">new</span> PolyMesh<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">buildPolyMesh</span><span class="br0">(</span>context, contourSet, config.<span class="me1">getMaxVertsPerPoly</span><span class="br0">(</span><span class="br0">)</span>, polyMesh<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not triangulate contours"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="co1">// Step 7. Create detail mesh which allows to access approximate height on each polygon.</span>
PolyMeshDetail polyMeshDetail <span class="sy0">=</span> <span class="kw1">new</span> PolyMeshDetail<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>RecastBuilder.<span class="me1">buildPolyMeshDetail</span><span class="br0">(</span>context, polyMesh, compactHeightfield, config, polyMeshDetail<span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not build detail mesh."</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
<span class="co1">// (Optional) Step 8. Create Detour data from Recast poly mesh.</span>
<span class="co1">// The GUI may allow more max points per polygon than Detour can handle.</span>
<span class="co1">// Only build the detour navmesh if we do not exceed the limit.</span>
<span class="kw1">if</span> <span class="br0">(</span>config.<span class="me1">getMaxVertsPerPoly</span><span class="br0">(</span><span class="br0">)</span> <span class="sy0">&gt;</span> DetourBuilder.<span class="me1">VERTS_PER_POLYGON</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
NavMeshCreateParams createParams <span class="sy0">=</span> <span class="kw1">new</span> NavMeshCreateParams<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
createParams.<span class="me1">getData</span><span class="br0">(</span>polyMesh<span class="br0">)</span><span class="sy0">;</span>
createParams.<span class="me1">getData</span><span class="br0">(</span>polyMeshDetail<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">//setting optional off-mesh connections (in my example there are none)</span>
createParams.<span class="me1">getData</span><span class="br0">(</span>config<span class="br0">)</span><span class="sy0">;</span>
createParams.<span class="me1">setBuildBvTree</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw4">char</span><span class="br0">[</span><span class="br0">]</span> navData <span class="sy0">=</span> DetourBuilder.<span class="me1">createNavMeshData</span><span class="br0">(</span>createParams<span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">if</span> <span class="br0">(</span>navData <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not build Detour navmesh."</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
NavMesh navMesh <span class="sy0">=</span> <span class="kw1">new</span> NavMesh<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
 
<span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>navMesh.<span class="me1">isAllocationSuccessful</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not create Detour navmesh"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
Status status<span class="sy0">;</span>
status <span class="sy0">=</span> navMesh.<span class="me1">init</span><span class="br0">(</span>navData, TileFlags.<span class="me1">DT_TILE_FREE_DATA</span>.<span class="me1">value</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>status.<span class="me1">isFailed</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not init Detour navmesh"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span>
 
NavMeshQuery query <span class="sy0">=</span> <span class="kw1">new</span> NavMeshQuery<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
status <span class="sy0">=</span> query.<span class="me1">init</span><span class="br0">(</span>navMesh, <span class="nu0">2048</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">if</span> <span class="br0">(</span>status.<span class="me1">isFailed</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Could not init Detour navmesh query"</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="kw1">return</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
After this (if everything is successful) you can use methods in <code>query</code> that was created for path-finding purposes.
</p>

</div>
<!-- EDIT6 SECTION "Example" [1452-8377] -->
<h2 class="sectionedit7" id="how_to_get_jnavigation">How to get jNavigation</h2>
<div class="level2">

<p>
There is 2 ways to get jNavigation:
</p>
<ul>
<li class="level1"><div class="li"> as plugin form</div>
</li>
<li class="level1"><div class="li"> as developmental project</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "How to get jNavigation" [8378-8498] -->
<h3 class="sectionedit8" id="plugin">Plugin</h3>
<div class="level3">

<p>
You can download “stable” version from <a href="https://github.com/QuietOne/jNavigationPlugin/tree/master" class="urlextern" title="https://github.com/QuietOne/jNavigationPlugin/tree/master" rel="nofollow">repository</a>
</p>

</div>
<!-- EDIT8 SECTION "Plugin" [8499-8629] -->
<h3 class="sectionedit9" id="developmental_project">Developmental project</h3>
<div class="level3">

<p>
Instructions for downloading and setting it up:
</p>
<ul>
<li class="level1"><div class="li"> Download C++ wrapper from <a href="https://github.com/QuietOne/jNavigation-native" class="urlextern" title="https://github.com/QuietOne/jNavigation-native" rel="nofollow">jNavigationNative repository</a></div>
</li>
<li class="level1"><div class="li"> Build downloaded project with C++ compiler</div>
</li>
<li class="level1"><div class="li"> Download java library from <a href="https://github.com/QuietOne/jNavigation" class="urlextern" title="https://github.com/QuietOne/jNavigation" rel="nofollow">jNavigation repository</a></div>
</li>
<li class="level1"><div class="li"> In Java project in class <code>com.jme3.ai.navigation.utils.RecastJNI.java</code> change <abbr title="Uniform Resource Locator">URL</abbr> to where your build of C++ project is.</div>
</li>
</ul>
<pre class="code java"><span class="kw1">static</span> <span class="br0">{</span>
    <span class="co1">// the URL that needs to be changed</span>
    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">load</span><span class="br0">(</span><span class="st0">".../jNavigationNative.dll"</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
If there is problem with building C++ project see <a href="/jme3/advanced/building_recast.html" class="wikilink1" title="jme3:advanced:building_recast">link</a>.
</p>

</div>
<!-- EDIT9 SECTION "Developmental project" [8630-9300] -->
<h3 class="sectionedit10" id="questions_suggestions">Questions &amp; Suggestions</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> For suggestion and/or question on jNavigation post on <a href="http://hub.jmonkeyengine.org/forum/board/development/summer-of-code/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/board/development/summer-of-code/" rel="nofollow">forum</a></div>
</li>
<li class="level1"><div class="li"> For question on Recast (C++ library) ask on <a href="https://groups.google.com/forum/#!forum/recastnavigation" class="urlextern" title="https://groups.google.com/forum/#!forum/recastnavigation" rel="nofollow">Google groups</a></div>
</li>
</ul>

</div>
<!-- EDIT10 SECTION "Questions & Suggestions" [9301-9596] -->
<h3 class="sectionedit11" id="source">Source</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> <a href="https://github.com/QuietOne/jNavigationPlugin/tree/master" class="urlextern" title="https://github.com/QuietOne/jNavigationPlugin/tree/master" rel="nofollow">jNavigation plugin repository</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/QuietOne/jNavigation" class="urlextern" title="https://github.com/QuietOne/jNavigation" rel="nofollow">Developmental jNavigation repository</a></div>
</li>
<li class="level1"><div class="li"> <a href="https://github.com/QuietOne/jNavigation-native" class="urlextern" title="https://github.com/QuietOne/jNavigation-native" rel="nofollow">Developmental jNavigationNative repository</a></div>
</li>
</ul>

</div>

<h4 id="useful_links">Useful links</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> <a href="/jme3/advanced/building_recast.html" class="wikilink1" title="jme3:advanced:building_recast">How to build the native recast bindings</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.critterai.org/projects/nmgen_study/" class="urlextern" title="http://www.critterai.org/projects/nmgen_study/" rel="nofollow">Study: Navigation Mesh Generation</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.stevefsp.org/projects/rcndoc/prod/index.html" class="urlextern" title="http://www.stevefsp.org/projects/rcndoc/prod/index.html" rel="nofollow">Documentation of C++ Recast library</a> It can be useful for tracing bugs.</div>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "Source" [9597-] -->
