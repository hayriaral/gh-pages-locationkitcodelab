---
title: "Step 6: Handle activity identification update events"
description: 5
---

When detecting an activity identification trigger event, the system broadcasts a notification to the user using `PendingIntent`.

1. In `ActivityIdentificationHelper.kt`, in `fromActivityToString()` function, return activity type as `String`.

   <pre><div id="copy-button29" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 6.1:
   return when (activityType) {
       ActivityIdentificationData.STILL -> "standing"
       ActivityIdentificationData.WALKING -> "walking"
       ActivityIdentificationData.RUNNING -> "running"
       ActivityIdentificationData.VEHICLE -> "driving"
       else -> "Unknown"
   }
   <span class="pln">
   </span></code></pre>

2. In `LocationBroadcastReceiver.kt`, override `onReceive()` method and use **when** statement to run related code block, if the action name of an intent matches triggered action. To get action name which set before when you created `PendingIntent`, use `getActivityIdentificationAction(`) function. Copy the code below, and paste into the statement code block. Obtain `ActivityIdentificationResponse` object from the intent. Then, use it to obtain `activityIdentificationData` calling `activityIdentificationDatas` method. Get activity type as `String` using `fromActivityToString()`. If the possibility more than equal to 70% pass the value to `createUserActivity()` method using `UserActivityRepositoryImpl`.

   <pre><div id="copy-button30" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 6.2:
   val identificationResponse =
       ActivityIdentificationResponse.getDataFromIntent(intent)
   identificationResponse?.let {
       identificationResponse.activityIdentificationDatas.forEach {
           Log.i(
               TAG,
               "Activity: %${it.possibility} ${fromActivityToString(it.identificationActivity)}"
           )
           if (it.possibility >= 70 &amp;&amp; !fromActivityToString(it.identificationActivity).equals(
                   "Unknown",
                   true
               )
           ) {
               UserActivityRepositoryImpl.createUserActivity(it)
           }
       }
   }
   <span class="pln">
   </span></code></pre>