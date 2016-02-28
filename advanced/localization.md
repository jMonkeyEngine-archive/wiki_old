---
title: Localizing jME 3 Games
---
<h1 class="sectionedit1" id="localizing_jme_3_games">Localizing jME 3 Games</h1>
<div class="level1">

</div>
<!-- EDIT1 SECTION "Localizing jME 3 Games" [1-38] -->
<h2 class="sectionedit2" id="scope">Scope</h2>
<div class="level2">

<p>
Localizing an application can mean several things: 
</p>
<ul>
<li class="level1"><div class="li"> At minimum you translate all messages and dialogs in the user interface to your target languages.</div>
</li>
<li class="level1"><div class="li"> You should also translate the “read me”, help, and other documentation.</div>
</li>
<li class="level1"><div class="li"> Also translating web content related to the application makes sure international users find out about your localized game.</div>
</li>
<li class="level1"><div class="li"> If you go the whole way of internationalization, you also “translate” metaphors in icons or symbols used. <br />
E.g. For localizations to right-to-left languages, you must also adjust the whole flow of the UI (order of menus and buttons).</div>
</li>
</ul>

<p>
There are tools that assist you with localizing Java Swing GUIs. jME3 applications do not typically have a Swing <abbr title="Graphical User Interface">GUI</abbr>, so those tools are not of much help. Just stick to the normal Java rules about using Bundle Properties:
</p>

</div>
<!-- EDIT2 SECTION "Scope" [39-879] -->
<h2 class="sectionedit3" id="preparing_the_localization">Preparing the Localization</h2>
<div class="level2">

<p>
<strong>Tip:</strong> The jMonkeyEngine SDK supports opening and editing Bundle.properties files. Also note the Tools &gt; Localization menu.
</p>

<p>
To prepare the application for localization, you have to first identify all hard-coded messages.
</p>
<ol>
<li class="level1"><div class="li"> Find every line in your jME3 game where you hard-coded message strings, e.g. <br />
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">print</span><span class="br0">(</span><span class="st0">"Hello World!"</span><span class="br0">)</span><span class="sy0">;</span>
UiText.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Score: "</span><span class="sy0">+</span>score<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Create one file named <code>Bundle.properties</code> in each directory where there are Java file that contain messages.</div>
</li>
<li class="level1"><div class="li"> For every hard-coded message, you add one line to the <code>Bundle.properties</code> file: First specify a unique key that identifies this string; then an equal sign; and the literal string itself. <br />
<pre class="code">greeting=Hello World!
score.display=Score: </pre>
</div>
</li>
<li class="level1"><div class="li"> In the source code, replace every occurence of a hard-coded message with the appropriate Resource Bundle call to its unique key: <pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">print</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+resourcebundle"><span class="kw3">ResourceBundle</span></a>.<span class="me1">getBundle</span><span class="br0">(</span><span class="st0">"Bundle"</span><span class="br0">)</span>.<span class="me1">getString</span><span class="br0">(</span><span class="st0">"greeting"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
UiText.<span class="me1">setText</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+resourcebundle"><span class="kw3">ResourceBundle</span></a>.<span class="me1">getBundle</span><span class="br0">(</span><span class="st0">"Bundle"</span><span class="br0">)</span>.<span class="me1">getString</span><span class="br0">(</span><span class="st0">"score.display"</span><span class="br0">)</span><span class="sy0">+</span>score<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
The language used in the Bundle.properties files will be the default language for your game.
</p>

</div>
<!-- EDIT3 SECTION "Preparing the Localization" [880-2088] -->
<h2 class="sectionedit4" id="translating_the_messages">Translating the Messages</h2>
<div class="level2">

<p>
Each additional language comes in a set of files that is marked with a (usually) two-letter suffix. Common locales are de for German, en for English, fr for French, ja for Japanese, pt for Portuguese, etc.
</p>

<p>
To translate the messages to another language, for example, German:
</p>
<ol>
<li class="level1"><div class="li"> Make a copy of the <code>Bundle.properties</code> files.</div>
</li>
<li class="level1"><div class="li"> Name the copy <code>Bundle_de.properties</code> for German. Note the added suffix _de.</div>
</li>
<li class="level1"><div class="li"> Translate all strings (text on the right side of the equal sign) in the <code>Bundle_de.properties</code> to German. <pre class="code">greeting=Hallo Welt!
score.display=Spielstand: </pre>

<p>
 <strong>Important:</strong> Do not modify any of the keys (text to the left of the equal sign)!
</p>
</div>
</li>
<li class="level1"><div class="li"> To test the German localization, start the application from the command line with <code>-Duser.language=de</code>. Note the parameter <code>de</code>.</div>
</li>
</ol>

<p>
<strong>Tip:</strong> In the jMonkeyEngine SDK, you set this VM Option in the Project properties under Run. Here you can also save individual run configuraions for each language you want to test.
</p>

<p>
To get the full list of language suffixes use 
</p>
<pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+arrays"><span class="kw3">Arrays</span></a>.<span class="me1">toString</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+locale"><span class="kw3">Locale</span></a>.<span class="me1">getISOLanguages</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT4 SECTION "Translating the Messages" [2089-3243] -->
<h2 class="sectionedit5" id="which_strings_not_to_translate">Which Strings Not to Translate</h2>
<div class="level2">

<p>
<strong>Important:</strong> In the Bundle.properties file, do not include any strings that are asset paths, node or geometry names, input mappings, or material layers.
</p>
<ul>
<li class="level1"><div class="li"> Keep material layers: <pre class="code java">mat.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, tex<span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Keep paths: <pre class="code java">teapot <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Teapot/Teapot.obj"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Keep geometry and node names: <pre class="code java">Geometry thing<span class="sy0">=</span><span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"A thing"</span>, mesh<span class="br0">)</span><span class="sy0">;</span>
Node vehicle <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"Vehicle"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
<li class="level1"><div class="li"> Keep mappings: <pre class="code java">inputManager.<span class="me1">addMapping</span><span class="br0">(</span><span class="st0">"Shoot"</span>, trigger<span class="br0">)</span><span class="sy0">;</span>
inputManager.<span class="me1">addListener</span><span class="br0">(</span>actionListener, <span class="st0">"Shoot"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>

<p>
Only localize messages and UI text!
</p>

</div>
<!-- EDIT5 SECTION "Which Strings Not to Translate" [3244-3918] -->
<h2 class="sectionedit6" id="common_localization_problems">Common Localization Problems</h2>
<div class="level2">

<p>
Typical problems include:
</p>
<ul>
<li class="level1"><div class="li"> Localized strings will be of vastly different lengths and will totally break your UI layout. ⇒ Test every localization.</div>
</li>
<li class="level1"><div class="li"> Strings with variable text or numbers don't work the same in different languages. ⇒ Either work in grammatical cases/numbers/gender for each language, or use <a href="http://www.gnu.org/software/gettext/manual/gettext.html#Plural-forms" class="urlextern" title="http://www.gnu.org/software/gettext/manual/gettext.html#Plural-forms" rel="nofollow">gettext</a> or <a href="http://userguide.icu-project.org/formatparse/messages" class="urlextern" title="http://userguide.icu-project.org/formatparse/messages" rel="nofollow">ICU4J</a>.</div>
</li>
<li class="level1"><div class="li"> The localizer only sees the strings, without any context. E.g. does “Search History” mean “display the history of searches”, or “search through the history”? ⇒ Use clear key labels. Work closely with the localizers if they require extra info, and add that info as comments to the translation file.</div>
</li>
<li class="level1"><div class="li"> Broken international characters ⇒ Make sure the files are saved with the same character encoding as the font file(s) you're using. Nowadays, that usually means UTF-8 since font files tend to come for Unicode.</div>
</li>
<li class="level1"><div class="li"> Missing international characters ⇒ Make sure that there's a glyph for every needed character in your font, either by using more complete font files or by having the translation changed.</div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Common Localization Problems" [3919-5131] -->
<h2 class="sectionedit7" id="more_documentation">More Documentation</h2>
<div class="level2">

<p>
<a href="http://java.sun.com/developer/technicalArticles/Intl/ResourceBundles/" class="urlextern" title="http://java.sun.com/developer/technicalArticles/Intl/ResourceBundles/" rel="nofollow">http://java.sun.com/developer/technicalArticles/Intl/ResourceBundles/</a>
</p>

<p>
<a href="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Localisation" class="urlextern" title="http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Localisation" rel="nofollow">http://sourceforge.net/apps/mediawiki/nifty-gui/index.php?title=Localisation</a>
</p>

</div>
<!-- EDIT7 SECTION "More Documentation" [5132-] -->
