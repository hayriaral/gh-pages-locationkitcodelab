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


<table style="padding:5px" border="2" >
    <td style="background-color:#d9ead3"><b>Note:</b> <b>android.permission.ACCESS_BACKGROUND_LOCATION</b> and <b>android.permission.ACTIVITY_RECOGNITION</b> permissions required for the runtime permissions which were added in Android Q.</td>
</table>



Your app can now support activity identification and geofence, you just need to add the code step by step.

**1. Locate following lireceivne to create the Wise Player Factory instance in
WisePlayerInit Object.**

<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    //TODO Initializing of Wise Player Factory
<cite class="pln">
</cite></code></pre>
**2. Create the Wise Player Factory instance**

<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    val factoryOptions = WisePlayerFactoryOptions.Builder().setDeviceId("xxx").build()
    // In the multi-process scenario, the onCreate method in Application is called multiple times.
    // The app needs to call the WisePlayerFactory.initFactory() API in the onCreate method of the app process (named "app package name") 
    // and WisePlayer process (named "app package name:player").
    WisePlayerFactory.initFactory(context, factoryOptions, object : InitFactoryCallback {
        override fun onSuccess(factory: WisePlayerFactory) {
            wisePlayerFactory = factory
        }
        override fun onFailure(errorCode: Int, msg: String) {
            Log.d("WisePlayerInit", "onFailure: $errorCode - $msg")
        }
    })
<span class="pln">
</span></code></pre>

​        


<p>Description of <strong>Wise Player Factory</strong> is as following:<br></p>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
	<tr><td colspan="1" rowspan="1"><p>Parameter</p>
	</td><td colspan="1" rowspan="1"><p>Type:</p>
	</td><td colspan="1" rowspan="1"><p>Mandatory or Not</p>
	</td><td colspan="1" rowspan="1"><p>Description</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>context</p>
	</td><td colspan="1" rowspan="1"><p>Context</p>
	</td><td colspan="1" rowspan="1"><p>M</p>
	</td><td colspan="1" rowspan="1"><p>Android context object, which is not set to null.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>options</p>
	</td><td colspan="1" rowspan="1"><p>Integer</p>
	</td><td colspan="1" rowspan="1"><p>M</p>
	</td><td colspan="1" rowspan="1"><p>Instance of the WisePlayer factory class initialization option <a href="https://developer.huawei.com/consumer/en/doc/HMSCore-References-V5/wpf-options-0000001050439397-V5" target="_blank">WisePlayerFactoryOptions</a></p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>callback</p>
	</td><td colspan="1" rowspan="1"><p>Object</p>
	</td><td colspan="1" rowspan="1"><p>M</p>
	</td><td colspan="1" rowspan="1"><p>Instance of the <a href="https://developer.huawei.com/consumer/en/doc/HMSCore-References-V5/init-factory-callback-0000001050199187-V5" target="_blank">InitFactoryCallback API</a> for initializing the WisePlayer factory class.</p>
	</td></tr>
</tbody></table>
**3. Locate following line and set the EditTexts Urls in MainActivity to
play related buttons**

<pre><div id="copy-button12" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>   // TODO Set video Url or Urls
<span class="pln">
</span></code></pre>

**4.Set the EditTexts Urls**

<pre><div id="copy-button13" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code> edtUrl.setText(resources.getString(R.string.single_url))
 edtMultipleUrl.setText(resources.getString(R.string.multiple_url))
 <span class="pln"></span></code></pre>

**5. Locate following line and create Wise Player Instance in
WisePlayerInit Object.**

<pre><div id="copy-button14" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  // TODO Initializing of Wise Player Instance
<span class="pln">
</span></code></pre>

**6. Create Wise Player Instance**

<pre><div id="copy-button15" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  return wisePlayerFactory.createWisePlayer()
<span class="pln">
</span></code></pre>

**Note: Frame Layout is necessary for SurfaceView to display videos,
otherwise only audio will be listened**

<br><img style="width: 400.00px" src="https://raw.githubusercontent.com/bekiryavuzkoc/testRepo/gh-pages/assets/framelayout.PNG" onclick="imageclick(src)">

**7. Locate following line in Play Activity.**

<pre><div id="copy-button17" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Setting the Listeners
<span class="pln">
</span></code></pre>

**8. Set listeners in Play Activity.**

<pre><div id="copy-button18" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setReadyListener(this)
  player.setErrorListener(this)
  player.setEventListener(this)
  player.setResolutionUpdatedListener(this)
  player.setLoadingListener(this)
  player.setPlayEndListener(this)
  player.setSeekEndListener(this)
  <span class="pln">
</span></code></pre>

**9. Locate following line in Play Activity.**

<pre><div id="copy-button19" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code> //TODO Callback Listener
<span class="pln">
</span></code></pre>

**10. Set the Callback Listener in Play Activity.**

<pre><div id="copy-button20" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  surfaceView.holder.addCallback(this)
<span class="pln">
</span></code></pre>

**11. Locate following line in Play Activity.**

<pre><div id="copy-button21" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code> //TODO Callback Listener
<span class="pln">
</span></code></pre>

**12. Set the Seekbar Listener in Play Activity.**

<pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  seekBar.setOnSeekBarChangeListener(this)
<span class="pln">
</span></code></pre>

**13. Locate following line in Play Activity.**

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Starting the Player
	<span class="pln">
</span></code></pre>

**14. Start Wise Player in Play Activity.**

<pre><div id="copy-button24" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player?.start()
<span class="pln">
</span></code></pre>

**15. Locate following line in Play Activity.**

<pre><div id="copy-button25" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Change
<span class="pln">
</span></code></pre>

**16. Set surface change to Wise Player.**

<pre><div id="copy-button26" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setSurfaceChange()
<span class="pln">
</span></code></pre>

**17. Locate following line in Play Activity.**

<pre><div id="copy-button27" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Destroy
<span class="pln">
</span></code></pre>

**18. Suspend the Wise Player if surface is destroyed.**

<pre><div id="copy-button28" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.suspend()
<span class="pln">
</span></code></pre>

**19. Locate following line in Play Activity.**

<pre><div id="copy-button29" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Create
<span class="pln">
</span></code></pre>

**20. Resume Wise Player with the current time when app is sent to
foreground.**

<pre><div id="copy-button30" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setView(surfaceView)
  player.resume(PlayerConstants.ResumeType.KEEP)
<span class="pln">
</span></code></pre>

**21. Locate following line in Play Activity.**

<pre><div id="copy-button31" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Release Wise Player
<span class="pln">
</span></code></pre>

**22. Release Wise Player and listeners in Play Activity.**

<pre><div id="copy-button32" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setErrorListener(null)
  player.setEventListener(null)
  player.setResolutionUpdatedListener(null)
  player.setReadyListener(null)
  player.setLoadingListener(null)
  player.setPlayEndListener(null)
  player.setSeekEndListener(null)
  player.release()
<span class="pln">
</span></code></pre>



