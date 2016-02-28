---
title: jMonkeyEngine 3 Tutorial (3) - Hello Assets
---
<h1 class="sectionedit1" id="jmonkeyengine_3_tutorial_3_-_hello_assets">jMonkeyEngine 3 Tutorial (3) - Hello Assets</h1>
<div class="level1">

<p>
Anterior: <a href="/jme3/beginner/hello_node_pt.html" class="wikilink1" title="jme3:beginner:hello_node_pt"> Hello Node pt</a>,
Próximo: <a href="/jme3/beginner/hello_main_event_loop_pt.html" class="wikilink1" title="jme3:beginner:hello_main_event_loop_pt"> Hello Update Loop pt</a>
</p>

<p>
Neste tutorial nós aprenderemos a carregar modelos 3D e colcoar texto no grafo de cena, usando o <a href="/jme3/advanced/asset_manager.html" class="wikilink1" title="jme3:advanced:asset_manager"> Gerenciador de Ativo (Asset Manager)</a> da JME. Você também aprenderá como determinar os caminhos corretos, e quais formatos de arquivo usar.
</p>

<p>
<a href="/resources/jme3-beginner-beginner-assets-models.png" class="media" title="jme3:beginner:beginner-assets-models.png"><img src="/resources/jme3-beginner-beginner-assets-models.png" class="mediacenter" alt="" width="320" height="250" /></a>
</p>

<p>
</p><p></p><div class="notetip"><a href="/sdk/sample_code.html" class="wikilink1" title="sdk:sample_code"> Problema no achar os arquivos para executar a amostra?</a> Para conseguir os ativos (modelos 3D), adicione o arquivo <code>jme3-test-data.jar</code> incluso para seu classpath. no projeto criado com o SDK da jMonkeyEngine (recomendado), simplesmente dê um clique com o botão direito em seu projeto, escolha “Propriedades” (“Properties”), vá para “Bibliotecas” (“Libraries”), pressione “Adicionar Biblioteca” (“Add Library”) e adiciona a biblioteca pré-configurada “jme3-test-data” library. 
</div>


</div>
<!-- EDIT1 SECTION "jMonkeyEngine 3 Tutorial (3) - Hello Assets" [1-1038] -->
<h2 class="sectionedit2" id="amostra_de_codigo">Amostra de Código</h2>
<div class="level2">
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.font.BitmapText</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.light.DirectionalLight</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Spatial</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
 
<span class="co3">/** Sample 3 - how to load an OBJ model, and OgreXML model, 
 * a material/texture, or text. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloAssets <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        HelloAssets app <span class="sy0">=</span> <span class="kw1">new</span> HelloAssets<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
        Spatial teapot <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Teapot/Teapot.obj"</span><span class="br0">)</span><span class="sy0">;</span>
        Material mat_default <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span> 
            assetManager, <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        teapot.<span class="me1">setMaterial</span><span class="br0">(</span>mat_default<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>teapot<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Create a wall with a simple texture from test_data</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, 2.5f,2.5f,1.0f<span class="br0">)</span><span class="sy0">;</span>
        Spatial wall <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box <span class="br0">)</span><span class="sy0">;</span>
        Material mat_brick <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span> 
            assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat_brick.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, 
            assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/BrickWall/BrickWall.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        wall.<span class="me1">setMaterial</span><span class="br0">(</span>mat_brick<span class="br0">)</span><span class="sy0">;</span>
        wall.<span class="me1">setLocalTranslation</span><span class="br0">(</span>2.0f,<span class="sy0">-</span>2.5f,0.0f<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>wall<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Display a line of text with a default font</span>
        guiNode.<span class="me1">detachAllChildren</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
        BitmapText helloText <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
        helloText.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        helloText.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Hello World"</span><span class="br0">)</span><span class="sy0">;</span>
        helloText.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">300</span>, helloText.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
        guiNode.<span class="me1">attachChild</span><span class="br0">(</span>helloText<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="co1">// Load a model from test_data (OgreXML + material + texture)</span>
        Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
        ninja.<span class="me1">scale</span><span class="br0">(</span>0.05f, 0.05f, 0.05f<span class="br0">)</span><span class="sy0">;</span>
        ninja.<span class="me1">rotate</span><span class="br0">(</span>0.0f, <span class="sy0">-</span>3.0f, 0.0f<span class="br0">)</span><span class="sy0">;</span>
        ninja.<span class="me1">setLocalTranslation</span><span class="br0">(</span>0.0f, <span class="sy0">-</span>5.0f, <span class="sy0">-</span>2.0f<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>ninja<span class="br0">)</span><span class="sy0">;</span>
        <span class="co1">// You must add a light to make the model visible</span>
        DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f, <span class="sy0">-</span>0.7f, <span class="sy0">-</span>1.0f<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span>
 
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Compile e execute a amostra de código. Você deveria ver um ninja verde com um bule colorido permanecendo atrás de uma parede. O texto na tela deveria dizer “Hello World”.
</p>

</div>
<!-- EDIT2 SECTION "Amostra de Código" [1039-3674] -->
<h2 class="sectionedit3" id="o_gerenciador_de_ativo">O gerenciador de ativo</h2>
<div class="level2">

<p>
<strong>Por ativos de jogo nós queremos dizer todos os arquivos multimídia, tais como modelos, materiais e texturas, cenas inteiras, shaders customizados, música e arquivos de som, e fontes customizadas.</strong> JME3 vem com um objeto AssetManager prático que ajuda você a acessar seus ativos. 
O AssetManager pode carregar arquivos de:
</p>
<ul>
<li class="level1"><div class="li"> O classpath atual (o nível do topo de seu diretório de projeto),</div>
</li>
<li class="level1"><div class="li"> O diretório <code>ativos</code> de seu projeto, e</div>
</li>
<li class="level1"><div class="li"> opcionalmente, caminhos persoanlizados que você registrar.</div>
</li>
</ul>

<p>
O seguinte é a estrutura de diretório recomendada em seu diretório de projeto: 
</p>
<pre class="code">MyGame/assets/Interface/
MyGame/assets/MatDefs/
MyGame/assets/Materials/
MyGame/assets/Models/
MyGame/assets/Scenes/
MyGame/assets/Shaders/
MyGame/assets/Sounds/
MyGame/assets/Textures/
MyGame/build.xml            &lt;-- Ant build script
MyGame/src/...              &lt;-- Java sources go here
MyGame/...</pre>

<p>
Isto é apenas um melhor prática sugerida, e é o que você consegue por padrão quando criando um novo projeto Java no <a href="/doku.php/jme3:beginner:sdk" class="wikilink2" title="jme3:beginner:sdk" rel="nofollow">SDK</a> da jMokeyEngine. Você pode criar um diretório de ativos e tecnicamente nomear os subdiretórios da maneira que você gostar.
</p>

</div>
<!-- EDIT3 SECTION "O gerenciador de ativo" [3675-4877] -->
<h3 class="sectionedit4" id="carregando_texturas">Carregando Texturas</h3>
<div class="level3">

<p>
Coloque suas texturas em um subdiretório de <code>assets/Textures/</code>. Carregue a textura em um material antes que você configure o Material. A seguinte amostra de código é do método <code>simpleInitApp()</code> e carrega um modelo de parede simples:
</p>
<pre class="code java"><span class="co1">// Create a wall with a simple texture from test_data</span>
<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> box <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, 2.5f,2.5f,1.0f<span class="br0">)</span><span class="sy0">;</span>
Spatial wall <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, box <span class="br0">)</span><span class="sy0">;</span>
Material mat_brick <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span> 
    assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
mat_brick.<span class="me1">setTexture</span><span class="br0">(</span><span class="st0">"ColorMap"</span>, 
    assetManager.<span class="me1">loadTexture</span><span class="br0">(</span><span class="st0">"Textures/Terrain/BrickWall/BrickWall.jpg"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
wall.<span class="me1">setMaterial</span><span class="br0">(</span>mat_brick<span class="br0">)</span><span class="sy0">;</span>
wall.<span class="me1">setLocalTranslation</span><span class="br0">(</span>2.0f,<span class="sy0">-</span>2.5f,0.0f<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>wall<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Neste caso, você <a href="/jme3/beginner/hello_material.html" class="wikilink1" title="jme3:beginner:hello_material">cria seu próprio Material</a> e aplica ele para a geometria (Geometry). Você baseia Materiais nas descrições de material padrão (por exemplo, “Unshaded.j3md”), como mostrado neste exemplo.
</p>

</div>
<!-- EDIT4 SECTION "Carregando Texturas" [4878-5847] -->
<h3 class="sectionedit5" id="carregando_texto_e_fontes">Carregando Texto e Fontes</h3>
<div class="level3">

<p>
Este exemplo exibe o texto “Hello World” na fonte padrão na aresta do fundo da janela. Você anexa texto para o nó da <abbr title="Graphical User Interface">GUI</abbr> (<code>guiNode</code>) – isto é um nó especial para elementos de exibição plana (ortogonal). Você exibe texto para mostrar a pontuação do jogo, a saúde do jogador, etc. 
A seguinte amostra de código vai no método <code>simpleInitApp()</code>.
</p>
<pre class="code java"><span class="co1">// Display a line of text with a default font</span>
guiNode.<span class="me1">detachAllChildren</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
guiFont <span class="sy0">=</span> assetManager.<span class="me1">loadFont</span><span class="br0">(</span><span class="st0">"Interface/Fonts/Default.fnt"</span><span class="br0">)</span><span class="sy0">;</span>
BitmapText helloText <span class="sy0">=</span> <span class="kw1">new</span> BitmapText<span class="br0">(</span>guiFont, <span class="kw2">false</span><span class="br0">)</span><span class="sy0">;</span>
helloText.<span class="me1">setSize</span><span class="br0">(</span>guiFont.<span class="me1">getCharSet</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getRenderedSize</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
helloText.<span class="me1">setText</span><span class="br0">(</span><span class="st0">"Hello World"</span><span class="br0">)</span><span class="sy0">;</span>
helloText.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">300</span>, helloText.<span class="me1">getLineHeight</span><span class="br0">(</span><span class="br0">)</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
guiNode.<span class="me1">attachChild</span><span class="br0">(</span>helloText<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Dica:</strong> Limpe o texto existente no nó da <abbr title="Graphical User Interface">GUI</abbr> (guiNode) por retirar todas as suas crianças.
</p>

</div>
<!-- EDIT5 SECTION "Carregando Texto e Fontes" [5848-6748] -->
<h3 class="sectionedit6" id="carregando_um_modelo">Carregando um modelo</h3>
<div class="level3">

<p>
Exporte seu modelo 3D no formato OgreXML (.mesh.xml, .scene, .material, .skeleton.xml) e coloque ele em um subdiretório de <code>assets/Models/</code>. A seguinte amostra de código vai no método <code>simpleInitApp()</code>.
</p>
<pre class="code java"><span class="co1">// Load a model from test_data (OgreXML + material + texture)</span>
Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
ninja.<span class="me1">scale</span><span class="br0">(</span>0.05f, 0.05f, 0.05f<span class="br0">)</span><span class="sy0">;</span>
ninja.<span class="me1">rotate</span><span class="br0">(</span>0.0f, <span class="sy0">-</span>3.0f, 0.0f<span class="br0">)</span><span class="sy0">;</span>
ninja.<span class="me1">setLocalTranslation</span><span class="br0">(</span>0.0f, <span class="sy0">-</span>5.0f, <span class="sy0">-</span>2.0f<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>ninja<span class="br0">)</span><span class="sy0">;</span>
<span class="co1">// You must add a directional light to make the model visible!</span>
DirectionalLight sun <span class="sy0">=</span> <span class="kw1">new</span> DirectionalLight<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
sun.<span class="me1">setDirection</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="sy0">-</span>0.1f, <span class="sy0">-</span>0.7f, <span class="sy0">-</span>1.0f<span class="br0">)</span>.<span class="me1">normalizeLocal</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">addLight</span><span class="br0">(</span>sun<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
Note que você precisa criar um Material se você exportou o modelo com um material. Lembre-se de adicionar uma fonte de luz, como mostrado, de outra maneira o material (e o modelo inteiro) não estará visível!
</p>

</div>
<!-- EDIT6 SECTION "Carregando um modelo" [6749-7706] -->
<h3 class="sectionedit7" id="carregando_ativos_de_caminhos_personalizados">Carregando Ativos de Caminhos Personalizados</h3>
<div class="level3">

<p>
E seu jogo dependen de arquivos de modelo fornecidos pelo usuário, que não estão inclusos na distribuição? Se um arquivo não é localizado no local padrão (e.g. diretório de ativos), você pode registrar um localizador (Locator) customizado e carregá-lo de qualquer caminho.
</p>

<p>
Aqui está um exemplo de uso de um ZipLocator que está registrado para um arquivo <code>town.zip</code> no nível topo de seu diretório de projeto:
</p>
<pre class="code java">    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Aque está um HttpZipLocator que pode baixar modelos zipados e carregá-los: 
</p>
<pre class="code java">    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span>
      <span class="st0">"http://jmonkeyengine.googlecode.com/files/wildhouse.zip"</span>, 
      HttpZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
JME3 oferece ClasspathLocator, ZipLocator, FileLocator, HttpZipLocator, e UrlLocator (Veja <code>com.jme3.asset.plugins</code>). 
</p>

</div>
<!-- EDIT7 SECTION "Carregando Ativos de Caminhos Personalizados" [7707-8808] -->
<h2 class="sectionedit8" id="criando_modelos_e_cenas">Criando Modelos e Cenas</h2>
<div class="level2">

<p>
Para criar modelos 3D e cenas, você precisa de um editor de malha 3D (3D Mesh Editor) com um plugin exportador (Exporter) OgreXML. Por exemplo, você pode <a href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/UV_Map_Basics" class="urlextern" title="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/UV_Map_Basics" rel="nofollow"> criar modelos completamente texturizados com Blender</a>. 
</p>

<p>
Você pode usar o <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> para <a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer">carregar modelos</a>, <a href="/sdk/blender.html" class="wikilink1" title="sdk:blender"> converter modelos</a> e <a href="/sdk/scene_composer.html" class="wikilink1" title="sdk:scene_composer"> criar cenas</a> deles.
</p>

<p>
Se você usar Blender, exporte seus modelos como malhas Ogre XML com materiais como se segue:
</p>
<ol>
<li class="level1"><div class="li"> Abra o menu Arquivo (File) &gt; Exportar (Export) &gt; Exportador OgreXML (OgreXML Exporter) para abrir o diálogo do exportador.</div>
</li>
<li class="level1"><div class="li"> No campo Exportar Materiais (Export Materials): Dê ao material o mesmo nome que o modelo. Por exemplo, o modelo <code>something.mesh.xml</code> acompanha <code>something.material</code>, mais (opcionalmente) <code>something.skeleton.xml</code> e alguns arquivos de textura JPG.</div>
</li>
<li class="level1"><div class="li"> No campo Exportar Malhas (Export Meshes): Selecione um subdiretório de seu diretório <code>assets/Models/</code> directory. E.g. <code>assets/Models/something/</code>.</div>
</li>
<li class="level1"><div class="li"> Ative as seguintes configurações do exportador:</div>
<ul>
<li class="level2"><div class="li"> Copiar Texturas (Copy Textures): YES</div>
</li>
<li class="level2"><div class="li"> Renderizar materiais (Rendering Materials): YES</div>
</li>
<li class="level2"><div class="li"> Virar Eixos (Flip Axis): YES</div>
</li>
<li class="level2"><div class="li"> Requer Materiais (Require Materials): YES</div>
</li>
<li class="level2"><div class="li"> Nome do Esqueleto segue o da malha (Skeleton name follows mesh): YES</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Clique em exportar.</div>
</li>
</ol>

</div>
<!-- EDIT8 SECTION "Criando Modelos e Cenas" [8809-10266] -->
<h3 class="sectionedit9" id="formatos_de_arquivo_de_modelo">Formatos de Arquivo de Modelo</h3>
<div class="level3">

<p>
JME3 pode carregar modelos Ogre XML + materials, Ogre DotScenes, bem como modelos Wavefront OBJ+MTL models. O código loadModel() trabalha com estes arquivos quando você executa o código diretamente do SDK da jMonkeyEngine SDK.
</p>

<p>
Se você construir os executáveis usando o scrit de construção padrão, então os arquivos de modelo originais (XML, OBJ, etc) não são inclusos. Quando você executar o executável, você obetrá uma mensagem de erro se você tentar carregar quaisquer modelos diretamente:
</p>
<pre class="code">com.jme3.asset.DesktopAssetManager loadAsset
WARNING: Cannot locate resource: Models/Ninja/Ninja.mesh.xml
com.jme3.app.Application handleError
SEVERE: Uncaught exception thrown in Thread[LWJGL Renderer Thread,5,main]
java.lang.NullPointerException</pre>

<p>
Carregando os arquivos XML/OBJ diretamente é somente aceitável durante a fase de desenvolvimento. Se seus projetista gráfico coloca arquivos atualizados para o diretório de ativos, você pode rapidamente revisar a versão mais recente em seu ambiente de desenvolvimento.
</p>

<p>
Para teste e para a construção de liberação final, voc~e usa arquivos .j3o exclusivamente. J3o é um formato binário otimizado para aplicações jME3, e arquivos .j3o são automaticamente inclusos no arquivo JAR distribuível pelo script de construção. Quando você faz construções de teste de QA (Quality and Assurance - Averiguação da Qualidade) ou está pronto para liberar, use o <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> para <a href="/sdk/model_loader_and_viewer.html" class="wikilink1" title="sdk:model_loader_and_viewer"> converter</a> todos os arquivos .obj/.scene/.xml/.blend para .j3o, e somente carregue as versões .j3o.
</p>

<p>
Abra seu Projeto JME3 no SDK da jMonkeyEngine.
</p>
<ol>
<li class="level1"><div class="li"> Dê um clique com o botão direito em um arquivo .Blend, .OBJ, ou .mesh.xml file na janela Projetos (Projects), e escolha “converter para binário JME3” (“convert to JME3 binary”).. </div>
</li>
<li class="level1"><div class="li"> O arquivo .j3o aparece próximo ao arquivo .mesh.xml file e tem o mesmo nome.</div>
</li>
<li class="level1"><div class="li"> Mude todas as linhas do seu loadModel() de acordo. Por exemplo: <pre class="code java">Spatial ninja <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Ninja/Ninja.j3o"</span><span class="br0">)</span><span class="sy0">;</span></pre>
</div>
</li>
</ol>

<p>
Se seu executável dá uma exceção em tempo de execução, tenha certeza de que você converteu todos os modelos para .j3o!
</p>

</div>
<!-- EDIT9 SECTION "Formatos de Arquivo de Modelo" [10267-12495] -->
<h3 class="sectionedit10" id="carregando_modelos_e_a_cena">Carregando Modelos e a Cena</h3>
<div class="level3">
<div class="table sectionedit11"><table class="inline">
	<thead>
	<tr class="row0">
		<th class="col0"> tarefa? </th><th class="col1"> Solução! </th>
	</tr>
	</thead>
	<tr class="row1">
		<td class="col0"> Carregar um modelo com materiais </td><td class="col1"> Use o método <code>loadModel()</code> do gerenciador de ativo (asset manager) e anexe o Spatial para o nó raiz (rootNode). <pre class="code java">Spatial elephant <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Elephant/Elephant.mesh.xml"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>elephant<span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial elephant <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Elephant/Elephant.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>elephant<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row2">
		<td class="col0"> carregar um modelo sem materiais </td><td class="col1"> Se você tiver um modelo sem materiais, você tem de dár a ele um material para fazê-lo visível. <pre class="code java">Spatial teapot <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Models/Teapot/Teapot.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/ShowNormals.j3md"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// default material</span>
teapot.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>teapot<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
	<tr class="row3">
		<td class="col0"> Carregar uma cena </td><td class="col1"> Você carrega cenas da mesma forma que você carrega modelos: <pre class="code java">Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/town/main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>
<pre class="code java">Spatial scene <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/town/main.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
rootNode.<span class="me1">attachChild</span><span class="br0">(</span>scene<span class="br0">)</span><span class="sy0">;</span></pre>
</td>
	</tr>
</table></div>
<!-- EDIT11 TABLE [12535-13662] -->
</div>
<!-- EDIT10 SECTION "Carregando Modelos e a Cena" [12496-13663] -->
<h2 class="sectionedit12" id="exercicio_-_como_carregar_ativos">Exercício - Como Carregar Ativos</h2>
<div class="level2">

<p>
Como um exercício, vamos tentar diferentes maneiras de carregar uma cena. Você aprenderá a como carregar a cena diretamente, ou de um arquivo zip.
</p>
<ol>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" class="urlextern" title="http://jmonkeyengine.googlecode.com/svn/trunk/engine/town.zip" rel="nofollow">baixe a cena de amostra town.zip</a>. </div>
</li>
<li class="level1"><div class="li"> (Opcional:) Dezipe o arquivo town.zip para ver a estrutura da Ogre dotScene contida: Você terá um diretório chamado <code>town</code>. Ele contém arquivos XML e textura, e o arquivo chamado main.scene. (Isto é apenas para sua informação, você não precisa fazer nada com ele.)</div>
</li>
<li class="level1"><div class="li"> Coloque o arquivo town.zip no diretório topo de nível de seu projeto JME3, assim:<pre class="code">jMonkeyProjects/MyGameProject/assets/
jMonkeyProjects/MyGameProject/build.xml
jMonkeyProjects/MyGameProject/src/
jMonkeyProjects/MyGameProject/town.zip
...</pre>
</div>
</li>
</ol>

<p>
Use o seguinte método para carregar modelos de um arquivo zip:
</p>
<ol>
<li class="level1"><div class="li"> Verifique se <code>town.zip</code> está no diretório do projeto.</div>
</li>
<li class="level1"><div class="li"> Registre um localizador de arquivo zip para o diretório do projeto: Adicione o seguinte código sobre <code>simpleInitApp(){</code><pre class="code java">    assetManager.<span class="me1">registerLocator</span><span class="br0">(</span><span class="st0">"town.zip"</span>, ZipLocator.<span class="kw1">class</span><span class="br0">)</span><span class="sy0">;</span>
    Spatial gameLevel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>5.2f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>gameLevel<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
O método loadModel() agora pesquisa pelo arquivo zip diretamente para carregar os arquivos (isto significa, não escreva <code>loadModel(town.zip/main.scene)</code> ou similar!) 
</p>
</div>
</li>
<li class="level1"><div class="li"> Limpe, construa e execute o projeto. <br />
Você deveria agora ver o Ninja+parede+bule permanecendo em uma cidade.</div>
</li>
</ol>

<p>
<strong>Dica:</strong>  se você registrar novos localizadores, tenha certeza de que você não tenha quaisquer conflitos de nome: Não nomeie todas as cenas <code>main.scene</code> mas dê a cada cena um nome único.
</p>

<p>
Anteriormente neste tutorial, você carregou cenas e modelos do diretório de ativo. Isto é a maneira mais comum que você estará carregando cenas e modelos. Aqui está o procedimento típico:
</p>
<ol>
<li class="level1"><div class="li"> Remova o código que você adicionou para o exercício anterior.</div>
</li>
<li class="level1"><div class="li"> Mova o diretório dezipado <code>town/</code> no diretório <code>assets/Scenes/</code> de seu projeto.</div>
</li>
<li class="level1"><div class="li"> Adicione o seguinte código sobre <code>simpleInitApp() {</code> <pre class="code java">    Spatial gameLevel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/town/main.scene"</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>5.2f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>gameLevel<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Note que o caminho é relativo ao diretório <code>assets/…</code>.
</p>
</div>
</li>
<li class="level1"><div class="li"> Limpe, construa e execute o projeto. De novo, você deveria ver o Ninja+parede+bule em uma cidade.</div>
</li>
</ol>

<p>
Aqui está um terceiro método que você deve conhecer, carregando uma cena/modelo de um arquivo .j3o:
</p>
<ol>
<li class="level1"><div class="li"> Remova o código do exercício anterior.</div>
</li>
<li class="level1"><div class="li"> Se você j´pa não fez, abra o <a href="/sdk.html" class="wikilink1" title="sdk">SDK</a> e abra o projeto que contém a classe HelloAsset..</div>
</li>
<li class="level1"><div class="li"> Na janela de projetos, navegue para o diretório <code>assets/Scenes/town</code>. </div>
</li>
<li class="level1"><div class="li"> Dê um clique com o botão direito em <code>main.scene</code> e converta a cena para binário: A jMonkeyPlatform gera um arquivo main.j3o.</div>
</li>
<li class="level1"><div class="li"> Adicione o seguinte código em <code>simpleInitApp() {</code><pre class="code java">    Spatial gameLevel <span class="sy0">=</span> assetManager.<span class="me1">loadModel</span><span class="br0">(</span><span class="st0">"Scenes/town/main.j3o"</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="nu0">0</span>, <span class="sy0">-</span>5.2f, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
    gameLevel.<span class="me1">setLocalScale</span><span class="br0">(</span><span class="nu0">2</span><span class="br0">)</span><span class="sy0">;</span>
    rootNode.<span class="me1">attachChild</span><span class="br0">(</span>gameLevel<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
 Novamente, note que o caminho é relativo ao diretório <code>assets/…</code> directory.
</p>
</div>
</li>
<li class="level1"><div class="li"> Limpe, construa e execute o projeto. <br />
De novo, você deveria ver o Ninja+parede+bule em uma cidade.</div>
</li>
</ol>

</div>
<!-- EDIT12 SECTION "Exercício - Como Carregar Ativos" [13664-17202] -->
<h2 class="sectionedit13" id="conclusao">Conclusão</h2>
<div class="level2">

<p>
Agora você sabe como popular o grafo de cena com modelos e formas estáticas, e como construir cenas. Você aprendeu como carregar ativos usando o <code>gerenciador de ativos (assetManager)</code> e você viu que os caminhos iniciam relativos ao seu diretório de projeto. Uma outra coisa importante que você aprendeu é converter modelos para o formato .j3o para os JARs executáveis etc.
</p>

<p>
Vamos adicionar alguma ação para a cena e continuar com o  <a href="/doku.php/jme3:beginner:hello_main_event_loop-pt" class="wikilink2" title="jme3:beginner:hello_main_event_loop-pt" rel="nofollow"> Loop de Atualização pt</a>!
</p>
<hr />

<p>
<strong>See also:</strong>
</p>
<ul>
<li class="level1"><div class="li"> <a href="/jme3/external/blender.html" class="wikilink1" title="jme3:external:blender">O tutorial de importação Blender definitivo</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.jmonkeyengine.com/forum/index.php?topic=14418.0" class="urlextern" title="http://www.jmonkeyengine.com/forum/index.php?topic=14418.0" rel="nofollow">Instantâneos de um grande modelo carregado</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://www.youtube.com/user/aramakara" class="urlextern" title="http://www.youtube.com/user/aramakara" rel="nofollow">Video tutoriais for obter OgreXML do 3DS Max usando OgreMax</a></div>
</li>
<li class="level1"><div class="li"> Se você quer aprender a como carregar sons, veja <a href="/doku.php/jme3:beginner:hello_audio_pt" class="wikilink2" title="jme3:beginner:hello_audio_pt" rel="nofollow">Hello Audio pt</a></div>
</li>
<li class="level1"><div class="li"> Se você quer aprender mais sobre carregar materiais, veja <a href="/doku.php/jme3:beginner:hello_material_pt" class="wikilink2" title="jme3:beginner:hello_material_pt" rel="nofollow">Hello Material pt</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/lightnode.html" class="wikilink1" title="tag:lightnode" rel="tag">lightnode</a>,
	<a href="/tag/material.html" class="wikilink1" title="tag:material" rel="tag">material</a>,
	<a href="/tag/model.html" class="wikilink1" title="tag:model" rel="tag">model</a>,
	<a href="/tag/node.html" class="wikilink1" title="tag:node" rel="tag">node</a>,
	<a href="/tag/gui.html" class="wikilink1" title="tag:gui" rel="tag">gui</a>,
	<a href="/tag/hud.html" class="wikilink1" title="tag:hud" rel="tag">hud</a>,
	<a href="/tag/texture.html" class="wikilink1" title="tag:texture" rel="tag">texture</a>
</span></div>

</div>
<!-- EDIT13 SECTION "Conclusão" [17203-] -->
