---
title: Step 1: Check library and receiver and assign permissions
description: 3
---

To use activity identification and geofence in your app, you must implement the **Huawei Location Kit** library to the dependencies, and specify related permissions in the app manifest.

1. Check HMS library required for activity identification and geofence in the **build.gradle** file, in app directory. There is no action needed for the step, just check the dependency.

<pre>
<div id="copy-button2" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div>
<code>implementation 'com.huawei.hms:location:5.0.4.300'
<cite class="pln"></cite></code>
</pre>

2. Check **receiver** tag in the **AndroidManifest.xml** file, in **application** tag. There is no action needed for the step, just check the receiver.

<pre>
<div id="copy-button3" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div>
<code><span class="tag">&lt;receiver</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">".util.LocationBroadcastReceiver"</span><span class="tag">/&gt;</span><span class="pln"></span><cite class="pln"></cite></code>
</pre>

3. Specify **android.permission.ACCESS_FINE_LOCATION,** **android.permission.ACCESS_COARSE_LOCATION** and **android.permission.ACCESS_BACKGROUND_LOCATION** permissions in the **AndroidManifest.xml** file to use geofence service.

<pre>
<div id="copy-button4" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div>
<code><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACCESS_FINE_LOCATION"</span><span class="tag">/&gt;</span><span class="pln"></span>
<span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACCESS_COARSE_LOCATION"</span><span class="tag">/&gt;</span><span class="pln">
<span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACCESS_BACKGROUND_LOCATION"</span><span class="tag">/&gt;</span><span class="pln">
<cite class="pln"></cite></code>
</pre>

4. Specify **com.huawei.hms.permission.ACTIVITY_RECOGNITION** and **android.permission.ACTIVITY_RECOGNITION** permissions in the **AndroidManifest.xml** file to use activity identification service.

<pre>
<div id="copy-button5" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div>
<code><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACTIVITY_RECOGNITION"</span><span class="tag">/&gt;</span><span class="pln"></span>
<span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"com.huawei.hms.permission.ACTIVITY_RECOGNITION"</span><span class="tag">/&gt;</span><span class="pln">
<cite class="pln"></cite></code>
</pre>
<aside class="special">
	<p><strong>Note:</strong> <strong>android.permission.ACCESS_BACKGROUND_LOCATION</strong> and <strong>android.permission.ACTIVITY_RECOGNITION</strong> permissions required for the runtime permissions which were added in Android Q.</p>
</aside>


Your app can now support activity identification and geofence, you just need to add the code step by step.

