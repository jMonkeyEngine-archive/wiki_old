---
title: Formatting Syntax
---
<h1 class="sectionedit1" id="formatting_syntax">Formatting Syntax</h1>
<div class="level1">

<p>
<a href="http://www.dokuwiki.org/DokuWiki" class="interwiki iw_doku" title="http://www.dokuwiki.org/DokuWiki">DokuWiki</a> supports some simple markup language, which tries to make the datafiles to be as readable as possible. This page contains all possible syntax you may use when editing the pages. Simply have a look at the source of this page by pressing the <em>Edit this page</em> button at the top or bottom of the page. If you want to try something, just use the <a href="/playground/playground.html" class="wikilink1" title="playground:playground">playground</a> page. The simpler markup is easily accessible via <a href="http://www.dokuwiki.org/toolbar" class="interwiki iw_doku" title="http://www.dokuwiki.org/toolbar">quickbuttons</a>, too.
</p>

</div>
<!-- EDIT1 SECTION "Formatting Syntax" [1-518] -->
<h2 class="sectionedit2" id="basic_text_formatting">Basic text formatting</h2>
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
<!-- EDIT2 SECTION "Basic text formatting" [519-1655] -->
<h2 class="sectionedit3" id="links">Links</h2>
<div class="level2">

<p>
DokuWiki supports multiple ways of creating links.
</p>

</div>
<!-- EDIT3 SECTION "Links" [1656-1726] -->
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
<!-- EDIT4 SECTION "External" [1727-2317] -->
<h3 class="sectionedit5" id="internal">Internal</h3>
<div class="level3">

<p>
Internal links are created by using square brackets. You can either just give a <a href="/doku.php/pages:wiki:pagename" class="wikilink2" title="pages:wiki:pagename" rel="nofollow">pagename</a> or use an additional <a href="/doku.php/pages:wiki:pagename" class="wikilink2" title="pages:wiki:pagename" rel="nofollow">link text</a>.
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
Linking to a specific section is possible, too. Just add the section name behind a hash character as known from <abbr title="HyperText Markup Language">HTML</abbr>. This links to <span class="curid"><a href="/pages/wiki/syntax.html" class="wikilink1" title="pages:wiki:syntax">this Section</a></span>.
</p>
<pre class="code">This links to [[syntax#internal|this Section]].</pre>

<p>
Notes:
</p>
<ul>
<li class="level1"><div class="li"> Links to <span class="curid"><a href="/pages/wiki/syntax.html" class="wikilink1" title="pages:wiki:syntax">existing pages</a></span> are shown in a different style from <a href="/doku.php/pages:wiki:nonexisting" class="wikilink2" title="pages:wiki:nonexisting" rel="nofollow">nonexisting</a> ones.</div>
</li>
<li class="level1"><div class="li"> DokuWiki does not use <a href="http://en.wikipedia.org/wiki/CamelCase" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/CamelCase">CamelCase</a> to automatically create links by default, but this behavior can be enabled in the <a href="http://www.dokuwiki.org/config" class="interwiki iw_doku" title="http://www.dokuwiki.org/config">config</a> file. Hint: If DokuWiki is a link, then it's enabled.</div>
</li>
<li class="level1"><div class="li"> When a section's heading is changed, its bookmark changes, too. So don't rely on section linking too much.</div>
</li>
</ul>

</div>
<!-- EDIT5 SECTION "Internal" [2318-3553] -->
<h3 class="sectionedit6" id="interwiki">Interwiki</h3>
<div class="level3">

<p>
DokuWiki supports <a href="http://www.dokuwiki.org/Interwiki" class="interwiki iw_doku" title="http://www.dokuwiki.org/Interwiki">Interwiki</a> links. These are quick links to other Wikis. For example this is a link to Wikipedia's page about Wikis: <a href="http://en.wikipedia.org/wiki/Wiki" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/Wiki">Wiki</a>.
</p>
<pre class="code">DokuWiki supports [[doku&gt;Interwiki]] links. These are quick links to other Wikis.
For example this is a link to Wikipedia's page about Wikis: [[wp&gt;Wiki]].</pre>

</div>
<!-- EDIT6 SECTION "Interwiki" [3554-3891] -->
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
<li class="level1"><div class="li"> For Mozilla and Firefox it can be enabled through the config option <a href="http://www.mozilla.org/quality/networking/docs/netprefs.html#file" class="urlextern" title="http://www.mozilla.org/quality/networking/docs/netprefs.html#file" rel="nofollow">security.checkloaduri</a> but this is not recommended.</div>
</li>
<li class="level1"><div class="li"> See <a href="http://bugs.dokuwiki.org/index.php?do=details&amp;task_id=151" class="interwiki iw_dokubug" title="http://bugs.dokuwiki.org/index.php?do=details&amp;task_id=151">151</a> for more info.</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Windows Shares" [3892-4538] -->
<h3 class="sectionedit8" id="image_links">Image Links</h3>
<div class="level3">

<p>
You can also use an image to link to another internal or external page by combining the syntax for links and <a href="#images_and_other_files" title="pages:wiki:syntax ↵" class="wikilink1">images</a> (see below) like this:
</p>
<pre class="code">[[http://www.php.net|{{wiki:dokuwiki-128.png}}]]</pre>

<p>
<a href="/resources/wiki-dokuwiki-128.png" class="media" title="http://www.php.net" rel="nofollow"><img src="/resources/wiki-dokuwiki-128.png" class="media" alt="" /></a>
</p>

<p>
Please note: The image formatting is the only formatting syntax accepted in link names.
</p>

<p>
The whole <a href="#images_and_other_files" title="pages:wiki:syntax ↵" class="wikilink1">image</a> and <a href="#links" title="pages:wiki:syntax ↵" class="wikilink1">link</a> syntax is supported (including image resizing, internal and external images and URLs and interwiki links).
</p>

</div>
<!-- EDIT8 SECTION "Image Links" [4539-5092] -->
<h2 class="sectionedit9" id="footnotes">Footnotes</h2>
<div class="level2">

<p>
You can add footnotes <sup><a href="#fn__1" id="fnt__1" class="fn_top">1)</a></sup> by using double parentheses.
</p>
<pre class="code">You can add footnotes ((This is a footnote)) by using double parentheses.</pre>

</div>
<!-- EDIT9 SECTION "Footnotes" [5093-5267] -->
<h2 class="sectionedit10" id="sectioning">Sectioning</h2>
<div class="level2">

<p>
You can use up to five different levels of headlines to structure your content. If you have more than three headlines, a table of contents is generated automatically – this can be disabled by including the string <code>~~NOTOC~~</code> in the document.
</p>

</div>
<!-- EDIT10 SECTION "Sectioning" [5268-5554] -->
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
<!-- EDIT11 SECTION "Headline Level 3" [5555-5781] -->
<h2 class="sectionedit12" id="images_and_other_files">Images and other files</h2>
<div class="level2">

<p>
You can include external and internal <a href="http://www.dokuwiki.org/images" class="interwiki iw_doku" title="http://www.dokuwiki.org/images">images</a> with curly brackets. Optionally you can specify the size of them.
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
If you specify a filename (external or internal) that is not an image (<code>gif, jpeg, png</code>), then it will be displayed as a link instead.
</p>

<p>
For linking an image to another page see <a href="#image_links" title="pages:wiki:syntax ↵" class="wikilink1">Image Links</a> above.
</p>

</div>
<!-- EDIT12 SECTION "Images and other files" [5782-7254] -->
<h2 class="sectionedit13" id="lists">Lists</h2>
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

</div>
<!-- EDIT13 SECTION "Lists" [7255-7851] -->
<h2 class="sectionedit14" id="smileys">Smileys</h2>
<div class="level2">

<p>
DokuWiki converts commonly used <a href="http://en.wikipedia.org/wiki/emoticon" class="interwiki iw_wp" title="http://en.wikipedia.org/wiki/emoticon">emoticon</a>s to their graphical equivalents. More smileys can be placed in the <code>smiley</code> directory and configured in the <code>conf/smileys.conf</code> file. Here is an overview of Smileys included in DokuWiki.
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
</ul>
<ul>
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
<!-- EDIT14 SECTION "Smileys" [7852-8525] -->
<h2 class="sectionedit15" id="typography">Typography</h2>
<div class="level2">

<p>
<a href="/pages/wiki/dokuwiki.html" class="wikilink1" title="pages:wiki:dokuwiki">DokuWiki</a> can convert simple text characters to their typographically correct entities. Here is an example of recognized characters.
</p>

<p>
→ ← ↔ ⇒ ⇐ ⇔ » « – — 640×480 © ™ ®
“He thought 'It's a man's world'…”
</p>
<pre class="code">-&gt; &lt;- &lt;-&gt; =&gt; &lt;= &lt;=&gt; &gt;&gt; &lt;&lt; -- --- 640x480 (c) (tm) (r)
"He thought 'It's a man's world'..."</pre>

<p>
Please note: These conversions can be turned off through a <a href="http://www.dokuwiki.org/config%3Atypography" class="interwiki iw_doku" title="http://www.dokuwiki.org/config%3Atypography">config option</a> and a <a href="http://www.dokuwiki.org/entities" class="interwiki iw_doku" title="http://www.dokuwiki.org/entities">pattern file</a>.
</p>

</div>
<!-- EDIT15 SECTION "Typography" [8526-9024] -->
<h2 class="sectionedit16" id="quoting">Quoting</h2>
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
<!-- EDIT16 SECTION "Quoting" [9025-9397] -->
<h2 class="sectionedit17" id="tables">Tables</h2>
<div class="level2">

<p>
DokuWiki supports a simple syntax to create tables. 
</p>
<div class="table sectionedit18"><table class="inline">
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
		<td class="col0 leftalign"> Row 3 Col 1    </td><td class="col1 leftalign"> Row 2 Col 2     </td><td class="col2 leftalign"> Row 2 Col 3        </td>
	</tr>
</table></div>
<!-- EDIT18 TABLE [9472-9703] -->
<p>
Table rows have to start and end with a <code>|</code> for normal rows or a <code>^</code> for headers.
</p>
<pre class="code">^ Heading 1      ^ Heading 2       ^ Heading 3          ^
| Row 1 Col 1    | Row 1 Col 2     | Row 1 Col 3        |
| Row 2 Col 1    | some colspan (note the double pipe) ||
| Row 3 Col 1    | Row 2 Col 2     | Row 2 Col 3        |</pre>

<p>
To connect cells horizontally, just make the next cell completely empty as shown above. Be sure to have always the same amount of cell separators!
</p>

<p>
Vertical tableheaders are possible, too.
</p>
<div class="table sectionedit19"><table class="inline">
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
<!-- EDIT19 TABLE [10223-10466] -->
<p>
As you can see, it's the cell separator before a cell which decides about the formatting:
</p>
<pre class="code">|              ^ Heading 1            ^ Heading 2          ^
^ Heading 3    | Row 1 Col 2          | Row 1 Col 3        |
^ Heading 4    | no colspan this time |                    |
^ Heading 5    | Row 2 Col 2          | Row 2 Col 3        |</pre>

<p>
Note: Vertical spans (rowspan) are not possible.
</p>

<p>
You can align the table contents, too. Just add at least two whitespaces at the opposite end of your text: Add two spaces on the left to align right, two spaces on the right to align left and two spaces at least at both ends for centered text.
</p>
<div class="table sectionedit20"><table class="inline">
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
<!-- EDIT20 TABLE [11107-11294] -->
<p>
This is how it looks in the source:
</p>
<pre class="code">^           Table with alignment           ^^^
|         right|    center    |left          |
|left          |         right|    center    |
| xxxxxxxxxxxx | xxxxxxxxxxxx | xxxxxxxxxxxx |</pre>

</div>
<!-- EDIT17 SECTION "Tables" [9398-11529] -->
<h2 class="sectionedit21" id="non-parsed_blocks">Non-parsed Blocks</h2>
<div class="level2">

<p>
You can include non-parsed blocks into your documents by either indenting them by at least two spaces (like used for the previous examples) or by using the tags <code>code</code> or <code>file</code>.
</p>
<pre class="code">This is preformatted code all spaces are preserved: like              &lt;-this</pre>
<pre class="file">This is pretty much the same, but you could use it to show that you quoted a file.  </pre>

<p>
To let the parser ignore an area completely (ie. do no formatting on it), enclose the area either with <code>nowiki</code> tags or even simpler, with double percent signs <code>%%</code>.
</p>

<p>

This is some text which contains addresses like this: http://www.splitbrain.org and **formatting**, but nothing is done with it.

</p>

<p>
See the source of this page to see how to use these blocks.
</p>

</div>
<!-- EDIT21 SECTION "Non-parsed Blocks" [11530-12336] -->
<h2 class="sectionedit22" id="syntax_highlighting">Syntax Highlighting</h2>
<div class="level2">

<p>
<a href="/wiki/dokuwiki.html" class="wikilink1" title="wiki:dokuwiki">DokuWiki</a> can highlight sourcecode, which makes it easier to read. It uses the <a href="http://qbnz.com/highlighter/" class="urlextern" title="http://qbnz.com/highlighter/" rel="nofollow">GeSHi</a> Generic Syntax Highlighter – so any language supported by GeSHi is supported. The syntax is the same like in the code block in the previous section, but this time the name of the used language is inserted inside the tag. Eg. <code>&lt;code java&gt;</code>.
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
The following language strings are currently recognized: <em>abap, actionscript-french, actionscript, actionscript3, ada, apache, applescript, asm, asp, autoit, bash, basic4gl, blitzbasic, bnf, boo, c, c_mac, caddcl, cadlisp, cfdg, cfm, cil, cobol, cpp, cpp-qt, csharp, css, delphi, diff, div, dos, dot, d, eiffel, fortran, freebasic, genero, glsl, gml, gnuplot, groovy, gettext, haskell, html, idl, ini, inno, io, java5, java, javascript, kixtart, klonec, klonecpp, latex, lisp, lotusformulas, lotusscript, lua, m68k, matlab, mirc, mpasm, mxml, mysql, nsis, objc, ocaml-brief, ocaml, oobas, oracle8, pascal, perl, per, php-brief, php, pic16, plsql, povray, powershell, progress, python, qbasic, rails, reg, robots, ruby, sas, scala, scheme, sdlbasic, smalltalk, smarty, sql, tcl, text, thinbasic, tsql, typoscript, vbnet, vb, verilog, vhdl, visualfoxpro, winbatch, xml, xorg_conf, xpp, z80</em>
</p>

</div>
<!-- EDIT22 SECTION "Syntax Highlighting" [12337-13936] -->
<h2 class="sectionedit23" id="rss_atom_feed_aggregation">RSS/ATOM Feed Aggregation</h2>
<div class="level2">

<p>
<a href="/pages/wiki/dokuwiki.html" class="wikilink1" title="pages:wiki:dokuwiki">DokuWiki</a> can integrate data from external XML feeds. For parsing the XML feeds, <a href="http://simplepie.org/" class="urlextern" title="http://simplepie.org/" rel="nofollow">SimplePie</a> is used. All formats understood by SimplePie can be used in DokuWiki as well. You can influence the rendering by multiple additional space separated parameters:
</p>
<div class="table sectionedit24"><table class="inline">
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
<!-- EDIT24 TABLE [14257-14697] -->
<p>
The refresh period defaults to 4 hours. Any value below 10 minutes will be treated as 10 minutes. <a href="/wiki/dokuwiki.html" class="wikilink1" title="wiki:dokuwiki">DokuWiki</a> will generally try to supply a cached version of a page, obviously this is inappropriate when the page contains dynamic external content. The parameter tells <a href="/wiki/dokuwiki.html" class="wikilink1" title="wiki:dokuwiki">DokuWiki</a> to re-render the page if it is more than <em>refresh period</em> since the page was last rendered.
</p>

<p>
<strong>Example:</strong>
</p>
<pre class="code">{{rss&gt;http://slashdot.org/index.rss 5 author date 1h }}</pre>
<ul class="rss"><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/J_pjEdfxCuE/how-an-irs-agent-stole-1m-from-taxpayers" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/J_pjEdfxCuE/how-an-irs-agent-stole-1m-from-taxpayers" rel="nofollow">How an IRS Agent Stole $1M From Taxpayers</a> by Soulskill (2016/01/05 18:53)</div></li><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/QvA2I323z-Q/gene-roddenberrys-floppy-disks-recovered" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/QvA2I323z-Q/gene-roddenberrys-floppy-disks-recovered" rel="nofollow">Gene Roddenberry's Floppy Disks Recovered</a> by Soulskill (2016/01/05 18:10)</div></li><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/pvCDF-Xeszw/comcasts-xfinity-home-security-flaw-leaves-doors-open" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/pvCDF-Xeszw/comcasts-xfinity-home-security-flaw-leaves-doors-open" rel="nofollow">Comcast's Xfinity Home Security Flaw Leaves Doors Open</a> by Soulskill (2016/01/05 17:28)</div></li><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/pMrkiYdJlts/brazil-cautions-women-to-avoid-pregnancy-over-zika-virus-outbreak" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/pMrkiYdJlts/brazil-cautions-women-to-avoid-pregnancy-over-zika-virus-outbreak" rel="nofollow">Brazil Cautions Women To Avoid Pregnancy Over Zika Virus Outbreak</a> by Soulskill (2016/01/05 16:48)</div></li><li><div class="li"><a href="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/hgfC4FEs7p0/nsa-targeted-the-two-leading-encryption-chips" class="urlextern" title="http://rss.slashdot.org/~r/Slashdot/slashdot/~3/hgfC4FEs7p0/nsa-targeted-the-two-leading-encryption-chips" rel="nofollow">NSA Targeted 'The Two Leading' Encryption Chips</a> by Soulskill (2016/01/05 16:15)</div></li></ul>
</div>
<!-- EDIT23 SECTION "RSS/ATOM Feed Aggregation" [13937-15216] -->
<h2 class="sectionedit25" id="embedding_html_and_php">Embedding HTML and PHP</h2>
<div class="level2">

<p>
You can embed raw <abbr title="HyperText Markup Language">HTML</abbr> or PHP code into your documents by using the <code>html</code> or <code>php</code> tags like this:
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
<pre class="code html4strict"><span class="sc2">&lt;<a href="http://december.com/html/4/element/p.html"><span class="kw2">p</span></a> <span class="kw3">style</span><span class="sy0">=</span><span class="st0">"border:2px dashed red;"</span>&gt;</span>And this is some block HTML<span class="sc2">&lt;<span class="sy0">/</span><a href="http://december.com/html/4/element/p.html"><span class="kw2">p</span></a>&gt;</span></pre><pre class="code">&lt;php&gt;
echo 'A logo generated by PHP:';
echo '&lt;img src="' . $_SERVER['PHP_SELF'] . '?=' . php_logo_guid() . '" alt="PHP Logo !" /&gt;';
echo '(generated inline HTML)';
&lt;/php&gt;
&lt;PHP&gt;
echo '&lt;table class="inline"&gt;&lt;tr&gt;&lt;td&gt;The same, but inside a block level element:&lt;/td&gt;';
echo '&lt;td&gt;&lt;img src="' . $_SERVER['PHP_SELF'] . '?=' . php_logo_guid() . '" alt="PHP Logo !" /&gt;&lt;/td&gt;';
echo '&lt;/tr&gt;&lt;/table&gt;';
&lt;/PHP&gt;</pre>

<p>
<code class="code php"><span class="kw1">echo</span> <span class="st_h">'A logo generated by PHP:'</span><span class="sy0">;</span>
<span class="kw1">echo</span> <span class="st_h">'&lt;img src="'</span> <span class="sy0">.</span> <span class="re0">$_SERVER</span><span class="br0">[</span><span class="st_h">'PHP_SELF'</span><span class="br0">]</span> <span class="sy0">.</span> <span class="st_h">'?='</span> <span class="sy0">.</span> <a href="http://www.php.net/php_logo_guid"><span class="kw3">php_logo_guid</span></a><span class="br0">(</span><span class="br0">)</span> <span class="sy0">.</span> <span class="st_h">'" alt="PHP Logo !" /&gt;'</span><span class="sy0">;</span>
<span class="kw1">echo</span> <span class="st_h">'(inline HTML)'</span><span class="sy0">;</span></code>
</p>
<pre class="code php"><span class="kw1">echo</span> <span class="st_h">'&lt;table class="inline"&gt;&lt;tr&gt;&lt;td&gt;The same, but inside a block level element:&lt;/td&gt;'</span><span class="sy0">;</span>
<span class="kw1">echo</span> <span class="st_h">'&lt;td&gt;&lt;img src="'</span> <span class="sy0">.</span> <span class="re0">$_SERVER</span><span class="br0">[</span><span class="st_h">'PHP_SELF'</span><span class="br0">]</span> <span class="sy0">.</span> <span class="st_h">'?='</span> <span class="sy0">.</span> <a href="http://www.php.net/php_logo_guid"><span class="kw3">php_logo_guid</span></a><span class="br0">(</span><span class="br0">)</span> <span class="sy0">.</span> <span class="st_h">'" alt="PHP Logo !" /&gt;&lt;/td&gt;'</span><span class="sy0">;</span>
<span class="kw1">echo</span> <span class="st_h">'&lt;/tr&gt;&lt;/table&gt;'</span><span class="sy0">;</span></pre>
<p>
<strong>Please Note</strong>: <abbr title="HyperText Markup Language">HTML</abbr> and PHP embedding is disabled by default in the configuration. If disabled, the code is displayed instead of executed.
</p>

</div>
<!-- EDIT25 SECTION "Embedding HTML and PHP" [15217-16648] -->
<h2 class="sectionedit26" id="control_macros">Control Macros</h2>
<div class="level2">

<p>
Some syntax influences how DokuWiki renders a page without creating any output it self. The following control macros are availble:
</p>
<div class="table sectionedit27"><table class="inline">
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
<!-- EDIT27 TABLE [16809-17151] -->
</div>
<!-- EDIT26 SECTION "Control Macros" [16649-17152] -->
<h2 class="sectionedit28" id="syntax_plugins">Syntax Plugins</h2>
<div class="level2">

<p>
DokuWiki's syntax can be extended by <a href="http://www.dokuwiki.org/plugins" class="interwiki iw_doku" title="http://www.dokuwiki.org/plugins">Plugins</a>. How the installed plugins are used is described on their appropriate description pages. The following syntax plugins are available in this particular DokuWiki installation:
</p>
<ul><li><div class="li"><a href="http://dokuwiki.org/plugin:info" class="urlextern" title="http://dokuwiki.org/plugin:info" rel="nofollow">Info Plugin</a> <em>2014-03-05</em> by <a href="mailto:andi@splitbrain.org" class="mail" title="andi@splitbrain.org">Andreas Gohr</a><br />Displays information about various DokuWiki internals</div></li><li><div class="li"><a href="http://www.dokuwiki.org/plugin:pagelist" class="urlextern" title="http://www.dokuwiki.org/plugin:pagelist" rel="nofollow">Pagelist Plugin</a> <em>2014-05-26</em> by <a href="mailto:michael@content-space.de" class="mail" title="michael@content-space.de">Matthias Schulte, Michael Hamann, Michael Klier, Gina Haeussge</a><br />Lists pages in a nice formatted way</div></li><li><div class="li"><a href="https://www.dokuwiki.org/plugin:siteexport" class="urlextern" title="https://www.dokuwiki.org/plugin:siteexport" rel="nofollow">Site Export</a> <em>2015-10-15</em> by <a href="mailto:tools@inetsoftware.de" class="mail" title="tools@inetsoftware.de">i-net software</a><br />exports the dokuwiki site in the given format</div></li><li><div class="li"><a href="https://www.dokuwiki.org/plugin:tag" class="urlextern" title="https://www.dokuwiki.org/plugin:tag" rel="nofollow">tag plugin</a> <em>2014-02-16</em> by <a href="mailto:michael@content-space.de" class="mail" title="michael@content-space.de">Michael Hamann, Gina Häussge, Christopher Smith, Michael Klier, Esther Brunner</a><br />tag wiki pages</div></li><li><div class="li"><a href="http://www.dokuwiki.org/plugin:iframe" class="urlextern" title="http://www.dokuwiki.org/plugin:iframe" rel="nofollow">iframe Plugin</a> <em>2008-10-31</em> by <a href="mailto:chris@jalakai.co.uk" class="mail" title="chris@jalakai.co.uk">Christopher Smith</a><br />Add an iframe containing the specified url<br />                     syntax: {{url&gt;http://www.somesite.com/somepage.htm [w,h]|alternate text}}</div></li><li><div class="li"><a href="http://www.dokuwiki.org/plugin:note" class="urlextern" title="http://www.dokuwiki.org/plugin:note" rel="nofollow">Note Plugin</a> <em>2009-06-15</em> by <a href="mailto:olive@deep-ocean.net" class="mail" title="olive@deep-ocean.net">Olivier Cortès / Eric Hameleers / Christopher Smith / Aurélien Bompard</a><br />Add Note/Important/Tip/Warning Capability (DIV+CSS box)</div></li></ul>
</div>
<!-- EDIT28 SECTION "Syntax Plugins" [17153-] --><div class="footnotes">
<div class="fn"><sup><a href="#fnt__1" id="fn__1" class="fn_bot">1)</a></sup> 
This is a footnote</div>
<div class="fn"><sup><a href="#fnt__2" id="fn__2" class="fn_bot">2)</a></sup> 
when the aspect ratio of the given width and height doesn't match that of the image, it will be cropped to the new ratio before resizing</div>
</div>
