---
title: Eclipse + jME3 + Android + JNI/NDK
---
<h1 class="sectionedit1" id="eclipse_jme3_android_jni_ndk">Eclipse + jME3 + Android + JNI/NDK</h1>
<div class="level1">

<p>
This guide will show you how to effectively set up your Eclipse environment for not only a basic JME3 project, but an Android project, an assets project, and a JNI project (including the ability to build for Android through NDK).
</p>

<p>
While you do not have to create a project of each type to use Eclipse and this guide, note that the Android and JNI projects do require having a base Eclipse project to be applicable using this guide.
</p>

<p>
The code samples provided in this guide should work for any IDE, but setting up/configuring your IDE to do what Eclipse does in this particular guide may require some creative workarounds.
</p>

<p>
</p><p></p><div class="notewarning">Please note that projects that use Android UI elements or are created using Eclipse <strong>can not</strong> be ported to iOS. See <a href="/jme3/android.html" class="wikilink1" title="jme3:android">this page</a> on how to create a cross-platform project using the jME SDK <strong>that can also be edited in the Eclipse IDE</strong>. This saves you the setup work outlined below.
</div>


</div>
<!-- EDIT1 SECTION "Eclipse + jME3 + Android + JNI/NDK" [1-993] -->
<h2 class="sectionedit2" id="setting_up_jme3">Setting up JME3</h2>
<div class="level2">

<p>
I will assume you already have downloaded (and built, if necessary) the JME3 binaries. If not, either download the <a href="http://hub.jmonkeyengine.org/downloads/" class="urlextern" title="http://hub.jmonkeyengine.org/downloads/" rel="nofollow">latest SDK release</a>, <a href="http://updates.jmonkeyengine.org/stable/3.0/engine" class="urlextern" title="http://updates.jmonkeyengine.org/stable/3.0/engine" rel="nofollow">engine build</a> (recommended for new users), or take a quick detour over to <a href="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:build_from_sources" class="urlextern" title="http://hub.jmonkeyengine.org/wiki/doku.php/jme3:build_from_sources" rel="nofollow">this guide</a> to build from source (recommended for advanced users).
</p>

<p>
</p><p></p><div class="noteclassic">One directory you should have on hand (or know where to find) is the location of the resulting library (JAR) files.
</div>


<p>
For the various methods of obtaining the libraries (as described above), the path is usually in one of the following places:
</p>
<ul>
<li class="level1"><div class="li"> <strong>SDK</strong>: [SDK Install Dir]/jmonkeyplatform/libs</div>
</li>
<li class="level1"><div class="li"> <strong>Nightly</strong>: /libs</div>
</li>
<li class="level1"><div class="li"> <strong>Source</strong>: [SDK Dir]/sdk/build/cluster/libs</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">Throughout the course of this guide, <strong>do not copy JAR files</strong> to any project directory - leave them in their original spots so they can be easily updated for when a JME3 update comes out or when you rebuild the source.
</div>


</div>
<!-- EDIT2 SECTION "Setting up JME3" [994-2087] -->
<h2 class="sectionedit3" id="workspace">Workspace</h2>
<div class="level2">

<p>
If you are unfamiliar with Eclipse and how it lays out/stores its configuration, one of the first things that you should be aware of is that almost all settings that are set at a workspace-level (i.e. through <em>Window → Preferences</em>) are stored in the workspace.
</p>

<p>
You can select your workspace either by starting Eclipse (if the initial prompt is enabled) or by navigating to <em>File → Switch Workspace → Other</em>.
</p>

<p>
<a href="/resources/jme3-eclipse-switch-workspace.png" class="media" title="jme3:eclipse-switch-workspace.png"><img src="/resources/jme3-eclipse-switch-workspace.png" class="media" title="Eclipse: Switch Workspace" alt="Eclipse: Switch Workspace" /></a>
</p>

<p>
For this guide, we're going to create a new folder called <code>JMonkey</code> in our <code>C:\</code> drive, however this folder can be anywhere on your drive (the same applies for users of other operating systems). We will also switch to it as a workspace.
</p>

</div>
<!-- EDIT3 SECTION "Workspace" [2088-2836] -->
<h2 class="sectionedit4" id="base_jme3_project_desktops">Base JME3 Project (Desktops)</h2>
<div class="level2">

<p>
<strong>Prerequisites</strong>:
</p>
<ul>
<li class="level1"><div class="li"> JME3 (downloaded/extracted/built/installed) libraries located</div>
</li>
</ul>

<p>
It's time to create our base JME3 project, which is actually relatively easy. Go to <em>File → New → Java Project</em>.
</p>

<p>
NOTE: If you don't see <em>Java Project</em>, you are more than likely in a perspective other than Java or Java EE. Simply select <em>Project…</em> and then select <em>Java → Java Project</em> from the window that appears.
</p>

<p>
Give your project a name (we'll call ours <code>JMEclipse-Base</code>) and click <em>Finish</em>. The project should show up in the Project Explorer pane on the left.
</p>

<p>
First, we need to configure our build path. Right click the new project entry and go to <em>Build Path → Configure Build Path</em>, and then select the <em>Libraries</em> tab.
</p>

<p>
There are a number of libraries you're going to need to include, as the 'core' JME3 system requires them.
</p>

<p>
</p><p></p><div class="noteimportant">There will be many libraries in the previously identified <code>libs</code> folder that aren't initially used. Certain aspects of JME3 (for instance, collision detection) will require the appropriate JAR if your code requires that functionality. However, it is highly recommended you do NOT include every JAR in the <code>libs</code> folder due to the fact that exporting them all when they are not needed will result in a huge jar file (~60MB).
</div>


<p>
Click <em>Add External JARs…</em>, navigate to the JME3 <code>libs</code> folder (see <em>Setting up JME3</em> if you're not sure where this is), and select each of the following:
</p>
<ul>
<li class="level1"><div class="li"> jME3-core.jar</div>
</li>
<li class="level1"><div class="li"> jME3-desktop.jar</div>
</li>
<li class="level1"><div class="li"> jME3-jogl.jar</div>
</li>
<li class="level1"><div class="li"> jME3-lwjgl-natives.jar</div>
</li>
<li class="level1"><div class="li"> jME3-lwjgl.jar</div>
</li>
<li class="level1"><div class="li"> jogl-all.jar</div>
</li>
<li class="level1"><div class="li"> lwjgl.jar</div>
</li>
<li class="level1"><div class="li"> vecmath.jar</div>
</li>
</ul>

<p>
Add the JARs, hit <em>OK</em>, and you've successfully set up the base JME3 build path for your project.
</p>

<p>
The last bit that must be added are assets. Note that while the SDK has a single way of managing your assets, assets can be handled in a number of ways in other IDEs.
</p>

<p>
The rule for assets is that their files <strong>must be on the build path</strong>. This means that you can either include the inner folders directly in your project, or you can create a separate project (and thus, a separate JAR) for your assets.
</p>

<p>
Alternatively, you can keep them in the local directory if you do not wish to package them with the JAR, though this may not be desirable for certain deployments (such as applets, Android apps, or JNLPs).
</p>

<p>
</p><p></p><div class="noteclassic">To include your assets within your base project, follow the <em>Assets</em> section without creating a new project. However, do note that this will make the process of including these assets in your Android project, if you create one, much harder.
</div>


<p>
Finally, the SDK creates a base source file for you that ends up being the main JME3 entry point. Since we're using Eclipse, we'll have to manually create that file.
</p>

<p>
Right click your project, go to <em>New → Class</em>, and fill out the appropriate information:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Package</strong>: your package name (i.e. <code>com.jme3.test</code>)</div>
</li>
<li class="level1"><div class="li"> <strong>Name</strong>: the class name (i.e. <code>MyGame</code>)</div>
</li>
<li class="level1"><div class="li"> <strong>Superclass</strong>: <code>com.jme3.app.SimpleApplication</code></div>
</li>
</ul>

<p>
Then hit Finish. This will create and open the new class file. Eclipse should have automatically inserted the method “simpleInitApp()” for you. This is where all of your game's start up code will go.
</p>

<p>
Finally, create a <code>main</code> function as the Java entry point:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
    MyGame app <span class="sy0">=</span> <span class="kw1">new</span> MyGame<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT4 SECTION "Base JME3 Project (Desktops)" [2837-6256] -->
<h3 class="sectionedit5" id="running">Running</h3>
<div class="level3">

<p>
Running your JME3 project is quite simple in Eclipse. You can either <a href="http://help.eclipse.org/juno/index.jsp?topic=/org.eclipse.jdt.doc.user/tasks/tasks-java-local-configuration.htm" class="urlextern" title="http://help.eclipse.org/juno/index.jsp?topic=/org.eclipse.jdt.doc.user/tasks/tasks-java-local-configuration.htm" rel="nofollow">create a Java run configuration</a> or you can simply hit <code>CTRL + F11</code> to run the project (if Eclipse doesn't know what to do, it will ask).
</p>

</div>
<!-- EDIT5 SECTION "Running" [6257-6600] -->
<h3 class="sectionedit6" id="packaging">Packaging</h3>
<div class="level3">

<p>
Packaging your JME3 project is also very straightforward. Assuming you heeded the warning stated earlier about not including every JAR in the <code>libs</code> folder, you should be able to right click your base JME3 project, go to <em>Export…</em>, select <em>Java → Runnable JAR file</em>, specify an output location and click <em>Finish</em>.
</p>

<p>
If you have assets set up as a JAR, make sure to read the <em>Packaging</em> section under <em>Assets</em>.
</p>

</div>
<!-- EDIT6 SECTION "Packaging" [6601-7046] -->
<h2 class="sectionedit7" id="assets_project">Assets Project</h2>
<div class="level2">

<p>
Each JME project has a set of assets that are used to load textures, models, and other resources used by your game.
</p>

<p>
As mentioned earlier, assets can be located/included in one of several ways. This section will describe how to include your project's assets through the use of a separate JAR file, which has the added advantage of allowing you to update assets without needing to update the JAR itself. If you have a dynamic class-path system set up, this could be very useful.
</p>

<p>
First, create another <strong>generic</strong> project by going to <em>File → New → Project… → General → Project</em> and giving it a name (we'll call ours <code>JMEclipse-Assets</code>).
</p>

<p>
</p><p></p><div class="notetip">We create a General (non-Java) project for cleanliness because our assets will not require any special build settings or the like.
</div>


<p>
For new users, it's a good idea to add the initial JME3 folders that the SDK creates, as they are referenced by many other guides on the web. To do this, for each of the following right click on the assets project and go to <em>New → Folder</em>, type in the name listed, and hit <em>Finish</em>:
</p>
<ul>
<li class="level1"><div class="li"> Interface</div>
</li>
<li class="level1"><div class="li"> MatDefs</div>
</li>
<li class="level1"><div class="li"> Materials</div>
</li>
<li class="level1"><div class="li"> Models</div>
</li>
<li class="level1"><div class="li"> Scenes</div>
</li>
<li class="level1"><div class="li"> Shaders</div>
</li>
<li class="level1"><div class="li"> Sounds</div>
</li>
<li class="level1"><div class="li"> Textures</div>
</li>
</ul>

<p>
Although this specific structure is what the JMonkeyEngine SDK generates upon the creation of a new project, it is by no means the only way to structure your project. All asset loading methods will work with folder names other than those listed above.
</p>

</div>
<!-- EDIT7 SECTION "Assets Project" [7047-8511] -->
<h3 class="sectionedit8" id="packaging1">Packaging</h3>
<div class="level3">

<p>
Packaging your assets is also a simple process. Right click the assets project and click <em>Export…</em> and then select <em>Java → Jar file</em>. It will show a list of files you can export; make sure to uncheck all files such as <code>.classpath</code>, <code>.project</code>, and any <code>.jardesc</code> files you may have created. As well, ensure only the resources and assets you want to export are checked.
</p>

<p>
Check <em>Export generated class files and resources</em>, select a destination for the JAR file, and check <em>Compress the contents of the JAR file</em>, <em>Add directory entries</em>, and <em>Overwrite existing files without warning</em>. Click <em>Finish</em>.
</p>

<p>
</p><p></p><div class="notetip">Optionally, you can click <em>Next</em> and specify a <code>.jardesc</code> file by checking <em>Save the description of this JAR in the workspace</em> and specifying a location for a <code>.jardesc</code> file. That way you can simply double-click the <code>.jardesc</code> file and easily re-export your assets when they change (remember, always refresh your project before exporting!).
</div>


</div>
<!-- EDIT8 SECTION "Packaging" [8512-9527] -->
<h2 class="sectionedit9" id="android_project">Android Project</h2>
<div class="level2">

<p>
<strong>Prerequisites</strong>:
</p>
<ul>
<li class="level1"><div class="li"> JME3 (downloaded/extracted/built/installed) libraries located</div>
</li>
<li class="level1"><div class="li"> JME3 Base Project created (as described above)</div>
</li>
<li class="level1"><div class="li"> Android SDK downloaded and the Android 8 (2.2) target installed (higher <abbr title="Application Programming Interface">API</abbr> versions work too but may limit compatibility when deploying)</div>
</li>
<li class="level1"><div class="li"> Assets compiled into a JAR (see <em>Packaging</em> under <em>Assets</em>)</div>
</li>
<li class="level1"><div class="li"> <a href="http://developer.android.com/sdk/installing/installing-adt.html" class="urlextern" title="http://developer.android.com/sdk/installing/installing-adt.html" rel="nofollow">Eclipse ADT plugin</a> installed</div>
</li>
</ul>

<p>
The Android project is a slightly more involved setup project, but is still quite simple, even for new users.
</p>

<p>
To start, create another Android project by going <em>File → New → Project… → Android → Android Application Project</em>.
</p>

<p>
Fill out the following information and then click Next:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Application Name</strong>: name of your application (i.e. <code>JMEclipse Test Project</code>)</div>
</li>
<li class="level1"><div class="li"> <strong>Project Name</strong>: name of the project in the workspace (i.e. <code>JMEclipse-Android</code>)</div>
</li>
<li class="level1"><div class="li"> <strong>Package Name</strong>: name of the base package, preferably the same as the one used in the base project (we'll re-use <code>com.jme3.test</code>)</div>
</li>
<li class="level1"><div class="li"> <strong>Minimum Required SDK</strong>: <abbr title="Application Programming Interface">API</abbr> 8 (Must be AT LEAST SDK 8 for OpenGLES2 and JNI)</div>
</li>
</ul>

<p>
</p><p></p><div class="noteclassic">Most of the lower options are defaulted based off of your ADT configuration and should work as-is.
</div>


<p>
After clicking <em>Next</em>, uncheck <em>Create activity</em> (JME3 provides a base activity class). You can check/uncheck <em>Create custom launcher icon</em> at your own preference.
</p>

<p>
Make sure that <em>Mark this project as a library</em> is unchecked and hit <em>Finish</em> (or <em>Next</em> if you chose to create a custom launcher icon; this will take you to a customization page, after which you will be forced to finish).
</p>

<p>
First, we need to set up our build path. Surprisingly enough, it's much easier than the base project, though it is done a little differently.
</p>

<p>
At the time of this guide's writing, the latest release of the ADT/Eclipse plugin creates a <code>libs</code> folder within your project structure. This special folder automatically includes all of its contents on the build path. 
</p>

<p>
Normally, you would drop the JAR files directly into this folder. However, this is undesirable as future releases/builds of JME3 would require you to re-copy all of the JAR files. Instead, we will simply link them.
</p>

<p>
For each of the following, right click the <code>libs</code> folder within your Android project and go to <em>New → File</em>, click <em>Advanced »</em>, check <em>Link to file in the file system</em>, click <em>Browse…</em>, navigate to the JME3 <code>libs</code> folder (as identified in the <em>Setting up JME3</em> section above), double click the listed JAR file, and then click <em>Finish</em>:
</p>
<ul>
<li class="level1"><div class="li"> jME3-android.jar</div>
</li>
<li class="level1"><div class="li"> jME3-core.jar</div>
</li>
</ul>

<p>
</p><p></p><div class="noteimportant">There will be many libraries in the previously identified <code>libs</code> folder that aren't initially used. Certain aspects of JME3 (for instance, collision detection) will require the appropriate JAR if your code requires that functionality. However, it is highly recommended you do NOT include every JAR in the <code>libs</code> folder due to the fact that exporting them all when they are not needed will result in a huge jar file (~60MB).
</div>


<p>
As well, repeat the above step for your compiled assets JAR (see <em>Packaging</em> under <em>Assets</em>).
</p>

<p>
Now that the core JME3 libraries have been added, we'll need to include our base project's code. To do this, right click on the Android project and go to <em>Build Path → Configure Build Path</em>, select the <em>Projects</em> tab, click <em>Add</em>, and select the base project (in our case, <code>JMEclipse-Base</code>).
</p>

<p>
Lastly, select the <em>Order and Export</em> tab. Ensure that your base project (i.e. <code>JMEclipse-Base</code>), <em>Android Private Libraries</em>, <em>Android Dependencies</em>, and optionally <em>Google APIs</em> (if you have that target enabled) are checked. This step is important, or your project's libraries/assets will NOT be exported into the end APK.
</p>

<p>
Click <em>OK</em>, and your project's build path will be set up.
</p>

<p>
The next step is to create the application's activity and edit <code>AndroidManifest.xml</code> to configure the project to actually use our JME3 project.
</p>

<p>
First, right click on the Android project and go to <em>New → Class</em>, entering the following information and hitting <em>Finish</em>:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Package</strong>: your application package (it's best to use the package specified in the project creation dialog; for this guide, we'll re-use <code>com.jme3.test</code>)</div>
</li>
<li class="level1"><div class="li"> <strong>Name</strong>: the activity class' name (i.e. <code>JMEclipseActivity</code>)</div>
</li>
<li class="level1"><div class="li"> <strong>Superclass</strong>: <code>com.jme3.app.AndroidHarness</code></div>
</li>
</ul>

<p>
This will create a new activity class. In the resulting file, create a default constructor and add the following code:
</p>
<pre class="code java"><span class="kw1">public</span> JMEclipseActivity<span class="br0">(</span><span class="br0">)</span>
<span class="br0">{</span>
	<span class="co1">// Set the application class to run</span>
	appClass <span class="sy0">=</span> <span class="st0">"com.jme3.test.MyGame"</span><span class="sy0">;</span>
 
	<span class="co1">// Try ConfigType.FASTEST; or ConfigType.LEGACY if you have problems</span>
	eglConfigType <span class="sy0">=</span> ConfigType.<span class="me1">BEST</span><span class="sy0">;</span>
 
	<span class="co1">// Exit Dialog title &amp; message</span>
	exitDialogTitle <span class="sy0">=</span> <span class="st0">"Quit game?"</span><span class="sy0">;</span>
	exitDialogMessage <span class="sy0">=</span> <span class="st0">"Do you really want to quit the game?"</span><span class="sy0">;</span>
 
	<span class="co1">// Choose screen orientation</span>
	screenOrientation <span class="sy0">=</span> ActivityInfo.<span class="me1">SCREEN_ORIENTATION_LANDSCAPE</span><span class="sy0">;</span>
 
	<span class="co1">// Invert the MouseEvents X (default = true)</span>
	mouseEventsInvertX <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
 
	<span class="co1">// Invert the MouseEvents Y (default = true)</span>
	mouseEventsInvertY <span class="sy0">=</span> <span class="kw2">true</span><span class="sy0">;</span>
<span class="br0">}</span></pre>

<p>
</p><p></p><div class="notetip">Pay close attention to the values above; <code>appClass</code> MUST be the full package + class name of the class in your base project that extends <code>SimpleApplication</code> (for advanced users, this is actually a subclass of <code>com.jme3.app.Application</code>).
</div>


</div>
<!-- EDIT9 SECTION "Android Project" [9528-14983] -->
<h3 class="sectionedit10" id="running1">Running</h3>
<div class="level3">

<p>
Running your Android project is just like <a href="http://developer.android.com/tools/building/building-eclipse.html" class="urlextern" title="http://developer.android.com/tools/building/building-eclipse.html" rel="nofollow">running any other Android project</a>. Assuming you've set up your build path correctly as instructed above, your application should deploy to any device/emulator and run as expected.
</p>

</div>
<!-- EDIT10 SECTION "Running" [14984-15296] -->
<h3 class="sectionedit11" id="packaging_deploying">Packaging / Deploying</h3>
<div class="level3">

<p>
Packaging your Android project is too vast to entirely cover in this guide. As this step is different for each project, I will simply link to this guide to <a href="http://developer.android.com/tools/publishing/app-signing.html" class="urlextern" title="http://developer.android.com/tools/publishing/app-signing.html" rel="nofollow">signing and exporting your APK</a> as it outlines the most common steps to exporting you Android application to be uploaded directly to Google Play (fmly. App Market).
</p>

</div>
<!-- EDIT11 SECTION "Packaging / Deploying" [15297-15717] -->
<h2 class="sectionedit12" id="native_jni_ndk_project">Native (JNI + NDK) Project</h2>
<div class="level2">

<p>
<strong>Prerequisites</strong>:
</p>
<ul>
<li class="level1"><div class="li"> JME3 Base Project created (as described above)</div>
</li>
<li class="level1"><div class="li"> <a href="http://www3.ntu.edu.sg/home/ehchua/programming/howto/EclipseCpp_HowTo.html" class="urlextern" title="http://www3.ntu.edu.sg/home/ehchua/programming/howto/EclipseCpp_HowTo.html" rel="nofollow">Eclipse CDT plugin</a> installed</div>
</li>
<li class="level1"><div class="li"> At least one configured toolchain for compiling on desktop platforms (Cygwin/MinGW/MSVC/GCC/etc.)</div>
</li>
<li class="level1"><div class="li"> Familiarity with JNI and how native libraries are included in a Java application's architecture (this section will assume you do)</div>
</li>
<li class="level1"><div class="li"> JDK for Java 6 or above</div>
</li>
</ul>

<p>
<strong>If additionally building for Android</strong>:
</p>
<ul>
<li class="level1"><div class="li"> Android SDK downloaded and the Android 8 (2.2) target installed (higher <abbr title="Application Programming Interface">API</abbr> versions work too but may limit compatibility when deploying)</div>
</li>
<li class="level1"><div class="li"> Android NDK downloaded</div>
</li>
<li class="level1"><div class="li"> Optional: <a href="http://tools.android.com/recent/usingthendkplugin" class="urlextern" title="http://tools.android.com/recent/usingthendkplugin" rel="nofollow">NDK Eclipse plugin</a> installed (although I haven't seen a real need for it quite yet - it's mainly for building/launching native Activities)</div>
</li>
</ul>

<p>
</p><p></p><div class="notewarning">It should be mentioned that this section will not go into C/C++ best practices, sample code, or any details about the inner workings of JNI; instead, this section simply shows you how to set up the environment/configurations to create a near-seamless build environment for including your native code in both your base project as well as your Android project (if you've created one).
</div>


<p>
Building JNI is actually quite straightforward (assuming you know how the C/C++ build process works). Even for Android, the NDK provides a slick system for building/including your compiled binaries in your project.
</p>

<p>
First, create a new C/C++ project by going to <em>File → New → Project… → C/C++ → C++ Project</em> and clicking <em>Next</em>, giving it a name (we'll use <code>JMEclipse-Native</code>), expanding <em>Shared Library</em> and selecting <em>Empty Project</em>, then selecting a toolchain (select the most appropriate for compiling on your immediate desktop/platform, even if you plan on compiling for Android). Click <em>Finish</em>.
</p>

<p>
Next, we need to configure our build settings. Right click the native project, click <em>Properties</em> and go to <em>C/C++ Build → Settings</em>. Select the <em>Build Artifact</em> tab, ensure the drop down menu says <em>Shared Library</em>, and change the <em>Artifact name</em> field to what you want to call your eventual JNI module.
</p>

<p>
</p><p></p><div class="notewarning">What you call your artifact is VERY important to how Java loads your library. For instance, linux dynamic library (.SO) objects require that the library have the “lib” prefix. Keep this in mind when specifying an artifact name.
</div>


<p>
If you plan on building for Android, you must include an Android makefile in your project. In order for the build process to be as seamless as possible, this guide sets it up unlike most tutorials instruct.
</p>

<p>
To do this, simply create a new file in your native project called <code>Android.mk</code> and <a href="http://www.kandroid.org/ndk/docs/ANDROID-MK.html" class="urlextern" title="http://www.kandroid.org/ndk/docs/ANDROID-MK.html" rel="nofollow">set it up accordingly</a>.
</p>

<p>
</p><p></p><div class="noteimportant">Even though the native project is not the Android project's directory, keep the <code>LOCAL_PATH</code> variable set to <code>my-dir</code>. This is important!
</div>


<p>
Next, we need to create a configuration for the Android target.
</p>

<p>
</p><p></p><div class="noteclassic">This step is only relevant/possible if you have the NDK Eclipse plugin installed. Otherwise, you will need to install awk/make (using Cygwin if on Windows) and build through the command line manually.
</div>


<p>
To do this, right click your native project, click <em>Properties</em>, and go to <em>C/C++ Build → Tool Chain Editor</em>. For the configuration, click <em>Manage Configurations…</em> and create new configuration(s) based on the current default configurations, putting “Android” in the name. Lastly, click <em>OK</em>.
</p>

<p>
For each of the Android configurations you just created, select them in the <em>Configuration</em> drop down menu, set <em>Current toolchain</em> to <em>Android GCC</em>, set <em>Current builder</em> to <em>Android Builder</em>, then click <em>Select Tools…</em>, remove everything from the right side and replace the last item with <em>Android GCC Compiler</em>. Click <em>Apply</em> and then <em>OK</em>.
</p>

<p>
After the toolchains have been set up, go to <em>C/C++ Build</em> and select the <em>Builder Settings</em> tab. For each of the Android configurations, select them in the <em>Configuration</em> drop down menu and change the <em>Build directory</em> to the Android project directory by clicking <em>Workspace…</em> and selecting the Android project (in our case it'd be <code>JMEclipse-Android</code>).
</p>

<p>
The last step in the Android setup is to create a symlink called <code>jni</code> (case sensitive) inside your Android project root that points to the root of your native project:
</p>
<ul>
<li class="level1"><div class="li"> <strong>Windows</strong>: CMD prompt → <code>cd path\to\Android\project</code> → <code>mklink /J jni path\to\native\project</code></div>
</li>
<li class="level1"><div class="li"> <strong>Linux/Mac</strong>: Terminal → <code>cd path/to/Android/project</code> → <code>ln -sv path/to/native/project jni</code></div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">What this has essentially done is created a separate project for C/C++ building while tricking the Android project into thinking the source files are located directly in the Android project itself. With this configuration scheme, you can easily build regular shared libraries for desktop platforms as well as build/install the Android libraries using the NDK without the need to have a copy of the source code inside of the <code>jni</code> folder of an Android project. By setting the workspace for the Android builder and creating a link, it executes the NDK builder inside your Android project while serving the source files as if they existed in the <code>jni</code> folder.
</div>


<p>
Lastly, some additional include paths need to be added. Within the properties window, go to <em>C/C++ General → Paths and Symbols</em> and select the <em>Includes</em> tab.
</p>

<p>
Under <em>Languages</em>, select <em>GNU C++</em> (or the correct C++ equivalent) and then <em>Add…</em>. Specify the absolute path to your JDK's <code>include</code> folder, check <em>Add to all configurations</em>, and hit <em>OK</em>.
</p>

<p>
</p><p></p><div class="notetip">For Windows platforms, repeat the above step for the <code>win32</code> directory within the JDK's <code>include</code> folder.
</div>


<p>
After hitting <em>OK</em>, you are now set to write your JNI code.
</p>

</div>
<!-- EDIT12 SECTION "Native (JNI + NDK) Project" [15718-21696] -->
<h3 class="sectionedit13" id="building">Building</h3>
<div class="level3">

<p>
Building your native project is fairly straightforward.
</p>

<p>
First, right click the native project, go to <em>Build Configurations</em>, select the configuration you want to build, and then right click the native project again and select <em>Build Project</em>. Short of packaging, that's all there is to it.
</p>

</div>
<!-- EDIT13 SECTION "Building" [21697-22011] -->
<h3 class="sectionedit14" id="packaging_deploying1">Packaging / Deploying</h3>
<div class="level3">

<p>
Packaging and deploying your native libraries is a two-sided topic. For Android, the NDK build script installs these for you, and they are packaged directly into the APK. For desktop applications, however, there are a multitude of ways to package your libraries - all of which are too vast to be included in this guide.
</p>

<p>
These libraries, however, are simply JNI libraries and should be loaded as such. A simple web search will explain how JNI works and how to load these libraries.
</p>

</div>
<!-- EDIT14 SECTION "Packaging / Deploying" [22012-] -->
