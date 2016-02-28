---
title: jMonkeyEngine 说明文档
---
<h1 class="sectionedit1" id="jmonkeyengine_说明文档">jMonkeyEngine 说明文档</h1>
<div class="level1">

<p>
本wiki页面包含jME3的安装和配置指南、jME3编程教程以及其他一些能够帮助你开发游戏项目的资料，请善用本页右上方的搜索框来检索整个wiki中的内容。
</p>

<p>
本文翻译自英文版<a href="/documentation.html" class="wikilink1" title="documentation">jME文档</a>，受编者水平所限，难免存在各种各样的问题。如果您在阅读的过程中发现任何错误，非常欢迎您直接修正错误的内容。编辑此页面需要<a href="http://hub.jmonkeyengine.org" class="urlextern" title="http://hub.jmonkeyengine.org" rel="nofollow">官方论坛</a>账号，然后点击本页右上角的“Tools → Login”登录。登录后点击右上角“Tools → Edit this page”或者每个段落后面的“Edit”按钮，即可编辑此页面。
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 说明文档" [1-698] -->
<h2 class="sectionedit2" id="下载和安装">下载和安装</h2>
<div class="level2">

<p>
<strong>在安装之前，请查阅<a href="/bsd_license.html" class="wikilink1" title="bsd_license">许可证</a>、<a href="/doku.php/jme3:features_zh" class="wikilink2" title="jme3:features_zh" rel="nofollow">jME3功能说明</a>和<a href="/jme3/requirements_zh.html" class="wikilink1" title="jme3:requirements_zh">开发需求</a>，</strong> 然后选择其中一个选项：
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0"> </td><th class="col1 leftalign"> 推荐     </th><th class="col2 leftalign"> 可选       </th><th class="col3 leftalign"> 可选  </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> 你打算… </th><td class="col1"> 使用jMonkeyEngine SDK开发 </td><td class="col2"> 在其他的IDE中使用jMonkeyEngine </td><td class="col3"> 利用源码来编译自定义引擎 </td>
	</tr>
	<tr class="row2">
		<th class="col0"> 请下载… </th><td class="col1"> <a href="http://jmonkeyengine.org/downloads/" class="urlextern" title="http://jmonkeyengine.org/downloads/" rel="nofollow">jMonkeyEngine SDK</a> </td><td class="col2"> <a href="http://updates.jmonkeyengine.org/stable" class="urlextern" title="http://updates.jmonkeyengine.org/stable" rel="nofollow">Binaries</a> </td><td class="col3"> <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine" rel="nofollow">Sources (Subversion)</a> </td>
	</tr>
	<tr class="row3">
		<th class="col0"> 你会得到… </th><td class="col1"> Sources, binaries, javadoc, SDK </td><td class="col2"> Latest stable binary build, sources, javadoc. </td><td class="col3"> Sources </td>
	</tr>
	<tr class="row4">
		<th class="col0"> 更多学习内容… </th><td class="col1"> <a href="/doku.php/sdk_zh" class="wikilink2" title="sdk_zh" rel="nofollow">学习使用SDK</a> <br />
<a href="/doku.php/sdk:project_creation_zh" class="wikilink2" title="sdk:project_creation_zh" rel="nofollow">使用SDK创建工程</a> <br />
<a href="/resources/sdk-jme3-jmonkeyplatform.png" class="media" title="sdk:jme3-jmonkeyplatform.png"><img src="/resources/sdk-jme3-jmonkeyplatform.png" class="mediacenter" alt="" width="144" height="90" /></a> </td><td class="col2"> <a href="/doku.php/jme3:maven_zh" class="wikilink2" title="jme3:maven_zh" rel="nofollow">在任何兼容maven的IDE中集成JME3</a> * <br />
<a href="/doku.php/jme3:setting_up_netbeans_and_jme3_zh" class="wikilink2" title="jme3:setting_up_netbeans_and_jme3_zh" rel="nofollow">在NetBeans中集成JME3</a> * <br />
<a href="/jme3/setting_up_jme3_in_eclipse_zh.html" class="wikilink1" title="jme3:setting_up_jme3_in_eclipse_zh">在Eclipse中集成JME3</a> * <br />
<a href="/doku.php/jme3:eclipse_jme3_android_jnindk_zh" class="wikilink2" title="jme3:eclipse_jme3_android_jnindk_zh" rel="nofollow">在Eclipse(含Android及JNI/NDK)中集成JME3</a> * </td><td class="col3"> <a href="/doku.php/jme3:build_from_sources_zh" class="wikilink2" title="jme3:build_from_sources_zh" rel="nofollow">编译JME3源码</a> <br />
<a href="/doku.php/jme3:build_jme3_sources_with_netbeans_zh" class="wikilink2" title="jme3:build_jme3_sources_with_netbeans_zh" rel="nofollow">在NetBeans中编译JME3源码</a> <br />
<a href="/doku.php/jme3:simpleapplication_from_the_commandline_zh" class="wikilink2" title="jme3:simpleapplication_from_the_commandline_zh" rel="nofollow">在(Linux)命令行下开发JME3</a> </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [904-2060] -->
<p>
(*) jME SDK创建的是基于Ant的项目，任何Java IDE都可以导入。我们建议其他IDE的用户也下载jME SDK，并选择 “File→Import Project→External Project Assets” 来创建一个不包含任何代码的资源项目，用以管理项目中的资源文件(如模型、材质、贴图等)。这样您就可以在自己选择的IDE中编码，并利用jME SDK来将您的模型转换成.j3o格式。
</p>

</div>
<!-- EDIT2 SECTION "下载和安装" [699-2477] -->
<h2 class="sectionedit4" id="创建jme工程">创建jME工程</h2>
<div class="level2">

<p>
下载安装jME之后，请把这个<a href="/jme3_zh.html" class="wikilink1" title="jme3_zh">jME教程</a>加入您的书签，然后动手开发您的第一个游戏吧！
</p>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> 教程 </th><th class="col1"> jMonkeyEngine SDK </th><th class="col2"> 其他文档 </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> <a href="/jme3_zh.html" class="wikilink1" title="jme3_zh">jME3初级教程</a> </td><td class="col1"> <a href="/doku.php/sdk_zh" class="wikilink2" title="sdk_zh" rel="nofollow">jMonkeyEngine SDK 文档和视频教程</a> </td><td class="col2"> <a href="http://javadoc.jmonkeyengine.org/" class="urlextern" title="http://javadoc.jmonkeyengine.org/" rel="nofollow">Full API JavaDoc</a> </td>
	</tr>
	<tr class="row2">
		<td class="col0"> <a href="/jme3_zh.html" class="wikilink1" title="jme3_zh">jME3中级教程</a> </td><td class="col1"> <a href="/doku.php/sdk:comic_zh" class="wikilink2" title="sdk:comic_zh" rel="nofollow">jMonkeyEngine SDK - 漫画 :-)</a> </td><td class="col2"> <a href="/doku.php/jme3:external:blender_zh" class="wikilink2" title="jme3:external:blender_zh" rel="nofollow">Blender建模指南</a> </td>
	</tr>
	<tr class="row3">
		<td class="col0"> <a href="/jme3_zh.html" class="wikilink1" title="jme3_zh">jME3进阶教程</a> </td><td class="col1 leftalign">  </td><td class="col2"> <a href="/doku.php/jme3:faq_zh" class="wikilink2" title="jme3:faq_zh" rel="nofollow">FAQ</a> </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [2633-3059] -->
</div>
<!-- EDIT4 SECTION "创建jME工程" [2478-3060] -->
<h2 class="sectionedit6" id="贡献代码">贡献代码</h2>
<div class="level2">

<p>
想给jME3贡献新的特性和功能吗？如果你是一名熟练的Java开发者，请看下列页面：
</p>
<ul>
<li class="level1"><div class="li"> 了解已有的<a href="/jme3/contributions.html" class="wikilink1" title="jme3:contributions">贡献</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/introduction/contributors-handbook/" class="urlextern" title="http://hub.jmonkeyengine.org/introduction/contributors-handbook/" rel="nofollow">阅读贡献者手册</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/" class="urlextern" title="http://hub.jmonkeyengine.org/" rel="nofollow">加入官方论坛的讨论</a></div>
</li>
<li class="level1"><div class="li"> <a href="/doku.php/jme3:jme3_source_structure_zh" class="wikilink2" title="jme3:jme3_source_structure_zh" rel="nofollow">学习jME3源码架构</a></div>
</li>
<li class="level1"><div class="li"> <a href="/doku.php/sdk_zh#development" class="wikilink2" title="sdk_zh" rel="nofollow">开发jME SDK插件以及可视化编辑器</a></div>
</li>
<li class="level1"><div class="li"> <a href="/doku.php/report_bugs_zh" class="wikilink2" title="report_bugs_zh" rel="nofollow">报告bug &amp; 提交补丁</a></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "贡献代码" [3061-3584] -->
<h2 class="sectionedit7" id="联系我们">联系我们</h2>
<div class="level2">

<p>
欢迎您的贡献和咨询：请通过<a href="mailto:contact@jmonkeyengine.com" class="mail" title="contact@jmonkeyengine.com">电子邮箱</a>联系<a href="http://jmonkeyengine.org/team/" class="urlextern" title="http://jmonkeyengine.org/team/" rel="nofollow">开发团队</a>，或者在 <a href="http://hub.jmonkeyengine.org/" class="urlextern" title="http://hub.jmonkeyengine.org/" rel="nofollow">官方论坛</a>发帖提问。
</p>
<ul>
<li class="level1"><div class="li"> <a href="mailto:contact@jmonkeyengine.com" class="mail" title="contact@jmonkeyengine.com">联系jME团队</a></div>
<ul>
<li class="level2"><div class="li"> <a href="http://jmonkeyengine.org/team/" class="urlextern" title="http://jmonkeyengine.org/team/" rel="nofollow">核心团队 - 我们是谁？</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="/report_bugs.html" class="wikilink1" title="report_bugs">发现bug</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/c/documentation-jme3" class="urlextern" title="http://hub.jmonkeyengine.org/c/documentation-jme3" rel="nofollow">发现文档内容含糊或文档不存在</a></div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "联系我们" [3585-4070] -->
<h2 class="sectionedit8" id="本页的多国语言版">本页的多国语言版</h2>
<div class="level2">

<p>
<a href="/documentation.html" class="wikilink1" title="documentation">英文原版</a> <br />

<a href="/doku.php/%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F" class="wikilink2" title="документация" rel="nofollow">俄语版</a> <br />

<a href="/documentacao.html" class="wikilink1" title="documentacao">葡萄牙语</a> <br />

<span class="curid"><a href="/documentation_zh.html" class="wikilink1" title="documentation_zh">中文版</a></span>
</p>

</div>
<!-- EDIT8 SECTION "本页的多国语言版" [4071-4252] -->
<h2 class="sectionedit9" id="中文开发者讨论群">中文开发者讨论群</h2>
<div class="level2">

<p>
本群不是jME的官方QQ群，而是由一群国内的jME爱好者聚集的讨论群，欢迎加入讨论，群号：423979787。
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>
</span></div>

</div>
<!-- EDIT9 SECTION "中文开发者讨论群" [4253-] -->
