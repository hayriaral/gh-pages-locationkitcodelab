---
title: "Step 1: Configure permissions and set constants"
description: 3
---

To use activity identification and geofence in your app, you must implement the **Huawei Location Kit** library to the dependencies, and specify related permissions in the app manifest.

1. Specify **android.permission.ACCESS_FINE_LOCATION,** **android.permission.ACCESS_COARSE_LOCATION** and **android.permission.ACCESS_BACKGROUND_LOCATION** permissions in the **AndroidManifest.xml** file to use geofence service.

   <pre><div id="copy-button8" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACCESS_FINE_LOCATION"</span><span class="tag">/&gt;</span><span class="pln"></span>
   <span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACCESS_COARSE_LOCATION"</span><span class="tag">/&gt;</span><span class="pln">
   </span><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACCESS_BACKGROUND_LOCATION"</span><span class="tag">/&gt;</span>
   <span class="pln">
   </span></code></pre>

2. Specify **com.huawei.hms.permission.ACTIVITY_RECOGNITION** and **android.permission.ACTIVITY_RECOGNITION** permissions in the **AndroidManifest.xml** file to use activity identification service.

   <pre><div id="copy-button9" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACTIVITY_RECOGNITION"</span><span class="tag">/&gt;</span><span class="pln"></span>
   <span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"com.huawei.hms.permission.ACTIVITY_RECOGNITION"</span><span class="tag">/&gt;</span>
   <span class="pln">
   </span></code></pre>

   <aside class="special">
   	<p><strong>Note:</strong> <strong>android.permission.ACCESS_BACKGROUND_LOCATION</strong> and <strong>android.permission.ACTIVITY_RECOGNITION</strong> permissions required for the runtime permissions which were added in Android Q.</p>
   </aside>

3. Check **receiver** tag in the **AndroidManifest.xml** file, in **application** tag. There is no action needed for the step, just check the receiver.

   <pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="tag">&lt;receiver</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">".util.LocationBroadcastReceiver"</span><span class="tag">/&gt;</span>
   <span class="pln">
   </span></code></pre>

4. If you create your own project, you need to change some constant variables to use broadcast receiver and map capabilities. In **util** package, go `Constants.kt` class, set the package name and AppGallery Connect API key as yours.

   You can find the API key, in AppGallery console, in **Project setting** > **General information.**

   <div style="padding: 5px">
           <img style="padding: 5px" src="https://raw.githubusercontent.com/hayricaral/gh-pages-locationkitcodelab/main/assets/agc-api-key-img.PNG">
   </div>
   
   <pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 1.4:
           private const val PACKAGE_NAME = "YOUR PACKAGE NAME"
           internal const val AGC_API_KEY = "YOUR API KEY"
   <span class="pln">
   </span></code></pre>



