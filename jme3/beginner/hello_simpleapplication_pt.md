---
title: jMonkeyEngine 3 Tutorial (1) - Hello SimpleApplication
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_1_-_hello_simpleapplication">jMonkeyEngine 3 Tutorial (1) - Hello SimpleApplication</h1>
<div class="level1">

<p>
Previous: <a href="/jme3.html" class="wikilink1" title="jme3">Instalando JME3</a>,
Next: <a href="/jme3/beginner/hello_node_pt.html" class="wikilink1" title="jme3:beginner:hello_node_pt">Hello Node pt</a>
</p>

<p>
<strong>Pré-requisitos:</strong> Este tutorial assume que você já tenha <a href="http://jmonkeyengine.org/wiki/doku.php/" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/" rel="nofollow">baixado o SDK da jMonkeyEngine</a>.
</p>

<p>
Nesta série de tutoriais, nós assumimos que você usa o <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> da jMonkeyEngine. Como um desenvolvedor Java intermediário ou avançado, você rapidamente verá que, em geral, você pode desenvolver código da jMonkeyEngine em qualquer ambiente de desenvolvimento integrado (NetBeans IDE, Eclipse, IntelliJ) ou mesmo da linha de comando.
</p>

<p>
OK, Vamos nos aprontar para criar nossa primeira aplicação jMonkeyEngine3.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (1) - Hello SimpleApplication" [1-734] -->
<h2 class="sectionedit2" id="crie_um_projeto">Crie um Projeto</h2>
<div class="level2">

<p>
Na SDK da jMonkeyEngine:
</p>
<ol>
<li class="level1"><div class="li"> Escolha Arquivo (File)→Novo Projeto (New Project)… do menu principal.</div>
</li>
<li class="level1"><div class="li"> No assistente de Novo Projeto, selecione o modelo JME3→Jogo Básico (Basic Game). Clique em prosseguir (Next). </div>
<ol>
<li class="level2"><div class="li"> Especifique um nome de projeto, e.g. “HelloWorldTutorial”</div>
</li>
<li class="level2"><div class="li"> Especifique um caminho para armazenar seu novo projeto, e.g. um diretório projetosjMonkey no seu diretório de usuário.</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Clique em terminar (Finish). </div>
</li>
</ol>

<p>
Se você tem perguntas, leia mais sobre Criação de Projeto aqui.
</p>

<p>
</p><p></p><div class="notetip">Nós recomendamos atravessar os passos você mesmo, como descrito nos tutoriais. Alternativamente, você pode criar um projeto baseado no modelo <a href="/sdk/sample_code.html" class="wikilink1" title="sdk:sample_code">JmeTests</a> no SDK da jMonkeyEngine. Isto criará um projeto que já contém as amostras jme3test.helloworld (e muitas outras). Por exemplo, você pode usar o projeto JmeTests para verificar se você tem a solução certa.
</div>


</div>
<!-- EDIT2 SECTION "Crie um Projeto" [735-1681] -->
<h2 class="sectionedit3" id="escreva_uma_aplicacao_de_amostra">Escreva uma aplicação de amostra</h2>
<div class="level2">

<p>
Para este tutorial, você deseja criar um pacote <code>jme3test.helloworld</code> no seu projeto, e criar um arquivo <code>HelloJME3.java</code> nele. 
</p>

<p>
No SDK da jMonkeyEngine:
</p>
<ol>
<li class="level1"><div class="li"> Dê um clique com o botão direito no nó pacotes de código-fonte (Source Packages) de seu projeto.</div>
</li>
<li class="level1"><div class="li"> Escolha Novo (New)… →Classe Java (Java Class) para criar um novo arquivo.</div>
</li>
<li class="level1"><div class="li"> Digite o nome da classe: <code>HelloJME3</code></div>
</li>
<li class="level1"><div class="li"> Digite o nome do pacote: <code>jme3test.helloworld</code>.</div>
</li>
<li class="level1"><div class="li"> Clique em Finalizar (Finish).</div>
</li>
</ol>

<p>
O SDK cria o arquivo HelloJME3.java para você.
</p>

</div>
<!-- EDIT3 SECTION "Escreva uma aplicação de amostra" [1682-2255] -->
<h2 class="sectionedit4" id="codigo_de_amostra">Código de Amostra</h2>
<div class="level2">

<p>
Substitua os conteúdos do arquivo HelloJME3.java com o seguinte código:
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 1 - começando com a mais simples aplicação JME 3.
 * Mostra um cubo 3D azul e veja todos os seus lados 
 * movendo o mouse e pressionando as teclas WASD. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloJME3 <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// start the game</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// cria a forma do cubo na origem</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// cria a geometria do cubo a partir da sua forma</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// cria um material simples</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// determina a cor do material para azul</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>                   <span class="co1">// determina o material do cubo</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>              <span class="co1">// faz o cubo aparecer na cena</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Dê um clique com o botão direito na classe HelloJME3 class e escolha Executar (Run). Se um diálogo de configurações da jME3 aparecer, confirme as configurações padrão.
</p>
<ol>
<li class="level1"><div class="li"> Você deveria ver uma janela simples exibindo um cubo 3D.</div>
</li>
<li class="level1"><div class="li"> Pressione as teclas WASD keys e mova para navegar ao redor.</div>
</li>
<li class="level1"><div class="li"> Olhe no texto do FPS e na informação de contagem de objeto na esquerda-fundo. Você usará esta informação durante o desenvolvimento, e você removerá ela para a liberação. (Para ler os números corretamente, considere que as 14 linhas de texto contam como 14 objetos com 914 vértices.)</div>
</li>
<li class="level1"><div class="li"> Pressione Escape (Esc) para fechar a aplicação.</div>
</li>
</ol>

<p>
Parabéns! Agora camos decobrir como isso funciona!
</p>

</div>
<!-- EDIT4 SECTION "Código de Amostra" [2256-4297] -->
<h2 class="sectionedit5" id="compreendendo_o_codigo">Compreendendo o código</h2>
<div class="level2">

<p>
O código acima tem inicializado a cena, e iniciado a aplicação.
</p>

</div>
<!-- EDIT5 SECTION "Compreendendo o código" [4298-4402] -->
<h3 class="sectionedit6" id="inicie_a_simpleapplication">Inicie a SimpleApplication</h3>
<div class="level3">

<p>
Olhe na primeira linha. A classe HelloJME3.java estende <code>com.jme3.app.SimpleApplication</code>. 
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> HelloJME3 <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
  <span class="co1">// seu código...</span>
<span class="br0">}</span></pre>

<p>
Todo jogo JME3 é uma instância de <code>com.jme3.app.SimpleApplication</code>. A classe SimpleApplication gerencia seu grafo de cena 3D e automaticamente desenha ele para a tela – isto é, em breve, o que uma engine de jogo faz para você! 
</p>

<p>
Você inicia todo jogo JME3 do método main(), como toda aplicação Java padrão::
</p>
<ol>
<li class="level1"><div class="li"> Instancie sua classe baseada em <code>SimpleApplication</code></div>
</li>
<li class="level1"><div class="li"> Chame o método <code>start()</code> da aplicação para iniciar a engine de jogo. </div>
</li>
</ol>
<pre class="code java">    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// instanciar o jogo</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>                     <span class="co1">// iniciar o jogo!</span>
    <span class="br0">}</span></pre>

<p>
Este código abre sua janela de aplicação. Vamos aprender a por alguma coisa para a janela em seguinda.
</p>

</div>
<!-- EDIT6 SECTION "Inicie a SimpleApplication" [4403-5388] -->
<h3 class="sectionedit7" id="entendendo_a_terminologia">Entendendo a Terminologia</h3>
<div class="level3">
<div class="table sectionedit8"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">O que você quer fazer</th><th class="col1">Como você diz isso na terminologia JME3</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Você quer criar um cubo.</td><td class="col1">Eu crio uma geometria (Geometry) com uma forma de caixa (Box) 1x1x1</td>
	</tr>
	<tr class="row2">
		<td class="col0">Você quer usar uma cor azul.</td><td class="col1">Eu crio um Material com uma propriedade cor (Color) azul</td>
	</tr>
	<tr class="row3">
		<td class="col0">Você quer colorir o cubo azul.</td><td class="col1">Eu coloco o Material da geometria caixa (Box Geometry)</td>
	</tr>
	<tr class="row4">
		<td class="col0">Você quer adicionar o cubo para a cena.</td><td class="col1">Eu anexo a geometria caixa (Box Geometry) para o nó raíz (rootNode)</td>
	</tr>
	<tr class="row5">
		<td class="col0">Você quer que o cubo apareça no centro.</td><td class="col1">Eu crio a caixa (Box) na origem = em <code>Vector3f.ZERO</code>.</td>
	</tr>
</table></div>
<!-- EDIT8 TABLE [5426-5978] -->
<p>
Se você não esta familiar com o vocabulário, leia mais sobre o <a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph"> Grafo de Cema</a> aqui.
</p>

</div>
<!-- EDIT7 SECTION "Entendendo a Terminologia" [5389-6094] -->
<h3 class="sectionedit9" id="inicialize_a_cena">Inicialize a Cena</h3>
<div class="level3">

<p>
Olhe no resto da amostra de código. O método <code>simpleInitApp()</code> é automaticamente chamado uma vez no início quando a aplicação inicia. Todo jogo JME3 deve ter este método. No mpetodo <code>simpleInitApp()</code>, você carrega objetos do jogo antes que o jogo inicie.
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
       <span class="co1">// seu código de inicialização...</span>
    <span class="br0">}</span></pre>

<p>
O código de inicialização de um cubo azul parece como se segue:
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// cria uma forma cúbica de 2x2x2 na origem</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// cria a geometria do cubo a partir da sua forma</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// cria um material simples</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>   <span class="co1">// determina a cor do material para azul</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>                   <span class="co1">// determina o material da geometria do cubo</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>              <span class="co1">// faz a geometria do cubo aparecer na cena</span>
    <span class="br0">}</span></pre>

<p>
Um jogo JME típico tem o seguinte processo de inicialização:
</p>
<ol>
<li class="level1"><div class="li"> Você inicializa os objetos do jogo: :</div>
<ul>
<li class="level2"><div class="li"> Você cria ou carrega objetos e posiciona eles.</div>
</li>
<li class="level2"><div class="li"> Você faz objetos aparecerem na cena por anexá-los ao  <code>nó raiz (rootNode)</code>.</div>
</li>
<li class="level2"><div class="li"> <strong>Exemplos:</strong> Carregar o jogador, terreno, céu, inimigos, obstáculos, …, e colocá-los nas suas posições de início.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Você inicializa variáveis</div>
<ul>
<li class="level2"><div class="li"> Você cria variáveis para rastrear o estado de jogo.</div>
</li>
<li class="level2"><div class="li"> Você configura as variáveis para os valores de início delas.</div>
</li>
<li class="level2"><div class="li"> <strong>Exemplos:</strong> Coloque a <code>pontuação</code> para 0, coloque a <code>saúde</code> para 100%, …</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Você inicializa as teclas e ações do mouse.</div>
<ul>
<li class="level2"><div class="li"> As seguintes ligações de entrada já estão pré-configuradas:</div>
<ul>
<li class="level3"><div class="li"> W,A,S,D keys – Mova ao redir da cena</div>
</li>
<li class="level3"><div class="li"> Movimento do mouse e teclas seta - Vire a câmera</div>
</li>
<li class="level3"><div class="li"> Escape (Esc) - Sai do jogo</div>
</li>
</ul>
</li>
<li class="level2"><div class="li"> Defina suas próprias teclas adicionais e ações de clique do mouse</div>
</li>
<li class="level2"><div class="li"> <strong>Exemplos:</strong> Clique para atirar, pressione a Barra de Espaço para pular, …</div>
</li>
</ul>
</li>
</ol>

</div>
<!-- EDIT9 SECTION "Inicialize a Cena" [6095-8278] -->
<h2 class="sectionedit10" id="conclusao">Conclusão</h2>
<div class="level2">

<p>
Você têm aprendido que uma SimpleApplication é um bom ponto de início porque ela fornece você com:
</p>
<ul>
<li class="level1"><div class="li"> Um método <code>simpleInitApp()</code> onde você cria objetos.</div>
</li>
<li class="level1"><div class="li"> Um <code>nó raiz (rootNode)</code> onde você anexa objetos para fazê-los aparecer na cena.</div>
</li>
<li class="level1"><div class="li"> Configurações de entrada padrão úteis que você pode usar para navegação na cena.</div>
</li>
</ul>

<p>
Quando desenvolvendo uma aplicação de jogo, você irá querer:
</p>
<ol>
<li class="level1"><div class="li"> Inicializar a cena de jogo</div>
</li>
<li class="level1"><div class="li"> Disparar ações de jogo</div>
</li>
<li class="level1"><div class="li"> Responder à entrada do usuário.</div>
</li>
</ol>

<p>
Agora os próximos tutoriais lhe ensinarão a como realizar estas tarefas com a jMonkeyEngine 3.
</p>

<p>
Continue com o tutorial <a href="/jme3/beginner/hello_node_pt.html" class="wikilink1" title="jme3:beginner:hello_node_pt">Hello Node pt</a>, onde você aprende mais detalhes sobre como inicializar o mundo do jogo, também conhecido como o grafo de cena.
</p>
<hr />

<p>
Veja também:
</p>
<ul>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/wiki/doku.php/" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/" rel="nofollow"> Instalar a JMoneyEngine</a></div>
</li>
<li class="level1"><div class="li"> <a href="/jme3/simpleapplication_from_the_commandline.html" class="wikilink1" title="jme3:simpleapplication_from_the_commandline"> SimpleApplication da Linha de comando</a></div>
</li>
<li class="level1"><div class="li"> <a href="/sdk/project_creation.html" class="wikilink1" title="sdk:project_creation">Criar um projeto JME3</a>.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/init.html" class="wikilink1" title="tag:init" rel="tag">init</a>,
	<a href="/tag/simpleapplication.html" class="wikilink1" title="tag:simpleapplication" rel="tag">simpleapplication</a>,
	<a href="/tag/basegame.html" class="wikilink1" title="tag:basegame" rel="tag">basegame</a>
</span></div>

</div>
<!-- EDIT10 SECTION "Conclusão" [8279-] -->
