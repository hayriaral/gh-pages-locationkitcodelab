---
title: "Step 5: Create and add activity identification"
description: 15
---

**Create pending intent**

You will create a PendingIntent in order to dynamically register to BroadcastReceiver through it.

1. In `MainFragment.kt`, above the `onViewCreated()` method, create a private type of `PendingIntent` variable which named `activityIdentificationPendingIntent` with lazy initialization. `getActivityIdentificationAction()` returns action name as `String`, and `getActivityIdentificationRequestCode()` returns request code as `Integer`. Both are implemented in `ActivityIdentificationHelper.kt`.

   <pre><div id="copy-button18" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 5.1:
   private val activityIdentificationPendingIntent: PendingIntent by lazy {
       val intent = Intent(context, LocationBroadcastReceiver::class.java)
       //Set an action for activity identification's intent.
       intent.action = getActivityIdentificationAction()
       PendingIntent.getBroadcast(
           context,
           getActivityIdentificationRequestCode(),
           intent,
           PendingIntent.FLAG_UPDATE_CURRENT
       )
   }
   <span class="pln">
   </span></code></pre>

**Create activity identification service**

You will create an activity identification service client to call activity identification-related APIs.

1. In `MainFragment.kt`, above the `onViewCreated()` method, declare a private type of `ActivityIdentificationService` variable which named `activityIdentificationService`.

   <pre><div id="copy-button19" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 5.2:
   private lateinit var activityIdentificationService: ActivityIdentificationService
   <span class="pln">
   </span></code></pre>

2. In `MainFragment.kt`, in the `onViewCreated()` method, initialize `activityIdentificationService` which is already declared above.

   <pre><div id="copy-button20" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 5.3:
   activityIdentificationService = ActivityIdentification.getService(context)
   <span class="pln">
   </span></code></pre>



