---
title: "Step 3: Handle geofence transition events"
description: 5
---

When detecting a geofence trigger event, the system broadcasts a notification to the user using `PendingIntent`.

1. In `GeofenceHelper.kt`, in `fromGeofenceTransitionToString()` function, return transition type as `String`.

   <pre><div id="copy-button21" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 3.1:
   return when (transitionType) {
       Geofence.ENTER_GEOFENCE_CONVERSION -> "You just got in the area!"
       else -> "UNKNOWN"
   }
   <span class="pln">
   </span></code></pre>
   
2. In `LocationBroadcastReceiver.kt`, override `onReceive()` method and use `when` statement to run related code block, if the action name of an intent matches triggered action. To get action name which set before when you created `PendingIntent`, use `getGeofenceAction()` function. Copy the code below, and paste into the statement code block. Then, obtain `GeofenceData` object from the intent. Get transition type as String using `fromGeofenceTransitionToString()` and inform user with `Toast`. Next, get `Geofence` using `convertingGeofenceList`. Last, apply `Landmark` repository functions using geofence’s `uniqueId`.

   <pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 3.2:
   val geofenceData = GeofenceData.getDataFromIntent(intent)
   geofenceData.let { it ->
       val info = fromGeofenceTransitionToString(geofenceData.conversion)
       val toast = Toast.makeText(context, info, Toast.LENGTH_LONG)
       toast.setGravity(Gravity.CENTER, 0, 0)
       toast.show()
       it.convertingGeofenceList.forEach {
           LandmarkRepositoryImpl.removeMarker(it.uniqueId)
           LandmarkRepositoryImpl.removeCircle(it.uniqueId)
           LandmarkRepositoryImpl.deleteLandmark(it.uniqueId)
       }
   }
   <span class="pln">
   </span></code></pre>
