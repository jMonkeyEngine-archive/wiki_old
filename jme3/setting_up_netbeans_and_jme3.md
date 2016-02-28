---
title: Setting up JME3 in Netbeans 6.x
---
<h1 class="sectionedit1" id="setting_up_jme3_in_netbeans_6x">Setting up JME3 in Netbeans 6.x</h1>
<div class="level1">

<p>
For development with the jMonkeyEngine 3, we recommend to use the jMonkeyEngine <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a>.
</p>

<p>
Alternatively, you can use your favorite IDE: In this tutorial we show how to download and set up the latest nightly build of the jMonkeyEngine 3 for use with the NetBeans IDE. Instructions for <a href="/jme3/setting_up_jme3_in_eclipse.html" class="wikilink1" title="jme3:setting_up_jme3_in_eclipse">Eclipse</a> are also available.
</p>

<p>
</p><p></p><div class="noteimportant">Note that the jMonkeyEngine SDK is built in top of the NetBeans Platform, and is identical to the NetBeans IDE for Java (plus some unique NetBeans plugins). Basically it's redundant and unnecessary to set up jME for NetBeans – but if you want to, it's easily possible. 
</div>


</div>
<!-- EDIT1 SECTION "Setting up JME3 in Netbeans 6.x" [1-694] -->
<h2 class="sectionedit2" id="downloading_jme3">Downloading jME3</h2>
<div class="level2">

<p>
The currently available JAR binaries are the nightly builds. 
</p>
<ol>
<li class="level1"><div class="li"> Download the most recent zipped build from <a href="http://nightly.jmonkeyengine.org/" class="urlextern" title="http://nightly.jmonkeyengine.org/" rel="nofollow">http://nightly.jmonkeyengine.org/</a></div>
</li>
<li class="level1"><div class="li"> Unzip the file and save it as <code>jME3_xx-xx-2010</code> in your NetBeansProjects directory. You should see the following files and directories:</div>
<ol>
<li class="level2"><div class="li"> <code>lib/</code> – The jMonkeyEngine binaries and libraries. (Don't remove.)</div>
</li>
<li class="level2"><div class="li"> <code>TestChooser.exe</code> – Run this file to see various feature demos. (optional)</div>
</li>
<li class="level2"><div class="li"> <code>javadoc/</code> – jME3 <abbr title="Application Programming Interface">API</abbr> documentation. (optional)</div>
</li>
</ol>
</li>
</ol>

</div>
<!-- EDIT2 SECTION "Downloading jME3" [695-1228] -->
<h2 class="sectionedit3" id="creating_a_project">Creating a Project</h2>
<div class="level2">

<p>
In NetBeans, choose File &gt; New Project, select Java &gt; Java Application, click Next.
</p>
<ul>
<li class="level1"><div class="li"> Project Name: HelloJME3</div>
</li>
<li class="level1"><div class="li"> Project Location: ~/NetBeansProjects</div>
</li>
<li class="level1"><div class="li"> Create main() Class: No</div>
</li>
<li class="level1"><div class="li"> Set as Main Project: Yes.</div>
</li>
<li class="level1"><div class="li"> Click Finish</div>
</li>
</ul>

<p>
The new project appears in the Projects window.
</p>

</div>
<!-- EDIT3 SECTION "Creating a Project" [1229-1539] -->
<h2 class="sectionedit4" id="setting_up_dependencies">Setting up Dependencies</h2>
<div class="level2">

<p>
Your project depends on the jMonkeyEngine libraries and needs to know where they are.
</p>
<ol>
<li class="level1"><div class="li"> In the Projects window, right-click the project's Libraries node and choose “Add JAR/Folder”.</div>
</li>
<li class="level1"><div class="li"> In the “Add JAR/Folder” dialog, browse to the <code>NetBeansProjects/jME3_xx-xx-2010</code> directory.</div>
</li>
<li class="level1"><div class="li"> Select all JARs in <code>lib/</code> and click Select.</div>
</li>
</ol>

<p>
The necessary libraries are now on the classpath and should appear in the Libraries list.
</p>

</div>
<!-- EDIT4 SECTION "Setting up Dependencies" [1540-2000] -->
<h2 class="sectionedit5" id="optionalconfiguring_the_javadoc_popups_in_netbeans">Optional: Configuring the JavaDoc Popups in NetBeans</h2>
<div class="level2">

<p>
Configuring Javadoc popups for jme3 classes in NetBeans can be very helpful during the development phase of your game. 
</p>
<ol>
<li class="level1"><div class="li"> In the HelloJME3 project</div>
<ol>
<li class="level2"><div class="li"> Right-click the Libraries node and choose Properties from the context menu</div>
</li>
<li class="level2"><div class="li"> Select the jMonkeyEngine3.jar library entry from the list and click Edit.</div>
<ol>
<li class="level3"><div class="li"> Javadoc: Browse to JME3's <code>javadoc</code> directory and click select.</div>
</li>
<li class="level3"><div class="li"> Sources: Browse to JME3's <code>src</code>directory and click select.</div>
</li>
</ol>
</li>
<li class="level2"><div class="li"> Click OK.</div>
</li>
</ol>
</li>
</ol>

<p>
Open a class of your HelloJME3 project, place the caret into a jme3 class, and press ctrl-space to see the javadoc popup, as well as code-completion.
</p>

</div>
<!-- EDIT5 SECTION "Optional: Configuring the JavaDoc Popups in NetBeans" [2001-2688] -->
<h2 class="sectionedit6" id="build_run_tips_in_netbeans">Build &amp; Run Tips in NetBeans</h2>
<div class="level2">

<p>
How to build and run in NetBeans:
</p>
<ul>
<li class="level1"><div class="li"> Clean and build the whole project by pressing Shift-F11.</div>
</li>
<li class="level1"><div class="li"> Run any file that is open in the editor and has a main() class by pressing Shift-F6.</div>
</li>
<li class="level1"><div class="li"> Run the Main class of the project by pressing F6.</div>
</li>
</ul>

<p>
Tips for configuring the main class in NetBeans:
</p>
<ul>
<li class="level1"><div class="li"> Right-click the HelloJME3 project and choose “Set as main project”. Now you can use the toolbar buttons (clean&amp;build, run, debug, etc) to control this project.</div>
</li>
<li class="level1"><div class="li"> Right-click the HelloJME3 project and choose Properties. Go to the Run section. </div>
</li>
<li class="level1"><div class="li"> Under Main Class, specify the class that will be executed when you run the whole project. For now, enter <code>hello.HelloJME3</code>.</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Build & Run Tips in NetBeans" [2689-3398] -->
<h2 class="sectionedit7" id="writing_a_simpleapplication">Writing a SimpleApplication</h2>
<div class="level2">

<p>
You can now continue to write <a href="/jme3/beginner/hello_simpleapplication.html" class="wikilink1" title="jme3:beginner:hello_simpleapplication">your first jme3 application</a>!
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>
</span></div>

</div>
<!-- EDIT7 SECTION "Writing a SimpleApplication" [3399-] -->
