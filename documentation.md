---
title: jMonkeyEngine Documentation
---
<h1 class="sectionedit1" id="jmonkeyengine_documentation">jMonkeyEngine Documentation</h1>
<div class="level1">

<p>
This documentation wiki contains installation and configuration guides, jME coding tutorials and other information that will help you get your game project going. You can search the contents of this wiki using the search box in the upper right.
</p>

<p>
You are also very welcome to fix mistakes or spelling as well as unclear paragraphs using the “Wiki” menu on top or the “Edit” buttons after each paragraph. You have to be logged in to edit the wiki.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine Documentation" [1-489] -->
<h2 class="sectionedit2" id="install">Install</h2>
<div class="level2">

<p>
<strong>Before installing, check the <a href="/bsd_license.html" class="wikilink1" title="bsd_license">license</a>, <a href="/jme3/features.html" class="wikilink1" title="jme3:features">features</a>, and <a href="/jme3/requirements.html" class="wikilink1" title="jme3:requirements">requirements</a>.</strong> Then choose one of these options:
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0"> </td><th class="col1 leftalign"> Recommended     </th><th class="col2 leftalign"> Optional       </th><th class="col3 leftalign"> Optional  </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> You want to… </th><td class="col1"> Get started with jMonkeyEngine </td><td class="col2"> Use jMonkeyEngine in another IDE </td><td class="col3"> Build custom engine from sources </td>
	</tr>
	<tr class="row2">
		<th class="col0"> Then download… </th><td class="col1"> <a href="http://jmonkeyengine.org/downloads/" class="urlextern" title="http://jmonkeyengine.org/downloads/" rel="nofollow">jMonkeyEngine SDK</a> </td><td class="col2"> <a href="http://updates.jmonkeyengine.org/stable" class="urlextern" title="http://updates.jmonkeyengine.org/stable" rel="nofollow">Binaries</a> </td><td class="col3"> <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine" rel="nofollow">Sources (Subversion)</a> </td>
	</tr>
	<tr class="row3">
		<th class="col0"> You receive… </th><td class="col1"> Sources, binaries, javadoc, SDK </td><td class="col2"> Latest stable binary build, sources, javadoc. </td><td class="col3"> Sources </td>
	</tr>
	<tr class="row4">
		<th class="col0"> Learn more here… </th><td class="col1"> <a href="/sdk.html" class="wikilink1" title="sdk">Using the SDK</a> <br />
<a href="/sdk/project_creation.html" class="wikilink1" title="sdk:project_creation">Project Creation</a> <br />
<a href="/resources/sdk-jme3-jmonkeyplatform.png" class="media" title="sdk:jme3-jmonkeyplatform.png"><img src="/resources/sdk-jme3-jmonkeyplatform.png" class="mediacenter" alt="" width="144" height="90" /></a> </td><td class="col2"> <a href="/jme3/maven.html" class="wikilink1" title="jme3:maven">Setting up jME3 with maven compatible IDEs</a> * <br />
<a href="/jme3/setting_up_netbeans_and_jme3.html" class="wikilink1" title="jme3:setting_up_netbeans_and_jme3">Setting up JME3 in the NetBeans IDE</a> * <br />
<a href="/jme3/setting_up_jme3_in_eclipse.html" class="wikilink1" title="jme3:setting_up_jme3_in_eclipse">Setting up JME3 in the Eclipse IDE</a> * <br />
<a href="/jme3/eclipse_jme3_android_jnindk.html" class="wikilink1" title="jme3:eclipse_jme3_android_jnindk">Setting up JME3 in the Eclipse IDE (with Android and/or JNI/NDK)</a> * </td><td class="col3"> <a href="/jme3/build_from_sources.html" class="wikilink1" title="jme3:build_from_sources">Building JME3 from the Sources</a> <br />
<a href="/jme3/build_jme3_sources_with_netbeans.html" class="wikilink1" title="jme3:build_jme3_sources_with_netbeans">Building JME3 from the sources with NetBeans</a> <br />
<a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline">Setting up JME3 on the commandline</a> </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [651-1833] -->
<p>
(*) The SDK creates Ant-based projects that any Java IDE can import. We recommend users of other IDEs to also download the jMonkeyEngine SDK and choose “File→Import Project→External Project Assets” to create a codeless project for managing assets only. This way you can code in the IDE of your choice, and use the SDK to convert your models to .j3o format.
</p>

</div>
<!-- EDIT2 SECTION "Install" [490-2193] -->
<h2 class="sectionedit4" id="create">Create</h2>
<div class="level2">

<p>
After downloading and installing, <a href="/jme3.html" class="wikilink1" title="jme3">bookmark the jME Documentation page</a> and start writing your first game!
</p>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Tutorials </th><th class="col1"> jMonkeyEngine SDK </th><th class="col2"> Other Documentation </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">jME3 beginner tutorials</a> </td><td class="col1"> <a href="/sdk.html" class="wikilink1" title="sdk">jMonkeyEngine SDK Documentation and Video Tutorials</a> </td><td class="col2"> <a href="http://javadoc.jmonkeyengine.org/" class="urlextern" title="http://javadoc.jmonkeyengine.org/" rel="nofollow">Full API JavaDoc</a> </td>
	</tr>
	<tr class="row2">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">jME3 intermediate articles</a> </td><td class="col1"> <a href="/sdk/comic.html" class="wikilink1" title="sdk:comic">jMonkeyEngine SDK - the Comic :-)</a> </td><td class="col2"> <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">Blender Modeling Guide</a> </td>
	</tr>
	<tr class="row3">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">jME3 advanced documentation</a> </td><td class="col1 leftalign">  </td><td class="col2"> <a href="/jme3/faq.html" class="wikilink1" title="jme3:faq">Answers to Frequently Asked Questions</a> </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [2330-2880] -->
</div>
<!-- EDIT4 SECTION "Create" [2194-2881] -->
<h2 class="sectionedit6" id="contribute">Contribute</h2>
<div class="level2">

<p>
Are you an experienced Java developer who wants to add new features or contribute patches to the jME3 project?
</p>
<ul>
<li class="level1"><div class="li"> Get inspired by existing <a href="/jme3/contributions.html" class="wikilink1" title="jme3:contributions">contributions</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/introduction/contributors-handbook/" class="urlextern" title="http://hub.jmonkeyengine.org/introduction/contributors-handbook/" rel="nofollow">Read the Contributors Handbook</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/" class="urlextern" title="http://hub.jmonkeyengine.org/" rel="nofollow">Chime in on the Contributors Forum</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/jme3_source_structure.html" class="wikilink1" title="jme3:jme3_source_structure">Learn about the source structure</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk.html" class="wikilink1" title="sdk">Write jMonkeyEngine SDK plugins and visual editors</a></div>
</li>
<li class="level1"><div class="li"> <a href="/report_bugs.html" class="wikilink1" title="report_bugs">Report bugs and submit patches</a></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Contribute" [2882-3439] -->
<h2 class="sectionedit7" id="contact">Contact</h2>
<div class="level2">

<p>
You are welcome to contribute and inquire about the project: Please <a href="mailto:contact@jmonkeyengine.com" class="mail" title="contact@jmonkeyengine.com">contact</a> the <a href="http://jmonkeyengine.org/team/" class="urlextern" title="http://jmonkeyengine.org/team/" rel="nofollow">developers</a> or ask on the <a href="http://hub.jmonkeyengine.org/" class="urlextern" title="http://hub.jmonkeyengine.org/" rel="nofollow">forums</a>.
</p>
<ul>
<li class="level1"><div class="li"> <a href="mailto:contact@jmonkeyengine.com" class="mail" title="contact@jmonkeyengine.com">Contact the jME team</a></div>
<ul>
<li class="level2"><div class="li"> <a href="http://jmonkeyengine.org/team/" class="urlextern" title="http://jmonkeyengine.org/team/" rel="nofollow">Core team - Who are we?</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="/report_bugs.html" class="wikilink1" title="report_bugs">Report a bug</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/c/documentation-jme3" class="urlextern" title="http://hub.jmonkeyengine.org/c/documentation-jme3" rel="nofollow">Report unclear or missing documentation</a></div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Contact" [3440-3921] -->
<h2 class="sectionedit8" id="languages">Languages</h2>
<div class="level2">

<p>
<a href="/doku.php/%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F" class="wikilink2" title="документация" rel="nofollow">Документация на Русском</a> <br />

<a href="/documentacao.html" class="wikilink1" title="documentacao">Documentação em Português</a> <br />

<a href="/documentation_zh.html" class="wikilink1" title="documentation_zh">中文版</a>
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Languages" [3922-] -->
