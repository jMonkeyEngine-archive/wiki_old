---
title: jMonkeyEngine 3 -- Source Structure
---
<h1 class="sectionedit1" id="jmonkeyengine_3_--_source_structure">jMonkeyEngine 3 -- Source Structure</h1>
<div class="level1">

<p>
An overview of the source structure of the JME3 project. In order to support both Desktop and Android Java platforms, it was necessary to split the source code into several parts. This wiki page describes the packages and their purpose. Status: Up-to-date for JME3 beta.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 -- Source Structure" [1-323] -->
<h2 class="sectionedit2" id="structure_of_src_directory">Structure of src directory</h2>
<div class="level2">

<p>
You can build jME using the included build.xml script: <code>ant clean; ant jar; ant run</code>
When building the sources in a project created with another IDE,  include every folder under <code>src</code> in the project as its own separate source root.
</p>

</div>
<!-- EDIT2 SECTION "Structure of src directory" [324-598] -->
<h3 class="sectionedit3" id="core">Core</h3>
<div class="level3">
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Source Package    </th><th class="col1 leftalign"> Description     </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> src/core         </td><td class="col1"> The main package. Must always be included, as all other packages depend on it. </td>
	</tr>
	<tr class="row2">
		<td class="col0"> src/core-effects </td><td class="col1"> Core effects like Water, PSSM etc. </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> src/core-data    </td><td class="col1"> Basic material definitions, shaders and fonts that are needed by most jME3 applications. </td>
	</tr>
	<tr class="row4">
		<td class="col0"> src/core-plugins </td><td class="col1"> Important asset plugins, such as .j3o model loader, .obj loader, font loader, basic image loaders. </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> src/desktop      </td><td class="col1 leftalign"> Must be included if deploying on desktop, applet or web start. <del>Android</del>  </td>
	</tr>
	<tr class="row6">
		<td class="col0 leftalign"> src/android      </td><td class="col1"> Must be included if deploying on the Android platform. <del>Desktop</del> </td>
	</tr>
	<tr class="row7">
		<td class="col0 leftalign"> src/lwjgl        </td><td class="col1"> LWJGL OpenGL display implementation. <del>Android</del> </td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [614-1335] -->
</div>
<!-- EDIT3 SECTION "Core" [599-1336] -->
<h3 class="sectionedit5" id="physics">Physics</h3>
<div class="level3">
<div class="table sectionedit6"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Source Package </th><th class="col1"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> src/jbullet       </td><td class="col1"> Game Physics Engine, based on the jBullet framework. <del>Bullet</del></td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> src/bullet        </td><td class="col1"> Game Physics Engine, based on the native Bullet framework. <del>jBullet</del></td>
	</tr>
	<tr class="row3">
		<td class="col0"> src/bullet-common </td><td class="col1"> Classes common between native and java Bullet implementations.</td>
	</tr>
	<tr class="row4">
		<td class="col0"> src/bullet-native </td><td class="col1"> Native Bullet implementation C++ classes. <del>jBullet</del></td>
	</tr>
</table></div>
<!-- EDIT6 TABLE [1356-1753] -->
<p>
Note: Only one of the physics libraries can be used at a time as they replace each other.
</p>

</div>
<!-- EDIT5 SECTION "Physics" [1337-1845] -->
<h3 class="sectionedit7" id="plugins_and_extra_packages">Plugins and Extra packages</h3>
<div class="level3">
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Source Package </th><th class="col1"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> src/ogre       </td><td class="col1"> Ogre3D model and scene loader. Supports skeletal and vertex animation, scene loading, and materials. </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> src/xml        </td><td class="col1 leftalign"> Provides an XML im/exporter.  </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> src/jogg       </td><td class="col1 leftalign"> OGG/Vorbis loader to play .ogg sound files.   </td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> src/niftygui   </td><td class="col1"> Support for custom Graphical User Interfaces. </td>
	</tr>
	<tr class="row5">
		<td class="col0 leftalign"> src/blender    </td><td class="col1"> Blender model importer </td>
	</tr>
	<tr class="row6">
		<td class="col0"> src/networking </td><td class="col1"> SpiderMonkey networking package </td>
	</tr>
	<tr class="row7">
		<td class="col0 leftalign"> src/terrain    </td><td class="col1"> Terrain generation tools</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [1883-2369] -->
</div>
<!-- EDIT7 SECTION "Plugins and Extra packages" [1846-2370] -->
<h3 class="sectionedit9" id="tests_games_and_tools">Tests, Games and Tools</h3>
<div class="level3">
<div class="table sectionedit10"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Source Package </th><th class="col1"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> src/test      </td><td class="col1"> Small sample Applications that demo individual jME3 features. ←- jme3_test-data.jar </td>
	</tr>
	<tr class="row2">
		<td class="col0"> src/test-data </td><td class="col1"> Data assets (jme3_test-data.jar) required by jme3_test samples. </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> src/tools     </td><td class="col1"> Tools and programs that help you use jme3. </td>
	</tr>
</table></div>
<!-- EDIT10 TABLE [2404-2688] -->
</div>
<!-- EDIT9 SECTION "Tests, Games and Tools" [2371-2689] -->
<h2 class="sectionedit11" id="structure_of_lib_directory">Structure of lib directory</h2>
<div class="level2">

<p>
JME3 depends on the following JARs and native libraries in the <code>lib</code> directory. The JAR libraries must be on the classpath. 
</p>

<p>
</p><p></p><div class="noteclassic">The jME3-*natives*.jar bundles contain the native libraries, those are necessary <code>.dll</code>, <code>.jnilib</code>, <code>lib*.so</code> files. You do not need to manually include native libraries on the java.library.path! jME3 handles the extraction of natives automatically via the JAR bundles.
</div>

<ul>
<li class="level1"><div class="li"> lib/android:</div>
<ul>
<li class="level2"><div class="li"> android.jar</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> lib/bullet:</div>
<ul>
<li class="level2"><div class="li"> android, jME3-bullet-natives-android.jar, jME3-bullet-natives.jar, jarcontent (natives)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> lib/jbullet:</div>
<ul>
<li class="level2"><div class="li"> asm-all.jar, jbullet.jar, stack-alloc.jar, vecmath.jar</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> lib/jogg:</div>
<ul>
<li class="level2"><div class="li"> j-ogg-oggd.jar, j-ogg-vorbisd.jar</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> lib/lwjgl:</div>
<ul>
<li class="level2"><div class="li"> jME3-lwjgl-natives.jar, jinput.jar, lwjgl.jar</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> lib/niftygui:</div>
<ul>
<li class="level2"><div class="li"> nifty.jar, nifty-javadoc.jar, xmlpull-xpp3.jar, eventbus.jar</div>
</li>
<li class="level2"><div class="li"> nifty-default-controls-javadoc.jar, nifty-default-controls.jar, </div>
</li>
<li class="level2"><div class="li"> nifty-examples.jar, nifty-examples-javadoc.jar, nifty-style-black.jar</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT11 SECTION "Structure of lib directory" [2690-3722] -->
<h2 class="sectionedit12" id="structure_of_jmonkeyengine3_jars">Structure of jMonkeyEngine3 JARs</h2>
<div class="level2">

<p>
After the build is complete (in the <code>dist</code> directory), you see that the jMonkeyEngine library is split up over several JAR files. This allows for better separation of the parts for different operating systems, projects etc. 
</p>
<div class="table sectionedit13"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> JAR file </th><th class="col1"> Purpose </th><th class="col2"> External Dependence </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> dist/lib/jME3-core.jar </td><td class="col1"> Platform-independent core libraries (math, animation, scenegraph, Wavefront OBJ model support, etc) </td><td class="col2"> None </td>
	</tr>
	<tr class="row2">
		<td class="col0"> dist/lib/jME3-effects.jar </td><td class="col1"> Core jME3 effects (Water, SSAO etc) </td><td class="col2"> None </td>
	</tr>
	<tr class="row3">
		<td class="col0"> dist/lib/jME3-desktop.jar </td><td class="col1"> Desktop PC only jME3 libraries </td><td class="col2"> None </td>
	</tr>
	<tr class="row4">
		<td class="col0"> dist/lib/jME3-plugins.jar </td><td class="col1"> Basic import plugins (OgreXML models and j3o XML) </td><td class="col2"> None </td>
	</tr>
	<tr class="row5">
		<td class="col0"> dist/lib/jME3-blender.jar </td><td class="col1"> Blender model import plugin (Desktop only) </td><td class="col2"> None </td>
	</tr>
	<tr class="row6">
		<td class="col0"> dist/lib/jME3-networking.jar </td><td class="col1"> “Spidermonkey” networking library </td><td class="col2"> None </td>
	</tr>
	<tr class="row7">
		<td class="col0"> dist/lib/jME3-jogg.jar </td><td class="col1"> J-OGG audio plugin </td><td class="col2"> j-ogg-vorbisd.jar, j-ogg-oggd.jar </td>
	</tr>
	<tr class="row8">
		<td class="col0"> dist/lib/jME3-terrain.jar </td><td class="col1"> Terrain system </td><td class="col2"> None </td>
	</tr>
	<tr class="row9">
		<td class="col0"> dist/lib/jME3-jbullet.jar </td><td class="col1"> jBullet physics </td><td class="col2"> jbullet.jar, vecmath.jar, stack-alloc.jar, asm-all-3.1.jar </td>
	</tr>
	<tr class="row10">
		<td class="col0"> dist/lib/jME3-bullet.jar </td><td class="col1"> Bullet physics (only jBullet <strong>or</strong> Bullet can be used)</td><td class="col2"> jME3-bullet-natives.jar </td>
	</tr>
	<tr class="row11">
		<td class="col0"> dist/lib/jME3-niftygui.jar </td><td class="col1"> NiftyGUI support </td><td class="col2"> nifty.jar, nifty-default-controls.jar, eventbus.jar, xmlpull-xpp3.jar </td>
	</tr>
	<tr class="row12">
		<td class="col0"> dist/lib/jME3-lwjgl.jar </td><td class="col1"> LWJGL Desktop Renderer </td><td class="col2"> lwjgl.jar, jME3-lwjgl-natives.jar, jinput.jar</td>
	</tr>
	<tr class="row13">
		<td class="col0"> dist/lib/jME3-android.jar </td><td class="col1"> Android Renderer </td><td class="col2"> Android system </td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [3996-5215] -->
<p>
Optional:
</p>
<ul>
<li class="level1"><div class="li"> nifty-examples.jar</div>
</li>
<li class="level1"><div class="li"> jME3-testdata.jar</div>
</li>
<li class="level1"><div class="li"> nifty-style-black.jar (default nifty style)</div>
</li>
</ul>

</div>
<!-- EDIT12 SECTION "Structure of jMonkeyEngine3 JARs" [3723-5319] -->
<h2 class="sectionedit14" id="api_structure">API Structure</h2>
<div class="level2">

<p>
For details see the <a href="http://jmonkeyengine.org/javadoc/" class="urlextern" title="http://jmonkeyengine.org/javadoc/" rel="nofollow">http://jmonkeyengine.org/javadoc/</a>.
</p>

</div>
<!-- EDIT14 SECTION "API Structure" [5320-5405] -->
<h2 class="sectionedit15" id="data_file_types">Data File Types</h2>
<div class="level2">
<div class="table sectionedit16"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Path </th><th class="col1"> File types </th><th class="col2"> purpose </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> /Common/MatDefs/*/ </td><td class="col1"> .glsllib </td><td class="col2"> Standard ShaderLibs </td>
	</tr>
	<tr class="row2">
		<td class="col0"> /Common/MatDefs/*/ </td><td class="col1"> .j3md </td><td class="col2"> Standard Material Definitions </td>
	</tr>
	<tr class="row3">
		<td class="col0"> /Common/Materials/*/ </td><td class="col1"> .j3m </td><td class="col2"> Standard Material </td>
	</tr>
	<tr class="row4">
		<td class="col0"> /Interface/Fonts/ </td><td class="col1"> .fnt + .png </td><td class="col2"> Standard Fonts </td>
	</tr>
</table></div>
<!-- EDIT16 TABLE [5435-5691] -->
<p>
See also supported <a href="/jme3/intermediate/file_types.html" class="wikilink1" title="jme3:intermediate:file_types">File Types</a>.
</p>

</div>
<!-- EDIT15 SECTION "Data File Types" [5406-] -->
