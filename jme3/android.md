---
title: Android Support in the jMonkeyEngine
---
<h1 class="sectionedit1" id="android_support_in_the_jmonkeyengine">Android Support in the jMonkeyEngine</h1>
<div class="level1">

<p>
jMonkeyEngine supports android deployment, and it's fully integrated in the SDK.
The android support is in constant enhancement so if you have questions or suggestions, please leave a comment on the <a href="http://jmonkeyengine.org/groups/android/forum/topic/android-deployment-via-checkbox-is-here" class="urlextern" title="http://jmonkeyengine.org/groups/android/forum/topic/android-deployment-via-checkbox-is-here" rel="nofollow">Android forum thread</a>!
</p>

</div>
<!-- EDIT1 SECTION "Android Support in the jMonkeyEngine" [1-370] -->
<h2 class="sectionedit2" id="requirements">Requirements</h2>
<div class="level2">

</div>
<!-- EDIT2 SECTION "Requirements" [371-393] -->
<h3 class="sectionedit3" id="developer_requirements">Developer Requirements</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Install <a href="/documentation.html" class="wikilink1" title="documentation">jMonkeyEngine SDK</a> (Remember to install <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" class="urlextern" title="http://www.oracle.com/technetwork/java/javase/downloads/index.html" rel="nofollow">JDK</a>)</div>
</li>
<li class="level1"><div class="li"> Install <a href="http://developer.android.com/sdk/index.html" class="urlextern" title="http://developer.android.com/sdk/index.html" rel="nofollow">Android SDK Manager 22.6.2</a> or newer.</div>
<ol>
<li class="level2"><div class="li"> (You don't need the ADT Bundle for Windows. Choose “USE AN EXISTING IDE” and download the SDK Tools)</div>
</li>
<li class="level2"><div class="li"> It's recommended to choose another destination folder.</div>
</li>
<li class="level2"><div class="li"> Start the SDK Manager and install the default selected 13 packages (accept licenses)</div>
</li>
</ol>
</li>
</ul>

<p>
<a href="/resources/jme3-android_sdk_manager.png" class="media" title="jme3:android_sdk_manager.png"><img src="/resources/jme3-android_sdk_manager.png" class="media" alt="" /></a>
</p>
<ul>
<li class="level1"><div class="li"> (Optional) Install NBAndroid in the jMonkeyEngine SDK:</div>
<ol>
<li class="level2"><div class="li"> Go to Tools→Plugins→Available Plugins.</div>
</li>
<li class="level2"><div class="li"> Install the “Android” plugin.</div>
</li>
</ol>
</li>
</ul>

</div>
<!-- EDIT3 SECTION "Developer Requirements" [394-1104] -->
<h3 class="sectionedit4" id="user_requirements">User Requirements</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> Android 2.3 device or better with development mode (“USB-Debugging”) enabled</div>
</li>
<li class="level1"><div class="li"> Graphic card that supports OpenGL ES 2.0 or better</div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/groups/android/forum/topic/does-my-phone-meet-the-requirements-necessary-to-run-jmonkeyengine-3/" class="urlextern" title="http://jmonkeyengine.org/groups/android/forum/topic/does-my-phone-meet-the-requirements-necessary-to-run-jmonkeyengine-3/" rel="nofollow">Does my phone meet the requirements necessary to run jMonkeyEngine 3?</a></div>
</li>
<li class="level1"><div class="li"> Remember to install the driver software on your computer</div>
</li>
</ul>

</div>
<!-- EDIT4 SECTION "User Requirements" [1105-1529] -->
<h2 class="sectionedit5" id="features">Features</h2>
<div class="level2">

</div>
<!-- EDIT5 SECTION "Features" [1530-1549] -->
<h3 class="sectionedit6" id="jmonkeyengine3_android_integration">jMonkeyEngine3 Android Integration</h3>
<div class="level3">
<ul>
<li class="level1"><div class="li"> JME app encapsulated in an Android activity (the AndroidHarness).</div>
</li>
<li class="level1"><div class="li"> JME display in a GlSurfaceView.</div>
</li>
<li class="level1"><div class="li"> Android touch events are encapsulated into JME touch event or translated into mouse events.</div>
</li>
<li class="level1"><div class="li"> Errors are handled universally in the Harness.</div>
</li>
<li class="level1"><div class="li"> Lifecycle management</div>
<ul>
<li class="level2"><div class="li"> Leaving the activity with the Back key destroys the app (quit).</div>
</li>
<li class="level2"><div class="li"> Leaving the activity with the Home key freezes the app in the background. When you return, the app is in the same state as when you left it (pause).</div>
</li>
</ul>
</li>
<li class="level1"><div class="li"> Currently supports all jmetests except:</div>
<ul>
<li class="level2"><div class="li"> Post processing filters. Functional but most of the time very slow</div>
</li>
<li class="level2"><div class="li"> Shadows. Functional but most of the time very slow</div>
</li>
<li class="level2"><div class="li"> Water. Functional but very slow.</div>
</li>
</ul>
</li>
</ul>

</div>
<!-- EDIT6 SECTION "jMonkeyEngine3 Android Integration" [1550-2309] -->
<h3 class="sectionedit7" id="jmonkeyengine_sdk_android_integration">jMonkeyEngine SDK Android Integration</h3>
<div class="level3">

<p>
Mobile deployment is a “one-click” option next to Desktop/WebStart/Applet deployment in the jMonkeyEngine SDK.
</p>
<ul>
<li class="level1"><div class="li"> Automatic creation of Android harness and settings.</div>
</li>
<li class="level2"><div class="li"> Ant script build target creates APK file.</div>
</li>
<li class="level2"><div class="li"> Ant script run target executes APK on Android Emulator or mobile device.</div>
</li>
</ul>

</div>
<!-- EDIT7 SECTION "jMonkeyEngine SDK Android Integration" [2310-2653] -->
<h2 class="sectionedit8" id="instructions">Instructions</h2>
<div class="level2">
<ol>
<li class="level1"><div class="li"> Make sure you have installed the Android Project Support into the jMonkeyEngine SDK.</div>
</li>
<li class="level1"><div class="li"> Open the jMonkeyEngine SDK Options&gt;Mobile and enter the path to your Android SDK directory, and click OK. E.g. <code>C:\Program Files\android-sdk</code></div>
</li>
</ol>

</div>

<h4 id="activate_android_deployment">Activate Android Deployment</h4>
<div class="level4">
<ol>
<li class="level1"><div class="li"> Open an existing JME3 project, or create a new JME3 project.</div>
</li>
<li class="level1"><div class="li"> Right-click the project node in the Projects Window and open the Properties.</div>
</li>
<li class="level1"><div class="li"> In the Application&gt;Android Properties, enable Android Deployment, and select an Android target. E.g. <code>Android 4.2.2</code> <br />
This creates a “mobile” folder in your projects directory. This folder contains a complete android project with correct settings to run the application using the AndroidHarness.</div>
</li>
<li class="level1"><div class="li"> (Restart the jMonkeyEngine)</div>
</li>
<li class="level1"><div class="li"> A Mobile Files node appears in the Project window. <br />
It lets you edit the MainActivitity.java, the AndroidManifest.xml, and build.properties.</div>
</li>
</ol>

<p>
<a href="/resources/jme3-nvyyd.png" class="media" title="jme3:nvyyd.png"><img src="/resources/jme3-nvyyd.png" class="media" alt="" /></a>
</p>

<p>
The Android deployment option creates a separate sub-project for android and makes the main project and associated libraries available to the sub-project as libraries. The sub-project can be edited using NBAndroid (see below) or using Eclipse or any other IDE that supports standard android projects. Normally you do not need to edit the android project files. Exceptions are described further below. <em>The libraries are first added to the android sub-project when the main project is built for the first time.</em>
</p>

</div>

<h4 id="build_and_run">Build and Run</h4>
<div class="level4">

<p>
Open your game project in the jMonkeyEngine SDK.
</p>

<p>
<strong>Building</strong>
</p>
<ol>
<li class="level1"><div class="li"> Right-click the project node to build your project. <br />
An APK file is created in the “dist” folder.</div>
</li>
</ol>

<p>
<strong>Running</strong>
</p>
<ol>
<li class="level1"><div class="li"> Right-click the project node and choose Set Main Project.</div>
</li>
<li class="level1"><div class="li"> Select the “Android Device” build configuration next to the Run toolbar button.</div>
</li>
<li class="level1"><div class="li"> <em>Make sure “Compile on Save” is disabled in your project preferences.</em></div>
</li>
<li class="level1"><div class="li"> Run the application on a connected phone by right-clicking it and selecting “Run” or press the “Play” button in the toolbar.</div>
</li>
<li class="level1"><div class="li"> The application will run and output its log to the “Output” window of the SDK.</div>
</li>
<li class="level1"><div class="li"> When finished testing, click the “x” next to the run status in the lower right to quit the logging output.</div>
</li>
</ol>

<p>
The default android run target uses the default device set in the Android configuration utility. If you set that to a phone you can run the application directly on your phone, the emulator does not support OpenGLES 2.0 and cannot run the engine.
</p>

<p>
</p><p></p><div class="noteimportant">When running your application on some Android devices, having a debugging session open via certain IDEs <strong>will significantly lower performance</strong> (some reports suggest a drop from 60 FPS to 4-8 FPS) until the debug session is detached or the application is started directly from the device.
</div>


<p>
Optionally, download <a href="http://code.google.com/p/jmonkeyengine/downloads/detail?name=Jme3Beta1Demo.apk&amp;can=1&amp;q=" class="urlextern" title="http://code.google.com/p/jmonkeyengine/downloads/detail?name=Jme3Beta1Demo.apk&amp;can=1&amp;q=" rel="nofollow">Jme3Beta1Demo.apk</a>
</p>

<p>
During build, the libraries and main jar file from the main project are copied to the android project libs folder for access. During this operation the desktop-specific libraries are replaced with android specific JARs.
</p>

<p>
<strong>Be aware that logging has been identified as having a significant performance hit in Android applications. If getting poor performance please try turning logging either down or off and retesting.</strong>
</p>

</div>

<h4 id="installing_nbandroid">Installing NBAndroid</h4>
<div class="level4">

<p>
Activating the nbandroid plugin in the jMonkeyEngine SDK is optional, but recommended. You do not need the nbandroid plugin for Android support to work, however nbandroid will not interfere and will in fact allow you to edit the android source files and project more conveniently. To be able to edit, extend and code android-specific code in Android projects, install NBAndroid from the update center:
</p>
<ol>
<li class="level1"><div class="li"> Open Tools→Plugins→Settings</div>
</li>
<li class="level1"><div class="li"> Go to Tools→Plugins→Available Plugins.</div>
</li>
<li class="level1"><div class="li"> Install the NbAndroid plugin. (Will show up as Android)</div>
</li>
</ol>

<p>
*If the android plugin is not in that list follow <a href="http://www.nbandroid.org/p/installation.html" class="urlextern" title="http://www.nbandroid.org/p/installation.html" rel="nofollow">these instructions</a>.*
</p>

</div>

<h4 id="notes">Notes</h4>
<div class="level4">
<ul>
<li class="level1"><div class="li"> The package name parameter is only used when creating the project and only sets the android MainActivity package name</div>
</li>
<li class="level1"><div class="li"> The needed android.jar comes with the plugin and is automatically added to the android build</div>
</li>
<li class="level1"><div class="li"> All non-android project libraries are automatically excluded from the android build. This is currently hard-coded in the build script, check nbproject/mobile-impl.xml for the details.</div>
</li>
<li class="level1"><div class="li"> The main application class parameter for the AndroidHarness is taken from the jme3 project settings when enabling android deployment. Currently it is not updated when you change the main class package or name.</div>
</li>
<li class="level1"><div class="li"> When you disable the mobile deployment option, the whole “mobile” folder is deleted.</div>
</li>
<li class="level1"><div class="li"> The “errors” shown in the MainActivity are wrongly displayed only in the editor and will disappear when you install NBAndroid (see below).</div>
</li>
<li class="level1"><div class="li"> To sign your application, edit the mobile/build.properties file to point at valid keystore files.</div>
</li>
</ul>

</div>
<!-- EDIT8 SECTION "Instructions" [2654-7647] -->
<h2 class="sectionedit9" id="android_considerations">Android Considerations</h2>
<div class="level2">

<p>
You can use the jMonkeyEngine SDK to save (theoretically) any jMonkeyEngine app as Android app. But the application has to be prepared for the fact that Android devices have a smaller screen resolution, touchscreens instead of mouse buttons, and (typically) no keyboards.
</p>
<ul>
<li class="level1"><div class="li"> <strong>Inputs:</strong> Devise an alternate control scheme that works for Android users (e.g. using com.jme3.input.controls.TouchListener). This mobile scheme is likely quite different from the desktop scheme.</div>
</li>
<li class="level1"><div class="li"> <strong>Effects:</strong> Android devices do no support 3D features as well as PCs – or even not at all. This restriction includes post-processor filters (depth-of-field blur, bloom, light scattering, cartoon, etc), drop shadows, water effects, 3D Audio. Be prepared that these effects will (at best) slow down the application or (in the worst case) not work at all. Provide the option to switch to a low-fi equivalent! </div>
</li>
<li class="level1"><div class="li"> <strong>Nifty <abbr title="Graphical User Interface">GUI</abbr>:</strong> Use different base UI layout XML files for the mobile version of your app to account for a different screen resolution.</div>
</li>
</ul>

<p>
<strong>Best Practice:</strong> Ideally, you write the core application code in a way that it checks for the environment it's being run on, and automatically adapts the device's limitations by switching off effects, changing input mechanisms etc. Learn how to <a href="/jme3/advanced/read_graphic_card_capabilites.html" class="wikilink1" title="jme3:advanced:read_graphic_card_capabilites">read graphic card capabilites</a> here.
</p>

</div>
<!-- EDIT9 SECTION "Android Considerations" [7648-9014] -->
<h2 class="sectionedit10" id="using_android_specific_functions">Using Android specific functions</h2>
<div class="level2">

<p>
As described above, you should always try to design your application as platform independent as possible. If your game becomes a sudden hit on android, why not release it on Facebook as an applet as well? When your application is designed in a platform independent way, you don't have to do much more but check a checkbox to deploy your application as an applet. But what if you want to for example access the camera of an android device? Inevitably you will have to use android specific api to access the camera.
</p>

<p>
Since the main project is not configured to access the android api directly, you have to install NBAndroid (see above) to be able to edit the created android project in the SDK. After installing, click the “open project” button and navigate to the “mobile” folder inside the main project folder (it should show up with an android “a” icon) and open it.
</p>

<p>
<a href="/resources/jme3-android_access.png" class="media" title="jme3:android_access.png"><img src="/resources/jme3-android_access.png" class="mediaright" alt="" /></a>
Although you will use android specific api, using a camera is not exactly android specific and so you should try to design this part of the application as platform independent as possible as well. As an example, if you want to use the phones camera as an image input stream for a texture, you can create e.g. the AppState that manages the image and makes it available to the application inside the main project (no android code is needed). Then in the android part of the code you make a connection to the camera and update the image in the AppState. This also allows you to easily support cameras on other platforms in the same way or fallback to something else in case the platform doesn't support a camera.
</p>

<p>
Note that you have to build the whole project once to make (new) classes in the main project available to the android part. 
</p>

</div>
<!-- EDIT10 SECTION "Using Android specific functions" [9015-10795] -->
<h2 class="sectionedit11" id="signing_an_apk">Signing an APK</h2>
<div class="level2">

<p>
When you have a mobile project in the “important files” section you have an “Android Properties” file.<br />

There are 2 entries in this file :<br />

key.store=path/to/your/keystore/on/your/drive/mykeystore.keystore<br />

key.alias=mykeystorealias<br />

</p>

<p>
If those entries are filled, the apk will be signed during the build.<br />

You’ll be prompted when building to enter the password (twice). It will generate a signed apk in the dist folder of your project.<br />

</p>

</div>
<!-- EDIT11 SECTION "Signing an APK" [10796-11276] -->
<h2 class="sectionedit12" id="more_info">More Info</h2>
<div class="level2">

<p>
There is currently no proper guidance of running on android.
The SDK will later provide tools to adapt the materials and other graphics settings of the Android deployment version automatically.
</p>
<ul>
<li class="level1"><div class="li"> <a href="https://www.youtube.com/watch?feature=player_embedded&amp;v=np3N4pCCTPo" class="urlextern" title="https://www.youtube.com/watch?feature=player_embedded&amp;v=np3N4pCCTPo" rel="nofollow">Youtube Video on Android deployment</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/groups/android/forum/topic/android-deployment-via-checkbox-is-here" class="urlextern" title="http://jmonkeyengine.org/groups/android/forum/topic/android-deployment-via-checkbox-is-here" rel="nofollow">Android Forum Thread (beta)</a></div>
</li>
<li class="level1"><div class="li"> <a href="http://jmonkeyengine.org/groups/android/forum/topic/how-to-run-your-jme3-application-on-android-androidharness" class="urlextern" title="http://jmonkeyengine.org/groups/android/forum/topic/how-to-run-your-jme3-application-on-android-androidharness" rel="nofollow">Android Forum Thread (alpha)</a></div>
</li>
</ul>
<div class="tags"><span>
	<a href="/tag/documentation.html" class="wikilink1" title="tag:documentation" rel="tag">documentation</a>,
	<a href="/tag/sdk.html" class="wikilink1" title="tag:sdk" rel="tag">sdk</a>,
	<a href="/tag/android.html" class="wikilink1" title="tag:android" rel="tag">android</a>,
	<a href="/tag/deployment.html" class="wikilink1" title="tag:deployment" rel="tag">deployment</a>,
	<a href="/tag/tool.html" class="wikilink1" title="tag:tool" rel="tag">tool</a>
</span></div>

</div>
<!-- EDIT12 SECTION "More Info" [11277-] -->
