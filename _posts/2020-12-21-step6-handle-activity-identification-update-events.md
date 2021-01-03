---
title: "Step 6: Handle activity identification update events"
description: 5
---

When detecting an activity identification trigger event, the system broadcasts a notification to the user using `PendingIntent`.

1. In `MainFragment.kt`, in `removeGeofence()` function, remove current geofence through `geofencePendingIntent`.

   <pre><div id="copy-button17" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 4.1:
   geofenceService.deleteGeofenceList(geofencePendingIntent)?.run {
       addOnSuccessListener {
           //Geofence removed successfully.
           Log.i(TAG, "Geofence has been removed.")
       }
       addOnFailureListener {
           //Geofence remove process failed.
           Log.i(TAG, "Failed to remove Geofence.")
       }
   }
   <span class="pln">
   </span></code></pre>
   
   

