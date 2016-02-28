---
title: Troubleshooting jMonkeyEngine3 SDK
---
<h2 class="sectionedit1" id="troubleshooting_jmonkeyengine3_sdk">Troubleshooting jMonkeyEngine3 SDK</h2>
<div class="level2">

</div>
<!-- EDIT1 SECTION "Troubleshooting jMonkeyEngine3 SDK" [1-47] -->
<h3 class="sectionedit2" id="graphics_card_driver">Graphics Card Driver</h3>
<div class="level3">

<p>
<strong>On Windows and Linux make sure you have the latest driver installed. Make sure its the one supplied by the card manufacturer and not just the <abbr title="Operating System">OS</abbr>-default one.</strong> On OSX, make sure you have the latest update for your MacOS.
</p>

</div>
<!-- EDIT2 SECTION "Graphics Card Driver" [48-301] -->
<h3 class="sectionedit3" id="stability_graphics_issues">Stability / Graphics issues</h3>
<div class="level3">

<p>
On some Linux and Windows systems, the SDK might perform unstable and quit with native VM crashes or “x errors”. There are a few things one can try to remedy those issues.
</p>

</div>

<h4 id="heavyweight_canvas">Heavyweight Canvas</h4>
<div class="level4">

<p>
First of all theres the new “OpenGL” settings page in the SDK global settings where you can enable the “heavyweight” canvas, which solved some issues for some people. The settings panel can be found under Tools→Options on Windows and Linux and in the main menu (or by pressing Apple-Comma) for MacOSX.
</p>

<p>
If you cannot start the SDK, edit the file <code>config/Preferences/com/jme3/gde/core.properties</code> in the SDK settings folder (see above). If it doesn't exist, create the file including all folders. Add the line <code>use_lwjgl_canvas=true</code>. To try OpenGL1 compatibility mode (works for both canvas settings) add <code>use_opengl_1=true</code>.
</p>

</div>

<h4 id="look_and_feel">Look and Feel</h4>
<div class="level4">

<p>
The <abbr title="Operating System">OS</abbr>-built-in look and feel might cause issues, you can change the LAF by using the appropriate command line switch (or add it to the [app folder]/etc/jmonkeyplatform.conf file, without the “- -” prefix).
</p>
<pre class="code">--laf javax.swing.plaf.nimbus.NimbusLookAndFeel</pre>

<p>
or alternatively
</p>
<pre class="code">--laf javax.swing.plaf.metal.MetalLookAndFeel</pre>

</div>

<h4 id="compiz">Compiz</h4>
<div class="level4">

<p>
Compiz on Linux might cause issues, if you set its rendering quality to “medium” these should go away.
* Appearance→Set Special effects to → “Medium”
</p>

</div>
<!-- EDIT3 SECTION "Stability / Graphics issues" [302-1713] -->
<h3 class="sectionedit4" id="updating_problems">Updating problems</h3>
<div class="level3">

<p>
If you have problems updating the SDK, try deleting all files from <code>jmonkeyplatform/update/download</code> and/or <code>[settings folder]/update/download</code> depending on your system (see below for the settings folder location).
</p>

<p>
If you are on Linux, check if the user you run the SDK with has access to the files in <code>jmonkeyplatform/jdk/bin</code> and that they are executable.
</p>

</div>
<!-- EDIT4 SECTION "Updating problems" [1714-2106] -->
<h3 class="sectionedit5" id="freezing_performance_problems">Freezing / Performance problems</h3>
<div class="level3">

<p>
If the SDK starts to become sluggish and / or slow or you get unexpected freezes of the application, you can try deleting the cache folder at var/cache in the settings folder (see below for the location of the settings folder). Do this while the SDK is not running, then restart the SDK.
</p>

</div>
<!-- EDIT5 SECTION "Freezing / Performance problems" [2107-2436] -->
<h3 class="sectionedit6" id="preferences_and_settings">Preferences and Settings</h3>
<div class="level3">

<p>
To completely remove and/or reinstall the SDK it is vital that the settings folder is deleted too. The location can be seen through the “about” menu and is as following for the different <abbr title="Operating System">OS</abbr>'s:
</p>
<ul>
<li class="level1"><div class="li"> Windows: <code>C:\Users\&lt;username&gt;\AppData\Roaming\.jmonkeyplatform</code></div>
</li>
<li class="level1"><div class="li"> Windows (alt): <code>C:\Users\&lt;username&gt;\.jmonkeyplatform\</code></div>
</li>
<li class="level1"><div class="li"> MacOSX: <code>/Users/&lt;username&gt;/Library/Application Support/jmonkeyplatform</code></div>
</li>
<li class="level1"><div class="li"> Ubuntu:  <code>/home/&lt;username&gt;/.jmonkeyplatform</code></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Preferences and Settings" [2437-2925] -->
<h3 class="sectionedit7" id="log">Log</h3>
<div class="level3">

<p>
To see or post the error output of the SDK in the forum, you can find the log of the application in the settings folder above too, the file is called <code>var/log/messages.log</code>
</p>

</div>
<!-- EDIT7 SECTION "Log" [2926-3115] -->
<h3 class="sectionedit8" id="getting_error_messages_and_reporting_issues">Getting error messages and reporting issues</h3>
<div class="level3">

<p>
When an exception happens in the SDK, a small warning sign appears in the lower right corner of the main window. Double-click it to open a window that allows you to see the exception stack trace. When posting about issues in the forum, always post the stack trace along with a description of what happens and how it can be reproduced.
</p>

</div>
<!-- EDIT8 SECTION "Getting error messages and reporting issues" [3116-3505] -->
<h3 class="sectionedit9" id="specifying_the_jdk_location">Specifying the JDK location</h3>
<div class="level3">

<p>
You can install another JDK for use with the jMonkey SDK. You then have to specify the location manually.
</p>
<ol>
<li class="level1"><div class="li"> Go to your jMonkeyEngine SDK installation directory. <br />
Mac users right-click jMonkeyApplication.app (which actually is a directory) in the Finder and select “Show package contents”. </div>
</li>
<li class="level1"><div class="li"> Navigate to the <code>etc</code> directory. <br />
Mac users navigate to <code>Contents/Resources/jmonkeyplatform/etc/</code>.</div>
</li>
<li class="level1"><div class="li"> Open the file <code>jmonkeyplatform.conf</code> in a text editor.</div>
</li>
<li class="level1"><div class="li"> Change the following line and enter the path to the JDK: <pre class="code">jdkhome="/path/to/jdk"</pre>
</div>
</li>
</ol>

</div>
<!-- EDIT9 SECTION "Specifying the JDK location" [3506-4106] -->
<h3 class="sectionedit10" id="freezing_at_startup">Freezing at startup</h3>
<div class="level3">

<p>
If you're behind a proxy or special network settings, try :
</p>
<pre class="code">1. disable your network connection
2. launch jme sdk (may wait 30s/1min for timeout)
3. go into tools-&gt;options-&gt;general
4. setup “manual proxy settings” (for some reason the “Use System Proxy Settings” option doesn't work on some Linux distributions)</pre>

<p>
<a href="http://hub.jmonkeyengine.org/forum/topic/jme-sdk-stalls-on-startup/" class="urlextern" title="http://hub.jmonkeyengine.org/forum/topic/jme-sdk-stalls-on-startup/" rel="nofollow">discussion</a>
</p>

</div>
<!-- EDIT10 SECTION "Freezing at startup" [4107-4550] -->
<h3 class="sectionedit11" id="known_issues">Known Issues</h3>
<div class="level3">

<p>
For a list of known issues and possible workarounds see the following link:
<a href="http://code.google.com/p/jmonkeyengine/issues/list?can=2&amp;q=label%3AProduct-Platform+Type%3DDefect+&amp;colspec=ID+Type+Status+Component+Priority+Product+Milestone+Owner+Summary&amp;cells=tiles" class="urlextern" title="http://code.google.com/p/jmonkeyengine/issues/list?can=2&amp;q=label%3AProduct-Platform+Type%3DDefect+&amp;colspec=ID+Type+Status+Component+Priority+Product+Milestone+Owner+Summary&amp;cells=tiles" rel="nofollow">List of known issues on googlecode</a>
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/faq.html" class="wikilink1" title="tag:faq" rel="tag">faq</a>
</span></div>

</div>
<!-- EDIT11 SECTION "Known Issues" [4551-] -->
