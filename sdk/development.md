---
title: Developing for jMonkeyEngine SDK
---
<h2 class="sectionedit1" id="developing_for_jmonkeyengine_sdk">Developing for jMonkeyEngine SDK</h2>
<div class="level2">

<p>
<em>Note that all info is subject to change while jMonkeyEngine SDK is still in beta!</em>
</p>

<p>
In general, developing plugins for jMonkeyEngine SDK is not much different than creating plugins for the NetBeans Platform which in turn is not much different than creating Swing applications. You can use jMonkeyEngine SDK to develop plugins, be it for personal use or to contribute to the community.
</p>

<p>
If you feel like you want to make an addition to jMonkeyEngine SDK, don't hesitate to contact the jme team regardless of your knowledge in NetBeans platform development. For new plugins, the basic project creation and layout of the plugin can always be handled by a core developer and you can go on from there fleshing out the plugin. By using the Platform functions, your plugin feels more like a Platform application (global save button, file type support etc.).
</p>

</div>

<h4 id="creating_plugins_and_components">Creating plugins and components</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> <a href="/sdk/development/setup.html" class="wikilink1" title="sdk:development:setup">Creating a plugin</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/development/general.html" class="wikilink1" title="sdk:development:general">Creating components</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/build_platform.html" class="wikilink1" title="sdk:build_platform">Building the jME SDK from scratch</a> (not necessary for plugin development, only for contributors)</div>
</li>
</ul>

</div>

<h4 id="extending_jmonkeyengine_sdk">Extending jMonkeyEngine SDK</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> <a href="/sdk/development/scene.html" class="wikilink1" title="sdk:development:scene">The Main Scene</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/development/sceneexplorer.html" class="wikilink1" title="sdk:development:sceneexplorer">The Scene Explorer</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/development/projects_assets.html" class="wikilink1" title="sdk:development:projects_assets">Projects and Assets</a></div>
</li>
</ul>

</div>

<h4 id="recipes">Recipes</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> <a href="/sdk/development/extension_library.html" class="wikilink1" title="sdk:development:extension_library">Create a library plugin from a jar file</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/development/model_loader.html" class="wikilink1" title="sdk:development:model_loader">Create a new or custom model filetype and loader</a></div>
</li>
</ul>

</div>

<h4 id="general_notes">General Notes</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> <strong>Remember the scene runs on the render thread and most everything you do in the plugin (button events etc.) runs on the AWT thread, always encapsulate calls to either side correctly via Callables/Runnables or register as an AppState to the SceneApplication to have an update() call by the render thread.</strong></div>
</li>
<li class="level1"><div class="li"> Although the scene can be accessed at any time via SceneApplication.getApplication() it is not recommended to modify the scene like that. Other plugins might be accessing the scene and updates will not be properly recognized. Use the sceneRequest object and the lookup of selected nodes and files to access things like the assetManager etc.</div>
</li>
<li class="level1"><div class="li"> It became a standard in jMonkeyEngine SDK to start the name of methods that execute directly on the OpenGL thread with “do” e.g “doMoveSpatial”, this makes identifying threading issues easier.</div>
</li>
<li class="level1"><div class="li"> The AssetManager of jme3 is threadsafe and can be used from any thread to load assets</div>
</li>
<li class="level1"><div class="li"> You can get access to the ProjectAssetManager via the Lookup of a JmeSpatial and other objects</div>
</li>
<li class="level1"><div class="li"> Use org.openide.filesystems.FileObject instead of java.io.File for file access, it always uses system-independent “/” path separators and has some more advanced functions that make file handling easier.</div>
</li>
<li class="level1"><div class="li"> You can get a file from a string using Repository.getDefault().getDefaultFileSystem().getRoot().getFileObject(“aaa/bbb/ccc/whatever”);</div>
</li>
<li class="level1"><div class="li"> You can convert a regular java File to a FileObject and vice versa using org.openide.filesystems.FileUtil</div>
</li>
<li class="level1"><div class="li"> If you have problems with unresolved classes, check if all needed Libraries are registered in the settings of your Project. To find out which library contains a certain class, just enter the name in the library search field.</div>
</li>
</ul>

</div>

<h4 id="teminology_used_here">Teminology used here</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> A “plugin” is anything you can tick in the plugin manager of the SDK. It can contain editors, simple “Java SE Libraries” that you can add to your projects as jar files and other things like project templates etc.</div>
</li>
<li class="level1"><div class="li"> A “module” is the project type that allows you to create plugins, strictly speaking all plugins are modules but there can be modules that are never shown in the plugin list and only exist as dependencies of other modules.</div>
</li>
<li class="level1"><div class="li"> A “library” is an entry for a jar file (and optionally sources and javadocs) which can be added to a SDK project to be used and distributed with it</div>
</li>
<li class="level1"><div class="li"> An “extension” is a generic name for stuff that extends the jME engine, like pathfinding algorithms or anything that can be used at the game runtime..</div>
</li>
</ul>

<p>
So if you have some cool code that others can use in their games too, you would make your extension a library by creating a module that the users can download as a plugin :)
</p>

</div>

<h4 id="handy_things_in_jmonkeyengine_sdk_core">Handy things in jMonkeyEngine SDK Core</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> com.jme3.gde.core.scene.controller</div>
<ul>
<li class="level2"><div class="li"> AbstractCameraController → A basic camera control for plugins, used by SimpleSceneComposer and “View Model”</div>
</li>
<li class="level2"><div class="li"> SceneToolController → A basic controller for having selection, cursor etc. displayed in the scene, used by SimpleSceneComposer</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> com.jme3.gde.core.scene</div>
<ul>
<li class="level2"><div class="li"> OffViewPanel → A panel that renders a 3d scene in a preview and displays it in a lightweight swing panel</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> com.jme3.gde.core.util</div>
<ul>
<li class="level2"><div class="li"> DataObjectSaveNode → Allows enabling the save all button by using any file and implementing the SvaeCookie yourself.</div>
</li>
</ul>
</li>
</ul>

<p>
Learn more about NetBeans Plugin Development at <a href="http://platform.netbeans.org" class="urlextern" title="http://platform.netbeans.org" rel="nofollow">http://platform.netbeans.org</a>
</p>

<p>
Also check out this Essential NetBeans Platform Refcard: <a href="http://refcardz.dzone.com/refcardz/essential-netbeans-platform" class="urlextern" title="http://refcardz.dzone.com/refcardz/essential-netbeans-platform" rel="nofollow">http://refcardz.dzone.com/refcardz/essential-netbeans-platform</a>
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/contribute.html" class="wikilink1" title="tag:contribute" rel="tag">contribute</a>
</span></div>

</div>
