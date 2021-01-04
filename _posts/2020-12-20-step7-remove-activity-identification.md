---
title: "Step 7: Remove activity identification"
description: 3
---

When you no longer need to receive activity identification, you can remove it through `PendingIntent`.

1. In `MainFragment.kt`, in `removeActivityIdentification()` function, remove current activity identification through `activityIdentificationPendingIntent`.

   <pre><div id="copy-button31" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//TODO 7.1:
   activityIdentificationService.deleteActivityIdentificationUpdates(
       activityIdentificationPendingIntent
   )
       ?.run {
           addOnSuccessListener {
               //Activity Identification removed successfully.
               Log.i(TAG, "Activity Identification has been stopped.")
           }
           addOnFailureListener {
               //Activity Identification remove process failed.
               Log.i(TAG, "Failed to stop Activity Identification.")
           }
       }
   <span class="pln">
   </span></code></pre>

