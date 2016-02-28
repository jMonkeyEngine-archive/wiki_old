---
title: Creating a jMonkeyEngine SDK plugin
---
<h1 class="sectionedit1" id="creating_a_jmonkeyengine_sdk_plugin">Creating a jMonkeyEngine SDK plugin</h1>
<div class="level1">

<p>
Note that the creation of a Module Suite is only necessary if you want to upload your plugin to the contribution update center.
</p>

</div>
<!-- EDIT1 SECTION "Creating a jMonkeyEngine SDK plugin" [1-178] -->
<h3 class="sectionedit2" id="using_jmonkeyengine_sdk_for_development">Using jMonkeyEngine SDK for development</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Install the “Netbeans Plugin Development” and “NetBeans <abbr title="Application Programming Interface">API</abbr> Documentation” plugins via Tools→Plugins</div>
</li>
<li class="level1"><div class="li"> Create a new “Module Suite” project (can be any name, this will be your local “collection” of plugins that you create)</div>
</li>
<li class="level1"><div class="li"> If no platform is listed, add one by selecting the SDK application folder</div>
<ul>
<li class="level2"><div class="li"> Mac users have to right-click the jmonkeyplatform application and select “show contents” and then select the jmonkeyplatform folder under Contents/Resources/</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Open the suite, right-click the “Modules” folder and select “Add new..”</div>
</li>
<li class="level1"><div class="li"> For “Project Name” enter an all-lowercase name without spaces like <code>my-library</code></div>
</li>
<li class="level1"><div class="li"> Make sure the “Project Location” is inside the module suite folder and press “Next”</div>
</li>
<li class="level1"><div class="li"> Enter the base java package for your plugin in “Code Name Base” like <code>com.mycompany.plugins.mylibrary</code></div>
</li>
<li class="level1"><div class="li"> Enter a “Module Display Name” for your plugin like “My Library”</div>
</li>
<li class="level1"><div class="li"> Press Finish</div>
</li>
<li class="level1"><div class="li"> To use core SDK or jME3 functions, add “SDK Core” and “SDK Engine” via “Module Properties→Library→Add Dependency”</div>
</li>
<li class="level1"><div class="li"> Write your plugin (e.g. <a href="/sdk/development.html" class="wikilink1" title="sdk:development">create a new editor</a> or <a href="/sdk/development/extension_library.html" class="wikilink1" title="sdk:development:extension_library">wrap a jar library</a>)</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Using jMonkeyEngine SDK for development" [179-1392] -->
<h3 class="sectionedit3" id="jmonkeyengine_sdk_contributions_update_center">jMonkeyEngine SDK Contributions Update Center</h3>
<div class="level3">

<p>
If you want your plugin to appear in the “jMonkeyEngine SDK Contributions Update Center” so users can download, install and update it easily via the plugin manager, you can host your plugin in the contributions update center svn repository. The contributions update center is based on a googlecode project for contributed plugins which will be automatically compiled, version-labeled and added to the contributions update center like the core jMonkeyEngine SDK plugins.
</p>

<p>
Effectively its one large module suite with multiple modules which each represent one plugin, extension library.
</p>

</div>

<h4 id="adding_your_plugin_to_the_repository">Adding your plugin to the repository</h4>
<div class="level4">

<p>
To add your plugin to the repository, do the following:
</p>
<ul>
<li class="level1"><div class="li"> Make sure the plugin is part of a “Module Suite” and that its located in the folder of the suite (this saves you from problems with the svn and local version not being configured the same)</div>
</li>
<li class="level1"><div class="li"> In “Module Properties→Sources”</div>
<ul>
<li class="level2"><div class="li"> Set the “Source Level” to 1.5 if possible (jMonkeyEngine SDK is compatible to Java 1.5)</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In “Module Properties→<abbr title="Application Programming Interface">API</abbr> Versioning”</div>
<ul>
<li class="level2"><div class="li"> Set a specification version for your plugin (like 0.8.1)</div>
</li>
<li class="level2"><div class="li"> Set the “implementation version” to “0” and select “append implementation versions automatically”</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In “Module Properties→Display”</div>
<ul>
<li class="level2"><div class="li"> Enter a purposeful description of your plugin and one of the following categories:</div>
<ul>
<li class="level3"><div class="li"> For a library plugin: “jME3 - Library”</div>
</li>
<li class="level3"><div class="li"> For a SDK plugin: “jME3 - SDK Plugin”</div>
</li>
<li class="level3"><div class="li"> For a model loader plugin: “jME3 - Loader”</div>
</li>
</ul>
</li>
</ul>
</li>
<li class="level1"><div class="li"> In “Module Properties→Build→Packaging”</div>
<ul>
<li class="level2"><div class="li"> Add your name</div>
</li>
<li class="level2"><div class="li"> Add a link to your forum post / home page relating to the plugin</div>
</li>
<li class="level2"><div class="li"> Add a license, you can use <code>../license-jme.txt</code> to insert the default jME BSD license or use a text file you store in the project folder</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Ask the managers or developers for access to the gc project</div>
</li>
<li class="level1"><div class="li"> Commit <strong>only the module project</strong> to trunk:</div>
<ul>
<li class="level2"><div class="li"> Right click the Module Project and select “Versioning → Import into Subversion Repository”</div>
</li>
<li class="level2"><div class="li"> Enter <code><a href="https://jmonkeyplatform-contributions.googlecode.com/svn/trunk" class="urlextern" title="https://jmonkeyplatform-contributions.googlecode.com/svn/trunk" rel="nofollow">https://jmonkeyplatform-contributions.googlecode.com/svn/trunk</a></code> in the <abbr title="Uniform Resource Locator">URL</abbr> field</div>
</li>
<li class="level2"><div class="li"> Enter your googlecode username and commit password (different than login pass, you can find your password <a href="https://code.google.com/hosting/settings" class="urlextern" title="https://code.google.com/hosting/settings" rel="nofollow">here</a>!) and press “Next”</div>
</li>
<li class="level2"><div class="li"> Check that the “Repository Folder” is <code>trunk/mypluginfolder</code> and enter an import message</div>
</li>
<li class="level2"><div class="li"> Press “Finish”</div>
</li>
</ul>
</li>
</ul>

<p>
And thats it, from now on each time you commit changes to your module it will be built and added to the contributions center automatically and the version number will be extended by the svn revision number (e.g. 0.8.1.1234)
</p>

</div>

<h4 id="building_wrapped_library_jar_files_on_the_server">Building wrapped library jar files on the server</h4>
<div class="level4">

<p>
You can just build your library locally and update and commit the jar file and javadoc/sources zip files to the <code>release/libs</code> folder of your plugin in the contrib repo. The users plugins will automatically be updated with the new jar files. You can however also build the library project on the server.
</p>

<p>
As normally only the module project is being built on the server, any projects that create the actual jar files for library plugins (“normal” projects from the SDK/NetBeans) have to be built from the module build file. To do that simply add the following ant targets to the module build file (adapt to your project file and folder names):
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;target</span> <span class="re0">name</span>=<span class="st0">"init"</span> <span class="re0">depends</span>=<span class="st0">"basic-init,files-init,build-init,-javac-init,-build-subproject"</span><span class="re2">/&gt;</span></span>
<span class="sc3"><span class="re1">&lt;target</span> <span class="re0">name</span>=<span class="st0">"-build-subproject"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;ant</span> <span class="re0">dir</span>=<span class="st0">"./AI"</span> <span class="re0">inheritall</span>=<span class="st0">"false"</span> <span class="re0">inheritrefs</span>=<span class="st0">"false"</span> <span class="re0">target</span>=<span class="st0">"clean"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;ant</span> <span class="re0">dir</span>=<span class="st0">"./AI"</span> <span class="re0">inheritall</span>=<span class="st0">"false"</span> <span class="re0">inheritrefs</span>=<span class="st0">"false"</span> <span class="re0">target</span>=<span class="st0">"jar"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;ant</span> <span class="re0">dir</span>=<span class="st0">"./AI"</span> <span class="re0">inheritall</span>=<span class="st0">"false"</span> <span class="re0">inheritrefs</span>=<span class="st0">"false"</span> <span class="re0">target</span>=<span class="st0">"javadoc"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;zip</span> <span class="re0">basedir</span>=<span class="st0">"./AI/dist/javadoc"</span> <span class="re0">file</span>=<span class="st0">"release/libs/jME3-ai-javadoc.zip"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;zip</span> <span class="re0">basedir</span>=<span class="st0">"./AI/src"</span> <span class="re0">file</span>=<span class="st0">"release/libs/jME3-ai-sources.zip"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;copy</span> <span class="re0">file</span>=<span class="st0">"./AI/dist/jME3-ai.jar"</span> <span class="re0">todir</span>=<span class="st0">"release/libs"</span><span class="re2">/&gt;</span></span>
<span class="sc3"><span class="re1">&lt;/target<span class="re2">&gt;</span></span></span></pre>

<p>
<strong>Note that for the module version number to increase automatically on a commit to the library project, the library project has to be a subfolder of the main module project.</strong>
</p>

</div>
<!-- EDIT3 SECTION "jMonkeyEngine SDK Contributions Update Center" [1393-] -->
