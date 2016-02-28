---
title: JME 3 Tutorial - Visualizing 3D Charts
---
<h1 class="sectionedit1" id="jme_3_tutorial_-_visualizing_3d_charts">JME 3 Tutorial - Visualizing 3D Charts</h1>
<div class="level1">

<p>
Previous: <a href="/jme3/tools/navigation.html" class="wikilink1" title="jme3:tools:navigation">Navigation</a>
</p>

<p>
In this tutorial we will have a look at creating a simple 3D cartography application that allows you to display 3D charts at different zoom levels.
</p>

<p>
This tutorial assumes that you know:
</p>
<ul>
<li class="level1"><div class="li"> About the <a href="/jme3/tools/navigation.html" class="wikilink1" title="jme3:tools:navigation">Navigation package</a>.</div>
</li>
<li class="level1"><div class="li"> How to create a <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">3D landscape</a> using image-based heightmaps.</div>
</li>
</ul>

<p>
<a href="/resources/jme3-tools-mercator_grid_3d_small.png" class="media" title="jme3:tools:mercator_grid_3d_small.png"><img src="/resources/jme3-tools-mercator_grid_3d_small.png" class="media" alt="" /></a>
</p>

<p>
You will learn that how to account for distortions that arise when mapping of one coordinate system into (i.e. when converting longitude/latitude into JME's World Units), how to construct a tile tree and how to render a dynamic mercator grid.
</p>

<p>
<strong>This article was sponsored by <a href="http://planetmayo.com/" class="urlextern" title="http://planetmayo.com/" rel="nofollow">PlanetMayo Ltd</a></strong>
</p>

</div>
<!-- EDIT1 SECTION "JME 3 Tutorial - Visualizing 3D Charts" [1-813] -->
<h2 class="sectionedit2" id="displaying_your_first_chart">Displaying your first chart</h2>
<div class="level2">

<p>
Let's think about how we are going to get JME to display our terrain. The easiest way is to use JME's<code>ImageBasedHeightMap</code>. Recall from the <a href="/jme3/beginner/hello_terrain.html" class="wikilink1" title="jme3:beginner:hello_terrain">Hello Terrain</a> tutorial that these are grayscale images which JME uses to create a terrain quad. So, in order to display a chart, we need an image of a (two-dimensional) mercator projection (such as the one depicted below), which we then load using:
</p>
<pre class="code java">Texture heightMapImage <span class="sy0">=</span> assetManager.<span class="me1">loadTexture</span><span class="br0">(</span>DEFAULT_HEIGHTMAP<span class="br0">)</span><span class="sy0">;</span>
heightmap <span class="sy0">=</span> <span class="kw1">new</span> ImageBasedHeightMap<span class="br0">(</span>heightMapImage.<span class="me1">getImage</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
heightmap.<span class="me1">load</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
terrain <span class="sy0">=</span> <span class="kw1">new</span> TerrainQuad<span class="br0">(</span><span class="st0">"terrain"</span>, <span class="nu0">257</span>, TERRAIN_SIZE, heightmap.<span class="me1">getHeightMap</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
applyDefaultTexture<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span></pre>

<p>
<a href="/resources/jme3-tools-globe.png" class="media" title="jme3:tools:globe.png"><img src="/resources/jme3-tools-globe.png" class="media" title="A 256x256 mercator projection of planet earth." alt="A 256x256 mercator projection of planet earth." /></a>
</p>

<p>
In essence, 3D chart visualization is achieved by converting the polygons composing planet earth's landmass into float matrices whereby each value within the matrix represents a specific terrain height. For example, given a terrain of 100 x 100 world units, we construct a heightmap by creating a 100 x 100 matrix. Each cell within the matrix corresponds to a terrain coordinate; each cell’s value to that coordinate’s desired height. But you already knew that, so where's the tricky part? Well, when visualizing a chart an accurate projection requires a translation of latitude/longitude coordinates into their equivalent world unit (x,y,z) counterparts. This translation however is not a straight forward mapping of one coordinate system into the other due to the distortion arising from projecting an oblate spheroid onto a flat surface (see my previous wiki article <a href="/jme3/tools/navigation.html" class="wikilink1" title="jme3:tools:navigation">here</a>). This means that if one would adhere to a linear scale, the Mercator projection would distort the size and shape of objects as the object distances itself from the equator, eventually resulting in infinite scaling as the pole is reached. So the first task at hand, is to construct accurate 2D projections of planet earth which we can then use as heightmaps. We can achieve this using the jme3.tools.navigation package and co-ordinate sets available at <a href="http://www.ngdc.noaa.gov/mgg/coast/" class="urlextern" title="http://www.ngdc.noaa.gov/mgg/coast/" rel="nofollow">noaa.gov</a>. 
</p>

<p>
As <a href="/jme3/tools/navigation.html" class="wikilink1" title="jme3:tools:navigation">previously discussed</a>, the distortion in latitude is derived by using the difference in meridional parts between the chart’s centre and the current position as a baseline; through converting the difference to world units by dividing it by the number of world units contained within one minute, a latitude’s y-coordinate can be obtained. Calculating a position’s x-coordinate is somewhat easier as the distortion only applies to latitude, not longitude. Therefore x merely equals the sum or difference between itself and the viewport’s centre coordinate, depending on the relative location of the position itself and the chart’s centre. Despite being able to convert between the two coordinate systems, slight precision problems remain once the chart projection is scaled down past a level of 6 meters. This is caused by the pixel referencing system of modern displays being integer based; once the ratio of minutes to pixels exceeds the aforementioned threshold, slight inaccuracies are introduced into the display. However this is of little relevance to most GIS (such as Debrief) as a) the inaccuracies are a matter of meters (or even centimetres) and b) it is impossible to notice this variation as GPS exposes a much higher inaccuracy (between 10 - 100 meters).
</p>

<p>
</p><p></p><div class="notetip">To lessen the computational load, coordinate system conversion should only takes place when either the chart is re-centered or a change in scale / resolution is requested. Once converted, the coordinate sets are rendered to a buffer whose contents is then drawn for every UI update cycle.
</div>.


</div>
<!-- EDIT2 SECTION "Displaying your first chart" [814-4656] -->
<h2 class="sectionedit3" id="creating_your_heightmaps">Creating your heightmaps</h2>
<div class="level2">

<p>
There are two ways to create your heightmaps (also referred to as 'tiles' as each heightmap is a tile that composes our chart of the world). One is to use third-party software such as <a href="http://geotools.org/" class="urlextern" title="http://geotools.org/" rel="nofollow">GeoTools</a>. The other is to use the jme3.tools.navigation package to write a tile generator:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> TileGenerator <span class="br0">{</span>
    <span class="kw1">private</span> <span class="kw4">int</span> lineCount<span class="sy0">;</span>
 
    <span class="coMULTI">/* List of polygons representing the countries that are to be drawn. */</span>
    <span class="kw1">private</span> List<span class="sy0">&lt;</span>PositionContainer<span class="sy0">&gt;</span> polygons<span class="sy0">;</span>
 
    <span class="coMULTI">/* The map projection used to generate the chart image. */</span>
    <span class="kw1">private</span> MapModel2D map<span class="sy0">;</span>
 
    <span class="coMULTI">/* The chart's resolution in minutes of longitude per pixel. */</span>
    <span class="kw1">private</span> <span class="kw4">double</span> mpp<span class="sy0">;</span>
 
    <span class="coMULTI">/* The chart's centre. */</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> centre<span class="sy0">;</span>
 
    <span class="co3">/**
     * Constructs a new instance of TileGenerator.
     *
     * @param worldSize         The width of the chart for which tiles are to be
     *                          generated.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> TileGenerator<span class="br0">(</span><span class="kw4">int</span> worldSize, <span class="kw4">double</span> mpp, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> centre<span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> dataDirectory <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a><span class="br0">(</span><span class="st0">"data"</span><span class="br0">)</span><span class="sy0">;</span>
        map <span class="sy0">=</span> <span class="kw1">new</span> MapModel2D<span class="br0">(</span>worldSize<span class="br0">)</span><span class="sy0">;</span>
        lineCount <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a><span class="br0">[</span><span class="br0">]</span> files <span class="sy0">=</span> dataDirectory.<span class="me1">listFiles</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+filefilter"><span class="kw3">FileFilter</span></a><span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
 
            <span class="kw1">public</span> <span class="kw4">boolean</span> accept<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> pathname<span class="br0">)</span> <span class="br0">{</span>
                <span class="kw1">if</span> <span class="br0">(</span>pathname.<span class="me1">toString</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">endsWith</span><span class="br0">(</span><span class="st0">".out"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                    <span class="kw1">return</span> <span class="kw2">true</span><span class="sy0">;</span>
                <span class="br0">}</span>
                <span class="kw1">return</span> <span class="kw2">false</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span><span class="br0">)</span><span class="sy0">;</span>
        loadChartData<span class="br0">(</span>files<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">mpp</span> <span class="sy0">=</span> mpp<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">centre</span> <span class="sy0">=</span> centre<span class="sy0">;</span>
    <span class="br0">}</span>
    <span class="kw1">public</span> <span class="kw4">void</span> createImageMap<span class="br0">(</span><span class="kw4">int</span> worldSize<span class="br0">)</span> <span class="br0">{</span>
        map.<span class="me1">setCentre</span><span class="br0">(</span>centre<span class="br0">)</span><span class="sy0">;</span>
        map.<span class="me1">calculateMinutesPerPixel</span><span class="br0">(</span>mpp<span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Generating chart with world width (in pixels): "</span> <span class="sy0">+</span> worldSize<span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Generating chart with meters per pixel: "</span> <span class="sy0">+</span> map.<span class="me1">getMetersPerPixel</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+bufferedimage"><span class="kw3">BufferedImage</span></a> img <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+bufferedimage"><span class="kw3">BufferedImage</span></a><span class="br0">(</span>worldSize,
                worldSize, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+bufferedimage"><span class="kw3">BufferedImage</span></a>.<span class="me1">TYPE_BYTE_GRAY</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+graphics2d"><span class="kw3">Graphics2D</span></a> g <span class="sy0">=</span> img.<span class="me1">createGraphics</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+point"><span class="kw3">Point</span></a> point1, point2<span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+generalpath"><span class="kw3">GeneralPath</span></a> polygonPath<span class="sy0">;</span>
        g.<span class="me1">setColor</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>.<span class="me1">WHITE</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw4">int</span> containerSize<span class="sy0">;</span>
 
        <span class="kw1">for</span> <span class="br0">(</span>PositionContainer container <span class="sy0">:</span> polygons<span class="br0">)</span> <span class="br0">{</span>
            polygonPath <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+generalpath"><span class="kw3">GeneralPath</span></a><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            containerSize <span class="sy0">=</span> container.<span class="me1">getPositions</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">1</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> containerSize<span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
                point1 <span class="sy0">=</span> map.<span class="me1">toPixel</span><span class="br0">(</span>container.<span class="me1">getPositions</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">get</span><span class="br0">(</span>i<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                point2 <span class="sy0">=</span> map.<span class="me1">toPixel</span><span class="br0">(</span>container.<span class="me1">getPositions</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">get</span><span class="br0">(</span>i <span class="sy0">-</span> <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                polygonPath.<span class="me1">moveTo</span><span class="br0">(</span><span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point1.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span>, <span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point1.<span class="me1">getY</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                polygonPath.<span class="me1">lineTo</span><span class="br0">(</span><span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point1.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span>, <span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point1.<span class="me1">getY</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                polygonPath.<span class="me1">lineTo</span><span class="br0">(</span><span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point2.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span>, <span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point2.<span class="me1">getY</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
            g.<span class="me1">draw</span><span class="br0">(</span>polygonPath<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
 
        <span class="co1">// Write resulting image to file</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            ImageIO.<span class="me1">write</span><span class="br0">(</span>img, <span class="st0">"png"</span>, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a><span class="br0">(</span><span class="st0">"map.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> ioe<span class="br0">)</span> <span class="br0">{</span>
            ioe.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
 
    <span class="co3">/**
     * Draws depth contours.
     * 
     * @param img           The image to draw to.
     * @param worldSize     The size of the chart.
     * @since 1.0
     */</span>
    <span class="kw1">private</span> <span class="kw4">void</span> drawContours<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+bufferedimage"><span class="kw3">BufferedImage</span></a> img, <span class="kw4">int</span> worldSize<span class="br0">)</span> <span class="br0">{</span>
        map.<span class="me1">setCentre</span><span class="br0">(</span>centre<span class="br0">)</span><span class="sy0">;</span>
        map.<span class="me1">calculateMinutesPerPixel</span><span class="br0">(</span>mpp<span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+bufferedimage"><span class="kw3">BufferedImage</span></a> img2 <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+bufferedimage"><span class="kw3">BufferedImage</span></a><span class="br0">(</span>worldSize,
                worldSize, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+bufferedimage"><span class="kw3">BufferedImage</span></a>.<span class="me1">TYPE_BYTE_GRAY</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+graphics2d"><span class="kw3">Graphics2D</span></a> g <span class="sy0">=</span> img2.<span class="me1">createGraphics</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        g.<span class="me1">drawImage</span><span class="br0">(</span>img, <span class="kw2">null</span>, <span class="kw2">null</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+point"><span class="kw3">Point</span></a> point1, point2<span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+generalpath"><span class="kw3">GeneralPath</span></a> polygonPath<span class="sy0">;</span>
<span class="co1">//        g.setColor(new Color(21, 21, 21));</span>
        g.<span class="me1">setColor</span><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+color"><span class="kw3">Color</span></a>.<span class="me1">WHITE</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw4">int</span> containerSize<span class="sy0">;</span>
 
        <span class="kw1">for</span> <span class="br0">(</span>PositionContainer container <span class="sy0">:</span> polygons<span class="br0">)</span> <span class="br0">{</span>
            polygonPath <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+generalpath"><span class="kw3">GeneralPath</span></a><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            containerSize <span class="sy0">=</span> container.<span class="me1">getPositions</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">size</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">1</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> containerSize<span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
                point1 <span class="sy0">=</span> map.<span class="me1">toPixel</span><span class="br0">(</span>container.<span class="me1">getPositions</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">get</span><span class="br0">(</span>i<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                point2 <span class="sy0">=</span> map.<span class="me1">toPixel</span><span class="br0">(</span>container.<span class="me1">getPositions</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">get</span><span class="br0">(</span>i <span class="sy0">-</span> <span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                polygonPath.<span class="me1">moveTo</span><span class="br0">(</span><span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point1.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span>, <span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point1.<span class="me1">getY</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                polygonPath.<span class="me1">lineTo</span><span class="br0">(</span><span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point1.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span>, <span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point1.<span class="me1">getY</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                polygonPath.<span class="me1">lineTo</span><span class="br0">(</span><span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point2.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span>, <span class="br0">(</span><span class="kw4">double</span><span class="br0">)</span> point2.<span class="me1">getY</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
            g.<span class="me1">draw</span><span class="br0">(</span>polygonPath<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
 
        <span class="co1">// Write resulting image to file</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            ImageIO.<span class="me1">write</span><span class="br0">(</span>img2, <span class="st0">"png"</span>, <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a><span class="br0">(</span><span class="st0">"map.png"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+ioexception"><span class="kw3">IOException</span></a> ioe<span class="br0">)</span> <span class="br0">{</span>
            ioe.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Loads country border information from .out files, parses the information
     * and stores it as a PositionContainer which is later used to
     * produce the .png chart image.
     *
     * @param files             A List of files that contain
     *                          country border data.
     * @since 1.0
     */</span>
    <span class="kw1">private</span> <span class="kw4">void</span> loadChartData<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a><span class="br0">[</span><span class="br0">]</span> files<span class="br0">)</span> <span class="br0">{</span>
        Scanner scan<span class="sy0">;</span>
        PositionContainer countryBorderPosition<span class="sy0">;</span>
        polygons <span class="sy0">=</span> <span class="kw1">new</span> ArrayList<span class="sy0">&lt;</span>PositionContainer<span class="sy0">&gt;</span><span class="br0">(</span><span class="nu0">300</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> tmp <span class="sy0">=</span> <span class="st0">""</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> tmpLat<span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> tmpLong<span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+stringtokenizer"><span class="kw3">StringTokenizer</span></a> stk<span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> pos<span class="sy0">;</span>
        <span class="kw1">for</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> file <span class="sy0">:</span> files<span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">try</span> <span class="br0">{</span>
                scan <span class="sy0">=</span> <span class="kw1">new</span> Scanner<span class="br0">(</span>file<span class="br0">)</span><span class="sy0">;</span>
                countryBorderPosition <span class="sy0">=</span> <span class="kw1">new</span> PositionContainer<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="kw1">while</span> <span class="br0">(</span>scan.<span class="me1">hasNext</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                    tmp <span class="sy0">=</span> scan.<span class="me1">nextLine</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="kw1">if</span> <span class="br0">(</span>tmp.<span class="me1">startsWith</span><span class="br0">(</span><span class="st0">"{"</span><span class="br0">)</span> <span class="sy0">||</span> tmp.<span class="me1">startsWith</span><span class="br0">(</span><span class="st0">"$"</span><span class="br0">)</span> <span class="sy0">||</span> tmp.<span class="me1">startsWith</span><span class="br0">(</span><span class="st0">";"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                        <span class="kw1">continue</span><span class="sy0">;</span>
                    <span class="br0">}</span>
                    <span class="kw1">if</span> <span class="br0">(</span>tmp.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"-1"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                        polygons.<span class="me1">add</span><span class="br0">(</span>countryBorderPosition<span class="br0">)</span><span class="sy0">;</span>
                        countryBorderPosition <span class="sy0">=</span> <span class="kw1">new</span> PositionContainer<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                        <span class="kw1">continue</span><span class="sy0">;</span>
                    <span class="br0">}</span>
                    stk <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+stringtokenizer"><span class="kw3">StringTokenizer</span></a><span class="br0">(</span>tmp, <span class="st0">" +"</span><span class="br0">)</span><span class="sy0">;</span>
                    <span class="kw1">while</span> <span class="br0">(</span>stk.<span class="me1">hasMoreTokens</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                        tmpLat <span class="sy0">=</span> stk.<span class="me1">nextToken</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">trim</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                        <span class="kw1">if</span> <span class="br0">(</span>tmpLat.<span class="me1">equals</span><span class="br0">(</span><span class="st0">"-1"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                            polygons.<span class="me1">add</span><span class="br0">(</span>countryBorderPosition<span class="br0">)</span><span class="sy0">;</span>
                            countryBorderPosition <span class="sy0">=</span> <span class="kw1">new</span> PositionContainer<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                            <span class="kw1">continue</span><span class="sy0">;</span>
                        <span class="br0">}</span>
                        tmpLong <span class="sy0">=</span> stk.<span class="me1">nextToken</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">trim</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                        pos <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+double"><span class="kw3">Double</span></a>.<span class="me1">parseDouble</span><span class="br0">(</span>tmpLat<span class="br0">)</span>, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+double"><span class="kw3">Double</span></a>.<span class="me1">parseDouble</span><span class="br0">(</span>tmpLong<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                        countryBorderPosition.<span class="me1">add</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
                        lineCount<span class="sy0">++;</span>
                    <span class="br0">}</span>
                <span class="br0">}</span>
            <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
                e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span>tmp<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
    <span class="br0">}</span>
 
    <span class="kw1">public</span> <span class="kw1">static</span> <span class="kw4">void</span> main<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> args<span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Debug 3D Tile Generator"</span><span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"==========================="</span><span class="br0">)</span><span class="sy0">;</span>
        args <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="nu0">3</span><span class="br0">]</span><span class="sy0">;</span>
        args<span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span> <span class="sy0">=</span> <span class="st0">"1.2"</span><span class="sy0">;</span>
        args<span class="br0">[</span><span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> <span class="st0">"51.8"</span><span class="sy0">;</span>
        args<span class="br0">[</span><span class="nu0">2</span><span class="br0">]</span> <span class="sy0">=</span> <span class="st0">"-8.3"</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>args.<span class="me1">length</span> <span class="sy0">&lt;</span> <span class="nu0">3</span> <span class="sy0">||</span> args.<span class="me1">length</span> <span class="sy0">&gt;</span> <span class="nu0">3</span><span class="br0">)</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Incorrect argument usage. Should be mpp latitude longitude"</span><span class="br0">)</span><span class="sy0">;</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Exiting"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> mppStr <span class="sy0">=</span> args<span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> latitudeStr <span class="sy0">=</span> args<span class="br0">[</span><span class="nu0">1</span><span class="br0">]</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> longitudeStr <span class="sy0">=</span> args<span class="br0">[</span><span class="nu0">2</span><span class="br0">]</span><span class="sy0">;</span>
        <span class="kw4">double</span> lon, lat, mpp<span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> centre<span class="sy0">;</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            mpp <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+double"><span class="kw3">Double</span></a>.<span class="me1">parseDouble</span><span class="br0">(</span>mppStr<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"MPP must be of type Double or Integer."</span><span class="br0">)</span><span class="sy0">;</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Exiting"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            lat <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+double"><span class="kw3">Double</span></a>.<span class="me1">parseDouble</span><span class="br0">(</span>latitudeStr<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Latitude must be of type Double or Integer."</span><span class="br0">)</span><span class="sy0">;</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Exiting"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            lon <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+double"><span class="kw3">Double</span></a>.<span class="me1">parseDouble</span><span class="br0">(</span>longitudeStr<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Longitude must be of type Double or Integer."</span><span class="br0">)</span><span class="sy0">;</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Exiting"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            centre <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span>lat, lon<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span>InvalidPositionException ipe<span class="br0">)</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Invalid latitude or longitude coordinates."</span><span class="br0">)</span><span class="sy0">;</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">err</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Exiting"</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">return</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Generating chart...Please wait..."</span><span class="br0">)</span><span class="sy0">;</span>
        TileGenerator generator <span class="sy0">=</span> <span class="kw1">new</span> TileGenerator<span class="br0">(</span>TerrainViewer.<span class="me1">TERRAIN_SIZE</span> <span class="sy0">-</span> <span class="nu0">1</span>, mpp, centre<span class="br0">)</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> chart <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a><span class="br0">(</span><span class="st0">"map.png"</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>chart.<span class="me1">exists</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            generator.<span class="me1">createImageMap</span><span class="br0">(</span>TerrainViewer.<span class="me1">TERRAIN_SIZE</span> <span class="sy0">-</span> <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+bufferedimage"><span class="kw3">BufferedImage</span></a> img <span class="sy0">=</span> ImageIO.<span class="me1">read</span><span class="br0">(</span>chart<span class="br0">)</span><span class="sy0">;</span>
            generator.<span class="me1">drawContours</span><span class="br0">(</span>img, TerrainViewer.<span class="me1">TERRAIN_SIZE</span> <span class="sy0">-</span> <span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
 
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
            e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Chart generated. Placed in file 'chart.png'. Exiting."</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
…where  .out file contains longitude / latitude coordinate pairs defining landmass contours. Here an extract:
</p>
<pre class="code">51.79188150756147+-8.25435369629442
51.79184641740534+-8.254357553715453
51.79182071886024+-8.254353833180712
51.79181370477922+-8.254312317813477
51.79181369284153+-8.254267011113086
51.79182535405747+-8.254221642581026
51.79184870922772+-8.254183732747943
51.79188146269924+-8.254183530764353
51.79190724220316+-8.254221208836046
51.79190960635914+-8.254296874457655
51.79188150756147+-8.25435369629442
-1
51.79165344300885+-8.255042583168985
51.79161872648091+-8.255072177259352
51.79158175153456+-8.255082912194254
51.79156558301037+-8.255041382314799
51.79156556852833+-8.254985072910559
51.79158171385971+-8.254936452917438
51.79159555664058+-8.25487274689492
51.79161403682817+-8.254824070938184
51.79164411466118+-8.254798004805433
51.79168584436759+-8.254817161260844
51.79170675060084+-8.25487006519348
51.79169051462138+-8.254930145346941
51.79167197282713+-8.254993914789209
51.79165344300885+-8.255042583168985</pre>

<p>
(-1 acts as a separator, denoting the end of one polygon and the beginning of another).
</p>

<p>
So what's happening here? Well, we basically read the contents of all specified files, whereby each line is broken up into longitude/latitude pairs, converted into pixel (x,y) coordinates and used to construct a polygon which is added to a polygon container once a polygon separator is encountered. Once the object’s paint method is called, this polygon container is iterated and any polygons falling within the canvas (aka viewport) bounds are painted to the graphics context.
Essentially, this algorithm can be summarized as follows:
</p>
<pre class="code">Constructor ( files ): 
   for each file in files
      for each line in file 
         if line == -1
            polygonList.add(polygon)
            new polygon
         else
            polygon.add(parse(line))
            
Paint ( graphics context ):
   for each polygon in polygonList
      if polygon inside view bounds
         graphics context.paint(polygon)</pre>

<p>
<a href="/resources/jme3-tools-heightmap_modelling.png" class="media" title="jme3:tools:heightmap_modelling.png"><img src="/resources/jme3-tools-heightmap_modelling.png" class="media" title="Summarizing process of visualizing a chart. From left to right: We draw the coordinates downloaded from noaa.gov. Ideally, each polygon should be filled in a light colour, whilst the surrounding ocean remains dark. JME uses these images to create an internal representation of the terrain (a float matrix)." alt="Summarizing process of visualizing a chart. From left to right: We draw the coordinates downloaded from noaa.gov. Ideally, each polygon should be filled in a light colour, whilst the surrounding ocean remains dark. JME uses these images to create an internal representation of the terrain (a float matrix)." /></a>
<strong>Above:</strong> Summarizing process of visualizing a chart. From left to right: We draw the coordinates downloaded from noaa.gov. Ideally, each polygon should be filled in a light colour, whilst the surrounding ocean remains dark. JME uses these images to create an internal representation of the terrain (a float matrix).
</p>

<p>
The heightmaps produced by the <code>TileGenerator</code> are essentially arrays containing float values ranging from 0 to 255. For convenience and efficiency, JME treats these arrays as Portable Network Graphic (PNG) images (again, see the Hello Terrain tutorial). This allows us to store each tile as an image, meaning that each tile will only need to be constructed once. Essentially what the tile generator therefore does is draw a greyscale image of each tile whereby dark colours (i.e. low values from 0 - 50) are valleys and high values (200 - 255) become mountains or hills. In order to maintain scale, these values are scaled by dividing the seabed’s maximum height (in meters) by the meters per pixel of the current chart.
With only a few specified points, JME interpolates the rest, making terrain construction using heightmaps more efficient than defining individual vertices for each pixel on the chart.
A tile’s texture is defined by its ”Alphamap”. This is a copy of its heightmap, but instead of defining height values, the floats composing the alphamap image define textures. For this purpose, a method known as ”texture splatting” is employed, whereby texture data is colour coded. That is, assuming that a spatial has two texture layers (let’s call them Tex1 and Tex2), each layer is associated with a colour: in the case of Debrief 3D, blue refers to a sand texture and red refers to dirt/grass textures. Although such an approach to texturing may sound confusing at first, it has the advantages that both heightmaps and alphamaps can be created in one go, and, as they are based on the same principle, can easily be modified in batch rather than individually.
</p>

</div>
<!-- EDIT3 SECTION "Creating your heightmaps" [4657-18070] -->
<h2 class="sectionedit4" id="what_s_all_this_talk_about_tiles">What's all this talk about tiles?</h2>
<div class="level2">

<p>
A tile tree is our way of keeping track of individual tiles. All that it is, is a set of nested sub-directories that holds charts. The top-level directory (our root) contains a chart of the entire world, and each sub-directory an enlarged area of our planet. For example, inside the root, we may have folders that contain a chart just for Ireland, the UK and France. As we traverse the tree further, we get the individual counties or provinces for each country. One way for us to represent this mess of directories, is via a <a href="http://en.wikipedia.org/wiki/Search_tree" class="urlextern" title="http://en.wikipedia.org/wiki/Search_tree" rel="nofollow">Search Tree</a>. 
</p>

</div>
<!-- EDIT4 SECTION "What's all this talk about tiles?" [18071-18701] -->
<h2 class="sectionedit5" id="creating_a_tile_tree">Creating a tile tree</h2>
<div class="level2">
<pre class="code java"><span class="kw1">try</span> <span class="br0">{</span>
            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> resourceDirectory <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a><span class="br0">(</span>worldResourcesDirectory<span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>resourceDirectory.<span class="me1">isDirectory</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">out</span>.<span class="me1">println</span><span class="br0">(</span><span class="st0">"Resource path must be a directory"</span><span class="br0">)</span><span class="sy0">;</span>
                <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+system"><span class="kw3">System</span></a>.<span class="me1">exit</span><span class="br0">(</span><span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
            worldStructure <span class="sy0">=</span> <span class="kw1">new</span> TileTree<span class="br0">(</span>resourceDirectory<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
            e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span></pre>

<p>
Upon initialization, these tiles are read into memory by the <code>TileTree</code> object which treats, as the name suggests, the tiles composing the chart as a tree whereby the root node refers to the entire globe. Its children refer to sub-sections of the globe, and its children in turn to sub-sections of that sub-section. For example, the ”Ireland” node is a direct child of the root node. The ”Cork Harbour” node in turn is a direct child of the ”Ireland” node and represents an enlarged version of a sub-section of the Irish coast. Each such Node consists of a unique ID (used to identify the node), a list of child nodes, a path to the heightmap (tile) that it represents, the zoom level (referred to as the longitude level as the zoom is defined by minutes of longitude per pixel) and a latitude/longitude pair denoting the tile’s centre.
</p>

<p>
Each heightmap is rendered depending on which ID the user selects (where each node in the tree is listed by its unique ID). As an ID is selected, the tree is traversed to find the node matching the given ID. The path to its heightmap is extracted and the heightmap is rendered by extracting the float array from the loaded image (that is, a texture object is created and loaded with the heightmap. A ImageBasedHeightMap object is then used to convert the heightmap and alphamap into corresponding height and texture arrays). → again, see JME tutorial on terrain.
</p>

<p>
The Tile Tree’s contents is stored in assets/Heightmaps, and each directory level is composed of one descriptor file, one heightmap (in the form of a PNG image) and one alphamap (also in the form of a PNG image). The descriptor files end in a.desc filename extension and contain the geo-coordinate centre of the tile as well as the resolution of the node that they are representing (as always, the resolution is represented in minutes per pixel (mpp)). A descriptor file’s sole purpose is to allow the re-construction of the tile tree upon application initialization. Specifically, this is achieved by the ChartModel object which instantiates the TileTree, passing a reference to <em>assets/Heightmaps</em>, which <code>TileTree</code> then recursively scans, constructing the tree by interpreting the descriptor files. It is worth noting that all files per level should be named according to the heightmap tile that it represents. That is, if your level represents a chart of Ireland and your heightmap is named Ireland.png then your descriptor file should be named <em>Ireland.desc</em>, while your alphamap should be named <em>Ireland.png.Alphamap.png</em>.
</p>

<p>
<a href="/resources/jme3-tools-slide1.jpg" class="media" title="jme3:tools:slide1.jpg"><img src="/resources/jme3-tools-slide1.jpg" class="media" title="The Tile Tree" alt="The Tile Tree" /></a>
<a href="/resources/jme3-tools-slide2.jpg" class="media" title="jme3:tools:slide2.jpg"><img src="/resources/jme3-tools-slide2.jpg" class="media" title="Looking inside a node..." alt="Looking inside a node..." /></a>
<strong>Above:</strong> A look inside the “Ireland node”. We can see the heightmap, descriptor file and alphamap.
</p>
<pre class="code java"><span class="coMULTI">/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */</span>
<span class="kw1">package</span> <span class="co2">util.datastructure</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">java.io.File</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.ArrayList</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.List</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.Scanner</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">jme3tools.navigation.Position</span><span class="sy0">;</span>
 
<span class="co3">/**
 * The TileTree handles the storage and retrieval of individual
 * charts. Each Node corresponds to one chart (a node's value being
 * the chart's absolute path. It's ID being the ID under which it is displayed).
 *
 * The tree reflects the application's chart directory structure, with the world
 * as its root and individual countries as its children. Sub-children of these nodes
 * represent "close up" version of each country / geographic sub areas of those countries.
 *
 * @author Benjamin Jakobus
 * @since 1.0
 * @version 1.0
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> TileTree <span class="br0">{</span>
 
    <span class="coMULTI">/* The tree's root node. */</span>
    <span class="kw1">private</span> Node root<span class="sy0">;</span>
 
    <span class="co3">/**
     * Creates a new instance of TileTree. Nodes are generated
     * depending on the contents of the resource directory.
     *
     * @param resourceDirectory         The root of the application's resource
     *                                  directory (the resource directory being the
     *                                  directory in which all charts (aka Heightmaps)
     *                                  are being stored).
     * @since 1.0
     */</span>
    <span class="kw1">public</span> TileTree<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> resourceDirectory<span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> directory <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="kw1">for</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> f <span class="sy0">:</span> resourceDirectory.<span class="me1">listFiles</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>f.<span class="me1">isDirectory</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                directory <span class="sy0">=</span> f<span class="sy0">;</span>
                <span class="kw1">continue</span><span class="sy0">;</span>
            <span class="br0">}</span>
            <span class="kw1">if</span> <span class="br0">(</span>f.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">endsWith</span><span class="br0">(</span><span class="st0">".desc"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                root <span class="sy0">=</span> initNode<span class="br0">(</span>f<span class="br0">)</span><span class="sy0">;</span>
 
            <span class="br0">}</span>
        <span class="br0">}</span>
        initTileTree<span class="br0">(</span>directory, root<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Initializes the tree's children. The root node should be initialized
     * prior to calling this method.
     *
     * @param resourceDirectory         The root of the application's resource
     *                                  directory (the resource directory being the
     *                                  directory in which all charts (aka Heightmaps)
     *                                  are being stored).
     * @param parentNode                The Node to which all
     *                                  subsequent nodes should be attached.
     * @since 1.0
     */</span>
    <span class="kw1">private</span> <span class="kw4">void</span> initTileTree<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> resourceDirectory, Node parentNode<span class="br0">)</span> <span class="br0">{</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> directory <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        Node node <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>parentNode <span class="sy0">==</span> <span class="kw2">null</span> <span class="sy0">||</span> resourceDirectory <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">for</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> f <span class="sy0">:</span> resourceDirectory.<span class="me1">listFiles</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">if</span> <span class="br0">(</span>f.<span class="me1">isDirectory</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                directory <span class="sy0">=</span> f<span class="sy0">;</span>
                <span class="kw1">continue</span><span class="sy0">;</span>
            <span class="br0">}</span>
            <span class="kw1">if</span> <span class="br0">(</span><span class="sy0">!</span>f.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">endsWith</span><span class="br0">(</span><span class="st0">".desc"</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                <span class="kw1">continue</span><span class="sy0">;</span>
            <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
                node <span class="sy0">=</span> initNode<span class="br0">(</span>f<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
        parentNode.<span class="me1">attachChild</span><span class="br0">(</span>node<span class="br0">)</span><span class="sy0">;</span>
        node <span class="sy0">=</span> parentNode<span class="sy0">;</span>
        initTileTree<span class="br0">(</span>directory, parentNode<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Initializes an individual node depending on the contents of the descriptor
     * file (for information on descriptor files, refer to the software documentation).
     *
     * @param file                          The descriptor File with
     *                                      which to initialize the node's contents.
     * @return                              A new Node.
     * @since 1.0
     */</span>
    <span class="kw1">private</span> Node initNode<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+file"><span class="kw3">File</span></a> file<span class="br0">)</span> <span class="br0">{</span>
        Node node <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        Scanner scan<span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> resourcePath <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> nodeID <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> longitudeLevel <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> centre <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="kw4">int</span> currentLine <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>file <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span> node<span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            scan <span class="sy0">=</span> <span class="kw1">new</span> Scanner<span class="br0">(</span>file<span class="br0">)</span><span class="sy0">;</span>
            resourcePath <span class="sy0">=</span> file.<span class="me1">getAbsolutePath</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">replace</span><span class="br0">(</span><span class="st0">".desc"</span>, <span class="st0">".png"</span><span class="br0">)</span><span class="sy0">;</span>
            resourcePath <span class="sy0">=</span> resourcePath.<span class="me1">substring</span><span class="br0">(</span>resourcePath.<span class="me1">indexOf</span><span class="br0">(</span><span class="st0">"assets"</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
            nodeID <span class="sy0">=</span>  file.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">replace</span><span class="br0">(</span><span class="st0">".desc"</span>, <span class="st0">""</span><span class="br0">)</span> <span class="sy0">+</span> <span class="st0">"_"</span> <span class="sy0">+</span> file.<span class="me1">getParentFile</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">getName</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="kw1">while</span> <span class="br0">(</span>scan.<span class="me1">hasNextLine</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                <span class="kw1">if</span> <span class="br0">(</span>currentLine <span class="sy0">==</span> <span class="nu0">0</span><span class="br0">)</span> <span class="br0">{</span>
                    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> tmp <span class="sy0">=</span> scan.<span class="me1">nextLine</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                    <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a><span class="br0">[</span><span class="br0">]</span> array <span class="sy0">=</span> tmp.<span class="me1">split</span><span class="br0">(</span><span class="st0">"<span class="es0">\\</span>+"</span><span class="br0">)</span><span class="sy0">;</span>
                    centre <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+double"><span class="kw3">Double</span></a>.<span class="me1">parseDouble</span><span class="br0">(</span>array<span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span><span class="br0">)</span>,
                            <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+double"><span class="kw3">Double</span></a>.<span class="me1">parseDouble</span><span class="br0">(</span>array<span class="br0">[</span><span class="nu0">1</span><span class="br0">]</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                    currentLine<span class="sy0">++;</span>
                <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
                    longitudeLevel <span class="sy0">=</span> scan.<span class="me1">nextLine</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">trim</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
                <span class="br0">}</span>
            <span class="br0">}</span>
            node <span class="sy0">=</span> <span class="kw1">new</span> Node<span class="br0">(</span>nodeID, resourcePath, longitudeLevel, centre<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> e<span class="br0">)</span> <span class="br0">{</span>
            e.<span class="me1">printStackTrace</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">return</span> node<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Returns the Node matching the given ID.
     *
     * @param nodeID                The ID of the Node that you
     *                              wish to retrieve.
     * @return                      The Node matching the given ID.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> Node find<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> nodeID<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> find<span class="br0">(</span>root, nodeID<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Returns the Node matching the given ID. This method is similar
     * to find() with the exception that it only begins searching from
     * a certain node downwards.
     * 
     * @param nodeToSearch          The Node from which to start searching.
     * @param nodeID                The ID of the Node that you
     *                              wish to retrieve.
     * @return                      The Node matching the given ID.
     * @since 1.0
     */</span>
    <span class="kw1">private</span> Node find<span class="br0">(</span>Node nodeToSearch, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> nodeID<span class="br0">)</span> <span class="br0">{</span>
        Node newNode <span class="sy0">=</span> <span class="kw2">null</span><span class="sy0">;</span>
        <span class="kw1">if</span> <span class="br0">(</span>nodeToSearch <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span> newNode<span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">if</span> <span class="br0">(</span>nodeToSearch.<span class="me1">getNodeID</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">trim</span><span class="br0">(</span><span class="br0">)</span>.<span class="me1">compareTo</span><span class="br0">(</span>nodeID.<span class="me1">trim</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="sy0">==</span> <span class="nu0">0</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span> nodeToSearch<span class="sy0">;</span>
        <span class="br0">}</span> <span class="kw1">else</span> <span class="br0">{</span>
            <span class="kw1">for</span> <span class="br0">(</span>Node n <span class="sy0">:</span> nodeToSearch.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
                newNode <span class="sy0">=</span> find<span class="br0">(</span>n, nodeID<span class="br0">)</span><span class="sy0">;</span>
                <span class="kw1">if</span> <span class="br0">(</span>newNode <span class="sy0">!=</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
                    <span class="kw1">return</span> newNode<span class="sy0">;</span>
                <span class="br0">}</span>
            <span class="br0">}</span>
        <span class="br0">}</span>
        <span class="kw1">return</span> newNode<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Retrieves all nodes within the tree.
     *
     * @return                      A List of all nodes within the
     *                              tree.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> List<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span> getNodes<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        List<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span> nodes <span class="sy0">=</span> <span class="kw1">new</span> ArrayList<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        getNodes<span class="br0">(</span>root, nodes<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">return</span> nodes<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Returns all the children of a specific Node.
     *
     * @param node                  The Node whose children you want.
     * @param nodes                 The List to which to add these children.
     * @since 1.0
     */</span>
    <span class="kw1">private</span> <span class="kw4">void</span> getNodes<span class="br0">(</span>Node node, List<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span> nodes<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">if</span> <span class="br0">(</span>node <span class="sy0">==</span> <span class="kw2">null</span><span class="br0">)</span> <span class="br0">{</span>
            <span class="kw1">return</span><span class="sy0">;</span>
        <span class="br0">}</span>
        <span class="kw1">for</span> <span class="br0">(</span>Node n <span class="sy0">:</span> node.<span class="me1">getChildren</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span> <span class="br0">{</span>
            getNodes<span class="br0">(</span>n, nodes<span class="br0">)</span><span class="sy0">;</span>
        <span class="br0">}</span>
        nodes.<span class="me1">add</span><span class="br0">(</span>node<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
..and the Node:
</p>
<pre class="code java"><span class="kw1">package</span> <span class="co2">util.datastructure</span><span class="sy0">;</span>
 
<span class="kw1">import</span> <span class="co2">java.util.ArrayList</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">java.util.List</span><span class="sy0">;</span>
<span class="kw1">import</span> <span class="co2">jme3tools.navigation.Position</span><span class="sy0">;</span>
 
<span class="co3">/**
 * An individual node within the TileTree. Each Node
 * represents an individual tile (i.e. heightmap + alphamap).
 *
 * @author Benjamin Jakobus
 * @since 1.0
 * @version 1.0
 */</span>
<span class="kw1">public</span> <span class="kw1">class</span> Node <span class="br0">{</span>
    <span class="coMULTI">/* The node's unique identifier. */</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> nodeID<span class="sy0">;</span>
 
    <span class="coMULTI">/* Path to the resource that the node represents (aka the node's value). */</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> resource<span class="sy0">;</span>
 
    <span class="coMULTI">/* The node's children. */</span>
    <span class="kw1">private</span> List<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span> children<span class="sy0">;</span>
 
    <span class="coMULTI">/* The resolution (width in degrees of longitude) represented by this node.
     * i.e. the resolution of the chart that the node represents.
     */</span>
    <span class="kw1">private</span> <span class="kw4">double</span> longitudeLevel<span class="sy0">;</span>
 
    <span class="coMULTI">/* The centre of the chart (aka tile) that the node represents. */</span>
    <span class="kw1">private</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> centre<span class="sy0">;</span>
 
    <span class="co3">/**
     * Constructor.
     * 
     * @param nodeID                The node's unique identifier.
     * @param resource              Path to the resource that the node represents
     *                              (aka the node's value).
     * @param longitudeLevel        The resolution (width in degrees of longitude)
     *                              represented by this node.
     * @param centre                The centre of the chart (aka tile) that the
     *                              node represents.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> Node<span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> nodeID, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> resource, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> longitudeLevel, <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> centre<span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">this</span>.<span class="me1">nodeID</span> <span class="sy0">=</span> nodeID<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">resource</span> <span class="sy0">=</span> resource<span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">longitudeLevel</span> <span class="sy0">=</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+double"><span class="kw3">Double</span></a>.<span class="me1">parseDouble</span><span class="br0">(</span>longitudeLevel<span class="br0">)</span><span class="sy0">;</span>
        <span class="kw1">this</span>.<span class="me1">centre</span> <span class="sy0">=</span> centre<span class="sy0">;</span>
        children <span class="sy0">=</span> <span class="kw1">new</span> ArrayList<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Returns all of the node's children.
     *
     * @return          A List containing all of the node's children.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> List<span class="sy0">&lt;</span>Node<span class="sy0">&gt;</span> getChildren<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> children<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Returns the node's ID.
     *
     * @return          The node's unique identifier.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> getNodeID<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> nodeID<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Returns the path to the tile that the node represents.
     *
     * @return          The path to the tile that the node represents.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+string"><span class="kw3">String</span></a> getResource<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> resource<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Attaches a child to this node.
     *
     * @param child     The Node to attach.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> <span class="kw4">void</span> attachChild<span class="br0">(</span>Node child<span class="br0">)</span> <span class="br0">{</span>
        children.<span class="me1">add</span><span class="br0">(</span>child<span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * Returns the width in degrees of longitude of the chart / resource that this
     * node represents.
     *
     * @return          the width in degrees of longitude of the chart / resource 
     *                  that this node represents.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> <span class="kw4">double</span> getLongitudeLevel<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> longitudeLevel<span class="sy0">;</span>
    <span class="br0">}</span>
 
    <span class="co3">/**
     * The centre coordinate of the tile / chart that this node represents.
     * 
     * @return          The chart's centre in terms of latitude / longitude.
     * @since 1.0
     */</span>
    <span class="kw1">public</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> getCentre<span class="br0">(</span><span class="br0">)</span> <span class="br0">{</span>
        <span class="kw1">return</span> centre<span class="sy0">;</span>
    <span class="br0">}</span>
<span class="br0">}</span></pre>

<p>
Loading a new chart is simple: all that we need to do is get the TileTree to find the chart for us (it'll handle loading the descriptor file and just return a node):
</p>
<pre class="code java">Node node <span class="sy0">=</span> tileTree.<span class="me1">find</span><span class="br0">(</span>chartID<span class="br0">)</span><span class="sy0">;</span></pre>

<p>
We then use the returned node, to adjust our zoom-level:
</p>
<pre class="code java">mapModel.<span class="me1">calculateMinutesPerWorldUnit</span><span class="br0">(</span>node.<span class="me1">getLongitudeLevel</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
mapModel.<span class="me1">setCentre</span><span class="br0">(</span>node.<span class="me1">getCentre</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span></pre>

</div>
<!-- EDIT5 SECTION "Creating a tile tree" [18702-32425] -->
<h2 class="sectionedit6" id="drawing_the_mercator_grid">Drawing the Mercator Grid</h2>
<div class="level2">

<p>
A mercator grid reflects the ”stretching” of the flat Mercator chart through the widening of the longitude / latitude lines. Using JME’s Mesh class, a 3D representation of the grid can be drawn procedurally (as opposed to pre-defining the mesh’s vertices using a 3D modelling tool such as Blender). This is achieved by defining a vector of positions, whereby each entry i within the vector denotes the starting point of a grid line, and i + 1 defining the line’s end-point. Next, the the order in which the mesh is constructed from these coordinates is defined. These are basically index pairs as the mesh consists of a set of lines, each having a start and end point. Finally, the coordinates vector and the indices are added to the mesh, which in turn is used to define the Geometry that is added to the scene graph:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw4">void</span> createGrid<span class="br0">(</span><span class="kw4">double</span> longitudeLevel, <span class="kw4">float</span> increment<span class="br0">)</span> <span class="br0">{</span>
        granularity <span class="sy0">=</span> increment<span class="sy0">;</span>
        Mesh m <span class="sy0">=</span> <span class="kw1">new</span> Mesh<span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        m.<span class="me1">setMode</span><span class="br0">(</span>Mesh.<span class="me1">Mode</span>.<span class="me1">Lines</span><span class="br0">)</span><span class="sy0">;</span>
        m.<span class="me1">setLineWidth</span><span class="br0">(</span>1f<span class="br0">)</span><span class="sy0">;</span>
 
        <span class="kw4">float</span> max <span class="sy0">=</span> <span class="br0">(</span>longitudeLevel <span class="sy0">&lt;</span> <span class="nu0">8</span> <span class="sy0">?</span> <span class="nu0">2</span> <span class="sy0">:</span> <span class="nu0">85</span><span class="br0">)</span><span class="sy0">;</span>
        <span class="kw4">float</span> max2 <span class="sy0">=</span> <span class="br0">(</span>longitudeLevel <span class="sy0">&lt;</span> <span class="nu0">8</span> <span class="sy0">?</span> <span class="nu0">180</span> <span class="sy0">/</span> <span class="nu0">8</span> <span class="sy0">:</span> <span class="nu0">180</span><span class="br0">)</span><span class="sy0">;</span>
        Vector3f<span class="br0">[</span><span class="br0">]</span> positions <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">[</span><span class="br0">(</span><span class="kw4">int</span><span class="br0">)</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+math"><span class="kw3">Math</span></a>.<span class="me1">ceil</span><span class="br0">(</span>max <span class="sy0">/</span> increment<span class="br0">)</span> <span class="sy0">*</span> <span class="nu0">4</span><span class="br0">)</span> <span class="sy0">+</span> <span class="br0">(</span><span class="kw4">int</span><span class="br0">)</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+math"><span class="kw3">Math</span></a>.<span class="me1">ceil</span><span class="br0">(</span>max2 <span class="sy0">/</span> increment<span class="br0">)</span> <span class="sy0">*</span> <span class="nu0">4</span><span class="br0">)</span><span class="br0">]</span><span class="sy0">;</span>
        <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a> pos<span class="sy0">;</span>
 
        <span class="kw4">int</span> i <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span>
        <span class="kw1">try</span> <span class="br0">{</span>
            <span class="co1">// Calculate initial spacings for the meridians and</span>
            <span class="co1">// parallels</span>
 
 
            <span class="co1">// Approach the grid construction from north to south and</span>
            <span class="co1">// east to west.</span>
            positions<span class="br0">[</span><span class="nu0">0</span><span class="br0">]</span> <span class="sy0">=</span> <span class="kw1">new</span> Vector3f<span class="br0">(</span><span class="nu0">0</span>, <span class="nu0">0</span>, <span class="nu0">0</span><span class="br0">)</span><span class="sy0">;</span>
 
            <span class="co1">// Latitude lines for northern hemisphere</span>
            <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">float</span> lat <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> lat <span class="sy0">&lt;</span> max<span class="sy0">;</span> lat <span class="sy0">+=</span> increment, i <span class="sy0">+=</span> <span class="nu0">2</span><span class="br0">)</span> <span class="br0">{</span>
                pos <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span>lat, <span class="nu0">180</span><span class="br0">)</span><span class="sy0">;</span>
                positions<span class="br0">[</span>i<span class="br0">]</span> <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">toWorldUnit</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span>lat, <span class="sy0">-</span><span class="nu0">180</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                positions<span class="br0">[</span>i <span class="sy0">+</span> <span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">toWorldUnit</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
 
            <span class="co1">// Latitude lines for southern hemisphere</span>
            <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">float</span> lat <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> lat <span class="sy0">&lt;</span> max<span class="sy0">;</span> lat <span class="sy0">+=</span> increment, i <span class="sy0">+=</span> <span class="nu0">2</span><span class="br0">)</span> <span class="br0">{</span>
                pos <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span>lat <span class="sy0">*</span> <span class="sy0">-</span><span class="nu0">1</span>, <span class="nu0">180</span><span class="br0">)</span><span class="sy0">;</span>
                positions<span class="br0">[</span>i<span class="br0">]</span> <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">toWorldUnit</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span>lat <span class="sy0">*</span> <span class="sy0">-</span><span class="nu0">1</span>, <span class="sy0">-</span><span class="nu0">180</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                positions<span class="br0">[</span>i <span class="sy0">+</span> <span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">toWorldUnit</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
 
            max <span class="sy0">=</span> <span class="br0">(</span>longitudeLevel <span class="sy0">&lt;</span> <span class="nu0">8</span> <span class="sy0">?</span> <span class="nu0">180</span> <span class="sy0">/</span> <span class="nu0">8</span> <span class="sy0">:</span> <span class="nu0">180</span><span class="br0">)</span><span class="sy0">;</span>
            <span class="co1">// Longitude lines for northern hemisphere</span>
            <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">float</span> lon <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> lon <span class="sy0">&lt;</span> max<span class="sy0">;</span> lon <span class="sy0">+=</span> increment, i <span class="sy0">+=</span> <span class="nu0">2</span><span class="br0">)</span> <span class="br0">{</span>
                pos <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span><span class="nu0">85</span>, lon<span class="br0">)</span><span class="sy0">;</span>
                positions<span class="br0">[</span>i<span class="br0">]</span> <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">toWorldUnit</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span><span class="sy0">-</span><span class="nu0">85</span>, lon<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                positions<span class="br0">[</span>i <span class="sy0">+</span> <span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">toWorldUnit</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
 
            <span class="co1">// Longitude lines for southern hemisphere</span>
            <span class="kw1">for</span> <span class="br0">(</span><span class="kw4">float</span> lon <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> lon <span class="sy0">&lt;</span> max<span class="sy0">;</span> lon <span class="sy0">+=</span> increment, i <span class="sy0">+=</span> <span class="nu0">2</span><span class="br0">)</span> <span class="br0">{</span>
                pos <span class="sy0">=</span> <span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span><span class="nu0">85</span>, lon <span class="sy0">*</span> <span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span><span class="sy0">;</span>
                positions<span class="br0">[</span>i<span class="br0">]</span> <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">toWorldUnit</span><span class="br0">(</span><span class="kw1">new</span> <a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a><span class="br0">(</span><span class="sy0">-</span><span class="nu0">85</span>, lon <span class="sy0">*</span> <span class="sy0">-</span><span class="nu0">1</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
                positions<span class="br0">[</span>i <span class="sy0">+</span> <span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">toWorldUnit</span><span class="br0">(</span>pos<span class="br0">)</span><span class="sy0">;</span>
            <span class="br0">}</span>
        <span class="br0">}</span> <span class="kw1">catch</span> <span class="br0">(</span><a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+exception"><span class="kw3">Exception</span></a> ipe<span class="br0">)</span> <span class="br0">{</span>
 
        <span class="br0">}</span>
 
        <span class="kw4">int</span><span class="br0">[</span><span class="br0">]</span> indices <span class="sy0">=</span> <span class="kw1">new</span> <span class="kw4">int</span><span class="br0">[</span>i<span class="br0">]</span><span class="sy0">;</span>
        <span class="kw4">int</span> v<span class="sy0">;</span>
        <span class="kw1">for</span> <span class="br0">(</span>i <span class="sy0">=</span> <span class="nu0">0</span>, v <span class="sy0">=</span> <span class="nu0">0</span><span class="sy0">;</span> i <span class="sy0">&lt;</span> indices.<span class="me1">length</span><span class="sy0">;</span> i <span class="sy0">+=</span> <span class="nu0">2</span>, v<span class="sy0">++</span><span class="br0">)</span> <span class="br0">{</span>
            indices<span class="br0">[</span>i<span class="br0">]</span> <span class="sy0">=</span> i<span class="sy0">;</span>
            indices<span class="br0">[</span>i <span class="sy0">+</span> <span class="nu0">1</span><span class="br0">]</span> <span class="sy0">=</span> i <span class="sy0">+</span> <span class="nu0">1</span><span class="sy0">;</span>
        <span class="br0">}</span>
 
        m.<span class="me1">setBuffer</span><span class="br0">(</span>Type.<a href="http://www.google.com/search?hl=en&amp;q=allinurl%3Adocs.oracle.com+javase+docs+api+position"><span class="kw3">Position</span></a>, <span class="nu0">3</span>, BufferUtils.<span class="me1">createFloatBuffer</span><span class="br0">(</span>positions<span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
 
        m.<span class="me1">setBuffer</span><span class="br0">(</span>Type.<span class="me1">Index</span>, <span class="nu0">1</span>, indices<span class="br0">)</span><span class="sy0">;</span>
        m.<span class="me1">updateBound</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        m.<span class="me1">updateCounts</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        Material mat <span class="sy0">=</span> <span class="kw1">new</span> Material<span class="br0">(</span>assetManager, <span class="st0">"Common/MatDefs/Misc/Unshaded.j3md"</span><span class="br0">)</span><span class="sy0">;</span>
        mat.<span class="me1">setColor</span><span class="br0">(</span><span class="st0">"m_Color"</span>, ColorRGBA.<span class="me1">Gray</span><span class="br0">)</span><span class="sy0">;</span>
        gridGeometry <span class="sy0">=</span> <span class="kw1">new</span> Geometry<span class="br0">(</span><span class="st0">"Grid"</span>, m<span class="br0">)</span><span class="sy0">;</span>
        gridGeometry.<span class="me1">setMaterial</span><span class="br0">(</span>mat<span class="br0">)</span><span class="sy0">;</span>
        Vector3f worldCentre <span class="sy0">=</span> TerrainViewer.<span class="me1">mapModel</span>.<span class="me1">getCentreWu</span><span class="br0">(</span><span class="br0">)</span><span class="sy0">;</span>
        gridGeometry.<span class="me1">setLocalTranslation</span><span class="br0">(</span><span class="kw1">new</span> Vector3f<span class="br0">(</span>worldCentre.<span class="me1">getX</span><span class="br0">(</span><span class="br0">)</span>,
                gridHeight, worldCentre.<span class="me1">getZ</span><span class="br0">(</span><span class="br0">)</span><span class="br0">)</span><span class="br0">)</span><span class="sy0">;</span>
    <span class="br0">}</span></pre>

<p>
<a href="/resources/jme3-tools-screen_shot_2011-12-18_at_13.12.01.png" class="media" title="jme3:tools:screen_shot_2011-12-18_at_13.12.01.png"><img src="/resources/jme3-tools-screen_shot_2011-12-18_at_13.12.01.png" class="media" alt="" /></a>
</p>

</div>
<!-- EDIT6 SECTION "Drawing the Mercator Grid" [32426-] -->
