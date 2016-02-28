---
title: Changing the Name of Your APK/Application:
---
<h3 class="sectionedit1" id="changing_the_name_of_your_apk_application">Changing the Name of Your APK/Application:</h3>
<div class="level3">

<p>
1. Open your project’s properties and navigate to Application<br />

2. Update the title<br />

</p>

<p>
This has no real effect, however it keeps continuity throughout your app. Actually, this likely renamed the window created to display your app. So, now go change the actual name of your APK:
</p>

<p>
1. Select File View in the left pane of the SDK<br />

2. Navigate to the mobile/res/values directory and open the strings.xml file<br />

3. There should be a string tag with the following key pair: name=”app_name”<br />

4. Replace MyGame with your app’s name and save the file.<br />

5. In File view, navigate to nbproject and open the project.properties file<br />

6. Edit the value of application.title to reflect your game’s name (unless step 1/2 above altered this for you)<br />

</p>

</div>
<!-- EDIT1 SECTION "Changing the Name of Your APK/Application:" [1-802] -->
<h3 class="sectionedit2" id="changing_the_apk_icon">Changing the APK Icon:</h3>
<div class="level3">

<p>
1. Under the File view of your project navigate to mobile/res and add a “drawable” folder if one does not exist.<br />

2. Add you icon file (png)<br />

3. Open the Android Manifest file and add the following to your application tag: android:icon=”@drawable/&lt;ICON FILE NAME WITHOUT EXTENSION&gt;”<br />

4. If you would like multiple size icons, add the following folders:<br />

</p>
<pre class="code">drawable-hdpi (should contain the icon named the same at 72×72 pixels)\\
drawable-ldpi (should contain the icon named the same at 36×36 pixels)\\
drawable-mdpi (should contain the icon named the same at 48×48 pixels)\\
drawable-xhdpi (should contain the icon named the same at 96×96 pixels)\\</pre>

</div>
<!-- EDIT2 SECTION "Changing the APK Icon:" [803-1506] -->
<h3 class="sectionedit3" id="adding_a_splash_screen_to_your_app">Adding a Splash Screen to your app:</h3>
<div class="level3">

<p>
1. Open Android Main Activity, ether through the Important Files list in Project view or in the File view under mobile/src/&lt;package name&gt;/ directory<br />

2. Add the following line to the MainActivity method:<br />

</p>

<p>
splashPicID = R.drawable.&lt;IMAGE NAME WITHOUT EXTENSION&gt;;
</p>

<p>
3. Add the image the the mobile/res/drawable directory
</p>

<p>
Compiling Google Play Services and Adding it to Your Project:
</p>

<p>
First get the api:
</p>

<p>
1. Download the google play services add-on through the SDK Manager under Extras (named Google Play services)<br />

2. Copy the directory from where you downloaded it to another location (like JME Projects Folder)<br />

</p>

</div>
<!-- EDIT3 SECTION "Adding a Splash Screen to your app:" [1507-2169] -->
<h3 class="sectionedit4" id="compile_the_jar_file_for_use_with_your_project">Compile the jar file for use with your project:</h3>
<div class="level3">

<p>
1. In the directory you copied, there is an android project file.<br />

2. In JME’s IDE, open this project<br />

3. In the General section of the project properties, there is a list of potential Android target platforms. Select the one you are using for your project by clicking on the list (this is not intuitive at all, as the list looks like nothing more than info… not selectable items)<br />

4. Under the Library section, click the checkbox that is labeled: Is Library<br />

5. Click Ok and then Clean &amp; Build this project.<br />

</p>

<p>
This will compile the play services all proper like so you can add it to your project. Now, for that step:
</p>

<p>
1. Open your project’s properties.<br />

2. In the Libraries section, click the “Add JAR/folder” button.<br />

3. Find and add the jar you compiled above (This can be found in: &lt;COPIED DIR&gt;\libproject\google-play-services_lib\libs\google-play-services.jar<br />

4. Modify your Android Manifest by adding the following tags under application:<br />

&lt;meta-data android:name=”com.google.android.gms.games.APP_ID”
android:value=”@string/app_id” /&gt;
&lt;meta-data android:name=”com.google.android.gms.version”
android:value=”@integer/google_play_services_version”/&gt;
5. Add the following tag to your mobile/res/values/integers.xml file (create it if it doesn’t exist):<br />

&lt;integer name=”google_play_services_version”&gt;4323000&lt;/integer&gt;
6. Clean &amp; Build your project<br />

</p>

</div>
<!-- EDIT4 SECTION "Compile the jar file for use with your project:" [2170-3623] -->
<h3 class="sectionedit5" id="adding_play_games_services_to_your_project">Adding Play Games Services to Your Project:</h3>
<div class="level3">

<p>
1. Download the project from: <a href="https://github.com/playgameservices/android-samples" class="urlextern" title="https://github.com/playgameservices/android-samples" rel="nofollow">https://github.com/playgameservices/android-samples</a><br />

2. In the following directory, you find java files you will need to add to your project:<br />

</p>
<pre class="code">&lt;DOWNLOAD DIR&gt;\android-samples-master\BasicSamples\libraries\BaseGameUtils\src\main\java\com\google\example\games\basegameutils\\
Grab GameHelper.java and GameHelperUtil.java and add them to the directory you projects Main Activity is in\\</pre>

<p>
3. In the following directoriy, you find a resource file you will need to add to your project:<br />

</p>
<pre class="code">&lt;DOWNLOAD DIR&gt;\android-samples-master\BasicSamples\libraries\BaseGameUtils\src\main\res\values\\
Grab the gamehelper_strings.xml into your mobile/res/values folder\\</pre>

<p>
4. Add the following jar from the Adroid SDK folder to your project as a library:<br />

</p>
<pre class="code">&lt;ANDROID SDK INSTALL DIR&gt;\adt-bundle-windows-x86_64-20131030\sdk\extras\android\support\v4\android-support-v4.jar\\</pre>

<p>
And this is the basics for setting this up.
</p>

</div>
<!-- EDIT5 SECTION "Adding Play Games Services to Your Project:" [3624-4610] -->
<h3 class="sectionedit6" id="adding_admob_support_to_your_project">Adding AdMob Support to Your Project:</h3>
<div class="level3">

<p>
1. Open your Android Manifest and add the following tag update the application tag:<br />

&lt;activity android:name=”com.google.android.gms.ads.AdActivity” android:configChanges=”keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize”/&gt;<br />

2. After the application tag, add the following tags:
&lt;uses-permission android:name=”android.permission.INTERNET”/&gt;<br />

&lt;uses-permission android:name=”android.permission.ACCESS_NETWORK_STATE”/&gt;<br />

3. In the onCreate method of your Main Activity, add the following snippet (configure however you like):<br />

</p>
<pre class="code">      adView = new AdView(this);
      adView.setAdSize(AdSize.FULL_BANNER);
      adView.setAdUnitId(“&lt;WHATEVER AD UNIT ID YOU ARE ASSIGNED THROUGH THE GOOGLE DEV CONSOLE&gt;”);
      adView.buildLayer(); 
      LinearLayout ll = new LinearLayout(this);
      ll.setGravity(Gravity.BOTTOM);
      ll.addView(adView);
      addContentView(ll, new ViewGroup.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));</pre>

</div>
<!-- EDIT6 SECTION "Adding AdMob Support to Your Project:" [4611-5704] -->
<h3 class="sectionedit7" id="communication_between_your_application_main_activity">Communication Between your Application &amp; Main Activity:</h3>
<div class="level3">

<p>
1. Create an interface named something along the lines of JmeToHarness.java
2. Open your Android Main Activity and implement this interface.
3. In Main.java of your Application, add the following:
</p>
<pre class="code"> JmeToHarness harness; 
 public JmeToHarness getHarness() {
   return this.harness;
 } 
 public void setHarnessListener(JmeToHarness harness) {
    this.harness = harness;
 }
 </pre>

<p>
4. Add the following snippet to the onCreate method of your Android Main Activity:
</p>
<pre class="code">if (app != null)
    ((Main)app).setHarnessListener(this);
    </pre>

<p>
5. Add error handling if you want it.
</p>

<p>
This bit is ultra useful for calling AdMob changes and Play Games methods (like updating achievements, leader boards, etc, etc)
</p>

<p>
EDIT: Keep this as generic as you possibly can as it should plug &amp; play with iOS &amp; Applets if you keep that in mind. Google Play Services/Play Games Services works for all of the above… soooo… anyways.
</p>

</div>
<!-- EDIT7 SECTION "Communication Between your Application & Main Activity:" [5705-6691] -->
<h3 class="sectionedit8" id="changing_the_package_name_after_project_creation">Changing the Package Name After Project Creation:</h3>
<div class="level3">

<p>
1. Open the project properties of your Application
2. Navigate to Application &gt; Android and edit the package name.
</p>

<p>
This does absolutely nothing, but help with consistency.
</p>

<p>
So, to actually change the package name, you will want to:
</p>

<p>
1. Open the Android Manifest
2. Edit the manifest tag key pair: package=”&lt;THE NEW PACKAGE NAME&gt;”
3. In File view, navigate to nbproject and open the project.properties file
4. Edit the value of mobile.android.package
</p>

<p>
Take a moment or 4 to navigate through the directory structure in file view and remove any artifacts left from the previous package name build. Alternately, you can run Clean on the project prior to updating the package name.
</p>

</div>
<!-- EDIT8 SECTION "Changing the Package Name After Project Creation:" [6692-] -->
