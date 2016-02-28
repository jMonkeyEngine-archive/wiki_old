---
title: iOS Deployment
---
<h2 class="sectionedit1" id="ios_deployment">iOS Deployment</h2>
<div class="level2">

<p>
To use iOS deployment you need a computer running MacOSX and a version of Xcode 4.0+ installed. To deploy to a device or the Apple App Store, you need an Apple developer account.
</p>

<p>
</p><p></p><div class="notewarning">Note that at the moment iOS deployment is in alpha state.
</div>


<p>
iOS deployment works via cross-compilation to native iOS ARM code, there is no virtual machine running on the device. The Avian JVM supports this feature while maintaining general compatibility to OpenJDK and JNI for native access. The minimum compatible iOS deployment target is 4.3.
</p>

<p>
</p><p></p><div class="notetip">To install the iOS deployment plugin, go to Tools→Plugins and under “Available plugins” select the “iOS Support” plugin.
</div>


</div>
<!-- EDIT1 SECTION "iOS Deployment" [1-710] -->
<h3 class="sectionedit2" id="enabling_ios_deployment">Enabling iOS deployment</h3>
<div class="level3">

<p>
To enable iOS deployment, go to the project settings and under “Application→iOS” select the “Enable iOS deployment” checkbox, adapt the application ID and then press OK.
</p>

<p>
<a href="/resources/jme3-ios-deployment.png" class="media" title="jme3:ios-deployment.png"><img src="/resources/jme3-ios-deployment.png" class="media" alt="" /></a>
</p>

<p>
After enabling deployment, a new <code>ios</code> directory is created in the project root that contains a <code>project</code> and a <code>src</code> folder. The <code>ios/project</code> folder contains an Xcode project that you will use to build and run the final iOS application for both iPhone and iOS. The <code>ios/src</code> folder contains java and native source files for bridging iOS and native code, you can add .java and .m files with your own iOS code here.
</p>

<p>
</p><p></p><div class="noteimportant">When you enable iOS deployment for the first time or any time that the Avian library and OpenJDK is updated, they will be extracted to your SDK settings folder, wait until it has been extracted before building an iOS-enabled project.
</div>


</div>
<!-- EDIT2 SECTION "Enabling iOS deployment" [711-1631] -->
<h3 class="sectionedit3" id="building_the_ios_binaries">Building the iOS binaries</h3>
<div class="level3">

<p>
The iOS binaries are automatically built when you have iOS deployment enabled and build your project in the jME3 SDK.
</p>

<p>
When the iOS binaries are built, all needed classes, including a complete copy of the OpenJDK7 classes are run through a proguard process that strips out the unnecessary classes for the project and optimizes the code for the platform. This happens without changing the naming structure so that reflection etc. still works. If necessary, adapt the proguard options in the ios properties file.
</p>

<p>
After the iOS classpath has been created the avian compiler is used to create a native .o file from the classpath for both arm (device) and i386 (simulator). Furthermore the other needed avian .o files are extracted and a library list is compiled which is referenced in the Xcode project.
</p>

<p>
If an error occurs about jni.h not being found, either install the SDK for 10.9 in XCode or set the header search path in the XCode project settings, in the default project thats <code>/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.9.sdk/System/Library/Frameworks/JavaVM.framework/Headers/</code>
</p>

</div>
<!-- EDIT3 SECTION "Building the iOS binaries" [1632-2803] -->
<h3 class="sectionedit4" id="running_and_deploying_the_application">Running and deploying the application</h3>
<div class="level3">

<p>
To run the application, open the Xcode project under <code>ios/project</code> in Xcode and press the run button. You can make changes to the UI and native invocation classes in the Xcode project as well. From here you can also deploy the application to your devices or the App Store.
</p><p></p><div class="notetip">Note that you should also adapt the project settings like application name and registration package in Xcode before deploying the final application.
</div>


</div>
<!-- EDIT4 SECTION "Running and deploying the application" [2804-3292] -->
<h3 class="sectionedit5" id="creating_native_and_java_code_for_ios">Creating native and java code for iOS</h3>
<div class="level3">

<p>
To bridge between native and java code, JNI is used like in a normal java application. The <code>ios/src</code> folder is for Java and C/Obj-C source files that are specific to your iOS application. In these java files you have access to the full project classpath as well as the iOS-specific jME3 classes.
</p>

<p>
The JmeAppHarness.java class is initialized and called from native code through the default project and you can extend it to perform other native operations. It has a simple native popup method. The JmeAppHarness.m file contains the native method needed for that popup.
</p>

<p>
Effectively native code can reside in both the Xcode project and in the <code>ios/src</code> folder. To keep the dependencies clean and make code reusable you should try to put generic native code that does not depend on the Xcode project in the <code>ios/src</code> folder. You can also mix and match ARC and non-ARC code through this by converting the main project to use ARC and putting code with manual memory management in the <code>ios/src</code> folder.
</p>

<p>
Java code for iOS should be in the <code>ios/src</code> folder as well for clean separation, its also the only place where they will be compiled with a reference to the iOS specific jME classes. For information on how to connect your application code and device specific code, see the <a href="/jme3/android.html" class="wikilink1" title="jme3:android">notes in the android deployment documentation</a>.
</p>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/ios.html" class="wikilink1" title="tag:ios" rel="tag">iOS</a>,
	<a href="/tag/mac.html" class="wikilink1" title="tag:mac" rel="tag">Mac</a>,
	<a href="/tag/macos.html" class="wikilink1" title="tag:macos" rel="tag">MacOS</a>,
	<a href="/tag/deployment.html" class="wikilink1" title="tag:deployment" rel="tag">deployment</a>,
	<a href="/tag/platform.html" class="wikilink1" title="tag:platform" rel="tag">platform</a>
</span></div>

</div>
<!-- EDIT5 SECTION "Creating native and java code for iOS" [3293-] -->
