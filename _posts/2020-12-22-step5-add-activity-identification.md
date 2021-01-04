---
title: "Step 5: Add activity identification"
description: 15
---

**Create pending intent**

You will create a `PendingIntent` in order to dynamically register to `BroadcastReceiver` through it.

1. In `MainFragment.kt`, above the `onViewCreated()` method, create a private type of `PendingIntent` variable which named `activityIdentificationPendingIntent` with lazy initialization. `getActivityIdentificationAction()` returns action name as `String`, and `getActivityIdentificationRequestCode()` returns request code as `Integer`. Both are implemented in `ActivityIdentificationHelper.kt`.

   
   <pre><div id="copy-button25" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 5.1:
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

   <pre><div id="copy-button26" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 5.2:
   private lateinit var activityIdentificationService: ActivityIdentificationService
   <span class="pln">
   </span></code></pre>

2. In `MainFragment.kt`, in the `onViewCreated()` method, initialize `activityIdentificationService` which is already declared above.

   <pre><div id="copy-button27" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 5.3:
   activityIdentificationService = ActivityIdentification.getService(context)
   <span class="pln">
   </span></code></pre>

**Start activity identification**

You will start activity identification if activity recognition permission has been granted before.

1. In `MainFragment.kt`, in `startActivityIdentification()` function, use `activityIdentificationService` to add activity identification. First, check the activity recognition permission calling `hasActivityRecognitionPermission()` function as an **if** condition. If the permission has not been granted before, the function will ask it. Then, add new activity identification by passing interval parameter in milliseconds as `Long`, and `activityIdentificationPendingIntent` to `createActivityIdentificationUpdates()` method. Copy the code below into the **if** statement.

<pre><div id="copy-button28" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 5.4:
activityIdentificationService.createActivityIdentificationUpdates(
    5000,
    activityIdentificationPendingIntent
)?.run {
    addOnSuccessListener {
        Log.i(TAG, "Activity Identification has been started.")
    }
    addOnFailureListener {
        Log.e(TAG, "Failed to start Activity Conversion updates.")
    }
}
<span class="pln">
</span></code></pre>