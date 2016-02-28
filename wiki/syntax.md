---
title: Formatting Syntax
---
<h1 class="sectionedit1" id="formatting_syntax">Formatting Syntax</h1>
<div class="level1">

<p>
<a href="http://www.dokuwiki.org/DokuWiki" class="interwiki iw_doku" title="http://www.dokuwiki.org/DokuWiki">DokuWiki</a> supports some simple markup language, which tries to make the datafiles to be as readable as possible. This page contains all possible syntax you may use when editing the pages. Simply have a look at the source of this page by pressing “Edit this page”. If you want to try something, just use the <a href="/playground/playground.html" class="wikilink1" title="playground:playground">playground</a> page. The simpler markup is easily accessible via <a href="http://www.dokuwiki.org/toolbar" class="interwiki iw_doku" title="http://www.dokuwiki.org/toolbar">quickbuttons</a>, too.
</p>

</div>
<!-- EDIT1 SECTION "Formatting Syntax" [1-472] -->
<h2 class="sectionedit2" id="basic_text_formatting">Basic Text Formatting</h2>
<div class="level2">

<p>
DokuWiki supports <strong>bold</strong>, <em>italic</em>, <em class="u">underlined</em> and <code>monospaced</code> texts. Of course you can <strong><em class="u"><em><code>combine</code></em></em></strong> all these.
</p>
<pre class="code">DokuWiki supports **bold**, //italic//, __underlined__ and ''monospaced'' texts.
Of course you can **__//''combine''//__** all these.</pre>

<p>
You can use <sub>subscript</sub> and <sup>superscript</sup>, too.
</p>
<pre class="code">You can use &lt;sub&gt;subscript&lt;/sub&gt; and &lt;sup&gt;superscript&lt;/sup&gt;, too.</pre>

<p>
You can mark something as <del>deleted</del> as well.
</p>
<pre class="code">You can mark something as &lt;del&gt;deleted&lt;/del&gt; as well.</pre>

<p>
<strong>Paragraphs</strong> are created from blank lines. If you want to <strong>force a newline</strong> without a paragraph, you can use two backslashes followed by a whitespace or the end of line.
</p>

<p>
This is some text with some linebreaks<br />
Note that the
two backslashes are only recognized at the end of a line<br />

or followed by<br />
a whitespace \\this happens without it.
</p>
<pre class="code">This is some text with some linebreaks\\ Note that the
two backslashes are only recognized at the end of a line\\
or followed by\\ a whitespace \\this happens without it.</pre>

<p>
You should use forced newlines only if really needed.
</p>

</div>
<!-- EDIT2 SECTION "Basic Text Formatting" [473-1609] -->
<h2 class="sectionedit3" id="links">Links</h2>
<div class="level2">

<p>
DokuWiki supports multiple ways of creating links.
</p>

</div>
<!-- EDIT3 SECTION "Links" [1610-1680] -->
<h3 class="sectionedit4" id="external">External</h3>
<div class="level3">

<p>
External links are recognized automagically: <a href="http://www.google.com" class="urlextern" title="http://www.google.com" rel="nofollow">http://www.google.com</a> or simply <a href="http://www.google.com" class="urlextern" title="http://www.google.com" rel="nofollow">www.google.com</a> - You can set the link text as well: <a href="http://www.google.com" class="urlextern" title="http://www.google.com" rel="nofollow">This Link points to google</a>. Email addresses like this one: <a href="mailto:andi@splitbrain.org" class="mail" title="andi@splitbrain.org">andi@splitbrain.org</a> are recognized, too.
</p>
<pre class="code">DokuWiki supports multiple ways of creating links. External links are recognized
automagically: http://www.google.com or simply www.google.com - You can set
link text as well: [[http://www.google.com|This Link points to google]]. Email
addresses like this one: &lt;andi@splitbrain.org&gt; are recognized, too.</pre>

</div>
<!-- EDIT4 SECTION "External" [1681-2271] -->
<h3 class="sectionedit5" id="internal">Internal</h3>
<div class="level3">

<p>
Internal links are created by using square brackets. You can either just give a <a href="/doku.php/wiki:pagename" class="wikilink2" title="wiki:pagename" rel="nofollow">pagename</a> or use an additional <a href="/doku.php/wiki:pagename" class="wikilink2" title="wiki:pagename" rel="nofollow">link text</a>.
</p>
<pre class="code">Internal links are created by using square brackets. You can either just give
a [[pagename]] or use an additional [[pagename|link text]].</pre>

<p>
<a href="http://www.dokuwiki.org/pagename" class="interwiki iw_doku" title="http://www.dokuwiki.org/pagename">Wiki pagenames</a> are converted to lowercase automatically, special characters are not allowed.
</p>

<p>
You can use <a href="/doku.php/some:namespaces" class="wikilink2" title="some:namespaces" rel="nofollow">namespaces</a> by using a colon in the pagename.
</p>
<pre class="code">You can use [[some:namespaces]] by using a colon in the pagename.</pre>

<p>
For details about namespaces see <a href="http://www.dokuwiki.org/namespaces" class="interwiki iw_doku" title="http://www.dokuwiki.org/namespaces">namespaces</a>.
</p>

<p>
Linking to a specific section is possible, too. Just add the section name behind a hash character as known from <abbr title="HyperText Markup Language">HTML</abbr>. This links to <span class="curid"><a href="/wiki/syntax.html" class="wikilink1" title="wiki:syntax">this Section</a></span>.
</p>
<pre class="code">This links to [[syntax#internal|this Section]].</pre>

<p>
Notes:
</p>
<ul>
<li class="level1"><div class="li"> Links to <span class="curid"><a href="/wiki/syntax.html" class="wikilink1" title="wiki:syntax">existing pages</a></span> are shown in a different style from <a href="/doku.php/wiki:nonexisting" class="wikilink2" title="wiki:nonexisting" rel="nofollow">nonexisting</a> ones.</div>
</li>
<li class="level1"><div class="li"> DokuWiki does not use <a href="http://en.wikipedia.org/wiki/CamelCase" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/CamelCase">CamelCase</a> to automatically create links by default, but this behavior can be enabled in the <a href="http://www.dokuwiki.org/config" class="interwiki iw_doku" title="http://www.dokuwiki.org/config">config</a> file. Hint: If DokuWiki is a link, then it's enabled.</div>
</li>
<li class="level1"><div class="li"> When a section's heading is changed, its bookmark changes, too. So don't rely on section linking too much.</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Internal" [2272-3506] -->
<h3 class="sectionedit6" id="interwiki">Interwiki</h3>
<div class="level3">

<p>
DokuWiki supports <a href="http://www.dokuwiki.org/Interwiki" class="interwiki iw_doku" title="http://www.dokuwiki.org/Interwiki">Interwiki</a> links. These are quick links to other Wikis. For example this is a link to Wikipedia's page about Wikis: <a href="http://en.wikipedia.org/wiki/Wiki" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/Wiki">Wiki</a>.
</p>
<pre class="code">DokuWiki supports [[doku&gt;Interwiki]] links. These are quick links to other Wikis.
For example this is a link to Wikipedia's page about Wikis: [[wp&gt;Wiki]].</pre>

</div>
<!-- EDIT6 SECTION "Interwiki" [3507-3843] -->
<h3 class="sectionedit7" id="windows_shares">Windows Shares</h3>
<div class="level3">

<p>
Windows shares like <a href="file://///server/share" class="windows" title="\\server\share">this</a> are recognized, too. Please note that these only make sense in a homogeneous user group like a corporate <a href="http://en.wikipedia.org/wiki/Intranet" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/Intranet">Intranet</a>.
</p>
<pre class="code">Windows Shares like [[\\server\share|this]] are recognized, too.</pre>

<p>
Notes:
</p>
<ul>
<li class="level1"><div class="li"> For security reasons direct browsing of windows shares only works in Microsoft Internet Explorer per default (and only in the “local zone”).</div>
</li>
<li class="level1"><div class="li"> For Mozilla and Firefox it can be enabled through different workaround mentioned in the <a href="http://kb.mozillazine.org/Links_to_local_pages_do_not_work" class="urlextern" title="http://kb.mozillazine.org/Links_to_local_pages_do_not_work" rel="nofollow">Mozilla Knowledge Base</a>. However, there will still be a JavaScript warning about trying to open a Windows Share. To remove this warning (for all users), put the following line in <code>conf/userscript.js</code>:</div>
</li>
</ul>
<pre class="code">LANG.nosmblinks = '';</pre>

</div>
<!-- EDIT7 SECTION "Windows Shares" [3844-4640] -->
<h3 class="sectionedit8" id="image_links">Image Links</h3>
<div class="level3">

<p>
You can also use an image to link to another internal or external page by combining the syntax for links and <a href="#images_and_other_files" title="wiki:syntax ↵" class="wikilink1">images</a> (see below) like this:
</p>
<pre class="code">[[http://www.php.net|{{wiki:dokuwiki-128.png}}]]</pre>

<p>
<a href="/resources/wiki-dokuwiki-128.png" class="media" title="http://www.php.net" rel="nofollow"><img src="/resources/wiki-dokuwiki-128.png" class="media" alt="" /></a>
</p>

<p>
Please note: The image formatting is the only formatting syntax accepted in link names.
</p>

<p>
The whole <a href="#images_and_other_files" title="wiki:syntax ↵" class="wikilink1">image</a> and <a href="#links" title="wiki:syntax ↵" class="wikilink1">link</a> syntax is supported (including image resizing, internal and external images and URLs and interwiki links).
</p>

</div>
<!-- EDIT8 SECTION "Image Links" [4641-5194] -->
<h2 class="sectionedit9" id="footnotes">Footnotes</h2>
<div class="level2">

<p>
You can add footnotes <sup><a href="#fn__1" id="fnt__1" class="fn_top">1)</a></sup> by using double parentheses.
</p>
<pre class="code">You can add footnotes ((This is a footnote)) by using double parentheses.</pre>

</div>
<!-- EDIT9 SECTION "Footnotes" [5195-5369] -->
<h2 class="sectionedit10" id="sectioning">Sectioning</h2>
<div class="level2">

<p>
You can use up to five different levels of headlines to structure your content. If you have more than three headlines, a table of contents is generated automatically – this can be disabled by including the string <code>~~NOTOC~~</code> in the document.
</p>

</div>
<!-- EDIT10 SECTION "Sectioning" [5370-5656] -->
<h3 class="sectionedit11" id="headline_level_3">Headline Level 3</h3>
<div class="level3">

</div>

<h4 id="headline_level_4">Headline Level 4</h4>
<div class="level4">

</div>

<h5 id="headline_level_5">Headline Level 5</h5>
<div class="level5">
<pre class="code">==== Headline Level 3 ====
=== Headline Level 4 ===
== Headline Level 5 ==</pre>

<p>
By using four or more dashes, you can make a horizontal line:
</p>
<hr />

</div>
<!-- EDIT11 SECTION "Headline Level 3" [5657-5883] -->
<h2 class="sectionedit12" id="media_files">Media Files</h2>
<div class="level2">

<p>
You can include external and internal <a href="http://www.dokuwiki.org/images" class="interwiki iw_doku" title="http://www.dokuwiki.org/images">images, videos and audio files</a> with curly brackets. Optionally you can specify the size of them.
</p>

<p>
Real size:                        <a href="/resources/wiki-dokuwiki-128.png" class="media" title="wiki:dokuwiki-128.png"><img src="/resources/wiki-dokuwiki-128.png" class="media" alt="" /></a>
</p>

<p>
Resize to given width:            <a href="/resources/wiki-dokuwiki-128.png" class="media" title="wiki:dokuwiki-128.png"><img src="/resources/wiki-dokuwiki-128.png" class="media" alt="" width="50" /></a>
</p>

<p>
Resize to given width and height<sup><a href="#fn__2" id="fnt__2" class="fn_top">2)</a></sup>: <a href="/resources/wiki-dokuwiki-128.png" class="media" title="wiki:dokuwiki-128.png"><img src="/resources/wiki-dokuwiki-128.png" class="media" alt="" width="200" height="50" /></a>
</p>

<p>
Resized external image:           <a href="/resources/fetch.php" class="media" title="http://de3.php.net/images/php.gif"><img src="/resources/fetch.php" class="media" alt="" width="200" height="50" /></a>
</p>
<pre class="code">Real size:                        {{wiki:dokuwiki-128.png}}
Resize to given width:            {{wiki:dokuwiki-128.png?50}}
Resize to given width and height: {{wiki:dokuwiki-128.png?200x50}}
Resized external image:           {{http://de3.php.net/images/php.gif?200x50}}</pre>

<p>
By using left or right whitespaces you can choose the alignment.
</p>

<p>
<a href="/resources/wiki-dokuwiki-128.png" class="media" title="wiki:dokuwiki-128.png"><img src="/resources/wiki-dokuwiki-128.png" class="mediaright" alt="" /></a>
</p>

<p>
<a href="/resources/wiki-dokuwiki-128.png" class="media" title="wiki:dokuwiki-128.png"><img src="/resources/wiki-dokuwiki-128.png" class="medialeft" alt="" /></a>
</p>

<p>
<a href="/resources/wiki-dokuwiki-128.png" class="media" title="wiki:dokuwiki-128.png"><img src="/resources/wiki-dokuwiki-128.png" class="mediacenter" alt="" /></a>
</p>
<pre class="code">{{ wiki:dokuwiki-128.png}}
{{wiki:dokuwiki-128.png }}
{{ wiki:dokuwiki-128.png }}</pre>

<p>
Of course, you can add a title (displayed as a tooltip by most browsers), too.
</p>

<p>
<a href="/resources/wiki-dokuwiki-128.png" class="media" title="wiki:dokuwiki-128.png"><img src="/resources/wiki-dokuwiki-128.png" class="mediacenter" title="This is the caption" alt="This is the caption" /></a>
</p>
<pre class="code">{{ wiki:dokuwiki-128.png |This is the caption}}</pre>

<p>
For linking an image to another page see <a href="#image_links" title="wiki:syntax ↵" class="wikilink1">Image Links</a> above.
</p>

</div>
<!-- EDIT12 SECTION "Media Files" [5884-7238] -->
<h3 class="sectionedit13" id="supported_media_formats">Supported Media Formats</h3>
<div class="level3">

<p>
DokuWiki can embed the following media formats directly.
</p>
<div class="table sectionedit14"><table class="inline">
	<tr class="row0">
		<td class="col0"> Image </td><td class="col1 leftalign"> <code>gif</code>, <code>jpg</code>, <code>png</code>  </td>
	</tr>
	<tr class="row1">
		<td class="col0"> Video </td><td class="col1"> <code>webm</code>, <code>ogv</code>, <code>mp4</code> </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Audio </td><td class="col1 leftalign"> <code>ogg</code>, <code>mp3</code>, <code>wav</code>  </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Flash </td><td class="col1 leftalign"> <code>swf</code>                    </td>
	</tr>
</table></div>
<!-- EDIT14 TABLE [7332-7487] -->
<p>
If you specify a filename that is not a supported media format, then it will be displayed as a link instead.
</p>

</div>
<!-- EDIT13 SECTION "Supported Media Formats" [7239-7598] -->
<h3 class="sectionedit15" id="fallback_formats">Fallback Formats</h3>
<div class="level3">

<p>
Unfortunately not all browsers understand all video and audio formats. To mitigate the problem, you can upload your file in different formats for maximum browser compatibility.
</p>

<p>
For example consider this embedded mp4 video:
</p>
<pre class="code">{{video.mp4|A funny video}}</pre>

<p>
When you upload a <code>video.webm</code> and <code>video.ogv</code> next to the referenced <code>video.mp4</code>, DokuWiki will automatically add them as alternatives so that one of the three files is understood by your browser.
</p>

<p>
Additionally DokuWiki supports a “poster” image which will be shown before the video has started. That image needs to have the same filename as the video and be either a jpg or png file. In the example above a <code>video.jpg</code> file would work.
</p>

</div>
<!-- EDIT15 SECTION "Fallback Formats" [7599-8329] -->
<h2 class="sectionedit16" id="lists">Lists</h2>
<div class="level2">

<p>
Dokuwiki supports ordered and unordered lists. To create a list item, indent your text by two spaces and use a <code>*</code> for unordered lists or a <code>-</code> for ordered ones.
</p>
<ul>
<li class="level1"><div class="li"> This is a list</div>
</li>
<li class="level1"><div class="li"> The second item</div>
<ul>
<li class="level2"><div class="li"> You may have different levels</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Another item</div>
</li>
</ul>
<ol>
<li class="level1"><div class="li"> The same list but ordered</div>
</li>
<li class="level1"><div class="li"> Another item</div>
<ol>
<li class="level2"><div class="li"> Just use indention for deeper levels</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> That's it</div>
</li>
</ol>
<pre class="code">  * This is a list
  * The second item
    * You may have different levels
  * Another item

  - The same list but ordered
  - Another item
    - Just use indention for deeper levels
  - That's it</pre>

<p>
Also take a look at the <a href="http://www.dokuwiki.org/faq%3Alists" class="interwiki iw_doku" title="http://www.dokuwiki.org/faq%3Alists">FAQ on list items</a>.
</p>

</div>
<!-- EDIT16 SECTION "Lists" [8330-8989] -->
<h2 class="sectionedit17" id="text_conversions">Text Conversions</h2>
<div class="level2">

<p>
DokuWiki can convert certain pre-defined characters or strings into images or other text or <abbr title="HyperText Markup Language">HTML</abbr>.
</p>

<p>
The text to image conversion is mainly done for smileys. And the text to <abbr title="HyperText Markup Language">HTML</abbr> conversion is used for typography replacements, but can be configured to use other <abbr title="HyperText Markup Language">HTML</abbr> as well.
</p>

</div>
<!-- EDIT17 SECTION "Text Conversions" [8990-9294] -->
<h3 class="sectionedit18" id="text_to_image_conversions">Text to Image Conversions</h3>
<div class="level3">

<p>
DokuWiki converts commonly used <a href="http://en.wikipedia.org/wiki/emoticon" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/emoticon">emoticon</a>s to their graphical equivalents. Those <a href="http://www.dokuwiki.org/Smileys" class="interwiki iw_doku" title="http://www.dokuwiki.org/Smileys">Smileys</a> and other images can be configured and extended. Here is an overview of Smileys included in DokuWiki:
</p>
<ul>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_cool.gif" class="icon" alt="8-)" />   8-)  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_eek.gif" class="icon" alt="8-O" />   8-O  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_sad.gif" class="icon" alt=":-(" />   :-(  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_smile.gif" class="icon" alt=":-)" />   :-)  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_smile2.gif" class="icon" alt="=)" />    =)   </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_doubt.gif" class="icon" alt=":-/" />   :-/  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_doubt2.gif" class="icon" alt=":-\" />   :-\  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_confused.gif" class="icon" alt=":-?" />   :-?  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_biggrin.gif" class="icon" alt=":-D" />   :-D  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_razz.gif" class="icon" alt=":-P" />   :-P  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_surprised.gif" class="icon" alt=":-O" />   :-O  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_silenced.gif" class="icon" alt=":-X" />   :-X  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_neutral.gif" class="icon" alt=":-|" />   :-|  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_wink.gif" class="icon" alt=";-)" />   ;-)  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_fun.gif" class="icon" alt="^_^" />   ^_^  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_question.gif" class="icon" alt=":?:" />   :?:  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_exclaim.gif" class="icon" alt=":!:" />   :!:  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/icon_lol.gif" class="icon" alt="LOL" />   LOL  </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/fixme.gif" class="icon" alt="FIXME" />   FIXME </div>
</li>
<li class="level1"><div class="li"> <img src="/lib/images/smileys/delete.gif" class="icon" alt="DELETEME" />  DELETEME </div>
</li>
</ul>

</div>
<!-- EDIT18 SECTION "Text to Image Conversions" [9295-9950] -->
<h3 class="sectionedit19" id="text_to_html_conversions">Text to HTML Conversions</h3>
<div class="level3">

<p>
Typography: <a href="/wiki/dokuwiki.html" class="wikilink1" title="wiki:dokuwiki">DokuWiki</a> can convert simple text characters to their typographically correct entities. Here is an example of recognized characters.
</p>

<p>
→ ← ↔ ⇒ ⇐ ⇔ » « – — 640×480 © ™ ®
“He thought 'It's a man's world'…”
</p>
<pre class="code">-&gt; &lt;- &lt;-&gt; =&gt; &lt;= &lt;=&gt; &gt;&gt; &lt;&lt; -- --- 640x480 (c) (tm) (r)
"He thought 'It's a man's world'..."</pre>

<p>
The same can be done to produce any kind of <abbr title="HyperText Markup Language">HTML</abbr>, it just needs to be added to the <a href="http://www.dokuwiki.org/entities" class="interwiki iw_doku" title="http://www.dokuwiki.org/entities">pattern file</a>.
</p>

<p>
There are three exceptions which do not come from that pattern file: multiplication entity (640×480), 'single' and “double quotes”. They can be turned off through a <a href="http://www.dokuwiki.org/config%3Atypography" class="interwiki iw_doku" title="http://www.dokuwiki.org/config%3Atypography">config option</a>.
</p>

</div>
<!-- EDIT19 SECTION "Text to HTML Conversions" [9951-10658] -->
<h2 class="sectionedit20" id="quoting">Quoting</h2>
<div class="level2">

<p>
Some times you want to mark some text to show it's a reply or comment. You can use the following syntax:
</p>
<pre class="code">I think we should do it

&gt; No we shouldn't

&gt;&gt; Well, I say we should

&gt; Really?

&gt;&gt; Yes!

&gt;&gt;&gt; Then lets do it!</pre>

<p>
I think we should do it
</p>
<blockquote><div class="no">
 No we shouldn't</div></blockquote>
<blockquote><div class="no">
<blockquote><div class="no">
 Well, I say we should</div></blockquote>
</div></blockquote>
<blockquote><div class="no">
 Really?</div></blockquote>
<blockquote><div class="no">
<blockquote><div class="no">
 Yes!</div></blockquote>
</div></blockquote>
<blockquote><div class="no">
<blockquote><div class="no">
<blockquote><div class="no">
 Then lets do it!</div></blockquote>
</div></blockquote>
</div></blockquote>

</div>
<!-- EDIT20 SECTION "Quoting" [10659-11031] -->
<h2 class="sectionedit21" id="tables">Tables</h2>
<div class="level2">

<p>
DokuWiki supports a simple syntax to create tables.
</p>
<div class="table sectionedit22"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Heading 1      </th><th class="col1 leftalign"> Heading 2       </th><th class="col2 leftalign"> Heading 3          </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> Row 1 Col 1    </td><td class="col1 leftalign"> Row 1 Col 2     </td><td class="col2 leftalign"> Row 1 Col 3        </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> Row 2 Col 1    </td><td class="col1" colspan="2"> some colspan (note the double pipe) </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> Row 3 Col 1    </td><td class="col1 leftalign"> Row 3 Col 2     </td><td class="col2 leftalign"> Row 3 Col 3        </td>
	</tr>
</table></div>
<!-- EDIT22 TABLE [11105-11336] -->
<p>
Table rows have to start and end with a <code>|</code> for normal rows or a <code>^</code> for headers.
</p>
<pre class="code">^ Heading 1      ^ Heading 2       ^ Heading 3          ^
| Row 1 Col 1    | Row 1 Col 2     | Row 1 Col 3        |
| Row 2 Col 1    | some colspan (note the double pipe) ||
| Row 3 Col 1    | Row 3 Col 2     | Row 3 Col 3        |</pre>

<p>
To connect cells horizontally, just make the next cell completely empty as shown above. Be sure to have always the same amount of cell separators!
</p>

<p>
Vertical tableheaders are possible, too.
</p>
<div class="table sectionedit23"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0 leftalign">              </td><th class="col1 leftalign"> Heading 1            </th><th class="col2 leftalign"> Heading 2          </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0 leftalign"> Heading 3    </th><td class="col1 leftalign"> Row 1 Col 2          </td><td class="col2 leftalign"> Row 1 Col 3        </td>
	</tr>
	<tr class="row2">
		<th class="col0 leftalign"> Heading 4    </th><td class="col1"> no colspan this time </td><td class="col2 leftalign">                    </td>
	</tr>
	<tr class="row3">
		<th class="col0 leftalign"> Heading 5    </th><td class="col1 leftalign"> Row 2 Col 2          </td><td class="col2 leftalign"> Row 2 Col 3        </td>
	</tr>
</table></div>
<!-- EDIT23 TABLE [11856-12099] -->
<p>
As you can see, it's the cell separator before a cell which decides about the formatting:
</p>
<pre class="code">|              ^ Heading 1            ^ Heading 2          ^
^ Heading 3    | Row 1 Col 2          | Row 1 Col 3        |
^ Heading 4    | no colspan this time |                    |
^ Heading 5    | Row 2 Col 2          | Row 2 Col 3        |</pre>

<p>
You can have rowspans (vertically connected cells) by adding <code>:::</code> into the cells below the one to which they should connect.
</p>
<div class="table sectionedit24"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Heading 1      </th><th class="col1 leftalign"> Heading 2                  </th><th class="col2 leftalign"> Heading 3          </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> Row 1 Col 1    </td><td class="col1" rowspan="3"> this cell spans vertically </td><td class="col2 leftalign"> Row 1 Col 3        </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> Row 2 Col 1    </td><td class="col1 leftalign"> Row 2 Col 3        </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> Row 3 Col 1    </td><td class="col1 leftalign"> Row 2 Col 3        </td>
	</tr>
</table></div>
<!-- EDIT24 TABLE [12574-12849] -->
<p>
Apart from the rowspan syntax those cells should not contain anything else.
</p>
<pre class="code">^ Heading 1      ^ Heading 2                  ^ Heading 3          ^
| Row 1 Col 1    | this cell spans vertically | Row 1 Col 3        |
| Row 2 Col 1    | :::                        | Row 2 Col 3        |
| Row 3 Col 1    | :::                        | Row 2 Col 3        |</pre>

<p>
You can align the table contents, too. Just add at least two whitespaces at the opposite end of your text: Add two spaces on the left to align right, two spaces on the right to align left and two spaces at least at both ends for centered text.
</p>
<div class="table sectionedit25"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 centeralign" colspan="3">           Table with alignment           </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 rightalign">         right</td><td class="col1 centeralign">    center    </td><td class="col2 leftalign">left          </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign">left          </td><td class="col1 rightalign">         right</td><td class="col2 centeralign">    center    </td>
	</tr>
	<tr class="row3">
		<td class="col0"> xxxxxxxxxxxx </td><td class="col1"> xxxxxxxxxxxx </td><td class="col2"> xxxxxxxxxxxx </td>
	</tr>
</table></div>
<!-- EDIT25 TABLE [13458-13645] -->
<p>
This is how it looks in the source:
</p>
<pre class="code">^           Table with alignment           ^^^
|         right|    center    |left          |
|left          |         right|    center    |
| xxxxxxxxxxxx | xxxxxxxxxxxx | xxxxxxxxxxxx |</pre>

<p>
Note: Vertical alignment is not supported.
</p>

</div>
<!-- EDIT21 SECTION "Tables" [11032-13924] -->
<h2 class="sectionedit26" id="no_formatting">No Formatting</h2>
<div class="level2">

<p>
If you need to display text exactly like it is typed (without any formatting), enclose the area either with <code>&lt;nowiki&gt;</code> tags or even simpler, with double percent signs <code>%%</code>.
</p>

<p>

This is some text which contains addresses like this: http://www.splitbrain.org and **formatting**, but nothing is done with it.

The same is true for //__this__ text// with a smiley ;-).
</p>
<pre class="code">&lt;nowiki&gt;
This is some text which contains addresses like this: http://www.splitbrain.org and **formatting**, but nothing is done with it.
&lt;/nowiki&gt;
The same is true for %%//__this__ text// with a smiley ;-)%%.</pre>

</div>
<!-- EDIT26 SECTION "No Formatting" [13925-14580] -->
<h2 class="sectionedit27" id="code_blocks">Code Blocks</h2>
<div class="level2">

<p>
You can include code blocks into your documents by either indenting them by at least two spaces (like used for the previous examples) or by using the tags <code>&lt;code&gt;</code> or <code>&lt;file&gt;</code>.
</p>
<pre class="code">This is text is indented by two spaces.</pre>
<pre class="code">This is preformatted code all spaces are preserved: like              &lt;-this</pre>
<pre class="file">This is pretty much the same, but you could use it to show that you quoted a file.</pre>

<p>
Those blocks were created by this source:
</p>
<pre class="code">  This is text is indented by two spaces.</pre>
<pre class="code">&lt;code&gt;
This is preformatted code all spaces are preserved: like              &lt;-this
&lt;/code&gt;</pre>
<pre class="code">&lt;file&gt;
This is pretty much the same, but you could use it to show that you quoted a file.
&lt;/file&gt;</pre>

</div>
<!-- EDIT27 SECTION "Code Blocks" [14581-15322] -->
<h3 class="sectionedit28" id="syntax_highlighting">Syntax Highlighting</h3>
<div class="level3">

<p>
<a href="/wiki/dokuwiki.html" class="wikilink1" title="wiki:dokuwiki">DokuWiki</a> can highlight sourcecode, which makes it easier to read. It uses the <a href="http://qbnz.com/highlighter/" class="urlextern" title="http://qbnz.com/highlighter/" rel="nofollow">GeSHi</a> Generic Syntax Highlighter – so any language supported by GeSHi is supported. The syntax uses the same code and file blocks described in the previous section, but this time the name of the language syntax to be highlighted is included inside the tag, e.g. <code>&lt;code java&gt;</code> or <code>&lt;file java&gt;</code>.
</p>
<pre class="code java"><span class="co3">/**
 * The HelloWorldApp class implements an application that
 * simply displays "Hello World!" to the standard output.
 */</span>
<span class="kw1">class</span> HelloWorldApp <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Hello World!"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">//Display the string.</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
The following language strings are currently recognized: <em>4cs, 6502acme, 6502kickass, 6502tasm, 68000devpac, abap, actionscript-french, actionscript, actionscript3, ada, algol68, apache, applescript, asm, asp, autoconf, autohotkey, autoit, avisynth, awk, bascomavr, bash, basic4gl, bf, bibtex, blitzbasic, bnf, boo, c, c_loadrunner, c_mac, caddcl, cadlisp, cfdg, cfm, chaiscript, cil, clojure, cmake, cobol, coffeescript, cpp, cpp-qt, csharp, css, cuesheet, d, dcs, delphi, diff, div, dos, dot, e, epc, ecmascript, eiffel, email, erlang, euphoria, f1, falcon, fo, fortran, freebasic, fsharp, gambas, genero, genie, gdb, glsl, gml, gnuplot, go, groovy, gettext, gwbasic, haskell, hicest, hq9plus, html, html5, icon, idl, ini, inno, intercal, io, j, java5, java, javascript, jquery, kixtart, klonec, klonecpp, latex, lb, lisp, llvm, locobasic, logtalk, lolcode, lotusformulas, lotusscript, lscript, lsl2, lua, m68k, magiksf, make, mapbasic, matlab, mirc, modula2, modula3, mmix, mpasm, mxml, mysql, newlisp, nsis, oberon2, objc, objeck, ocaml-brief, ocaml, oobas, oracle8, oracle11, oxygene, oz, pascal, pcre, perl, perl6, per, pf, php-brief, php, pike, pic16, pixelbender, pli, plsql, postgresql, povray, powerbuilder, powershell, proftpd, progress, prolog, properties, providex, purebasic, pycon, python, q, qbasic, rails, rebol, reg, robots, rpmspec, rsplus, ruby, sas, scala, scheme, scilab, sdlbasic, smalltalk, smarty, sql, systemverilog, tcl, teraterm, text, thinbasic, tsql, typoscript, unicon, uscript, vala, vbnet, vb, verilog, vhdl, vim, visualfoxpro, visualprolog, whitespace, winbatch, whois, xbasic, xml, xorg_conf, xpp, yaml, z80, zxbasic</em>
</p>

</div>
<!-- EDIT28 SECTION "Syntax Highlighting" [15323-17749] -->
<h3 class="sectionedit29" id="downloadable_code_blocks">Downloadable Code Blocks</h3>
<div class="level3">

<p>
When you use the <code>&lt;code&gt;</code> or <code>&lt;file&gt;</code> syntax as above, you might want to make the shown code available for download as well. You can do this by specifying a file name after language code like this:
</p>
<pre class="code">&lt;file php myexample.php&gt;
&lt;?php echo "hello world!"; ?&gt;
&lt;/file&gt;</pre>
<dl class="file">
<dt><a href="/doku.php/wiki:syntax?do=export_code&amp;codeblock=6" title="Download Snippet" class="mediafile mf_php">myexample.php</a></dt>
<dd><pre class="code file php"><span class="kw2">&lt;?php</span> <span class="kw1">echo</span> <span class="st0">"hello world!"</span><span class="sy0">;</span> <span class="sy1">?&gt;</span></pre>
</dd></dl>

<p>
If you don't want any highlighting but want a downloadable file, specify a dash (<code>-</code>) as the language code: <code>&lt;code - myfile.foo&gt;</code>.
</p>

</div>
<!-- EDIT29 SECTION "Downloadable Code Blocks" [17750-18280] -->
<h2 class="sectionedit30" id="embedding_html_and_php">Embedding HTML and PHP</h2>
<div class="level2">

<p>
You can embed raw <abbr title="HyperText Markup Language">HTML</abbr> or PHP code into your documents by using the <code>&lt;html&gt;</code> or <code>&lt;php&gt;</code> tags. (Use uppercase tags if you need to enclose block level elements.)
</p>

<p>
<abbr title="HyperText Markup Language">HTML</abbr> example:
</p>
<pre class="code">&lt;html&gt;
This is some &lt;span style="color:red;font-size:150%;"&gt;inline HTML&lt;/span&gt;
&lt;/html&gt;
&lt;HTML&gt;
&lt;p style="border:2px dashed red;"&gt;And this is some block HTML&lt;/p&gt;
&lt;/HTML&gt;</pre>

<p>
<code class="code html4strict">This is some <span class="sc2">&lt;<a href="http://december.com/html/4/element/span.html"><span class="kw2">span</span></a> <span class="kw3">style</span><span class="sy0">=</span><span class="st0">"color:red;font-size:150%;"</span>&gt;</span>inline HTML<span class="sc2">&lt;<span class="sy0">/</span><a href="http://december.com/html/4/element/span.html"><span class="kw2">span</span></a>&gt;</span></code>
</p>
<pre class="code html4strict"><span class="sc2">&lt;<a href="http://december.com/html/4/element/p.html"><span class="kw2">p</span></a> <span class="kw3">style</span><span class="sy0">=</span><span class="st0">"border:2px dashed red;"</span>&gt;</span>And this is some block HTML<span class="sc2">&lt;<span class="sy0">/</span><a href="http://december.com/html/4/element/p.html"><span class="kw2">p</span></a>&gt;</span></pre>
<p>
PHP example:
</p>
<pre class="code">&lt;php&gt;
echo 'The PHP version: ';
echo phpversion();
echo ' (generated inline HTML)';
&lt;/php&gt;
&lt;PHP&gt;
echo '&lt;table class="inline"&gt;&lt;tr&gt;&lt;td&gt;The same, but inside a block level element:&lt;/td&gt;';
echo '&lt;td&gt;'.phpversion().'&lt;/td&gt;';
echo '&lt;/tr&gt;&lt;/table&gt;';
&lt;/PHP&gt;</pre>

<p>
<code class="code php"><span class="kw1">echo</span> <span class="st_h">'The PHP version: '</span><span class="sy0">;</span>
<span class="kw1">echo</span> <a href="http://www.php.net/phpversion"><span class="kw3">phpversion</span></a><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
<span class="kw1">echo</span> <span class="st_h">' (inline HTML)'</span><span class="sy0">;</span></code>
</p>
<pre class="code php"><span class="kw1">echo</span> <span class="st_h">'&lt;table class="inline"&gt;&lt;tr&gt;&lt;td&gt;The same, but inside a block level element:&lt;/td&gt;'</span><span class="sy0">;</span>
<span class="kw1">echo</span> <span class="st_h">'&lt;td&gt;'</span><span class="sy0">.</span><a href="http://www.php.net/phpversion"><span class="kw3">phpversion</span></a><span class="br0">(</span><span class="br0">)</span><span class="sy0">.</span><span class="st_h">'&lt;/td&gt;'</span><span class="sy0">;</span>
<span class="kw1">echo</span> <span class="st_h">'&lt;/tr&gt;&lt;/table&gt;'</span><span class="sy0">;</span></pre>
<p>
<strong>Please Note</strong>: <abbr title="HyperText Markup Language">HTML</abbr> and PHP embedding is disabled by default in the configuration. If disabled, the code is displayed instead of executed.
</p>

</div>
<!-- EDIT30 SECTION "Embedding HTML and PHP" [18281-19514] -->
<h2 class="sectionedit31" id="rss_atom_feed_aggregation">RSS/ATOM Feed Aggregation</h2>
<div class="level2">

<p>
<a href="/wiki/dokuwiki.html" class="wikilink1" title="wiki:dokuwiki">DokuWiki</a> can integrate data from external XML feeds. For parsing the XML feeds, <a href="http://simplepie.org/" class="urlextern" title="http://simplepie.org/" rel="nofollow">SimplePie</a> is used. All formats understood by SimplePie can be used in DokuWiki as well. You can influence the rendering by multiple additional space separated parameters:
</p>
<div class="table sectionedit32"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Parameter  </th><th class="col1"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> any number </td><td class="col1"> will be used as maximum number items to show, defaults to 8 </td>
	</tr>
	<tr class="row2">
		<td class="col0 leftalign"> reverse    </td><td class="col1"> display the last items in the feed first </td>
	</tr>
	<tr class="row3">
		<td class="col0 leftalign"> author     </td><td class="col1"> show item authors names </td>
	</tr>
	<tr class="row4">
		<td class="col0 leftalign"> date       </td><td class="col1"> show item dates </td>
	</tr>
	<tr class="row5">
		<td class="col0"> description</td><td class="col1"> show the item description. If <a href="http://www.dokuwiki.org/config%3Ahtmlok" class="interwiki iw_doku" title="http://www.dokuwiki.org/config%3Ahtmlok">HTML</a> is disabled all tags will be stripped </td>
	</tr>
	<tr class="row6">
		<td class="col0"> <em>n</em>[dhm] </td><td class="col1"> refresh period, where d=days, h=hours, m=minutes. (e.g. 12h = 12 hours). </td>
	</tr>
</table></div>
<!-- EDIT32 TABLE [19835-20275] -->
<p>
The refresh period defaults to 4 hours. Any value below 10 minutes will be treated as 10 minutes. <a href="/wiki/dokuwiki.html" class="wikilink1" title="wiki:dokuwiki">DokuWiki</a> will generally try to supply a cached version of a page, obviously this is inappropriate when the page contains dynamic external content. The parameter tells <a href="/wiki/dokuwiki.html" class="wikilink1" title="wiki:dokuwiki">DokuWiki</a> to re-render the page if it is more than <em>refresh period</em> since the page was last rendered.
</p>

<p>
<strong>Example:</strong>
</p>
<pre class="code">{{rss&gt;http://slashdot.org/index.rss 5 author date 1h }}</pre>
<ul class="rss"><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/QvA2I323z-Q/gene-roddenberrys-floppy-disks-recovered" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/QvA2I323z-Q/gene-roddenberrys-floppy-disks-recovered" rel="nofollow">Gene Roddenberry's Floppy Disks Recovered</a> by Soulskill (2016/01/05 18:10)</div></li><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/pvCDF-Xeszw/comcasts-xfinity-home-security-flaw-leaves-doors-open" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/pvCDF-Xeszw/comcasts-xfinity-home-security-flaw-leaves-doors-open" rel="nofollow">Comcast's Xfinity Home Security Flaw Leaves Doors Open</a> by Soulskill (2016/01/05 17:28)</div></li><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/pMrkiYdJlts/brazil-cautions-women-to-avoid-pregnancy-over-zika-virus-outbreak" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/pMrkiYdJlts/brazil-cautions-women-to-avoid-pregnancy-over-zika-virus-outbreak" rel="nofollow">Brazil Cautions Women To Avoid Pregnancy Over Zika Virus Outbreak</a> by Soulskill (2016/01/05 16:48)</div></li><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/hgfC4FEs7p0/nsa-targeted-the-two-leading-encryption-chips" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/hgfC4FEs7p0/nsa-targeted-the-two-leading-encryption-chips" rel="nofollow">NSA Targeted 'The Two Leading' Encryption Chips</a> by Soulskill (2016/01/05 16:15)</div></li><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/9tWlPLOwPSw/the-unreasonable-effectiveness-of-adhesive-tape" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/9tWlPLOwPSw/the-unreasonable-effectiveness-of-adhesive-tape" rel="nofollow">The Unreasonable Effectiveness of Adhesive Tape</a> by Soulskill (2016/01/05 15:42)</div></li></ul>
</div>
<!-- EDIT31 SECTION "RSS/ATOM Feed Aggregation" [19515-20794] -->
<h2 class="sectionedit33" id="control_macros">Control Macros</h2>
<div class="level2">

<p>
Some syntax influences how DokuWiki renders a page without creating any output it self. The following control macros are availble:
</p>
<div class="table sectionedit34"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0 leftalign"> Macro           </th><th class="col1"> Description </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0 leftalign"> ~~NOTOC~~   </td><td class="col1"> If this macro is found on the page, no table of contents will be created </td>
	</tr>
	<tr class="row2">
		<td class="col0"> ~~NOCACHE~~ </td><td class="col1"> DokuWiki caches all output by default. Sometimes this might not be wanted (eg. when the &lt;php&gt; syntax above is used), adding this macro will force DokuWiki to rerender a page on every call </td>
	</tr>
</table></div>
<!-- EDIT34 TABLE [20955-21297] -->
</div>
<!-- EDIT33 SECTION "Control Macros" [20795-21298] -->
<h2 class="sectionedit35" id="syntax_plugins">Syntax Plugins</h2>
<div class="level2">

<p>
DokuWiki's syntax can be extended by <a href="http://www.dokuwiki.org/plugins" class="interwiki iw_doku" title="http://www.dokuwiki.org/plugins">Plugins</a>. How the installed plugins are used is described on their appropriate description pages. The following syntax plugins are available in this particular DokuWiki installation:
</p>
<ul><li><div class="li"><a href="http://dokuwiki.org/plugin:info" class="urlextern" title="http://dokuwiki.org/plugin:info" rel="nofollow">Info Plugin</a> <em>2014-03-05</em> by <a href="mailto:andi@splitbrain.org" class="mail" title="andi@splitbrain.org">Andreas Gohr</a><br />Displays information about various DokuWiki internals</div></li><li><div class="li"><a href="http://www.dokuwiki.org/plugin:pagelist" class="urlextern" title="http://www.dokuwiki.org/plugin:pagelist" rel="nofollow">Pagelist Plugin</a> <em>2014-05-26</em> by <a href="mailto:michael@content-space.de" class="mail" title="michael@content-space.de">Matthias Schulte, Michael Hamann, Michael Klier, Gina Haeussge</a><br />Lists pages in a nice formatted way</div></li><li><div class="li"><a href="https://www.dokuwiki.org/plugin:siteexport" class="urlextern" title="https://www.dokuwiki.org/plugin:siteexport" rel="nofollow">Site Export</a> <em>2015-10-15</em> by <a href="mailto:tools@inetsoftware.de" class="mail" title="tools@inetsoftware.de">i-net software</a><br />exports the dokuwiki site in the given format</div></li><li><div class="li"><a href="https://www.dokuwiki.org/plugin:tag" class="urlextern" title="https://www.dokuwiki.org/plugin:tag" rel="nofollow">tag plugin</a> <em>2014-02-16</em> by <a href="mailto:michael@content-space.de" class="mail" title="michael@content-space.de">Michael Hamann, Gina Häussge, Christopher Smith, Michael Klier, Esther Brunner</a><br />tag wiki pages</div></li><li><div class="li"><a href="http://www.dokuwiki.org/plugin:iframe" class="urlextern" title="http://www.dokuwiki.org/plugin:iframe" rel="nofollow">iframe Plugin</a> <em>2008-10-31</em> by <a href="mailto:chris@jalakai.co.uk" class="mail" title="chris@jalakai.co.uk">Christopher Smith</a><br />Add an iframe containing the specified url<br />                     syntax: {{url&gt;http://www.somesite.com/somepage.htm [w,h]|alternate text}}</div></li><li><div class="li"><a href="http://www.dokuwiki.org/plugin:note" class="urlextern" title="http://www.dokuwiki.org/plugin:note" rel="nofollow">Note Plugin</a> <em>2009-06-15</em> by <a href="mailto:olive@deep-ocean.net" class="mail" title="olive@deep-ocean.net">Olivier Cortès / Eric Hameleers / Christopher Smith / Aurélien Bompard</a><br />Add Note/Important/Tip/Warning Capability (DIV+CSS box)</div></li></ul>
</div>
<!-- EDIT35 SECTION "Syntax Plugins" [21299-] --><div class="footnotes">
<div class="fn"><sup><a href="#fnt__1" id="fn__1" class="fn_bot">1)</a></sup> 
This is a footnote</div>
<div class="fn"><sup><a href="#fnt__2" id="fn__2" class="fn_bot">2)</a></sup> 
when the aspect ratio of the given width and height doesn't match that of the image, it will be cropped to the new ratio before resizing</div>
</div>
