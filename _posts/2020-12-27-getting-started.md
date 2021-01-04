---
title: Getting started
description: 5
---

To get started, clone the GitHub repository of the codelab and switch to the start branch.

<pre><div id="copy-button1" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>$git clone https://github.com/huaweicodelabs/LocationKit/tree/master/activity-identification-and-geofence
<span class="pln">
</span></code></pre>
You’ll be using the start branch, which is the starting point for the codelab. On master branch, you can check your work, or reference if you face any issues.

## **Creating a Project**

**Step 1:** Start Android Studio.

**Step 2:** Choose **File** \> **Open**, go to the directory where the sample project is decompressed, and click **OK**.

**Step 3:** Configure the AppGallery Connect plug-in, Maven repository address, build dependencies, obfuscation scripts, and permissions.

<aside class="special">
	<p><strong>Note:</strong> These items have been configured in the sample code. If any of them
does not meet your requirements, change it in your own project.</p>
</aside>


**1. Configure the Maven repository address and AppGallery Connect plug-in in the project's build.gradle file.**

- Go to **allprojects** \> **repositories** and configure the Maven repository address for the HMS Core SDK.

  <pre><div id="copy-button1" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">allprojects </span><span class="pun">{</span><span class="pln">
  		repositories </span><span class="pun">{</span><span class="pln">
  			maven </span><span class="pun">{</span><span class="pln"> url </span><span class="str">'https://developer.huawei.com/repo/'</span><span class="pln"> </span><span class="pun">}</span><span class="pln">
  			</span><span class="pun">...</span><span class="pln">
  		</span><span class="pun">}</span><span class="pln">
  	</span><span class="pun">}</span><span class="pln">
  	</span></code></pre>

- Go to **buildscript** \> **repositories** and configure the Maven repository address for the HMS Core SDK.

  <pre><div id="copy-button2" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">buildscript </span><span class="pun">{</span><span class="pln">
  		repositories </span><span class="pun">{</span><span class="pln">
  		   maven </span><span class="pun">{</span><span class="pln">url </span><span class="str">'https://developer.huawei.com/repo/'</span><span class="pun">}</span><span class="pln">
  			</span><span class="pun">...</span><span class="pln">
  		</span><span class="pun">}</span><span class="pln">
  		</span><span class="pun">...</span><span class="pln">
  	</span><span class="pun">}</span><span class="pln">
  </span></code></pre>

- Go to **buildscript** \> **dependencies** and add build dependencies.

  <pre><div id="copy-button3" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">buildscript </span><span class="pun">{</span><span class="pln">
  		dependencies </span><span class="pun">{</span><span class="pln">
       </span><span class="str">                   //Replace {agconnect_version} with the actual AGC plugin version number.</span><span class="pln">
       </span><span class="str">                   //Example: classpath 'com.huawei.agconnect:agcp: 1.4.1.300'</span><span class="pln">
  			classpath </span><span class="str">'com.huawei.agconnect:agcp:{agconnect_version}'</span><span class="pln">
  		</span><span class="pun">}</span><span class="pln">
  	</span><span class="pun">}</span><span class="pln">
  	</span></code></pre>

**2. Configure the dependency package in the app's build.gradle file.**

- Add a dependency package to the **dependencies** section in the **build.gradle** file.

  <pre><div id="copy-button4" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">dependencies </span><span class="pun">{</span><span class="pln">
  		</span><span class="pun">...</span><span class="pln">
      </span><span class="str">		//Location Kit</span><span class="pln">
  		implementation </span><span class="str">'com.huawei.hms:location:5.0.4.300'</span><span class="pln">
  		</span><span class="pun">...</span><span class="pln">
  	</span><span class="pun">}</span><span class="pln">
  	</span></code></pre>


  Please, refer to [latest version](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/version-change-history-0000001050986155) for Location Kit.

- Add the following information under **apply plugin: 'com.android.application'** in the file header:

  <pre><div id="copy-button5" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">apply plugin</span><span class="pun">:</span><span class="pln"> </span><span class="str">'com.huawei.agconnect'</span><span class="pln">
  	</span></code></pre>

**3. Configure obfuscation scripts.**

- Configure the following information in the **app/proguard-rules.pro** file:

  <pre><div id="copy-button6" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pun">-</span><span class="pln">ignorewarnings</span><span class="pln">
  </span><span class="pun">-</span><span class="pln">keepattributes </span><span class="pun">*</span><span class="typ">Annotation</span><span class="pun">*</span><span class="pln">
  </span><span class="pun">-</span><span class="pln">keepattributes </span><span class="typ">Exceptions</span><span class="pln">
  </span><span class="pun">-</span><span class="pln">keepattributes </span><span class="typ">InnerClasses</span><span class="pln">
  </span><span class="pun">-</span><span class="pln">keepattributes </span><span class="typ">Signature</span><span class="pln">
  </span><span class="pun">-</span><span class="pln">keepattributes </span><span class="typ">SourceFile</span><span class="pun">,</span><span class="typ">LineNumberTable</span><span class="pln">
  </span><span class="pun">-</span><span class="pln">keep </span><span class="kwd">class</span><span class="pln"> com</span><span class="pun">.</span><span class="pln">hianalytics</span><span class="pun">.</span><span class="pln">android</span><span class="pun">.**{*;}</span><span class="pln">
  </span><span class="pun">-</span><span class="pln">keep </span><span class="kwd">class</span><span class="pln"> com</span><span class="pun">.</span><span class="pln">huawei</span><span class="pun">.</span><span class="pln">updatesdk</span><span class="pun">.**{*;}</span><span class="pln">
  </span><span class="pun">-</span><span class="pln">keep </span><span class="kwd">class</span><span class="pln"> com</span><span class="pun">.</span><span class="pln">huawei</span><span class="pun">.</span><span class="pln">hms</span><span class="pun">.**{*;}</span><span class="pln">
  	</span></code></pre>

- If you are using AndResGuard, add it to the allowlist in the obfuscation script file.

  <pre><div id="copy-button7" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
  <span class="str">"R.string.hms*"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.string.connect_server_fail_prompt_toast"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.string.getting_message_fail_prompt_toast"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.string.no_available_network_prompt_toast"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.string.third_app_*"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.string.upsdk_*"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.layout.hms*"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.layout.upsdk_*"</span><span class="pun">,</span><span class="pln"> 
  </span><span class="str">"R.drawable.upsdk*"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.color.upsdk*"</span><span class="pun">,</span><span class="pln"> 
  </span><span class="str">"R.dimen.upsdk*"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.style.upsdk*"</span><span class="pun">,</span><span class="pln">
  </span><span class="str">"R.string.agc*"</span><span class="pln">
  	</span></code></pre>

**Step 4**: In the Android Studio window, choose **File** \> **Sync Project with Gradle Files** to synchronize the project.



Now, you’re set up, and ready to implement geofence and activity identification services. 