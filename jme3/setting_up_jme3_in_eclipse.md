---
title: Setting up JME3 in Eclipse
---
<h1 class="sectionedit1" id="setting_up_jme3_in_eclipse">Setting up JME3 in Eclipse</h1>
<div class="level1">

<p>
For development with the jMonkeyEngine 3, we recommend to use the jMonkeyEngine SDK.
</p>

<p>
Alternatively, you can use your favorite IDE: In this tutorial we show how to download and set up the latest nightly build of the jMonkeyEngine 3 for use with the Eclipse IDE. Instructions for <a href="/jme3/setting_up_netbeans_and_jme3.html" class="wikilink1" title="jme3:setting_up_netbeans_and_jme3">NetBeans IDE</a> are also available.
</p>

</div>
<!-- EDIT1 SECTION "Setting up JME3 in Eclipse" [1-394] -->
<h2 class="sectionedit2" id="downloading_jme3">Downloading jME3</h2>
<div class="level2">

<p>
The currently available JAR binaries are the nightly builds. 
</p>
<ol>
<li class="level1"><div class="li"> Download the most recent zipped build from <a href="http://updates.jmonkeyengine.org/stable/3.0/engine" class="urlextern" title="http://updates.jmonkeyengine.org/stable/3.0/engine" rel="nofollow">http://updates.jmonkeyengine.org/stable/3.0/engine</a></div>
</li>
<li class="level1"><div class="li"> Unzip the file and save it as <code>jME3_2012-xx-xx</code> in your home directory ($HOME). You should see the following files and directories:</div>
<ul>
<li class="level2"><div class="li"> <code>lib/</code> – The jMonkeyEngine binaries, and libraries used by the jMonkeyEngine. (Don't remove)</div>
</li>
<li class="level2"><div class="li"> <code>TestChooser.exe</code> – Run this file to see various feature demos. (optional)</div>
</li>
<li class="level2"><div class="li"> <code>javadoc/</code> – jME3 <abbr title="Application Programming Interface">API</abbr> documentation. (optional)</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Downloading jME3" [395-967] -->
<h2 class="sectionedit3" id="creating_a_new_game_project">Creating a New Game Project</h2>
<div class="level2">
<ul>
<li class="level1"><div class="li"> In Eclipse, choose File &gt; New &gt; Java Project</div>
</li>
<li class="level1"><div class="li"> Project Name: HelloJME3</div>
</li>
<li class="level1"><div class="li"> Click Finish</div>
</li>
</ul>

<p>
The new project appears in the Explorer.
</p>

</div>
<!-- EDIT3 SECTION "Creating a New Game Project" [968-1145] -->
<h2 class="sectionedit4" id="setting_up_dependencies">Setting up Dependencies</h2>
<div class="level2">

<p>
Your project depends on the jMonkeyEngine libraries and needs to know where they are.
</p>
<ol>
<li class="level1"><div class="li"> Right-click the project in the explorer and choose <code>Build Path &gt; Add External Archives</code></div>
</li>
<li class="level1"><div class="li"> In the “JAR selection” dialog, browse to the <code>$HOME/jME3_2012-xx-xx</code> directory.</div>
</li>
<li class="level1"><div class="li"> Select all JARs in the <code>lib</code> directory and click Open.</div>
</li>
</ol>

<p>
All necessary JAR libraries are now on the classpath and should appear in the Referenced Libraries list. For a detailed description of the separate jar files see <a href="/jme3/jme3_source_structure.html" class="wikilink1" title="jme3:jme3_source_structure">this list</a>.
</p>

</div>
<!-- EDIT4 SECTION "Setting up Dependencies" [1146-1747] -->
<h2 class="sectionedit5" id="setting_up_assets">Setting up Assets</h2>
<div class="level2">

<p>
The easiest way to make sure the asset manager can access the assets is by adding the assets folder to the classpath.
</p>
<ol>
<li class="level1"><div class="li"> Go to Project Properties</div>
</li>
<li class="level1"><div class="li"> Select Java Build Path</div>
</li>
<li class="level1"><div class="li"> Under the Source tab click add folder </div>
</li>
<li class="level1"><div class="li"> Add your Assets folder</div>
</li>
</ol>

</div>
<!-- EDIT5 SECTION "Setting up Assets" [1748-2024] -->
<h2 class="sectionedit6" id="writing_a_simple_application">Writing a Simple Application</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> From the menu call File &gt; New &gt; New Package. Name the src package for example <code>hello</code>.</div>
</li>
<li class="level1"><div class="li"> From the menu call File &gt; New &gt; Class. </div>
<ul>
<li class="level2"><div class="li"> Select package <code>hello</code>.</div>
</li>
<li class="level2"><div class="li"> Name the class for example <code>MyGame</code>.</div>
</li>
<li class="level2"><div class="li"> Superclass: <code>com.jme3.app.SimpleApplication</code></div>
</li>
<li class="level2"><div class="li"> Make sure that the checkbox to Create the <code>main()</code> Method is active</div>
</li>
<li class="level2"><div class="li"> Make sure that the checkbox to Inheriting Abstract Methods is active</div>
</li>
<li class="level2"><div class="li"> Click Finish.</div>
</li>
</ul>
</li>
</ol>

<p>
You can now continue to write <a href="/jme3/beginner/hello_simpleapplication.html" class="wikilink1" title="jme3:beginner:hello_simpleapplication">your first jme3 application</a>!
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>,
	<a href="/tag/eclipse.html" class="wikilink1" title="tag:eclipse" rel="tag">eclipse</a>
</span></div>

</div>
<!-- EDIT6 SECTION "Writing a Simple Application" [2025-] -->
