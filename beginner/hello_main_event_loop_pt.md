---
title: jMonkeyEngine 3 Tutorial (4) - Hello Update Loop
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_4_-_hello_update_loop">jMonkeyEngine 3 Tutorial (4) - Hello Update Loop</h1>
<div class="level1">

<p>
Anterior: <a href="/doku.php/jme3:beginner:hello_asset-pt" class="wikilink2" title="jme3:beginner:hello_asset-pt" rel="nofollow"> Hello Assets pt</a>,
Next: <a href="/jme3/beginner/hello_input_system-pt.html" class="wikilink1" title="jme3:beginner:hello_input_system-pt"> Hello Input System pt</a>
</p>

<p>
Agora que você sabe como carregar ativos, como modelos 3D, você quer implementar alguma jogabilidade que usa estes ativos. Neste tutorial nós olhamos no loop de atualização. O loop de atualização de seu jogo é onde a ação acontece.
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (4) - Hello Update Loop" [1-442] -->
<h2 class="sectionedit2" id="amostra_de_codigo">Amostra de Código</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 4 - how to trigger repeating actions from the main update loop.
 * In this example, we make the player character rotate. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloLoop <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloLoop app <span class="sy0">=</span> <span class="kw1">new</span> HelloLoop<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="kw1">protected</span> Geometry player<span class="sy0">;</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        player <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"blue cube"</span>, b<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
          <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        player.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>player<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="coMULTI">/* This is the update loop */</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleUpdate<span class="br0">(</span><span class="kw4">float</span> tpf<span class="br0">)</span> <span class="br0">{</span>
        <span class="co1">// make the player rotate</span>
        player.<span class="me1">rotate</span><span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">2</span><span class="sy0">*</span>tpf, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span> 
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Compile e execute o arquivo: Você vê um cubo rotacionando constantemente.
</p>

</div>
<!-- EDIT2 SECTION "Amostra de Código" [443-1673] -->
<h2 class="sectionedit3" id="entendendo_o_codigo">Entendendo o Código</h2>
<div class="level2">

<p>
Comparado a nossos exemplos de código anteriores você nota que a geometria (Geometry) do jogador é agora um campo (atributo) de classe. Isto é porque nós queremos que o loop de atualização seja capaz de acessar e transformar esta geometria (Geometry). Como notmal, nós inicializamos o objeto jogador no método <code>simpleInitApp()</code>.
</p>

<p>
Agora dê uma olhada mais de perto no método <code>simpleUpdate()</code> – este é o loop de atualização.
</p>
<ul>
<li class="level1"><div class="li"> A linha <code>player.rotate(0, 2*tpf, 0);</code> muda a rotação do objeto jogador.</div>
</li>
<li class="level1"><div class="li"> Nós usamos a variável <code>tpf</code> (tempo por quadro) (“time per frame”) para temporizar esta ação dependendo da taxa atual de quadros por segundo. Isto simplesmente significa que o cubo rotaciona com a mesma velocidade em máquinas rápidas e lentas, e o jogo permanece jogável.</div>
</li>
<li class="level1"><div class="li"> Quando o jogo executa, o código rotate() é executado repetidamente.</div>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Entendendo o Código" [1674-2589] -->
<h2 class="sectionedit4" id="usando_o_loop_de_atualizacao">Usando o Loop de Atualização</h2>
<div class="level2">

<p>
Um objeto rotacionando é apenas um exemplo simples. No loop de atualização, você tipicamente tem muitos testes e dispara várias ações de jogo. Isto é onde você atualiza a pontuação e pontos de vida, checa por colisões, faz os inimigos calcularem o próximo movimento deles, rola os dados se uma armadilha foi colocada, toca sons ambiente aleatórios, e muito mais.
</p>
<ul>
<li class="level1"><div class="li"> O método <code>simpleUpdate()</code> inicia sua execução após o método <code>simpleInitApp()</code> ter inicializado o grafo de cena e as variáveis de estado.</div>
</li>
<li class="level1"><div class="li"> JME3 executa tudo no método simpleUpdate() repetidamente, tão rápido quanto possível.</div>
<ol>
<li class="level2"><div class="li"> Use o loop para consultar o estado do jogo e então inciar ações.</div>
</li>
<li class="level2"><div class="li"> Use o loop para disparar reações e atualizar o estado do jogo.</div>
</li>
<li class="level2"><div class="li"> Use o loop com sabedoria, por que ter chamadas demais no loop também faz o jogo mais executar mais lento.</div>
</li>
</ol>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "Usando o Loop de Atualização" [2590-3515] -->
<h2 class="sectionedit5" id="inicializar_-_atualizar_-_renderizar">Inicializar - Atualizar - Renderizar</h2>
<div class="level2">

<p>
Note o contraste:
</p>
<ul>
<li class="level1"><div class="li"> O método <code>simpleInitApp()</code> é executado somente uma vez, imediatamente no início;</div>
</li>
<li class="level1"><div class="li"> O método <code>simpleUpdate()</code> executa repetidamente, durante o jogo.</div>
</li>
<li class="level1"><div class="li"> Depois de toda atualização a jMonkeyEngine automaticamente redesenha (renderiza) a tela para você!</div>
</li>
</ul>

<p>
Desde que rendering é automático e, inicialização e a atualiação são os dois conceitos mais importantes em uma SimpleApplication para você imediatamente. Estes métodos são onde você carrega e cria dados do jogo (uma vez), e (repetidamente) muda as propriedades deles para atualizar o estado do jogo:
</p>
<ul>
<li class="level1"><div class="li"> <code>simpleInitApp()</code> é a “primeira respiração” da aplicação.</div>
</li>
<li class="level1"><div class="li"> <code>simpleUpdate()</code> é a batida de coração da aplicação. <br />
A unidade de tempo de atualização é chamada <code>tiques (ticks)</code>.</div>
</li>
</ul>

<p>
</p><p></p><div class="notetip">Tudo em um jogo acontece ou durante a inicialização ou durante o loop de atualização. Isto significa que estes dois métodos crescem muito com o tempo. Há duas estratégias como desenvolvedores experientes espalham o código de atualização e inicialização em várias classes Java:

<ul>
<li class="level1"><div class="li"> Mova os blocos de código do método simpleInitApp() para <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states"> AppStates</a>.</div>
</li>
<li class="level1"><div class="li"> Mova os blocos de código do método simpleUpdate() para <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls">Custom Controls</a>.</div>
</li>
</ul>

<p>
mantenha isto em mente pata depois quando sua aplicação crescer.

</p></div>


</div>
<!-- EDIT5 SECTION "Inicializar - Atualizar - Renderizar" [3516-4954] -->
<h2 class="sectionedit6" id="exercicios">Exercícios</h2>
<div class="level2">

<p>
Aqui estão algumas coisas divertidas para experimentar:
</p>
<ol>
<li class="level1"><div class="li"> O que acontece se você dar ao método rotate() números negativos?</div>
</li>
<li class="level1"><div class="li"> Você pode criar duas geometrias (Geometries) uma próxima a outra, e fazer uma rotacionar duas vezes mais rápido que a outra? (use a varuável <code>tpf</code>)</div>
</li>
<li class="level1"><div class="li"> Você pode fazer um cubo que pulsa (cresce e diminui)</div>
</li>
<li class="level1"><div class="li"> Você pode fazer um cubo que muda de cor? (mude e configure o Material)</div>
</li>
<li class="level1"><div class="li"> Você pode fazer um cubo que role (rotacione ao redor do eixo x, e translade ao longo do eixo z)</div>
</li>
</ol>

<p>
Olhe de volta no tutorial <a href="/jme3/beginner/hello_node.html" class="wikilink1" title="jme3:beginner:hello_node">Hello Node</a> se você não lembra os métodos de transformação para escalonar, transladar, e rotacionar.
</p>

<p>
</p><p></p><div class="noteimportant">Link para soluções propostas pelos usuário: <a href="http://jmonkeyengine.org/wiki/doku.php/jm3:solutions" class="urlextern" title="http://jmonkeyengine.org/wiki/doku.php/jm3:solutions" rel="nofollow">http://jmonkeyengine.org/wiki/doku.php/jm3:solutions</a>
<em class="u"> Esteja certo de tentar resolvê-las por si só primeiro!</em>
</div>


</div>
<!-- EDIT6 SECTION "Exercícios" [4955-5824] -->
<h2 class="sectionedit7" id="conclusao">Conclusão</h2>
<div class="level2">

<p>
Agora você está ouvindo ao loop de atualização, “a batida do coração” do jogo, e você pode adicionar todos os tipos de ação a ele.
</p>

<p>
A próxima coisa que o jogo precisa é alguma interação! Continue aprendendo a como <a href="/jme3/beginner/hello_input_system-pt.html" class="wikilink1" title="jme3:beginner:hello_input_system-pt"> responder a entrada do usuário pt</a>.
</p>
<hr />

<p>
Veja também:
</p>
<ul>
<li class="level1"><div class="li"> Desenvolvedores jME3 avançados usam <a href="/jme3/advanced/application_states.html" class="wikilink1" title="jme3:advanced:application_states"> Estados da Aplicação (Application States)</a> e <a href="/jme3/advanced/custom_controls.html" class="wikilink1" title="jme3:advanced:custom_controls"> Controles Personalizados (Custom Controls)</a> para implementar mecânicas de jogo no loop de atualização deles. Você topará nestes tópicos de novo mais tarde quando você proceder para documentação mais avançada.</div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/state.html" class="wikilink1" title="tag:state" rel="tag">state</a>,
	<a href="/tag/states.html" class="wikilink1" title="tag:states" rel="tag">states</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/control.html" class="wikilink1" title="tag:control" rel="tag">control</a>,
	<a href="/tag/loop.html" class="wikilink1" title="tag:loop" rel="tag">loop</a>
</span></div>

</div>
<!-- EDIT7 SECTION "Conclusão" [5825-] -->
