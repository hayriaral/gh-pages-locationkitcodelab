---
title: "Step 8: Add activity conversion"
description: 15
---

**Create pending intent**

You will create a `PendingIntent` in order to dynamically register to `BroadcastReceiver` through it.

1. In `MainFragment.kt`, above the `onViewCreated()` method, create a private type of `PendingIntent` variable which named `activityConversionPendingIntent` with lazy initialization. `getActivityConversionAction()` returns action name as `String`, and `getActivityConversionRequestCode()` returns request code as `Integer`. Both are implemented in `ActivityIdentificationHelper.kt`.

   <pre><div id="copy-button33" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 8.1:
   private val activityConversionPendingIntent: PendingIntent by lazy {
       val intent = Intent(context, LocationBroadcastReceiver::class.java)
       //Set an action for activity conversion's intent.
       intent.action = getActivityConversionUpdatesAction()
       PendingIntent.getBroadcast(
           context,
           getActivityConversionRequestCode(),
           intent,
           PendingIntent.FLAG_UPDATE_CURRENT
       )
   }
   <span class="pln">
   </span></code></pre>

**Build activity conversion and create an activity conversion request**

You will build an activity conversion information object and create an activity conversion request in order to listen activity conversions.

1. In `MainFragment.kt`, in the `buildActivityConversion()` function, build an activity conversion using `ActivityConversionInfo.Builder()`. Set the followings: 

   - An activity type.
   - A conversion type.

   Finally, return the activity conversion info.

   <pre><div id="copy-button34" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 8.2:
   return ActivityConversionInfo.Builder()
       .setActivityType(activityType)
       .setConversionType(conversionType)
       .build()
   <span class="pln">
   </span></code></pre>

2. In `MainFragment.kt`, in the `createActivityConversionRequest()` function, add activity conversion information objects into a list. Finally, pass the list as a parameter to `ActivityConversionRequest()` and return the object.

   <pre><div id="copy-button35" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 8.3:
   val activityConversions: MutableList&lsaquo;ActivityConversionInfo&rsaquo; = ArrayList()
   activityConversions.add(
       buildActivityConversion(
           ActivityIdentificationData.STILL,
           ActivityConversionInfo.ENTER_ACTIVITY_CONVERSION
       )
   )
   activityConversions.add(
       buildActivityConversion(
           ActivityIdentificationData.WALKING,
           ActivityConversionInfo.ENTER_ACTIVITY_CONVERSION
       )
   )
   activityConversions.add(
       buildActivityConversion(
           ActivityIdentificationData.WALKING,
           ActivityConversionInfo.EXIT_ACTIVITY_CONVERSION
       )
   )
   activityConversions.add(
       buildActivityConversion(
           ActivityIdentificationData.VEHICLE,
           ActivityConversionInfo.ENTER_ACTIVITY_CONVERSION
       )
   )
   activityConversions.add(
       buildActivityConversion(
           ActivityIdentificationData.VEHICLE,
           ActivityConversionInfo.EXIT_ACTIVITY_CONVERSION
       )
   )
   activityConversions.add(
       buildActivityConversion(
           ActivityIdentificationData.RUNNING,
           ActivityConversionInfo.ENTER_ACTIVITY_CONVERSION
       )
   )
   activityConversions.add(
       buildActivityConversion(
           ActivityIdentificationData.RUNNING,
           ActivityConversionInfo.EXIT_ACTIVITY_CONVERSION
       )
   )
   return ActivityConversionRequest(activityConversions)
   <span class="pln">
   </span></code></pre>

**Start activity conversion**

You will start activity conversion if activity recognition permission has been granted before.

1. In `MainFragment.kt`, in `startActivityConversion()` function, use `activityIdentificationService` to add activity conversion. Add new activity conversion by passing `activityConversionPendingIntent`, and `createActivityConversionRequest()` functions to `createActivityConversionUpdates()` method.

   <pre><div id="copy-button36" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 8.4:
   activityIdentificationService.createActivityConversionUpdates(
       createActivityConversionRequest(),
       activityConversionPendingIntent
   )?.run {
       addOnSuccessListener {
           Log.i(TAG, "Activity Conversion updates has been started.")
       }
       addOnFailureListener {
           Log.i(TAG, "Failed to start Activity Conversion updates.")
       }
   }
   <span class="pln">
   </span></code></pre>