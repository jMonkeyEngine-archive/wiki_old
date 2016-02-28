---
title: jMonkeyEngine SDK: Log Files
---
<h1 class="sectionedit1" id="jmonkeyengine_sdklog_files">jMonkeyEngine SDK: Log Files</h1>
<div class="level1">

<p>
You find the jMonkeyEngine SDK log file in <code>/dev/var/log/messages.log</code> in the jMonkeyEngine SDK preferences folder. You can learn the location of the preferences folder in the “About” screen of the jMonkeyEngine SDK under the label <strong>Userdir</strong>. 
</p>
<ul>
<li class="level1"><div class="li"> Windows: <code>C:\Documents and Settings\YOUR_NAME\.jmonkeyplatform\</code></div>
</li>
<li class="level1"><div class="li"> Linux: <code>/home/YOUR_NAME/.jmonkeyplatform/</code></div>
</li>
<li class="level1"><div class="li"> Mac <abbr title="Operating System">OS</abbr>: <code>/Users/YOUR_NAME/Library/Application Support/jmonkeyplatform/</code></div>
</li>
</ul>

<p>
The message log contains all paths and <a href="/jme3/advanced/read_graphic_card_capabilites.html" class="wikilink1" title="jme3:advanced:read_graphic_card_capabilites">capabilities</a> used in your development system, and also warnings, e.g. if a plugin crashed.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine SDK: Log Files" [1-676] -->
<h2 class="sectionedit2" id="example_log">Example Log</h2>
<div class="level2">
<pre class="code">&gt;Log Session: Saturday, September 24, 2011 10:45:30 AM CEST
&gt;System Info: 
  Product Version         = jMonkeyPlatform Alpha-4
  Operating System        = Mac OS X version 10.6.8 running on i386
  Java; VM; Vendor        = 1.6.0_26; Java HotSpot(TM) Client VM 20.1-b02-384; Apple Inc.
  Runtime                 = Java(TM) SE Runtime Environment 1.6.0_26-b03-384-10M3425
  Java Home               = /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
  System Locale; Encoding = de_DE (jmonkeyplatform); MacRoman
  Home Directory          = /Users/joemonkey
  Current Directory       = /
  User Directory          = /Users/joemonkey/Library/Application Support/jmonkeyplatform/dev
  Installation            = /Applications/jmonkeyplatform.app/Contents/Resources/jmonkeyplatform/jmonkeyplatform
  ...</pre>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/file.html" class="wikilink1" title="tag:file" rel="tag">file</a>
</span></div>

</div>
<!-- EDIT2 SECTION "Example Log" [677-] -->
