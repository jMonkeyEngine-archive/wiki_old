---
title: jMonkeyEngine 3 Tutorial (2) - Hello Node
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_2_-_hello_node">jMonkeyEngine 3 Tutorial (2) - Hello Node</h1>
<div class="level1">

<p>
Anterior: <a href="/jme3/beginner/hello_simpleapplication_pt.html" class="wikilink1" title="jme3:beginner:hello_simpleapplication_pt">Hello SimpleApplication pt</a>,
Próximo: <a href="/jme3/beginner/hello_asset_pt.html" class="wikilink1" title="jme3:beginner:hello_asset_pt">Hello Assets pt</a>. 
</p>

<p>
Neste tutorial nós daremos uma olhada na criação de uma cena 3D.
</p>
<ul>
<li class="level1"><div class="li"> Este tutorial assume que você save o que o <a href="/jme3/the_scene_graph.html" class="wikilink1" title="jme3:the_scene_graph"> grafo de cena</a> é. is.</div>
</li>
<li class="level1"><div class="li"> Para uma introdução visual, cheque o <a href="/jme3/scenegraph_for_dummies.html" class="wikilink1" title="jme3:scenegraph_for_dummies"> Grafo de Cena para Novatos</a>.</div>
</li>
</ul>

<p>
Quando criando um jogo 3D
</p>
<ol>
<li class="level1"><div class="li"> Você cria alguns objetos como jogadores, edifícios, etc.</div>
</li>
<li class="level1"><div class="li"> Você adiciona os objetos para a cena.</div>
</li>
<li class="level1"><div class="li"> Você move, redimensiona, rotaciona, colore, e anima eles.</div>
</li>
</ol>

<p>
Você aprendera que o grafo de cena representa o mundo 3D, e porque o nó raiz (rootNode) é importante. Você aprenderá como criar objetos simples, como deixá-los transportar dados customizados (como, por exemplo, pontos de saúde), e como “transformá-los” por mover, escalonar e rotacionar. Você compreenderá a diferença entre os dois tipos de “Espaciais” no grafo de cena: nós (Nodes) e geometrias (Geometries).
</p>

</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (2) - Hello Node" [1-1099] -->
<h2 class="sectionedit2" id="amostra_de_codigo">Amostra de código</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Node</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 2 - Como usar os nós como agrupamentos para manipular os objetos da cena.
 * Você pode rotacionar, mover, e redimensionar manipulando os nós pai.
 * O nó raiz (rootNode) é especial: Somente o que está ligado ao nó raiz aparece na cena. */</span>
 
<span class="kw1">public</span> <span class="kw1">class</span> HelloNode <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloNode app <span class="sy0">=</span> <span class="kw1">new</span> HelloNode<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        <span class="co3">/** cria uma caixa azul nas coordenadas (1,-1,1) */</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box1 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry blue <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box1<span class="br0">)</span><span class="sy0">;</span>
        Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
                <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        blue.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
        blue.<span class="me1">move</span><span class="br0">(</span><span class="nu0">1</span>,<span class="sy0">-</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co3">/** cria uma caixa vermelha logo acima da caixa azul em (1,3,1) */</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry red <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box2<span class="br0">)</span><span class="sy0">;</span>
        Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, 
                <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
        red.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span>
        red.<span class="me1">move</span><span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">3</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co3">/** Cria um nó pivô em (0,0,0) e liga ele ao nó raiz(rootNode) */</span>
        Node pivot <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"pivot"</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pivot<span class="br0">)</span><span class="sy0">;</span> <span class="co1">// põe este nó na cena</span>
 
        <span class="co3">/** Liga os dois cubos ao nó *pivot*. */</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>blue<span class="br0">)</span><span class="sy0">;</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>red<span class="br0">)</span><span class="sy0">;</span>
        <span class="co3">/** Rotaciona o nó pivô: Veja que ambas as caixas rotacionaram! */</span>
        pivot.<span class="me1">rotate</span><span class="br0">(</span>.4f,.4f,0f<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Construa e execute a amostra de código. Você deveria ver duas caixas coloridas inclinadas no mesmo ângulo.
</p>

</div>
<!-- EDIT2 SECTION "Amostra de código" [1100-3178] -->
<h2 class="sectionedit3" id="entendendo_a_terminologia">Entendendo a Terminologia</h2>
<div class="level2">

<p>
Neste tutorial você aprenderá alguns novos termos:
</p>
<div class="table sectionedit4"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0">O que você quer fazer </th><th class="col1"> Como você diz isso na terminologia JME3</th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Colocar a disposição da cena 3D </td><td class="col1"> Popular o grafo de cena</td>
	</tr>
	<tr class="row2">
		<td class="col0">Criar objetos da cena </td><td class="col1"> Criar espaciais (Spatials) (e.g. criar geometrias (Geometries) )</td>
	</tr>
	<tr class="row3">
		<td class="col0">Fazer um objeto aparecer na cena </td><td class="col1"> Anexar um espacial (Spatial) para o nó raiz rootNode</td>
	</tr>
	<tr class="row4">
		<td class="col0">Fazer um objeto desaparecer da cena </td><td class="col1"> Retirar um espacial (Spatial) do nó raiz rootNode</td>
	</tr>
	<tr class="row5">
		<td class="col0">Posicionar/mover, virar, ou redimensionar um objeto </td><td class="col1"> Transladar, ou rotacionar, ou escalar um objeto = transformar um objeto</td>
	</tr>
</table></div>
<!-- EDIT4 TABLE [3272-3802] -->
<p>
Toda aplicação JME3 tem um nó raiz (rootNode): Seu jogo automaticamente herda o objeto <code>rootNode</code> de SimpleApplication. Tudo anexado ao nó raiz (rootNode) é parte do grafo de cena. Os elementos do grafo de cena são os espaciais (Spatials).
</p>
<ul>
<li class="level1"><div class="li"> Um Spatial contém a localização, rotação e escala de um objeto.</div>
</li>
<li class="level1"><div class="li"> Um Spatial pode ser carregado, transformado, e salvo.</div>
</li>
<li class="level1"><div class="li"> Há dois tipos de Spatials: nós (Nodes) e geometrias (Geometries).</div>
</li>
</ul>
<div class="table sectionedit5"><table class="inline">
	<thead>
	<tr class="row0">
		<td class="col0 leftalign">  </td><th class="col1"> Geometria (Geometry) </th><th class="col2"> Nó (Node) </th>
	</tr>
	</thead>
	<tr class="row1">
		<th class="col0"> Visibilidade: </th><td class="col1"> Uma geometria (Geometry) é um objeto de cena visível </td><td class="col2"> Um nó (Node) é uma “alavanca” invisível para objetos da cena. </td>
	</tr>
	<tr class="row2">
		<th class="col0"> Propósito: </th><td class="col1"> Uma geometria (Geometry) armazena a aparência de um objeto. </td><td class="col2"> Um nó (Node) agrupa geometrias (Geometries) e outros nós (Nodes) juntos. </td>
	</tr>
	<tr class="row3">
		<th class="col0"> Exemplos: </th><td class="col1"> Uma caixa, uma esfera, um jogador, um edifício, um pedaço de terreno, um veículo, mísseis, NPCs, etc… </td><td class="col2"> O <code>nó raiz (rootNode)</code>, um nó de chão agrupando vários terrenos, um nó veículo-com-passageiros customizado, um nó jogador-com-arma, um nó de aúdio, etc… </td>
	</tr>
</table></div>
<!-- EDIT5 TABLE [4256-4886] -->
</div>
<!-- EDIT3 SECTION "Entendendo a Terminologia" [3179-4887] -->
<h2 class="sectionedit6" id="entendendo_o_codigo">Entendendo o Código</h2>
<div class="level2">

<p>
O que acontece no trecho de código? Você usa o método <code>simpleInitApp()</code> que foi introduzido no primeiro tutorial para inicializar a cena.
</p>
<ol>
<li class="level1"><div class="li"> Você cria a primeira geometria caixa.</div>
<ul>
<li class="level2"><div class="li"> Crie uma forma caixa (Box) com extensões de (1,1,1), isto faz a caixa 2x2x2 unidades do mundo grande.</div>
</li>
<li class="level2"><div class="li"> Posicione a caixa em (1,-1,1) usando o método move() method. (Não mude o Vector3f.ZERO a menos que você queira mudar o centro de rotação)</div>
</li>
<li class="level2"><div class="li"> Envolva a forma caixa (Box) em uma geometria (Geometry).</div>
</li>
<li class="level2"><div class="li"> Crie um material azul</div>
</li>
<li class="level2"><div class="li"> Aplique o material azul para a geometria da caixa (Box Geometry). <pre class="code java">    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box1 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    Geometry blue <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box1<span class="br0">)</span><span class="sy0">;</span>
    Material mat1 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
      <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat1.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
    blue.<span class="me1">setMaterial</span><span class="br0">(</span>mat1<span class="br0">)</span><span class="sy0">;</span>
    blue.<span class="me1">move</span><span class="br0">(</span><span class="nu0">1</span>,<span class="sy0">-</span><span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Você cria uma segunda geometria (Geometry) de caixa.</div>
<ul>
<li class="level2"><div class="li"> Crie uma segunda forma caixa (Box) com o mesmo tamanho.</div>
</li>
<li class="level2"><div class="li"> Posicione a segunda caixa em (1,3,1). Isto é imediatamente acima da primeira caixa, com uma lacuna de 2 unidades do mundo entre elas.</div>
</li>
<li class="level2"><div class="li"> Envolva a forma caixa (Box) em uma geometria (Geometry).</div>
</li>
<li class="level2"><div class="li"> Crie um material vermelho</div>
</li>
<li class="level2"><div class="li"> Aplique o material vermelho para a geometria caixa (Box Geometry). <pre class="code java">    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span> Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>,<span class="nu0">1</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
    Geometry red <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box2<span class="br0">)</span><span class="sy0">;</span>
    Material mat2 <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
      <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
    mat2.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Red</span><span class="br0">)</span><span class="sy0">;</span>
    red.<span class="me1">setMaterial</span><span class="br0">(</span>mat2<span class="br0">)</span><span class="sy0">;</span>
    red.<span class="me1">move</span><span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">3</span>,<span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Você cria um nó (Node) pivô. </div>
<ul>
<li class="level2"><div class="li"> Nomeie o nó “pivot”.</div>
</li>
<li class="level2"><div class="li"> Por padrão o nó (Node) é posicionado em (0,0,0).</div>
</li>
<li class="level2"><div class="li"> Anexe o nó (Node) ao nó raiz (rootNode).</div>
</li>
<li class="level2"><div class="li"> O nó (Node) não tem aparência visível na cena. <pre class="code java">    Node pivot <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span><span class="st0">"pivot"</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>pivot<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Se você executar a aplicação somente com o código dado até aqui, a cena parece vazia. Isto é porque o nó (Node) está invisível, e você não tem ainda anexado quaisquer geometrias (Geometries) visíveis para o nó raiz (rootNode).. 
</p>
</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Anexe as duas caixas para o nó pivô <pre class="code java">        pivot.<span class="me1">attachChild</span><span class="br0">(</span>blue<span class="br0">)</span><span class="sy0">;</span>
        pivot.<span class="me1">attachChild</span><span class="br0">(</span>red<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Se você executar o aplicativo com somente o código dado até aqui, você vê dois cubos: Um vermelho imediatamente acima de um azul.
</p>
</div>
</li>
<li class="level1"><div class="li"> Rotacione o nó pivô.<pre class="code java">        pivot.<span class="me1">rotate</span><span class="br0">(</span> 0.4f , 0.4f , 0.0f <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Se você executar o aplicativo agora, você verá duas caixas uma no topo da outra - ambas inclinadas no mesmo ângulo.
</p>
</div>
</li>
</ol>

</div>
<!-- EDIT6 SECTION "Entendendo o Código" [4888-7578] -->
<h3 class="sectionedit7" id="o_que_e_um_no_pivo_pivot_node">O que é um nó pivô (Pivot Node)?</h3>
<div class="level3">

<p>
Você pode transformar (e.g. rotacionar) geometrias (Geometries) ao redor do próprio centro delas, ou ao redor de um ponto central definido pelo usuário. Um ponto central definido pelo usuário para um ou mais geometrias (Geometries) é chamado pivô.
</p>
<ul>
<li class="level1"><div class="li"> Neste exemplo, você agrupou duas geometrias (Geometries) por anexá-las para um nó pivô (Node). Você vê o nó (Node) pivô como um instrumento para rotacionar as duas geometrias (Geometries) ao mesmo tempo ao redor de um centro em comum. Rotacionar o nó (Node) pivô rotaciona todas as geometrias (Geometries) anexadas, de uma única vez. O nó pivô é o centro da rotação. Antes de anexar as outras geometrias (Geometries), tenha certeza que o nó pivô está em (0,0,0). Transformar um nó (Node) pai para transformar todas as crianças espaciais (Spatials) anexadas é uma tarefa comum. Você usará este método muito em seus jogos quando você mover espaciais (Spatials).</div>
</li>
</ul>

<p>
Exemplos: Um veículo e seu motorista movem juntos; um planeta com sua lua orbitam o sol.
</p>
<ul>
<li class="level1"><div class="li"> Contraste este caso com a outra opção: Se você não criar um nó pivô extra e transformar uma geometria (Geometry), então toda transformação é feita relativa a origem da geometria (Geometry) (tipicamente o centro dela). <br />
<strong>Exemplos:</strong>  Se você rotacionar cada cubo diretamente (usando <code>red.rotate(0.1f , 0.2f , 0.3f);</code> e <code>blue.rotate(0.5f , 0.0f , 0.25f);</code>), então cada cubo é rotacionado individualmente ao redor do seu centro. Isto é similar a um planeta rotacionando ao redor de seu próprio centro.</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "O que é um nó pivô (Pivot Node)?" [7579-9184] -->
<h2 class="sectionedit8" id="como_eu_populo_o_grafo_de_cena">Como eu Populo o Grafo de Cena?</h2>
<div class="level2">
<div class="table sectionedit9"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Tarefa…? </th><th class="col1"> Solução! </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Crie um espacial (Spatial) </td><td class="col1"> Crie uma forma malha (Mesh), envolva ela em uma geometria (Geometry), e dê a ela um Material. Por exemplo: <pre class="code java"><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> mesh <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// a cuboid default mesh</span>
Geometry thing <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"thing"</span>, mesh<span class="br0">)</span><span class="sy0">;</span> 
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
   <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
thing.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row2">
		<td class="col0"> Faça um objeto aparecer na cena </td><td class="col1"> Anexe o espacial (Spatial) para o <code>nó raiz (rootNode)</code>, ou para qualquer no que esteja anexado para o nó raiz (rootNode). <pre class="code java">rootNode.<span class="me1">attachChild</span><span class="br0">(</span>thing<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row3">
		<td class="col0"> Remova objetos da cena </td><td class="col1"> Retire o nó espacial (Spatial) do <code>nó raiz (rootNode)</code>, e de qualquer nó que esteja vinculado ao nó raiz (rootNode). <pre class="code java">rootNode.<span class="me1">detachChild</span><span class="br0">(</span>thing<span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">rootNode.<span class="me1">detachAllChildren</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row4">
		<td class="col0"> Ache um nó espacial na cena pelo nome do objeto, ou ID, ou por sua posição na hierarquia pai-criança. </td><td class="col1"> Olhe na criança ou pai do nó:  <pre class="code java">Spatial thing <span class="sy0">=</span> rootNode.<span class="me1">getChild</span><span class="br0">(</span><span class="st0">"thing"</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial twentyThird <span class="sy0">=</span> rootNode.<span class="me1">getChild</span><span class="br0">(</span><span class="nu0">22</span><span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial parent <span class="sy0">=</span> myNode.<span class="me1">getParent</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row5">
		<td class="col0"> Especifique o que deveria ser carregado no início </td><td class="col1"> Tudo que você inicializa e anexa ao <code>nó raiz (rootNode)</code> no método <code>simpleInitApp()</code> é parte da cena no início do jogo. </td>
	</tr>
</table></div>
<!-- EDIT9 TABLE [9230-10610] -->
</div>
<!-- EDIT8 SECTION "Como eu Populo o Grafo de Cena?" [9185-10611] -->
<h2 class="sectionedit10" id="como_eu_transformo_espaciais_spatials">Como eu transformo espaciais (Spatials)?</h2>
<div class="level2">

<p>
Há três tipos de transformação 3D: Translação, Escalonamento, e Rotação.
</p>
<div class="table sectionedit11"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Translação move espaciais (Spatials ) </th><th class="col1"> eixo X-</th><th class="col2"> eixo Y </th><th class="col3"> eixo Z </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"></td><td class="col1"></td><td class="col2"></td><td class="col3"></td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [10748-10933] -->
<p>
Para mover um espacial (Spatial) para coordenadas específicas, tais como (0,40.2f,-2), use:  
</p>
<pre class="code java">thing.<span class="me1">setLocalTranslation</span><span class="br0">(</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span> 0.0f, 40.2f, <span class="sy0">-</span>2.0f <span class="br0">)</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Para mover um espacial (Spatial) por uma certa quantia, e.g. mais acima (y=40.2f) e mais atrás (z=-2.0f): 
</p>
<pre class="code java">thing.<span class="me1">move</span><span class="br0">(</span> 0.0f, 40.2f, <span class="sy0">-</span>2.0f <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 |+right -left|+up -down|+forward -backward|
</p>
<div class="table sectionedit12"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Escalonamento redimensiona espaciais (Spatials) </th><th class="col1"> eixo X-</th><th class="col2"> eixo Y </th><th class="col3"> eixo Z </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Especifique o fator de escalonamento em cada dimensão: tamanho, altura, comprimento. <br />
 um valor entre 0.0f e 1.0f diminue o espacial (Spatial); maior que 1.0f estica ele; 1.0f mantém ele o mesmo. <br />
 Usando o mesmo valor para cada dimensão escalona proporcionalmente, valor diferentes esticam ele. <br />
 Para escalonar um espacial (Spatial) 10 vezes mais longo, um décimo da altura, e manter o mesmo comprimento:  <pre class="code java">thing.<span class="me1">scale</span><span class="br0">(</span> 10.0f, 0.1f, 1.0f <span class="br0">)</span><span class="sy0">;</span></pre>
</td><td class="col1">length</td><td class="col2">height</td><td class="col3">width</td>
	</tr>
</table></div>
<!-- EDIT12 TABLE [11315-11886] --><div class="table sectionedit13"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Rotação gira espaciais (Spatials) </th><th class="col1"> eixo X-</th><th class="col2"> eixo Y </th><th class="col3"> eixo Z </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0">Rotação 3-D é um pouco complicado (<a href="/jme3/rotate.html" class="wikilink1" title="jme3:rotate">aprenda os detalhes aqui</a>)). em breve: Você pode rotacionar ao redor de três eixos: Pitch (X), yaw (Y), e roll (Z). Você pode especificar ângulos em graus por multiplicar o valor de graus com <code>FastMath.DEG_TO_RAD</code>. <br />
 Para rolar um objeto 180° ao redor do z axis: : <pre class="code java">thing.<span class="me1">rotate</span><span class="br0">(</span> 0f , 0f , <span class="nu0">180</span><span class="sy0">*</span>FastMath.<span class="me1">DEG_TO_RAD</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Tip: Dica: Se sua idéia de jogo pede uma quantidade séria de rotações, é merecedor dar uma olhada em <a href="/jme3/quaternion.html" class="wikilink1" title="jme3:quaternion">quaternion</a>s, uma estrutura de dado que pode combinar e armazenar rotações eficientemente. 
</p>
<pre class="code java">thing.<span class="me1">setLocalRotation</span><span class="br0">(</span> 
  <span class="kw1">new</span> Quaternion<span class="br0">(</span><span class="br0">)</span>.<span class="me1">fromAngleAxis</span><span class="br0">(</span><span class="nu0">180</span><span class="sy0">*</span>FastMath.<span class="me1">DEG_TO_RAD</span>, <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">1</span>,<span class="nu0">0</span>,<span class="nu0">0</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>
</td><td class="col1">pitch = fazer um sinal de sim com sua cabeça</td><td class="col2">yaw = agitar sua cabeça</td><td class="col3">roll = inclinar sua cabeça</td>
	</tr>
</table></div>
<!-- EDIT13 TABLE [11888-12785] -->
</div>
<!-- EDIT10 SECTION "Como eu transformo espaciais (Spatials)?" [10612-12786] -->
<h2 class="sectionedit14" id="como_eu_resolvo_problemas_com_espaciais_spatials">Como eu Resolvo Problemas com espaciais (Spatials)?</h2>
<div class="level2">

<p>
Se você obtém resultados inesperados, cheque se você fez os seguintes enganos frequentes:
</p>
<div class="table sectionedit15"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> Problema? </th><th class="col1"> Solução! </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Geometria (Geometry) criada não aparece na cena. </td><td class="col1"> Você anexou ela a (um nó que está vinculado a) o nó raiz (rootNode)? <br />
 Ela tem um Material? <br />
 Qual é sua translação (posição)? Ela está atrás da câmera ou coberta por uma outra geometria (Geometry)? <br />
 Ela é tão minúscula ou tão gigante para ver? <br />
 Ela está tão distante da câmera? (Tente <a href="http://jmonkeyengine.org/javadoc/com/jme3/renderer/Camera.html#setFrustumFar%28float%29" class="urlextern" title="http://jmonkeyengine.org/javadoc/com/jme3/renderer/Camera.html#setFrustumFar%28float%29" rel="nofollow">cam.setFrustumFar</a>(111111f); para ver mais distante) </td>
	</tr>
	<tr class="row2">
		<td class="col0"> Um espacial (Spatial) rotaciona em maneiras inesperadas. </td><td class="col1"> Você usou os valores em radianos, e não em graus? (Se você usou graus, multiplique eles com FastMath.DEG_TO_RAD para convertê-los para radianos) <br />
 Você criou o espacial (Spatial) na origem (Vector.ZERO) antes de movê-lo? <br />
 Você rotacionou ao redor do nó pivô ou ao redor de algo mais? <br />
 Você rotacionou ao redor do eixo certo? </td>
	</tr>
	<tr class="row3">
		<td class="col0"> Uma geometria (Geometry) tem cor (Color) ou Material inepserado. </td><td class="col1 leftalign"> Você reusou um Material de uma outra geometria (Geometry) e tem inadvertidamente mudado suas propriedades? (Se sim, considere cloná-lo: mat2 = mat.clone(); )  </td>
	</tr>
</table></div>
<!-- EDIT15 TABLE [12946-14125] -->
</div>
<!-- EDIT14 SECTION "Como eu Resolvo Problemas com espaciais (Spatials)?" [12787-14126] -->
<h2 class="sectionedit16" id="como_eu_adiciono_um_dado_customizado_para_espaciais_spatials">Como eu Adiciono um Dado Customizado para espaciais (Spatials)?</h2>
<div class="level2">

<p>
Muitos espaciais (Spatials) representam personagens ou outras entidades que o jogador pode interagir. O código acima que rotaciona as duas caixas ao redor de um centro em comum (pivô) poderia ser usado para uma espaçonave estacionada em uma estação espacial orbital, por exemplo.
</p>

<p>
Dependendo do seu jogo, entidades de jogo não somente mudam a posição delas, rotação ou escala (as transformações que você aprendeu). Entidades de jogo também têm propriedades personalizadas, como saúde, inventário carregado, equipamento usado para um personagem, ou força do casco e combustível restante para uma aeronave. Em Java, você representa dados de entidade como variáveis de classe, e.g. floats, Strings, ou Arrays.
</p>

<p>
Você pode adicionar dados personalizados diretamente para qualquer nó (Node) ou geometria (Geometry). <strong> Você não precisa estender a classe nó (Node) para incluir variáveis! </strong>
</p>

<p>
Por exemplo, para adicionar um número de id customizado para um nó, você usaria:
</p>
<pre class="code java">pivot.<span class="me1">setUserData</span><span class="br0">(</span> <span class="st0">"pivot id"</span>, <span class="nu0">42</span> <span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Para ler o id do nó (Node) em outro lugar, você usaria:
</p>
<pre class="code java"><span class="kw4">int</span> id <span class="sy0">=</span> pivot.<span class="me1">getUserData</span><span class="br0">(</span> <span class="st0">"pivot id"</span> <span class="br0">)</span><span class="sy0">;</span> </pre>

<p>
Por usar diferentes chaves de Strings (aqui a chave é o <code>id do pivô</code>), você pode recuperar e configurar vários valores para quaisquer dados que o espacial (Spatial) precisa carregar. Quando você iniciar a escrever seu jogo, você talvez adicione um valor de combustível para um nó carro, valor de velocidade para um nó avião, ou número de moedas douradas para um nó jogador, e muito mais. Entretanto, deve-se notar que somente objetos customizados que implementam Savable podem ser passados.
</p>

</div>
<!-- EDIT16 SECTION "Como eu Adiciono um Dado Customizado para espaciais (Spatials)?" [14127-15882] -->
<h2 class="sectionedit17" id="conclusao">Conclusão</h2>
<div class="level2">

<p>
Você aprenderu que sua cena 3D é um grafo de cena composto de espaciais (Spatials): Geometrias (Geometries) visíveis e nós (Nodes) invisíveis. Você pode transformar espaciais (Spatials), ou anexá-los a nós e transformar os nós. Você sabe a maneira mais fácil de como adicionar propriedades de entidade customizadas (tais como a saúde do jogador ou a velocidade do veículo) para espaciais (Spatials).
</p>

<p>
Desde que formas padrões como esferas e caixas ficam velhas rápido, continue com o próximo capítulo onde você aprenderá a <a href="/jme3/beginner/hello_asset.html" class="wikilink1" title="jme3:beginner:hello_asset"> carregar ativos, como por exemplo, modelos 3-D</a>.
</p>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/rootnode.html" class="wikilink1" title="tag:rootnode" rel="tag">rootNode</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/color.html" class="wikilink1" title="tag:color" rel="tag">color</a>,
	<a href="/tag/spatial.html" class="wikilink1" title="tag:spatial" rel="tag">spatial</a>,
	<a href="/tag/geometry.html" class="wikilink1" title="tag:geometry" rel="tag">geometry</a>,
	<a href="/tag/scenegraph.html" class="wikilink1" title="tag:scenegraph" rel="tag">scenegraph</a>,
	<a href="/tag/mesh.html" class="wikilink1" title="tag:mesh" rel="tag">mesh</a>
</span></div>

</div>
<!-- EDIT17 SECTION "Conclusão" [15883-] -->
