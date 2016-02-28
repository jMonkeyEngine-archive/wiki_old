---
title: Logging and Monitoring
---
<h1 class="sectionedit1" id="logging_and_monitoring">Logging and Monitoring</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Logging and Monitoring" [1-38] -->
<h2 class="sectionedit2" id="logging_like_a_newbie">Logging Like a Newbie</h2>
<div class="level2">

<p>
Many developers just use <code>System.out.println()</code> to print diagnostic strings to the terminal. The problem with that is that before the release, you have to go through all your code and make certain you removed all these <code>println()</code> calls. You do not want your customers to see them, and needlessly worry about ominous outdated debugging diagnostics. 
</p>

</div>
<!-- EDIT2 SECTION "Logging Like a Newbie" [39-428] -->
<h2 class="sectionedit3" id="logging_like_a_pro">Logging Like a Pro</h2>
<div class="level2">

<p>
Instead of <code>println()</code>, use the standard Java logger from <code>java.util.logging</code>. It has many advantages for professional game development:
</p>
<ul>
<li class="level1"><div class="li"> You tag each message with its <strong>log level</strong>: Severe error, informative warning, etc.</div>
</li>
<li class="level1"><div class="li"> You can <strong>switch off or on printing of log messages</strong> up to certain log level with just one line of code.</div>
<ul>
<li class="level2"><div class="li"> During development, you would set the log level to <code>fine</code>, because you want all warnings printed.</div>
</li>
<li class="level2"><div class="li"> For the release, you set the log level to only report <code>severe</code> errors, and never print informative diagnostics.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> The logger message string is <strong>localizable</strong> and can use variables. Optimally, you localize all error messages.</div>
</li>
</ul>

<p>
To print comments like a pro, you use the following logger syntax.
</p>
<ol>
<li class="level1"><div class="li"> Declare the logger object once per file. In the following code, replace <code>HelloWorld</code> by the name of the class where you are using this line.<pre class="code java"><span class="kw1">private</span> <span class="kw1">static</span> <span class="kw1">final</span> Logger logger <span class="sy0">=</span> Logger.<span class="me1">getLogger</span><span class="br0">(</span>HelloWorld.<span class="kw1">class</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Declare the info that you want to include in the message. The variables (here <code>a, b, c</code>) can be any printable Java object. <br />
Example: <code>Vector3f a = cam.getLocation();</code> </div>
</li>
<li class="level1"><div class="li"> Put the variables in a new <code>Object</code> array. Refer to the variables as <code>{0},{1},{2}</code> etc in the message string. Variables are numbered in the order you put them into the <code>Object</code> array. </div>
</li>
<li class="level1"><div class="li"> Add the logger line and specify the log level:</div>
<ul>
<li class="level2"><div class="li"> Usecase 1: During debugging, a developer uses a warning to remind himself of a bug:<pre class="code java">logger.<span class="me1">log</span><span class="br0">(</span>Level.<span class="me1">WARNING</span>, <span class="st0">"why is {0} set to {1} again?!"</span>, 
                      <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span>a , b<span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level2"><div class="li"> Usecase 2: For the release, you inform the customer of a problem and how to solve it. <pre class="code java">logger.<span class="me1">log</span><span class="br0">(</span>Level.<span class="me1">SEVERE</span>, <span class="st0">"MyGame error: {0} must not be {1} after {2}! Adjust flux generator settings."</span>, 
                      <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+object"><span class="kw3">Object</span></a><span class="br0">[</span><span class="br0">]</span><span class="br0">{</span>a , b , c<span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
</ol>

<p>
</p><p></p><div class="noteimportant">As you see in the examples, you should phrase potentially “customer facing” errors in a neutral way and offer <em>a reason and a solution</em> for the error (if you don't, it has no value to your customer). If your deveopment team uses WARNINGs as replacement for casual printlns, make sure you deactivate them for the release.
</div>


<p>
More details about <a href="http://download.oracle.com/javase/6/docs/api/java/util/logging/Level.html" class="urlextern" title="http://download.oracle.com/javase/6/docs/api/java/util/logging/Level.html" rel="nofollow">Java log levels</a> here.
</p>

</div>
<!-- EDIT3 SECTION "Logging Like a Pro" [429-2826] -->
<h2 class="sectionedit4" id="switching_the_logger_on_and_off">Switching the Logger on and off</h2>
<div class="level2">

<p>
In the release version you will deactivate the logging output to the terminal.
</p>

<p>
To deactivate the default logger for a release, you set the log level to only report <code>severe</code> messages:
</p>
<pre class="code java">Logger.<span class="me1">getLogger</span><span class="br0">(</span>””<span class="br0">)</span>.<span class="me1">setLevel</span><span class="br0">(</span>Level.<span class="me1">SEVERE</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
During development or a beta test, you can tune down the default logger, and set the log level to only report <code>warning</code>s:
</p>
<pre class="code java">Logger.<span class="me1">getLogger</span><span class="br0">(</span>””<span class="br0">)</span>.<span class="me1">setLevel</span><span class="br0">(</span>Level.<span class="me1">WARNING</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
To activate full logging, e.g. for debugging and testing, use the <code>fine</code> level: 
</p>
<pre class="code java">Logger.<span class="me1">getLogger</span><span class="br0">(</span>””<span class="br0">)</span>.<span class="me1">setLevel</span><span class="br0">(</span>Level.<span class="me1">FINE</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Switching the Logger on and off" [2827-3468] -->
<h2 class="sectionedit5" id="advanced_error_handling">Advanced Error Handling</h2>
<div class="level2">

<p>
When an uncaught exception reaches certain parts of the jME3 system then the default response is to log the error and then exit the application. This is because an error happening every frame will rapidly fill logs with repeated failings and potentially mask or over-write the original cause of the problem or even the application may continue for a while and then suffer other errors caused by the first and make the root cause hard to determine.
</p>

<p>
This behaviour can be partially modified by overriding the method handleError in SimpleApplication, for example to display a custom message to users, or to provide users with information on how to report a bug or even to change the way that the error is logged. 
</p>

</div>
<!-- EDIT5 SECTION "Advanced Error Handling" [3469-] -->
