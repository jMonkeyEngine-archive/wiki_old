---
title: How to integrate your own jME3 compile in jMonkeyEngine SDK projects
---
<h2 class="sectionedit1" id="how_to_integrate_your_own_jme3_compile_in_jmonkeyengine_sdk_projects">How to integrate your own jME3 compile in jMonkeyEngine SDK projects</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> <a href="/jme3/build_jme3_sources_with_netbeans.html" class="wikilink1" title="jme3:build_jme3_sources_with_netbeans">Download jme3 project from svn</a></div>
</li>
<li class="level1"><div class="li"> Make your changes</div>
</li>
<li class="level1"><div class="li"> Compile jme3 project</div>
</li>
<li class="level1"><div class="li"> Go to Tools → Libraries</div>
</li>
<li class="level1"><div class="li"> Press “New Library”</div>
</li>
<li class="level1"><div class="li"> Name it “jme3-modified”</div>
</li>
<li class="level1"><div class="li"> Press “Add Jar/Folder”</div>
</li>
<li class="level1"><div class="li"> Select all JAR files from the <code>dist</code> dir of the compiled jme3 version</div>
</li>
<li class="level1"><div class="li"> Add the <code>src</code> folder of the jme3 project in the “sources” tab</div>
</li>
<li class="level1"><div class="li"> Optionally javadoc in the “javadoc” tab</div>
</li>
<li class="level1"><div class="li"> Press “OK”</div>
</li>
<li class="level1"><div class="li"> Right-click your project and select “Properties”</div>
</li>
<li class="level1"><div class="li"> Select “Libraries” to the left</div>
</li>
<li class="level1"><div class="li"> Remove the “jme3” library</div>
</li>
<li class="level1"><div class="li"> Press “Add Library” and select the “jme3-modified” library</div>
</li>
</ol>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/project.html" class="wikilink1" title="tag:project" rel="tag">project</a>,
	<a href="/tag/builds.html" class="wikilink1" title="tag:builds" rel="tag">builds</a>
</span></div>

</div>
