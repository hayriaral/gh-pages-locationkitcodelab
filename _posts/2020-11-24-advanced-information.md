---
title: Advanced Features
description: 5

---

1. ### Seekbar:

    With the feature of Seekbar, displayed video can be rewound or forwarded. With Wise Player's seek feature videos can be played from a specified time.

   **1. Locate following line in Play Activity.**

   <pre><div id="copy-button33" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Seekbar Change
   <span class="pln">
   </span></code></pre>

   **2. Implement the Wise Player’s seek method.**

   <pre><div id="copy-button34" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  seekBar?.progress?.let {player.seek(it)}
   <span class="pln">
   </span></code></pre>

   ### 2.Handler and Runnable:

   A Handler allows you to send and process Message and Runnable objects
   associated with a thread's MessageQueue. With the feature of Handler, we
   can update the UI elements for every 1 seconds.

   **1. Locate following line in Play Activity.**

   <pre><div id="copy-button35" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Handler and Runnable Implementation
   <span class="pln">
   </span></code></pre>
**2. Implement the Wise Player’s seek method.**
   
<pre><div id="copy-button36" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>        //Player UI
           configureControlView()
           //Text UI Elements 
           configureContentView()
           if (!mStopHandler) {
               mHandler.postDelayed(runnable, DELAY_SECOND)
           }
           <span class="pln">
   </span></code></pre>
   
