---
title: "Step 4: Remove geofence"
description: 3
---

When you no longer need a geofence, you can remove it by geofence’s uniqueId or through `PendingIntent`.

1. In `MainFragment.kt`, in `removeGeofence()` function, remove current geofence through `geofencePendingIntent`.

   <pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 4.1:
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
   
   

