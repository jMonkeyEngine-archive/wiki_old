---
title: WebStart (JNLP) Deployment
---
<h1 class="sectionedit1" id="webstart_jnlp_deployment">WebStart (JNLP) Deployment</h1>
<div class="level1">

<p>
When you <a href="/sdk/application_deployment.html" class="wikilink1" title="sdk:application_deployment">use the jMonkeyEngine SDK to deploy your application</a>, you can configure the project to build files required for WebStart automatically. If you use another IDE, or work on the command line, use the following tips to set up WebStart correctly:
</p>

</div>
<!-- EDIT1 SECTION "WebStart (JNLP) Deployment" [1-326] -->
<h2 class="sectionedit2" id="problem_statement">Problem Statement</h2>
<div class="level2">

<p>
<strong>Problem:</strong>
</p>

<p>
When running under WebStart, jMonkeyEngine may not have permission to extract the native libraries to the current directory. 
</p>

<p>
<strong>Solution: </strong>
</p>

<p>
You can instruct WebStart to load the native libraries itself using the JNLP file, and then instruct jME3 not to try to do so itself.
</p>

</div>
<!-- EDIT2 SECTION "Problem Statement" [327-649] -->
<h2 class="sectionedit3" id="simple_way">Simple way</h2>
<div class="level2">

<p>
You can import the LWJGL JNLP extension directly into your extension, however be aware that your application will break whenever they update their jars. Simply add this line to your JNLP:
</p>
<pre class="code xml"><span class="sc3"><span class="re1">&lt;extension</span> <span class="re0">name</span>=<span class="st0">"lwjgl"</span> <span class="re0">href</span>=<span class="st0">"http://lwjgl.org/webstart/2.7.1/extension.jnlp"</span> <span class="re2">/&gt;</span></span></pre>

</div>
<!-- EDIT3 SECTION "Simple way" [650-963] -->
<h2 class="sectionedit4" id="reliable_way">Reliable way</h2>
<div class="level2">

</div>
<!-- EDIT4 SECTION "Reliable way" [964-989] -->
<h3 class="sectionedit5" id="native_jars">Native jars</h3>
<div class="level3">

<p>
You can download the LWJGL native jars from their site, or to ensure you're using the exact same version as bundled with your jME3 release, make your own:
</p>
<pre class="code">mkdir tmp
cd tmp
jar xfv ../jME3-lwjgl-natives.jar
cd native
for i in *; do
  cd $i
  jar cfv ../../native_$i.jar .
  cd ..
done</pre>

<p>
For Windows:
</p>
<pre class="code">@echo off
md tmp
cd tmp
"%JDK_HOME%\bin\jar" -xfv ..\jME3-lwjgl-natives.jar
cd native
for /D %%i in ("*") do (
  cd %%i
  "%JDK_HOME%\bin\jar" -cfv ..\..\native_%%i%.jar .
  cd ..
)
cd ..</pre>

<p>
Remember to sign all the jar files and move them into the right place from the tmp directory.
</p>

</div>
<!-- EDIT5 SECTION "Native jars" [990-1626] -->
<h3 class="sectionedit6" id="jnlp_file">JNLP file</h3>
<div class="level3">

<p>
Add the following to your JNLP file:
</p>
<pre class="code xml">  <span class="sc3"><span class="re1">&lt;resources</span> <span class="re0">os</span>=<span class="st0">"Windows"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;j2se</span> <span class="re0">version</span>=<span class="st0">"1.4+"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;nativelib</span> <span class="re0">href</span>=<span class="st0">"native_windows.jar"</span><span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;/resources<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;resources</span> <span class="re0">os</span>=<span class="st0">"Linux"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;j2se</span> <span class="re0">version</span>=<span class="st0">"1.4+"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;nativelib</span> <span class="re0">href</span>=<span class="st0">"native_linux.jar"</span><span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;/resources<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;resources</span> <span class="re0">os</span>=<span class="st0">"Mac OS X"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;j2se</span> <span class="re0">version</span>=<span class="st0">"1.4+"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;nativelib</span> <span class="re0">href</span>=<span class="st0">"native_macosx.jar"</span><span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;/resources<span class="re2">&gt;</span></span></span>
  <span class="sc3"><span class="re1">&lt;resources</span> <span class="re0">os</span>=<span class="st0">"SunOS"</span> <span class="re0">arch</span>=<span class="st0">"x86"</span><span class="re2">&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;j2se</span> <span class="re0">version</span>=<span class="st0">"1.4+"</span><span class="re2">/&gt;</span></span>
    <span class="sc3"><span class="re1">&lt;nativelib</span> <span class="re0">href</span>=<span class="st0">"native_solaris.jar"</span><span class="re2">/&gt;</span></span>
  <span class="sc3"><span class="re1">&lt;/resources<span class="re2">&gt;</span></span></span></pre>

</div>
<!-- EDIT6 SECTION "JNLP file" [1627-2158] -->
<h3 class="sectionedit7" id="set_low-permissions_mode">Set low-permissions mode</h3>
<div class="level3">

<p>
In your main() method, if running under WebStart, tell jME3 it is running in a low-permission environment so that it doesn't try to load the natives itself:
</p>
<pre class="code java">  <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span>
  <span class="br0">{</span>
      <span class="kw1">if</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">getProperty</span><span class="br0">(</span><span class="st0">"javawebstart.version"</span><span class="br0">)</span> <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
        JmeSystem.<span class="me1">setLowPermissions</span><span class="br0">(</span><span class="kw2">true</span><span class="br0">)</span><span class="sy0">;</span>
      <span class="br0">}</span></pre>

</div>
<!-- EDIT7 SECTION "Set low-permissions mode" [2159-] -->
