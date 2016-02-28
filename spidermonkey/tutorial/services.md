---
title: Service system
---
<h1 class="sectionedit1" id="service_system">Service system</h1>
<div class="level1">

<p>
</p><p></p><div class="notewarning">This article covers a deprecated <abbr title="Application Programming Interface">API</abbr>! See <a href="/jme3/advanced/networking.html" class="wikilink1" title="jme3:advanced:networking">networking</a> for current documentation.
</div>


<p>
The service system is meant to create a common way of using plugins. It is a tiny system, on Server and Client level. In this tutorial I'll tell you how to use services, and how to create your own.
</p>

</div>
<!-- EDIT1 SECTION "Service system" [1-347] -->
<h3 class="sectionedit2" id="creating_services">Creating services</h3>
<div class="level3">

<p>
Creating services is really easy - you just have to implement the Service interface. <strong>Make sure you don't do anything time consuming</strong> since the developer may not be expecting it. Services can choose to support Server, Client, or both. To implement this, use the appropriate constructors:
</p>
<pre class="code java"><span class="kw1">public</span> <span class="kw1">class</span> MyExampleService <span class="kw1">implements</span> Service <span class="br0">{</span>
   <span class="kw1">public</span> MyExampleService<span class="br0">(</span>Server server<span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// By adding the constructor with the Server as argument, this service</span>
      <span class="co1">//  now supports servers.</span>
   <span class="br0">}</span>
 
   <span class="kw1">public</span> MyExampleService<span class="br0">(</span>Client client<span class="br0">)</span> <span class="br0">{</span>
      <span class="co1">// Same goes for client. I could just leave this constructor out, and</span>
      <span class="co1">//  SpiderMonkey would determine this service does not support client mode.</span>
   <span class="br0">}</span>
<span class="br0">}</span></pre>

</div>
<!-- EDIT2 SECTION "Creating services" [348-1103] -->
<h3 class="sectionedit3" id="using_services">Using services</h3>
<div class="level3">

<p>
The Server and Client class both have a method called getService(). It retrieves a service based on class name, and instantiates it if necessary. From there you can use the service.
</p>

<p>
The Service system is not a terribly powerful system, neither does it do safety checks and service management - it just provides a way to commonly manage extensions.
</p>

<p>
That's it! Next tutorial we're going to have a look at how to use the streaming <abbr title="Application Programming Interface">API</abbr>.
</p>

</div>
<!-- EDIT3 SECTION "Using services" [1104-] -->
