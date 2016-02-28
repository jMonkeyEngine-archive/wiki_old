---
title: Documentação jMonkeyEngine
---
<h1 class="sectionedit1" id="documentacao_jmonkeyengine">Documentação jMonkeyEngine</h1>
<div class="level1">

<p>
Essa wiki contém guias de instalação e configuração, tutoriais de codificação jME3 e outras informaçõess que lhe ajudarão a dar andamento no seu projeto de jogo. Você pode pesquisar o conteúdo dessa wiki usando a caixa de pesquisa “Search” localizado na direita-superior dessa página.
</p>

<p>
Você também é convidado a corrigir equívicos ou problemas de digitação, como também parágrafos confusos, usando o menu “Tools” localizado na direita-superior dessa página ou o botão “Edit” em cada parágrafo. Você precisa estar conectado na wiki para poder editar.
</p>

</div>
<!-- EDIT1 SECTION "Documentação jMonkeyEngine" [1-619] -->
<h2 class="sectionedit2" id="instalacao">Instalação</h2>
<div class="level2">

<p>
<strong>Antes de instalar, verifique a <a href="/bsd_license.html" class="wikilink1" title="bsd_license">licença</a>, <a href="/jme3/features.html" class="wikilink1" title="jme3:features">funcionalidades</a>, e <a href="/jme3/requerimentos.html" class="wikilink1" title="jme3:requerimentos">requerimentos</a>.</strong> Então, escolha uma das seguintes opções:
</p>
<div class="table sectionedit3"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0"> </td><th class="col1 leftalign"> Recomendado     </th><th class="col2 leftalign"> Opcional       </th><th class="col3 leftalign"> Opcional  </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> Você gostaria de… </th><td class="col1"> Iniciar com a jMonkeyEngine </td><td class="col2"> Usar a jMonkeyEngine em outra IDE </td><td class="col3"> Construir uma “engine” a partir do código fonte </td>
	</tr>
	<tr class="row2">
		<th class="col0"> Então baixe… </th><td class="col1"> <a href="http://jmonkeyengine.org/downloads/" class="urlextern" title="http://jmonkeyengine.org/downloads/" rel="nofollow">jMonkeyEngine SDK</a> </td><td class="col2"> <a href="http://updates.jmonkeyengine.org/stable" class="urlextern" title="http://updates.jmonkeyengine.org/stable" rel="nofollow">Binários</a> </td><td class="col3"> <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine" rel="nofollow">Fontes (Subversion)</a> </td>
	</tr>
	<tr class="row3">
		<th class="col0"> Você receberá… </th><td class="col1"> Fontes, binários, javadoc, SDK </td><td class="col2"> Ultima versão estável, fontes, javadoc. </td><td class="col3"> Fontes </td>
	</tr>
	<tr class="row4">
		<th class="col0"> Aprenda mais… </th><td class="col1"> <a href="/sdk.html" class="wikilink1" title="sdk">Utilizando o SDK</a> <br />
<a href="/sdk/project_creation.html" class="wikilink1" title="sdk:project_creation">Criação de Projeto</a> <br />
<a href="/resources/sdk-jme3-jmonkeyplatform.png" class="media" title="sdk:jme3-jmonkeyplatform.png"><img src="/resources/sdk-jme3-jmonkeyplatform.png" class="mediacenter" alt="" width="144" height="90" /></a> </td><td class="col2"> <a href="/jme3/maven.html" class="wikilink1" title="jme3:maven">Configurando o JME3 com IDE compatívels com maven</a> * <br />
<a href="/jme3/setting_up_netbeans_and_jme3.html" class="wikilink1" title="jme3:setting_up_netbeans_and_jme3">Configurando o JME3 no NetBeans IDE</a> * <br />
<a href="/jme3/setting_up_jme3_in_eclipse.html" class="wikilink1" title="jme3:setting_up_jme3_in_eclipse">Configurando o JME3 no Eclipse IDE</a> * <br />
<a href="/jme3/eclipse_jme3_android_jnindk.html" class="wikilink1" title="jme3:eclipse_jme3_android_jnindk">Configurando o JME3 no Eclipse IDE (com Android e/ou JNI/NDK)</a> * </td><td class="col3"> <a href="/jme3/build_from_sources.html" class="wikilink1" title="jme3:build_from_sources">Compilando JME3 a partir dos Fontes</a> <br />
<a href="/jme3/build_jme3_sources_with_netbeans.html" class="wikilink1" title="jme3:build_jme3_sources_with_netbeans">Compilando jME3 a partir dos Fontes com NetBeans</a> <br />
<a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline">Configurando o jME3 na linha de comando</a> </td>
	</tr>
</table></div>
<!-- EDIT3 TABLE [814-2054] -->
<p>
(*) O SDK cria projetos baseados em ANT que qualquer Java IDE pode importar. Nós recomendamos que usuários de outras IDEs baixem a jMonkeyEngine SDK e escolham “Arquivo→Importar Projeto→Pastas de Projeto Externo” para criar um projeto sem código, apanas para gerenciar os assets. Dessa forma, você pode codificar no IDE de sua escolha e ainda utilizar o SDK para converter seus modelos para o formato .j3o.
</p>

<p>
<strong> EM CONSTRUÇÃO </strong>
</p>

</div>
<!-- EDIT2 SECTION "Instalação" [620-2492] -->
<h2 class="sectionedit4" id="crie">Crie</h2>
<div class="level2">

<p>
Depois de baixado e instalado, <a href="/jme3.html" class="wikilink1" title="jme3">adicione esta página em seus favoritos</a> e comece a escrever seu primeiro jogo!
</p>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Tutoriais </th><th class="col1"> jMonkeyEngine SDK </th><th class="col2"> Outras Documentações </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">jME3 tutoriais para iniciantes</a> </td><td class="col1"> <a href="/sdk.html" class="wikilink1" title="sdk">Documentação jMonkeyEngine SDK e Vídeo Tutoriais</a> </td><td class="col2"> <a href="http://javadoc.jmonkeyengine.org/" class="urlextern" title="http://javadoc.jmonkeyengine.org/" rel="nofollow">API JavaDoc Completa</a> </td>
	</tr>
	<tr class="row2">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">Artigos jME3 intermediário</a> </td><td class="col1"> <a href="/sdk/comic.html" class="wikilink1" title="sdk:comic">jMonkeyEngine SDK - a Comédia :-)</a> </td><td class="col2"> <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">Guia de Modelagem em Blender</a> </td>
	</tr>
	<tr class="row3">
		<td class="col0"> <a href="/jme3.html" class="wikilink1" title="jme3">jME3 documentação avançada</a> </td><td class="col1 leftalign">  </td><td class="col2"> <a href="/jme3/faq.html" class="wikilink1" title="jme3:faq">Respostas para Perguntas Frequentes</a> </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [2632-3204] -->
</div>
<!-- EDIT4 SECTION "Crie" [2493-3205] -->
<h2 class="sectionedit6" id="contribua">Contribua</h2>
<div class="level2">

<p>
Você é um desenvolvedor Java experiente que quer adicionar novas funcionalidades ou contribuír com o projeto jME3?
</p>
<ul>
<li class="level1"><div class="li"> Inspire-se com <a href="/jme3/contributions.html" class="wikilink1" title="jme3:contributions">contribuições</a> existentes</div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/introduction/contributors-handbook/" class="urlextern" title="http://hub.jmonkeyengine.org/introduction/contributors-handbook/" rel="nofollow">Leia o guia dos Contribuídores</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/" class="urlextern" title="http://hub.jmonkeyengine.org/" rel="nofollow">Grite no fórum dos Contribuídores</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/jme3_source_structure.html" class="wikilink1" title="jme3:jme3_source_structure">Aprenda sobre a estrutura dos Fontes</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk.html" class="wikilink1" title="sdk">Escreva plugins e editores visuais para a jMonkeyEngine SDK</a></div>
</li>
<li class="level1"><div class="li"> <a href="/report_bugs.html" class="wikilink1" title="report_bugs">Reporte bugs e envie correções</a></div>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "Contribua" [3206-3804] -->
<h2 class="sectionedit7" id="contato">Contato</h2>
<div class="level2">

<p>
Você é bem-vindo em contribuír ou perguntar sobre o projeto: Por favor <a href="mailto:contact@jmonkeyengine.com" class="mail" title="contact@jmonkeyengine.com">contate</a> os
<a href="http://jmonkeyengine.org/team/" class="urlextern" title="http://jmonkeyengine.org/team/" rel="nofollow">desenvolvedores</a> ou pergunte no <a href="http://hub.jmonkeyengine.org/" class="urlextern" title="http://hub.jmonkeyengine.org/" rel="nofollow">fórum</a>.
</p>
<ul>
<li class="level1"><div class="li"> <a href="mailto:contact@jmonkeyengine.com" class="mail" title="contact@jmonkeyengine.com">Contate o time jME</a></div>
<ul>
<li class="level2"><div class="li"> <a href="http://jmonkeyengine.org/team/" class="urlextern" title="http://jmonkeyengine.org/team/" rel="nofollow">Core Team - Quem somos?</a></div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> <a href="/report_bugs.html" class="wikilink1" title="report_bugs">Reporte uma falha</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://hub.jmonkeyengine.org/c/documentation-jme3" class="urlextern" title="http://hub.jmonkeyengine.org/c/documentation-jme3" rel="nofollow">Reporte documentação confusa ou faltante</a></div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "Contato" [3805-4303] -->
<h2 class="sectionedit8" id="linguas">Línguas</h2>
<div class="level2">

<p>
<a href="/doku.php/%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F" class="wikilink2" title="документация" rel="nofollow">Документация на Русском</a>
<span class="curid"><a href="/documentacao.html" class="wikilink1" title="documentacao">Documentação em Português</a></span>
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/install.html" class="wikilink1" title="tag:install" rel="tag">install</a>
</span></div>

</div>
<!-- EDIT8 SECTION "Línguas" [4304-] -->
