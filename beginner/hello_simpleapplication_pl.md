---
title: JME 3 Tutorial (1) - Tworzymy SimpleApplication
---
<h1 class="sectionedit1" id="jme_3_tutorial_1_-_tworzymy_simpleapplication">JME 3 Tutorial (1) - Tworzymy SimpleApplication</h1>
<div class="level1">

<p>
Poprzednie: <a href="/jme3.html" class="wikilink1" title="jme3">Instalacja JME3</a>,
Następne: <a href="/jme3/beginner/hello_node_pl.html" class="wikilink1" title="jme3:beginner:hello_node_pl">Hello Node</a> <br />
<br />

W tym tutorialu zakładamy, że już <a href="/jme3.html" class="wikilink1" title="jme3">pobrałeś oraz odpowiednio ustawiłeś jMonkeyEngine3</a> w swoim środowisku programistycznym. <br />
<br />

Tak więc jesteś gotowy na stworzenie pierwszej w gry w jMonkeyEngine3 ! Możesz korzystać z tych wprowadzających tutoriali pracując w praktycznie dowolnym środowisku programistycznym (IDE), takim jak jMonkeyEngine SDK, NetBeans, Eclipse, lub po prostu uruchamiać wszystko z wiersza poleceń. <br />
<br />

</p>

</div>
<!-- EDIT1 SECTION "JME 3 Tutorial (1) - Tworzymy SimpleApplication" [1-652] -->
<h2 class="sectionedit2" id="czas_na_simpleapplication">Czas na SimpleApplication</h2>
<div class="level2">

<p>
Stwórzmy pakiet <code>jme3test.helloworld</code> oraz plik <code>HelloJME3.java</code>. <br />
<br />

W środowisku NetBeans, klikamy prawym przyciskiem myszy na Source Packages :
</p>
<ul>
<li class="level1"><div class="li"> Wybieramy <code>New… &gt; Java Class</code> aby stworzyć nowy plik.</div>
</li>
<li class="level1"><div class="li"> Wprowadzamy nazwę klasy: <code>HelloJME3</code></div>
</li>
<li class="level1"><div class="li"> Wprowadzamy wartość dla package: <code>jme3test.helloworld</code></div>
</li>
<li class="level1"><div class="li"> Klikamy Finish.</div>
</li>
</ul>

</div>
<!-- EDIT2 SECTION "Czas na SimpleApplication" [653-1035] -->
<h3 class="sectionedit3" id="przykladowy_kod_zrodlowy">Przykładowy kod źródłowy</h3>
<div class="level3">

<p>
Jak widzimy stworzony został plik HelloJME3.java. Skopiuj poniższy kod do niego:
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">jme3test.helloworld</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.app.SimpleApplication</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.material.Material</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.Vector3f</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.Geometry</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.scene.shape.Box</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">com.jme3.math.ColorRGBA</span><span class="sy0">;</span>
<span class="co3">/** Przykład 1 - zaczynamy prace z najprostsza aplikacja.
 * Wyswietlamy trojwymiarowy szescian i spogladamy na niego z wszystkich stron
 * poprzez ruch mysza lub klawisze WSAD. */</span>
<span class="kw1">public</span> <span class="kw1">class</span> HelloJME3 <span class="kw1">extends</span> SimpleApplication <span class="br0">{</span>
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span><span class="br0">{</span>
        HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
    @Override
    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Zbuduj i uruchom klasę HelloJME3. Jeżeli ukaże się jakiekolwiek okno dialogowe, potwierdź domyślne ustawienia.
</p>
<ol>
<li class="level1"><div class="li"> Zobaczysz okno, w którym wyświetlany jest sześcian.</div>
</li>
<li class="level1"><div class="li"> Możesz nawigować w oknie za pomocą klawiszy WASD oraz myszy.</div>
</li>
<li class="level1"><div class="li"> Naciśnij klawisz Escape, aby wyłączyć aplikację.</div>
</li>
</ol>

<p>
Gratulacje, coś w końcu działa. Jak jednak to zrobiłeś?
</p>

</div>
<!-- EDIT3 SECTION "Przykładowy kod źródłowy" [1036-2470] -->
<h2 class="sectionedit4" id="jak_to_wszystko_zrozumiec">Jak to wszystko zrozumieć?</h2>
<div class="level2">

<p>
Poniżej przedstawione są podstawowe zasady, którymi “rządzą się” gry wykonane w JME3:
</p>

</div>
<!-- EDIT4 SECTION "Jak to wszystko zrozumieć?" [2471-2602] -->
<h3 class="sectionedit5" id="start_gry">Start gry</h3>
<div class="level3">

<p>
Zauważ, że klasa HelloJME3.java class rozszerza <code>com.jme3.app.SimpleApplication</code>, która z kolei jest podklasą <code>com.jme3.app.Application</code>. Każda gra wykonana w JME3 jest egzemplarzem <code>com.jme3.app.Application</code> (pośrednio lub bezpośrednio). <br />
<br />

Aby uruchomić grę, musisz na początku stworzyć egzemplarz odpowiedniej klasy, następnie wywołać jego metodę <code>start()</code>:
</p>
<pre class="code java">HelloJME3 app <span class="sy0">=</span> <span class="kw1">new</span> HelloJME3<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
app.<span class="me1">start</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<strong>Porada:</strong> Jeżeli jesteś zaawansowanym programistą języka Java możesz stworzyć kopię <code>SimpleApplication</code>  i używać jej jako szablonu dla własnych klas.
</p>

</div>
<!-- EDIT5 SECTION "Start gry" [2603-3240] -->
<h3 class="sectionedit6" id="inicjalizacja_sceny">Inicjalizacja sceny</h3>
<div class="level3">

<p>
Ta prosta “gra” składa się tylko z sześcianu. Poniżej zaprezentowany jest kod, który odpowiada za jego stworzenie, wypozycjonowanie, nadanie koloru oraz samo podpięcie do sceny. (Tymi wszystkimi szczegółami zajmiemy się nieco później.)
</p>
<pre class="code java">    <span class="kw1">public</span> <span class="kw4">void</span> simpleInitApp<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a> b <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+box"><span class="kw3">Box</span></a><span class="br0">(</span>Vector3f.<span class="me1">ZERO</span>, <span class="nu0">1</span>, <span class="nu0">1</span>, <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// tworzy ksztalt szescianu</span>
        Geometry geom <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Box"</span>, b<span class="br0">)</span><span class="sy0">;</span>  <span class="co1">// tworzy geometrie szescianu z ksztaltu</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager,
         <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// tworzy material</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"Color"</span>, ColorRGBA.<span class="me1">Blue</span><span class="br0">)</span><span class="sy0">;</span> <span class="co1">// ustawia kolor materialu</span>
        geom.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>                   <span class="co1">// przypisuje material do szescianu</span>
        rootNode.<span class="me1">attachChild</span><span class="br0">(</span>geom<span class="br0">)</span><span class="sy0">;</span>              <span class="co1">// podpina szescian do sceny</span>
    <span class="br0">}</span></pre>

<p>
Metoda <code>simpleInitApp()</code> jest automatycznie wywoływana raz, kiedy uruchamiana jest gra. W tej metodzie tworzysz lub wczytujesz obiekty zanim zacznie się gra! Tak wygląda standardowy proces:
</p>
<ol>
<li class="level1"><div class="li"> Przygotowanie obiektów gry:</div>
<ul>
<li class="level2"><div class="li"> Stwórz lub wczytaj wszystkie obiekty i rozmieść je odpowiednio.</div>
</li>
<li class="level2"><div class="li"> Aby geometria (jak przykładowo pudełko) ukazała się na scenie, podepnij ją do <code>rootNode</code>.</div>
</li>
<li class="level2"><div class="li"> Przykłady: Wczytaj gracza, teren, niebo, wrogów, przeszkodzy i umieść je w odpowiednich miejsach.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Przygotowanie zmiennych gry:</div>
<ul>
<li class="level2"><div class="li"> Zmienne w grze “śledzą” stan gry. Należy ustawić poprawne wartości początkowe.</div>
</li>
<li class="level2"><div class="li"> Przykłady: Ustaw <code>wynik</code> na 0, a <code>zdrowie</code> na 100% i tak dalej.</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Przygotowanie nawigacji:</div>
<ul>
<li class="level2"><div class="li"> Poniższe klawisze są ustawione domyślnie:</div>
<ul>
<li class="level3"><div class="li"> W,A,S,D – Poruszanie się</div>
</li>
<li class="level3"><div class="li"> Mysz i strzałki – Zmiana pozycji kamery</div>
</li>
<li class="level3"><div class="li"> Escape - Opuszczanie aplikacji</div>
</li>
</ul>
</li>
</ul>
</li>
</ol>

<p>
W JME3 kluczowym obiektem jest <code>rootNode</code>. Wszystko co jest podpięte do rootNode pojawia się na scenie. Innymi słowy: Obiekt który został stworzony, ale nie jest podpięty do rootNode, pozostaje niewidoczny.
</p>

</div>
<!-- EDIT6 SECTION "Inicjalizacja sceny" [3241-5226] -->
<h2 class="sectionedit7" id="podumowanie">Podumowanie</h2>
<div class="level2">

<p>
Te kilka linijek kodu, nie  nothing but display a static object in 3-D, but they already allow you to navigate around in 3D. Dowiedziałeś się również, że SimpleApplication jest naprawdę dobrym miejscem na start ponieważ masz już:
</p>
<ul>
<li class="level1"><div class="li"> metodę <code>simpleInitApp()</code> służąca inicjalizacji obiektów gry</div>
</li>
<li class="level1"><div class="li"> <code>rootNode</code> where you attach geometries to make them appear in the scene</div>
</li>
<li class="level1"><div class="li"> domyślne ustawienia nawigacyjne</div>
</li>
</ul>

<p>
W prawdziwej grze, musisz:
</p>
<ol>
<li class="level1"><div class="li"> Initialize the game world,</div>
</li>
<li class="level1"><div class="li"> Trigger actions in the event loop,</div>
</li>
<li class="level1"><div class="li"> Respond to user input.</div>
</li>
</ol>

<p>
W kolejnych tutorialach dowiesz się, jak te zadania mogą zostać wykonane w jMonkeyEngine! <br />
<br />

Przejdź do lekcji  <a href="/jme3/beginner/hello_node_pl.html" class="wikilink1" title="jme3:beginner:hello_node_pl">Hello Node</a> , gdzie na początku pokażemy Ci więcej szczegółów how to initialize the game world, also known as the scene graph.
</p>
<hr />

<p>
Zobacz również: <a href="/doku.php/jme3:simpleapplication_z_wiersza_polecen" class="wikilink2" title="jme3:simpleapplication_z_wiersza_polecen" rel="nofollow">SimpleApplication z wiersza poleceń</a>
</p>
<div class="tags"><span>
	<a href="/tag/beginner.html" class="wikilink1" title="tag:beginner" rel="tag">beginner</a>,
	<a href="/tag/intro.html" class="wikilink1" title="tag:intro" rel="tag">intro</a>,
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/init.html" class="wikilink1" title="tag:init" rel="tag">init</a>,
	<a href="/tag/polish.html" class="wikilink1" title="tag:polish" rel="tag">Polish</a>
</span></div>

</div>
<!-- EDIT7 SECTION "Podumowanie" [5227-] -->
