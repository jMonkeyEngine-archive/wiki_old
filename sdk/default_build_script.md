---
title: Default Build Script
---
<h1 class="sectionedit1" id="default_build_script">Default Build Script</h1>
<div class="level1">

<p>
If you use jMonkeyEngine libraries together with the jMonkeyEngine SDK (recommended) then you benefit from the provided build script. Every new project comes with a default Ant script. The toolbar buttons and clean/build/run actions in the jMonkeyEngine SDK are already pre-configured.  
</p>

</div>
<!-- EDIT1 SECTION "Default Build Script" [1-325] -->
<h2 class="sectionedit2" id="default_targets">Default Targets</h2>
<div class="level2">

<p>
The build script includes targets for the following tasks:
</p>
<ul>
<li class="level1"><div class="li"> clean – deletes the built classes and executables in the dist directory.</div>
</li>
<li class="level1"><div class="li"> jar – compiles the classes, bundles the assets, builds the executable JAR in the dist directory, copies libraries.</div>
</li>
<li class="level1"><div class="li"> run – builds and runs the executable JAR (e.g. for the developers to test it).</div>
</li>
<li class="level1"><div class="li"> javadoc – compiles javadoc from your java files into html files.</div>
</li>
<li class="level1"><div class="li"> debug – used by the jMonkeyEngine SDK Debugger plugin.</div>
</li>
<li class="level1"><div class="li"> test – Used by the jMonkeyEngine SDK JUnit Test plugin.</div>
</li>
</ul>

<p>
You can call these targets on the command line using default Ant commands:
</p>
<pre class="code">ant clean
ant jar
ant run</pre>

<p>
</p><p></p><div class="notetip">We recommended to use the user-friendly menu items, F-keys, or toolbar buttons in the jMonkeyEngine SDK to trigger clean, build, and run actions.
</div>


</div>
<!-- EDIT2 SECTION "Default Targets" [326-1167] -->
<h2 class="sectionedit3" id="browsing_the_build_script">Browsing the Build Script</h2>
<div class="level2">

<p>
To see the build script and the predefined tasks
</p>
<ol>
<li class="level1"><div class="li"> Open your project in the jMonkeyEngine SDK if it isn't already open (File &gt; Open Project…)</div>
</li>
<li class="level1"><div class="li"> Open the Files window (Window &gt; Files)</div>
</li>
<li class="level1"><div class="li"> Open the project node. You see <code>build.xml</code> listed.</div>
<ol>
<li class="level2"><div class="li"> Double-click <code>build.xml</code> to see how the jme3-specify build targets were defined. You typically do not need to edit the existing ones, but you can.</div>
</li>
<li class="level2"><div class="li"> Click the triangle next to <code>build.xml</code> to see all targets.</div>
<ol>
<li class="level3"><div class="li"> Double-click a target in the Files window, or the Navigator, to see how the target was defined. <br />
You will notice that the file <code>nbproject/build-impl.xml</code> opens. It contains very generic targets that you typically will never need to edit. Note that <code>build.xml</code> includes <code>build-impl.xml</code>!</div>
</li>
</ol>
</li>
</ol>
</li>
</ol>

</div>
<!-- EDIT3 SECTION "Browsing the Build Script" [1168-1979] -->
<h2 class="sectionedit4" id="adding_custom_targets">Adding Custom Targets</h2>
<div class="level2">

<p>
<a href="/resources/sdk-build-impl.png" class="media" title="sdk:build-impl.png"><img src="/resources/sdk-build-impl.png" class="mediaright" alt="" /></a>
The build script is a non-proprietary Apache Ant script. It will work out-of-the-box, but if necessary, you can extend and customize it. 
</p>

<p>
Read the comments in <code>build.xml</code>, they explain how to override targets, or extend them, to customize the build process without breaking the existing functionality.
</p>

<p>
Additionally, you can manually override the targets in the <code>*-impl.xml</code> files that are created when you change the deployment settings:
</p>
<ul>
<li class="level1"><div class="li"> linuxlauncher-impl.xml,</div>
</li>
<li class="level1"><div class="li"> macapp-impl.xml, </div>
</li>
<li class="level1"><div class="li"> mobile-impl.xml, </div>
</li>
<li class="level1"><div class="li"> jnlp-impl.xml, etc. </div>
</li>
</ul>

<p>
Simply copy&amp;paste a target from these files into the main build.xml and that will be run instead with all modifications.
</p>

<p>
Don't edit the base <code>*-impl.xml</code> files directly, if you deactivate and reactivate a deployment setting, the SDK resets these files, so you have to copy the whole target and its dependencies, else your build script will become invalid when you disable the deployment option.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/builds.html" class="wikilink1" title="tag:builds" rel="tag">builds</a>,
	<a href="/tag/project.html" class="wikilink1" title="tag:project" rel="tag">project</a>,
	<a href="/tag/deployment.html" class="wikilink1" title="tag:deployment" rel="tag">deployment</a>
</span></div>

</div>
<!-- EDIT4 SECTION "Adding Custom Targets" [1980-] -->
