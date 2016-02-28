---
title: Einführung in die jMonkeyEngine 3.0
---
<h1 class="sectionedit1" id="einfuehrung_in_die_jmonkeyengine_30">Einführung in die jMonkeyEngine 3.0</h1>
<div class="level1">

<p>
<strong>Du bist Java Entwickler und möchtest 3D Spiele schreiben, die auf Windows, Mac, Linux, im Webbrowser, und auf der Android Plattform laufen? Dann bist du hier richtig! Das jMonkeyEngine Framework (jME) ist eine leistungsstarke, 3D Szenen-basierte Grafik <abbr title="Application Programming Interface">API</abbr> mit <a href="/jme3/features.html" class="wikilink1" title="jme3:features">modernen Features</a>.</strong>
</p>

<p>
Die jMonkeyEngine 3 ist ein Bündel aus JAR Dateien, das du in den Java Classpath platzierst. Die Software ist in Java geschrieben und nutzt LWJGL für den Zugriff auf OpenGL. Die jMonkeyEngine Open Source Community gibt diese Bibliotheken lizensiert unter der <a href="/bsd_license.html" class="wikilink1" title="bsd_license">BSD Lizenz</a> heraus, welche sie jedem frei zur Verfügung stellt, so wie er sie benötigt – sei es für das eigene Hobby, für Lehrzwecke, oder kommerziell.
</p>

<p>
Die dritte Version der jMonkeyEngine ist nun im Beta Stadium. Du nutzt noch die <a href="http://jme2.jmonkeyengine.org/" class="urlextern" title="http://jme2.jmonkeyengine.org/" rel="nofollow">jME2</a>? Dann lies doch bitte unsere <a href="/choose-jme2-or-jme3.html" class="wikilink1" title="choose-jme2-or-jme3">Begründung für die Wahl der jME2 oder jME3</a> und den <a href="/compare-jme2-jme3.html" class="wikilink1" title="compare-jme2-jme3">jME2/jME3 Feature-Vergleich</a> und beginne mit dem Portieren zur jME3.
</p>

</div>

<h4 id="was_ist_das_jmonkeyengine_sdk">Was ist das jMonkeyEngine SDK?</h4>
<div class="level4">

<p>
Das <a href="http://jmonkeyengine.org/downloads/" class="urlextern" title="http://jmonkeyengine.org/downloads/" rel="nofollow">jMonkeyEngine3 SDK</a> ist ein vorkonfiguriertes Software-Entwicklungskit, maßgeschneidert für Java Spielentwickler. Das SDK kombiniert alle jME3 Bibliotheken und einige <a href="/sdk.html" class="wikilink1" title="sdk">einmalige Entwickler Werkzeuge</a>, die dir das Leben leichter machen, wenn du in Java programmierst und deine Projekte managst. Das SDK beinhaltet Projekt- und Dateiassistenten, einen erweiterten Code Editor, Spieldaten-Management, Dateikonverter, Szenenbetrachter und -designer, eine Codeschnipselablage, einen Terrain-Editor, und vieles mehr.
</p>

</div>
<!-- EDIT1 SECTION "Einführung in die jMonkeyEngine 3.0" [1-1712] -->
<h2 class="sectionedit2" id="installation">Installation</h2>
<div class="level2">

<p>
<strong>Bevor du die Installation startest, lies dir die <a href="/bsd_license.html" class="wikilink1" title="bsd_license">Lizenz</a> durch, <a href="/jme3/features.html" class="wikilink1" title="jme3:features">die jME3 Features</a>, und die <a href="/jme3/requirements.html" class="wikilink1" title="jme3:requirements">Systemanforderungen</a>.</strong> Wähle dann eine der folgenden Optionen:
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0"> </td><th class="col1 leftalign"> Empfohlen     </th><th class="col2 leftalign"> Optional       </th><th class="col3 leftalign"> Optional  </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> Du möchtest … </th><td class="col1"> Dich mit der jMonkeyEngine vertraut machen </td><td class="col2"> Die jMonkeyEngine in einer anderen IDE nutzen </td><td class="col3"> Eine benutzerdefinierte Engine aus dem Quellcode erstellen </td>
	</tr>
	<tr class="row2">
		<th class="col0"> Dann downloade … </th><td class="col1"> <a href="http://jmonkeyengine.org/downloads/" class="urlextern" title="http://jmonkeyengine.org/downloads/" rel="nofollow">Das jMonkeyEngine SDK</a> </td><td class="col2"> <a href="http://nightly.jmonkeyengine.org/" class="urlextern" title="http://nightly.jmonkeyengine.org/" rel="nofollow">Binäre Dateien</a> </td><td class="col3"> <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine" rel="nofollow">Denn Quellcode (Subversion)</a> </td>
	</tr>
	<tr class="row3">
		<th class="col0"> Du bekommst … </th><td class="col1"> Quellcode, binäre Dateien, JavaDoc, SDK </td><td class="col2"> Den aktuellsten nightly build, Quellcodes, JavaDoc. </td><td class="col3"> Quellcodes </td>
	</tr>
	<tr class="row4">
		<th class="col0"> Erfahre mehr … </th><td class="col1"> <a href="/sdk.html" class="wikilink1" title="sdk">Benutzung des SDK</a> <br />
<a href="/sdk/project_creation.html" class="wikilink1" title="sdk:project_creation">Projekte erstellen</a> <br />
<a href="/resources/sdk-jme3-jmonkeyplatform.png" class="media" title="sdk:jme3-jmonkeyplatform.png"><img src="/resources/sdk-jme3-jmonkeyplatform.png" class="mediacenter" alt="" width="144" height="90" /></a> </td><td class="col2"> <a href="/jme3/setting_up_netbeans_and_jme3.html" class="wikilink1" title="jme3:setting_up_netbeans_and_jme3">Nutzung der jME3 in NetBeans</a> * <br />
<a href="/jme3/setting_up_jme3_in_eclipse.html" class="wikilink1" title="jme3:setting_up_jme3_in_eclipse">Nutzung der jME3 in Eclipse</a> * </td><td class="col3"> <a href="/jme3/build_from_sources.html" class="wikilink1" title="jme3:build_from_sources">Kompilieren der jME3 aus den Quellcodes</a> <br />
<a href="/jme3/build_jme3_sources_with_netbeans.html" class="wikilink1" title="jme3:build_jme3_sources_with_netbeans">Kompilieren der jME3 aus den Quellcodes mit NetBeans</a> <br />
<a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline">Einrichtung der jME3 über die Kommandozeileneingabe</a> </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [1953-3091] -->
<p>
(*) Das SDK erstellt Ant-basierte Projekte, welche jede Java IDE importieren kann. Wir empfehlen Benutzern anderer IDEs sich ebenfalls das jMonkeyEngine SDK herunterzuladen und die Spieldaten dann zu importieren (File→Import Project→External Project Assets), um die Spieldaten gesondert verwalten zu können, ohne Code. So kannst du mit der IDE deiner Wahl Code schreiben, und gleichzeitig das SDK nutzen, um deine Modelle in das .j3o Format zu konvertieren.
</p>

</div>
<!-- EDIT2 SECTION "Installation" [1713-3554] -->
<h2 class="sectionedit4" id="entwicklung_des_ersten_eigenen_spiels">Entwicklung des ersten, eigenen Spiels</h2>
<div class="level2">

<p>
Nachdem du alles heruntergeladen und installiert hast, <a href="/jme3.html" class="wikilink1" title="jme3">lege dir ein Lesezeichen für die jME3 Dokumentation an</a>. Dann kann es auch schon losgehen mit der Entwicklung deines ersten, eigenen Spiels! ;)
</p>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Tutorials </th><th class="col1"> jMonkeyEngine SDK </th><th class="col2"> Andere Dokumentationen </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">jME3 Einsteiger Tutorial</a> </td><td class="col1"> <a href="/sdk.html" class="wikilink1" title="sdk">jMonkeyEngine SDK Dokumentation und Video Tutorials</a> </td><td class="col2"> <a href="http://jmonkeyengine.org/javadoc/" class="urlextern" title="http://jmonkeyengine.org/javadoc/" rel="nofollow">Komplettes API JavaDoc</a> </td>
	</tr>
	<tr class="row2">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">jME3 Doku für geübte Benutzer</a> </td><td class="col1"> <a href="/sdk/comic.html" class="wikilink1" title="sdk:comic">jMonkeyEngine SDK - der Comic :-)</a> </td><td class="col2"> <a href="/jme3/faq.html" class="wikilink1" title="jme3:faq">Antworten zu häufig gestellten Fragen</a> </td>
	</tr>
	<tr class="row3">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">jME3 Doku für fortgeschrittene Benutzer</a> </td><td class="col1"></td><td class="col2"></td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [3817-4342] -->
</div>
<!-- EDIT4 SECTION "Entwicklung des ersten, eigenen Spiels" [3555-4343] -->
<h2 class="sectionedit6" id="wenn_du_etwas_beitragen_moechtest">Wenn du etwas beitragen möchtest</h2>
<div class="level2">

<p>
Du bist ein erfahrener Java Entwickler und möchtest neue Features oder Verbesserungen in das jME3 Projekt einbringen?
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/introduction/contributors-handbook/" class="urlextern" title="http://jmonkeyengine.org/introduction/contributors-handbook/" rel="nofollow">Lies das Mitarbeiter Handbuch</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.jmonkeyengine.com/forum/index.php?board=30.0" class="urlextern" title="http://www.jmonkeyengine.com/forum/index.php?board=30.0" rel="nofollow">Klinke dich im Mitarbeiter Forum ein</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/jme3_source_structure.html" class="wikilink1" title="jme3:jme3_source_structure">Lerne die Quellcode Strukturen kennen</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk.html" class="wikilink1" title="sdk">Schreibe Plugins für das jME SDK und visuelle Editoren</a></div>
</li>
<li class="level1"><div class="li"> <a href="/report_bugs.html" class="wikilink1" title="report_bugs">Melde Fehler und reiche Patches ein</a></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Wenn du etwas beitragen möchtest" [4344-4918] -->
<h2 class="sectionedit7" id="kontakt">Kontakt</h2>
<div class="level2">

<p>
Gerne darfst du unser Projekt unterstützen, oder Fragen dazu stellen: Bitte <a href="mailto:contact@jmonkeyengine.com" class="mail" title="contact@jmonkeyengine.com">kontaktiere</a> die <a href="http://jmonkeyengine.org/team/" class="urlextern" title="http://jmonkeyengine.org/team/" rel="nofollow">Entwickler</a> oder frage im <a href="http://jmonkeyengine.org/forums" class="urlextern" title="http://jmonkeyengine.org/forums" rel="nofollow">Forum</a> nach.
</p>
<ul>
<li class="level1"><div class="li"> <a href="mailto:contact@jmonkeyengine.com" class="mail" title="contact@jmonkeyengine.com">Schreibe dem jME Team eine Mail!</a></div>
<ul>
<li class="level2"><div class="li"> <a href="http://jmonkeyengine.org/team/" class="urlextern" title="http://jmonkeyengine.org/team/" rel="nofollow">Das Kern-Team - Wer sind wir?</a></div>
</li>
<li class="level2"><div class="li"> <a href="http://jmonkeyengine.org/groups/contributor/members/" class="urlextern" title="http://jmonkeyengine.org/groups/contributor/members/" rel="nofollow">Mitarbeiter - Wer sind wir?</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/wiki/doku.php/report_bugs" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/report_bugs" rel="nofollow">Du hast einen Fehler gefunden? Hier kannst du ihn melden!</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://code.google.com/p/jmonkeyengine/issues/list?can=2&amp;q=label:Component-Docs" class="urlextern" title="http://code.google.com/p/jmonkeyengine/issues/list?can=2&amp;q=label:Component-Docs" rel="nofollow">Es fehlt etwas in der Doku? Bitte gib uns bescheid!</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>
</span></div>

</div>
<!-- EDIT7 SECTION "Kontakt" [4919-] -->
