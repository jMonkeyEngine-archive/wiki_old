---
title: Building jMonkeyEngine 3 from the Sources
---
<h1 class="sectionedit1" id="building_jmonkeyengine_3_from_the_sources">Building jMonkeyEngine 3 from the Sources</h1>
<div class="level1">

<p>
We recommend downloading the <a href="http://hub.jmonkeyengine.org/downloads" class="urlextern" title="http://hub.jmonkeyengine.org/downloads" rel="nofollow">jMonkeyEngine SDK</a> - but of course you can also build the jMonkeyEngine yourself from the sources. In this case, you need the <a href="http://subversion.tigris.org" class="urlextern" title="http://subversion.tigris.org" rel="nofollow">Subversion</a> file version system installed (svn).
</p>
<ol>
<li class="level1"><div class="li"> <strong>Checkout:</strong> Checkout the Subversion repository. <pre class="code">svn checkout http://jmonkeyengine.googlecode.com/svn/branches/3.0final/engine jme3</pre>
</div>
<ul>
<li class="level2"><div class="li"> You can leave login and password empty</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <strong>Build:</strong> Execute <code>ant jar</code></div>
<ul>
<li class="level2"><div class="li"> This compiles the JAR files in <code>dist/libs/*</code></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <strong>Javadoc:</strong> Execute <code>ant javadoc</code> </div>
<ul>
<li class="level2"><div class="li"> This generates javadocs in the <code>dist/javadoc</code> directory.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <strong>Run:</strong> Execute <code>ant run</code></div>
<ul>
<li class="level2"><div class="li"> This runs the TestChooser where you can browse examples.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <strong>Use:</strong> Create a Java SE project and place all JARs from the <code>dist/lib</code> directory on the classpath.</div>
<ul>
<li class="level2"><div class="li"> You can now extend your first game from <code>com.jme3.app.SimpleApplication</code>. </div>
</li>
</ul>
</li>
</ol>

<p>
For a detailed description of the created jar files see <a href="/jme3/jme3_source_structure.html" class="wikilink1" title="jme3:jme3_source_structure">this list</a>.
</p>
<hr />

<p>
Learn more about:
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline">Setting up JME3 on the commandline (generic)</a>.</div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/build_jme3_sources_with_netbeans.html" class="wikilink1" title="jme3:build_jme3_sources_with_netbeans">Building JME3 from the sources with NetBeans</a> </div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>
</span></div>

</div>
