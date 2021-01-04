---
title: "Step 9: Handle activity conversion update events"
description: 5
---

When detecting an activity conversion trigger event, the system broadcasts a notification to the user using `PendingIntent`.

1. In `ActivityIdentificationHelper.kt`, in `fromActivityConversionToString()` function, return conversion type as `String`.

   <pre><div id="copy-button37" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 9.1:
   return when (conversionType) {
       ActivityConversionInfo.ENTER_ACTIVITY_CONVERSION -> "start"
       ActivityConversionInfo.EXIT_ACTIVITY_CONVERSION -> "stop"
       else -> "Unknown"
   }
   <span class="pln">
   </span></code></pre>

2. In `LocationBroadcastReceiver.kt`, override `onReceive()` method and use **when** statement to run related code block, if the action name of an intent matches triggered action. To get action name which set before when you created `PendingIntent`, use `getActivityConversionAction()` function. Copy the code below, and paste into the statement code block. Obtain `ActivityConversionResponse` object from the intent. Then, use it to obtain `activityConversionData` calling `activityConversionDatas` method. Get activity type as `String` using `fromActivityConversionToString()`. Pass the value to `createUserActivity()` method using `UserActivityRepositoryImpl`.

   <pre><div id="copy-button38" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 9.2:
   val conversionResponse = ActivityConversionResponse.getDataFromIntent(intent)
   conversionResponse?.let {
       conversionResponse.activityConversionDatas.forEach {
           Log.i(
               TAG,
               "${fromActivityConversionToString(it.conversionType)} ${fromActivityToString(it.activityType)}"
           )
           UserActivityRepositoryImpl.createUserActivity(it)
       }
   }
   <span class="pln">
   </span></code></pre>